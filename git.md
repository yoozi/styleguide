Git使用规范
================

## Git config

* 必须「MUST」设置Git用户相关信息，如下所示：

    ```
    # 中文名 公司邮箱
    # 张三 zhangsan@domain.com
    git config --global user.name "张三"
    git config --global user.email "zhangsan@domain.com"
    ```

* 必须「MUST」设置如下配置：

    ```
    # 原样checkout，Unix LF 换行格式commit。
    git config --global core.autocrlf input
    # UTF-8 编码
    git config --global i18n.logoutputencoding utf8
    git config --global i18n.commitencoding utf8
    ```

## `gitignore` file

* 由于项目使用技术和框架不一定一致，`gitignore` 首先必须「MUST」根据 [gitignore项目](https://github.com/github/gitignore) 指引使用。
* 在 [gitignore项目](https://github.com/github/gitignore) 中没有找到相关所使用的技术框架，必须「MUST」研发部开会讨论。
* 已定义`gitignore`文件在`files/gitignore`子文件夹中。目前有：
    * document.gitignore
    * laravel-project.gitignore

## `gitattributes` file

> TODO:
待说明

> See Also:
Path-based git attributes
https://www.kernel.org/pub/software/scm/git/docs/gitattributes.html


## 分支管理

对于一个代码类项目。

固定分支

Name           | Usage
---------------|----------------------------------------
develop        | 开发主分支
master         | 主分支,代码功能已经稳定
pre-production | 准备上线功能,内部测试服务器环境,供完整测试
production     | 正式服务器线上环境


临时分支

Name        | Usage
------------|--------------------------------
feature/xxx | 新增功能
fix/xxx     | 修复功能

使用斜杠 `/` 和 减号 `-` 分隔。

## 协作流程



图形界面操作略，以下是命令行操作：

1. 首先克隆 `ssh://git@github.com/xxx/test.git`
	```
    # ~/home
    git clone ssh://git@github.com/xxx/test.git
    ```

2. 建立分支 `develop` 和 `feature/user-extension`
    ```
    # ~/home
    cd test
    (master)$: git branch develop
    (master)$: git branch feature/user-extension
    ```

3. 切换当前分支到 `feature/user-extension`，开发新功能
    ```
    (master)$: git checkout feature/user-extension
    (feature/user-extension)$: git add xxx
    (feature/user-extension)$: git commit -am 'Added function user-add' -s
    ## BLABLABLA
    (feature/user-extension)$: git add xxx
    (feature/user-extension)$: git commit -am 'Added function user-delete' -s
    ```

4. 功能开发完成后，Push 本地 `feature/user-extension` 至 remote `feature/user-extentsion`
    ```
    git push origin feature/user-extension
    ```

5. 建议在 `http://github.com/` 上发起 Pull Request  之前 rebase


## Git commit

* 新功能或 Bug 要创建 Issue 追踪, 确认解决后 Commit 开头 `Fixed #123 解决了某某BUG` 会自动把 `Issue 123` 关闭。

* 简单

    * Added 新加入的需求
    * Fixed 修正Bug
    * Changed/Modified 修改功能
    * Updated 完成任务，或者模块变化做的更新
    * Removed 移除
    * Refactored 重构

* 复杂

    * 第一行为对改动的简要总结，建议长度不超过 50，用语采用命令式而非过去式。

        Vim很贴心，在默认配置下，注释的第一行文字颜色是黄色，超过50列之后就变成白色了。
        格式可参考上面「简单」

    * 第一行结尾不要英文的句号「.」，中文的就也不要「。」吧。


    * 第二行为空行。

        如果配置了自动发送邮件，那么第一行就用来做邮件标题， 第三行开始的内容是邮件正文， 第二行是分隔线，用于区分两者。

    * 第三行开始，是对改动的详细介绍，可以是多行内容，建议每行长度不超过72。

        可以包括原因、做法、效果等很多内容，一切你认为与当前改动相关的。为何是72长度呢？因为git log输出的时候能显示得比较好看，前面4个空格作为缩进，后面留4个空格机动（英文按单词排版）。Vim的gq命令排版很方便。

        一些项目还对这个部分的内容有特殊要求，比如加一些特定标签什么的。

    * 建议使用中文，务必 UTF-8 编码。也可使用全英文，首字母大写。禁止在描述中，中英文语句混搭。

    * 避免注释不清晰。

        比如只有「修正 BUG」、「改错」、「升级」、「添加某文件」等，没有其他内容，等于没说。

    * 一个改动不一次提交完成。

        「提交」的概念是具有独立的功能、修正等作用。小可以小到只修改一行，大可以到改动很多文件，但划分的标准不变，一个提交就是解决一个问题的。对格式的修正，不应该和其他功能修补一起提交，这种情况应该考虑使用 `git add --edit` ，`git add -p` 也可以用用，更复杂和强大一些。在提交前，按实际情况，可使用 `Rebase` 压缩自己本地的多个小提交。

* 特殊

    * 版本号更新

        格式： `Bump version: 0.1.2-dev → 0.1.2`


参考资料
==========

https://ruby-china.org/topics/15737

https://github.com/erlang/otp/wiki/Writing-good-commit-messages

https://www.gitignore.io

https://github.com/thephpleague/skeleton

https://www.reddit.com/r/PHP/comments/2jzp6k/i_dont_need_your_tests_in_my_production

https://www.kernel.org/pub/software/scm/git/docs/gitattributes.html