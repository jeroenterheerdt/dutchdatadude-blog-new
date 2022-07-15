---
id: 842
title: 'Automatically building a Microsoft BI machine using PowerShell – Start of Series'
date: '2015-05-12T14:30:59+01:00'
author: 'Jeroen ter Heerdt'
layout: post
guid: 'http://www.dutchdatadude.com/?p=842'
permalink: /automatically-building-a-microsoft-bi-machine-using-powershell-start-of-series/
categories:
    - Azure
    - 'Business Intelligence'
    - SharePoint
    - 'SQL Server'
    - Uncategorized
tags:
    - 'Power Pivot'
    - 'power view'
    - PowerShell
---

I used to spend quite some time on building and re-building Microsoft BI demo machines. As you can imagine this manual process takes a lot of time and effort. Therefore (and also for my own education on PowerShell) I decided to look into automating the whole process. I will explain this in this series of posts.

<strong>The goal
</strong>

In the end, we want to have a virtual machine that is configured as follows: Windows Server 2012 R2, with Active Directory Domain Controller role. Additionally, SQL Server 2014 is installed and configured as well as SharePoint 2013. Finally, the BI tools like Power Pivot and Power View are configured.

<strong>Ok, but how do we build such a machine?
</strong>

Here are the steps to take. I always do them in this order, partly because there are some dependencies and partly because it stops me from going insane.
<ol>
	<li>Install Windows (doh). I will skip this step (therefore it is number 0) since I use Azure and a VM in Azure comes with Windows Server pre-installed. I happen to use Windows Server 2012 R2 b.t.w.</li>
	<li>Disable Internet Explorer Enhanced Security Configuration. Although it is a great idea (see <a href="http://technet.microsoft.com/en-us/library/dd883248(v=WS.10).aspx">http://technet.microsoft.com/en-us/library/dd883248(v=WS.10).aspx</a> for more info on this) it is hard to give a good demo on the machine with this thing on. So first step is disabling it.</li>
	<li>Set up Active Directory; AD is required for the PowerPivot service.</li>
	<li>After AD has been set up we need to promote the Domain Controller.</li>
	<li>After promotion we configure a very unrestrictive password policy; remember, this is just a demo machine!</li>
	<li>Virus protection is important, even for a demo machine; therefore set up System Center Endpoint Protection.</li>
	<li>Install SQL Server 2014.</li>
	<li>Install SharePoint.</li>
	<li>Install PowerPivot Service.</li>
	<li>Configure PowerPivot Service.</li>
	<li>Configure last parts of PowerPivot Service.</li>
	<li>Configure Master Data Services.</li>
	<li>Configure Data Quality Services.</li>
	<li>Configure other SharePoint Service Applications.</li>
	<li>Activate SharePoint site features.</li>
	<li>Add favorites in Internet Explorer to point to MDS and SharePoint site.</li>
</ol>
In this blog series I will share my PowerShell code to accomplish this. Please note that I am not a developer so things can probably be done a lot smarter <span style="font-family: Wingdings;">J</span>

Next step is preparation: <a href="http://www.dutchdatadude.com/automatically-building-a-microsoft-bi-machine-using-powershell-preparation-install-files-using-disk-post-2/">the install files.</a>