---
layout: post
title: "Dropbox-todo.txt-conky Best Note Taking Ever!"
date: 2013-06-29 13:03
comments: true
categories: [android, conky, dropbox, linux, mac, os x, todo.txt]
---

<p>I own a Macbook on which I run OS X and Linux and an Andoid phone.
I really wanted a notetaking app which would work across all these devices and would keep all my notes syncd and well managed.
I am a guy who procrastinate a lot and I wanted something (some sort of widget) which would sit right on my Desktop and my phone home screen, reminding me to do what is important.</p>

<!--more-->


<h2>Options</h2>

<p>Let&#8217;s take a look at the options:</p>

<ul>
<li><a href="http://www.rememberthemilk.com">RTM</a> (Remember the milk)</li>
</ul>


<p>A really famous and powerful app, which even had plasma widget in KDE, I was really hoping this would do the job, but sadly the widget wasn&#8217;t available anymore for latest version of KDE and also for placing a widget on your Android home screen you need to buy the &#8220;pro&#8221;(or whatver) version of it from Android market for which you will have to pay annually. Haha.. :D</p>

<ul>
<li><a href="http://www.wunderlist.com">Wunderlist</a></li>
</ul>


<p>A really nice cross platform notetaking app, or perhaps more than that, you can set reminds which would pop up on your phone and also you will be sent an email, for free!. But sadly they didn&#8217;t have any app for Linux for Wunderlist 2. App for Wunderlist 1 worked &#8216;OK&#8217; for Wunderlist 2 on my Arch but then again I wanted something which sits on my desktop, not some app which I need to launch and then press <strong>sync</strong> button, which might or might not sync after that.
So, thank you Wunderlist, sadly you are not the one.</p>

<ul>
<li><a href="http://todoist.com/">Todoist</a></li>
</ul>


<p>A really nice app for Android (with widget) also for Mac but nothing for Linux. :( Also for setting reminders you need to pay (though that was not something which I really wanted)</p>

<ul>
<li><a href="http://astrid.com">Astrid</a></li>
</ul>


<p>No way to access in LInux, may be via web (I didn&#8217;t check)</p>

<ul>
<li><a href="http://www.any.do">Any.do</a></li>
</ul>


<p>A really nice solution for android, but no app for LInux, apart from web browser plugin.</p>

<p>Finally after thinking for while and checking out few apps, I got a way out to get what I wanted.</p>

<center>
<img class="noborder" src="/images/posts/conky.png"><br>
<img class ="noborder" src="/images/posts/dropbox_logo.png"><img class="noborder" src="/images/posts/todotxt_logo.png">
</center>


<p><strong><a href="https://www.dropbox.com/">Dropbox</a> + <a href="http://todotxt.com">todo.txt</a> + <a href="http://conky.sourceforge.net">conky</a></strong></p>

<p><strong>Dropbox</strong> : A service to upload files online and also have a copy of them offline. App available for OS X, Linux, Android, iOS(idc). All the files would be synced across all your devices and it works like charm, the daemon does a really nice job.</p>

<p><strong>todo.txt</strong> : An Android app using which you can make a plain text todo list in a file, which would be stored in your Dropbox account. (You need to have Dropbox app installed on your phone to use it). It has one time fee of around $2, which I was ready to pay happily.</p>

<p><strong>conky</strong> : Is piece of software, which can monitor system variable and display them on you Desktop. All I wanted it to do was to read a file and display it on my Desktop, which I was expecting a widget to do, but conky does it better than any widget out there.</p>

<h2>Installation</h2>

<p>So, it&#8217;s simple.</p>

<ul>
<li>Make a directory &#8216;todo&#8217; (or whatever name you like) in your Dropbox account</li>
<li>Place a file &#8220;todo.txt&#8221; inside it</li>
<li>Install <strong>Dropbox</strong> on your Android phone, OS X and Linux, and <strong>todo.txt</strong> on your Android phone</li>
<li>Configure <strong>todo.txt</strong> app on your phone to use /todo/todo.txt file for storing notes</li>
<li>Use conky script to display the content of /todo/todo.txt on your Linux Desktop</li>
<li>Use <strong>todo.txt</strong> app&#8217;s widget on your Android home screen</li>
<li>Use <strong><a href="https://itunes.apple.com/in/app/geektool/id456877552?mt=12">GeekTool</a></strong> on OS X, which would do the job of conky and would display the content of /todo/todo.txt on Mac Desktop</li>
</ul>


<h2>Use</h2>

<p>It works like charm, open your Linux desktop with notes being displayed on your Desktop via <strong>conky</strong>, update the notes from your Android phone and within 5 secs (well it also depends on your internet bandwidth) the notes on the Desktop are updated!</p>
