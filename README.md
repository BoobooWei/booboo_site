# Booboo Wei 的个人网站

www.toberoot.com

<!-- Markdown snippet -->

[![Build Status](https://travis-ci.org/hexojs/site.svg?branch=master)](https://travis-ci.org/hexojs/site)

网站源码修改自 `The website for Hexo`.

## Getting started

Install dependencies:

```bash
$ git clone xxx.git
$ cd site
$ npm install
```

Generate:

```bash
$ hexo generate
```

Run server:

```bash
$ hexo server
```


```bash
cd /bioai/00_plan/
# index 
ll *.md | awk '{print "* ["$9"](/bioai/00_plan/"$9")"}' | sed 's/.md//'|sed 's/.md/.html/g'
# sidebar
ll *.md | awk '{print ""$9": /bioai/00_plan/"$9""}' | sed 's/.md//'|sed 's/.md/.html/g' 
# en
ll *.md | awk '{print ""$9": "$9""}' | sed 's/.md//'|sed 's/.md//g'
```