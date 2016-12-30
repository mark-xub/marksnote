---
title: 搭建博客
date: 2016-12-29 16:39:29
tags: [工具]
---
没事折腾一下，其实很久以前也搭过，试一下[Hexo](https://hexo.io/)。
<!-- more -->

### 安装Hexo
跟着Hexo的guide，就可以轻松构建一个blog系统了，不再赘述。

### 选择主题
我选了最热门的[NexT](https://github.com/iissnan/hexo-theme-next)，按照guide配置很简单，选择自己喜欢的就好。

### 选择Markdown编辑器
Mac下选择了[MacDown](http://macdown.uranusjr.com/)，开源，免费。
### 部署到公网
利用[Github Pages](https://pages.github.com/)，可以把博客部署到公网中。
修改_config.yml  

```
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git
  repo: ssh://git@github.com/mark-xub/mark-xub.github.io
  branch: master
```
之后当运行 Hexo deploy -g 时，就会把内容推送到github上，就能访问啦。
### 博客托管
当然是用github，把一些配置和文章保存起来，以防丢失。
Next主题有个小坑，about页面的列表渲染没有小圆圈，查了一下已经有人提[issue](https://github.com/iissnan/hexo-theme-next/issues/934)了，但是作者还没修复。解决方案就是修改blog\themes\next\source\css\_custom\custom.styl 文件，加入  
```css
ul {
   list-style-type: circle;
}
```





