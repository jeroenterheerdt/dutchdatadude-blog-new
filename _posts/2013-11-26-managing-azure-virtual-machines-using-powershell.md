---
id: 444
title: 'Managing Azure Virtual Machines using PowerShell'
date: '2013-11-26T10:30:30+01:00'
author: 'Jeroen ter Heerdt'
layout: post
guid: 'http://www.dutchdatadude.com/?p=444'
permalink: /managing-azure-virtual-machines-using-powershell/
categories:
    - Azure
tags:
    - azure
    - PowerShell
---

I use Azure for my demo machines and needed a way to easily shut all VMs down and also to start my BI demo machines. What better way to do this other than with PowerShell!

In order to be able to talk to Azure with Powershell you will need to install Windows Azure Powershell (download link: <a href="http://www.windowsazure.com/en-us/downloads/">http://www.windowsazure.com/en-us/downloads/</a> ).

Also you will need to get your Azure Publish Settings file which is specific to your subscription. You can get it from the Azure portal once you are logged in: <a href="https://windows.azure.com/download/publishprofile.aspx">https://windows.azure.com/download/publishprofile.aspx</a> .

Let's start with stopping all VMs. Start the PowerShell ISE (search for powershell_ise on Windows 8) and create the following script:
<p style="background: white;"></p>

<pre>Import-Module "C:\Program Files (x86)\Microsoft SDKs\Windows Azure\PowerShell\Azure\Azure.psd1"
Import-AzurePublishSettingsFile "PathToYourPublishSettingsFile"
echo "Stopping ALL VMs"
get-azureSubscription | ForEach-Object {
 get-azureVM | Where-Object {$_.Status -like "Ready*"} | ForEach-Object {
  echo $_.Name
  Stop-AzureVM -ServiceName $_.ServiceName -Name $_.Name -Force }
}</pre>
<p style="background: white;">Make sure to enter the path to where you stored your publish profile that you have downloaded.</p>
Basically what this script does is iterate over all your subscriptions if you have more than 1 and look for VMs that are in a running state using get-AzureVM. Then for each VM that is running it will echo its name and then stop the VM using stop-AzureVM.

Save the script and then you can just run it and all of your VMs will be turned off. Pretty easy huh?

For my BI demos I use a maximum of four VMs and I made another script that starts them in the correct other (first the domain controller, then the SQL server and then finally the two SharePoint servers I need):
<pre>Import-Module "C:\Program Files (x86)\Microsoft SDKs\Windows Azure\PowerShell\Azure\Azure.psd1"
Import-AzurePublishSettingsFile "PathToYourPublishSettingsFile"

function StartVM($serviceName, $name) {
get-azureSubscription | ForEach-Object {
$vm = get-AzureVM |Where-Object {($_.Name = $name) -and ($_.ServiceName = $serviceName)}
if($vm -ne $null) {
if($vm[0].Status = "StoppedDeallocated") {
Start-AzureVM -ServiceName $serviceName -Name $name
Write-Host "$name started"
 }
else {
Write-Host "$name already running"
 }
 }
 }
}

echo "Starting BI Demo VMs"
StartVM -serviceName "VMServiceName" -name "VMName"
StartVM -serviceName "VMServiceName" -name "VMName"
StartVM -serviceName "VMServiceName" -name "VMName"
StartVM -serviceName "VMServiceName" -name "VMName"</pre>
This script defines a function that wraps a check if the VM is already running and otherwise starts it. The bottom part of this script uses that function to specify which VMs to start in which order. I replaced the original names for security reasons.

This saves a lot of time. It saves me from logging into the Azure portal and starting / stopping each VM by hand. The best part is I can let this run in the background while presenting and nobody sees it <span style="font-family: Wingdings;">J</span>
<p style="background: white;"><span style="font-family: Lucida Console; font-size: 9pt;">
</span></p>