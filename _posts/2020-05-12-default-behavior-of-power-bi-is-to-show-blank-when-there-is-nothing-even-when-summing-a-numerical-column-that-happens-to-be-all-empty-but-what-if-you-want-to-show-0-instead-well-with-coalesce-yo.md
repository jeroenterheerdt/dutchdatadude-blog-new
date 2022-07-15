---
id: 7683
title: 'Power BI Pro Tip: show 0 instead of (Blank)'
date: '2020-05-12T17:00:00+01:00'
author: 'Jeroen ter Heerdt'
excerpt: 'Default behavior of Power BI is to show (Blank) even when summing a numerical column that happens to be all empty. Want to show 0 instead? COALESCE helps.'
layout: post
guid: 'http://www.dutchdatadude.com/?p=7683'
permalink: /default-behavior-of-power-bi-is-to-show-blank-when-there-is-nothing-even-when-summing-a-numerical-column-that-happens-to-be-all-empty-but-what-if-you-want-to-show-0-instead-well-with-coalesce-yo/
spay_email:
    - ''
image: '../wp-content/uploads/2020/05/coalesce.jpg'
categories:
    - 'Business Intelligence'
    - 'Power BI'
tags:
    - '0'
    - blank
    - COALESCE
    - DAX
---

<!-- wp:paragraph -->
<p>This one is easy once you know how to do it. It is also buried in <a href="https://docs.microsoft.com/en-us/dax/coalesce-function-dax#example-2">the documentation.</a> <a href="https://twitter.com/Kjonge/status/1256317833299943424">Kasper de Jonge mentioned it to me on Twitter</a> and I thought it would not hurt to just write it down quickly (also to make it easier for myself to find it in the future):</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Default behavior of Power BI is to show <strong>(Blank)</strong> when there is nothing, even when summing a numerical column that happens to be all empty. But what if you want to show <strong>0</strong> instead? Well, with <a href="https://docs.microsoft.com/en-us/dax/coalesce-function-dax">COALESCE </a>you can.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>In this simple example I have a table showing sales per region for a company that is not doing so good - they are not selling anything. </p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":7684,"sizeSlug":"large"} -->
<figure class="wp-block-image size-large"><img src="../wp-content/uploads/2020/05/image.png" alt="" class="wp-image-7684"/><figcaption>Sales are <em>null</em>, maybe it's the Regions?</figcaption></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>Assuming SalesAmount is a numerical column, if you make a visual with this you get:</p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":7685,"sizeSlug":"large"} -->
<figure class="wp-block-image size-large"><img src="../wp-content/uploads/2020/05/image-1.png" alt="" class="wp-image-7685"/><figcaption>Technically correct return value</figcaption></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>Business users might just want to see <strong>0</strong> in this case, not the (more correct) <strong>(Blank)</strong>. To make this happen, add a simple measure:</p>
<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">TotalSales = COALESCE(SUM('Sales'[SalesAmount]),0)</pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<p>Creating a visual with that measure shows:</p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":7686,"sizeSlug":"large"} -->
<figure class="wp-block-image size-large"><img src="../wp-content/uploads/2020/05/image-2.png" alt="" class="wp-image-7686"/><figcaption>What your business user wants to see</figcaption></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>The way this works is that the COALESCE function will just return the first thing it finds reading from left to write in the parameter list <em>that is not null/blank</em>. That happens to be 0. If for whatever reason you wanted to show  <strong>-1</strong> when there are no sales, you can do that as well, just change the 0 to -1.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Enjoy and don't forget to feel good about making your business users happy :)</p>
<!-- /wp:paragraph -->