---
layout: post
title: "Development setup"
date: 2021-01-11 13:13:13 -0000
---

# Development setup

I spent the first half of my carreer working for big companies. During that time, I was was mostly working on one project at a time and switching to a new project would mean switching to a new computer, or at least begin from a clean install. I would then install and configure the current project dependencies and call it a day, never having to worry about conflicting versions of tools living on the same operating system.

But starting working within alqemist meant I was going to use my own computer, and I would need to switch projects more regularly, maintaining past ones while developping current ones.


Talk about compound effect of improving over time


This is my current (as of 2021/01/11) development setup. 

## Tools

### System

- homebrew

Looking towards Nix, but seems to be a bit of a pain in the ass on mac os

- asdf

I mainly work with Ruby on Rails, so the first thing I need is a Ruby executable, and since most of the web applications now need a frontend buildchain, I also need a NodeJS executable. 

I'm also profoundly a geek, and I love to tinker with languages and ecosystems to get a taste of what's available out there

As I can switch projects quite regularly, and those projects depends on different versions of those executables. For years I've had used rbenv to manage different Ruby versions, then when it became unavoidable to manage different NodeJS versions as well, I added nvm to the mix. Nowadays, I rely on asdf for every language I might need. asdf works with plugins and tehre are a lot (https://github.com/asdf-community)

- docker-compose


This meant I was going to have to manage multiple configurations 

- Direnv

