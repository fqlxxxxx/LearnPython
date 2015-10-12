# 0Week(10.12~16)

#### 课前"被动"自学体验:
* 找到了一个国外非常棒的技术方面的互助问答网站 stackoverflow, 已经帮助我解决非常多的软件使用配置问题.
* 逐渐习惯了看官方文档的习惯,
* 看到英文文档也不是发憷了, 虽然还有不少单词不认识.
* 通过查看官方文档最终解决了不少问题, 比如github 和 Gitbook 互通的操作.

## 配置学习生产环境
** 想法: **
* 工具选择
    * 选择一款合适的 GitHub 客户端工具
    * 选择一款合适的 markdown 工具
    * 选择一款合适的代码编辑工具
* 实现功能
    * GitHub 与 Gitbook互通, 即在 GitHub 和 Gitbook 任一网站上修改相关文件,两边都可以同步.
    * markdown工具 与 GitHub/Gitbook 互通, 编辑后不用再调整summary, commit & push到 GitHub 上即可更新 Gitbook
    * 代码工具至少满足: 好看, 代码自动补齐, 代码高亮, 可直接或间接执行 .py

## 任务
* 大妈任务
    * 实现 GitHub 与 Gitbook 互通
    * 配置 Gitbook 评论插件
    * 根据极简 Python 上手导念中的一页解说 Python 代码
    * 录入为个人仓库中的 ```_src/om2py0w/0wex0/main.py ```
    * … …
* 本周个人任务
    * 搞懂 git 的运行逻辑
    * 对 GitHub 的基础操作熟练上手
    * 笨办法学 Python继续, 每天1~2课的进度
    * 记录本周学习中的 坑和体会
* 未来个人任务
    * 命令行操作git
    * 深入熟悉掌握 GitHub
   
##遇到难题
1. 使用Github的webhook服务推送到gitbook时，不稳定，两次成功其余不成功，提示无效授权。
    * 原来只需要在 gitbook 中设置好 github 的仓库名字即可,不用设置下面的 webhook.耽误了两天时间, 纠结 webhook 的设置, 这个 webhook 究竟是个什么鬼?
    * >Webhooks allow GitBook to be notified when you push to the GitHub repository (only public repos).
    * >Webhooks allow external services to be notified when certain events happen within your repository. When the specified events happen, we’ll send a POST request to each of the URLs you provide. Learn more in our Webhooks Guide.
2. 执行git serve、安装disqus插件时不成功。






## 待解疑问
* GitHub网页端如何 revert last commit？
* 怎么使用 git 备份并管理代码?
* github客户端和网页版什么关系?
* github 网页版是否能 revert last commit?


