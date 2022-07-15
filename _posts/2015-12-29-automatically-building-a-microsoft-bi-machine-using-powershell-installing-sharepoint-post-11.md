---
id: 2261
title: 'Automatically building a Microsoft BI machine using PowerShell – Installing SharePoint (post #11)'
date: '2015-12-29T14:30:34+01:00'
author: 'Jeroen ter Heerdt'
layout: post
guid: 'http://www.dutchdatadude.com/?p=2261'
permalink: /automatically-building-a-microsoft-bi-machine-using-powershell-installing-sharepoint-post-11/
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

<em>This post is #11 in the series to automatically build a Microsoft BI machine using PowerShell – <a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-start-of-series/">see the start of series</a>.
</em>

In this series so far:

<a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-start-of-series/">Start of series – introduction and layout of subjects</a>
<a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-preparation-install-files-using-disk-post-2/">Post #2 – Preparation: install files using Azure disk</a>
<a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-preparation-install-files-using-azure-file-service-post-3/">Post #3 – Preparation: install files using Azure File Service</a>
<a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-preparation-logging-infrastructure-post-4/">Post #4 –Preparation: logging infrastructure</a>
<a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-master-script-post-5/">Post #5 – Master script</a>
<a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-disabling-internet-explorer-enhanced-security-configuration-post-6/">Post #6 – Disabling Internet Explorer Enhanced Security Configuration</a>
<a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-active-directory-setup-post-7/">Post #7 – Active Directory setup</a>
<a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-password-policy-post-8/">Post #8 – Configuring Password policy</a>
<a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-installing-system-center-endpoint-protection-post-9/">Post #9 – Installing System Center Endpoint Protection</a>
<a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-installing-sql-server-post-10/">Post #10 – Installing SQL Server</a>

Wow, so the last post was pretty intense, wasn't it? I think we are ready for the next one: installing SharePoint. To build this script I used the following sources: <a href="http://social.technet.microsoft.com/wiki/contents/articles/14582.sharepoint-2013-install-prerequisites-offline-or-manually-on-windows-server-2012-a-comprehensive-guide.aspx#Installing_the_Roles_and_Features_for_SharePoint_2013_on_Windows_Server_2012_Offline_with_PowerShell">http://social.technet.microsoft.com/wiki/contents/articles/14582.sharepoint-2013-install-prerequisites-offline-or-manually-on-windows-server-2012-a-comprehensive-guide.aspx#Installing_the_Roles_and_Features_for_SharePoint_2013_on_Windows_Server_2012_Offline_with_PowerShell</a> and <a href="http://blogs.msdn.com/b/uksharepoint/archive/2013/03/18/scripted-installation-of-sharepoint-2013-and-office-web-apps-server-from-the-field-part-2.aspx">http://blogs.msdn.com/b/uksharepoint/archive/2013/03/18/scripted-installation-of-sharepoint-2013-and-office-web-apps-server-from-the-field-part-2.aspx</a>.

Since this is again a quite lengthly script we will split it up in steps.

<strong>Step A: enabling IIS and other features
</strong>

This step enables a whole load of features on Windows that are required by SharePoint, including IIS. If a restart is required, the script will reboot after the setup of the features. Some times your machine might reboot more than once to complete the setup of all these features.
<pre class="lang:c# decode:true ">Write-Log -Verbose  "Step 6: Install SharePoint"
Import-Module ServerManager
#Add .Net 4.5 features
Add-WindowsFeature NET-WCF-HTTP-Activation45,NET-WCF-TCP-Activation45,NET-WCF-Pipe-Activation45
#Add the rest of the needed features for IIS role
$result = Add-WindowsFeature Net-Framework-Features,Web-Server,Web-WebServer,Web-Common-Http,Web-Static-Content,Web-Default-Doc,Web-Dir-Browsing,Web-Http-Errors,Web-App-Dev,Web-Asp-Net,Web-Net-Ext,Web-ISAPI-Ext,Web-ISAPI-Filter,Web-Health,Web-Http-Logging,Web-Log-Libraries,Web-Request-Monitor,Web-Http-Tracing,Web-Security,Web-Basic-Auth,Web-Windows-Auth,Web-Filtering,Web-Digest-Auth,Web-Performance,Web-Stat-Compression,Web-Dyn-Compression,Web-Mgmt-Tools,Web-Mgmt-Console,Web-Mgmt-Compat,Web-Metabase,Application-Server,AS-Web-Support,AS-TCP-Port-Sharing,AS-WAS-Support, AS-HTTP-Activation,AS-TCP-Activation,AS-Named-Pipes,AS-Net-Framework,WAS,WAS-Process-Model,WAS-NET-Environment,WAS-Config-APIs,Web-Lgcy-Scripting,Windows-Identity-Foundation,Server-Media-Foundation,Xps-Viewer
if($result.RestartNeeded -eq "Yes")
{
    Set-Restart-AndResume $global:script "7"
}</pre>
&nbsp;

<strong>Step B: Installing SharePoint Prerequisites
</strong>

SharePoint itself has a number of prerequisites; in this still we will install them all.
<pre class="lang:c# decode:true ">#Mount SharePoint iso
$mountresult = Mount-DiskImage -ImagePath $global:pathToSharePointISO -PassThru
$driveLetter = ($mountresult | Get-Volume).DriveLetter
Write-Log -Verbose  "Installing SharePoint PreReqs...."
$setupFile = $driveLetter+":\prerequisiteinstaller.exe"
$process = Start-Process $setupFile -PassThru -Wait -ArgumentList "/unattended /SQLNCli:$global:SharePoint2013Path\PrerequisiteInstallerFiles\sqlncli.msi /IDFX:$global:SharePoint2013Path\PrerequisiteInstallerFiles\Windows6.1-KB974405-x64.msu /IDFX11:$global:SharePoint2013Path\PrerequisiteInstallerFiles\MicrosoftIdentityExtensions-64.msi /Sync:$global:SharePoint2013Path\PrerequisiteInstallerFiles\Synchronization.msi /AppFabric:$global:SharePoint2013Path\PrerequisiteInstallerFiles\WindowsServerAppFabricSetup_x64.exe /KB2671763:$global:SharePoint2013Path\PrerequisiteInstallerFiles\AppFabric1.1-RTM-KB2671763-x64-ENU.exe /MSIPCClient:$global:SharePoint2013Path\PrerequisiteInstallerFiles\setup_msipc_x64.msi /WCFDataServices:$global:SharePoint2013Path\PrerequisiteInstallerFiles\WcfDataServices.exe"</pre>
&nbsp;

<strong>Step C: Installing SharePoint
</strong>

SharePoint is installed in this step from the ISO that the script mounts.
<pre class="lang:c# decode:true ">if($process.ExitCode -eq 0) {
        #install sharepoint
        Write-Log -Verbose  "Installing SharePoint...."
        $path = $driveLetter+":\Setup.exe"
        $sharePointInstallProcess = Start-Process -Wait -PassThru $path -ArgumentList "/config $global:SharePoint2013Path\FarmSilentConfig.xml"
        switch($sharePointInstallProcess.ExitCode)
        {
            0 {
                Write-Log -Verbose  "SharePoint successfully installed"
                Write-Log -Verbose  "SharePoint Installed"
                if ($global:DoAllTasks) {
                    Set-Restart-AndResume $global:script "8"
                    }
            }
            default{
                Write-Log -Verbose  "An error has occured in installing SharePoint. Code: " $sharePointInstallProcess.ExitCode
            }
        }
    }
    else {
        if($process.ExitCode -eq 3010) {
            Write-Log -Verbose  "SharePoint prereqs install requires a reboot"
        }
        else {
            Write-Log -Verbose  "SharePoint prereqs not succesfully installed, please investigate.  Code: " $process.ExitCode
        }
    }</pre>
&nbsp;

<strong>Step D: Cleaning up
</strong>

This step simply unmounts the SharePoint installation media.
<pre class="lang:c# decode:true ">Dismount-DiskImage -ImagePath $global:pathToSharePointISO</pre>
&nbsp;

Pff, are we done yet? No! Next up: Installing PowerPivot for SharePoint.