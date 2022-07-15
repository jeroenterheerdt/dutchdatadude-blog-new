---
id: 590
title: 'Power BI Pro Tip: Troubleshooting Power BI Data Refresh'
date: '2014-04-08T15:00:20+01:00'
author: 'Jeroen ter Heerdt'
layout: post
guid: 'http://www.dutchdatadude.com/?p=590'
permalink: /power-bi-pro-tip-troubleshooting-power-bi-data-refresh/
categories:
    - 'Business Intelligence'
    - Office
    - 'SQL Server'
tags:
    - DMG
    - 'Office 365'
    - 'power bi'
---

With Power BI you can create an Excel sheet based on your data and then get it refreshed so your report always has the latest information.

If you run into trouble with this, here is how to troubleshoot the data refresh.
<ol>
	<li>Firstly, make sure you use Power Pivot to connect to your data source and not Power Query as refresh with Power Query is currently not supported.</li>
	<li>When making the connection to your data source, just use a regular data connection to the SQL Server source and not through an OData feed.</li>
	<li>In Power Pivot, make sure to use the same data provider as your data source has been configured to use in the Power BI Admin Portal (i.e. Native SQL or OLEDB) and enter the server and database name <strong>exactly</strong> the same as the data source has been configured in your Power BI Admin panel. With "exactly" I mean also casing: so <em>myServer</em> is something else than <em>MyServer</em>. So the server and database name needs to be identical, including casing.</li>
	<li>Finish your workbook and upload it.</li>
	<li>Make sure the Database Management Gateway is running. Do this by checking the status in the Power BI Admin Portal and check under Data Management Gateways.</li>
	<li>Next in the Power BI Admin Portal, check that the data sources have correct settings for server name and database name. Also check that the credentials entered here have permissions to the data sources on the server and have been re-entered after the last time the DMG has been registered. There is no harm in re-entering them just to be sure. Also check that the connection provider here matches the one used in Power Pivot and again the server and database name need to be exactly the same as in your Power Pivot connection settings (see item #3 above).</li>
	<li>In the Power BI Admin Portal, check that the user you will be using to schedule the refresh has permissions to do so on every data source you would like to refresh. Do this by opening the settings for the data source in the Power BI Admin Portal and making sure the user is listed under 'users and groups'.</li>
	<li>Plan the refresh on the file. When the schedule hits, your schedule should start and finish successfully.</li>
</ol>
&nbsp;