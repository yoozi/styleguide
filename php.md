# 游子 PHP 编码规范

## 0 声明

除特别声明，游子旗下所有解决方案、研发产品凡涉及 PHP 程序的部分，均需严格遵守本编码规范。已存代码、但不符合本规范的部分，需逐步改善形成统一代码风格，以保证代码简洁明了、容易阅读。本规范与 [CodeIgniter 框架编码规范](http://codeigniter.org.cn/user_guide/general/styleguide.html)有许多相似之处，但在部分地方会有所不同。

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

对于所有需要通过比较、或判断返回值的场景，请按需使用 `===` 和 `!==` 这样的操作符。

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

请不要使用短标签：即请不要简写 PHP 的开启标签、闭合标签。

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

### 1.10 去除每行语句后面的空格

请通过各编辑器的插件去除每行代码后面的空格。

### 1.11 长语句请换行

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

* 字符串中没有需要解析的变量，但字符串中存在需要转义的内容（如单引号）。
* 字符串中存在需要解析的变量。对于复杂的字符串，我们还推荐使用大括号对变量进行包裹，以防止变量最长贪婪解析（greedy token parsing）。

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

### 3.3 操作符空格的使用

除了如 3.1 参数之间要使用空格外，所有操作符之间都要使用空格，包括字符连接符(.)。

```
$host . ':' . $port
```

## 4 命名规则

### 4.1 文件命名

几乎所有应用最终都部署在 Linux 内核的服务器上，而由于 Unix/Linux 操作系统文件的命名对大小写敏感，所以请特别注意文件的大小写问题。对于内核使用 CodeIgniter 的应用，文件的命名基本遵循 CodeIgniter 框架对不同类型文件制定的命名规则，简单来说：

* [Controllers](http://codeigniter.com/user_guide/general/controllers.html)：控制器文件名称请小写，类名首字母需大写。
* [Views](http://codeigniter.com/user_guide/general/views.html)：视图文件名称需小写。
* [Models](http://codeigniter.com/user_guide/general/models.html)：模型文件名称需小写、类声明首字母需大写且与文件名匹配。
* [Helpers](http://codeigniter.com/user_guide/general/helpers.html)：助手文件名称请小写，且增加 `_helper` 后缀。
* [Libraries](http://codeigniter.com/user_guide/general/creating_libraries.html)：自定义类库文件首字母需大写、类声明首字母需大写且与文件名匹配。

CodeIgniter 其他文件的命名规则，请通过 CodeIgniter [框架手册](http://codeigniter.com/user_guide/)了解详情。

### 4.2 类和方法（函数）的命名

* 当新引入的类主要用于拓展 CodeIgniter 内核，那么此类需要遵循 CodeIgniter [框架手册](http://codeigniter.com/user_guide/)中对于不同类型类文件的命名规则。
* 当新引入的类是组件型的、完整的第三方工具包，比如将 [Zend Framework](http://framework.zend.com/) 以 `third_party` 方式引入 CodeIgniter，此时仅需遵守引入的第三方工具包自身的命名规则即可。

对于 CodeIgniter 中的类：类名的首字母应该大写。如果名称由多个词组成，词之间要用下划线分隔，不要使用骆驼命名法。类中所有其他方法的名称应该完全小写并且名称能明确指明这个函数的用途，最好用动词开头。尽量避免过长和冗余的名称。

```
// 不当的:
class superclass
class SuperClass

// 适当的:
class Super_class
```

```
// 不当的:
function fileproperties()  // 方法名没有清晰的描述以及下划线分割单词
function fileProperties()  // 方法名没有清晰的描述以及使用了驼峰法命名
function getfileproperties()  // 还可以!但是忘记了下划线分割单词
function getFileProperties()  // 使用了驼峰法命名
function get_the_file_properties_from_the_file() // 方法名太冗长

// 适当的:
function get_file_properties() // 清晰的方法名描述，下划线分割单词，全部使用小写字母
```

### 4.3 变量命名

变量的命名规则与 4.2 中方法的命名规则类似：变量名应只包含小写字母、用下划线分隔、并能适当地指明变量的用途和内容。那些短的、无意义的变量名应该只作为迭代器用在 for() 循环里。

```
// 不当的:
$j = 'foo';  // 单字符变量应该只作为 for() 的循环变量使用
$Str   // 使用了大写字母
$bufferedText  // 使用了驼峰命名，而且变量名应该更短，并有清晰的语法含义
$groupid  // 多个词组，应该使用下划线分割
$name_of_last_city_used // 太长了

// 适当的:
for ($j = 0; $j < 10; $j++)
$str
$buffer
$group_id
$last_city
```

### 4.4 常量命名

常量命名除需全部大写外，其他的规则都和变量相同。在适当的时候，始终使用 CodeIgniter 定义好的常量，例如`LASH`, `LD`, `RD`, `PATH_CACHE`等等.

```
// 不当的:
myConstant // 未使用下划线分割单词，未全部使用大写字母
N  // 不能使用单个字母作为常量
S_C_VER  // 常量名没有清晰的含义
$str = str_replace('{foo}', 'bar', $str); // 应使用 LD 和 RD 两个预定义常量

// 恰当的:
MY_CONSTANT
NEWLINE
SUPER_CLASS_VERSION
$str = str_replace(LD.'foo'.RD, 'bar', $str);
```

一般情况下请勿自定义常量，它会增加代码的维护成本。如果一定要增加常量，请尽量放置在如下两处：

* 入口文件 index.php: 用来放置应用程序级别的常量，比如 app 路径。
* 配置文件 config/constants.php：其他常用常量，比如文件读写状态标识。

## 5 注释

所有注释（特别是 5.1 节、5.2 节）需遵循“[文档块(DocBlock)](http://manual.phpdoc.org/HTMLSmartyConverter/HandS/phpDocumentor/tutorial_phpDocumentor.howto.pkg.html#basics.docblock)”，从而通过文档生成工具 PHPDocumentor 自动生成 API 文档。 

### 5.1 文件注释

每个文件头部均需加入如下代码片段，包括：版权声明、版本编号规则、团队信息等基本信息。

```
<?php (defined('BASEPATH')) OR exit('No direct script access allowed');
/**
 *	项目标题
 *
 *  项目简短描述
 *
 *	@package	Yoozi
 *	@author		Yoozi Dev Team
 *	@copyright	Copyright (c) 2010, Yoozi.org
 *	@since		Version 1.0.0
 *	@filesource
 */
```
此代码片段应由每个项目的研发总监在项目开始时指定，其他开发人员需严格遵循。

### 5.2 类、方法（函数）注释

每个类、方法（函数）的头部需要加入如下代码片段，用来描述类、方法的功能和类别等。

```
/**
 *	类的一句话描述
 *
 *  类的简短描述、说明、注意事项等
 *
 *	@package	Yoozi
 *	@subpackage Classad
 *	@category	Controller
 *	@author		Saturn <yangg.hu@yoozi.org>
 *	@link
 */
 ```
 ```
 /**
 * Encodes string for use in XML
 *
 * @todo security check
 * @access public
 * @param string
 * @return string
 */
function xml_encode($str)
 ```
### 5.3 行间注释

通常我们需要对复杂逻辑的代码编写行间注释，以达到提醒其他开发人员、增加代码可读性的作用。

行注释需要注意如下几点：

1. 使用 `//` 双左斜线开启每个行注释，且第一个字符与斜线间保持一个空格的距离。
2. 每行注释不要超过 70 个字符，超过部分请折多行。
3. 使用行注释时，在大的注释块和代码间留一个空行。

```
// break up the string by newlines
$parts = explode("\n", $str);

// A longer comment that needs to give greater detail on what is
// occurring and why can use multiple single-line comments.  Try to
// keep the width reasonable, around 70 characters is the easiest to
// read.  Don't hesitate to link to permanent external resources
// that may provide greater detail:
//
// http://example.com/information_about_something/in_particular/

$parts = $this->foo($parts);
```

### 5.4 方法、函数的注释间隔

不同方法、函数间请使用如下 `注释间隔` 区分开，以此增加代码在阅读上的结构感。此间隔的缩进取决于同级方法、函数的缩进距离。同时，本间隔上下需要分别留一个空行。

```
// ------------------------------------------------------------------------
```

```
 /**
 * 设置经度
 *
 * @access protected
 * @return void
 */
protected function set_longitude()
{
	$this->data['longitude'] = $this->post['longitude'];
}

// ------------------------------------------------------------------------

 /**
 * 设置经度
 *
 * @access protected
 * @return void
 */
protected function set_latitude()
{
	$this->data['latitude'] = $this->post['latitude'];
}
```

## 6 代码布局

### 6.1 类内部方法排序

类方法排序遵循：public、protected、private的顺序。

```
__construct
__destruct
public
protected
private
```
### 6.2 类属性声明的排序

```
public
protected
private
```

### 6.3 行间空行的使用

行间空行的使用是一门艺术，是程序员对代码节奏的控制。说它是艺术，是因为它并没有很好的规律可言。优秀的程序员能够比较好的控制好空行的使用，从而提高代码的可读性。

我的经验：

1. 将逻辑上联系不太紧密的代码块，通过空行分隔开。
2. 不要使用每行一个空行的编码风格。
3. 具体操作请各位自己把握。
4. 每个程序员写满 50 万行代码之后，艺术风格开始显现。:)

下面举个简单的例子：

```
/**
 * Render the final page
 *
 * @access public
 * @return void
 */
public function render()
{
	// Call hook: pre render
	$this->call_pre_render_hook();

	// Iterator all the possible elements handlers
	$handlers = array_keys($this->page_elements);
	foreach($handlers as $handler)
	{
		$this->{'set_' . $handler}();
	}

	// 信息被删除
	if($this->post['is_deleted'])
	{
		// 用户删除
		if($post['deleted_by'] == 'user')
		{
			$this->template->title(lang('posts.is_deleted'))
				->set_metadata('description', lang('txt_post_deleted'), 'meta')
				->build('posts/deleted');
			return;
		}

		// 信息已被归档
		show_404();
	}

	// 信息违反规则
	if($this->post['is_abused'])
	{
		$this->template->title(lang('posts.is_abused'))
			->set_metadata('description', lang('txt_post_deleted'), 'meta')
			->build('posts/deleted');
		return;
	}

	// 信息需要人工审核
	if($this->post['is_cursed'])
	{
		$this->template->title(lang('posts.is_abused'))
			->build('posts/cursed');
		return;
	}

	// Call hook: before render
	$this->call_post_render_hook();

	// Build and show the final page...
	CI()->template
		->set_partial('inline_js', 'posts/posts_js')
		->inject_partial('active_category', $this->post['parent_category']['cate_id'])
		->set_metadata('og:title', $this->data['title'], 'property')
		->set_metadata('og:type', 'website', 'property')
		->set_metadata('og:url', $this->data['post_url'], 'property')
		->build('posts/posts', $this->data);
}
```

## 7 作者

此处仅列出本文的主要撰写者：

* Saturn：<yangg.hu@yoozi.cn>

## 8 致谢

感谢 [Wordpress](http://codex.wordpress.org/WordPress_Coding_Standards)、[CodeIgniter](http://codeigniter.org.cn/user_guide/general/styleguide.html)、[Typecho](http://docs.typecho.org/phpcoding) 三个优秀开源项目对本文档的贡献，向他们的作者致敬和感谢。

## 9 参与互动

通过如下两种方式之一来参与互动：

* 请直接 fork 本项目，然后 pull request 即可。
* 直接提交[改进建议](https://github.com/yoozi/styleguide/issues/new)。