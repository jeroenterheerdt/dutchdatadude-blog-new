---
id: 829
title: 'Azure SQL Database almost on par with the on-premise version'
date: '2015-04-14T14:09:29+01:00'
author: 'Harry Tolsma'
layout: post
guid: 'http://www.dutchdatadude.com/?p=829'
permalink: /azure-sql-database-almost-on-par-with-the-on-premise-version/
categories:
    - Azure
    - PAAS
    - 'SQL Server'
tags:
    - 'SQL Azure'
---

Hi blogreaders <span style="font-family: Wingdings;">J</span>

I started the blog with the title: "Azure SQL Database almost on par with the on-premise version".

And looking from a T-SQL perspective it is.
Our latest version of Azure SQL Database (let's call it SQL Azure for now) is for 95% compatible with SQL 2014.
So not a bad title!

But there is more to it…

There are two perspectives to take in account here:
<ol>
	<li>Microsoft is not only working on T-SQL compatibility, but is working on al fronts to enhance functionality.
So actually… the engine powering SQL Azure is already beyond SQL 2014 and more towards SQL 2016.</li>
	<li>
<div>SQL Azure is a PAAS offering in Azure.
So… you don't only get the database, but also services around it in maintenance like:</div>
<ol>
	<li>Automatic replication of your date 3 times (and 3 more times if geo-redundant)</li>
	<li>Point in time restore up to 14 days</li>
	<li>Patching, security updates</li>
</ol>
</li>
</ol>
Thinking of SQL Azure of being on par with SQL 2014 is kind of old skool thinking.
Thinking of SQL Azure should be about thinking about using a relational database as a service.
And those services will enhance in time.

So no more thinking about versions, but thinking about functions.
This changes the paradigm of developing big time!
You will have to develop is a much more pure way.
Keeping your application architecture clean and crisp.

For example: No more business logic in database triggers, but logic in webservices and the call's to the database in as plain as ANSI-SQL as possible.
Code examples can be found at: <a href="https://msdn.microsoft.com/en-us/library/azure/ee621787.aspx">https://msdn.microsoft.com/en-us/library/azure/ee621787.aspx</a>
And to keep up to speed on the latest developments of SQL Azure keep checking the blog: <a href="http://azure.microsoft.com/blog/">http://azure.microsoft.com/blog/</a>

Happy programming!