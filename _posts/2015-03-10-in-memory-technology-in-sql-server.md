---
id: 810
title: 'In memory technology in SQL Server'
date: '2015-03-10T14:14:17+01:00'
author: 'Harry Tolsma'
layout: post
guid: 'http://www.dutchdatadude.com/?p=810'
permalink: /in-memory-technology-in-sql-server/
categories:
    - 'Big Data'
    - 'SQL Server'
tags:
    - 'In memory'
---

Everybody noticed the increase in technology using in memory techniques. At SAP they fully go for Hana, Oracle just started last year with in-memory database. At Microsoft we started in 2012 with in memory analytics and added OLPT in memory April 2014. The buzz is high with big marketing events, lots of whitepapers and broad press coverage.

So, but what about the real life practice?

When I visit my customers (top-50 in The Netherlands) I rarely see in memory databases used. So I always ask why they don’t make use of it. This resulted in the following reasons:
<ol>
	<li>I didn’t know I could run in memory with my databases.
The marketing engine could be hitting the wrong people. Lots of database administrators are not up to speed.</li>
	<li>We don’t do it because it must be very difficult.
True – if you use SAP then it’s common knowledge that implementing SAP Hana is not very easy. And you have to rewrite some of your programs. False – if you use Microsoft SQL Server. To start using in memory you can switch it on for certain tables (or part of tables) and without any change to the application it will work.</li>
	<li>The power of our servers is high enough. We don’t need the power.
This is of course a compliment that our SQL Servers run so smoothly (-:</li>
</ol>
But still I think that by using in memory technology you can achieve the following:
<ul>
	<li>Prevent hardware refresh. If servers run out of performance, moving to in memory the speeds increases again by 5x – 10x. Thus the servers can remain the same.</li>
	<li>Run more VM’s on a host. By using in memory technology the number of cores can be less because of the more economic processing in memory. Thus more core’s for new VM’s on the same host.</li>
	<li>Increase processing to reduce wait time for your users</li>
</ul>
So my advice: Start experimenting with the technology and look for those business cases.

My ask: anyone who has experience with the practical implementation: please reply with your live experience!