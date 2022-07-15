---
id: 465
title: 'Setup and register a Data Management Gateway for Power BI'
date: '2013-12-10T10:30:55+01:00'
author: 'Jeroen ter Heerdt'
layout: post
guid: 'http://www.dutchdatadude.com/?p=465'
permalink: /setup-and-register-a-data-management-gateway-for-power-bi/
categories:
    - 'Business Intelligence'
    - Office
    - SharePoint
    - 'SQL Server'
    - Uncategorized
tags:
    - DMG
    - 'power bi'
    - 'sql server'
---

In this post we will have a look at how to install, setup and register a Data Management Gateway for Power BI. It involves installing software on a server which will function as the gateway as well as configuration through the Power BI Admin Center. Once set up you can use the gateway to publish on-premises sources for use through Power BI.
<ol>
	<li>
<div>To create and register a Data Management Gateway follow these steps:</div>
<ol>
	<li>In the Power BI Admin Center, click gateways and click 'new gateway'.
<img alt="" src="../wp-content/uploads/2013/11/112013_1106_Setupandreg1.png" /></li>
	<li>Specify a name for the gateway and an optional description. Then, select 'Store the credentials securely in the cloud' to store credentials in the gateway rather than on the machine where the gateway is installed. Storing credentials in the cloud enables you to restore the gateway to another machine if the original one is lost. Click 'Next'.</li>
	<li>Click 'Create' to create the gateway. Then we need to copy the Gateway Key for later use. Click 'Download' to download the Data Management Gateway software. Install the software on your machine and start the Gateway Setup wizard.</li>
	<li>In the wizard paste the Gateway key you copied. Finally go to the Power BI Admin Center and click 'Finish'. Your gateway should now be listed as 'Online'.</li>
	<li>Switch back to your setup wizard and choose whether you want to use an existing certificate or a Power BI generated certificate to protect the credentials. Click 'Next'. On the specify endpoint access page specify if you want to use HTTP or HTTPs and make configuration settings accordingly. Click 'Next' and 'Finish' to close the wizard. Make sure the gateway name matches the name in the Admin Center and that is shows as Registered and Started.</li>
</ol>
</li>
</ol>
That's it! You have now successfully installed and registered a Data Magement Gateway for Power BI. Next up is creating sources. I'll discuss in a future post how to create an OData feed through the Power BI Admin Center.