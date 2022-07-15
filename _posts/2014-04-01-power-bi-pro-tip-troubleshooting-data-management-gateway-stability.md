---
id: 592
title: 'Power BI Pro Tip: Troubleshooting Data Management Gateway stability'
date: '2014-04-01T15:00:29+01:00'
author: 'Jeroen ter Heerdt'
layout: post
guid: 'http://www.dutchdatadude.com/?p=592'
permalink: /power-bi-pro-tip-troubleshooting-data-management-gateway-stability/
categories:
    - 'Business Intelligence'
    - Office
    - 'SQL Server'
tags:
    - DMG
    - 'Office 365'
    - 'power bi'
---

If your Data Management Gateway crashes a lot, just make sure you have .NET framework version 4.5.1 or later installed. 4.5.1. introduced fixes that the Data Management Gateway needs.

If you install it and reboot the server your DMG should be running much more smoothly.