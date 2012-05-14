---
layout: post
title: "Managing services provided by homebrew"
date: 2012-05-14 09:53
comments: true
categories: 
- mac
- homebrew
---

## Background information

I have MacBook with [homebrew](https://github.com/mxcl/homebrew) and I tried to keep my machine as clean as possible. Don't like to have many services running at the same time, or when I'm not programming. The services I'm talking about are [redis](http://redis.io), [mysql](http://mysql.com), [postgresql](http://www.postgresql.org/), and other programs that runs on the background, and that drains my cpu and my battery (when unplugged). 

So yesterday, after doing some cleaning I decided to have all those services not running at boot time, and start them only when needed, like only I'm working on a project that requires any of those.

When installing a service, <code>homebrew</code> adds a launch script on <code>$HOME/Library/LaunchAgents</code> so you can start/stop it using <code>launchctl</code>, the default service manager program. <code>launchctl</code> is impossible to use. The CLI is stupid. 

Anyway, what I found out is that <code>homebrew</code> already supports a better way of dealing with <code>launchctl</code>. 

Yeah, pretty simple. 

So you want to start <code>redis</code> right now? 

    ~ brew services start redis
    ==> Successfully started `redis` (label: com.github.homebrew.redis)
    
Is it running? 
    
    ~ brew services list 
    redis      started    50582 .../Library/LaunchAgents/com.github.homebrew.redis.plist

Let's stop it
  
    ~ brew services stop redis
    Stopping `redis`... (might take a while)
    ==> Successfully stopped `redis` (label: com.github.homebrew.redis)
    

To get a list available commands do the following:

    ~ brew services help
    usage: [sudo] brew services [--help] <command> [<formula>]

    Small wrapper around `launchctl` for supported formulas, commands available:
       cleanup Get rid of stale services and unused plists
       list    List all services managed by `brew services`
       restart Gracefully restart selected service
       start   Start selected service
       stop    Stop selected service

    Options, sudo and paths:
    
      sudo   When run as root, operates on /Library/LaunchDaemons (run at boot!)
      Run at boot:  /Library/LaunchDaemons
      Run at login: /Users/lucasefe/Library/LaunchAgents
      
      
##A word for the wise

When you start a service, it start at that moment, and if you reboot the computer, it will start again. This happens because on the service's <code>launchctl</code> script says so, by default:

    ~ cat   /Users/lucasefe/Library/LaunchAgents/com.github.homebrew.redis.plist
    
    ...
    <plist version="1.0">
      <dict>
        ...
        <key>RunAtLoad</key>
        ...
      </dict>
    </plist>

So in order to not having it loaded at boot, you have to remove that line from each <code>launchctl</code> script. 

## Conclusion

It was not a perfect solution from the get-go, but after editing these files it turned out to be exactly what I needed. Only the service I need, when I need it. 

Useful? there are probably better solutions, but I'm not aware of them. If you have an alternative way, please, tell me about it. 
