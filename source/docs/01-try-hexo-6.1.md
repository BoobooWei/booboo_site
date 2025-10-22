---
title: Hexo博客本地环境恢复失败记录
categories:
  - news
tags:
  - hexo
date: 2025-10-20 18:33:39
---

## help

[site](https://github.com/BoobooWei/site/tree/master)
[hexo doc](https://hexo.io/zh-cn/docs/)
[hexo package](https://www.npmjs.com/package/hexo?activeTab=versions)

## 依赖软件版本

hexo: v6.1.0
hexo-cli: v4.2.0
node: v14.15.5

## 实际安装版本

先试一下是否能恢复之前的环境，如果不行，就使用最新的hexo版本

### install git@2.39.5

```bash
$ git --version
git version 2.39.5 (Apple Git-154)

$ git clone https://github.com/BoobooWei/site.git

```

### install node@v14.21.3

```bash
# 6.0+	hexo 对应的 node版本：12.13.0 ~18.5.0
# 本次安装 v14.21.3 版本
This package will install:
    •	Node.js v14.21.3 to /usr/local/bin/node
    •	npm v6.14.18 to /usr/local/bin/npm

# Verify the Node.js version:
node -v # Should print "v14.21.3".

# Verify npm version:
npm -v # Should print "6.14.18".
```

### install hexo-cli@4.2.0

```bash
# 修改 npm 全局安装路径
# 创建一个用户专属的全局安装目录：
mkdir "${HOME}/.npm-global"
# 告诉 npm 以后把全局包装在这里：
npm config set prefix "${HOME}/.npm-global"
# 把这个目录加进 PATH（让命令行能找到）：
echo 'export PATH=$HOME/.npm-global/bin:$PATH' >> ~/.zshrc
source ~/.zshrc
# 安装指定版本的 hexo-cli
sudo npm install -g hexo-cli@4.2.0
/Users/booboowei/.npm-global/bin/hexo -> /Users/booboowei/.npm-global/lib/node_modules/hexo-cli/bin/hexo
+ hexo-cli@4.2.0
added 60 packages from 53 contributors in 2.389s

$ which hexo
/Users/booboowei/.npm-global/bin/hexo
$ hexo --version
hexo-cli: 4.2.0
os: Darwin 24.6.0 darwin x64
node: 14.21.3
v8: 8.4.371.23-node.88
uv: 1.42.0
zlib: 1.2.11
brotli: 1.0.9
ares: 1.18.1
modules: 83
nghttp2: 1.42.0
napi: 8
llhttp: 2.1.6
openssl: 1.1.1t
cldr: 40.0
icu: 70.1
tz: 2022f
unicode: 14.0

```

### install hexo@6.1.0

```bash
npm install hexo@6.1.0

+ hexo@6.1.0
added 99 packages from 90 contributors and audited 99 packages in 7.1s
👉 Hexo 已经成功安装了，并没有失败。

echo 'export PATH="$PATH:/Users/booboowei/Desktop/个人博客/node_modules/.bin"' >> ~/.zshrc
```

## 验证hexo是否可以正常工作|不行老版本hexo有很多不兼容

```bash
$ cd /Users/booboowei/Desktop/个人博客
$ hexo init 2025Blog

INFO  Cloning hexo-starter https://github.com/hexojs/hexo-starter.git
INFO  Install dependencies
added 232 packages from 203 contributors and audited 234 packages in 5.994s

36 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities

INFO  Start blogging with Hexo!

$ cd 2025Blog
$ npm install

# 初始化后，您的项目文件夹将如下所示：
[2025Blog]$ tree ./ -L 1
./
├── _config.landscape.yml
├── _config.yml
├── node_modules
├── package-lock.json
├── package.json
├── scaffolds
├── source
└── themes

[2025Blog]$ hexo new 01
FATAL
Error [ERR_REQUIRE_ESM]: Must use import to load ES Module: /Users/booboowei/Desktop/个人博客/2025Blog/node_modules/strip-ansi/index.js
require() of ES modules is not supported.
require() of /Users/booboowei/Desktop/个人博客/2025Blog/node_modules/strip-ansi/index.js from /Users/booboowei/Desktop/个人博客/2025Blog/node_modules/hexo/dist/plugins/console/list/common.js is an ES module file as it is a .js file whose nearest parent package.json contains "type": "module" which defines all .js files in that package scope as ES modules.
Instead rename index.js to end in .cjs, change the requiring code to use import(), or remove "type": "module" from /Users/booboowei/Desktop/个人博客/2025Blog/node_modules/strip-ansi/package.json.

    at new NodeError (internal/errors.js:322:7)
    at Object.Module._extensions..js (internal/modules/cjs/loader.js:1131:13)
    at Module.load (internal/modules/cjs/loader.js:979:32)
    at Function.Module._load (internal/modules/cjs/loader.js:819:12)
    at Module.require (internal/modules/cjs/loader.js:1003:19)
    at require (internal/modules/cjs/helpers.js:107:18)
    at Object.<anonymous> (/Users/booboowei/Desktop/个人博客/2025Blog/node_modules/hexo/dist/plugins/console/list/common.js:7:38)
    at Module._compile (internal/modules/cjs/loader.js:1114:14)
    at Object.Module._extensions..js (internal/modules/cjs/loader.js:1143:10)
    at Module.load (internal/modules/cjs/loader.js:979:32)
    at Function.Module._load (internal/modules/cjs/loader.js:819:12)
    at Module.require (internal/modules/cjs/loader.js:1003:19)
    at require (internal/modules/cjs/helpers.js:107:18)
    at Object.<anonymous> (/Users/booboowei/Desktop/个人博客/2025Blog/node_modules/hexo/dist/plugins/console/list/page.js:7:18)
    at Module._compile (internal/modules/cjs/loader.js:1114:14)
    at Object.Module._extensions..js (internal/modules/cjs/loader.js:1143:10)
    at Module.load (internal/modules/cjs/loader.js:979:32)
    at Function.Module._load (internal/modules/cjs/loader.js:819:12)
    at Module.require (internal/modules/cjs/loader.js:1003:19)
    at require (internal/modules/cjs/helpers.js:107:18)
    at Object.<anonymous> (/Users/booboowei/Desktop/个人博客/2025Blog/node_modules/hexo/dist/plugins/console/list/index.js:6:32)
    at Module._compile (internal/modules/cjs/loader.js:1114:14)
```

## 卸载环境

有时候环境乱掉、版本冲突、或者想“重来一遍干净的安装”，确实得彻底清理。
卸载 Hexo、Hexo CLI、Node.js，确保系统干净。

```bash
npm uninstall -g hexo
npm uninstall -g hexo-cli
sudo rm -rf /usr/local/bin/npm
sudo rm -rf /usr/local/bin/node

# 清理~/.zshrc
vim ~/.zshrc
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion

export PATH=$HOME/.npm-global/bin:$PATH
export PATH="$PATH:/Users/booboowei/Desktop/个人博客/node_modules/.bin"

node -v
npm -v
hexo -v


```
