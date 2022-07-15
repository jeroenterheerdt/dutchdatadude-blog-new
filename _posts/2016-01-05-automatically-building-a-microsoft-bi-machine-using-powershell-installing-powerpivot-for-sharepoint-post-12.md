---
id: 2291
title: 'Automatically building a Microsoft BI machine using PowerShell – Installing PowerPivot for SharePoint (post #12)'
date: '2016-01-05T14:30:50+01:00'
author: 'Jeroen ter Heerdt'
layout: post
guid: 'http://www.dutchdatadude.com/?p=2291'
permalink: /automatically-building-a-microsoft-bi-machine-using-powershell-installing-powerpivot-for-sharepoint-post-12/
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

<em>This post is #12 in the series to automatically build a Microsoft BI machine using PowerShell – <a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-start-of-series/">see the start of series</a>.
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
<a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-installing-sharepoint-post-11/">Post #11 – Installing SharePoint Server</a>

Ok, now that both SQL Server and SharePoint Server are installed, we just need to set up PowerPivot for SharePoint and configure it. Easy huh? Well, it turns out it is pretty difficult to get it right. Installation is not difficult (this post) but the configuration is harder (the next post). Here is how to install PowerPivot. I used MSDN for the info: <a href="http://msdn.microsoft.com/en-us/library/ee210645.aspx">http://msdn.microsoft.com/en-us/library/ee210645.aspx</a>.

Installing PowerPivot involves mounting the SQL Server Installation Media and calling the setup with the right parameters.
<pre class="lang:c# decode:true ">Function InstallPowerPivot
{
Param(
        [Parameter(Mandatory=$true)]
        [ValidateNotNullOrEmpty()]
        $Password
)
    Write-Log -Verbose  "Step 7: Install PowerPivot"
    #MOUNT SQL ISO
    $mountresult = Mount-DiskImage -ImagePath $global:pathToSQLISO -PassThru
    $driveLetter = ($mountresult | Get-Volume).DriveLetter
    $setupFile = $driveLetter+":\setup.exe"
    #Remove Service Account if it already existed
    Get-ADServiceAccount -Filter {Name -eq 'PP'} | Remove-ADServiceAccount
    $ppAccountName = "PP"
    $ppAccountNameFQ = $global:domainpart+"\"+$ppAccountName
    CreateServiceAccount -AccountName $ppAccountName -DisplayName "PowerPivot" -Description "Service Account for PowerPivot for SharePoint" -Path $global:path -Password $Password
    #do PP installation
    #trying with plain text pwd in call
    $process = Start-Process -NoNewWindow -Wait $setupFile -ArgumentList "/ACTION=INSTALL /IACCEPTSQLSERVERLICENSETERMS /Q /INSTANCENAME=POWERPIVOT /ERRORREPORTING=1 /SQMREPORTING=1 /ASSVCACCOUNT=$ppAccountNameFQ /ASSVCPASSWORD=$Password /ASSYSADMINACCOUNTS=$global:currentUserName /ROLE=SPI_AS_ExistingFarm"
    #SPI_AS_ExistingFarm
    
    #dismount
    Dismount-DiskImage -ImagePath $global:pathToSQLISO
    Write-Log -Verbose  "If above an error is shown please check out C:\Program Files\Microsoft SQL Server\120\Setup Bootstrap\Log\Summary.txt"
    Write-Log -Verbose  "PowerPivot Installed"
    if ($global:DoAllTasks) {
        Set-Restart-AndResume $global:script "9"
        }
}</pre>
Next time: configuring PowerPivot.