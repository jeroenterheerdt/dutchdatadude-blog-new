---
id: 8
title: 'SQL Server 2012 Unboxing'
date: '2013-05-22T07:38:48+01:00'
author: 'Jeroen ter Heerdt'
layout: post
guid: 'http://www.dutchdatadude.com/?p=8'
permalink: /sql-server-2012-unboxing/
snap_isAutoPosted:
    - '1'
snapEdIT:
    - '1'
snapLI:
    - 's:391:"a:1:{i:0;a:8:{s:4:"doLI";s:1:"1";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:27:"New blog post on %SITENAME%";s:11:"SNAPformatT";s:18:"New Post - %TITLE%";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:123:"http://www.linkedin.com/updates?discuss=&amp;scope=15370591&amp;stype=M&amp;topic=5745043178013077504&amp;type=U&amp;a=BTbl";s:5:"pDate";s:19:"2013-05-28 07:10:31";}}";'
snapTW:
    - 's:243:"a:1:{i:0;a:7:{s:4:"doTW";s:1:"1";s:10:"SNAPformat";s:33:"Blogged: %TITLE% - %SURL% %htags%";s:8:"attchImg";s:1:"0";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:18:"339278758387269633";s:5:"pDate";s:19:"2013-05-28 07:15:34";}}";'
snapFB:
    - 's:152:"a:1:{i:0;a:4:{s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:28:"1327098618_10201316795425025";s:5:"pDate";s:19:"2013-05-28 07:25:21";}}";'
categories:
    - 'Business Intelligence'
    - 'SQL Server'
tags:
    - BI
    - 'business intelligence'
    - database
    - dqs
    - mds
    - 'sql server'
    - ssas
    - ssde
    - ssis
    - ssrs
    - streaminsight
---

Just about every new consumer technology device will be greeted with "unboxing" videos on YouTube. A lot of the people I talk to really need to start unboxing SQL Server 2012 and start to understand what is in the box. Most of them already have access to SQL Server 2012 and still think it is just a database. There is so much more! This post is aimed to providing a quick overview of what exactly is in the box with pointers to where you can find documentation.
<ol>
	<li><strong>Database Engine (SSDE)</strong>
First off, let's start with the product that gave SQL its name: the database. This is without doubt the best known product of the whole SQL suite and also the most used. More often than not this is also the only product people use and know. Find out more here: <a href="http://technet.microsoft.com/en-us/library/ms187875.aspx">http://technet.microsoft.com/en-us/library/ms187875.aspx</a></li>
	<li><strong>Data Quality Services (DQS / SSDQS)
</strong>Introduced with SQL Server 2012, DQS is a knowledge-driven data quality solution that works on the premise of specifying what defines data quality in a knowledge base and using to cleanse data automatically during ETL (see SSIS below), Master Data Management (see MDS below) processes or manually.
See: <a href="http://technet.microsoft.com/en-us/library/ff877925.aspx">http://technet.microsoft.com/en-us/library/ff877925.aspx</a></li>
	<li><strong>Analyis Services (SSAS)
</strong>Analysis Services is SQL Server's analytical database or cube. It features both more traditional cubes and tabular models, provides self-service analysis capabilities and includes data mining. See <a href="http://technet.microsoft.com/en-us/library/bb522607.aspx">http://technet.microsoft.com/en-us/library/bb522607.aspx</a></li>
	<li><strong>Integration Services (SSIS)
</strong>Integration Services is a full-blown ETL tool and can be used for all sorts of data integration solution. SSIS features a drag and drop interface to build the solution and provides a lot of components out of the box with connectors to and from just about any database, file storage or file format. If need be, you can also use the power of .NET to build the exact behavior required. SSIS also integrates with DQS to use data quality knowledge bases during ETL processes. For more info visit: <a href="http://technet.microsoft.com/en-us/library/ms141026.aspx">http://technet.microsoft.com/en-us/library/ms141026.aspx</a></li>
	<li><strong>Master Data Services (MDS)
</strong>Master Data Services enables users to build a Master Data Management solution on top of SQL Server. MDS integrates with DQS to make data quality aspects a part of the overall MDM solution. See <a href="http://technet.microsoft.com/en-us/library/ee633763.aspx">http://technet.microsoft.com/en-us/library/ee633763.aspx</a></li>
	<li><strong>Reporting Services (SSRS)
</strong>Reporting Services is the enterprise reporting solution that delivers web-enabled reports that can get information from a variety sources and be rendered in various formats (including Excel, Word and PDF). Also, reports can be retrieved on demand, on subscription bases or based on a alert. Find out more here: <a href="http://technet.microsoft.com/en-us/library/ms159106.aspx">http://technet.microsoft.com/en-us/library/ms159106.aspx</a></li>
	<li><strong>StreamInsight
</strong>StreamInsight is Microsoft's Complex Event Processor (CEP). CEP technology enables high throughput and real-time (low latency) processing of streams of data (events). Examples include financial trading, Web analytics, sensor data, etc. StreamInsight is provides a familiar development platform based on .NET to quickly start using real-time information. See: <a href="http://technet.microsoft.com/en-us/library/ee391416.aspx">http://technet.microsoft.com/en-us/library/ee391416.aspx</a></li>
</ol>
That concludes the quick unboxing of SQL Server 2012. Although there is a lot more to say (about features, but also around editions and capabilities) , this should give you a good idea of what is in the box. Bottom line: there is a lot more to SQL Server than just a database!