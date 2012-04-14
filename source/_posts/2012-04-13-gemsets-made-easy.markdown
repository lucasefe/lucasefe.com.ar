---
layout: post
title: "gemsets made easy"
date: 2012-04-13 09:17
comments: true
categories: 
- ruby
- other-side
- gemsets
- isolation
---

[rvm](https://rvm.beginrescueend.com/rvm/install/) has a great feature: [gemsets](http://beginrescueend.com/gemsets/basics/). If you don't know what it is, please, go read about it. 

Anyway, what I really like about rvm's gemsets is the isolation level they provide. It super easy to try something for a while and then wipe it out in a second. 

But there's a problem, I no longer use rvm :-) 

Enter [gs](https://github.com/soveran/gs). 

[gs](https://github.com/soveran/gs) is a gem that provides the features I need without having to depend on rvm's good behavior.

As an example, let's say I'm working on a pull request of a gem I'm using for project.

{% codeblock Cloning cuba gem into my blackhole folder %}
~/code/bh 0 $ git clone git@github.com:lucasefe/cuba.git
Cloning into cuba...
remote: Counting objects: 889, done.
remote: Compressing objects: 100% (451/451), done.
remote: Total 889 (delta 436), reused 837 (delta 386)
Receiving objects: 100% (889/889), 121.69 KiB | 125 KiB/s, done.
Resolving deltas: 100% (436/436), done.
~/code/bh 0 $ cd cuba/
{% endcodeblock %}

I can create a gemset just by executing the following command. Note that a gemset is only a .gs folder in the current directory. 

{% codeblock %}
~/code/bh/cuba master 0 $ gs init
{% endcodeblock %}

To use the gemset, just run gs with no parameters

{% codeblock %}
~/code/bh/cuba master 0 $ gs
cuba ~/code/bh/cuba master 0 $
{% endcodeblock %}

Notice how my prompt changed? This is not provided by gs, but this [gist](https://gist.github.com/da4cd5674373e7f6042a) does the trick (it alters your PS1 variable). The name of the gemset is the folder's name. Simple, no complex stuff here. 

Ok, let's install some dependencies. In this case I'm using [dep](https://github.com/twpil/dep) (topic for another post), bundler's simple alternative for dependencies tracking.

{% codeblock %}
cuba ~/code/bh/cuba master 0 $ dep install
  gem install rack -v 1.4.1
  gem install tilt -v 1.3.3
  gem install capybara -v 1.1.2
  gem install cutest -v 1.1.3

cuba ~/code/bh/cuba master 0 $ gem list 
addressable (2.2.7)
bigdecimal (1.1.0)
capybara (1.1.2)
childprocess (0.3.1)
clap (0.0.2)
cutest (1.1.3)
dep (1.0.1)
ffi (1.0.11)
gs (0.1.0)
libwebsocket (0.1.3)
mime-types (1.18)
multi_json (1.2.0)
nokogiri (1.5.2)
rack (1.4.1)
rack-test (0.6.1)
rake (0.9.2.2)
rubyzip (0.9.7)
selenium-webdriver (2.21.0)
tilt (1.3.3)
xpath (0.1.4)
{% endcodeblock %}

Ok, a lot of gems, right? If I want to leave the gemset, I just need to exit (either by typing <code>exit</code> or with <code>Ctrl-d</code>). And now we have only the original gems installed. 

{% codeblock %}
cuba ~/code/bh/cuba master 0 $ exit
~/code/bh/cuba master 0 $ gem list 
bigdecimal (1.1.0)
clap (0.0.2)
dep (1.0.1)
gs (0.1.0)
rake (0.9.2.2)
{% endcodeblock %}

Do you want to remove the gemset? Just remove the .gs folder. 

{% codeblock %}
~/code/bh/cuba master 0 $ rm -fr .gs
{% endcodeblock %}

So how does this thing work? I leave that as an exercise, 'cause I think you'll be amazed. Check the [code base](https://github.com/soveran/gs/blob/master/bin/gs#L27-45). 

To me, this is a great example of how to build simple and useful stuff, without doing more than what is needed. We need more of this and less [complected](http://www.infoq.com/presentations/Simple-Made-Easy) stuff.
