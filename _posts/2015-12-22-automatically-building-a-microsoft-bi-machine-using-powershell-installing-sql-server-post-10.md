---
id: 2231
title: 'Automatically building a Microsoft BI machine using PowerShell – Installing SQL Server (post #10)'
date: '2015-12-22T14:30:33+01:00'
author: 'Jeroen ter Heerdt'
layout: post
guid: 'http://www.dutchdatadude.com/?p=2231'
permalink: /automatically-building-a-microsoft-bi-machine-using-powershell-installing-sql-server-post-10/
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

<em>This post is #10 in the series to automatically build a Microsoft BI machine using PowerShell – <a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-start-of-series/">see the start of series</a>.
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

In this tenth post we will get to the heart of it: installing SQL Server. After this script completes we will have SQL Agent, SQL Database, Analysis Services (multidimensional and tabular), Integration Services, Data Quality Services, Master Data Services, FullText search, Filestreaming, Development and Management tools and Reporting Services (both native and SharePoint integrated mode) installed. This script will be lengthier than earlier scripts simply because there is a lot more to do. Info I used to create this script: <a href="http://msdn.microsoft.com/en-us/library/ms144259.aspx">http://msdn.microsoft.com/en-us/library/ms144259.aspx</a>. Here we go.

<strong>Step A: creating new service accounts
</strong>

In this step we first remove any service account that starts with 'SQL Server' and then create new serviceaccounts using the configured password.
<pre class="lang:c# decode:true">#Remove Service Accounts for SQL in case they already exist
Get-ADServiceAccount -Filter {DisplayName -like 'SQL Server*'} | Remove-ADServiceAccount
#Create accounts
$sqlagentAccountName = "SQLAgent"
$ssasAccountName = "SSAS"
$sqldbAccountName = "SQLDB"
$ssisAccountName = "SSIS"
$ssrsAccountName = "SSRS"
$sqlagentAccountNameFQ = $global:domainpart+"\"+$sqlagentAccountName
$ssasAccountNameFQ = $global:domainpart+"\"+$ssasAccountName
$sqldbAccountNameFQ = $global:domainpart+"\"+$sqldbAccountName
$ssisAccountNameFQ = $global:domainpart+"\"+$ssisAccountName
$ssrsAccountNameFQ = $global:domainpart+"\"+$ssrsAccountName
     
CreateServiceAccount -AccountName $sqlagentAccountName -DisplayName "SQL Server Agent" -Description "Service Account for SQL Server Agent" -Path $global:path -Password $password
CreateServiceAccount -AccountName $ssasAccountName -DisplayName "SQL Server Analysis Services" -Description "Service Account for SQL Server Analysis Services" -Path $global:path -Password $password
CreateServiceAccount -AccountName $sqldbAccountName -DisplayName "SQL Server Database Engine" -Description "Service Account for SQL Server Database Engine" -Path $global:path -Password $password
CreateServiceAccount -AccountName $ssisAccountName -DisplayName "SQL Server Integration Services" -Description "Service Account for SQL Server Integration Services" -Path $global:path -Password $password
CreateServiceAccount -AccountName $ssrsAccountName -DisplayName "SQL Server Reporting Services" -Description "Service Account for SQL Server Reporting Services" -Path $global:path -Password $password</pre>
&nbsp;

<strong>Step B: making sure required features are installed
</strong>

In this step we make sure .NET 3.5 feature is enabled in Windows.
<pre class="lang:c# decode:true">#Make sure the .Net 3.5 feature is enabled
Install-WindowsFeature –name NET-Framework-Core</pre>
&nbsp;

<strong>Step C: Mounting the ISO and set up the parameters
</strong>

We can now mount the SQL Server installation ISO and set up parameters for the setup to run with. We will do two phases (passes) since we cannot install both SSRS Native and SharePoint integrated mode and SSAS Multidimensional and Tabular mode in one go.
<pre class="lang:c# decode:true ">#Mount and Install SQL
    
$mountresult = Mount-DiskImage -ImagePath $global:pathToSQLISO -PassThru
$driveLetter = ($mountresult | Get-Volume).DriveLetter
$setupFile = $driveLetter+":\setup.exe"
#Run first pass of SQL Install: SQLDB,DQ,FullText,FileStreaming,AS,RSNative,DataQualityCLient,IS,MDS,Tools
$featuresPass1 = "SQL,AS,RS,DQC,IS,MDS,TOOLS"
$featuresPass2 = "AS,RS_SHP,RS_SHPWFE"</pre>
&nbsp;

<strong>Step D: do the actual installations
</strong>

Now we execute SQL Server setup with the right argument list. This configures instance names, service accounts and passwords and the features to install. The install will be silent.
<pre class="lang:c# decode:true ">Start-Process $setupFile -NoNewWindow -Wait -ArgumentList "/ACTION=INSTALL /IACCEPTSQLSERVERLICENSETERMS /Q /INSTANCENAME=MSSQLSERVER /ERRORREPORTING=1 /SQMREPORTING=1 /AGTSVCACCOUNT=$sqlagentAccountNameFQ /AGTSVCPASSWORD=$Password /ASSVCACCOUNT=$ssasAccountNameFQ /ASSVCPASSWORD=$Password /ASSERVERMODE=MULTIDIMENSIONAL /ASSYSADMINACCOUNTS=$global:currentUserName /SQLSVCACCOUNT=$sqldbAccountNameFQ /SQLSVCPASSWORD=$Password /SQLSYSADMINACCOUNTS=$global:currentUserName /FILESTREAMLEVEL=1 /ISSVCACCOUNT=$ssisAccountNameFQ /ISSVCPASSWORD=$Password /RSINSTALLMODE=DefaultNativeMode /RSSVCACCOUNT=$ssrsAccountNameFQ /RSSVCPASSWORD=$Password /FEATURES=$featuresPass1"
Write-Log -Verbose  "SQL Server Installation Pass 1 completed: SQL, AS Multidimensional, RS Native, Data QUality Client, DQS IS, MDS, TOOLS, FullText, FileStreaming"
Start-Process $setupFile -NoNewWindow -Wait -ArgumentList "/ACTION=INSTALL /IACCEPTSQLSERVERLICENSETERMS /Q /INSTANCENAME=TABULAR /ERRORREPORTING=1 /SQMREPORTING=1 /ASSVCACCOUNT=$ssasAccountNameFQ /ASSVCPASSWORD=$Password /ASSERVERMODE=TABULAR /ASSYSADMINACCOUNTS=$global:currentUserName /FEATURES=$featuresPass2"
Write-Log -Verbose  "SQL Server Installation Pass 2 completed: RS SharePoint, AS Tabular"</pre>
&nbsp;

<strong>Step E: wrapping up
</strong>

In this step we unmount the SQL Server installation media and write to the log.
<pre class="lang:c# decode:true ">Dismount-DiskImage -ImagePath $global:pathToSQLISO
Write-Log -Verbose  "SQL Server Installed"
if ($global:DoAllTasks) {
   Set-Restart-AndResume $global:script "7"
}</pre>
&nbsp;
<p style="background: white;"><span style="font-family: Lucida Console; font-size: 9pt;"> </span></p>
Next step: installing SharePoint