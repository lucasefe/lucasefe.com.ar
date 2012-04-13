---
layout: post
title: "Ruby & Rails Mac OS X Setup for the masses"
date: 2012-04-13 09:16
comments: true
categories: 
- ruby
- english
- rails
---

Lately it seems like setting up rails on Mac OS X is a complicated task, something only the hackers of the world can achieve. Since I'm no hacker, and I do it constantly, I decided to write a quick outline of what I do every time I have a new clean Mac, to achieve this "impossible" task. 

In my experience, you don't need much to get started. I am not even using [rvm](https://rvm.beginrescueend.com/rvm/install/), [ry](https://github.com/jayferd/ry) or [rbenv](https://github.com/sstephenson/rbenv). There's always time to learn more about them, and you can wait until you need different ruby versions to start complicating your life.

Let's face it: we, the hardcore ruby devs (?) always recommend this or that tool, but in the beginning you need to learn the basics. You don't care about which one is the best database, or if imagemagick is crap. You can learn about all the details later, when the problem is in your face.

Let's get started. 

## Install Mac OS X's build tools

In order to compile anything, you need this.

### For Lion (10.7.x):

Download [OSX GCC Installer](https://github.com/kennethreitz/osx-gcc-installer) and the [Command Line Tools for Xcode](http://developer.apple.com/xcode/index.php). <small> Sorry, but there is no direct link for Apple's stuff. </small>

### For Snow Leopard (10.6.x):

Download [Xcode for Snow Leopard](http://developer.apple.com/xcode/index.php)

Install the right thing for your OS version. 

## Install homebrew

[Homebrew](https://github.com/mxcl/homebrew) is my package manager of choice. The recipes or formulas are written in ruby, so it's as good as it gets. You have one of this on most *nix like operating systems. 

{% codeblock Current instructions recommend doing this %}
/usr/bin/ruby -e "$(/usr/bin/curl \
-fksSL https://raw.github.com/mxcl/homebrew/master/Library/Contributions/install_homebrew.rb)"
{% endcodeblock %}

After executing that, provided that you didn't mess up, you'll be able to install most software you'll ever need. 

Homebrew will install by default on /usr/local, and your new friend is the <code>brew</code> command.  

## Install Ruby

Watch out for this, because it's very complicated stuff. 

{% codeblock %}
brew install ruby
# Put the pava on the fire for the mate.
#.... Downloading, compiling...
# Remove the pava from the fire. 

ruby -v
# ruby 1.9.3p125 (2012-02-16 revision 34643) [x86_64-darwin11.3.0]
{% endcodeblock %}

I know, I know... You feel the pain. 

## Install Rails

{% codeblock %}
gem install rails # I know, it's amazing...
{% endcodeblock %}

### Note

At this point in my life I feel that there are many other ways to do web development with Ruby. Of course, Rails is the preferred one since forever, but be aware of other lighter, more flexible solutions. I'll write some more about this later. 

## Install the database

This is completely optional, alright? Rails works out of the box with sqlite3, so without doing this you are still set, ready to go. 

{% codeblock %}
brew install mysql # for example, but it can be also postgresql, redis, etc. 
{% endcodeblock %}

## Next Steps

At some point, you are gonna start adding gems, and some of them are going to require other libraries in order to work. Nokogiri requires libxml2, paperclip requires imagemagick, and so on. Just brew the dependency named at the library's Readme file. It's not that complicated, is it? 

## Done

You're done, man. Start learning and blow our minds away.
