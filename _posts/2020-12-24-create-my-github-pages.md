---
layout: post
title:  "创建自己的 Github-Pages"
date:   2020-12-24 09:12:19 +0800
categories: blog
---

> 博主是印象笔记的重度用户，常常用笔记记录生活、写文章、临时保存东西等，不得不说这是一款非常好的软件。但在分享笔记方面还有有待改善，例如如果你想分享笔记，需要对方也是印象笔记用户；在他人的电脑上查找自己的笔记需要下载软件和登录。为了更好的可访问性，于是尝试使用 Github-Pages。

### 关于 Github-Pages 
[Github-Pages](https://docs.github.com/en/free-pro-team@latest/github/working-with-github-pages/about-github-pages) 允许用户将库里的 HTML, CSS, JavaScript 文件编译成可访问的静态网页，并可通过 xxx.github.io 访问。

比如，创建一个库的介绍页面。就可以在库设置中启用 Github-Pages，通过 https://quan3969.github.io/cc2640r2f-web-ble/ 访问 Readme.md。

或者像博主一样创建一个以 username.github.io 的库，便能通过 username.github.io 访问。

Github-Pages 默认使用 [Jekyll](https://jekyllrb.com/) 进行静态网页编译，配合众多 Jekyll-themes，用户可以创建出个性化的网页。创建过程简单，出来的结果也非常美观，因此也衍生出了用 `Github-Pages + Jekyll` 来写网页和博客的做法。

### 创建 Github-Pages 
如何创建 Github-Pages？官方给出了非常详细的教程，如果想创建属于自己的博客，可创建 username.github.io，具体分为三步：([Youtube 视频教程](https://youtube.com/playlist?list=PLLAZ4kZ9dFpOPV5C5Ay0pHaa0RJFhcmcB))
1. [创建 user.github.io 的库并启用 Github-Pages](https://docs.github.com/en/free-pro-team@latest/github/working-with-github-pages/creating-a-github-pages-site)
2. [配置 Jekyll，用 Jekyll 编辑网页内容](https://jekyllrb.com/docs/)
3. 将库同步到所创建的库

#### 配置 Jekyll 
##### Windows 下配置 
1. 下载 [Ruby](https://rubyinstaller.org/downloads/) "WITH DEVKIT" 的版本并安装，完成后用命令行运行以下命令检测是否安装成功
    ```bash
    ruby -v
    ```
    ```bash
    gem -v
    ```
2. 用 Ruby 的 gem 工具安装 jekyll 和 bundler
    ```bash
    gem install jekyll bundler
    ```
    安装完成后，检测是否安装成功
    ```bash
    jekyll -v
    ```
    ```bash
    bundler -v
    ```

##### MacOS 下配置
1. 打开终端并安装 Xcode 命令行工具集，安装后工具集中包含 Git, Ruby, Gem 等常用命令工具
    ```bash
    xcode-select --install
    ```
2. 安装 Jekyll 
    ```Bash
    sudo gem install bundler
    ```
    ```Bash
    sudo gem install -n /usr/local/bin/ jekyll
    ```
3. 检查安装的版本
    ```bash
    jekyll -v
    ```
    ```bash
    bundler -v
    ```

#### 运行 Jekyll
1. 首次运行，新建 jekyll
    ```bash
    bundle exec jekyll serve
    ```
    以后更新文件内容运行
    ```bash
    jekyll serve
    ``` 
2. 从服务器上下载下来，更新 Jekyll
    ```Bash
    bundle update
    ```