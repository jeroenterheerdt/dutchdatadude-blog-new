---
id: 3106
title: 'Passing filters to Power BI reports using the URL / query string'
date: '2016-12-02T10:16:49+01:00'
author: 'Jeroen ter Heerdt'
layout: post
guid: 'http://www.dutchdatadude.com/?p=3106'
permalink: /passing-filters-to-power-bi-reports-using-the-url-query-string/
categories:
    - Azure
    - 'Big Data'
    - 'Business Intelligence'
tags:
    - 'power bi'
---

<p>It was only recently that I discovered this – you can pass filters to Power BI reports by deep linking to it and adding a filter in the URL (also called query string). I am not even sure this is a feature, since it only seems to work for 'equals' and does not work on Dashboards in Power BI. 
</p><p>First of all, we need to understand deep linking in Power BI. Most artifacts in Power BI (for example reports and dashboards) have a their own URL. This means we can open them directly when we know the URL. The URL will have the following format:
</p><p><span style="font-family:Courier New">https://[tenant].powerbi.com/groups/[workspace]/[artifact type]/[artifact id]/[optional part to be opened]
</span></p><p>Thus, the URL may look like this:
</p><p><span style="font-family:Courier New">https://app.powerbi.com/groups/me/reports/dc121d4b-9aad-4494-b1de-8037f53d8355/ReportSection3
</span></p><p>This would open page <span style="font-family:Courier New">ReportSection3</span> in report with id <span style="font-family:Courier New">dc121d4b-9aad-4494-b1de-8037f53d8355</span> in my personal workspace in the tenant <span style="font-family:Courier New">app</span>.
</p><p>If you know anything about web development, you know that you can pass things through the URL to the application this is normally done by adding a question mark to the end of the URL and specifying whatever you want to pass. Multiple items can be added by separating them out by ampersands, like this:
</p><p><span style="font-family:Courier New">https://myurl.com/?firstname=Jeroen&amp;Lastname=ter%20Heerdt
</span></p><p>(notice the %20, which is a URL encoded space).
</p><p>Combining these two things, you can pass parameters to Power BI reports if you have the report URL (simply open the report to get that). Once you have it, add the following:
</p><p><span style="font-family:Courier New">?filter=[tablename]/[columnname] eq '[filter value]'
</span></p><p>So, if I wanted to filter the <span style="font-family:Courier New">activity</span> column in my <span style="font-family:Courier New">workitem</span> table so it only shows items where the <span style="font-family:Courier New">activity</span> is <span style="font-family:Courier New">blogging</span>, I would add the following:
</p><p><span style="font-family:Courier New">?filter=workitem/activity eq 'blogging'
</span></p><p>(eq is short for equals here).
</p><p>This needs, however, to be encoded for the URL. You can easily find tools online to do that for you, or if you know a little bit about what you are doing, you can do it by yourself. The addition above becomes:
</p><p><span style="font-family:Courier New">?filter=workitem%252Factivity%20eq%20%27blogging%27
</span></p><p>(/ becomes %252F, space becomes %20 and ' becomes %27)
</p><p>This would open page <span style="font-family:Courier New">ReportSection3</span> in report with id <span style="font-family:Courier New">dc121d4b-9aad-4494-b1de-8037f53d8355</span> in my personal workspace in the tenant <span style="font-family:Courier New">app</span> with a filter set on the <span style="font-family:Courier New">workitem</span> table's <span style="font-family:Courier New">activity</span> column to be equal to <span style="font-family:Courier New">blogging</span>:
</p><p><span style="font-family:Courier New">https://app.powerbi.com/groups/me/reports/dc121d4b-9aad-4494-b1de-8037f53d8355/ReportSection3?filter=workitem%252Factivity%20eq%20%27blogging%27
</span></p><p>By the way, you would probably only want to use this is very specific scenario's. It is way better to look at <a href="https://azure.microsoft.com/en-us/services/power-bi-embedded/">Power BI Embedded</a> to integrate Power BI in your applications. Note that Power BI Embedded is targeted at organizations providing software to others (hosted or not). It is not for internal applications.</p>