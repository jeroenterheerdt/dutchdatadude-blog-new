---
id: 33
title: 'Multilingual SSRS reports'
date: '2013-06-25T10:00:18+01:00'
author: 'Jeroen ter Heerdt'
layout: post
guid: 'http://www.dutchdatadude.com/?p=33'
permalink: /multilingual-ssrs-reports/
snap_isAutoPosted:
    - '2'
snapEdIT:
    - '1'
snapFB:
    - 's:297:"a:1:{i:0;a:8:{s:4:"doFB";s:1:"1";s:8:"PostType";s:1:"A";s:10:"AttachPost";s:1:"2";s:10:"SNAPformat";s:51:"New post (%TITLE%) has been published on %SITENAME%";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:28:"1327098618_10201322369324369";s:5:"pDate";s:19:"2013-05-29 07:35:56";}}";'
snapLI:
    - 's:391:"a:1:{i:0;a:8:{s:4:"doLI";s:1:"1";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:27:"New blog post on %SITENAME%";s:11:"SNAPformatT";s:18:"New Post - %TITLE%";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:123:"http://www.linkedin.com/updates?discuss=&amp;scope=15370591&amp;stype=M&amp;topic=5745411985177067520&amp;type=U&amp;a=Zx8n";s:5:"pDate";s:19:"2013-05-29 07:36:01";}}";'
snapTW:
    - 's:243:"a:1:{i:0;a:7:{s:4:"doTW";s:1:"1";s:10:"SNAPformat";s:33:"Blogged: %TITLE% - %SURL% %htags%";s:8:"attchImg";s:1:"0";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:18:"339646299668348929";s:5:"pDate";s:19:"2013-05-29 07:36:03";}}";'
categories:
    - 'Business Intelligence'
tags:
    - localization
    - multilingual
    - ssrs
---

When thinking about supporting multiple languages for SSRS reports, most people think about changing the display language of one or more of the following items:
<ul>
	<li>Labels (text boxes, axis labels, table headers, etc.)</li>
	<li>Dataset results</li>
	<li>Parameter prompts</li>
</ul>
When considering presenting SSRS reports in multiple languages, one also needs to consider where to store translations. Translations can either be:
<ul>
	<li>stored in a data source (database, cube) or resource file, either accessed directly from the report or through a service call</li>
	<li>retrieved from an external translation service, such as Bing Translate</li>
</ul>
In most solutions retrieving a predefined translation would be preferable to doing an automatic translation using an external translation service, since the quality of the results can be questionable. A scenario I come across often is that the external translation service is only used when a predefined translation is not available. The scenarios discussed in this series of posts do not pose any requirement on how the translation is retrieved. Reporting Services can pass the user's language setting along. That can then be used to get the right translation.

Additionally, some of the items considered when thinking about a multilingual SSRS solution are:
<ul>
	<li>Can the report be developed once and presented in multiple languages? All of the scenarios discussed in this series provide this capability.</li>
	<li>Impact on report creation process. Does the solution chosen require manual activities when designing the report?</li>
	<li>Performance</li>
	<li>Implementation complexity</li>
</ul>
In this series of blog posts we talk about options for implementing multilingual SSRS reports. Below is a quick scoring of each option on the above capabilities and requirements. Of course the importance of requirements and the correct choice depends on the situation.

Each scenario will be discussed in a post in this series.
<div>
<table style="border-collapse: collapse;" border="0"><colgroup> <col style="width: 372px;" /> <col style="width: 74px;" /> <col style="width: 86px;" /> <col style="width: 214px;" /> <col style="width: 151px;" /></colgroup>
<tbody valign="top">
<tr>
<td style="border: 0.5pt solid currentColor; border-image: none; padding-right: 7px; padding-left: 7px;"><strong>Requirement / Scenario</strong></td>
<td style="border-width: 0.5pt 0.5pt 0.5pt medium; border-style: solid solid solid none; border-color: currentColor; padding-right: 7px; padding-left: 7px;"><strong>Assembly</strong></td>
<td style="border-width: 0.5pt 0.5pt 0.5pt medium; border-style: solid solid solid none; border-color: currentColor; padding-right: 7px; padding-left: 7px;"><strong>Change RDL</strong></td>
<td style="border-width: 0.5pt 0.5pt 0.5pt medium; border-style: solid solid solid none; border-color: currentColor; padding-right: 7px; padding-left: 7px;"><strong>Report Definition Customization</strong></td>
<td style="border-width: 0.5pt 0.5pt 0.5pt medium; border-style: solid solid solid none; border-color: currentColor; padding-right: 7px; padding-left: 7px;"><strong>Custom ReportViewer</strong></td>
</tr>
<tr>
<td style="border-width: medium 0.5pt 0.5pt; border-style: none solid solid; border-color: currentColor; padding-right: 7px; padding-left: 7px;">Translate labels (textboxes, axis labels, table headers, etc.)</td>
<td style="background: #c5e0b3; border-width: medium 0.5pt 0.5pt medium; border-style: none solid solid none; border-color: currentColor; padding-right: 7px; padding-left: 7px;">
<p style="text-align: center;"><span style="font-size: 8pt;">Yes</span></p>
</td>
<td style="background: #c5e0b3; border-width: medium 0.5pt 0.5pt medium; border-style: none solid solid none; border-color: currentColor; padding-right: 7px; padding-left: 7px;">
<p style="text-align: center;"><span style="font-size: 8pt;">Yes</span></p>
</td>
<td style="background: #c5e0b3; border-width: medium 0.5pt 0.5pt medium; border-style: none solid solid none; border-color: currentColor; padding-right: 7px; padding-left: 7px;">
<p style="text-align: center;"><span style="font-size: 8pt;">Yes</span></p>
</td>
<td style="background: #c5e0b3; border-width: medium 0.5pt 0.5pt medium; border-style: none solid solid none; border-color: currentColor; padding-right: 7px; padding-left: 7px;">
<p style="text-align: center;"><span style="font-size: 8pt;">Yes</span></p>
</td>
</tr>
<tr>
<td style="border-width: medium 0.5pt 0.5pt; border-style: none solid solid; border-color: currentColor; padding-right: 7px; padding-left: 7px;">Translate dataset results</td>
<td style="background: #dfb5b5; border-width: medium 0.5pt 0.5pt medium; border-style: none solid solid none; border-color: currentColor; padding-right: 7px; padding-left: 7px;">
<p style="text-align: center;"><span style="font-size: 8pt;">No</span></p>
</td>
<td style="background: #c5e0b3; border-width: medium 0.5pt 0.5pt medium; border-style: none solid solid none; border-color: currentColor; padding-right: 7px; padding-left: 7px;">
<p style="text-align: center;"><span style="font-size: 8pt;">Yes</span></p>
</td>
<td style="background: #c5e0b3; border-width: medium 0.5pt 0.5pt medium; border-style: none solid solid none; border-color: currentColor; padding-right: 7px; padding-left: 7px;">
<p style="text-align: center;"><span style="font-size: 8pt;">Yes</span></p>
</td>
<td style="background: #c5e0b3; border-width: medium 0.5pt 0.5pt medium; border-style: none solid solid none; border-color: currentColor; padding-right: 7px; padding-left: 7px;">
<p style="text-align: center;"><span style="font-size: 8pt;">Yes</span></p>
</td>
</tr>
<tr>
<td style="border-width: medium 0.5pt 0.5pt; border-style: none solid solid; border-color: currentColor; padding-right: 7px; padding-left: 7px;">Translate parameter prompts</td>
<td style="background: #dfb5b5; border-width: medium 0.5pt 0.5pt medium; border-style: none solid solid none; border-color: currentColor; padding-right: 7px; padding-left: 7px;">
<p style="text-align: center;"><span style="font-size: 8pt;">No</span></p>
</td>
<td style="background: #c5e0b3; border-width: medium 0.5pt 0.5pt medium; border-style: none solid solid none; border-color: currentColor; padding-right: 7px; padding-left: 7px;">
<p style="text-align: center;"><span style="font-size: 8pt;">Yes</span></p>
</td>
<td style="background: #dfb5b5; border-width: medium 0.5pt 0.5pt medium; border-style: none solid solid none; border-color: currentColor; padding-right: 7px; padding-left: 7px;">
<p style="text-align: center;"><span style="font-size: 8pt;">No</span></p>
</td>
<td style="background: #c5e0b3; border-width: medium 0.5pt 0.5pt medium; border-style: none solid solid none; border-color: currentColor; padding-right: 7px; padding-left: 7px;">
<p style="text-align: center;"><span style="font-size: 8pt;">Yes</span></p>
</td>
</tr>
<tr>
<td style="border-width: medium 0.5pt 0.5pt; border-style: none solid solid; border-color: currentColor; padding-right: 7px; padding-left: 7px;">Impact on report creation</td>
<td style="background: #dfb5b5; border-width: medium 0.5pt 0.5pt medium; border-style: none solid solid none; border-color: currentColor; padding-right: 7px; padding-left: 7px;">
<p style="text-align: center;"><span style="font-size: 8pt;">High</span></p>
</td>
<td style="background: #c5e0b3; border-width: medium 0.5pt 0.5pt medium; border-style: none solid solid none; border-color: currentColor; padding-right: 7px; padding-left: 7px;">
<p style="text-align: center;"><span style="font-size: 8pt;">Low</span></p>
</td>
<td style="background: #c5e0b3; border-width: medium 0.5pt 0.5pt medium; border-style: none solid solid none; border-color: currentColor; padding-right: 7px; padding-left: 7px;">
<p style="text-align: center;"><span style="font-size: 8pt;">Low</span></p>
</td>
<td style="background: #c5e0b3; border-width: medium 0.5pt 0.5pt medium; border-style: none solid solid none; border-color: currentColor; padding-right: 7px; padding-left: 7px;">
<p style="text-align: center;"><span style="font-size: 8pt;">Low</span></p>
</td>
</tr>
<tr>
<td style="border-width: medium 0.5pt 0.5pt; border-style: none solid solid; border-color: currentColor; padding-right: 7px; padding-left: 7px;">Impact on report rendering performance</td>
<td style="background: #ffe599; border-width: medium 0.5pt 0.5pt medium; border-style: none solid solid none; border-color: currentColor; padding-right: 7px; padding-left: 7px;">
<p style="text-align: center;"><span style="font-size: 8pt;">Low</span></p>
</td>
<td style="background: #ffe599; border-width: medium 0.5pt 0.5pt medium; border-style: none solid solid none; border-color: currentColor; padding-right: 7px; padding-left: 7px;">
<p style="text-align: center;"><span style="font-size: 8pt;">Low</span></p>
</td>
<td style="background: #dfb5b5; border-width: medium 0.5pt 0.5pt medium; border-style: none solid solid none; border-color: currentColor; padding-right: 7px; padding-left: 7px;">
<p style="text-align: center;"><span style="font-size: 8pt;">Medium</span></p>
</td>
<td style="background: #dfb5b5; border-width: medium 0.5pt 0.5pt medium; border-style: none solid solid none; border-color: currentColor; padding-right: 7px; padding-left: 7px;">
<p style="text-align: center;"><span style="font-size: 8pt;">Medium</span></p>
</td>
</tr>
<tr>
<td style="border-width: medium 0.5pt 0.5pt; border-style: none solid solid; border-color: currentColor; padding-right: 7px; padding-left: 7px;">Implementation complexity</td>
<td style="background: #c5e0b3; border-width: medium 0.5pt 0.5pt medium; border-style: none solid solid none; border-color: currentColor; padding-right: 7px; padding-left: 7px;">
<p style="text-align: center;"><span style="font-size: 8pt;">Low</span></p>
</td>
<td style="background: #ffe599; border-width: medium 0.5pt 0.5pt medium; border-style: none solid solid none; border-color: currentColor; padding-right: 7px; padding-left: 7px;">
<p style="text-align: center;"><span style="font-size: 8pt;">Medium</span></p>
</td>
<td style="background: #efc1a5; border-width: medium 0.5pt 0.5pt medium; border-style: none solid solid none; border-color: currentColor; padding-right: 7px; padding-left: 7px;">
<p style="text-align: center;"><span style="font-size: 8pt;">High</span></p>
</td>
<td style="background: #dfb5b5; border-width: medium 0.5pt 0.5pt medium; border-style: none solid solid none; border-color: currentColor; padding-right: 7px; padding-left: 7px;">
<p style="text-align: center;"><span style="font-size: 8pt;">Very<span style="background-color: #dfb5b5;">
</span>High</span></p>
</td>
</tr>
</tbody>
</table>
</div>
&nbsp;

Did I miss a requirement or solution? Please let me know!

Next time: <a title="Multilingual SSRS reports – Scenario 1: Assembly" href="http://www.dutchdatadude.com/multilingual-ssrs-reports-scenario-1-assembly/">Scenario 1: Assembly</a>.

Do you want to jump to a specific scenario? Here you go:

<a title="Multilingual SSRS reports – Scenario 1: Assembly" href="http://www.dutchdatadude.com/multilingual-ssrs-reports-scenario-1-assembly/">Scenario 1: Assembly</a>
<a title="Multilingual SSRS reports - Scenario 2: Change RDL" href="http://www.dutchdatadude.com/multilingual-ssrs-reports-scenario-2-change-rdl-2/">Scenario 2: Change RDL</a>
<a title="Multilingual SSRS reports – Scenario 3: Report Definition Customization Extension" href="http://www.dutchdatadude.com/multilingual-ssrs-reports-scenario-3-report-definition-customization-extension/">Scenario 3: Report Definition Customization</a>
Scenario 4: Custom ReportViewer