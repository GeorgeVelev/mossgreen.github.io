---
title: Two Ways of Creating a Github Repository
search: true
categories: 
  - Git
---


> First thing you need to know if you want to play with Github.

## Two ways of creating a GitHub repository

There are at least two ways to create a Github repository, one is pushing, another is pulling.

###  Create a repo on Github and Clone it to local
1. Create a repo on Github
2. Go to the project, find a URL 
3. Go to your local folder, run command `git clone URL`

### Create a local repository, push it to your Github account
1. Create a directory to contain the project, go into this directory
2. `git init` to initialise it as a Git Repository
3. You’ll probably want to create a `.gitignore` file
4. Run `git add .` and `git commit -m ""`
5. Go to your Github page,  create a new repository, select **Push an existing repository**, get your **repo address**
6. In your local, run `git remote add origin https://github.com/username/new_repo`
7. Push your code: `git push origin YOUR_BRANCH` 

## References: 
- [Start a new git repository](http://kbroman.org/github_tutorial/pages/init.html)
- [Understanding git init](https://stackoverflow.com/questions/13525629/understanding-git-init)