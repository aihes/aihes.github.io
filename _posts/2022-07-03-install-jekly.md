---
layout: home
title:  "Jekyll安装过程记录"
date:   2022-07-03 09:29:09 +0800
categories: jekyll update
---

1、升级Homobrew
2、通过brew安装ruby
```shell
brew install ruby
```
3、安装jekyll相关的包
```shell
sudo gem install jekyll bundler
jekyll new myblog
cd myblog
bundle exec jekyll serve
```

4、配置jekyll的主题；https://mmistakes.github.io/minimal-mistakes/docs/configuration/
```shell
# 添加Gemfile
gem "minimal-mistakes-jekyll"
# 安装主题
bundle
# 配置主题，在_config.yml
theme: minimal-mistakes-jekyll
```

5、去Github上配置默认的网站
- 新建一个repositoy：仓库的名字一定要和个人的名字相同: https://pages.github.com/
- 配置当前的jekelly内容到github上
