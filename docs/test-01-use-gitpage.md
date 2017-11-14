# use HEXO built github blogs

## 1 Install the software

> we use `mac`, `homebrew`,`Git`,`Node.js`

* Install `homebrew`

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

# show version
brew -v
```

* Install `git`

```bash
brew install git 

# show version
git --version
```

* Install `Node.js`

```bash
brew install node

# show version
node -v
npm -v
```


## 2 Use github


* register your github

[reference: register and use github](https://guides.github.com/)


## 3 Git connect github 

* github email and username

```bash
# set & modify
git config --global user.name "yourusername in github"
git config --global user.email "youremail in github"

# show 
git config user.name
git config user.email

```

* local push to remote

```bash
# change directory to your work directory 
cd  /path/yourdirectory

# init your repository 
git init

# write code
echo "建设中..." > index.html

# Adding a new SSH key to your GitHub account
https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/

# add 
git add .

# commit 
git commit -m 'add message'

# push
git push

# viste you github

```

