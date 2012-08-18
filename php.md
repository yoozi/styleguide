# 游子 PHP 编码规范

## 0 Preface

除非特别声明，游子旗下所有解决方案、研发产品凡涉及到 PHP 程序的部分，均需严格遵守本编码规范。已存代码、但不符合本规范的部分，需逐步改善形成统一代码风格，以保证代码简洁明了、容易阅读。本规范与 [CodeIgniter 框架编码规范](http://codeigniter.org.cn/user_guide/general/styleguide.html)有许多相似之处，但在部分地方会有所不同。

一切不按此编码规则行事者，都是**耍流氓**。

## 1 约定

### 1.1 文件编码

请调整编辑器文件编码为 Unicode（UTF-8），并关闭 [UTF-8 BOM](http://en.wikipedia.org/wiki/Byte_order_mark) 功能。BOM 可能导致 PHP 产生预期之外的输出，从而中断正常运行的脚本程序（[抛出“headers already sent by”异常](http://stackoverflow.com/questions/8028957/headers-already-sent-by-php)）。

注意：在任何情况下都不要使用 Windows 自带的记事本编辑项目文件。推荐使用 [Sublime Text 2](http://www.sublimetext.com/2) 编辑器作为日常开发编辑器，使用 [Vim](http://www.vim.org/download.php) 作为 Linux 环境下的文本编辑器。团队为开发人员准备了 ST2 的正版序列号，请邮件至 [support@yoozi.cn](support@yoozi.cn) 索要序列号。

### 1.2 UNIX风格换行

使用 UNIX 风格的换行符，即只有换行( LF 或 “\n”)没有回车( CR 或 “\r”)，请在你的编辑器内调整。

### 1.3 代码缩进

黄金准则是：**在行首使用 tab 缩进, 在行内使用空格。**

每次使用一个 tab （宽度：4）进行代码缩进，从而表现代码的逻辑结构。使用 tab 代替空格有利于那些阅读你代码的开发者在他们各自所使用的编辑器中自定义缩进方式。

*例外情况*：很多时候我们希望通过对齐某段代码从而使其更具可读性——此时可在行内使用空格。如下所示：


```
[tab]$foo   = 'somevalue';
[tab]$foo2  = 'somevalue2';
[tab]$foo34 = 'somevalue3';
[tab]$foo5  = 'somevalue4';
```

对于多维数组通常也存在此情况。例如：

```
$my_array = array(
[tab]'foo'   => 'somevalue',
[tab]'foo2'  => 'somevalue2',
[tab]'foo3'  => 'somevalue3',
[tab]'foo34' => 'somevalue3',
);
```

### 1.4 缩进风格

始终使用 [Allman 缩进](http://en.wikipedia.org/wiki/Indent_style#Allman_style)风格进行缩进：除了类（Class）声明之外，括号总是独占一行，且需缩进至当前控制语句同级，括号内语句需缩进至下一级别。

```
// 错误
while (x == y) {
    something();
    somethingelse();
}

// 正确
while (x == y)
{
    something();
    somethingelse();
}

// 错误
if ($foo == $bar) {
 // ...
} else {
 // ...
}

// 正确
if ($foo == $bar)
{
	// do something...
}
else
{
	// do another...
}
```

### 1.5 PHP 闭合标签

所有 PHP 文件应该省略这个 `?>` 闭合标签，并插入一段注释来标明这是文件的底部。底部注释需要正确插入文件路径和名称。

错误做法：

```
<?php

echo "Here's my code!";

?>
```

正确做法：

```
<?php

echo "Here's my code!";

/* End of file myfile.php */
/* Location: ./system/modules/mymodule/myfile.php */
```

*例外情况*： 本规则仅适用于纯 PHP 代码文件，混合代码文件（如视图）无需遵循。