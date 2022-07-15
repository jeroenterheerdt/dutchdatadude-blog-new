---
id: 2381
title: 'Automatically building a Microsoft BI machine using PowerShell – Final post (post #14)'
date: '2016-01-19T14:30:40+01:00'
author: 'Jeroen ter Heerdt'
layout: post
guid: 'http://www.dutchdatadude.com/?p=2381'
permalink: /automatically-building-a-microsoft-bi-machine-using-powershell-final-post-post-14/
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

<em>This post is #14 in the series to automatically build a Microsoft BI machine using PowerShell – <a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-start-of-series/">see the start of series</a>.
</em>

In this series:

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
<a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-installing-powerpivot-for-sharepoint-post-12/">Post #12 – Installing PowerPivot for SharePoint</a>
<a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-configuring-powerpivot-post-13/">Post #13 – Configuring PowerPivot for SharePoint</a>

Wow. This has been a long and wild ride. But you and I made it together. We now have the full recipe to automatically configure a Microsoft BI demo machine with PowerShell. Of course there is more to be done, such as configuring other Service Accounts and deploying demo content; this script however saves me a lot of time every time I need to stand up a new demo machine.

<a href="https://github.com/jeroenterheerdt/dutchdatadude/tree/master/Automatically-building-a-Microsoft-BI-machine-using-PowerShell">You can download the script on Github.</a> Please note (again) that the code is provided as-is and you should use it at your own risk. It is probably still buggy but should give you a good starting point to adapt it to your needs.

I enjoyed the ride with you; hope I made your life a bit easier of the course of this series. Enjoy!