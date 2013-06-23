---
layout: post
category: Blog
tags: [Git, Hosting, Github, Bitbucket]
title: "Using git on a shared hosting"
---

As most of the shared hosting companies out there mine doesn't grants you root access, that's ok, but it does gives you SSH access using a weird control panel where you need to enter you current IP and then they let you in. Said that I wanted to use git on that server, to then simply do a `git pull origin staging` and get all the fancy thing I'm working on to the stating server. 

To do so we need: 

1. SSH access
2. Git installed (without root access compiling one won't be easy/feasible)
3. A published repo. I've done it with [Github](https://github.com/) and [Bitbucket's](https://bitbucket.org/ "Bitbucket")

## Too easy to be true

First attempt:

{% highlight bash %}
git clone https://github.com/[REPO_URL]
error: error setting certificate verify locations:
  CAfile: /etc/pki/tls/certs/ca-bundle.crt
  CApath: none
 while accessing https://github.com/[REPO_URL]
{% endhighlight %}

As you can see this is simple chiming you don't have any certificates or you don't have access to the path specified, at this point you may want to get in touch with your hosting support guy… or you can disable the check for SSL certificates, after all you are accessing a 'public' repo for read-only proposes.

## The DIY way

Need to grab the https address of the repo to clone and then on the server do the following:

{% highlight bash %}
mkdir REPO_NAME
cd REPO_NAME
git init
git remote add origin https://github.com/[REPO_URL]
git config --local -l #You should see the repo url here
git config --add http.sslVerify false
git pull origin master
{% endhighlight %}

That worked for me and I hope it saves you some time.