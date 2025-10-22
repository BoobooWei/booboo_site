---
title: 编辑器选择 VSCodium
categories:
  - news
tags:
  - hexo
  - VSCodium
date: 2025-10-17 18:33:39
---

## 背景

之前一直保持写技术博客的习惯，加入现在的公司后，太忙了，已经间隔3年多没有写博客了，最近想重新整理工作中的技术知识，发现电脑中的编辑环境都没有了。之前喜欢用 `Typora`+ `Atom`, 现在发现atom的插件已经不更新了，即使安装了使用上也有问题，尤其的markdown的插件。

不得不重新寻找替代方案了。

如果只是快速写 Markdown 文档，我已经购买了Typora，但是它有个问题，就是TOC并不是html的语法，而是`[toc]` 命令，因此不能完全满足。

**生成 TOC 的示例：**

```
<!-- TOC -->
- [章节一](#章节一)
- [章节二](#章节二)
<!-- /TOC -->
```

我喜欢的是那种能快速写 Markdown 文档、自动生成目录（TOC）、轻量但又能扩展的编辑环境，那就精准锁定：**支持 Markdown + 自动 TOC 的现代替代方案** 💪

## chatgpt推荐

| 使用风格                     | 推荐编辑器             | 备注                                                      |
| ---------------------------- | ---------------------- | --------------------------------------------------------- |
| 想延续 Atom + 插件生态       | **VS Code / VSCodium** | 推荐组合：Markdown All in One + Markdown Preview Enhanced |
| 想体验 Atom 团队新作         | **Zed**                | 新一代编辑器，轻快漂亮                                    |
| 笔记 / 知识管理 / 结构化写作 | **Obsidian**           | TOC、标签、双链一应俱全                                   |
| 专注写 Markdown，无干扰      | **Typora**             | 简洁、稳定、可导出                                        |

# VSCodium

---

## 1 安装 VS Code（或 VSCodium）

- **官方下载地址：**
  👉 https://code.visualstudio.com/
- （如果你更注重隐私、想要无遥测版本）
  👉 https://vscodium.com/

两者界面几乎一模一样，插件也完全兼容。

```bash
brew install --cask vscodium

==> Downloading https://github.com/VSCodium/vscodium/releases/download/1.105.06808/VSCodium-darwin-arm6
==> Downloading from https://release-assets.githubusercontent.com/github-production-release-asset/14459
################################################################################################ 100.0%
==> Installing Cask vscodium
==> Moving App 'VSCodium.app' to '/Applications/VSCodium.app'
==> Linking Binary 'codium' to '/opt/homebrew/bin/codium'
🍺  vscodium was successfully installed!
```

---

## 2 安装 Markdown 插件组合（核心四件套）

| 功能                          | 插件名      | 作者                                   | 用途说明 |
| ----------------------------- | ----------- | -------------------------------------- | -------- |
| **Markdown All in One**       | _Yu Zhang_  | 自动生成 / 更新目录（TOC），快捷键丰富 |          |
| **Markdown Preview Enhanced** | _Yiyi Wang_ | 实时预览、公式渲染、导出 PDF / HTML    |          |
| **Markdown PDF**              | _yzane_     | 一键导出为 PDF                         |          |
| **Prettier – Code Formatter** | _Prettier_  | 自动格式化 Markdown（对齐缩进、列表）  |          |

> 🔹安装方式：
> 在 VS Code 里打开扩展（左侧方块图标） → 搜索插件名 → 点击 **Install**。

---

## 3 配置自动生成目录（TOC）

安装 **Markdown All in One** 后：

1. 在 Markdown 文件中放置光标，输入：

   ```markdown
   <!-- TOC -->
   <!-- /TOC -->
   ```

2. 按下：

   ```
   Ctrl + Shift + P
   ```

   搜索命令：

   ```
   Create Table of Contents
   ```

   💡 即可自动生成目录（标题自动识别，自动加锚点）。

3. 每次保存文件时，TOC 会自动更新（可在设置中开关）。

---

## 4 可选优化配置（建议）

打开 VS Code 的设置文件（`Ctrl + ,` → 搜索 `"settings.json"` → 点击右上角 “Open Settings (JSON)”）
添加以下配置片段：

```json
{
  "markdown.extension.toc.levels": "1..3",
  "markdown.extension.toc.updateOnSave": true,
  "markdown.preview.breaks": true,
  "markdown.preview.scrollEditorWithPreview": true,
  "markdown.preview.scrollPreviewWithEditor": true,
  "markdown-preview-enhanced.previewTheme": "github-light.css",
  "editor.wordWrap": "on",
  "editor.renderWhitespace": "all"
}
```

含义说明：

- 自动更新 TOC；
- 预览与编辑同步滚动；
- 样式使用 GitHub 风格；
- 自动换行；
- 显示空格和缩进辅助。

---

## 5 导出为 PDF / HTML

打开 Markdown 文件后：

- 右键 → 选择 **Markdown PDF: Export (pdf)**
  即可导出带目录的 PDF。
  （如果目录点击不跳转，可在导出前确保标题格式标准，如 `## 标题`）

---

## 6 进阶插件推荐（可选）

| 插件名                         | 功能                                               |
| ------------------------------ | -------------------------------------------------- |
| **Paste Image**                | 截图后粘贴图片，自动保存到本地并插入 Markdown 链接 |
| **Markdown Notes**             | 自动链接同文件夹下的文档，像 Obsidian 一样         |
| **GitHub Theme / Tokyo Night** | 美化 Markdown 预览界面                             |
| **Spell Right**                | 拼写检查（支持中英文混写）                         |

---

## 7 你的第一份 Markdown 文件试跑

```markdown
# 我的 Markdown 测试

<!-- TOC -->
<!-- /TOC -->

## 一、引言

写 Markdown 真香。

## 二、自动目录

保存后这里会自动生成 TOC。

## 三、导出测试

可以导出成漂亮的 PDF。
```

保存文件 → 按 `Ctrl + Shift + V` 打开右侧实时预览，你会看到自动生成的目录 🎉
