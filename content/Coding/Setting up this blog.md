---
title: Setting This Up
draft: false
tags:
  - coding
  - blog
---
## The Requirements
I've actually had this idea in mind for a while. In particular, I've wanted to use Obsidian on various platforms (my phone, ipad, laptop, etc.) alongside the ability to share notes with friends or have a website to direct to. 
1. Be able to use this scheme on multiple platforms
	1. Requires some form of sync
2. Be able to access this online
3. Keep it as low cost as possible

### The Ideas
There are a few different options for .md file blog generation/hosting online, but I decided to use [quartz](https://quartz.jzhao.xyz/) since I found it pretty easy to understand and configurable enough out-of-the-box to make me happy. This, alongside github pages, gave me the option to access my notes online.

For syncing, I've had my eye on [obsidian-git](https://github.com/denolehov/obsidian-git) for a while. I find it extremely cool that they're able to offer this sync type of behavior across platforms (tested so far with my phone and my laptop, which should cover almost 99% of cases for me). 

### The Problem and The Solution
The first and probably only major issue I ran into was the obsidian-git plugin having some issues with larger vaults. The option to use the entire quartz repo as my vault didn't work the best, so I decided to extract out my notes vault to a completely separate repo. This ensured that I could keep my vault as lightweight as possible, allowing obsidian-git to sync without issues.

From there, I needed to create a couple of github action scripts + enhancements. The two repos needed to be connected in some way, and while I don't think it's the cleanest solution, for now it works. (My experience with github actions has been little to none. Only kinda understood this stuff because I use gitlab actions at work)

The workflow is as follows:
- Vault repo gets pushed to
- Vault repo actions triggers the site repo to begin both github actions
- Site repo actions trigger and build the website

### The Results
For now, I'm happy with this workflow. There are some annoying bits like needing to remember a "git backup" action via the plugin since I'm concerned about merge conflicts and how the plugin deals with those, but overall it's definitely not bad. I'm looking forward to being able to jot random things down, either from my laptop or phone, and to be able to share it with whomever, whenever.