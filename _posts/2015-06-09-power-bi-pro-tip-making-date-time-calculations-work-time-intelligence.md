---
id: 873
title: 'Power BI Pro Tip: making date / time calculations work (Time Intelligence)'
date: '2015-06-09T14:30:20+01:00'
author: 'Jeroen ter Heerdt'
layout: post
guid: 'http://www.dutchdatadude.com/?p=873'
permalink: /power-bi-pro-tip-making-date-time-calculations-work-time-intelligence/
categories:
    - 'Big Data'
    - 'Business Intelligence'
    - Office
tags:
    - DAX
    - 'power bi'
    - PowerPivot
---

Ever so often I get asked how to do a year-over-year, quarter-over-quarter, month-over-month or year-vs-year calculation in Power BI. In most cases people would like to create a KPI to measure a certain periods performance compared to another. Power BI (specifically DAX) provides great functions for this; <a href="https://support.office.com/en-us/article/Time-Intelligence-in-Power-Pivot-in-Excel-2013-016ACF7B-9DED-411E-BA6C-ED8B8C368011">the Time Intelligence functions</a>. In this scenarios PREVIOUSMONTH, PREVIOUSYEAR, SAMEPERIODLASTYEAR are used most. However, there are some frequent mistakes that result in errors when using these functions:

1) You will need to have a Date table in your model. Technically you do not need one, but you need to make sure the column you use for the time based calculations contains only unique values/dates. This is often not the case with sales happening more than once a day! Once you have the date table in the model, make sure to create a relationship between your facts date (for example sales date) and the date table.

2) The time intelligence functions should really be used as measures; not as calculated columns. This means their position in the Excel PowerPivot 2013 screen is under the horizontal line, not in the columns above.

3) Time intelligence functions work best when using totals, averages or other aggregated info.

Here are some examples. I will use 'Date'[Date] as the reference to my date column in my date table. Also, for a best practice I split the calculation in two parts: the first part just calculates the total sales, while the other calculations refer to that base calculation.
<pre class="lang:c# decode:true">Sales:=SUM([SalesAmount])
SalesPreviousYear:=[Sales](PREVIOUSYEAR('Date'[Date]))
SalesPreviousMonth:=[Sales](PREVIOUSMONTH('Date'[Date]))
SalesSamePeriodLastYear:=[Sales](SAMEPERIODLASTYEAR('Date'[Date]))</pre>
Note that the last one uses SAMEPERIODLASTYEAR which is more flexible as it will select the same day in the previous year or the same month in the previous year depending on the selection the user makes in the tables/graphs. This is however not always what you want; so you can make it more specific by using PREVIOUSYEAR / PREVIOUSMONTH etc.

You could also use DATEADD to be even more flexible:
<pre class="lang:c# decode:true">Sales14DaysBack:=[Sales](DATEADD('Date'[Date],-14,DAY))</pre>
Notice by the way that I tend to use the short-hand notation to prevent me from having to type CALCULATE all the time (yes I am lazy :)). Here is an example of the two ways to get the sales for the previous year, the first line is the short-hand, the second is the more elaborate but not less correct option:
<pre class="lang:c# decode:true">SalesPreviousYearShortHand:=[Sales](PREVIOUSYEAR('Date'[Date]))
SalesPreviousYear:=CALCULATE([Sales];PREVIOUSYEAR('Date'[Date]))</pre>
Hope this helps!

&nbsp;