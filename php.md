# 游子 PHP 编码规范

## 0 声明

除非特别声明，游子旗下所有解决方案、研发产品凡涉及 PHP 程序的部分，均需严格遵守本编码规范。已存代码、但不符合本规范的部分，需逐步改善形成统一代码风格，以保证代码简洁明了、容易阅读。本规范与 [CodeIgniter 框架编码规范](http://codeigniter.org.cn/user_guide/general/styleguide.html)有许多相似之处，但在部分地方会有所不同。

一切不按此编码规范行事者，都是**耍流氓**。

## 1 约定

### 1.1 文件编码

请调整编辑器文件编码为 Unicode（UTF-8），并关闭 [UTF-8 BOM](http://en.wikipedia.org/wiki/Byte_order_mark) 功能。BOM 可能导致 PHP 产生预期之外的输出，从而中断正常运行的脚本程序（[抛出“headers already sent by”异常](http://stackoverflow.com/questions/8028957/headers-already-sent-by-php)）。

请不要使用 Windows 自带的记事本（Notepad）编辑项目文件。团队推荐如下编辑器：

* 使用 [Sublime Text 2](http://www.sublimetext.com/2) 作为日常开发编辑器。我们为开发人员准备了 ST2 的正版序列号，请邮件至 [support@yoozi.cn](support@yoozi.cn) 索要序列号。
* 使用 [Vim](http://www.vim.org/download.php) 作为 Linux 环境下的文本编辑器。对 Vim 不熟悉或欠熟悉的同学，请前往 [OpenVim](http://www.openvim.com/tutorial.html) 网站进行学习。

鉴于团队的所有全职开发人员、部分高级技术顾问将会采用 Mac OS X 作为日常开发环境，我们还推荐其使用 [Panic Coda](http://panic.com/coda/) 作为 Mac 下备选 IDE。

### 1.2 UNIX风格换行

使用 UNIX 风格的换行符，即只有换行( LF 或 “\n”)没有回车( CR 或 “\r”)，请在你的编辑器内作相应调整。

### 1.3 代码缩进

**在行首使用 tab 缩进, 在行内使用空格。**

每次使用一个 tab （宽度：4）进行代码缩进，从而表现代码的逻辑结构。使用 tab 代替空格有利于那些阅读你代码的开发者在他们各自所使用的编辑器中自定义缩进方式。

例外情况：很多时候我们希望通过对齐某段代码从而使其更具可读性——此时可在行内使用空格。如下所示：


```
[tab]$foo   = 'somevalue';
[tab]$foo2  = 'somevalue2';
[tab]$foo34 = 'somevalue3';
[tab]$foo5  = 'somevalue4';
```

对于多维数组通常也存在类似例外情况。例如：

```
$my_array = array(
[tab]'foo'   => 'somevalue',
[tab]'foo2'  => 'somevalue2',
[tab]'foo3'  => 'somevalue3',
[tab]'foo34' => 'somevalue3',
);
```

### 1.4 PHP 闭合标签

所有 PHP 文件应该省略文件结尾 `?>` 闭合标签，并插入一段注释来标明这是文件的底部。底部注释需要正确插入文件路径和名称。

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

例外情况：本规则仅适用于纯 PHP 代码文件，混合代码文件（如视图）无需遵循。

### 1.5 TRUE, FALSE 和 NULL

布尔（boolean）常量关键字 `TRUE` 与 `FALSE` 、以及空值常量关键字 `NULL` 应始终保持大写。

```
if ($foo == TRUE)
$bar = FALSE;
function foo($bar = NULL)
return TRUE;
```

### 1.6 OR, AND 和 !

对于逻辑操作符，使用英文关键字 `OR` 和 `AND` 来分别替代他们的简化符号写法 `||` 和 `&&` 。因为在部分特殊显示外设下， `||` 会被识别为 `11` ，从而降低代码可读性。

```
if ($foo OR $bar) // recommended
if ($foo AND $bar) // recommended
```

逻辑关键字与非 `!` 出现时，应保证其前后分别存在一个空格：

```
if ( ! $foo)
if ( ! is_array($foo))
```

### 1.7 比较返回值和强制转换

有些 PHP 函数（如 `strpos`）在执行失败时会返回 `FALSE`，但由于它们也可能返回 `""` 和 `0` 这样的有效值——在逻辑判断时，`FALSE` / `""` / `0`三个中的任何一个值都会导致松散比较（`==`）返回 `FALSE`。处理此类函数需要尤其注意，否则松散比较可能会导致非期望的结果。

对于所有需要通过比较、或判断返回值的场景下，请按需使用 `===` 和 `!==` 这样的操作符。

```
// 错误:
// If 'foo' is at the beginning of the string, strpos will return a 0,
// resulting in this conditional evaluating as TRUE
if (strpos($str, 'foo') == FALSE)

// 正确:
if (strpos($str, 'foo') === FALSE)
```

```
// 错误:
function build_string($str = "")
{
	if ($str == "")	// 假设此时传入 0 或 FALSE 时，会产生何结果？
	{

	}
}

// 正确：
function build_string($str = "")
{
	if ($str === "")
	{

	}
}
```

有时为了确保逻辑比较的严谨、防止出现 bug，我们可能会需要对输入参数执行[强制转换](http://us3.php.net/manual/en/language.types.type-juggling.php#language.types.typecasting)操作，然后才进行逻辑比较。例如：在字符串强制转换中，`NULL` 和 布尔值 `FALSE` 将会转化成值为 `""`(长度为 0 的字符串)，而布尔值 `TRUE` 将会被转化成值为 `"1"` 的字符串。

```
$str = (string) $str;	// cast $str as a string
$str = (string) 1; // "1"
$str = (string) TRUE; // "1"
$str = (string) NULL; // ""
$str = (string) 123; // "123"
```

### 1.8 短标签

请不要使用短标签：即简写 PHP 的开启标签、闭合标签。

```
// 错误：
<? echo $foo; ?>
<?=$foo?>

// 正确：
<?php echo $foo;?>
```

### 1.9 每行一条语句

保证每行一条 PHP 语句，请不要在一行写多条语句。

```
// 错误：
$foo = 'this'; $bar = 'that'; $bat = str_replace($foo, $bar, $bag);

// 正确：
$foo = 'this';
$bar = 'that';
$bat = str_replace($foo, $bar, $bag);
```

### 1.10 长语句请换行

当语句过长、超过 80 个字符宽度时，请折行编写。折行的所有子语句需前进一个 tab 的宽度。

```
// Let's do it!
$this->template
[tab]->title(lang('browse.category_title', $this->city_name))
[tab]->set_metadata('description', lang('browse.category_desc'), 'meta')
[tab]->inject_partial('show_top_topic', TRUE)
[tab]->inject_partial('active_category', -1)
[tab]->build('browse/index', $this->data);
```

```
// 保持 SQL 语句中的关键词大写
// 考虑到可读性，请将句子分成多行来写
$query = $this->db->query("SELECT foo, bar, baz, foofoo, foobar AS raboof, foobaz
[tab]FROM exp_pre_email_addresses
[tab]WHERE foo != 'oof'
[tab]AND baz != 'zab'
[tab]ORDER BY foobaz
[tab]LIMIT 5, 100");
```

### 1.11 单、双引号

除非你需要解析变量，否则请始终使用单引号。

```
// 不好
"My String"; // 降低 php 解析效率
// 好
'My String'; 
```

双引号仅用在如下场景中：

* 没有需要解析的变量，但字符串中存在需要转义的内容（如单引号）。
* 存在需要解析的变量。对于复杂的字符串，我们还推荐使用大括号对变量进行包裹，以防止变量最长贪婪匹配（greedy token parsing）。

```
// 正确，但不够好：
'SELECT foo FROM bar WHERE baz = \'bag\'' // 转义单引号''时这样写比较难看，可以使用双引号
// 正确，且可读性高：
"SELECT foo FROM bar WHERE baz = 'bag'"
```

```
$foo = 'Saturn';
$kind = 'super';

// 错误：
"$foo is a $kindman." // $kind 存在贪婪匹配

// 正确
"$foo is a ${kind}man."; // "Saturn is a superman."
```

## 2 大括号放置

始终使用 [Allman 缩进](http://en.wikipedia.org/wiki/Indent_style#Allman_style)风格进行大括号的放置与代码缩进：

除了类（Class）声明之外，括号总是独占一行，且需缩进至当前控制语句同级，括号内语句需缩进至下一级别。

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

## 3 逗号与空格放置

### 3.1 逗号放置

函数中用逗号来分隔参数，所有的参数与前面的逗号之间要增加一个空格(第一个参数除外)。

```
public function connect($host, $port, $db, $user, $password, $charset = NULL)
```

### 3.2 方括号及圆括号内的空格

不要在方括号 `[]` 和圆括号 `()` 内增加任何空格。

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

例外情况：在结构控制语句后通常需要跟一个空格，以更好将控制体与普通函数区分开来。

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