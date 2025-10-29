---
title: Hexo 站点新增 /AMY/ 文章
categories:
  - Hexo
tags:
  - 新增文章
  - amy
date: 2025-10-29 13:33:39
---

## 手动操作

目前我要新增加一个非post的文章，大概流程如下：

需要开发个脚本，自动帮我做一些工作。让我只需要关注内容本身。


```bash
touch source/amy/withme/2025-10-29-amy.md
vim source/_data/sidebar.yml
    'Amy开心语录-第5篇': /amy/withme/2025-10-29-amy.html
vim themes/navy/languages/en.yml
    'Amy开心语录-第5篇': 'Amy开心语录-第5篇'

git add -A
git commit -m '[amy]add Amy经典语录-第5篇'
git push

hexo g
hexo s
hexo d
```



