---
id: 2171
title: 'Automatically building a Microsoft BI machine using PowerShell – Password policy (post #8)'
date: '2015-12-08T14:30:01+01:00'
author: 'Jeroen ter Heerdt'
layout: post
guid: 'http://www.dutchdatadude.com/?p=2171'
permalink: /automatically-building-a-microsoft-bi-machine-using-powershell-password-policy-post-8/
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

<em>This post is #8 in the series to automatically build a Microsoft BI machine using PowerShell – <a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-start-of-series/">see the start of series</a>.
</em>

In this series so far:

<a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-start-of-series/">Start of series – introduction and layout of subjects</a>
<a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-preparation-install-files-using-disk-post-2/">Post #2 – Preparation: install files using Azure disk</a>
<a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-preparation-install-files-using-azure-file-service-post-3/">Post #3 – Preparation: install files using Azure File Service</a>
<a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-preparation-logging-infrastructure-post-4/">Post #4 –Preparation: logging infrastructure</a>
<a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-master-script-post-5/">Post #5 – Master script</a>
<a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-disabling-internet-explorer-enhanced-security-configuration-post-6/">Post #6 – Disabling Internet Explorer Enhanced Security Configuration</a>
<a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-active-directory-setup-post-7/">Post #7 – Active Directory setup</a>

In this step we will configure a very permissive password policy. This of course requires that the previous step (setting up Active Directory) has successfully completed. The password policy set using this script is only suitable for demo environments since it is very, very (did I say very?) permissive; it sets a minimal password length of 0, does not record any history of passwords (you can re-use your password again and again), passwords never expire and do not have to follow complexity rules. So, even an empty password is allowed (although not recommended since your Windows services will then not start). However, having '1234' as password would work perfectly under this policy (and no, this is not the password I use for my demo machines).
<pre class="lang:c# decode:true ">Function ConfigurePasswordPolicy {
    Param(
        [Parameter(Mandatory=$true,HelpMessage="Domain name required, please specify in format yyy.zzz")]
        [ValidateNotNullOrEmpty()]
        $DomainName
    )
    Write-Log -Verbose  "Step 3: Configure Password Policy"
   try {
    Set-ADDefaultDomainPasswordPolicy -Identity $DomainName -MinPasswordLength:0 -PasswordHistoryCount:0 -MaxPasswordAge:0 -MinPasswordAge:0 -ComplexityEnabled:$false
    Write-Log -Verbose  "Password Policy Configured"
    if ($global:DoAllTasks) {
        Set-Restart-AndResume $global:script "5"
    }
    }
    catch {
    Write-Log -Verbose  "Failed to configure Password Policy. Error: $_.Exception.Message"
    }
}</pre>
&nbsp;

Next step: installing System Center Endpoint protection