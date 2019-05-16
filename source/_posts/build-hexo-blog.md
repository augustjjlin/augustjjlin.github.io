---
title: Build a Personal Blog by Hexo + Github Pages
date: 2019-05-16 22:55:26
tags:
- Hexo
- GitHub
- Blog
categories:
- Web
---

# Homebrew

`Homebrew` is a free and open-source software package management system that simplifies the installation of software on Apple's macOS operating system and Linux.

## Installation

In the terminal type the following command to install Home-brew

```shell
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

<br><br>

# Node.js

`Node.js` is a JavaScript runtime built on [Chrome's V8 JavaScript engine](https://v8.dev/).

## Installation

In the terminal type the following command to install Node.

```bash
$ brew install node
```

If everything installed successfully then you can type in the following commands in the terminal to check the Node and NPM version.

```shell
$ node -v
v12.1.0
```

```shell
$ npm -v
6.9.0
```

<br><br>

# Hexo

`Hexo` is a fast, simple & powerful blog framework

## Build a Hexo Blog

### Install and Configurate Hexo

#### Install Hexo

```shell
$ npm install -g hexo-cli
```

If you successfully install Hexo, you will see:

```shell
/usr/local/bin/hexo -> /usr/local/lib/node_modules/hexo-cli/bin/hexo

> fsevents@1.2.9 install /usr/local/lib/node_modules/hexo-cli/node_modules/fsevents
> node install

node-pre-gyp WARN Using needle for node-pre-gyp https download 
[fsevents] Success: "/usr/local/lib/node_modules/hexo-cli/node_modules/fsevents/lib/binding/Release/node-v72-darwin-x64/fse.node" is installed via remote
+ hexo-cli@1.1.0
added 293 packages from 458 contributors in 6.015s
```

#### Initialize Hexo

```shell
$ hexo init blog
```

#### Configurate Hexo

```shell
$ cd blog
$ npm install
```

### Hexo theme

[Find](https://hexo.io/themes/) a favourite theme, mine is [Next](https://github.com/theme-next/hexo-theme-next) 

1. In the blog's `root` directory:

   ``` shell
   $ git clone https://github.com/theme-next/hexo-theme-next themes/next
   ```

2. Change the `theme` property in the `config.yml` file.

   ```yaml
   # theme: landscape
   theme: next
   ```

3. Configurate  `themes/next/_config.yml`  file.

4. Configurate [MathJax](https://github.com/theme-next/hexo-theme-next/blob/master/docs/MATH.md)

   To enable MathJax, add `mathjax: true`

5. Run and Test

   ```shell
   $ hexo generate
   $ hexo server
   ```

   Then go to http://localhost:4000 to see your initial blog

## Deploy the initialized Hexo blog to GitHub Pages

1. Create a github repository with name : [username].github.io

   - `[username]` must be replaced by your own username.
   - Remember to initialize this reposity with a README in order to have a initial **master** branch

   ![](/images/build-hexo-blog/pic_001.png)

2. Configurate `_config.yml ` in your blog's root directory

   ```yaml
   # URL
   ## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
   url: https://augustjjlin.github.io/  #The URL of your website
   root: /
   permalink: :year/:month/:day/:title/
   permalink_defaults:
   ```

   ```yaml
   # Deployment
   ## Docs: https://hexo.io/docs/deployment.html
   deploy:
     type: git 
     repo: https://github.com/augustjjlin/augustjjlin.github.io # GitHub/Bitbucket/Coding/GitLab repository URL
     branch: master # Branch name.
   ```

3. Install [hexo-deployer-git](https://github.com/hexojs/hexo-deployer-git).

   ```shell
   $ npm install hexo-deployer-git --save
   ```

   If you see

   ```shell
   babel-eslint@10.0.1 requires a peer of eslint@>= 4.12.1 but none is installed. You must install peer dependencies yourself.
   
   ajv-keywords@3.4.0 requires a peer of ajv@^6.9.1 but none is installed. You must install peer dependencies yourself.
   ```

   Then you can install the `babel-eslint@10.0.1`, `eslint@4.12.1`, `ajv-keywords@3.4.0` and `ajv@^6.9.1` from the following commands:

   ```shell
   $ npm install babel-eslint@10.0.1 eslint@4.12.1 --save-dev
   $ npm install ajv-keywords@3.4.0 ajv@^6.9.1 --save-dev
   ```

4. Clean the Hexo

   ```shell
   $ hexo clean
   ```

5. Initialize current repository using git

   ```shell
   $ git init
   ```

6. Remove the git of `next` theme

   ```shell
   $ rm -rf themes/next/.git
   ```

7. Link your remote Github Page repository

   ```shell
   $ git remote add origin https://github.com/augustjjlin/augustjjlin.github.io.git
   ```

8. Pull the remote repository to avoid conflict

   ```shell
   $ git pull origin master
   ```

9. Add and commit remain Hexo files

   ```shell
   $ git add -A
   $ git commit -m 'Initial Commit'
   ```

10. Create and Checkout a new branch `hexo`

    ```shell
    $ git branch hexo
    $ git checkout hexo
    ```

11. Push the hexo branch to remote Github Pages repository

    ```shell
    $ git push origin hexo
    ```

12. Go to your remote Github Pages repository settings, and set the default branch to `hexo`

    ![](/images/build-hexo-blog/pic_002.png)

13. Now you can deploy your blog to Github Pages using following commands

    ```shell
    $ hexo clean && hexo generate && hexo deploy
    ```

14. You can see [this](##Manage your Hexo codes in different computer) about managing your Hexo codes when you use a different computer

15. You can [modify](https://hexo.io/docs/configuration.html) the information of your blog and [modify](https://github.com/probberechts/hexo-theme-cactus) the cactus theme of your blog.

## Manage your Hexo codes in different computer

1. Clone your remote Github Pages `hexo` branch

   If you switch your default branch to `hexo`, you can use the following commands:

   ```shell
   $ git clone https://github.com/augustjjlin/augustjjlin.github.io.git
   $ cd augustjjlin.github.io
   ```

3. Install the required dependencies

   ```shell
   $ npm install -g hexo-cli
   $ npm install
   ```

4. Test the Hexo blog in your local server

   ```shell
   $ hexo clean && hexo generate && hexo server
   ```

5. After you create a new post, use the following commands to deploy:

   ```shell
   $ hexo clean
   $ git add and commit your new files
   $ git push origin hexo
   $ hexo clean && hexo generate && hexo deploy
   ```

<br><br>

# Configurate Custom Domain

- Purchase a domain name from [GoDaddy](https://www.godaddy.com) or other domain providers

- Check the IP address of your GitHub Pages default domain

  ```shell
  $ dig augustjjlin.github.io +noall +answer
  
  ; <<>> DiG 9.10.6 <<>> augustjjlin.github.io +noall +answer
  ;; global options: +cmd
  augustjjlin.github.io.	2201	IN	A	185.199.111.153
  augustjjlin.github.io.	2201	IN	A	185.199.109.153
  augustjjlin.github.io.	2201	IN	A	185.199.110.153
  augustjjlin.github.io.	2201	IN	A	185.199.108.153
  ```

- Follow your DNS provider's instructions to configurate the DNS

  ![](/images/build-hexo-blog/pic_003.png)

- Use following commands to see if you successfully configurate the DNS

  ```shell
  $ dig augustjjlin.com +noall +answer
  
  ; <<>> DiG 9.10.6 <<>> augustjjlin.com +noall +answer
  ;; global options: +cmd
  augustjjlin.com.	1773	IN	A	185.199.111.153
  augustjjlin.com.	1773	IN	A	185.199.108.153
  augustjjlin.com.	1773	IN	A	185.199.109.153
  augustjjlin.com.	1773	IN	A	185.199.110.153
  
  $ dig www.augustjjlin.com +noall +answer
  
  ; <<>> DiG 9.10.6 <<>> www.augustjjlin.com +noall +answer
  ;; global options: +cmd
  www.augustjjlin.com.	2243	IN	CNAME	augustjjlin.github.io.
  augustjjlin.github.io.	2243	IN	A	185.199.108.153
  augustjjlin.github.io.	2243	IN	A	185.199.111.153
  augustjjlin.github.io.	2243	IN	A	185.199.109.153
  augustjjlin.github.io.	2243	IN	A	185.199.110.153
  ```

- Create a `CNAME` file under source/

  ```shell
  $ echo 'augustjjlin.com' >> source/CNAME
  ```

- Modify the URL part of `_config.yml`

  ```yaml
  # URL
  ## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
  url: https://augustjjlin.com/  #The URL of your website
  root: /
  permalink: :year/:month/:day/:title/
  permalink_defaults:
  ```
  
- Add and commit your changes, push to remote `hexo` branch

  ```shell
  $ git add and commit your changes
  $ git push origin hexo
  ```
  
- Deploy the Hexo

  ```shell
  $ hexo clean && hexo generate && hexo deploy
  ```
  
- Add your custom domain name to your Github Pages Settings

  ![](/images/build-hexo-blog/pic_004.png)

- Wait until your DNS certificate is completed, then go to your `Custom Domain` to see your blog