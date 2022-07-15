---
id: 875
title: 'CTP2 of the new SQL Server 2016 has been released to public'
date: '2015-05-28T12:43:53+01:00'
author: 'Harry Tolsma'
layout: post
guid: 'http://www.dutchdatadude.com/?p=875'
permalink: /ctp2-of-the-new-sql-server-2016-has-been-released-to-public/
categories:
    - Azure
    - 'SQL Server'
tags:
    - 'SQL 2016'
---

With this new beta release of SQL Server we get a better insight in what we can expect in the full product.
Some of the top capabilities in SQL Server 2016 CTP2 are:
<ul style="margin-left: 54pt;">
	<li>Real-time Operational Analytics &amp; In-Memory OLTP, enhanced for up to 30x faster transactions for a greater number of applications, customers can configure the in-memory columnstore to work on top of a transactional database to achieve real-time operational analytics with breakthrough OLTP performance.</li>
	<li>Always Encrypted helps protect data at rest, in motion and while in use, on-premises and in the cloud.
With Always Encrypted, SQL Server can perform operations on encrypted data.
Best of all the encryption key resides with the application in the customer's trusted environment.</li>
	<li>Stretch Database technology keeps historical data at users' fingertips by transparently stretching warm and cold data in a more secure manner to Microsoft Azure on demand without application changes.</li>
</ul>
I advise you to take a special look into the stretched databases.

It is a technique originating in Azure where it's already very easy to scale up or down on a working database.
And not only on a single database!
Also a set of databases (called Elastic Pool) can be tailored to meet the per time different demand of power for each individual database.
A brand new concept which you could use in use-cases like having a database per customer or project which scale needs are different in time and in database.

In my next blogpost I will dig deeper on the new concept of elastic database.

Harry