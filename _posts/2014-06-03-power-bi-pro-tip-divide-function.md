---
id: 639
title: 'Power BI Pro Tip: DIVIDE() function'
date: '2014-06-03T15:30:22+01:00'
author: 'Jeroen ter Heerdt'
layout: post
guid: 'http://www.dutchdatadude.com/?p=639'
permalink: /power-bi-pro-tip-divide-function/
categories:
    - 'Business Intelligence'
    - Office
    - Uncategorized
tags:
    - 'power bi'
    - 'Power Pivot'
---

If you ever used Power Pivot to calculate things such as sales amount per capita or averages of some sort you will have run into the situation that the denominator (the column you want to divide by) is empty or zero. To cope with a potential division by zero, Power Pivot outputs Infinity. This can be seen in the screenshot below where the 'Per Capita' column is defined as:
<pre class="lang:c# decode:true">=[SalesAmount]/[Numer of citizens]</pre>
Of course you can fix this by using
<pre class="lang:c# decode:true">IF(ISBLANK([InputColumn]))</pre>
and others to work around the error. However, the DIVIDE() function makes this all a lot easier!

The DIVIDE() function takes two required and one optional parameters, which are: numerator, denominator and an optional value to return when division by zero occurs.

To see what DIVIDE() does, consider the following screenshot:

<img src="../wp-content/uploads/2014/05/052714_1253_PowerBIProT2.png" alt="" />

The Divide1 column here is defined as:
<pre class="lang:c# decode:true">=DIVIDE([SalesAmount];[Number of citizens])</pre>
W<span style="font-size: 11pt;">hereas the Divide2 column contains the following function: </span>
<pre class="lang:c# decode:true">=DIVIDE([SalesAmount];[Number of citizens];0)</pre>
&nbsp;

<span style="font-size: 11pt;">The results are great, no Infinities are returned! By default DIVIDE() returns empty in case of a problem (Divide1 column). You can override this by specifying the third parameter so to return a fixed value in cased of a problem (Divide2 column in my example).</span>

<span style="font-size: 11pt;">Hope this helps!</span>