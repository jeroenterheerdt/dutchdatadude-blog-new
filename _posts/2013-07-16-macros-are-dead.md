---
id: 199
title: 'Macros are dead'
date: '2013-07-16T10:00:01+01:00'
author: 'Jeroen ter Heerdt'
layout: post
guid: 'http://www.dutchdatadude.com/?p=199'
permalink: /macros-are-dead/
categories:
    - Office
tags:
    - apps
    - macros
    - office
    - security
---

<span style="color: #333333; font-family: Helvetica; font-size: 11pt;">Macros are dead. Or soon will be. Think about it: in Office 2003 when you opened a file with a macro the macro was automatically enabled and ready to run.
Then with the arrival of Office 2007 things turned bad for macros and macro creators. Macros were treated as security risk:
</span><img alt="" src="../wp-content/uploads/2013/07/070613_1157_Macrosarede11.png" /><span style="color: #333333; font-family: Helvetica; font-size: 11pt;">
</span>

<span style="color: #333333; font-family: Helvetica; font-size: 11pt;">As a user you explicitly have to choose to run the macro.
</span><span style="color: #333333; font-family: Helvetica; font-size: 11pt;">Then, Office 2010 came along and the security warnings became bigger (and I believe you had to click twice to enable them instead of once). The same goes for Office 2013.
</span>

<img alt="" src="../wp-content/uploads/2013/07/070613_1157_Macrosarede21.png" /><span style="color: #333333; font-family: Helvetica; font-size: 11pt;">
</span>

&nbsp;

<span style="color: #333333; font-family: Helvetica; font-size: 11pt;">Also, along the way this warning was introduced:
</span>

<img alt="" src="../wp-content/uploads/2013/07/070613_1157_Macrosarede31.png" /><span style="color: #333333; font-family: Helvetica; font-size: 11pt;">
</span>

<span style="color: #333333; font-family: Helvetica; font-size: 11pt;">Look at those first lines: 'might contain viruses or other security hazards'. That kind of says it all: macros are dead. With the extra focus on security this makes sense. Also, eliminiating macros helps you to deal with spaghetti code lurking around in your documents. I feel you should not be creating any new files with macros and files with macros should be checked and migrated to something "better".</span>

<span style="color: #333333; font-family: Helvetica; font-size: 11pt;">Do not use macros if you want your document to be opened without security warnings. Also, know that macros do not run on all mobile devices (For example, Office RT does not run macros). </span>

<span style="color: #333333; font-family: Helvetica; font-size: 11pt;">So, what do you need to do if you need to program in your Office documents? Well, if you're using Office 2007 or 2010 you should be developing a VSTO (Visual Studio Tools for Office) add-in, which is a piece of managed code built using Visual Studio, which is essentially an add-in with the big difference that the code is not sitting in the document itself, but outside of it. If done well, this code can be centrally managed and be treated as what it actually is: application code.
See: <a href="http://msdn.microsoft.com/en-us/magazine/cc163292.aspx">http://msdn.microsoft.com/en-us/magazine/cc163292.aspx</a>.
</span><span style="color: #333333; font-family: Helvetica; font-size: 11pt;">
Now, for Office 2013 you should be building apps: <a href="http://msdn.microsoft.com/en-us/office/apps/fp160950.aspx">http://msdn.microsoft.com/en-us/office/apps/fp160950.aspx</a>.</span>