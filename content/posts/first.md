---
title: "Hello Cunts!"
date: 2022-07-15T11:30:03+00:00
# weight: 1
# aliases: ["/first"]
tags: ["Announcements"]
author: "Me"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: false
description: ""
canonicalURL: "https://canonical.url/to/page"
categories : ["Tutorial"]
disableHLJS: true # to disable highlightjs
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: true
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: true
cover:
    image: "<image path/url>" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
editPost:
    URL: "https://github.com/<path_to_repo>/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

Before you say anything about disgraceful or tasteless my choice of words are, i'd like to take a moment to say to you that - this is my blog, not yours! Go build your fucking own!
Speaking of building blogs  , here's why and how I built mine.

# Why?
To have a repertoire of my learnings.   

# How?
I wanted something I could build fast and deploy easily and free, something lightweight thats why I chose Hugo

## Installing Hugo
```
DONT $ apt install hugo
```
it didn't do shit for me except installing a decomposing 2020 version of hugo full of maggots.

Instead go to Hugo's github release page, get the debian package and knock yourself out https://github.com/gohugoio/hugo/releases

Yeah next up, it would probably install it in /usr/local/bin/hugo
so you gotta place that in your $PATH so that you can run the hugo command without specifying the whole path

```bash
$ export PATH=$PATH:/usr/local/bin/
$ source ~/.bashrc
```

#### Create a new site with the following commands 
```bash
$ hugo new site new-site -f yml
```

## Theming
Go to https://themes.gohugo.io/ choose your favorite theme, they all come with installation guides.

You'll prolly want to edit your config.yml file to specify your theme name and most importantly the baseurl


## github
```bash
git init
touch .gitmodules
```

Edit .gitmodules to make themes folder as a submodules for easy updates:
```
[submodule "themes/theme-name"]
    path = /themes/theme-name
    url = "theme-url-github"
```

```bash
$ git commit -m "first commit"
$ git branch -M master
$ git remote add origin <url>
$ git push -u origin master
```


