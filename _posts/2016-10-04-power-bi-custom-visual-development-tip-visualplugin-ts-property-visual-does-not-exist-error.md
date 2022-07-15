---
id: 3093
title: 'Power BI Custom Visual Development Tip: VisualPlugin.ts: Property ‘Visual’ does not exist error'
date: '2016-10-04T14:30:37+01:00'
author: 'Jeroen ter Heerdt'
layout: post
guid: 'http://www.dutchdatadude.com/?p=3093'
permalink: /power-bi-custom-visual-development-tip-visualplugin-ts-property-visual-does-not-exist-error/
categories:
    - 'Big Data'
    - 'Business Intelligence'
tags:
    - development
    - 'power bi'
    - TypeScript
---

So here you are, creating your very own Power BI custom visual. You have read the documentation and ran the tutorial (<a href="https://github.com/Microsoft/PowerBI-visuals/blob/master/Readme.md">https://github.com/Microsoft/PowerBI-visuals/blob/master/Readme.md</a> and <a href="https://github.com/Microsoft/PowerBI-visuals-sampleBarChart">https://github.com/Microsoft/PowerBI-visuals-sampleBarChart</a>). You feel proud because you are done creating your awesome looking 3d-piechart-barchart-mashup visual. Then it happens. You run: <span style="font-family: Courier New;">pbiviz start</span> to view your visual and….BAM:

<img src="../wp-content/uploads/2016/09/093016_1235_PowerBICust1.png" alt="" />

Ouch. Now, before you starting banging your head against the wall until it hurts, here is the solution:

Most probably you have (as good practice dictates) changed the class name of your visual from the default 'Visual' to something more interesting, such as <span style="font-family: Courier New;">MyAwesome3DpieChartBarChartMashupTheDutchDataDudeIsSoGoingToHateThisVisual</span>.

Well, you forgot to change the <span style="font-family: Courier New;">visualClassName</span> as specified in <span style="font-family: Courier New;">pbiviz.json</span> so the code can actually find the entry point for your awesome visual. So, quick fix: open <span style="font-family: Courier New;">pbiviz.json</span> and change the <span style="font-family: Courier New;">visualClassName </span>property into your class name (which is hopefully not alike the one above). Save the file, re-run <span style="font-family: Courier New;">pbiviz start</span> and done!

(I know this is a very newbie / getting started type of error, but it took me more than 5 minutes searching for it when I first encountered it. I figured it is worthwhile saving everyone's time and log it for my own future reference ;))