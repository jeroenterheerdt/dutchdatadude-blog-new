---
id: 134
title: 'Installing Master Data Services add-in for Excel 2013'
date: '2013-06-18T10:00:29+01:00'
author: 'Jeroen ter Heerdt'
layout: post
guid: 'http://www.dutchdatadude.com/?p=134'
permalink: /installing-master-data-services-add-in-for-excel-2013/
categories:
    - 'SQL Server'
    - Uncategorized
tags:
    - Excel
    - 'master data services'
    - mds
    - sql
    - 'sql server'
---

I recently picked up my new laptop, which of course runs Office 2013 and Windows 8.
When you try to install the Master Data Services add-in for SQL 2012 you may run into a warning that says you need Office 2010.

There is an easy fix: just install the Master Data Services add-in for SQL 2012 SP1 (get it here: <a href="http://www.microsoft.com/en-us/download/details.aspx?id=35581">http://www.microsoft.com/en-us/download/details.aspx?id=35581</a> . Be sure to pick 32 / 64 bit to match your Office version.

Oh and of course you will have to get the other pre-req as well: Visual Studio 2010 Tools for Office runtime (find it here: <a href="http://www.microsoft.com/en-my/download/details.aspx?id=35594">http://www.microsoft.com/en-my/download/details.aspx?id=35594</a>).

See <a href="http://support.microsoft.com/kb/2774422">http://support.microsoft.com/kb/2774422</a> for more information.