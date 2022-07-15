---
id: 215
title: 'Keep macros under control'
date: '2013-08-13T10:00:01+01:00'
author: 'Jeroen ter Heerdt'
layout: post
guid: 'http://www.dutchdatadude.com/?p=215'
permalink: /keep-macros-under-control/
snapLI:
    - 's:43:"a:1:{i:0;a:1:{s:11:"isPrePosted";s:1:"1";}}";'
snap_isAutoPosted:
    - '1'
snapTW:
    - 's:142:"a:1:{i:0;a:4:{s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:18:"367209781335166976";s:5:"pDate";s:19:"2013-08-13 09:03:29";}}";'
categories:
    - Office
tags:
    - audit
    - Excel
    - macros
    - security
---

I have been getting some feedback during the past three weeks (during which I was on vacation) on <a href="http://www.dutchdatadude.com/macros-are-dead/">my post about macros, where I claim that macros are dead</a>. Apart from the odd hateful mail from a hardcore macro lover, the main feedback was: <em>I get what you say but right now I am stuck with all these Excel files with macros. I do not know where to begin, can you help?</em>

To those of you I say: do not despair. If you have a lot of Excel sheets with macros (and lets face it, Excel files are where most macros are found!) and you have Office 2013 the solution is just around the corner.

Open Excel, click File, Options, Add-ins. Then at the bottom where it says 'Manage', select COM add-ins and click 'Go'. Then enable 'Inquire' and click OK.

This add-in enables you to investigate an Excel sheets for lots of things, such as hidden sheets, very hidden sheets (I did not even know that was possible), formula's and macros. Also, you can check out dependencies between sheets and sources and compare two sheets. When comparing two sheets you can even spot the difference between macros down to a single line of code!

This solution is also available as server solution for some more automatic scanning of your Excel workbooks. It is called Audit and Management Control Server 2013.

More info here:

Inquire add-in for Excel: <a href="http://office.microsoft.com/en-us/excel-help/what-you-can-do-with-spreadsheet-inquire-HA102835926.aspx">http://office.microsoft.com/en-us/excel-help/what-you-can-do-with-spreadsheet-inquire-HA102835926.aspx</a>

Audit and Control management server 2013: <a href="http://technet.microsoft.com/en-us/library/jj631654.aspx">http://technet.microsoft.com/en-us/library/jj631654.aspx</a>

Get those spreadsheets under control!