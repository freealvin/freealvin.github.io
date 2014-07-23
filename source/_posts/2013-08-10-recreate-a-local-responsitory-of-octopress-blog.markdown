---
layout: post
title: "recreate a local repository of Octopress blog"
date: 2013-08-10 19:04
comments: true
categories: [octopress, git] 
---

<!--more-->
<h2>Recreating a local Octopress repository </h2>
To recreate the local directory structure of an existing Octopress blog, follow these instructions.

<h2>Clone your blog to the new machine</h2>

First you need to clone the source branch to the local octopress folder.

{% codeblock %}
$ git clone -b source git@github.com:username/username.github.com.git octopress
{% endcodeblock %}

Then clone the master branch to the _deploy subfolder.
{% codeblock %}
$ cd octopress
$ git clone git@github.com:username/username.github.com.git _deploy 
{% endcodeblock %}

Then run the rake installation to configure everything
{% codeblock %}
$ gem install bundler
$ rbenv rehash
$ bundle install
$ rake setup_github_pages
{% endcodeblock %}

<h2> Pushing changes from two different machines</h2>

If you want to blog from more than one computer, you need to make sure that you push everything before switching computers. From the first machine do the following whenever you’ve made changes:

{% codeblock %}
$ rake generate
$ git add .
$ git commit -am "Some comment here." 
$ git push origin source  # update the remote source branch 
$ rake deploy             # update the remote master branch
{% endcodeblock %}

Then on the other machine, you need to pull those changes.

{% codeblock %}
$ cd octopress
$ git pull origin source  # update the local source branch
$ cd ./_deploy
$ git pull origin master  # update the local master branch
{% endcodeblock %}

