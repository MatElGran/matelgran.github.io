---
layout: page
title: "Development setup"
date: 2021-01-11 13:13:13 -0000
---

# Development setup

This is my current (as of 2021/01/11) development setup. This 

## Tools

### System

- homebrew

Lokking towards Nix, but seems top be a bit of a pain in the ass on mac os

- asdf

I mainly work with Ruby on Rails, so the first thing I need is a Ruby executable, and since most of the web applications now need a frontend buildchain, I also need a NodeJS executable

As I can switch projects quite regularly, and those projects depends on different versions of those executables. For years I've had used rbenv to manage different Ruby versions, then when it became unavoidable to manage different NodeJS versions as well, I added nvm to the mix. Nowadays, I rely on asdf for every language I might need. asdf works with plugins and tehre are a lot (https://github.com/asdf-community)

- docker-compose



- Direnv

