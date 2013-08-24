---
layout: post
title: "Expect- talk with programs using scripts"
date: 2011-12-22 07:07
comments: true
categories: expect
---
"OK! Now I can't bear it anymore" - The condition after our endsems got over, as Insti bandwidth usages was on peak, one had no work other than running behind monkey (yeah we do have monkeys in our campus, all around us, so blessed we are, aren't we?) to scare them to death or stick your bum to chair and do some time pass on internet.
 
But they say there is solution to every problem, here was it.<!--more--> We had access to our departmental network, which uses different proxy server, and since the LAN is common throughout the Insti we could connect to it, to get a little relief in internet speed, obviously everyone could do that, but you don't expect students from Bio-tech people to type commands in terminal(they are already happy enough by looking at windows animation), until that's the only option to save the human race.
<center><img class="noborder" src="/images/posts/batmantux.png"></center> <br>
 
But for lazzy bum like me it was painful to type the command to ssh to the departmental computers every time I login to my laptop. So I wrote a script to do that, obviously auto-run on system start.
But there was a catch, we had to input our login password while connecting to departmental computers and there was no way in linux terminal to supply the password automatically on request :(
 
When will google come to work?! I googled it and got to know about Expect, it is a toolkit for automating interactive programs, such as TELNET and FTP, written by Don Libes. It knows what can be expected from a program and what the correct response would be.
You can this page to get an idea of how expect works, it contains six basic examples: <a href="http://www.thegeekstuff.com/2010/10/expect-examples/">http://www.thegeekstuff.com/2010/10/expect-examples/</a>
 
For more info you can click at: <a href="http://oreilly.com/catalog/expect/chapter/ch03.html">http://oreilly.com/catalog/expect/chapter/ch03.html</a>
 
<p>
<strong>edit:</strong> Instead of running the script of system startup, you can ask network manager to do it for you, that way even if the network goes off while you are working and comes back again, you wold be reconnected. You can put your script in <strong>/etc/network/if-up.d</strong> on debian based distros and in <strong>/etc/NetworkManager/dispatcher.d/</strong> in fedora/redhat based distros, that would be executed when the network connects. If you plan to put more than one script you can specify the sequence by naming them
starting with a number between 1 and 99, they would be executed in ascending order, ex. <code>5-myscript.sh</code>, default is 50.
</p>
