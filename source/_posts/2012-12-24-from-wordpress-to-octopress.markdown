---
layout: post
title: "From Wordpress to Octopress"
date: 2012-12-24 18:20
comments: true
categories: [wordpress, octopress]
---
<center><img class="noborder" src="/images/posts/octopress-logo.png"></center><br>
I am writing this post about <a href="http://octopress.org">Octopress</a>, and this is my second migration from <a href="http://wordpress.org">Wordpress</a> to Octopress.
When I moved for the first time it was actually a transition to <a href="https://github.com/mojombo/jekyll/wiki">Jekyll</a> and not Octopress, it was more of a experimentation, I installed it, generated the pages, pushed it and checked, it was all cool but it all seemed a little rough and I didn't give it enough time to soak into and switched back immediately to WP. But when I came across Octopress, I realized it was a huge improvement on top of jekyll and read few reviews too and it turned out it suits me best for the needs.

The site you are curretly viewing doesn't need a server to generate html or maintain database. It consist entirely of pre-baked pages,<!--more--> mean what-you-get is what-is-stored, you can fire it up directly in your browser from hard disk, you carry the entire working blog along with you and deploy it with zero effort anywhere, anytime that's the coolest things about Octopress, it runs your blog on flat files as compared to Wordpess (and million other blogging tools/CMS) which stores you posts/contents in
databases. 

Now that doesn't mean Wordpress is not cool, I have used it for quite a long time, but just that I think it's intended toward a different set of users, and I feel maitaining such a huge CMS with a databse and it's plugins and keeping them up-to-date is a little too much extra homework for a(my) blog, it just feels unnatural for a simple blog. While with Octopress the fact that I work with my blog like an application, I can work on it, commit it, make a draft and when it's in presentable form then deploy it with one command, and can tar the entire(working) blog and carry it in my thumb drive and launch it off anywhere and it needs minimum requirement for hosting (just a bare minimum computer running all the time), give a real comfy feeling. Since it's static there is no native support for comments but <a href="http://disqus.com">disqus</a> rocks!

and while talking of being comfy, there is extra bonus which comes with Octopress, since html is pre-generated and no database is required you can host it for free (free as in freedom and also free as in free beer ;) ) on <a href="http://pages.github.com">Github Pages</a> or on <a href="http://heroku.com">Heroku</a>, no bandwidth limit or anything, hurray! 
and of course you can deploy it if you have your own web hosting, 

<h2>Goodbye! Wordpress</h2>
<center><img class="bd" src="/images/posts/Exit-Signboard2.jpg" height=100% width=100%></center><br>
You can use <a href="https://github.com/thomasf/exitwp/">exitwp</a> to extract the posts from your Wordpess blog which would convert your XML to markdown format, which can be used with Octopress directly. You can extract everything apart from comments, if you used disqus or <a href="http://livefyre.com">livefyre</a> or some similar service then transferring comments shouldn't be a problem at all, else you might have to just say good-bye to them.

<h2>Setting it up</h2>
<center><img class="bd" title="Let's go back to Static" alt="Let's go back to static" src="/images/posts/fromwptoop.jpg"></center><br>
Setting up Octopress is a piece of cake, if you are developer of any sort then it would take not more than 20 mins to get it up and running on your Github. Just run a little rake script and get the job done.

I'll give a short pathway to get it up and running:

Fork the Octopress from here
<pre class="sh_bash">
git clone git://github.com/imathis/octopress.git octopress
</pre>
Install ruby(if not already installed)
You can use Rbenv or RVM to install ruby, I personally prefer the RVM way
<pre class="sh_bash">
curl -L https://get.rvm.io | bash -s stable --ruby
rvm install 1.9.3
rvm use 1.9.3
rvm rubygems latest
</pre>

Install dependencies for Octopress
<pre class="sh_bash">
// cd into octopress directory
gem install bundler
bundle install
</pre>

This would complete the setup process, now you can add new posts with
<pre class="sh_bash">
rake new_post['Post title']
</pre>

this would generate a markdown file in /source/_posts/Post-title.markdown
you can add content to it, and install default theme and generate static html by running
<pre class="sh_bash">
rake install
rake generate
</pre>

now if you want to push your blog to Github make a repository USERNAME.github.com in your Github account
and run

<pre class="sh_bash">
rake setup_github_pages
</pre>

give the details and run

<pre class="sh_bash">
rake deploy
</pre>

to push it to your github repository, and open USERNAME.github.com and voila!

<h2>CNAME</h2>
Not only this, even if you want to use your custom domain for your blog, it's just two step away. 
<ul>
<li> Make a file <strong>CNAME</strong> in site root, with your domain name as content i.e. mydomain.com
<li> Make a A record in your domain settings pointing to Github which is <code>204.232.175.78</code> (at the time of writing, check <a href="https://help.github.com/articles/setting-up-a-custom-domain-with-pages">here</a> for latest details).
</ul>
and one thing which you would start feeling and enjoying just as you start using Octopress is you would have a complete control over your blog, you decide it entirely, how it looks, what it does and which code goes where. It's based on a very powerful blog engine, Jekyll. 

<h2>Finally</h2>
Here is the final landing:
<ul class="reasons">
<li> Static pages, no need of PHP server for hosting</li>
<li> No database, no hassle of backing it up etc, you blog is with you all the time </li>
<li> Posting just became more efficient and enjoyable, fire up the terminal and open your favorite editor and enjoy! </li>
<li> HTML files are great for caching </li>
<li> Free hosting and unlimited bandwidth </li>
<li> Ultimate control over my blog</li>
</ul>

Blogging is just a breeze now. I love you Octopress!
