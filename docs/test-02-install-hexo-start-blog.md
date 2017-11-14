# Install Hexo & start my blog

## 1 Install Hexo
* download 

```bash
npm install -g hexo-cli
```

* init

```bash
# besure you in the work directoy 
hexo init ./hexo
cd hexo/
```

* lanch

```bash
# the default port is 4000 , -p set port
hexo server -p 4400

```

## 2 start my blog

* set blog `_config.yml`

```bash
# Site
title: Viviwong's Blog
subtitle:
description:
author: viviwong
language:default
timezone:

# URL
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
url: http://viviwong.github.io
root: /
permalink: Blog/:year/:month/:day/:title.html
permalink_defaults:

```

* create a new blog .md

```bash
hexo new  instHexo
```
> * `Hexo` will in `/hexo-dir/source/_posts` dicrectory create `instHexo.md`
* 


* show you blog

```bash
hexo g; hexo s -p 4400
```
> * visit `http://localhost:4400/`

* auto deploy script

```bash
# shell script 
#!/bin/bash
hexo_dir="/2T/smb/git/hexo"
ghID=maxchendt
cd $hexo_dir
rm -rf public db.json
hexo generate
cd ..
rm -rf $ghID.github.io
git clone https://github.com/$ghID/$ghID.github.io
cp -R $hexo_dir/public/* $ghID.github.io/
cd $ghID.github.io
git add --all
git commit -m "$1"
git push -u origin master
```