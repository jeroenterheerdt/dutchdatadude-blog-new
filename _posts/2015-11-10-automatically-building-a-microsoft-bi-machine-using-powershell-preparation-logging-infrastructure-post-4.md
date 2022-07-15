---
id: 2021
title: 'Automatically building a Microsoft BI machine using PowerShell – preparation: logging infrastructure (post #4)'
date: '2015-11-10T14:30:16+01:00'
author: 'Jeroen ter Heerdt'
layout: post
guid: 'http://www.dutchdatadude.com/?p=2021'
permalink: /automatically-building-a-microsoft-bi-machine-using-powershell-preparation-logging-infrastructure-post-4/
sharing_disabled:
    - '1'
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

<em>This post is #4 in the series to automatically build a Microsoft BI machine using PowerShell – <a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-start-of-series/">see the start of series</a>.
</em>

In this series so far:

<a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-start-of-series/">Start of series – introduction and layout of subjects</a>
<a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-preparation-install-files-using-disk-post-2/">Post #2 – Preparation: install files using Azure disk</a>
<a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-preparation-install-files-using-azure-file-service-post-3/">Post #3 – Preparation: install files using Azure File Service</a>

Our final step in preparation is setting up a logging infrastructure. I found a very simple to use function online, see the code below:
<pre class="lang:c# decode:true">Function Write-Log {
    [cmdletbinding()]

    Param(
    [Parameter(Position=0)]
    [ValidateNotNullOrEmpty()]
    [string]$Message
    )
    
    #Pass on the message to Write-Verbose if -Verbose was detected
    Write-Verbose $Message
    
    Write-Output "$(Get-Date) $Message" | Out-File -FilePath $global:LogFile -Append
    

} #end function</pre>
Including this function in the script enables any step to write to a log by passing a $Message to this function.

Next post will be our master script.