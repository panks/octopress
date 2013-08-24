---
layout: post
title: "Cron job to schedule your jobs"
date: 2011-11-15 08:20
comments: true
categories: [cron, schedule]
---
While writing an Application for an Advertising company I came across this utility, this called <code>Cron</code>.
It’s a <a href="http://gnu.org">GNU-Linux</a> application to run programs or scripts at specified date/time, so basically you can schedule you jobs using Cron.

<strong>How to use it:</strong>
It’s actually a demon. (In case you don’t know) <a href="http://en.wikipedia.org/wiki/Daemon_(computing)">Demons</a> are applications which are started once to keep them running in background and sit idle until they are required. It is already installed in most of the Linux distributions.
<!--more-->

In the <code>/etc</code> directory you will probably find some sub directories called ‘<code>cron.hourly</code>‘, ‘<code>cron.daily</code>‘, ‘<code>cron.weekly</code>‘ and ‘<code>cron.monthly</code>‘. If you place a script into one of those directories it will be run either hourly, daily, weekly or monthly, depending on the name of the directory.

<center><img src="/images/posts/cron.png" height=70% width=70%></center>

If you want more flexibility than this, you can edit a crontab (the name for cron’s config files). The main config file is normally <code>/etc/crontab</code>.

On a default RedHat install, the crontab will look something like this:
<pre class="sh_bash">
root@pingu # cat /etc/crontab
SHELL=/bin/bash
PATH=/sbin:/bin:/usr/sbin:/usr/bin
MAILTO=root
HOME=/

# run-parts
01 * * * * root run-parts /etc/cron.hourly
02 4 * * * root run-parts /etc/cron.daily
22 4 * * 0 root run-parts /etc/cron.weekly
42 4 1 * * root run-parts /etc/cron.monthly
</pre>

The first part is almost self explanatory; it sets the variables for cron.

 

<strong>SHELL</strong> is the ‘shell’ cron runs under. If unspecified, it will default to the entry in the /etc/passwd file.

<strong>PATH</strong> contains the directories which will be in the search path for cron

e.g if you’ve got a program ‘foo’ in the directory /usr/cog/bin, it might be worth adding /usr/cog/bin to the path, as it will stop you having to use the full path to ‘foo’ every time you want to call it.

<strong>MAILTO</strong> is who gets mailed the output of each command. If a command cron is running has output (e.g. status reports, or errors), cron will email the output to whoever is specified in this variable. If no one if specified, then the output will be mailed to the owner of the process that produced the output.

<strong>HOME</strong> is the home directory that is used for cron. If unspecified, it will default to the entry in the /etc/passwd file.

 

Now for the more complicated second part of a crontab file. An entry in cron is made up of a series of fields, much like the /etc/passwd file is, but in the crontab they are separated by a space. There are normally seven fields in one entry. The fields are:

<code>minute hour dom month dow user cmd</code>


<strong>minute</strong> This controls what minute of the hour the command will run on, and is between ’0′ and ’59′

<strong>hour</strong> This controls what hour the command will run on, and is specified in the 24 hour clock, values must be between 0 and 23 (0 is midnight)

<strong>dom</strong> This is the Day of Month, that you want the command run on, e.g. to run a command on the 19th of each month, the dom would be 19.

<strong>month</strong> This is the month a specified command will run on, it may be specified numerically (0-12), or as the name of the month (e.g. May)

<strong>dow</strong> This is the Day of Week that you want a command to be run on, it can also be numeric (0-7) or as the name of the day (e.g. sun).

<strong>user</strong> This is the user who runs the command.

<strong>cmd</strong> This is the command that you want run. This field may contain multiple words or spaces.

 

If you don’t wish to specify a value for a field, just place a * in the field.

e.g.

<pre class="sh_bash">
01 * * * * root echo “This command is run at one min past every hour”
17 8 * * * root echo “This command is run daily at 8:17 am”
17 20 * * * root echo “This command is run daily at 8:17 pm”
00 4 * * 0 root echo “This command is run at 4 am every Sunday”
* 4 * * Sun root echo “So is this”
42 4 1 * * root echo “This command is run 4:42 am every 1st of the month”
01 * 19 07 * root echo “This command is run hourly on the 19th of July”
</pre>
 

<strong>Notes:</strong>

Under dow 0 and 7 are both Sunday.

If both the dom and dow are specified, the command will be executed when either of the events happen.

e.g.

<pre class="sh_bash">
* 12 16 * Mon root cmd
</pre>

Will run cmd at midday every Monday and every 16th, and will produce the same result as both of these entries put together would:

<pre class="sh_bash">
* 12 16 * * root cmd
* 12 * * Mon root cmd
</pre>

 

Vixie Cron also accepts lists in the fields. Lists can be in the form, 1,2,3 (meaning 1 and 2 and 3) or 1-3 (also meaning 1 and 2 and 3).

e.g.

<pre class="sh_bash">
59 11 * * 1,2,3,4,5 root backup.sh
</pre>

Will run backup.sh at 11:59 Monday, Tuesday, Wednesday, Thursday and Friday, as will:

<pre class="sh_bash">
59 11 * * 1-5 root backup.sh
</pre>

 

Cron also supports ‘step’ values.

A value of */2 in the dom field would mean the command runs every two days and likewise, */5 in the hours field would mean the command runs every 5 hours.

e.g.

<pre class="sh_bash">
* 12 10-16/2 * * root backup.sh
</pre>
is the same as:
<pre class="sh_bash">
* 12 10,12,14,16 * * root backup.sh
</pre>

<pre class="sh_bash">
*/15 9-17 * * * root connection.test
</pre>

Will run connection.test every 15 mins between the hours or 9am and 5pm

Lists can also be combined with each other, or with steps:

<pre class="sh_bash">
* 12 1-15,17,20-25 * * root cmd
</pre>

Will run cmd every midday between the 1st and the 15th as well as the 20th and 25th (inclusive) and also on the 17th of every month.

<pre class="sh_bash">
* 12 10-16/2 * * root backup.sh
</pre>

is the same as:

<pre class="sh_bash">
* 12 10,12,14,16 * * root backup.sh
</pre>
When using the names of weekdays or months, it isn’t case sensitive, but only the first three letters should be used, e.g. Mon, sun or Mar, jul.

Comments are allowed in crontabs, but they must be preceded with a '<code>#</code>’, and must be on a line by them self.
