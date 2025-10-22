---
title: Git与GitHub的简单同步
---

| 课程 | 内容                   | 备注                                                     |
| :--- | :--------------------- | :------------------------------------------------------- |
| 30   | 注册一个GitHub账号     | [https://github.com/](https://github.com/)               |
| 31   | 配置公私钥             | [https://help.github.com/cn](https://help.github.com/cn) |
| 32   | 在GitHub上创建个人仓库 | [https://help.github.com/cn](https://help.github.com/cn) |
| 33   | 把本地仓库同步到GitHub | [https://help.github.com/cn](https://help.github.com/cn) |

```shell
git remote -v 查看远程版本库信息
git remote add github <url> 添加github远程版本库
git fetch github 拉取远程版本库
git merge -h 查看合并帮助信息
git merge --allow-unrelated-histories github/master 合并github上的master分支（两分支不是父子关系，所以合并需要添加 --allow-unrelated-histories）
git push github 推送同步到githup仓库


# github上面新建一个空仓库 booboo_site
# 本地目录 booboo_site
# git init
# git add -A
# git commit -m '1'
# 要添加远程存储库的 URL（将在其中推送本地存储库），请运行以下命令。 将 REMOTE-URL 替换为 GitHub 上的存储库完整 URL。
# git remote add origin https://github.com/BoobooWei/booboo_site.git
# 要验证远程 URL 设置是否正确，请运行以下命令。
git remote -v
# 要将本地存储库的更改推送到 GitHub，请运行以下命令。
git push -u origin main --force
```
