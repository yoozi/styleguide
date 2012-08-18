# 游子 PHP 程序代码编码规范

## 0 Preface

除非特别声明，游子旗下所有解决方案、研发产品凡涉及到 PHP 程序的部分，均需严格遵守本编码规范。已存代码、但不符合本规范的部分，需逐步改善形成统一代码风格，以保证代码简洁明了、容易阅读。本规范与 [CodeIgniter 框架编码规范](http://codeigniter.org.cn/user_guide/general/styleguide.html)有许多相似之处，但在部分地方会有所不同。

一切不按此编码规则行事者，都是**耍流氓**。

## 1 约定

## 1.1 文件编码

请调整编辑器文件编码为 Unicode（UTF-8），并关闭 [UTF-8 BOM](http://en.wikipedia.org/wiki/Byte_order_mark) 功能。BOM 可能导致 PHP 产生预期之外的输出，从而中断正常运行的脚本程序（[抛出“headers already sent by”异常](http://stackoverflow.com/questions/8028957/headers-already-sent-by-php)）。

注意：在任何情况下都不要使用 Windows 自带的记事本编辑项目文件。推荐使用 [Sublime Text 2](http://www.sublimetext.com/2) 编辑器作为日常开发编辑器，使用 [Vim](http://www.vim.org/download.php) 作为 Linux 环境下的文本编辑器。团队为开发人员准备了 ST2 的正版序列号，请邮件至 [support@yoozi.cn](support@yoozi.cn) 索要序列号。

## 1.2 UNIX风格换行

使用 UNIX 风格的换行符，即只有换行( LF 或 “\n”)没有回车( CR 或 “\r”)，请在你的编辑器内调整。


