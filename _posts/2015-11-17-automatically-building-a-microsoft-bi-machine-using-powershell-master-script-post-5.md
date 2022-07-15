---
id: 2071
title: 'Automatically building a Microsoft BI machine using PowerShell – master script (post #5)'
date: '2015-11-17T14:30:38+01:00'
author: 'Jeroen ter Heerdt'
layout: post
guid: 'http://www.dutchdatadude.com/?p=2071'
permalink: /automatically-building-a-microsoft-bi-machine-using-powershell-master-script-post-5/
categories:
    - Azure
    - 'Business Intelligence'
    - SharePoint
    - 'SQL Server'
tags:
    - 'Power Pivot'
    - 'power view'
    - PowerShell
---

<em>This post is #5 in the series to automatically build a Microsoft BI machine using PowerShell – <a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-start-of-series/">see the start of series</a>.
</em>

In this series so far:

<a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-start-of-series/">Start of series – introduction and layout of subjects</a>
<a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-preparation-install-files-using-disk-post-2/">Post #2 – Preparation: install files using Azure disk</a>
<a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-preparation-install-files-using-azure-file-service-post-3/">Post #3 – Preparation: install files using Azure File Service</a>
<a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-preparation-logging-infrastructure-post-4/">Post #4 –Preparation: logging infrastructure</a>

Now that we have our preparation completed, it is time to present the master script. This script will be called by the user with parameters specifying what to install; also this script will call other scripts to install components and potentially reboot the machine and resume working. My master script is called 'SetupMSBIDemoMachine.ps1'. It has one master switch called -DoAllTasks, what does as it says. Also, it provides switches to just executed a part of the total install, such as just installing SQL Server by specifying –InstallSQLServer. Optionally, this script can do automatic reboots of the server and auto-resume working after the reboot; very useful when –DoAllTasks is specified.

A sample call that would complete the full install with a certain domainname and passphrase (for SharePoint) and also auto reboots the machine would look like this:
<pre class="lang:c# decode:true ">.\SetupMSBIDemoMachine -DoAllTasks -DomainName mydomain.local -passphrase pass@word1 -AutoReboot</pre>
Just running .\SetupMSBIDemoMachine -? returns the following info, which shows all the parameters available. The parameters map to the steps outline in the start of this series. Again, -DoAllTasks would mean just executing these steps in turn.
<pre class="lang:c# decode:true ">NAME
    C:\Users\jterh\OneDrive - Microsoft\Demo Machine\SetupMSBIDemoMachine.ps1
    
SYNOPSIS
    Installs and sets up a MSBI Demo Machine in a number of steps
    
    
SYNTAX
    C:\Users\jterh\OneDrive - Microsoft\Demo Machine\SetupMSBIDemoMachine.ps1 [-DisableIEESC] 
    [-SetupActiveDirectory] [[-DomainName] ] [-ConfigurePasswordPolicy] 
    [-InstallSystemCenterEndpointProtection] [-InstallSQLServer] [-InstallSharePoint] 
    [-InstallPowerPivot] [-ConfigurePowerPivot] [-ConfigurePowerPivotPart2] [[-passphrase] ] 
    [-DoAllTasks] [[-Password] &lt;String&gt;] [[-Step] &lt;String&gt;] [-AutoReboot] [&lt;CommonParameters&gt;]
    
    
DESCRIPTION
    

RELATED LINKS

REMARKS
    To see the examples, type: "get-help C:\Users\jterh\OneDrive - Microsoft\Demo 
    Machine\SetupMSBIDemoMachine.ps1 -examples".
    For more information, type: "get-help C:\Users\jterh\OneDrive - Microsoft\Demo 
    Machine\SetupMSBIDemoMachine.ps1 -detailed".
    For technical information, type: "get-help C:\Users\jterh\OneDrive - Microsoft\Demo 
    Machine\SetupMSBIDemoMachine.ps1 -full".
</pre>
&nbsp;

<strong>Part 1: Parameter binding
</strong>
<pre class="lang:c# decode:true">[CmdletBinding()]
Param(
[switch]$DisableIEESC,
[switch]$SetupActiveDirectory,
[string]$DomainName,
[switch]$ConfigurePasswordPolicy,
[switch]$InstallSystemCenterEndpointProtection,
[switch]$InstallSQLServer,
[switch]$InstallSharePoint,
[switch]$InstallPowerPivot,
[switch]$ConfigurePowerPivot,
[switch]$ConfigurePowerPivotPart2,
[string]$passphrase,
[switch]$DoAllTasks,
[string]$Password="pass@word1",
[string]$Step="1",
[switch]$AutoReboot=$false
)</pre>
This part of the script binds to the parameters and specifies defaults for the password to be used for service accounts and the internal $Step variable. Also, note that by default AutoReboot is disabled.

&nbsp;

<strong>Part 2: Imports
</strong>
<pre class="lang:c# decode:true "># -------------------------------------
# Imports
# -------------------------------------
$global:script = $myInvocation.MyCommand.Definition
$scriptPath = Split-Path -parent $global:script
. (Join-Path $scriptpath RestartAndResumeFunctions.ps1)
. (Join-Path $scriptpath DisableIEESC.ps1)
. (Join-Path $scriptPath Set-Restart-AndResume.ps1)
. (Join-Path $scriptPath SetupActiveDirectory.ps1)
. (Join-Path $scriptPath ConfigurePasswordPolicy.ps1)
. (Join-Path $scriptPath InstallSystemCenterEndpointProtection.ps1)
. (Join-Path $scriptPath CreateServiceAccount.ps1)
. (Join-Path $scriptPath InstallSQLServer.ps1)
. (Join-Path $scriptPath InstallSharePoint.ps1)
. (Join-Path $scriptPath InstallPowerPivot.ps1)
. (Join-Path $scriptPath ConfigurePowerPivot.ps1)</pre>
This part join-paths to make sure we have all the items we need; the script uses restart and resume functions as an include, these functions enable auto restart and resume of the tasks (available in RestartAndResumeFunctions.ps1). The other scripts included here are the scripts that actually do the work of installing and configuring services.

&nbsp;

<strong>Part 3: Parameter passing
</strong>
<pre class="lang:c# decode:true ">$global:DoAllTasks = $DoAllTasks
$global:AutoReboot = $AutoReboot
Set-Location $scriptPath

#get the passed parameters
$Myparameters = $myinvocation.BoundParameters
#remove step from the list
$Myparameters.Remove("Step")
#build parameter string
$global:line = ""
foreach ($key in $Myparameters.keys)
{
    $value = (get-variable $key).Value 
    #is this a switch
    if($value -eq $true) {
        $global:line+= " -"+$key
    }
    else
    {
        $global:line+=" -"+$key+" "+$value
    }
}</pre>
This part is used to pass parameters between the master script and downstream scripts, even after auto reboot.

&nbsp;

<strong>Part 4: Setting global variables
</strong>
<pre class="lang:c# decode:true ">#Set the hostname
$global:HostName = hostname
$global:HostNameFull = $HostName
$global:HostNameFull += ".cloudapp.net"
$global:httpHostName = "http://"
$global:httpHostName += $HostName
#Set current user name
$global:currentUserName = [System.Security.Principal.WindowsIdentity]::GetCurrent().Name;
#Path to SQL ISO
$global:pathToSQLISO = ".\Resources\SQLServer2014DeveloperEdition\en_sql_server_2014_developer_edition_x64_dvd_3940406.iso"
$global:pathToSQLISO = Resolve-Path $global:pathToSQLISO
#Path to SHarePoint ISO
$global:pathToSharePointISO = ".\Resources\SharePoint2013\en_sharepoint_server_2013_with_sp1_x64_dvd_3823428.iso"
$global:pathToSharePointISO = Resolve-Path $global:pathToSharePointISO
#Path to SharePoint Prerequisites
$global:SharePoint2013Path = ".\Resources\SharePoint2013"
$global:SharePoint2013Path = Resolve-Path $global:SharePoint2013Path
#Domain Vars
#$global:path = "CN=Managed Service Accounts,"
$global:path = "CN=Users,"
$global:root = [ADSI]''
$global:dn = $global:root.distinguishedName
$global:path += $global:dn
$global:domainpart = (gwmi Win32_NTDomain).DomainName
#SPFarm Account Name
$global:spAccount = "SPFarm"
</pre>
Here some items are set up, such as the hostname of the machine, the current user name, the paths to ISO files for SharePoint and SQL. Also, the account name for the SharePoint farm account is specified here.

&nbsp;

<strong>Part 5: the actual program
</strong>
<pre class="lang:c# decode:true ">#ACTUAL PROGRAM

#STEP 1 - Disable IE ESC
if ($DisableIEESC -or ($DoAllTasks -and (Should-Run-Step "1"))) {
    DisableIEESC
}
#Step 2 - Setup AD
if ($SetupActiveDirectory -or ($DoAllTasks -and (Should-Run-Step "2"))) {
    SetupActiveDirectory -DomainName $DomainName
}
#Step 3 - Configure Password Policy
if ($ConfigurePasswordPolicy -or ($DoAllTasks -and (Should-Run-Step "3"))) {
    ConfigurePasswordPolicy -DomainName $DomainName
}
#Step 4 - Install System Center Endpoint Protection
if($InstallSystemCenterEndpointProtection -or ($DoAllTasks -and (Should-Run-Step "4"))) {
    InstallSystemCenterEndpointProtection
}
#Step 5 - Install SQL Server
if($InstallSQLServer -or ($DoAllTasks -and (Should-Run-Step "5"))) {
    InstallSQLServer -Password $Password
}
#Step 6- Install SharePoint
if($InstallSharePoint -or ($DoAllTasks -and (Should-Run-Step "6"))) {
    InstallSharePoint
}
#Step 7- Install PowerPivot
if($InstallPowerPivot -or ($DoAllTasks -and (Should-Run-Step "7"))) {
    InstallPowerPivot -Password $Password
}
#Step 8 - Configure PowerPivot
if($ConfigurePowerPivot -or ($DoAllTasks -and (Should-Run-Step "8"))) {
    ConfigurePowerPivot -passphrase $passphrase -Password $Password
}
#Step 9 - Configure PowerPivot Part 2
if($ConfigurePowerPivotPart2 -or ($DoAllTasks -and (Should-Run-Step "9"))) {
    ConfigurePowerPivotPart2 -passphrase $passphrase -Password $Password
}</pre>
This part of the script calls the right downstream execution script with the right parameters.

Up next: the script that disables Internet Explorer Enhanced Security Configuration.