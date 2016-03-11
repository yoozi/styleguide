# JavaScript 编码规范

> [ES 5 细节规范](es5/README.md)

> [ES 6 细节规范](es6/README.md)



## 1 代码风格


### 1.1 空白

- 使用 2 个空格作为缩进

- 在花括号前放一个空格

- 在控制语句（if、while 等）的小括号前放一个空格。在函数调用及声明中，不在函数的参数列表前加空格。

- 如果通过 `if` 和 `else` 使用多行代码块，把 `else` 放在 `if` 代码块关闭括号的同一行。

- 使用大括号包裹所有的多行代码块。

- 使用空格把运算符隔开。

- 在文件末尾插入一个空行。

- 在块末和新语句前插入空行。


### 1.2 逗号

- 不使用行首逗号

- ES5 额外的行末逗号：**不需要**。这样做会在 IE6/7 和 IE9 怪异模式下引起问题。同样，多余的逗号在某些 ES3 的实现里会增加数组的长度。在 ES5 中已经澄清了 ([source](http://es5.github.io/#D))：

  > Edition 5 clarifies the fact that a trailing comma at the end of an ArrayInitialiser does not add to the length of the array. This is not a semantic change from Edition 3 but some implementations may have previously misinterpreted this.

	```javascript
	// bad
	var hero = {
	 firstName: 'Kevin',
	 lastName: 'Flynn',
	};
	
	var heroes = [
	 'Batman',
	 'Superman',
	];
	
	// good
	var hero = {
	 firstName: 'Kevin',
	 lastName: 'Flynn'
	};
	
	var heroes = [
	 'Batman',
	 'Superman'
	];
	```

- ES6 增加结尾的逗号
> 为什么? 这会让 git diffs 更干净。另外，像 babel 这样的转译器会移除结尾多余的逗号，也就是说你不必担心老旧浏览器的[尾逗号问题](es5/README.md#commas)。

  ```javascript
  // bad - git diff without trailing comma
  const hero = {
       firstName: 'Florence',
  -    lastName: 'Nightingale'
  +    lastName: 'Nightingale',
  +    inventorOf: ['coxcomb graph', 'modern nursing']
  }

  // good - git diff with trailing comma
  const hero = {
       firstName: 'Florence',
       lastName: 'Nightingale',
  +    inventorOf: ['coxcomb chart', 'modern nursing'],
  }

  // bad
  const hero = {
    firstName: 'Dana',
    lastName: 'Scully'
  };

  const heroes = [
    'Batman',
    'Superman'
  ];

  // good
  const hero = {
    firstName: 'Dana',
    lastName: 'Scully',
  };

  const heroes = [
    'Batman',
    'Superman',
  ];
  ```


### 1.3 分号

- 使用分号


### 1.4 注释

- 使用 `/** ... */` 作为多行注释。包含描述、指定所有参数和返回值的类型和值。

	```javascript
	/**
	 * make() returns a new element
	 * based on the passed in tag name
	 *
	 * @param {String} tag
	 * @return {Element} element
	 */
	function make(tag) {
	
	  // ...stuff...
	
	  return element;
	}
	```

- 使用 `//` 作为单行注释。在评论对象上面另起一行使用单行注释。在注释前插入空行。

- 给注释增加 `FIXME` 或 `TODO` 的前缀可以帮助其他开发者快速了解这是一个需要复查的问题，或是给需要实现的功能提供一个解决方式。这将有别于常见的注释，因为它们是可操作的。使用 `FIXME -- need to figure this out` 或者 `TODO -- need to implement`。

- 使用 `// FIXME:` 标注问题。

	```javascript
	function Calculator() {
	
	  // FIXME: shouldn't use a global here
	  total = 0;
	
	  return this;
	}
	```

- 使用 `// TODO:` 标注问题的解决方式。

	```javascript
	function Calculator() {
	
	  // TODO: total should be configurable by an options param
	  this.total = 0;
	
	  return this;
	}
	```



## 2 命名规范


### 2.1 函数、对象命名

- 避免单字母命名。命名应具备描述性。

- 使用驼峰式命名对象、函数和实例。

	```javascript
	var thisIsMyObject = {};
	function thisIsMyFunction() {}
	```
	
- 使用帕斯卡式命名构造函数或类。
	
	```javascript
	function User(options) {
	  this.name = options.name;
	}
	
	var good = new User({
	  name: 'yup'
	});
	```


### 2.2 属性、方法命名

- 使用下划线 `_` 开头命名私有属性。

- 不要使用保留字作为键名，它们在 IE8 下不工作。更多信息。

- 如果你需要存取函数时使用 `getVal()` 和 `setVal('value')`

- 如果属性是布尔值，使用 `isVal()` 或 `hasVal()`。

- 使用同义词替换需要使用的保留字。

	```javascript
	// bad
	var superman = {
	  class: 'alien'
	};
	
	// bad
	var superman = {
	  klass: 'alien'
	};
	
	// good
	var superman = {
	  type: 'alien'
	};
	```


### 2.3 文件命名

- 如果你的文件导出一个类，你的文件名应该与类名完全相同。



## 3 测试

 - 你应当编写测试代码



## 4 资源


**工具** 

- Compiler
	+ [Babel](https://babeljs.io/)
  
- Code Style Linters
	+ [ESlint](http://eslint.org/) - [Airbnb Style .eslintrc](https://github.com/airbnb/javascript/blob/master/linters/.eslintrc)  
	  
	+ [JSHint](http://www.jshint.com/) - [Airbnb Style .jshintrc](https://github.com/airbnb/javascript/blob/master/linters/jshintrc)

	+ [JSCS](https://github.com/jscs-dev/node-jscs) - [Airbnb Style Preset](https://github.com/jscs-dev/node-jscs/blob/master/presets/airbnb.json)

	+ [EditorConfig](http://editorconfig.org/) 
		
