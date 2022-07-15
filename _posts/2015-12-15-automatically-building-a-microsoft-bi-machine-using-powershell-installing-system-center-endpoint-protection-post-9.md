---
id: 2201
title: 'Automatically building a Microsoft BI machine using PowerShell – Installing System Center Endpoint Protection (post #9)'
date: '2015-12-15T14:30:45+01:00'
author: 'Jeroen ter Heerdt'
layout: post
guid: 'http://www.dutchdatadude.com/?p=2201'
permalink: /automatically-building-a-microsoft-bi-machine-using-powershell-installing-system-center-endpoint-protection-post-9/
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

<em>This post is #9 in the series to automatically build a Microsoft BI machine using PowerShell – <a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-start-of-series/">see the start of series</a>.
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

Although in the last step we configured a very permissive password policy we need a bit of security, so that is why I opted to install System Center Endpoint Protection. Now, in Azure you can also have extensions for security (both with Microsoft and 3<sup>rd</sup> party security products) so probably you will never install System Center Endpoint protection yourself, but for the sake of reference, here is how to install it using PowerShell.
<pre class="lang:c# decode:true ">Function InstallSystemCenterEndpointProtection
{
    Write-Log -Verbose  "Step 4: Install System Center Endpoint Protection"
    Start-Process .\Resources\SystemCenterEndpointProtection\scepinstall.exe -Wait -ArgumentList "/s /q" #-NoNewWindow
    Write-Log -Verbose  "System Center Endpoint Protection Installed"
    if ($global:DoAllTasks) {
        Set-Restart-AndResume $global:script "6"
        }
}</pre>
Next step: installing SQL Server