---
id: 3064
title: 'Adding sequence numbers using R in Azure ML'
date: '2016-08-16T14:30:33+01:00'
author: 'Jeroen ter Heerdt'
layout: post
guid: 'http://www.dutchdatadude.com/?p=3064'
permalink: /adding-sequence-numbers-using-r-in-azure-ml/
categories:
    - Azure
    - 'Big Data'
tags:
    - 'Azure ML'
    - 'machine learning'
    - R
---

When going through data preparation sometimes sequence numbers need to be added. If you are like me, you probably spent some time looking for a component in Azure ML to do this. I never found it.

Turns out it is really easy to do this in R and as a result also very easy to do in Azure ML.

In your experiment, add an <strong>Execute R Script</strong> component and connect it to the data flow.

Edit the script and add a column to the dataset that equals:
<pre class="lang:r decode:true ">seq.int(nrow(dataset1))</pre>
See my code example:
<pre class="lang:r decode:true"># Map 1-based optional input ports to variables]
dataset1 &lt;- maml.mapInputPort(1) # class: data.frame
dataset1$time=seq.int(nrow(dataset1)) 
# Select data.frame to be sent to the output Dataset port 
maml.mapOutputPort("dataset1");</pre>
&nbsp;

On the third line the column is added and defined as a sequence number. The resulting dataset indeed has an extra column (called time) that like this:

<img src="../wp-content/uploads/2016/08/081016_1424_Addingseque1.png" alt="" />

The small histogram at the top and the details that right confirm it has only unique values and starts at 1; our sequence column has been added!