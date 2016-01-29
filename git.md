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


