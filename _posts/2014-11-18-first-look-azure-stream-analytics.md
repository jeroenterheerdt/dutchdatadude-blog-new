---
id: 743
title: 'First Look: Azure Stream Analytics'
date: '2014-11-18T14:30:36+01:00'
author: 'Jeroen ter Heerdt'
layout: post
guid: 'http://www.dutchdatadude.com/?p=743'
permalink: /first-look-azure-stream-analytics/
categories:
    - Azure
    - 'Business Intelligence'
    - 'SQL Server'
tags:
    - CEP
    - 'First Look'
    - 'Stream Analytics'
---

<span style="color: #333333; font-family: Helvetica; font-size: 11pt;"><em>The First Look series focusses on new products, recent announcements, previews or things I have not had the time to provide a first look at and serves as introduction to the subject. First look posts are fairly short and high level.
</em></span>

<span style="color: #333333; font-family: Helvetica; font-size: 11pt;">Today in <em>First Look</em>: Azure Stream Analytics. This service is currently in preview and provides low latency, high available and scalable complex event processing in the cloud. To do complex event processing SQL Server has <a href="http://technet.microsoft.com/en-us/library/ee362541(v=sql.111).aspx">StreamInsight</a>; with Azure Stream Analytics we provide a CEP engine in the cloud.
</span>

<span style="color: #333333; font-family: Helvetica; font-size: 11pt;">Azure Stream Analytics is built to read data from a source, let's say a device sensor and collect, process and take action on it in a blink of the eye. A simple example would be to read temperatures from a sensor, aggregate them to calculate an average temperature per 5 seconds and store that data into SQL server. Or a fairly more complex example would be to take output from a video camera that reads license plates, run the license plate through a list of license plates of stolen cars and immediately send a message to a police car nearby.
</span>

<span style="color: #333333; font-family: Helvetica; font-size: 11pt;">Because this solution is cloud based it is easy to get started. You can be up and running in literally minutes.
</span>

More info is available on <a href="http://azure.microsoft.com/en-us/documentation/articles/stream-analytics-introduction/">http://azure.microsoft.com/en-us/documentation/articles/stream-analytics-introduction/</a>

More to come!