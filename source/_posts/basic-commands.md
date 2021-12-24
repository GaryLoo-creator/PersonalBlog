---
title: hexo基础命令
updated_option: "date"
description: 只顯示description
categories:
  - 基础
tags:
  - 基础
  - hexo命令
---

欢迎来到我的博客! 这是我的第一篇文章。查看文档[documentation](https://hexo.io/docs/)以获取更多信息。如果你在使用 Hexo 时遇到任何问题，you 你可以在[故障排除](https://hexo.io/docs/troubleshooting.html)中找到答案，也可以前往[GitHub](https://github.com/hexojs/hexo/issues).

{% blockquote 更多详情 https://hexo.io/zh-cn/docs/tag-plugins %}
这是引用块

```
{% blockquote [author[, source]] [link] [source_link_title] %}
内容
{% endblockquote %}
```

{% endblockquote %}

{% asset_img example.jpg This is an example image %}

## 基础命令

### 创建一个新帖子

```bash
$ hexo new "My New Post"
```

更多详情: [Writing](https://hexo.io/docs/writing.html)

### 运行服务

```bash
$ hexo server
```

更多详情: [Server](https://hexo.io/docs/server.html)

### 生成静态文件

```bash
$ hexo generate
```

更多详情: [Generating](https://hexo.io/docs/generating.html)

### 清除缓存

```bash
$ hexo clean
```

清除缓存文件 (db.json) 和已生成的静态文件 (public)。
在某些情况（尤其是更换主题后），如果发现您对站点的更改无论如何也不生效，您可能需要运行该命令。
更多详情: [Generating](https://hexo.io/docs/generating.html)

### 部署网站（部署之前预先生成静态文件）

```bash
$ hexo deploy
```

更多详情: [Deployment](https://hexo.io/docs/one-command-deployment.html)
