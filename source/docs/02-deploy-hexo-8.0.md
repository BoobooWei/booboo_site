---
title: Hexo部署最新版本
categories:
  - news
tags:
  - hexo
date: 2025-10-20 19:33:39
---

## help

[hexo doc](https://hexo.io/zh-cn/docs/)

| Hexo 版本 | 最低版本 (Node.js 版本) | 最高版本 (Node.js 版本) |
| :-------- | :---------------------- | :---------------------- |
| 7.0+      | 14.0.0                  | latest                  |

## 实际安装版本

先试一下是否能恢复之前的环境，如果不行，就使用最新的hexo版本

### install git@2.39.5

```bash
$ git --version
git version 2.39.5 (Apple Git-154)
```

### install node@v22.20.0

```bash
This package has installed:
    •	Node.js v22.20.0 to /usr/local/bin/node
    •	npm v10.9.3 to /usr/local/bin/npm
Make sure that /usr/local/bin is in your $PATH.

# Verify the Node.js version:
node -v # Should print "v22.20.0".
# Verify npm version:
npm -v # Should print "10.9.3".
npm install -g npm@11.6.2
```

### install hexo-cli@4.3.2

```bash
# 修改 npm 全局安装路径
# 创建一个用户专属的全局安装目录：
mkdir "${HOME}/.npm-global"
# 告诉 npm 以后把全局包装在这里：
npm config set prefix "${HOME}/.npm-global"
# 把这个目录加进 PATH（让命令行能找到）：
echo 'export PATH=$HOME/.npm-global/bin:$PATH' >> ~/.zshrc
source ~/.zshrc

npm install -g hexo-cli

hexo --version
hexo-cli: 4.3.2
os: darwin 24.6.0 15.6.1

node: 22.20.0
acorn: 8.15.0
ada: 2.9.2
amaro: 1.1.2
ares: 1.34.5
brotli: 1.1.0
cjs_module_lexer: 2.1.0
cldr: 47.0
icu: 77.1
llhttp: 9.3.0
modules: 127
napi: 10
nbytes: 0.1.1
ncrypto: 0.0.1
nghttp2: 1.64.0
openssl: 3.5.2
simdjson: 3.13.0
simdutf: 6.4.2
sqlite: 3.50.4
tz: 2025b
undici: 6.21.2
unicode: 16.0
uv: 1.51.0
uvwasi: 0.0.23
v8: 12.4.254.21-node.33
zlib: 1.3.1-470d3a2
zstd: 1.5.7
```

### install hexo@8.0.0

```bash
npm install hexo

hexo@8.0.0

echo 'export PATH="$PATH:/Users/booboowei/Desktop/个人博客/node_modules/.bin"' >> ~/.zshrc
```
