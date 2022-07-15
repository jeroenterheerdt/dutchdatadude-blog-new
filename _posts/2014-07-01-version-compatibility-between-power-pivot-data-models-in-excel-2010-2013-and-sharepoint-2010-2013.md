---
id: 673
title: 'Version compatibility between Power Pivot Data Models in Excel 2010 / 2013 and SharePoint 2010 / 2013'
date: '2014-07-01T15:30:31+01:00'
author: 'Jeroen ter Heerdt'
layout: post
guid: 'http://www.dutchdatadude.com/?p=673'
permalink: /version-compatibility-between-power-pivot-data-models-in-excel-2010-2013-and-sharepoint-2010-2013/
categories:
    - Office
    - SharePoint
    - 'SQL Server'
tags:
    - Excel
    - PowerPivot
    - sharepoint
---

I have been getting a lot of questions on compatibility around Excel 2010 / Excel 2013 / SharePoint 2010 / SharePoint 2013. To be honest, I have been confused myself.

I encourage you to check out <a href="http://office.microsoft.com/en-us/excel-help/version-compatibility-between-power-pivot-data-models-in-excel-2010-and-excel-2013-HA103929426.aspx">our Excel help page</a>, which makes it crystal clear:

<strong>Note to SharePoint Server 2010 customers:</strong> Client applications used to create a Data Model need to align with the server applications that host a Data Model. For SharePoint Server 2010, this means you’ll need to continue to use Excel 2010 and a Power Pivot for Excel add-in to create and maintain a Data Model. <strong>Excel 2013 cannot be used to create Data Models that run on SharePoint Server 2010.</strong>

This means that you <em>can</em> upload an Excel 2013 file with a Power Pivot data model in it to SharePoint. However, if you interact with it (click refresh, click a slicer, etc) you will get an error message.

It does not get any more specific than that, right?

&nbsp;

&nbsp;