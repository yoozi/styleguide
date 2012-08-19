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

_例外情况_：很多时候我们希望通过对齐某段代码从而使其更具可读性——此时可在行内使用空格。如下所示：


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

### 1.4 PHP 闭合标签

所有 PHP 文件应该省略这个 `?>` 闭合标签，并插入一段注释来标明这是文件的底部。底部注释需要正确插入文件路径和名称。

错误：

```
<?php

echo "Here's my code!";

?>
```

正确：

```
<?php

echo "Here's my code!";

/* End of file myfile.php */
/* Location: ./system/modules/mymodule/myfile.php */
```

_例外情况_：本规则仅适用于纯 PHP 代码文件，混合代码文件（如视图）无需遵循。

### 1.5 TRUE, FALSE 和 NULL

布尔（boolean）常量关键字 `TRUE`与`FALSE`、以及空值常量关键字`NULL`应始终保持大写。

```
if ($foo == TRUE)
$bar = FALSE;
function foo($bar = NULL)
return TRUE;
```

### 1.6 OR, AND 和 !

对于逻辑操作符，使用英文关键字`OR`和`AND`来分别替代他们的简化符号写法`||`和`&&`。原因是，在部分特殊显示外设下，`||`会被识别为`11`。

```
if ($foo OR $bar)
if ($foo AND $bar) // recommended
```

逻辑关键字与非`!`出现时，应保证其前后分别存在一个空格：

```
if ( ! $foo)
if ( ! is_array($foo))
```

## 2 大括号放置

始终使用 [Allman 缩进](http://en.wikipedia.org/wiki/Indent_style#Allman_style)风格进行大括号的放置与代码缩进：除了类（Class）声明之外，括号总是独占一行，且需缩进至当前控制语句同级，括号内语句需缩进至下一级别。

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

## 3 逗号与空格

### 3.1 逗号放置

函数中用逗号来分隔参数，所有的参数与前面的逗号之间要空格(第一个参数除外)。

```
public function connect($host, $port, $db, $user, $password, $charset = NULL)
```

### 3.2 方括号及圆括号内的空格

不要在方括号`[]`和圆括号`()`内增加任何空格符。

```
// 错误：
$arr[ $foo ] = 'foo';
// 正确：
$arr[$foo] = 'foo'; // no spaces around array keys

// 错误：
function foo ( $bar ) {}

// 正确：
function foo($bar) // no spaces around parenthesis in function declarations
{

}
```

_例外情况_：在结构控制语句后通常需要跟一个空格，以更好将控制体与普通函数区分开来。

```
// 错误：
foreach( $query->result() as $row )

// 正确：
foreach ($query->result() as $row) // single space following PHP control structures, but not in interior parenthesis
```

## 3.3 操作符空格的使用

除了如 3.1 参数之间要使用空格外，所有操作符之间都要使用空格，包括字符连接符(.)。

```
$host . ':' . $port
```