---
id: 2092
title: 'Automatically building a Microsoft BI machine using PowerShell – Disabling Internet Explorer Enhanced Security Configuration (post #6)'
date: '2015-11-24T14:30:43+01:00'
author: 'Jeroen ter Heerdt'
layout: post
guid: 'http://www.dutchdatadude.com/?p=2092'
permalink: /automatically-building-a-microsoft-bi-machine-using-powershell-disabling-internet-explorer-enhanced-security-configuration-post-6/
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

<em>This post is #6 in the series to automatically build a Microsoft BI machine using PowerShell – <a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-start-of-series/">see the start of series</a>.
</em>

In this series so far:

<a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-start-of-series/">Start of series – introduction and layout of subjects</a>
<a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-preparation-install-files-using-disk-post-2/">Post #2 – Preparation: install files using Azure disk</a>
<a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-preparation-install-files-using-azure-file-service-post-3/">Post #3 – Preparation: install files using Azure File Service</a>
<a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-preparation-logging-infrastructure-post-4/">Post #4 –Preparation: logging infrastructure</a>
<a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-master-script-post-5/">Post #5 – Master script</a>

In this step we will disable the Internet Explorer Enhanced Security Configuration. In general IEESC is a great idea, but on demo machines it is not very useful and makes the demo less usable. This script comes from <a href="http://itproctology.blogspot.nl/2013/09/powershell-to-disable-ie-enhanced.html">http://itproctology.blogspot.nl/2013/09/powershell-to-disable-ie-enhanced.html</a>:
<pre class="lang:c# decode:true ">#Disables Internet Explorer Enhanced Security Configuration
#source: http://itproctology.blogspot.nl/2013/09/powershell-to-disable-ie-enhanced.html
Function DisableIEESC {
    Write-Log -Verbose "Step 1: Disable Internet Explorer Enhanced Security"
    try {
        $AdminKey = “HKLM:\SOFTWARE\Microsoft\Active Setup\Installed Components\{A509B1A7-37EF-4b3f-8CFC-4F3A74704073}”
        $UserKey = “HKLM:\SOFTWARE\Microsoft\Active Setup\Installed Components\{A509B1A8-37EF-4b3f-8CFC-4F3A74704073}”
        Set-ItemProperty -Path $AdminKey -Name “IsInstalled” -Value 0
        Set-ItemProperty -Path $UserKey -Name “IsInstalled” -Value 0
        Stop-Process -Name Explorer
        Write-Log -Verbose  "IE ESC succesfully disabled"
        if ($global:DoAllTasks) {
            Set-Restart-AndResume $global:script "2"
        }
    }
    catch {
        Write-Log -Verbose  "Failed to disable IE ESC. Error: $_.Exception.Message"
    }
}</pre>
Next step: set up Active Directory.