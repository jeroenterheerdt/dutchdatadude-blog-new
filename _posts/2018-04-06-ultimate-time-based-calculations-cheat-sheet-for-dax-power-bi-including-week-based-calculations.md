---
id: 4499
title: 'Ultimate Time Based Calculations Cheat Sheet for DAX / Power BI (including Week based calculations)'
date: '2018-04-06T12:55:08+01:00'
author: 'Jeroen ter Heerdt'
layout: post
guid: 'http://www.dutchdatadude.com/?p=4499'
permalink: /ultimate-time-based-calculations-cheat-sheet-for-dax-power-bi-including-week-based-calculations/
snap_isAutoPosted:
    - '1523015709'
dsq_thread_id:
    - '6784775024'
snap_MYURL:
    - ''
snapEdIT:
    - '1'
snapFB:
    - 's:1712:"a:1:{i:0;a:52:{s:11:"rpstBtwDays";s:0:"";s:11:"rpstRndMins";s:0:"";s:12:"rpstPostIncl";s:0:"";s:8:"rpstType";s:0:"";s:12:"rpstTimeType";s:0:"";s:12:"rpstFromTime";s:0:"";s:10:"rpstToTime";s:0:"";s:10:"rpstOLDays";s:0:"";s:10:"rpstNWDays";s:0:"";s:10:"nxsCPTSeld";s:0:"";s:7:"tagsSel";s:0:"";s:11:"rpstBtwHrsT";s:0:"";s:8:"tagsSelX";s:0:"";s:14:"rpstBtwHrsType";s:0:"";s:11:"rpstBtwHrsF";s:0:"";s:5:"nDays";s:0:"";s:4:"nHrs";s:0:"";s:5:"proxy";s:0:"";s:5:"fltrs";s:0:"";s:7:"fltrsOn";s:0:"";s:4:"nMin";s:0:"";s:5:"qTLng";s:0:"";s:1:"v";i:350;s:2:"do";s:1:"0";s:5:"nName";s:8:"Facebook";s:9:"msgFormat";s:51:"New post (%TITLE%) has been published on %SITENAME%";s:10:"msgAFormat";s:0:"";s:11:"msgATFormat";s:0:"";s:11:"msgACFormat";s:0:"";s:6:"appKey";s:15:"533598756698031";s:6:"appSec";s:32:"ddcec66dcd849101682d3c91c520435d";s:4:"pgID";s:16:"jeroen.terheerdt";s:11:"accessToken";s:164:"CAAHlTiRYd68BAGZBOGVnTztH7SdZCHK8nY18Bui0fUXlK38YrZBcgcmInOgcV6DI8IFZCvmjNv5K60ON1JGcLHufSFpS9L23M9IIAmVNrlj9N572gQf3Jw0GaFurjgmelznEdKzjZAnNCXqW6Y7ZBq3yRAtSR7XW8ZD";s:8:"authUser";s:10:"1327098618";s:12:"authUserName";s:0:"";s:15:"pageAccessToken";s:164:"CAAHlTiRYd68BAGZBOGVnTztH7SdZCHK8nY18Bui0fUXlK38YrZBcgcmInOgcV6DI8IFZCvmjNv5K60ON1JGcLHufSFpS9L23M9IIAmVNrlj9N572gQf3Jw0GaFurjgmelznEdKzjZAnNCXqW6Y7ZBq3yRAtSR7XW8ZD";s:15:"appsecret_proof";s:0:"";s:8:"postType";s:1:"A";s:10:"attachInfo";s:1:"F";s:6:"imgUpl";s:1:"T";s:5:"fbURL";s:41:"https://www.facebook.com/jeroen.terheerdt";s:8:"destType";s:0:"";s:11:"attachVideo";s:1:"N";s:10:"riComments";i:0;s:12:"riCommentsAA";i:0;s:3:"tpt";s:0:"";s:6:"isUpdd";s:1:"1";s:9:"isAutoImg";s:1:"A";s:8:"imgToUse";s:0:"";s:9:"isAutoURL";s:1:"A";s:8:"urlToUse";s:0:"";s:4:"doFB";i:0;}}";'
snapLI:
    - 's:1704:"a:1:{i:0;a:59:{s:11:"rpstBtwDays";s:0:"";s:11:"rpstRndMins";s:0:"";s:12:"rpstPostIncl";s:0:"";s:8:"rpstType";s:0:"";s:12:"rpstTimeType";s:0:"";s:12:"rpstFromTime";s:0:"";s:10:"rpstToTime";s:0:"";s:10:"rpstOLDays";s:0:"";s:10:"rpstNWDays";s:0:"";s:10:"nxsCPTSeld";s:0:"";s:7:"tagsSel";s:0:"";s:11:"rpstBtwHrsT";s:0:"";s:8:"tagsSelX";s:0:"";s:14:"rpstBtwHrsType";s:0:"";s:11:"rpstBtwHrsF";s:0:"";s:5:"nDays";s:0:"";s:4:"nHrs";s:0:"";s:5:"proxy";a:2:{s:5:"proxy";s:0:"";s:2:"up";s:0:"";}s:5:"fltrs";a:0:{}s:7:"fltrsOn";i:0;s:4:"nMin";s:0:"";s:5:"qTLng";s:0:"";s:1:"v";i:350;s:2:"do";s:1:"1";s:5:"nName";s:15:"Jeroen LinkedIn";s:8:"apiToUse";s:4:"liv1";s:6:"appKey";s:29:"x5g9a44j5j436s5j4u2a4k5q5z5g4";s:6:"appSec";s:37:"d3h0aq375d33534l3k3p4m5o5q5k306r2y2n3";s:13:"oAuthVerifier";s:5:"16590";s:11:"accessToken";s:36:"09e2d709-c080-4f95-bacb-7ffae841e396";s:14:"accessTokenSec";s:36:"bf0def89-59d8-48a3-86ff-2faa5304f35e";s:10:"oAuthToken";s:40:"78--ee0258f5-8c05-4738-800e-07bbcf16b61c";s:16:"oAuthTokenSecret";s:36:"ec2bec59-72e7-49e2-b39d-dc3dfe60a719";s:14:"accessTokenExp";s:0:"";s:8:"liUserID";s:0:"";s:10:"liUserInfo";s:30:"ohqYGF-_fJ - Jeroen ter Heerdt";s:7:"imgSize";s:0:"";s:9:"msgFormat";s:27:"New blog post on %SITENAME%";s:10:"msgAFormat";s:0:"";s:8:"postType";s:1:"A";s:5:"grpID";s:0:"";s:8:"whToPost";s:2:"PR";s:5:"pgcID";s:0:"";s:5:"pggID";s:0:"";s:4:"pgID";s:1:"p";s:5:"uPage";s:0:"";s:8:"inclTags";i:0;s:11:"msgCTFormat";s:7:"%TITLE%";s:10:"msgCFormat";s:9:"%RAWTEXT%";s:11:"msgATFormat";s:0:"";s:6:"isUpdd";s:1:"1";s:7:"proxyOn";i:0;s:9:"wpImgSize";s:4:"full";s:7:"useSURL";i:0;s:9:"isAutoImg";s:1:"A";s:8:"imgToUse";s:0:"";s:9:"isAutoURL";s:1:"A";s:8:"urlToUse";s:0:"";s:4:"doLI";i:0;}}";'
snapMD:
    - "s:510:\"a:1:{i:0;a:17:{s:2:\"do\";s:1:\"1\";s:5:\"nName\";s:13:\"Jeroen Medium\";s:9:\"msgFormat\";s:19:\"%FULLTEXT%\r\n\r\n%URL%\";s:10:\"msgTFormat\";s:7:\"%TITLE%\";s:6:\"appKey\";s:29:\"x5g9a44c464j584r25434i5h5i554\";s:6:\"appSec\";s:85:\"d3h0aq2745454i544w2l5a4a4h534j5r2x2z244a4s2b4a4e4z244s223v2s2s284m5z2n5u2a4x274742303\";s:7:\"fltrsOn\";i:0;s:5:\"fltrs\";a:0:{}s:7:\"proxyOn\";i:0;s:9:\"wpImgSize\";s:4:\"full\";s:7:\"useSURL\";i:0;s:1:\"v\";i:350;s:8:\"inclTags\";i:0;s:4:\"publ\";s:1:\"0\";s:9:\"isAutoURL\";s:1:\"A\";s:8:\"urlToUse\";s:0:\"\";s:4:\"doMD\";i:0;}}\";"
snapTW:
    - 's:1305:"a:1:{i:0;a:43:{s:11:"rpstBtwDays";s:0:"";s:11:"rpstRndMins";s:0:"";s:12:"rpstPostIncl";s:0:"";s:8:"rpstType";s:0:"";s:12:"rpstTimeType";s:0:"";s:12:"rpstFromTime";s:0:"";s:10:"rpstToTime";s:0:"";s:10:"rpstOLDays";s:0:"";s:10:"rpstNWDays";s:0:"";s:10:"nxsCPTSeld";s:0:"";s:7:"tagsSel";s:0:"";s:11:"rpstBtwHrsT";s:0:"";s:8:"tagsSelX";s:0:"";s:14:"rpstBtwHrsType";s:0:"";s:11:"rpstBtwHrsF";s:0:"";s:5:"nDays";s:0:"";s:4:"nHrs";s:0:"";s:5:"proxy";s:0:"";s:5:"fltrs";s:0:"";s:7:"fltrsOn";s:0:"";s:4:"nMin";s:0:"";s:5:"qTLng";s:0:"";s:1:"v";i:350;s:2:"do";s:1:"1";s:5:"nName";s:7:"Twitter";s:8:"attchImg";s:1:"0";s:9:"msgFormat";s:32:"New blog %TITLE% - %SURL% %TAGS%";s:6:"appKey";s:22:"BBCKMnAy6xa0OK3ZJOE2qQ";s:6:"appSec";s:40:"C6cruJh0ofbgG5J8DMBZPrPg8z8DJ0B5GQXIJQTM";s:5:"twURL";s:35:"https://twitter.com/jeroenterheerdt";s:11:"accessToken";s:50:"94532914-9xj4DdDhZrcH9lmr9jJwSKUkWl8AzKHto2j6hT18o";s:14:"accessTokenSec";s:43:"Kaa6LYwDhpweIREzi8QQgG0OPBwqVyAfWmzelZrUxSY";s:7:"imgSize";s:0:"";s:6:"isUpdd";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:18:"982225193836806146";s:7:"postURL";s:61:"https://twitter.com/jeroenterheerdt/status/982225193836806146";s:5:"pDate";s:19:"2018-04-06 11:55:10";s:9:"isAutoImg";s:1:"A";s:8:"imgToUse";s:0:"";s:9:"isAutoURL";s:1:"A";s:8:"urlToUse";s:0:"";s:4:"doTW";i:0;}}";'
categories:
    - 'Business Intelligence'
tags:
    - DAX
    - 'power bi'
    - 'time intelligence'
    - weeks
---

Power BI provides great time intelligence features to calculate Year-to-date (YTD), Month-to-date (MTD) and Quarter-to-date (QTD) totals. There is no such thing as Week-to-date (WTD) or Period-to-date (PTD) where period could be any arbitrary period definition (I used two-month periods in my example below). If you want those, you will have to create the calculations yourself. I was inspired by<a href="https://www.sqlbi.com/articles/week-based-time-intelligence-in-dax/"> this excellent blog post</a> and created an ultimate time-intelligence calculations Power BI file. I used <a href="https://www.mattmasson.com/2014/02/creating-a-date-dimension-with-a-power-query-script/">Matt Massons excellent date dimension generation script</a> to generate the date table for my example.

<a href="https://wp.me/a3AIGJ-1aO">Download the full Power BI file here</a> or <a href="https://wp.me/a3AIGJ-1aM">get just the DAX formulas</a>. Enjoy!

<strong>Basic Measures</strong>

<ul>
    <li>Total Amount:
<pre class="lang:c# decode:true">TotalAmount = SUM(Sales[Amount])</pre>
</li>
    <li>Total Quantity:
<pre class="lang:c# decode:true">TotalQuantity = SUM(Sales[Quantity])</pre>
</li>
</ul>

<strong>Day Measures</strong>

<ul>
    <li>Total Amount for Last Day (Yesterday)
<pre class="lang:c# decode:true ">Amount_LastDay = CALCULATE([TotalAmount],PREVIOUSDAY('Date'[Date]))</pre>
</li>
    <li>Total Amount for same Day last Year
<pre class="lang:c# decode:true ">Amount_SameDayLastYear = CALCULATE([TotalAmount],SAMEPERIODLASTYEAR('Date'[Date]))</pre>
</li>
    <li>Variance of total Amount compared to Total Amount for Last Day
<pre class="lang:c# decode:true ">Amount_DOD_Variance = [TotalAmount]-[Amount_LastDay]</pre>
</li>
    <li>Variance % of total Amount compared to Total Amount for Last Day
<pre class="lang:c# decode:true ">Amount_DOD_Variance% = DIVIDE([Amount_DOD_Variance],[Amount_LastDay])</pre>
</li>
    <li>Variance of total Amount compared to Total Amount for same Day last Year
<pre class="lang:c# decode:true ">Amount_YOY_Variance = [TotalAmount]-[Amount_SameDayLastYear]</pre>
</li>
    <li>Variance % of total Amount compared to Total Amount same Day last Year
<pre class="lang:c# decode:true ">Amount_YOY_Variance% = DIVIDE([Amount_YOY_Variance],[Amount_LastDay])</pre>
</li>
    <li>Total Quantity for Last Day (Yesterday)
<pre class="lang:c# decode:true ">Quantity_LastDay = CALCULATE([TotalQuantity],PREVIOUSDAY('Date'[Date]))</pre>
</li>
    <li>Total Quantity for same Day last Year
<pre class="lang:c# decode:true ">Quantity_SameDayLastYear = CALCULATE([TotalQuantity],SAMEPERIODLASTYEAR('Date'[Date]))</pre>
</li>
    <li>Variance of total Quantity compared to Total Quantity for Last Day
<pre class="lang:c# decode:true ">Quantity_DOD_Variance = [TotalQuantity]-[Quantity_LastDay]</pre>
</li>
    <li>Variance % of total Quantity compared to Total Quantity for Last Day
<pre class="lang:c# decode:true ">Quantity_DOD_Variance% = DIVIDE([Quantity_DOD_Variance],[Quantity_LastDay])</pre>
</li>
    <li>Variance of total Quantity compared to total Quantity for same Day last Year
<pre class="lang:c# decode:true ">Quantity_YOY_Variance = [TotalQuantity]-[Quantity_SameDayLastYear]</pre>
</li>
    <li>Variance % of total Quantity compared to total Quantity for same Day last Year
<pre class="lang:c# decode:true ">Quantity_YOY_Variance% = DIVIDE([Quantity_YOY_Variance],[Quantity_LastDay])</pre>
</li>
</ul>

<strong>Week Measures</strong>

<ul>
    <li>Total Amount Week To Date
<pre class="lang:c# decode:true ">Amount_WTD = IF (
    HASONEVALUE ( 'Date'[Year] )
        &amp;&amp; HASONEVALUE ('Date'[WeekNumber] ), CALCULATE(
        [TotalAmount],
        FILTER (
            ALL ( 'Date' ),
            'Date'[Year] = VALUES ( 'Date'[Year] )
                &amp;&amp; 'Date'[WeekNumber] = VALUES ( 'Date'[WeekNumber] )
                &amp;&amp; 'Date'[Date] &lt;= MAX ( 'Date'[Date] )
        )
    ))</pre>
</li>
    <li>Total Amount for Last Week
<pre class="lang:c# decode:true ">Amount_LastWeek = SUMX(
    FILTER(ALL('Date'),
        IF(SELECTEDVALUE('Date'[WeekNumber])=1,
            'Date'[WeekNumber]=CALCULATE(MAX('Date'[WeekNumber]), ALL('Date')) &amp;&amp; 'Date'[Year]=FORMAT(VALUE(SELECTEDVALUE('Date'[Year]))-1,""),
            'Date'[WeekNumber]=SELECTEDVALUE('Date'[WeekNumber])-1 &amp;&amp; 'Date'[Year]=FORMAT(VALUE(SELECTEDVALUE('Date'[Year])),""))
    ),
    [TotalAmount])</pre>
</li>
    <li>Total Amount for same Week Last Year
<pre class="lang:c# decode:true ">Amount_SameWeekLastYear = IF (
    HASONEVALUE ( 'Date'[Year] )
        &amp;&amp; HASONEVALUE ('Date'[WeekNumber] ), CALCULATE(
        SUM ( Sales[Amount] ),
        FILTER (
            ALL ( 'Date' ),
            'Date'[Year] = FORMAT(VALUES ( 'Date'[Year] )-1,"")
                &amp;&amp; 'Date'[WeekNumber] = VALUES ( 'Date'[WeekNumber] )
                &amp;&amp; 'Date'[Date] &lt;= MAX ( 'Date'[Date] )
        )
    ))</pre>
</li>
    <li>Variance of total Amount Week To Date compared to Total Amount for Last Week
<pre class="lang:c# decode:true ">Amount_WTD_WOW_Variance = [Amount_WTD]-[Amount_LastWeek]</pre>
</li>
    <li>Variance % of total Amount Week To Date compared to Total Amount for Last Week
<pre class="lang:c# decode:true ">Amount_WTD_WOW_Variance% = DIVIDE([Amount_WTD_WOW_Variance],[Amount_LastWeek])</pre>
</li>
    <li>Variance of total Amount Week to Date compared to Total Amount for same Week last Year
<pre class="lang:c# decode:true ">Amount_WTD_YOY_Variance = [Amount_WTD]-[Amount_SameWeekLastYear]</pre>
</li>
    <li>Variance % of total Amount Week to Date compared to Total Amount for same Week last Year
<pre class="lang:c# decode:true ">Amount_WTD_YOY_Variance% = DIVIDE([Amount_WTD_YOY_Variance],[Amount_SameWeekLastYear])</pre>
</li>
    <li>Total Quantity Week To Date
<pre class="lang:c# decode:true ">Quantity_WTD = IF (
    HASONEVALUE ( 'Date'[Year] )
        &amp;&amp; HASONEVALUE ('Date'[WeekNumber] ),
    CALCULATE (
        [TotalQuantity],
        FILTER (
            ALL ( 'Date' ),
            'Date'[Year] = VALUES ( 'Date'[Year] )
                &amp;&amp; 'Date'[WeekNumber] = VALUES ( 'Date'[WeekNumber] )
                &amp;&amp; 'Date'[Date] &lt;= MAX ( 'Date'[Date] )
        )
    ),
    BLANK ()
)</pre>
</li>
    <li>Total Quantity for same Week Last Year
<pre class="lang:c# decode:true ">Quantity_SameWeekLastYear = IF (
    HASONEVALUE ( 'Date'[Year] )
        &amp;&amp; HASONEVALUE ('Date'[WeekNumber] ), CALCULATE(
        SUM ( Sales[Quantity] ),
        FILTER (
            ALL ( 'Date' ),
            'Date'[Year] = FORMAT(VALUES ( 'Date'[Year] )-1,"")
                &amp;&amp; 'Date'[WeekNumber] = VALUES ( 'Date'[WeekNumber] )
                &amp;&amp; 'Date'[Date] &lt;= MAX ( 'Date'[Date] )
        )
    ))</pre>
</li>
    <li>Total Quantity for Last Week
<pre class="lang:c# decode:true ">Quantity_LastWeek = SUMX(
    FILTER(ALL('Date'),
        IF(SELECTEDVALUE('Date'[WeekNumber])=1,
            'Date'[WeekNumber]=CALCULATE(MAX('Date'[WeekNumber]), ALL('Date')) &amp;&amp; 'Date'[Year]=FORMAT(VALUE(SELECTEDVALUE('Date'[Year]))-1,""),
            'Date'[WeekNumber]=SELECTEDVALUE('Date'[WeekNumber])-1 &amp;&amp; 'Date'[Year]=FORMAT(VALUE(SELECTEDVALUE('Date'[Year])),""))
    ),
    [TotalQuantity])</pre>
</li>
    <li>Variance of total Quantity Week To Date compared to Total Quantity for Last Week
<pre class="lang:c# decode:true ">Quantity_WTD_WOW_Variance = [Quantity_WTD]-[Quantity_LastWeek]</pre>
</li>
    <li>Variance % of total Quantity Week To Date compared to Total Quantity for Last Week
<pre class="lang:c# decode:true ">Quantity_WTD_WOW_Variance% = DIVIDE([Quantity_WTD_WOW_Variance],[Quantity_LastWeek])</pre>
</li>
    <li>Variance of total Quantity Week to Date compared to Total Quantity for same Week last Year
<pre class="lang:c# decode:true ">Quantity_WTD_YOY_Variance = [Quantity_WTD]-[Quantity_SameWeekLastYear]</pre>
</li>
    <li>Variance % of total Quantity Week to Date compared to Total Quantity for same Week last Year
<pre class="lang:c# decode:true ">Quantity_WTD_YOY_Variance% = DIVIDE([Quantity_WTD_YOY_Variance],[Quantity_SameWeekLastYear])</pre>
</li>
</ul>

<strong>Month Measures</strong>

<ul>
    <li>Total Amount Month To Date
<pre class="lang:c# decode:true ">Amount_MTD = TOTALMTD([TotalAmount],'Date'[Date])</pre>
</li>
    <li>Total Amount for same Month Last Year
<pre class="lang:c# decode:true ">Amount_SameMonthLastYear = CALCULATE([Amount_MTD],SAMEPERIODLASTYEAR('Date'[Date]))</pre>
</li>
    <li>Total Amount for Last Month
<pre class="lang:c# decode:true ">Amount_LastMonth = CALCULATE([TotalAmount],PREVIOUSMONTH('Date'[Date]))</pre>
</li>
    <li>Variance of total Amount Month To Date compared to Total Amount for Last Month
<pre class="lang:c# decode:true ">Amount_MTD_MOM_Variance = [Amount_MTD]-[Amount_LastMonth]</pre>
</li>
    <li>Variance % of total Amount Month To Date compared to Total Amount for Last Month
<pre class="lang:c# decode:true ">Amount_MTD_MOM_Variance% = DIVIDE([Amount_MTD_MOM_Variance],[Amount_LastMonth])</pre>
</li>
    <li>Variance of total Amount Month to Date compared to Total Amount for same Month last Year
<pre class="lang:c# decode:true ">Amount_MTD_YOY_Variance = [Amount_MTD]-[Amount_SameMonthLastYear]</pre>
</li>
    <li>Variance % of total Amount Month to Date compared to Total Amount for same Month last Year
<pre class="lang:c# decode:true ">Amount_MTD_YOY_Variance% = DIVIDE([Amount_MTD_YOY_Variance],[Amount_SameMonthLastYear])</pre>
</li>
    <li>Total Quantity Month To Date
<pre class="lang:c# decode:true ">Quantity_MTD = TOTALMTD([TotalQuantity],'Date'[Date])</pre>
</li>
    <li>Total Quantity for same Month Last Year
<pre class="lang:c# decode:true ">Quantity_SameMonthLastYear = CALCULATE([Quantity_MTD],SAMEPERIODLASTYEAR('Date'[Date]))</pre>
</li>
    <li>Total Quantity for Last Month
<pre class="lang:c# decode:true ">Quantity_LastMonth = CALCULATE([TotalQuantity],PREVIOUSMONTH('Date'[Date]))</pre>
</li>
    <li>Variance of total Quantity Month To Date compared to Total Quantity for Last Month
<pre class="lang:c# decode:true ">Quantity_MTD_MOM_Variance = [Quantity_MTD]-[Quantity_LastMonth]</pre>
</li>
    <li>Variance % of total Quantity Month To Date compared to Total Quantity for Last Month
<pre class="lang:c# decode:true ">Quantity_MTD_MOM_Variance% = DIVIDE([Quantity_MTD_MOM_Variance],[Quantity_LastMonth])</pre>
</li>
    <li>Variance of total Quantity Month to Date compared to Total Quantity for same Month last Year
<pre class="lang:c# decode:true ">Quantity_MTD_YOY_Variance = [Quantity_MTD]-[Quantity_SameMonthLastYear]</pre>
</li>
    <li>Variance % of total Quantity Month to Date compared to Total Quantity for same Month last Year
<pre class="lang:c# decode:true ">Quantity_MTD_YOY_Variance% = DIVIDE([Quantity_MTD_YOY_Variance],[Quantity_SameMonthLastYear])</pre>
</li>
</ul>

<strong>Period Measures</strong>

<ul>
    <li>Total Amount Period To Date
<pre class="lang:c# decode:true">Amount_PTD = IF (
    HASONEVALUE ( 'Date'[Year] )
        &amp;&amp; HASONEVALUE ('Date'[TwoMonthPeriod] ),
    CALCULATE (
        [TotalAmount],
        FILTER (
            ALL ( 'Date' ),
            'Date'[Year] = VALUES ( 'Date'[Year] )
                &amp;&amp; 'Date'[TwoMonthPeriod] = VALUES ( 'Date'[TwoMonthPeriod] )
                &amp;&amp; 'Date'[Date] &lt;= MAX ( 'Date'[Date] )
        )
    ),
    BLANK ()
)</pre>
</li>
    <li>Total Amount for same Period Last Year
<pre class="lang:c# decode:true ">Amount_SamePeriodLastYear = CALCULATE([Amount_PTD],SAMEPERIODLASTYEAR('Date'[Date]))</pre>
</li>
    <li>Total Amount for Last Period
<pre class="lang:c# decode:true ">Amount_LastPeriod = CALCULATE([TotalAmount],DATEADD('Date'[Date],-2,MONTH))</pre>
</li>
    <li>Variance of total Amount Period To Date compared to Total Amount for Last Period
<pre class="lang:c# decode:true ">Amount_PTD_POP_Variance = [Amount_PTD]-[Amount_LastPeriod]</pre>
</li>
    <li>Variance % of total Amount Period To Date compared to Total Amount for Last Period
<pre class="lang:c# decode:true ">Amount_PTD_POP_Variance% = DIVIDE([Amount_PTD_POP_Variance],[Amount_LastPeriod])</pre>
</li>
    <li>Variance of total Amount Period to Date compared to Total Amount for same Period last Year
<pre class="lang:c# decode:true ">Amount_PTD_YOY_Variance = [Amount_PTD]-[Amount_SamePeriodLastYear]</pre>
</li>
    <li>Variance % of total Amount Period to Date compared to Total Amount for same Period last Year
<pre class="lang:c# decode:true ">Amount_PTD_YOY_Variance% = DIVIDE([Amount_PTD_YOY_Variance],[Amount_SamePeriodLastYear])</pre>
</li>
    <li>Total Quantity Period To Date
<pre class="lang:c# decode:true ">Quantity_PTD = IF (
    HASONEVALUE ( 'Date'[Year] )
        &amp;&amp; HASONEVALUE ('Date'[TwoMonthPeriod] ),
    CALCULATE (
        [TotalQuantity],
        FILTER (
            ALL ( 'Date' ),
            'Date'[Year] = VALUES ( 'Date'[Year] )
                &amp;&amp; 'Date'[TwoMonthPeriod] = VALUES ( 'Date'[TwoMonthPeriod] )
                &amp;&amp; 'Date'[Date] &lt;= MAX ( 'Date'[Date] )
        )
    ),
    BLANK ()
)</pre>
</li>
    <li>Total Quantity for same Period Last Year
<pre class="lang:c# decode:true ">Quantity_SamePeriodLastYear = CALCULATE([Quantity_PTD],SAMEPERIODLASTYEAR('Date'[Date]))</pre>
</li>
    <li>Total Quantity for Last Period
<pre class="lang:c# decode:true ">Quantity_LastPeriod = CALCULATE([TotalQuantity],DATEADD('Date'[Date],-2,MONTH))</pre>
</li>
    <li>Variance of total Quantity Period To Date compared to Total Quantity for Last Period
<pre class="lang:c# decode:true ">Quantity_PTD_POP_Variance = [Quantity_PTD]-[Quantity_LastPeriod]</pre>
</li>
    <li>Variance % of total Quantity Period To Date compared to Total Quantity for Last Period
<pre class="lang:c# decode:true ">Quantity_PTD_POP_Variance% = DIVIDE([Quantity_PTD_POP_Variance],[Quantity_LastPeriod])</pre>
</li>
    <li>Variance % of total Quantity Period to Date compared to Total Quantity for same Period last Year
<pre class="lang:c# decode:true ">Quantity_PTD_YOY_Variance = [Quantity_PTD]-[Quantity_SamePeriodLastYear]</pre>
</li>
    <li>Variance of total Quantity Period to Date compared to Total Quantity for same Period last Year
<pre class="lang:c# decode:true ">Quantity_PTD_YOY_Variance% = DIVIDE([Quantity_PTD_YOY_Variance],[Quantity_SamePeriodLastYear])</pre>
</li>
</ul>

<strong>Quarter Measures</strong>

<ul>
    <li>Total Amount Quarter To Date
<pre class="lang:c# decode:true ">Amount_QTD = TOTALQTD([TotalAmount],'Date'[Date])</pre>
</li>
    <li>Total Amount for same Quarter Last Year
<pre class="lang:c# decode:true ">Amount_SameQuarterLastYear = CALCULATE([Amount_QTD],SAMEPERIODLASTYEAR('Date'[Date]))</pre>
</li>
    <li>Total Amount for Last Quarter
<pre class="lang:c# decode:true ">Amount_LastQuarter = CALCULATE([TotalAmount],PREVIOUSQUARTER('Date'[Date]))</pre>
</li>
    <li>Variance of total Amount Quarter To Date compared to Total Amount for Last Quarter
<pre class="lang:c# decode:true ">Amount_QTD_QOQ_Variance = [Amount_QTD]-[Amount_LastQuarter]</pre>
</li>
    <li>Variance % of total Amount Quarter To Date compared to Total Amount for Last Quarter
<pre class="lang:c# decode:true ">Amount_QTD_QOQ_Variance% = DIVIDE([Amount_QTD_QOQ_Variance],[Amount_LastQuarter])</pre>
</li>
    <li>Variance of total Amount Quarter to Date compared to Total Amount for same Quarter last Year
<pre class="lang:c# decode:true ">Amount_QTD_YOY_Variance = [Amount_QTD]-[Amount_SameQuarterLastYear]</pre>
</li>
    <li>Variance % of total Amount Quarter to Date compared to Total Amount for same Quarter last Year
<pre class="lang:c# decode:true ">Amount_QTD_YOY_Variance% = DIVIDE([Amount_QTD_YOY_Variance],[Amount_SameQuarterLastYear])</pre>
</li>
    <li>Total Quantity Quarter To Date
<pre class="lang:c# decode:true ">Quantity_QTD = TOTALQTD([TotalQuantity],'Date'[Date])</pre>
</li>
    <li>Total Quantity for same Quarter Last Year
<pre class="lang:c# decode:true ">Quantity_SameQuarterLastYear = CALCULATE([Quantity_QTD],SAMEPERIODLASTYEAR('Date'[Date]))</pre>
</li>
    <li>Total Quantity for Last Quarter
<pre class="lang:c# decode:true ">Quantity_LastQuarter = CALCULATE([TotalQuantity],PREVIOUSQUARTER('Date'[Date]))</pre>
</li>
    <li>Variance of total Quantity Quarter To Date compared to Total Quantity for Last Quarter
<pre class="lang:c# decode:true ">Quantity_QTD_QOQ_Variance = [Quantity_QTD]-[Quantity_LastQuarter]</pre>
</li>
    <li>Variance % of total Quantity Quarter To Date compared to Total Quantity for Last Quarter
<pre class="lang:c# decode:true ">Quantity_QTD_QOQ_Variance% = DIVIDE([Quantity_QTD_QOQ_Variance],[Quantity_LastQuarter])</pre>
</li>
    <li>Variance of total Quantity Quarter To Date compared to Total Quantity or same Quarter last Year
<pre class="lang:c# decode:true ">Quantity_QTD_YOY_Variance = [Quantity_QTD]-[Quantity_SameQuarterLastYear]</pre>
</li>
    <li>Variance % of total Quantity Quarter To Date compared to Total Quantity for same Quarter last Year
<pre class="lang:c# decode:true ">Quantity_QTD_YOY_Variance% = DIVIDE([Quantity_QTD_YOY_Variance],[Quantity_SameQuarterLastYear])</pre>
</li>
</ul>

<strong>Year Measures</strong>

<ul>
    <li>Total Amount Year To Date
<pre class="lang:c# decode:true ">Amount_YTD = TOTALYTD([TotalAmount],'Date'[Date])</pre>
</li>
    <li>Total Amount for Last Year
<pre class="lang:c# decode:true ">Amount_LastYear = CALCULATE([Amount_YTD],PREVIOUSYEAR('Date'[Date]))</pre>
</li>
    <li>Variance of total Amount Year To Date compared to Total Amount for Last Year
<pre class="lang:c# decode:true ">Amount_YTD_YOY_Variance = [Amount_YTD]-[Amount_LastYear]</pre>
</li>
    <li>Variance% of total Amount Year To Date compared to Total Amount for Last Year
<pre class="lang:c# decode:true ">Amount_YTD_YOY_Variance% = DIVIDE([Amount_YTD_YOY_Variance],[Amount_LastYear])</pre>
</li>
    <li>Total Quantity Year To Date
<pre class="lang:c# decode:true ">Quantity_YTD = TOTALYTD([TotalQuantity],'Date'[Date])</pre>
</li>
    <li>Total Quantity for Last Year
<pre class="lang:c# decode:true ">Quantity_LastYear = CALCULATE([TotalQuantity],PREVIOUSYEAR('Date'[Date]))</pre>
</li>
    <li>Variance of total Quantity Year To Date compared to Total Quantity for Last Year
<pre class="lang:c# decode:true ">Quantity_YTD_YOY_Variance = -[Quantity_YTD]-[Quantity_LastYear]</pre>
</li>
    <li>Variance% of total Quantity Year To Date compared to Total Quantity for Last Year
<pre class="lang:c# decode:true ">Quantity_YTD_YOY_Variance% = DIVIDE([Quantity_YTD_YOY_Variance],[Quantity_LastYear])</pre>
</li>
</ul>