---
id: 816
title: 'Platform as a Service (PAAS) moving a rocket speed!'
date: '2015-03-23T09:08:48+01:00'
author: 'Harry Tolsma'
layout: post
guid: 'http://www.dutchdatadude.com/?p=816'
permalink: /platform-as-a-service-paas-moving-a-rocket-speed/
categories:
    - Azure
    - PAAS
    - 'SQL Server'
tags:
    - azure
    - 'big data'
    - 'sql server'
---

As an Enterprise Architect in an organization life has always been dynamic to say the least! It is your responsibility to keep up with the latest developments in ICT both in technique as in architecture. In the old days of on-premise only that was a big challenge. But with the Cloud as a integral part of your information systems it became even more complex.

But still… The Cloud was moving vm’s to Amazon or Microsoft. So architecturally not that complex. Identity &amp; access off course, but that’s about it. Then came Platform as a service (PAAS). That was something completely different! Not moving vm’s to the Cloud, but move complete technical workloads to the Cloud like an ESB in the Cloud, Media Services, Federated identity, Storage, etc, etc..

This does impact your architecture!

A blazing 78 new PAAS services were introduced in 2014 within Azure. So it's moving rocket fast! And to be fair: not only at Microsoft, also are other Cloud vendors moving into the PAAS area with new services.

What is the impact for you as Enterprise Architect?

In your normal day to day work you make choices based on software you can purchase and implement at your data center. But now you should at least ask yourself for every choice you have to make: Do I want to do this myself or shall I take this as a service from one of the Cloud vendors.

An example: Your organization wants to use Cloud services from multiple Cloud vendors but you want a single sign on experience for your users. Now you can buy a federated identity server, do research on all Cloud vendors on how to connect and then build the connections. But you can also use The Windows Azure Active Directory Federation Service (ADFS) from Microsoft with over 2600 Cloud vendors already pre-installed.

Second example: You have a new web application that you need to deploy. Again you can buy a few servers, install IIS, SQL Server, the application and install everything and schedule things like backup, patch management, storage, etc., etc. But you can also take a web-role to host the web-application, Azure SQL database to host you data and let Microsoft worry about backup’s, 3 replica’s for DR, patching the server, etc.., etc.

So my message to all you Enterprise Architects out there: Examine carefully the PAAS offerings from the Cloud vendors before making expensive buy decisions. My recommendations to checkout:

Azure Service Bus, Azure Machine Learning, WAAS, BizTalk Services and Azure SQL Database. Next blog-post I will dig deeper on Azure SQL Database.