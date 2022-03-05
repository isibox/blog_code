---
title: "Create a Blog With Hugo and Github"
date: 2022-02-26T16:28:56+01:00
tags:
  - github
  - hugo
categories:
  - Front
  - Code
---

## Prerequisites on Github

- Create a public respository **blog_code** for storing the code.
- Create an another public repository **mygithubname.github.io** to deploy (publish) the site. This one must have the same name as the Github username.

## Open a shell on your dev environment

Clone the blog_code respository.

  ```bash
  git clone git@github.com:isibox/blog_code.git
  ```

Go to the blog_code folder.

  ```bash
  cd blog_code
  ```

### Create a new site with Hugo

  ```bash
  hugo new site cloud-guru-blog
  ```

### Install a theme for Hugo

Go to new site folder, and then in the themes folder.

  ```bash
  cd ./cloud-guru-blog/themes
  ```

Clone the themes you want to use.

  ```bash
  git clone https://github.com/CaiJimmy/hugo-theme-stack.git
  ```

Go back to the site folder and rename the config.toml file site.

  ```bash
  cd ..
  mv config.toml config.yml
  ```

Configure the site to use the chosen theme

  ```yaml
  baseURL: "http://isibox.github.io/"
  languageCode: "en-us"
  title: "Cloud-Guru's Blog"
  theme: "hugo-theme-stack"
  ```

### Create a first post

  ```bash
  hugo new posts/my-first-post.md
  ```

And then, edit the file and write an simple example like below:

  ````yaml
  ---
  title: "My First Post"
  date: 2022-02-26T15:18:53+01:00
  tags:
    - shortcodes
    - code blocks
    - mermaid
  ---
  
  A simple example of bash block code:
  
  ```bash
  echo "My first post with hugo"
  ```
  ````

Go back to your local source code repository and clone the push repository

  ```bash
  git clone git@github.com:isibox/isibox.github.io.git
  
  ```

Go in deploy repository and create a new branch main. and then create an empty README.md file.

  ```bash
  cd isibox.github.io
  git checkout -b main
  touch README.md
  ```

Then commit the change:

  ```bash
  git status
  git add .
  git commit -m "init commit"
  ```

And then push the result:

  ```bash
  git push origin main
  ```

Now you should 
