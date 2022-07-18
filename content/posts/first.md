---
title: "Hello World!"
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

Here's a mini tutorial on how I built this blog. Using Ubuntu 20.04 as my local machine and hugo as the static website generator.

# Why?
To have a repertoire of my learnings.   

# How?
I wanted something I could build fast and deploy easily and free, something lightweight thats why I chose Hugo - an opensource static site generator https://gohugo.io/

## Installing Hugo
```
DONT $ apt install hugo
```
it didn't do shit for me except installing a decomposing 2020 version of hugo.

Instead go to Hugo's github release page, get the debian package and run it to install https://github.com/gohugoio/hugo/releases

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
Go to https://themes.gohugo.io/ choose your favorite theme, they all come with installation guides. Installing via gitsubmodule, it will make it easier for updates.

You'll prolly want to edit your config.yml file to specify your theme name and most importantly the baseurl

#### activating theme
To activate the theme edit the file ***config.yml*** and change/add the following line

```hugo
theme : theme-name
```

#### Creating a post
the following command will create a new post
```
hugo new posts/first.md 
```
you can edit that file and add your blog contents below the **---** using markdown syntax. Heres a link to markdown formatting https://www.markdownguide.org/cheat-sheet/

#### Generating the static website

To serve the website live and see changes.
```bash
$ hugo server
```

then goto http://localhost:1313/

Now make hugo generate the static html of your site, just use this simple command.

```bash
$ hugo
```

## Publishing the website

We are going to use github pages to publish our website and also use github actions as your CI/CD to automatically build and publish the static website.

We need to prepare a few things before making a GitHub-Pages deployment, so open your config.yml file.

#### publishdir
add the following line
```yml
publishdir : docs
```
#### baseurl
To get a baseURL, push your code to a github repository first
Create a new repo in your GitHub account then push to it. Make sure you've ran **$ hugo** first if you have made any changes.
```bash
$ git add .
$ git commit -m "first commit"
$ git branch -M master
$ git remote add origin <url>
$ git push -u origin master
```

change baseURL to the following
```yml
baseURL: "https://<username>.github.io/<repositoryname>"
```
run **$ hugo** and do a final git push.

Then go to: ```https://github.com/<username>/<repositoryname>/settings/pages```

Change **master** as branch and choose **/docs** as folder.
save.

**Congratulations, your website is blog should now be published on  ```https://<username>/<repositoryname>/```**

### Advanced GitHub actions
Instead of running **$ hugo** everytime to generate the static file, you can get GitHub to automatically do that for you on every push and it will also automatically deploy the static version of your site.

for automatic builds, you need to create a file */.github/workflows/gh-pages.yml*

```
name: github pages

on:
  push:
    branches:
      - master  # Set a branch to deploy
  pull_request:

jobs:
  deploy:
    runs-on: ubuntu-20.04
    steps:
      - uses: actions/checkout@v2
        with:
          submodules: true  # Fetch Hugo themes (true OR recursive)
          fetch-depth: 0    # Fetch all history for .GitInfo and .Lastmod

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: 'latest'
          # extended: true

      - name: Build
        run: hugo --minify

      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        if: github.ref == 'refs/heads/main'
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./doc

```

save it and thats it, it will be automatically added to your github actions workflows and run on every push to generate the hugo static website.


Thats all folks,
Next up I'll be working on a blockchain using zig programing language, just need to learn it