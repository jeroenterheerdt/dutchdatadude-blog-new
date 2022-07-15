---
id: 6176
title: 'Passing command line settings to SQL Server Integration Services (SSIS) packages using dtexec on Linux'
date: '2019-03-01T00:21:22+01:00'
author: 'Jeroen ter Heerdt'
layout: post
guid: 'https://www.dutchdatadude.com/?p=6176'
permalink: /passing-command-line-settings-to-sql-server-integration-services-ssis-packages-using-dtexec-on-linux/
snap_isAutoPosted:
    - '1551396093'
snap_MYURL:
    - ''
snapEdIT:
    - '1'
snapFB:
    - 's:238:"a:1:{i:0;a:8:{s:2:"do";s:1:"0";s:9:"msgFormat";s:51:"New post (%TITLE%) has been published on %SITENAME%";s:8:"postType";s:1:"A";s:9:"isAutoImg";s:1:"A";s:8:"imgToUse";s:0:"";s:9:"isAutoURL";s:1:"A";s:8:"urlToUse";s:0:"";s:4:"doFB";i:0;}}";'
snapMD:
    - "s:169:\"a:1:{i:0;a:6:{s:2:\"do\";s:1:\"1\";s:10:\"msgTFormat\";s:7:\"%TITLE%\";s:9:\"msgFormat\";s:19:\"%FULLTEXT%\r\n\r\n%URL%\";s:9:\"isAutoURL\";s:1:\"A\";s:8:\"urlToUse\";s:0:\"\";s:4:\"doMD\";i:0;}}\";"
snapTW:
    - 's:404:"a:1:{i:0;a:12:{s:2:"do";s:1:"1";s:9:"msgFormat";s:32:"New blog %TITLE% - %SURL% %TAGS%";s:8:"attchImg";s:1:"1";s:9:"isAutoImg";s:1:"A";s:8:"imgToUse";s:0:"";s:9:"isAutoURL";s:1:"A";s:8:"urlToUse";s:0:"";s:4:"doTW";i:0;s:8:"isPosted";s:1:"1";s:4:"pgID";s:19:"1101261323126669312";s:7:"postURL";s:62:"https://twitter.com/jeroenterheerdt/status/1101261323126669312";s:5:"pDate";s:19:"2019-02-28 23:22:14";}}";'
snapLI:
    - 's:367:"a:1:{i:0;a:12:{s:2:"do";s:1:"1";s:9:"msgFormat";s:27:"New blog post on %SITENAME%";s:8:"postType";s:1:"A";s:9:"isAutoImg";s:1:"A";s:8:"imgToUse";s:0:"";s:9:"isAutoURL";s:1:"A";s:8:"urlToUse";s:0:"";s:4:"doLI";i:0;s:8:"isPosted";s:1:"1";s:4:"pgID";s:0:"";s:7:"postURL";s:50:"www.linkedin.com/updates?topic=6507027017974771712";s:5:"pDate";s:19:"2019-02-28 23:22:16";}}";'
image: '../wp-content/uploads/2019/03/dtexec.jpg'
categories:
    - 'Business Intelligence'
    - 'SQL Server'
tags:
    - dtexec
    - Linux
    - ssis
---

<!-- wp:paragraph {"dropCap":true} -->
<p class="has-drop-cap">This is my first blog post since I moved to Redmond. A lot of time has passed, sorry for that! I kept busy filling out forms, forms and some more forms. After that came more forms. I dream about forms, I breath forms. I <em>am </em>a form. Wait, let's stop there.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Recently I had to figure out how to pass in settings to an <a href="https://docs.microsoft.com/en-us/sql/integration-services/sql-server-integration-services?view=sql-server-2017">SQL Server Integration Services (SSIS)</a> package when calling it using <strong>dtexec from bash on Linux</strong>.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong><a href="https://docs.microsoft.com/en-us/sql/integration-services/packages/dtexec-utility">The dtexec utility</a></strong> is utility to execute a SSIS packages. The name goes back to the time that SSIS was called Data Transformation Services (DTS) - that is also the reason why SSIS packages carry the <em>.dtsx</em> extension. The dtexec utility is available for both Windows and Linux. </p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>One of the interesting things you can do with dtexec is passing in values to variables (using the /Par(ameter) option or even change a connection string <em>at runtime </em>(using the /Conn[ection]). I had to do the latter. Here is where the fun started. The /Par and /Conn options (and maybe others) expect something like this: [name];[value]. For example:</p>
<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">dtexec /F myfile.dtsx /Conn "MasterSQL";"Data Source=myserver;User ID=myuser;Initial Catalog=master;Password=mypassword"</pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<p>Notice the ';' between the name of the source connection and the connection string. This is all great, unless you are trying to call dtexec from the bash command line in Linux, because ; actually means something in bash: when bash sees ; it thinks the current command has ended and the next instruction follows. That is not what we want here.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>I had to escape a number of items to get this to work correct in bash:</p>
<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">/CONN "MasterSQL"\;"\"Data Source=myserver;User ID=myuser;Initial Catalog=mydb;Password=mypassword\""</pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<p>See what I did there? I had to escape the first ; (between 'MasterSQL' and 'Data Source') as well as escape the quotes that surround the data source definition itself and have it double quoted.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>If you need to pass in a value to a string parameter you need to follow the same logic:</p>
<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">/PAR "$Project::myparam"\;"\"myvalue\""</pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<p>For a string variable you can pass in the value like this:</p>
<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">/SET "\\package.variables[myvariable].Value"\;"\"myvalue\""</pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<p>Hope this helps!</p>
<!-- /wp:paragraph -->