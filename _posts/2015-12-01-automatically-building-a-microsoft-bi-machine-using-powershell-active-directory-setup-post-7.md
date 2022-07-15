---
id: 2121
title: 'Automatically building a Microsoft BI machine using PowerShell – Active Directory Setup (post #7)'
date: '2015-12-01T14:30:30+01:00'
author: 'Jeroen ter Heerdt'
layout: post
guid: 'http://www.dutchdatadude.com/?p=2121'
permalink: /automatically-building-a-microsoft-bi-machine-using-powershell-active-directory-setup-post-7/
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

<em>This post is #7 in the series to automatically build a Microsoft BI machine using PowerShell – <a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-start-of-series/">see the start of series</a>.
</em>

In this series so far:

<a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-start-of-series/">Start of series – introduction and layout of subjects</a>
<a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-preparation-install-files-using-disk-post-2/">Post #2 – Preparation: install files using Azure disk</a>
<a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-preparation-install-files-using-azure-file-service-post-3/">Post #3 – Preparation: install files using Azure File Service</a>
<a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-preparation-logging-infrastructure-post-4/">Post #4 –Preparation: logging infrastructure</a>
<a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-master-script-post-5/">Post #5 – Master script</a>
<a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-disabling-internet-explorer-enhanced-security-configuration-post-6/">Post #6 – Disabling Internet Explorer Enhanced Security Configuration</a>

In this step we will set up Active Directory. This script has been inspired on <a href="http://blogs.technet.com/b/ashleymcglone/archive/2013/04/18/touch-free-powershell-dcpromo-in-windows-server-2012.aspx">http://blogs.technet.com/b/ashleymcglone/archive/2013/04/18/touch-free-powershell-dcpromo-in-windows-server-2012.aspx</a>.
<pre class="lang:c# decode:true ">#Set up Active Directory
#source: http://blogs.technet.com/b/ashleymcglone/archive/2013/04/18/touch-free-powershell-dcpromo-in-windows-server-2012.aspx
Function SetupActiveDirectory {
    Param(
        [Parameter(Mandatory=$true,HelpMessage="Domain name required, please specify in format yyy.zzz")]
        [ValidateNotNullOrEmpty()]
        $DomainName
    )
    Write-Log -Verbose  "Step 2: Set up Active Directory"
    
    try {
        Install-WindowsFeature -Name AD-Domain-Services -IncludeManagementTools
        if ($global:DoAllTasks) {
            Set-Restart-AndResume $global:script "3"
        }
    }
    catch {
        Write-Log -Verbose  "Failed to set up Active Directory. Error: $_.Exception.Message"
    }
}
Function SetupActiveDirectoryPart2 {
    Param(
        [Parameter(Mandatory=$true,HelpMessage="Domain name required, please specify in format yyy.zzz")]
        [ValidateNotNullOrEmpty()]
        $DomainName
    )
    Write-Log -Verbose  "Step 2: Set up Active Directory"
    
    try {
        Import-Module ADDSDeployment
        $dotposition = $DomainName.LastIndexOf('.')
        $netbiosname = $DomainName.Substring(0,$dotposition)
        $result = Install-ADDSForest -DomainName $DomainName -InstallDNS:$true -Confirm:$false -NoRebootOnCompletion:$true -Force:$true -DatabasePath "C:\Windows\NTDS" -DomainMode Win2012R2 -ForestMode Win2012R2 -LogPath "C:\Windows\NTDS" -SysvolPath "C:\Windows\SYSVOL" -DomainNetbiosName $netbiosname
        Write-Log -Verbose  "Active Directory set up done"
        if ($global:DoAllTasks) {
            Set-Restart-AndResume $global:script "4"
        }
    }
    catch {
        Write-Log -Verbose  "Failed to set up Active Directory. Error: $_.Exception.Message"
    }
}</pre>
&nbsp;

Next step: configuring a very permissive password policy.