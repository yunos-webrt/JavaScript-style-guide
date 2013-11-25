JavaScript-style-guide
======================

# JavaScript规范

## <a name="TOC">内容列表</a>
1. [基本格式化](#basic)
2. [注释](#comments)
3. [语句和表达式](#statement)
4. [变量、函数和运算符](#function)


## <a name="basic">基本格式化</a>
- **缩进**
	+ 所有的缩进都使用四空格。（可以对编辑器设置为tab即为四空格）
	
- **结尾**
	+ 必须使用分号结尾。
	
- **换行**
 	+ 行的长度不超过80字符
 	+ 在运算符后换行，换行后两个缩进。
 	
- **空行**
	+ 在方法之间。
	+ 在方法的局部变量和第一条语句之间。
	+ 在方法内不同的逻辑片段内，提高可读性。
- **命名**
	+ 驼峰命名，首字母小写，后续每个单词首字母大写。
	+ 变量名使用名词，函数名使用动词
	
        ```javascript
        // bad
        var getCount = 10;
    
        function theName() {
        }

        // good
        var count = 10;
        function getName() {
        }
        ```
    
    + 常量全部大写。
    + 构造函数遵循大驼峰命名规范，首字母大写。
    + 命名私有属性时前面加个下划线 `_`

        ```javascript
        // bad
        this.__firstName__ = 'Panda';
        this.firstName_ = 'Panda';

        // good
        this._firstName = 'Panda';
        ```
    + 当保存对 `this` 的引用时使用 `_this`.

        ```javascript
        // bad
        function() {
        var self = this;
          return function() {
            console.log(self);
            };
        }

        // bad
        function() {
            var that = this;
            return function() {
            console.log(that);
            };
        }

        // good
        function() {
        var _this = this;
        return function() {
            console.log(_this);
            };
        }
        ```
    
- **直接量**
 
	+ 字符串使用双引号。多行字符串使用“+”号连接。
	
	 ```javascript
	// bad
	var longString = "Here's the story, of a man \
			named Brady";
	//good
	var longString = "Here's the story, of a man " + 
			"named Brady";
	```
	
	+ null，不要和undefined混淆。将null理解为一个对象的占位符。
	
		+ 用来初始化变量，变量可能赋值为一个对象。
		+ 用来和一个已经初始化的变量比较。
		+ 当函数的参数期望是对象时，作为参数传入。
		+ 当函数的返回值期望是对象时，作为返回值传出。
		
		+ 不要使用null来和为初始化的变量比较
		+ 不要使用null来检查未初始化的变量。
		
	 ```javascript
	// bad
	var person;
	if(person != null) {
	}
	//bad 
	function doSomething(arg1, arg2, arg3) {
			if(arg4 != null) {
			}
	}
	```
	
	+ 对象直接量
	
		+ 使用直接量创建对象。
		
			```javascript
	
			// bad
			var item = new Object();

			// good
			var item = {};
			```
		
		+ 不要使用保留字 [reserved words](https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Reserved_Words) 作为键

		    ```javascript
		    // bad
		   var superman = {
		        class: "superhero",
		        default: { clark: "kent" },
		        private: true
		    };
		    // good
		    var superman = {
		        klass: "superhero",
		        defaults: { clark: "kent" },
		        hidden: true
		    };
		    ```
    
 
	+ 数组直接量
    
   		 - 使用字面值创建数组

		  ```javascript
		    // bad
		    var items = new Array();
		    // good
	            var items = [];
    		  ```

  	 	- 如果你不知道数组的长度，使用push

		 ```javascript
		  var someStack = [];
		  // bad
		  someStack[someStack.length] = "abracadabra";
		  // good
		  someStack.push("abracadabra");
		  ```

 		- 当你需要拷贝数组时使用slice. [jsPerf](http://jsperf.com/converting-arguments-to-an-array/7)

		  ```javascript
		  var len = items.length,
		    itemsCopy = [],
		    i;
		   // bad
		  for (i = 0; i < len; i++) {
		    itemsCopy[i] = items[i];
    	          }
		  // good
		    itemsCopy = items.slice();
		  ```

  		- 使用slice将类数组的对象转成数组.

		 ```javascript
		 function trigger() {
		   var args = Array.prototype.slice.call(arguments);
		   ...
		 }
		 ```

	 **[[⬆]](#TOC)**
    
## <a name="comments">注释</a>
  - 对于难以理解的代码必须加上注释。对于可能被误认为错误的代码必须加上注释。

  - 使用 `/** ... */` 进行多行注释，包括描述，指定类型以及参数值和返回值

    ```javascript
    // bad
    // make() returns a new element
    // based on the passed in tag name
    //
    // @param <String> tag
    // @return <Element> element
    function make(tag) {

      // ...stuff...

      return element;
    }

    // good
    /**
     * make() returns a new element
     * based on the passed in tag name
     *
     * @param <String> tag
     * @return <Element> element
     */
    function make(tag) {

      // ...stuff...

      return element;
    }
    ```

  - 使用 `//` 进行单行注释，在评论对象的上面进行单行注释，注释前放一个空行.

    ```javascript
    // bad
    var active = true;  // is current tab

    // good
    // is current tab
    var active = true;

    // bad
    function getType() {
      console.log("fetching type...");
      // set the default type to "no type"
      var type = this._type || "no type";

      return type;
    }

    // good
    function getType() {
      console.log("fetching type...");

      // set the default type to "no type"
      var type = this._type || "no type";

      return type;
    }
    ```

  - 如果你有一个问题需要重新来看一下或如果你建议一个需要被实现的解决方法的话需要在你的注释前面加上 `FIXME` 或 `TODO` 帮助其他人迅速理解

    ```javascript
    function Calculator() {

      // FIXME: shouldn't use a global here
      total = 0;

      return this;
    }
    ```

    ```javascript
    function Calculator() {

      // TODO: total should be configurable by an options param
      this.total = 0;

      return this;
    }
  ```

    **[[⬆]](#TOC)**
## <a name="statement">语句和表达式</a>
  - 所有的块语句都需要使用花括号，包括：
  	+ if
  	+ for
  	+ while
  	+ do...while...
  	+ try..catch...
  - 花括号的对齐方式
  
    ```javascript
	if (condition) {
	    doSomething();
	} else {
	    doSomethingElse()	;
	}
    ```	

  - 在左圆括号之前和右圆括号之后各添加一个空格。
  - switch 语句,每条case相对于switch关键字缩进一层，每个case语句之间有一个空行。
  ```javascript
  switch(condition) {
	case: "firset":
		//code
		break;

	case: "second":
		//code
		break;
	
	default:
		//code
  }
	```
  - 在做长方法链时使用缩进.

    ```javascript
    // bad
    $("#items").find(".selected").highlight().end().find(".open").updateCount();

    // good
    $("#items")
      .find(".selected")
        .highlight()
        .end()
      .find(".open")
        .updateCount();

    // bad
    var leds = stage.selectAll(".led").data(data).enter().append("svg:svg").class("led", true)
        .attr("width",  (radius + margin) * 2).append("svg:g")
        .attr("transform", "translate(" + (radius + margin) + "," + (radius + margin) + ")")
        .call(tron.led);

    // good
    var leds = stage.selectAll(".led")
        .data(data)
      .enter().append("svg:svg")
        .class("led", true)
        .attr("width",  (radius + margin) * 2)
      .append("svg:g")
        .attr("transform", "translate(" + (radius + margin) + "," + (radius + margin) + ")")
        .call(tron.led);
    ```

  - 不要将逗号放前面

    ```javascript
    // bad
    var once
      , upon
      , aTime;

    // good
    var once,
        upon,
        aTime;

    // bad
    var hero = {
        firstName: "Bob"
      , lastName: "Parr"
      , heroName: "Mr. Incredible"
      , superPower: "strength"
    };

    // good
    var hero = {
      firstName: "Bob",
      lastName: "Parr",
      heroName: "Mr. Incredible",
      superPower: "strength"
    };
    ```

  - 不要加多余的逗号，这可能会在IE下引起错误，同时如果多一个逗号某些ES3的实现会计算多数组的长度。

    ```javascript
    // bad
    var hero = {
      firstName: "Kevin",
      lastName: "Flynn",
    };

    var heroes = [
      "Batman",
      "Superman",
    ];

    // good
    var hero = {
      firstName: "Kevin",
      lastName: "Flynn"
    };

    var heroes = [
      "Batman",
      "Superman"
    ];
    ```
      **[[⬆]](#TOC)**
## <a name="function">变量、函数和运算符</a>

- 变量

  - 总是使用 `var` 来声明变量，如果不这么做将导致产生全局变量，我们要避免污染全局命名空间。

    ```javascript
    // bad
    superPower = new SuperPower();

    // good
    var superPower = new SuperPower();
    ```

  - 使用一个 `var` 以及新行声明多个变量，缩进4个空格。

    ```javascript
    // bad
    var items = getItems();
    var goSportsTeam = true;
    var dragonball = "z";

    // good
    var items = getItems(),
        goSportsTeam = true,
        dragonball = "z";
    ```

  - 最后再声明未赋值的变量，当以后你想给一个依赖之前已赋值变量的变量时很有用。

    ```javascript
    // bad
    var i, len, dragonball,
        items = getItems(),
        goSportsTeam = true;

    // bad
    var i, items = getItems(),
        dragonball,
        goSportsTeam = true,
        len;

    // good
    var items = getItems(),
        goSportsTeam = true,
        dragonball,
        length,
        i;
    ```

  - 在作用域顶部声明变量，避免变量声明和赋值引起的相关问题。

    ```javascript
    // bad
    function() {
      test();
      console.log("doing stuff..");

      //..other stuff..

      var name = getName();

      if (name === "test") {
        return false;
      }

      return name;
    }

    // good
    function() {
      var name = getName();

      test();
      console.log("doing stuff..");

      //..other stuff..

      if (name === "test") {
        return false;
      }

      return name;
    }

    // bad
    function() {
      var name = getName();

      if (!arguments.length) {
        return false;
      }

      return true;
    }

    // good
    function() {
      if (!arguments.length) {
        return false;
      }

      var name = getName();

      return true;
    }
    ```
- 函数

 - 函数表达式:

    ```javascript
    // 匿名函数表达式
    var anonymous = function() {
      return true;
    };

    // 有名函数表达式
    var named = function named() {
      return true;
    };

    // 立即调用函数表达式
    (function() {
      console.log("Welcome to the Internet. Please follow me.");
    })();
    ```

  - 绝对不要在一个非函数块里声明一个函数，把那个函数赋给一个变量。浏览器允许你这么做，但是它们解析不同。
  - **注:** ECMA-262定义把`块`定义为一组语句，函数声明不是一个语句。[阅读ECMA-262对这个问题的说明](http://www.ecma-international.org/publications/files/ECMA-ST/Ecma-262.pdf#page=97).

    ```javascript
    // bad
    if (currentUser) {
      function test() {
        console.log("Nope.");
      }
    }

    // good
    if (currentUser) {
      var test = function test() {
        console.log("Yup.");
      };
    }
    ```

  - 绝对不要把参数命名为 `arguments`, 这将会逾越函数作用域内传过来的 `arguments` 对象.

    ```javascript
    // bad
    function nope(name, options, arguments) {
      // ...stuff...
    }

    // good
    function yup(name, options, args) {
      // ...stuff...
    }
    ```
- 属性
  - 当使用变量访问属性时使用中括号.

    ```javascript
    var luke = {
      jedi: true,
      age: 28
    };

    function getProp(prop) {
      return luke[prop];
    }

    var isJedi = getProp("jedi");
    ```
- 符号
 - 使用 `===` 和 `!==` ，而不是 `==` 和 `!=`.
 - 条件表达式的强制类型转换遵循以下规则：

    + **对象** 被计算为 **true**
    + **Undefined** 被计算为 **false**
    + **Null** 被计算为 **false**
    + **布尔值** 被计算为 **布尔的值**
    + **数字** 如果是 **+0, -0, or NaN** 被计算为 **false** , 否则为 **true**
    + **字符串** 如果是空字符串 `""` 则被计算为 **false**, 否则为 **true**

    ```javascript
    if ([0]) {
      // true
      // An array is an object, objects evaluate to true
    }
    ```

  - 使用快捷方式.

    ```javascript
    // bad
    if (name !== "") {
      // ...stuff...
    }

    // good
    if (name) {
      // ...stuff...
    }

    // bad
    if (collection.length > 0) {
      // ...stuff...
    }

    // good
    if (collection.length) {
      // ...stuff...
    }
    ```
    
    **[[⬆]](#TOC)**
