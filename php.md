# PHP 工程编码规范和使用指南

> Code is poetry.

> (Wordpress)

## 0 声明

除特别说明，游子/奥飞智能旗下所有解决方案、研发产品凡涉及 PHP 程序的部分，均必须 MUST 严格遵守本编码规范。现存代码不符合本规范的部分，需逐步改善形成本规范所规定的代码风格。

本规范自 2016Q1 起正式对游子科技和奥飞智能科技（奥飞娱乐智能事业部）研发部生效。

## 1 编码规范

本规范基本遵循 [Laravel 贡献指南中](https://laravel.com/docs/5.2/contributions)的编码规范说明，PHP 工程必须 MUST 遵循 [PSR-2 编码规范](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md)和 [PSR-4 自动加载规范](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader.md)。

## 2 编辑器和工具

### 2.1 推荐 IDE

团队成员可以按个人偏好选择 IDE 编辑器，但我们推荐使用如下 IDE 编辑器：

* 推荐使用 [Sublime Text](http://www.sublimetext.com/) 作为日常开发编辑器。
* 推荐使用 [Vim](http://www.vim.org/download.php) 作为 Linux 环境下的文本编辑器。
* 请不要使用 Windows 自带的记事本（Notepad）编辑项目文件。

对 Vim 不熟悉或欠熟悉的同学，请前往 [OpenVim](http://www.openvim.com/tutorial.html) 网站进行学习。

### 2.2 EditorConfig 插件

各主流 IDE 均支持 ``.editorconfig`` 用于编码规范的定义和约束，请下载并安装相应 IDE 支持的 EditorConfig 插件：

http://editorconfig.org/

### 2.3 代码风格修正

在提交代码到版本库前，开发人员可以使用 [PHP-CS-Fixer](https://github.com/FriendsOfPHP/PHP-CS-Fixer) 对代码风格进行检查和修复。

在完成[全局安装](https://github.com/FriendsOfPHP/PHP-CS-Fixer#globally-manual)后，开发人员可以通过命令行进入项目工程根目录下执行如下命令完成检查：

```
php-cs-fixer fix
```

## 3 开发环境

无论是 Ubuntu/OS X，推荐开发人员使用 [VirtualBox](https://www.virtualbox.org/wiki/Downloads) + [Vagrant](https://www.vagrantup.com/) 虚拟机组合工具进行日常开发，具体来说：

* 如果在研项目中存在自定义的 Vagrant 配置，则优先使用项目配置。
* 如果在研项目没有指定 Vagrant 虚拟机配置，则应该使用 Laravel 官方推荐的 [Homestead](https://laravel.com/docs/5.2/homestead) 配置。

## 3 作者

* Saturn：<yangg.hu@yoozi.cn>

## 4 引用/参考

1. https://laravel.com/docs/5.2/contributions
2. http://editorconfig.org/
3. https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md
4. https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader.md

## 5 参与互动

通过如下两种方式之一来参与互动：

* 请直接 [fork 本项目](https://github.com/yoozi/styleguide)，然后 pull request 即可。
* 直接提交[改进建议](https://github.com/yoozi/styleguide/issues/new)。