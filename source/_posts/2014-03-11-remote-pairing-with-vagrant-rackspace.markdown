---
layout: post
title: "Remote pairing with vagrant-rackspace"
date: 2014-03-12 10:30
comments: true
author: Evan Light
published: false
categories:
 - Ruby
 - Vagrant
 - vagrant-rackspace
---

I'm working with a fellow Racker on an Open Source project. He's in San Antonio but I'm half-way across the country in Falls Church, VA!  What is a developer to do?

[Vagrant](http://vagrantup.com) to the rescue!

Vagrant is a command line tool, written in Ruby, that makes it simple to create and provision a cloud server from the command line.  And Vagrant has supported Rackspace
since last year via [this plugin](https://github.com/mitchellh/vagrant-rackspace).

In this blog post, I'm going to focus on the nuts and bolts of setting up a (Ruby) development environment in the cloud suitable for pairing.

<!--more-->

If you've never used Vagrant before, the next section is a quick rehash [from a blog post of ours from last year](/blog/vagrant-now-supports-rackspace-open-cloud.html).

If you've used Vagrant before, you will likely want to skip the next section.

## Vagrant refresher

### 1. Download and install the latest Vagrant

**NOTE: These instructions are out of date. Make sure you are using the latest version of Vagrant.**

Go to <http://www.vagrantup.com/downloads.html>, find an installer for your
operating system, download it and run it.

### 2. Install vagrant-rackspace Vagrant plugin

This plugin allows you to launch Vagrant virtual machines on Rackspace Cloud.

    $ vagrant plugin install vagrant-rackspace

### 3. Download and install the Rackspace dummy box

    $ vagrant box add dummy https://github.com/mitchellh/vagrant-rackspace/raw/master/dummy.box

### 4. Configure Vagrantfile

Make a Vagrantfile which looks similar to the one below.

<script src="https://gist.github.com/Kami/5146027.js"></script>

Don’t forget to replace `rs.username` and `rs.api_key` with your Rackspace
Cloud API username and key. If you don’t yet have a Cloud account you can
create one at [https://cart.rackspace.com/cloud/](https://cart.rackspace.com/cloud/).

In this Vagrantfile example we use a Cloud server with 512 MB of memory (flavor
attribute), but you can specify an ID or a regular expression for a name of any
other size supported by Rackspace Cloud. You can find a list of all the available
sizes at
[http://www.rackspace.com/cloud/servers/techdetails/](http://www.rackspace.com/cloud/servers/techdetails/).

## Rig for pairing

A good remote pairing environment has less to do with Vagrant and more with
having a suite of installed tools that facilitate pairing.

My weapons of choice are:

* [tmux](http://tmux.sourceforge.net/)
* [emacs](https://www.gnu.org/software/emacs/) with the [multi-term](http://www.emacswiki.org/emacs/MultiTerm) package

### tmux

"tmux" stands for "terminal multiplexer".  It allows you to have multiple shells
over a single connection to your server.  But it has another less known use.

tmux is awesome for pairing!

With tmux, you and your pair can share a single session on your server
as though you were physically looking at the same screen.

### emacs

I know, I know, talking about editors is a holy war waiting to happen.
But, really, I have a good reason for using emacs.

Above, I said that tmux will let you run multiple shells over a single
connection. So, really, you could use whatever editor you want and
just open additional shells as necessary.

But down this ride lies madness.

### tmux + your editor

tmux provides a bevvy of key bindings. I'm sure your editor of choice does as
well.  While you could run any old editor in one shell and use tmux to switch
between shells, you will likely find yourself with a new problem: you now
have to remember which shell has focus and what modality it has. 

Your shell probably responds to different keybindings than your editor.

Well... mine doesn't.

### Running a terminal inside emacs

I run my shell inside emacs using multi-term.  And I've tweaked my emacs
slightly so that multi-term responds to emacs' typical scrolling
keybindings (C-x v and M-x v) .  Plus I can search in my multi-term history just as though
it was any other emacs buffer (C-x s, etc.).






