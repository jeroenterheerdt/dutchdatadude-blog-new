---
id: 7756
title: 'Making your own &#8216;smart&#8217; garage door controller'
date: '2021-02-09T18:30:00+01:00'
author: 'Jeroen ter Heerdt'
layout: post
guid: 'http://www.dutchdatadude.com/?p=7756'
permalink: /making-your-own-smart-garage-door-controller/
spay_email:
    - ''
image: '../wp-content/uploads/2021/02/wiring.png'
categories:
    - 'Home Automation'
tags:
    - arduino
    - 'garage doors'
    - 'home assistant'
    - 'home automation'
    - HSCR04
    - relay
    - wemos
---

<!-- wp:paragraph -->
<p>I have two garage doors, both of which can have motors and can be opened automatically from my car, using a remote or a press off a button. Very convienient.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>However, sometimes I want to check if the garage doors are closed and be able to close / open them remotely, even if I am not anywhere near them.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Now, you can buy new garage door motors or buy something that makes them smart, but what's the fun in that? It is just another app on your mobile phone, another company storing your data in the cloud and another security hole in your network.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>I decided to make my own controllers for my garage doors. In fact, my idea was very simple: since most automatic garage doors have a physical, wired, button a relay should be able to mimic that button press. Also, I wanted to make it a bit more fancy and know if the door was closed, open or if a vehicle was parked in the parking spot. For that I needed a ultrasonic distance sensor.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>I looked at various solutions, including <a href="https://opengarage.io/">opengarage.io</a>, which is very similar, but too expensive for my taste, because I had to buy two (one for each door). Also I did not like their interface.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>In the end, this is my solution:</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>A Wemos D1 mini that runs a custom Arduino solution, which sends status and accepts commands over MQTT from a solution like <a href="https://www.home-assistant.io/">Home Assistant</a>. It also is configured for updates over the air.</li><li>Two relays, one for each garage door</li><li>Two HCSR04 ultrasonic distance sensors, one for each garage door.</li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>The code can be easily extended to handle more than two doors.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>I wanted to make the solution relatively secure, so I came up with a 'rolling cypher' security scheme. The controller only accepts the command to open the door when the cypher provided with the command matches with its calculation. For security purposes I removed that part from the code before sharing.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>You can find the code and how to make it work for your situation <a href="https://github.com/jeroenterheerdt/garagedoors-mqtt-arduino">on my GitHub</a>.</p>
<!-- /wp:paragraph -->