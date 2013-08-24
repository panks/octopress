---
layout: post
title: "Git basic commands"
date: 2011-12-11 07:11
comments: true
categories: [git, tutorial]
---
While I was working during my winter break at home I 
had to use git a lot for debugging KDE apps. So, I thought of writing 
this article. It will help newbies a lot to just read this single page 
and get started with. No need to read that GIT book or tutorial if you 
are short of time and you need only basic stuff for your job.

So first of all,

<center><img class="noborder" src="/images/posts/github-logo.png"></center>
<strong>What is Git?</strong>

<!--more-->
Git is a&nbsp;distributed version control system, 
which is designed by the same person who made 
the&nbsp;Linux&nbsp;kernel, Linus Torvalds. Written completely in C.

<strong>What is Version Control?</strong>

When editing, you can&nbsp;<em>Save As…</em>&nbsp;a 
different file, or copy the file somewhere first before saving if you 
want to savour old versions. You can compress them too to save space. 
This is a primitive and labour-intensive form of version control. 
Computer games improved on this long ago, many of them providing 
multiple automatically timestamped save slots.

Let’s make the problem slightly tougher. Say you have a 
bunch of files that go together, such as source code for a project, or 
files for a website. Now if you want to keep an old version you have to 
archive a whole directory. Keeping many versions around by hand is 
inconvenient, and quickly becomes expensive.

With some computer games, a saved game really does 
consist of a directory full of files. These games hide this detail from 
the player and present a convenient interface to manage different 
versions of this directory.

Version control systems are no different. They all 
have nice interfaces to manage a directory of stuff. You can save the 
state of the directory every so often, and you can load any one of the 
saved states later on. Unlike most computer games, they’re usually smart
 about conserving space. Typically, only a few files change from version
 to version, and not by much. Storing the differences instead of entire 
new copies saves room.

<strong>What is Distributed Control System?</strong>

Now lets change the situation a little bit. Imagine a 
very difficult computer game. So difficult to finish that many 
experienced gamers all over the world decide to team up and share their 
saved games to try to beat it. Speedruns are real-life examples: players
 specializing in different levels of the same game collaborate to 
produce amazing results.

How would you set up a system so they can get at each other’s saves easily? And upload new ones?

In the old days, every project used centralized 
version control. A server somewhere held all the saved games. Nobody 
else did. Every player kept at most a few saved games on their machine. 
When a player wanted to make progress, they’d download the latest save 
from the main server, play a while, save and upload back to the server 
for everyone else to use.

What if a player wanted to get an older saved game for
 some reason? Maybe the current saved game is in an unwinnable state 
because somebody forgot to pick up an object back in level three, and 
they want to find the latest saved game where the game can still be 
completed. Or maybe they want to compare two older saved games to see 
how much work a particular player did.

There could be many reasons to want to see an older 
revision, but the outcome is the same. They have to ask the central 
server for that old saved game. The more saved games they want, the more
 they need to communicate.

The new generation of version control systems, of 
which Git is a member, are known as distributed systems, and can be 
thought of as a generalization of centralized systems. When players 
download from the main server they get every saved game, not just the 
latest one. It’s as if they’re mirroring the central server.
This initial cloning operation can be expensive, especially if there’s a
 long history, but it pays off in the long run. One immediate benefit is
 that when an old save is desired for any reason, communication with the
 central server is unnecessary.So, that’s all about Git and how it 
works. Now lets get our hands dirty..


<h2>Prerequisite</h2>
1) You need a computer ;), with preferably Linux (any flavor) installed on it. (This post does not deal with <a title="Git for windows" href="http://code.google.com/p/msysgit/">Windows</a>, though you may use the commands given here without any modifications (probably!)).

2) You need Git.

on Fedora distribution, you may install git using the following command

<pre>$ sudo yum install git</pre>
On Ubuntu distribution, you may install git using the following command

<pre>$ sudo apt-get install git
$ sudo apt-get install git-core</pre>
For other methods and building from source check out <a title="Git dowloads" href="http://git.or.cz/#download">this page</a>.

3) You need some project which you are developing (or would be 
developing) &nbsp;. The project’s language could be anything .. C, C++, 
D, Python, Perl, HTML, JavaScript, plain text files … you got the idea 
right?

<h2>Let the show begin</h2>
<h3>Command 1 : Initializing an empty git repository.</h3>
Before you can start using the power of git you need to create an 
empty repository and tell git which files to track. The first command 
that I’m presenting initializes an empty git repository.

Before executing the command you need to be at base folder of you 
project. For example if you have all the source code for you project 
stored here <strong>/home/panks/SourceCode/myProject</strong>, (We’ll call this folder as the <strong>base folder </strong>for ease of discussion), move there first. Now execute the following command once you are in the base folder.

<pre>$ git init</pre>
This will create an empty repository in the current directory (the base folder).

For every project that you want to track using git, go to its base 
folder and issue this command first and then the next 2 commands 
presented below.

<h3>Command 2 : Adding files to git repository.</h3>
The next step is to add files to your git repository, essentially 
telling git that these are the files we want to keep track of. Execute 
the following command from the base folder.

<pre>$ git add .</pre>
This will add all the files from the current folder and sub-folders recursively to the git repository.

<h3>Command 3 : The commit command.</h3>
This is one command you’ll be using quite often.

the above command adds the files but does not commit the changes to 
the git repository. So you need to issue the following command to make 
the changes final.

<pre>$ git commit -a</pre>
This will open a text editor (probably vi) where you can add some 
comments about this commit. If you prefer not to use the text editor, 
you can specify the commit message from the command line it self, just 
use the following format instead of the above one.

<pre>$ git commit -a -m "Initial import"</pre>
The -m switch is used to specify the commit message. In our case the 
commit message is “Initial import”. You can put anything between the 
quotes for your message.

<h2>You are ‘all’ ready!</h2>
Now open your favorite text editor and start coding. When you feel 
you have accomplished something or you just want to save the current 
state of your source code issue the git-commit command as described 
above. The commit command will create a new checkpoint and save the 
current status of your source code.

Git (like any other version control system) saves all the commits you
 have done to your source code repository. This enables you to go back 
and forth between commits and inspect the changes.

Now let’s move forward and learn a few more commands.

<h3>Command 4 : Viewing the commit log.</h3>
You can view all the commits you have done till now using the following command

<pre>$ git log</pre>
This command shows the commit history with the
<ol>
<li>Unique commit hash
<li>Name and email of the person who performed the commit
<li>Date and time of commit
<li>The commit message
</ul>

Of all these, the first item, the unique commit identifier, the SHA1 
hash is of importance to us. This hash will be used with some of the 
commands listed next, and is used with a plethora of other git commands,
 not listed here

<h3>Command 5 : Checking the current status.</h3>
While coding, you may want to see what all files have changed, before
 you do a commit to store them in the git repository. This command helps
 you achieve that.

<pre>$ git status</pre>
The above command will list all files that have changed since your last commit.

<h3>Command 6 : Finding the difference between commits.</h3>
Apart from just viewing files that have changed, you may be interested in viewing the actual differences in the source code.

<pre>$ git diff</pre>
The above command will show a difference ( a diff ) with respect to your last commit and current changes.

The diff command can actually be used to compare difference between any commits

<strong>To view difference between a previous commit and current changes.</strong>

<pre>$ git diff <em>commit_hash</em></pre>
here the <em>commit_hash</em> is the first eight characters (hex 
digits) of commit hash as shown in the commit log by the git-log 
command. Yes! you need not specify the full hash, just the first eight 
digits are good enough.

<strong>To view differences between two previous commits.</strong>

<pre>$ git diff <em>commit_hash_1</em> <em>commit_hash_2</em></pre>
This command will display differences between the two commits identified by the <em>commit_hash_1</em> and <em>commit_hash_2.</em>

<h3>Command 7 : Creating branches!</h3>
Don’t be scared by the word “branching”, specially if you never dealt
 with them. Branches are easy to play with and are very useful.

Before I show you the command a bit more discussion about branches.

<ul>
<li>- You can view branches as being diversion from the main linear commit tree.</li>
<li>- All branches stem out from the <strong>master branch</strong>, the name given to the main trunk.</li>
<li>- Every branch has it’s own commit log.</li>
<li>- You can have different code in same files across difference 
branches. (This is the main feature of branching). Actually git goes 
even further and allows you to have not only different content in files 
across branches but even different sets of files across different 
branches.</li>
<li>- At one point of time, you can be sitting only on one branch. What 
this means is that, the source code from the current branch will be the 
effective one, the one to which you would be making changes.</li>
</ul>
<strong>Why use branches?</strong>

Suppose you have an almost stable source code and you are to release 
the product in a month or in a week or two. You also have plans to 
include another great feature into your code, but are afraid it might 
break your code and your release plans may go hay-wire.

This is where branches come into picture. Just create an experimental
 branch from you main stable trunk ( the one you’ve been working on up 
till now is the main trunk, the <strong>master</strong> branch). After 
you have created the experimental branch, you can continue fixing bugs 
and polishing the code on the main, i.e. the master branch. Meanwhile 
you can also continue working on the experimental branch without 
affecting a line of code on the master branch.

In the end, if you find that the experimental feature is working good
 enough, merge it into the master branch and release your product. If 
the experimental feature didn’t quite work out, you can still release 
the product from the master branch. The experimental branch is still 
there so you can continue working on it till it gets stable.

This is one scenario (and the most often reason, though not the only one), to create branches.

Okay now, back to commands . Issue the following command when you want to create a branch.

<strong>Creating a branch</strong>

<pre>$ git branch <em>branch_name</em></pre>
<em>branch_name </em>could be anything that you wish, for example:

<pre>$ git branch <strong>experimental_feature </strong></pre>
<strong>Branching a branch or “I want more branches”.
</strong>

You can create as many branches from inside any branch you want, creating a very dense tree if you like.

Just move inside (check-out that branch, see command 8 below) and issue the branch creation command.

<h3>Command 8 : Moving to a branch and listing all branches</h3>
Once you have created the branch move to it by issuing the command listed below. <strong>Always</strong> Make sure you do a commit before you issue this command or else changes will move across branches. <em>Make this a habit!</em>

<pre>$ git checkout branch_name</pre>
Here the branch name is the branch where you want to move. Once 
checked-out, you can view staus, log, diff etc, using the commands 
presented earlier.

To go back to the <strong>master</strong> branch (the main trunk) issue the following command. (Again make sure you had issued the commit command)

<pre>$ git checkout master</pre>
<strong>Listing all branches</strong>

Issue the following command to see all available branches in the current repository.

<pre>$ git branch</pre>
<h3>Command 9 : Merging two branches</h3>
Move to (checkout) the branch with which you want the merge to happen and issue the following command.

<pre>$ git merge branch_name</pre>
This will merge the branch branch_name with the current branch.

For example if you want to merger the “experimental_feature” branch with the master branch, issue the following commands

<pre>$ git checkout master
$ git merge experimental_feature</pre>
Git will notify you with any conflicts it cannot resolve automatically (if any). You can then resolve the conflicts manually.

<strong>Deleting a branch</strong>

After the merge is done you can delete the experimental branch if you wish by issuing the command

<pre>$ git branch -d experimental_branch</pre>
The above command will only delete the branch if it is fully merged 
with the current branch’s HEAD. HEAD is the current position in your 
branch, the latest commit.

<h3>Command 10 : Deleting stuff from the repository.</h3>
Issue the following command if you do not want git to keep track of a
 file or folder and (this is the opposite of the git-add command). The 
file stays in the working directory, on the disk.

<pre>$ git rm --cached path/to/the/folder_or_file</pre>
The <em>git-rm</em> command removes the files from the repository for current HEAD <em>only</em>; previous revisions/commits will still have the file.

<h2>That’s it, you’re done!</h2>
Before I leave you a few more command/features that may interest you, but are not totally necessary as of now.

<h3>A graphical repository viewer</h3>
To invoke a graphical repository viewer, invoke the following command

<pre>$ gitk</pre>
<h3>Git – Graphical user interface</h3>
For those who prefer GUI, you can install a graphical front end to git.

<strong>On Fedora</strong>

<pre>$ yum install git-gui</pre>
<strong>On Ubuntu</strong>

<pre>$ apt-get install git-gui</pre>
Run the gui by issuing the following command

<pre>$ git-gui</pre>
