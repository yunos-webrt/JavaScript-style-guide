JavaScript-style-guide
======================

# JavaScript规范

## <a name='TOC'>内容列表</a>
1. [基本格式化](#basic)


## <a name='basic'>基本格式化</a>
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
		      class: 'superhero',
		     default: { clark: 'kent' },
		     private: true
		    };
		    // good
		    var superman = {
		     klass: 'superhero',
		     defaults: { clark: 'kent' },
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
		 someStack[someStack.length] = 'abracadabra';
		 // good
		 someStack.push('abracadabra');
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
    
## <a name='comments'>注释</a>

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
      console.log('fetching type...');
      // set the default type to 'no type'
      var type = this._type || 'no type';

      return type;
    }

    // good
    function getType() {
      console.log('fetching type...');

      // set the default type to 'no type'
      var type = this._type || 'no type';

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
	


