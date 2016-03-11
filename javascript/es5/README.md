# JavaScript (ES5) 编码规范



## 1 数组

  - 向数组增加元素时使用 Array#push 来替代直接赋值。

  - 当你需要拷贝数组时，使用 Array#slice。[jsPerf](http://jsperf.com/converting-arguments-to-an-array/7)

    ```javascript
    var len = items.length;
    var itemsCopy = [];
    var i;

    // bad
    for (i = 0; i < len; i++) {
      itemsCopy[i] = items[i];
    }

    // good
    itemsCopy = items.slice();
    ```


## 2 字符串

  - 使用单引号 `''` 包裹字符串。

  - 超过 80 个字符的字符串应该使用连接符 `+` 写成多行。
  - 注：若过度使用，通过连接符连接的长字符串可能会影响性能。[jsPerf](http://jsperf.com/ya-string-concat) & [讨论](https://github.com/airbnb/javascript/issues/40).

  - 程序化生成的字符串使用 Array#join 连接而不是使用连接符。尤其是 IE 下：[jsPerf](http://jsperf.com/string-vs-array-concat/2).


## 3 函数

  - 永远不要在一个非函数代码块（if、while 等）中声明一个函数，把那个函数赋给一个变量。浏览器允许你这么做，但它们的解析表现不一致。

  - **注：** ECMA-262 把 `块` 定义为一组语句。函数声明不是语句。[阅读对 ECMA-262 这个问题的说明](http://www.ecma-international.org/publications/files/ECMA-ST/Ecma-262.pdf#page=97)。

    ```javascript
    // bad
    if (currentUser) {
      function test() {
        console.log('Nope.');
      }
    }

    // good
    var test;
    if (currentUser) {
      test = function test() {
        console.log('Yup.');
      };
    }
    ```


## 4 变量

  - 使用 `var` 声明每一个变量。
    这样做的好处是增加新变量将变的更加容易，而且你永远不用再担心调换错 `;` 跟 `,`。

    ```javascript
    // bad
    var items = getItems(),
        goSportsTeam = true,
        dragonball = 'z';

    // bad
    // （跟上面的代码比较一下，看看哪里错了）
    var items = getItems(),
        goSportsTeam = true;
        dragonball = 'z';

    // good
    var items = getItems();
    var goSportsTeam = true;
    var dragonball = 'z';
    ```

  - 最后再声明未赋值的变量。当你需要引用前面的变量赋值时这将变的很有用。

  - 在作用域顶部声明变量。这将帮你避免变量声明提升相关的问题。


## 5 构造函数

  - 给对象原型分配方法，而不是使用一个新对象覆盖原型。覆盖原型将导致继承出现问题：重设原型将覆盖原有原型！

  - 方法可以返回 `this` 来实现方法链式使用。


## 6 模块

  - 模块应该以 `!` 开始。这样确保了当一个不好的模块忘记包含最后的分号时，在合并代码到生产环境后不会产生错误。[详细说明](https://github.com/airbnb/javascript/issues/44#issuecomment-13063933)

  - 文件应该以驼峰式命名，并放在同名的文件夹里，且与导出的名字一致。

  - 增加一个名为 `noConflict()` 的方法来设置导出的模块为前一个版本并返回它。

  - 永远在模块顶部声明 `'use strict';`。

    ```javascript
    // fancyInput/fancyInput.js

    !function(global) {
      'use strict';

      var previousFancyInput = global.FancyInput;

      function FancyInput(options) {
        this.options = options || {};
      }

      FancyInput.noConflict = function noConflict() {
        global.FancyInput = previousFancyInput;
        return FancyInput;
      };

      global.FancyInput = FancyInput;
    }(this);
    ```

## 7 jQuery

  - 使用 `$` 作为存储 jQuery 对象的变量名前缀。

    ```javascript
    // bad
    var sidebar = $('.sidebar');

    // good
    var $sidebar = $('.sidebar');
    ```

  - 缓存 jQuery 查询。

    ```javascript
    // bad
    function setSidebar() {
      $('.sidebar').hide();

      // ...stuff...

      $('.sidebar').css({
        'background-color': 'pink'
      });
    }

    // good
    function setSidebar() {
      var $sidebar = $('.sidebar');
      $sidebar.hide();

      // ...stuff...

      $sidebar.css({
        'background-color': 'pink'
      });
    }
    ```
    

## 8 参考链接
  - [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript/blob/master/es5/README.md)
  - [Airbnb Javascript Style 中文翻译](https://github.com/sivan/javascript-style-guide/blob/master/es5/README.md)

