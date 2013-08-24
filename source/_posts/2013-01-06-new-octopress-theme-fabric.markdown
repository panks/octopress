---
layout: post
title: "New Octopress theme- Fabric"
date: 2013-01-06 03:50
comments: true
categories: [octopress, theme, fabric]
---
Somehow I got interested in octopress while I was at home during winter vacation. I tried few themes from <a href="https://github.com/imathis/octopress/wiki/3rd-Party-Octopress-Themes">octopress wiki</a> there are some pretty nice ones out there, but just out of curiosity I ended up writing a theme on my own - <a href="https://github.com/panks/fabric">Fabric</a>. This website uses the latest version of this theme, so you can play around with it here without having to install.

I share some of the installation details and functionality here:

<h2>Installation</h2>
It's the regular, and you probably won't even read this section if you have ever played a little with Octopress.
Go to your Octopress directory, clone my theme and run the rake script to install it, and then 'rake generate' to apply it to your blog.
<!-- more -->

{% codeblock %}
$ cd octopress
$ git clone git://github.com/panks/fabric.git .themes/fabric
$ rake install['fabric']
$ rake generate
{% endcodeblock %}

<h2>Disable Ajaxification</h2>
Here I tried something new, though the blog is completely static and based on pre-baked files, I thought it would be cool to load the pages(not post) without reloading the entire blog in browser.

It's a small script but does the job, also it gives your hash url so you can actually pass the links to others if you want. 

To use it make the <code>list item</code> of your navigation bar item  with id as 'ajax', navigation bar is defined in <code>octopress/.themes/fabric/source/_includes/custom/navigation.html</code>, for instance:
<script src="https://gist.github.com/4464452.js"></script>

Anyway, some might find it little annoying or uneasy to work with and prefer just plan simple urls and reloading of pages. So to disable it:

Go to: <code> octopress/.themes/fabric/source/_includes/head.html</code> and remove the javascript file <strong>ajaxify.js</strong> I have also commented it in there for easy identification.

And then reinstall the theme and rebuild your blog with
{% codeblock %}
$ rake install['fabric']
$ rake generate
{% endcodeblock %}

or you can remove those <code>id="ajax"</code> for list items in navigation bar.

Done!



<h2>Tapirgo Search</h2>

This is probably the biggest change which I put into the theme which was not available by default and wasn't even discussed about in other themes available - <a href="http://tapirgo.com/">Tapirgo</a>

Most of the people using Octopress use google custom search for providing search to their users but I don't really like it that way,

<strong>One</strong> - You have redirect your users to another website in a new tab

<strong>Two</strong> - Google shows it's ads which is annoying

and <strong>Three</strong> -Google search from it's cache so your readers won't get the latest content from your website listed on the search result rather they would get something which google stored at it's server while crawling your blog, so it might contain some article which you deleted a few days back or might not contain the latest post of yours. Which beats the whole point of searching the blog.
Taprigo on the other hand gives you a real nice way to search static websites, using your <a href="http://en.wikipedia.org/wiki/RSS">RSS</a> feeds i.e. your atom.xml file, and it's keeps reading your feeds every 15 mins (well that's what they claim) and they also provide you with their API using which you can ping the server to reindex your feeds immediately.

For using is just <a href="http://tapirgo.com/">go to tapirgo</a> and enter the url to your atom.xml file in 'Your RSS feed' field and your email in the next field and click 'go' and then you would be provided with two tokens, one is public and the other one would be a secret token, you would need only the public token for using it in your Octopress blog.

<img src="/images/posts/tapirgohome.png">

Now create a field named <code>tapir_token</code> in your _config.yml file in Octopress directory and assign it's value as the public token.
That's all from your side. Now one can search your blog while being inside your blog and in the real content.

For some reason if you want to use google search then you can do it this way:

Go to: <code>octopress/.themes/fabric/source/_includes/custom/navigation.html</code>
and <strong>Replace</strong>
<script src="https://gist.github.com/4464380.js"></script>

<strong>with</strong>

<script src="https://gist.github.com/4464423.js"></script>

<h2>Add accounts for social links</h2>
It has a real nice social bar in which you can display your github, facebook, twitter, linkedin, googleplus, lastfm, skype and youtube accounts.
For using it just make a field <strong>sitename_user</strong> in your '_config.yml file and supply your username/id in it.

For instance for facebook, add <code>facebook_user: yourfacebookusername</code>

For some of the services the fields are already present in the _config file.

<h2> Disable scroll to top button</h2>
I have give a scroll to top button, which become visible as the user start scrolling the page and would scroll the top of the page when clicked on it, which slows it's speed down when reaches the top.

But there are all sort of people on this planet and for some weird reason from mars few of them might find it annoying so to disable it:

Go to: <code> octopress/.themes/fabric/source/_layouts/default.html</code> and remove the following lines as described there.

And then reinstall the theme and rebuild your blog
{% codeblock %}
$ rake install['fabric']
$ rake generate
{% endcodeblock %}

<h2>Image border</h2>
Image borders by default are made in such way to give the effect of a real photograph pasted on a surface (I have disabled it for the next image).

<img class="noborder" src="/images/posts/imagewithborderex.png">

To disable that effect, class your image to 'noborder' :
{% codeblock %}
<img src="/image/location/filename.png" class="noborder">
{% endcodeblock %}


<h2>Arrow after 'Read on'</h2>
This is a tiny stuff and someone who has used Octopress for a month of two won't even need it, but I just felt like mentioning it for the sake of completion.

When you use <code><!--more--></code> in your posts to show excerpts then there is a 'Read on' link after each summary to go the full post and you would notice there would be bold arrow before it and a tiny arrow in front of it. That bold arrow is put by my and the tiny arrow is put by Octopress configuration, so to remove the tiny arrow go to your _config.yml file and search for this line
{% codeblock %}
excerpt_link: "Read on & rarr;"  # "Continue reading" link text at the bottom of excerpted articles
{% endcodeblock %}
and remove the <code>& rarr;</code> from it. That's it.

There won't be space between & and r I have given it so that It won't change to an arrow here.

Well that's all, hope you would like this theme. For furthur information or any suggestion feel free to contact me.

