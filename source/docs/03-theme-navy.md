---
title: Hexo 站点搭建搭配 Navy 主题
categories:
  - news
tags:
  - hexo
  - typora
date: 2025-10-20 22:33:39
---

> `Hexo`支持大量的主题，但是我看中了 `hexo.io` 站点使用的 `navy`主题哈，直接 `git clone` 下来魔改即可。
>
> 第一次使用这个主题是在 2020年6月1日~ 但由于各种原因已经3年没有更新过自己的博客了，本地环境已经没有了，尝试了恢复，但是失败了。
>
> 所以这次直接使用最新版本的`hexo`和`navy`主题来搭建站点。

## help

[hexo doc](https://hexo.io/zh-cn/docs/)

| Hexo 版本 | 最低版本 (Node.js 版本) | 最高版本 (Node.js 版本) |
| :-------- | :---------------------- | :---------------------- |
| 7.0+      | 14.0.0                  | latest                  |

## 定制魔改主题

```bash
git clone https://github.com/hexojs/site.git
cd site
git branch b1
git checkout b1

# 如果搞失败了，就删除分支
git branch -D b1

npm install
hexo generate
hexo server

# 需要修改的内容：
## 修改网站readme
cp my/readme.md site/readme.md
## 修改About的内容为自己的信息
cp my/source/about/index.md site/source/about/index.md
## 去除comment功能 -- 这里我直接注释了comment的代码
cp my/themes/navy/layout/partial/comment.njk site/themes/navy/layout/partial/comment.njk
## 修改_config.yml 配置
cp site/_config.yml site/_config.yml.back
cp my/_config.yml site/_config.yml
rm -rf site/_config.yml.back
## 替换icon
mv site/source/icon site/source/icon.back
cp -rp my/icon site/source/icon
rm -rf site/source/icon.back
## 替换logo
mv site/source/logo.png site/source/logo.png.back
mv site/source/logo.svg site/source/logo.svg.back
mv site/source/favicon.ico site/source/favicon.ico.back

cp my/source/logo.* site/source/
cp my/source/favicon.ico site/source

rm -rf site/source/logo.png.back
rm -rf site/source/logo.svg.back
rm -rf site/source/favicon.ico.back

## index 网页首页固定元素修改
mv site/themes/navy/layout/index.njk site/themes/navy/layout/index.njk.back
cp my/themes/navy/layout/index.njk site/themes/navy/layout/index.njk
rm -rf site/themes/navy/layout/index.njk.back

mv site/themes/navy/layout/partial/share.njk site/themes/navy/layout/partial/share.njk.back
cp my/themes/navy/layout/partial/share.njk site/themes/navy/layout/partial/share.njk
rm -rf site/themes/navy/layout/partial/share.njk.back

## 修改首页footer中的元素,改为youtube和github
mv site/themes/navy/layout/partial/footer.njk site/themes/navy/layout/partial/footer.njk.back
cp my/themes/navy/layout/partial/footer.njk site/themes/navy/layout/partial/footer.njk
rm -rf site/themes/navy/layout/partial/footer.njk.back

#  删除支持的那么多语言，只需要保留默认的中文即可，右上角的选择框改为展示about
mv site/source/_data/languages.yml site/source/_data/languages.yml.back
cp my/source/_data/languages.yml site/source/_data/languages.yml
rm -rf site/source/_data/languages.yml.back

rm -rf site/source/es
rm -rf site/source/ja
rm -rf site/source/ko
rm -rf site/source/pt-br
rm -rf site/source/ru
rm -rf site/source/th
rm -rf site/source/zh-cn
rm -rf site/source/zh-tw

rm -rf site/themes/navy/languages/de.yml
rm -rf site/themes/navy/languages/es.yml
rm -rf site/themes/navy/languages/fr.yml
rm -rf site/themes/navy/languages/ja.yml
rm -rf site/themes/navy/languages/ko.yml
rm -rf site/themes/navy/languages/pt-br.yml
rm -rf site/themes/navy/languages/ru.yml
rm -rf site/themes/navy/languages/th.yml
rm -rf site/themes/navy/languages/zh-cn.yml
rm -rf site/themes/navy/languages/zh-tw.yml

mv site/themes/navy/layout/partial/header.njk site/themes/navy/layout/partial/header.njk.back
cp my/themes/navy/layout/partial/header.njk site/themes/navy/layout/partial/header.njk
rm -rf site/themes/navy/layout/partial/header.njk.back

# 开始定制自己的首页内容
mv site/source/index.md site/source/index.md.back
cp my/source/index.md site/source/index.md
rm -rf site/source/index.md.back

# 展示内容的时候一行展示3个，需要修改css
mv site/themes/navy/source/css/_partial/index.styl site/themes/navy/source/css/_partial/index.styl.back
cp my/themes/navy/source/css/_partial/index.styl site/themes/navy/source/css/_partial/index.styl
rm -rf site/themes/navy/source/css/_partial/index.styl.back


## 具体修改的信息
.intro-feature-wrap
  padding-top: 20px
  @media mq-tablet
    flex: 0 0 30% # 从一行2列 50% 改为一行3个 30%
    padding-top: 50px
  @media mq-normal
    flex: 0 0 30%
    padding-top: 50px



## 修改首页的搜索框 --- ing
npm install hexo-algoliasearch --save

mv site/themes/navy/layout/partial/after_footer.njk site/themes/navy/layout/partial/after_footer.njk.back
mv site/themes/navy/layout/partial/header.njk site/themes/navy/layout/partial/header.njk.back
mv site/themes/navy/source/css/_partial/header.styl site/themes/navy/source/css/_partial/header.styl.back

cp my/themes/navy/layout/partial/after_footer.njk site/themes/navy/layout/partial/after_footer.njk
cp my/themes/navy/layout/partial/header.njk site/themes/navy/layout/partial/header.njk
cp my/themes/navy/source/css/_partial/header.styl site/themes/navy/source/css/_partial/header.styl

rm -rf site/themes/navy/layout/partial/after_footer.njk.back
rm -rf site/themes/navy/layout/partial/header.njk.back
rm -rf site/themes/navy/source/css/_partial/header.styl.back

# 修改news页面
mv site/themes/navy/layout/archive.njk site/themes/navy/layout/archive.njk.back
cp my/themes/navy/layout/archive.njk site/themes/navy/layout/archive.njk
rm -rf site/themes/navy/layout/archive.njk.back

mv site/themes/navy/layout/post.njk site/themes/navy/layout/post.njk.back
cp my/themes/navy/layout/post.njk site/themes/navy/layout/post.njk
rm -rf site/themes/navy/layout/post.njk.back
```

## 支持hexo + typora 图片插入解决办法 `![](path)`

> 这一步在网上找了好多方法，信息比较乱。
>
> 总结下来就是：
>
> 1、 我喜欢用typora写文章，那么文章中有图片咋整？ 是不是要搞个目录存放一下呀~
>
> hello/01.jpg
> hello.md
>
> 那么我们就需要`hexo new hello`的时候，自动帮我们生成hello目录，实现方式
>
> ```yaml
> # _config.yml
> ## 开启后，hexo new [layout] <title> 命令创建新文章时自动创建一个文件夹
> post_asset_folder: true
> ```
>
> 2、图片我直接贴在typora文档中，图片的地址怎么设置成相对路径呢？
>
> ![](/docs/pic/image-20251020221318309.png)
>
> 3、 文章写好了，接下来就要用`hexo g;hexo s` 发布看看了哇~ 结果发现图片不展示呀，检查发现public中html页面上面的图片地址不对
>
> ```html
> <img src="/abc/image.png" alt="aaa" />
>
> 我们实际需要有方案能够改为下面的路径：
> <img src="/news/2025/10/20/abc/image.png" alt="aaa" />
> ```
>
> 4、安装插件`hexo-asset-img` 不用考虑了我已经成功解决了，这个插件就是实现 Typora 等 Markdown 编辑器预览 与 Hexo 发布预览 均能正常显示图片 的。来，跟着走：
>
> ```bash
> # _config.yml
> marked:
>   prependRoot: true
>   postAsset: true
> relative_link: false
>
> # 使用本插件 即可实现 Typora 等 Markdown 编辑器预览 与 Hexo 发布预览 均能正常显示图片
> npm install hexo-asset-img --save
> # 检查一下版本，因为hexo >=7.0 需要使用hexo-asset-img@1.2.0
> npm list hexo-asset-img
>
> └── hexo-asset-img@1.2.0
> ```
>
> 5、再次发布试试咯！ 成功！
> 但是只有 \_posts 下的 Markdown（Post）能自动把图片解析为 post asset 路径，和它同级的 docs 目录下的 Markdown 没有被处理。

https://cloud.tencent.com/developer/article/1970544

https://github.com/yiyungent/hexo-asset-img/blob/main/README_zh.md

```bash
# _config.yml
## 开启后，hexo new [layout] <title> 命令创建新文章时自动创建一个文件夹
post_asset_folder: true
marked:
  prependRoot: true
  postAsset: true
relative_link: false

# 使用本插件 即可实现 Typora 等 Markdown 编辑器预览 与 Hexo 发布预览 均能正常显示图片
npm install hexo-asset-img --save
npm list hexo-asset-img


└── hexo-asset-img@1.2.0

# 插件的作用：
<img src="/abc/image.png" alt="aaa">
变为：
<img src="/news/2025/10/20/abc/image.png" alt="aaa">

mv site/source/_posts site/source/_posts.back
cp my/source/_posts site/source/_posts
```

## 为news页面的文章展示页面添加固定的目录

![](/docs/pic/image.png)

### `site/themes/navy/layout/post.njk`

```html
<div id="content-wrap">
  <div id="content" class="wrapper">
    <div id="content-inner">
      <article
        class="article-container"
        itemscope
        itemtype="http://schema.org/Article"
      >
        <div class="article-inner">
          <div class="article">
            <div class="inner">
              <div class="article-content" itemprop="articleBody">
                {{ partial('partial/post', {post: page}) }}
              </div>
              <footer class="article-footer">
                <time
                  class="article-footer-updated"
                  datetime="{{ date_xml(page.updated) }}"
                  itemprop="dateModified"
                  >{{ __('page.last_updated', date(page.updated)) }}</time
                >
                {{ page_nav() }}
              </footer>
              {{ partial('partial/comment') }}
            </div>
          </div>
          <aside id="article-toc" role="navigation">
            <div id="article-toc-inner">
              {{ partial('partial/carbonads') }}
              <strong class="sidebar-title">{{ __('page.contents') }}</strong>
              {{ toc(page.content, {list_number: false}) }}
              <a href="#" id="article-toc-top">{{ __('page.back_to_top') }}</a>
            </div>
          </aside>
        </div>
      </article>
      {{ partial('partial/sidebar') }}
    </div>
  </div>
</div>
```

### `site/themes/navy/layout/partial/carbonads.njk`

```html
<div id="carbonads" class="carbonads">
  <span class="carbon-wrap">
    <a
      href="https://github.com/booboowei"
      class="carbon-img"
      target="_blank"
      rel="noopener sponsored"
    >
      <img
        src="https://avatars2.githubusercontent.com/u/21328020?s=460&u=88cf6127c32932188f936d05636b7b0d36783ee1&v=4"
        alt="ads via Carbon"
        border="0"
        style="width:80px;height:80px;border-radius:50%;max-width:130px;"
      />
    </a>
    <a
      href="/about/"
      class="carbon-text"
      target="_blank"
      rel="noopener sponsored"
    >
      除了自己的无知，我什么都不知道
    </a>
  </span>
</div>
```

### `site/themes/navy/source/css/_partial/carbonads.styl`

```
#carbonads
  display: block
  overflow: hidden
  margin-top: 40px
  max-width: 130px
  text-align: left
  font-size: 13px
  line-height: 1.5
  a
    color: inherit
    text-decoration: none
  &:hover
    color: inherit
  span
    display: block
    overflow: hidden

.carbon-img
  display: block
  margin: 0 auto 8px
  line-height: 1

.carbon-text
  display: block
  margin-bottom: 8px

.carbon-poweredby
  display: block
  text-transform: uppercase
  letter-spacing: 1px
  font-size: 9px
  line-height: 1
```

### `site/themes/navy/source/css/navy.styl`

```
@import "nib"
@import "_variables"

@import "_partial/base"
@import "_partial/header"
@import "_partial/index"
@import "_partial/sidebar"
@import "_partial/page"
@import "_partial/post"
@import "_partial/plugins"
@import "_partial/archive"
@import "_partial/mobile_nav"
@import "_partial/footer"
@import "_partial/highlight"
@import "_partial/carbonads"
```

## 为其他page展示页面添加固定的目录

```bash
vim site/themes/navy/layout/page.njk
          <aside id="article-toc" role="navigation">
            <div id="article-toc-inner">
              {{ partial('partial/carbonads') }} ## 增加这条
              <strong class="sidebar-title">{{ __('page.contents') }}</strong>
              {{ toc(page.content, {list_number: false}) }}
              <a href="#" id="article-toc-top">{{ __('page.back_to_top') }}</a>
            </div>
          </aside>
```

## 修改 menu | 将 DOC 改为 Hexo

```bash
vim site/source/_data/menu.yml
hexo: /docs/

vim site/themes/navy/languages/en.yml
menu:
  hexo: Hexo

vim site/source/_data/sidebar.yml
docs:
  getting_started:
    overview: index.html
    setup_vscodium: /docs/setup-vscodium.html

vim site/themes/navy/languages/en.yml
sidebar:
  docs:
    getting_started: Getting Started
    overview: Overview
    setup_vscodium: Setup VSCodium
```
