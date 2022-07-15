---
id: 2801
title: 'Azure Machine Learning pricing explained'
date: '2016-03-15T14:30:57+01:00'
author: 'Jeroen ter Heerdt'
layout: post
guid: 'http://www.dutchdatadude.com/?p=2801'
permalink: /azure-machine-learning-pricing-explained/
dsq_thread_id:
    - '6785496289'
categories:
    - Azure
    - 'Big Data'
tags:
    - azure
    - 'machine learning'
---

Many customers asked me questions on <a href="https://azure.microsoft.com/en-us/services/machine-learning/">Azure Machine Learning</a> (Microsoft's fully managed machine learning and data mining solution) and more specifically on it's <a href="https://azure.microsoft.com/en-us/pricing/details/machine-learning/">pricing</a>. In this post I will try to explain how the pricing works and what components you need to be aware of.

Azure Machine Learning is offered in two tiers: Free and Standard. The Free tier is obviously, well, free. It is however as you could expect limited compared to Standard. Differences are mostly in performance (multiple nodes for execution in standard vs. just one node in free) or storage (10 gb in free, unlimited in standard). There is no SLA for the free version, you cannot set up a production Web API to automate experiments in free and the staging web API is throttled.

For the standard tier, the following items need to be taken into consideration:
<ul>
	<li><strong>Seat;</strong> Azure ML has a monthly fee per seat, which translates to a user (mostly your data scientist) using the Azure ML web interface to develop and tune experiments. This price is per month per subscription/seat.</li>
	<li><strong>Studio usage</strong>; This is an hourly price for running experiments. You will pay this according to the number of hours your experiments run and thus claim computing resources.</li>
	<li><strong>API Usage</strong>; Azure ML allows you to bring an experiment online through the use of RESTful web services. This means you can automate score and training and have applications, websites, etc. use the experiment without human interference. With this you could do an automated credit scoring, recommendation or churn prediction directly from your app or website. In order to make this work you will need to create a web service in Azure ML (also called API). Azure ML charges per hour for compute used in an API that is production, so that is the fee you will need to pay per hour the web service / API is 'online' and usable. Also, you will need to pay per 1000 transactions. Transactions in this case are interactions with the API, such as one recommendation, one churn or one credit score.</li>
</ul>
&nbsp;

Hope this clarifies a bit. Please refer to the official page linked above&nbsp;for more details and for the pricing details.

&nbsp;