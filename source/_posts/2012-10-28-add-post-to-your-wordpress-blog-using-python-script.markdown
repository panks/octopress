---
layout: post
title: "Add post to your wordpress Blog using python script"
date: 2012-06-12 08:00
comments: true
categories: [wordpress, python, automate, post]
---
 <p>I was searching for some way(read script) to automatically transfer/add post to my WordPress blog from another site. The main mission was to transfer around 500 posts to wordpress and no way I was going to do it manually.</p>
 <p>On googling a little bit I got to know wordpress has it&#8217;s own api which uses xlrpc interface for communicating to blog and I can use that to automate my job. Below is the script I used. I just set the vars and loops and started it in terminal and voila! within ~30 min the new wordpress was up and running proudly with 500 new posts.</p>
<!--more-->
 <p>Find the script below.<br />
 It uses xmlpclib, read about it <a href="http://codex.wordpress.org/XML-RPC_Support">here.</a></p>
<center><img class="noborder" src="/images/posts/wordpressicon.png" height=40% width=40%></center><br>
<p>For using it you need to:</p>
<p>1. Enable XML-RPC functionality in your blog: go to <a title="Settings Writing Screen" href="http://codex.wordpress.org/Settings_Writing_Screen#Remote_Publishing">Settings &gt; Writing &gt; Remote Publishing</a> and check the checkbox.</p>
<p>2. Install <code>python</code> and <a href="http://sourceforge.net/projects/py-xmlrpc/">xmlpc</a>.</p>
<p>3. You are all set to go.</p>
<p>You may also add custom date and time to your posts.</p>


<pre class="sh_python">
import datetime, xmlrpclib

wp_url = "http://www.yourblog.com/xmlrpc.php"
wp_username = "USERNAME"
wp_password = "PASSWD"
wp_blogid = ""
status_draft = 0
status_published = 1

server = xmlrpclib.ServerProxy(wp_url)

title = "Title with spaces"
content = "Body with lots of content"
date_created = xmlrpclib.DateTime(datetime.datetime.strptime("2011-10-20 21:08", "%Y-%m-%d %H:%M"))
categories = ["category here"]
tags = ["sometag", "othertag"] 
data = {'title': title, 'description': content, 'dateCreated': date_created, 'categories': categories, 'mt_keywords': tags}

post_id = server.metaWeblog.newPost(wp_blogid, wp_username, wp_password, data, status_published)
</pre>
