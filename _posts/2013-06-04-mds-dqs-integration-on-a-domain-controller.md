---
id: 16
title: 'MDS / DQS integration on a domain controller'
date: '2013-06-04T12:00:26+01:00'
author: 'Jeroen ter Heerdt'
layout: post
guid: 'http://www.dutchdatadude.com/?p=16'
permalink: /mds-dqs-integration-on-a-domain-controller/
snapEdIT:
    - '1'
snapLI:
    - 's:159:"a:1:{i:0;a:4:{s:4:"doLI";s:1:"1";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:27:"New blog post on %SITENAME%";s:11:"SNAPformatT";s:18:"New Post - %TITLE%";}}";'
snapTW:
    - 's:117:"a:1:{i:0;a:3:{s:4:"doTW";s:1:"1";s:10:"SNAPformat";s:33:"Blogged: %TITLE% - %SURL% %htags%";s:8:"attchImg";s:1:"0";}}";'
categories:
    - 'Business Intelligence'
    - 'SQL Server'
tags:
    - 'master data management'
    - 'master data services'
    - mdm
    - mds
---

Normally I would never advice you installing anything on a domain controller, let alone SQL, MDS and DQS. However if you have BI demo machine you will probably have all this (and more) running on the same box. At least I do <span style="font-family: Wingdings;">J</span>

If you do you will probably get this error message when you try to enable the DQS integration from Master Data Services Configuration Manager after you successfully installed DQS and MDS.

<img alt="" src="../wp-content/uploads/2013/05/052213_0830_MDSDQSinteg1.png" />

When clicking the button 'Enable integration with Data Quality Services' an error will pop-up:

<img alt="" src="../wp-content/uploads/2013/05/052213_0830_MDSDQSinteg2.png" />

Here is where it gets a bit confusing. If you read the error message closely, it seems that MDS is looking for a local account on your machine instead of a domain account. However, with it being a domain controller, you cannot create local accounts…

To make this work you need to do the following:
<ol>
	<li>
<div>Add a Windows User Login into SQL Server for [YourDomain]\MDS_ServiceAccounts.</div>
<img alt="" src="../wp-content/uploads/2013/05/052213_0830_MDSDQSinteg3.png" />

&nbsp;</li>
	<li>Then run the following query against your DQS_MAIN database, which creates a user on the DQS_MAIN database which maps to the login you just created and adds the user to the DQS_Administrator role. Of course you can also do this using the UI. Make sure to enter your DOMAIN in the query below before executing.
<span style="font-size: 10pt;"><span style="font-size: 10pt;">
use [DQS_MAIN]
GO
IF NOT EXISTS (SELECT * FROM SYS.SYSUSERS WHERE NAME = 'MDS_ServiceAccounts')
CREATE USER [MDS_ServiceAccounts] FOR LOGIN [<strong>YourDomain</strong>\MDS_ServiceAccounts]
exec sp_addrolemember @rolename=N'dqs_administrator',@membername=N'MDS_ServiceAccounts'</span></span></li>
	<li>
<div>When done go back to the Master Data Services configuration manager and hit the button again. Now it should come back with:</div>
<img alt="" src="../wp-content/uploads/2013/05/052213_0830_MDSDQSinteg4.png" /></li>
</ol>
Victory ! <span style="font-family: Wingdings;">J</span>

&nbsp;