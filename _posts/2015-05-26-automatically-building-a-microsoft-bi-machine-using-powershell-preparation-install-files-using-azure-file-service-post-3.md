---
id: 854
title: 'Automatically building a Microsoft BI machine using PowerShell – preparation: install files using Azure File Service (post #3)'
date: '2015-05-26T14:30:54+01:00'
author: 'Jeroen ter Heerdt'
layout: post
guid: 'http://www.dutchdatadude.com/?p=854'
permalink: /automatically-building-a-microsoft-bi-machine-using-powershell-preparation-install-files-using-azure-file-service-post-3/
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

<em>This post is #3 in the series to automatically build a Microsoft BI machine using PowerShell – <a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-start-of-series/">see the start of series</a>.</em>

&nbsp;

In this series so far:

<a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-start-of-series/">Start of series – introduction and layout of subjects</a>
<a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-preparation-install-files-using-disk-post-2/">Post #2 – Preparation: install files using Azure disk</a>

&nbsp;

&nbsp;

<a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-preparation-install-files-using-disk-post-2/">In our last post we looked a one way of working with the install files required for automating the installation of a BI machine, using disks</a>. This post will focus on sharing the install files using Azure File Service. The Azure File Service exposes file shares using the standard SMB 2.1 protocol. It is in some ways an addition to storage accounts. See <a href="http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx">http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx</a> for more information. This service is in beta at the moment, so you will need to subscribe to the beta using the Azure Preview portal: <a href="http://azure.microsoft.com/en-us/services/preview/">http://azure.microsoft.com/en-us/services/preview/</a>. Look for 'Azure Files' in the list and click on 'Try it' to get your account activated for the preview.

The Azure File Service is not exposed in any portal, probably since it is in preview. Also, keep in mind that while the service is in preview existing storage accounts will not have access to the File Service, so we will need to create a new storage account as well. To do this login into the portal and click on 'New' and create a new storage account. After the storage account has been created, you will need to use PowerShell to create a file share. Make sure you have the latest version of Azure PowerShell installed and then run the following in Azure PowerShell or use ISE:
<pre class="lang:ps decode:true ">$storageAccountName  = "YourStorageAccountName"
$storageAccountKey = "YourStorageAccountKey" 
$ctx = New-AzureStorageContext $storageAccountName $storageAccountKey
$s = New-AzureStorageShare YourShareName -Context $ctx
</pre>
After this runs you should be able to access the file share in multiple ways, but the easiest way I found is mapping the share as a folder in a VM by running:
<pre class="lang:default decode:true ">Net use e: \\YourStorageAccountName.file.core.windows.net\YourShareName /u:YourStorageAccountName YourStorageAccountKey</pre>
Now you can download and store files on the share just as you can with disks, <a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-preparation-install-files-using-disk-post-2/">as discussed in post #2 on using install files using Azure disks</a>.

Next post will be our final step of the preparation: logging.

&nbsp;

&nbsp;

&nbsp;