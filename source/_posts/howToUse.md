---
title: howToUse
date: 2018-06-27 18:38:25
tags:
---
# win10使用hexo方法

1、win10下需要安装python,官网下载安装包后安装（记住你的安装路径！），安装成功后进入控制面板>用户账户>更改我的环境变量>path编辑>新增python的安装路径

2、本地克隆博客地址：https://github.com/wynyfe/blog.git

3、执行 yarn 安装依赖包

4、执行npm install -g hexo-cli

5、 安装 hexo-theme-apollo ：执行npm install --save hexo-renderer-jade hexo-generator-feed hexo-generator-sitemap hexo-browsersync hexo-generator-archive，安装完毕后继续执行git clone https://github.com/pinggod/hexo-theme-apollo.git themes/apollo

以上配置完毕就可以新建你的文章了

1、新建文章：hexo new 'pageName'

2、markdown中编辑你的文章 复制到博客根目录下source>_posts>新建文章中，执行hexo g 生成博客静态页面

3、执行hexo s 在本地启动服务器，访问localhost：4000 即可查看到你本地博客页面

4、hexo  d 发布到GitHub

