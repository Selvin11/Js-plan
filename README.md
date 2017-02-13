# Js-plan
a new understanding about javascript

1. [Js基本组成](#1)
2. [数据类型](#2)
3. [数组](#3)
4. [字符串](#4)
5. [函数](#5)
6. [对象](#6)
7. [Symbol](#7)
8. [Set and Map](#8)
9. [浏览器环境](#9)
10. [栈与堆](#10)
<h2 id="1">1 . Js 基本组成</h2>

* 基础语法 —— 语法、数据类型、数据类型转换、错误处理机制等
* 标准库 ——　各类广义对象及其携带的属性、方法
* DOM API
* 浏览器 API
* WEB API

<h2 id="2">2 . Js 数据类型 —— 字符串、数值、布尔值、undefined、null、对象、数组、函数、Symbol</h2>

* 原始类型 —— 字符串、数值、布尔值
* 合成类型 ——　对象 （JavaScript的所有数据，都可以视为广义的对象）
    
    对象分为　——　狭义的对象（仅指Object）、数组、函数
    
* 运算符
    
    * '+'  : 一般的加法运算以及重载（由于参数不同，而改变自身行为的现象，叫做“重载”）
        ```javascript
          '1' + {foo: 'bar'} // "1[object Object]"
          '1' + 1 // "11"
          '1' + true // "1true"
          '1' + [1] // "11"
        ```
    * 其余运算符（-、*、/、%等）均将符号右边转换为数值类型进行运算
      
* this
    
    this返回属性或方法“当前”所在的对象。

* 单线程
    
    一个程序运行之后便称为“进程”，进程中包含程序需要执行的各项任务，形成了任务队列，
    一般采用多线程来处理多项任务，线程中执行任务分为同步和异步。
    * 同步 ： 下一个任务等待上一个任务执行完成之后再执行
    * 异步 ： 任务提交请求之后，通过回调函数处理回应，从而继续执行任务，任务之间没有等待

<h2 id="3">3 . 数组</h2>

* 数组： Js中的数组，是按照顺序排列的一组值，索引为0开始的数字，索引值可以为任意数据类型
* 数组的方法：
    * valueOf() 
    
        ```
        [1,2].valueOf() // [1,2] 返回本身
        ```
    * toString()
    
        ```
        [1, 2, 3, [4, 5, 6]].toString() // "1,2,3,4,5,6" 返回字符串
        ```
    * push()  从数组末端添加一个或多个元素，返回值为添加后的数组长度
    * unshift()  从数组第一个个位置添加元素，返回值为添加后的数组长度
    * pop()  删除数组最后一个元素，返回值为删除的元素
    * shift()  删除数组第一个元素，返回值为删除的元素
    * join() 以参数作为分隔符，将数组成员组成一个字符串返回，原数组不变

      ```
      [1, 2, 3].join() // "1,2,3" 默认为逗号
      ```
    * concat() 数组合并，原数组不变

      ```
      [1, 2, 3].concat([4,5]) // [1,2,3,4,5] 
      [1, 2, 3].concat(4,5) // [1,2,3,4,5] 
      //如果不提供参数，concat方法返回当前数组的一个浅拷贝。
      //所谓“浅拷贝”，指的是如果数组成员包括复合类型的值（比如对象），则新数组拷贝的是该值的引用
      var obj = { a:1 };
      var oldArray = [obj];

      var newArray = oldArray.concat();

      obj.a = 2;
      newArray[0].a // 2
      ```
    * reverse() 颠倒数组中的元素顺序，返回改变后的数组，并改变原数组
    * slice(startIndex,endIndex) 返回起始到终止位置的数组

      ```
      //slice() 将类似数组的对象转化为真正的数组
      Array.prototype.slice.call({ 0: 'a', 1: 'b', length: 2 })
      // ['a', 'b']
      ```
    * splice(startIndex,deleteNum,insertElement)
    * sort() 数组排序，可以传入回调函数控制排序颗粒度
    * map() 数组遍历，对数组所有成员依次调用一个回调函数，返回新数组，原数组不变
    * foreach() 数组遍历同map()，但没有返回值，forEach方法遍历无法中断，即不能加入中断条件，这种情况可以采用for循环，第一个参数为函数，第二个参数为绑定函数的上下文（this指向）
    * filter() 数组筛选，函数作为参数，返回结果为true的成员组成一个新的数组返回，原数组不变，第一个参数为函数，第二个参数为绑定函数的上下文（this指向）



* 数组的解构赋值： 数组的元素是按照次序来排列的，变量的取值由它的位置来决定。

    `var [a, b, c] = [1, 2, 3];`
         
<h2 id="4">4 . 字符串</h2>


<h2 id="5">5. 函数</h2>

* 构造函数： 

        “对象”是单个实物的抽象。通常需要一个模板，表示某一类实物的共同特征，然后“对象”根据这个模板生成。
        JavaScript语言使用构造函数（constructor）作为对象的模板。
        构造函数的写法就是一个普通的函数，但是有自己的特征和用法。
        
        
        ```javascript
          var Vehicle = function (){
            this.price = 1000;
          };
          
          //通过new命令，让构造函数Vehicle生成一个实例对象，保存在变量v中。
            这个新生成的实例对象，从构造函数Vehicle继承了price属性。
            
          // new 命令执行的操作步骤
            1.创建一个空对象，作为将要返回的对象实例
            2.将这个空对象的原型，指向构造函数的prototype属性
            3.将这个空对象赋值给函数内部的this关键字
            4.开始执行构造函数内部的代码
          
          //若没有添加new命令，则price成为了全局变量，v.price也会报错提示undefined
          var v = new Vehicle();
          v.price // 1000
          
          function Vehicle(){
            //防止漏用new命令
            if (!(this instanceof Vehicle)) {
              return new Vehicle();
            }
          
            this.price = 1000;
          }
        ```

* Function.prototype.call() && Function.prototype.apply() && Function.prototype.bind()
    
    第一个参数为函数调用的对象，后面的参数为该函数执行时需要的参数
    
    函数.call(obj,argment1,argment2...)
    
    函数.apply(obj,[argment1,argment2...])
    
    ```javascript
      var a = ['a', , 'b'];
      
      function print(i) {
        console.log(i);
      }
      
      a.forEach(print)
      // a
      // b
      
      Array.apply(null, a).forEach(print)
      // a
      // undefined
      // b
    ```
    函数.bind(obj,argment1,argment2...)  
        
        将函数体内的this绑定到指定的对象上
        每运行一次返回一个新函数
    
    ```javascript
    //自定义bind , 防止部分浏览器不支持
      if(!('bind' in Function.prototype)){
        Function.prototype.bind = function(){
          var fn = this;
          var context = arguments[0];
          var args = Array.prototype.slice.call(arguments, 1);
          return function(){
            return fn.apply(context, args);
          }
        }
      }
    ```
    
    prototype 原型链 
    
    * 读取对象属性时，先从本身开始寻找，再向对象原型寻找，逐级向上，直至到Object.prototype，返回null
    * instanceof运算符用来比较一个对象是否为某个构造函数的实例
    * prototype对象有一个constructor属性，默认指向prototype对象所在的构造函数
    
* 参数的解构赋值

  写法一函数参数的默认值是空对象，但是设置了对象解构赋值的默认值；
  写法二函数参数的默认值是一个有具体属性的对象，但是没有设置对象解构赋值的默认值。
    
    ```javascript
        // 写法一
        function m1({x = 0, y = 0} = {}) {
          return [x, y];
        }
        m1(); // 此时m1函数没有传参，及参数为空（广义的对象），则输出默认值
        // 写法二
        function m2({x, y} = { x: 0, y: 0 }) {
          return [x, y];
        }
    ```
* 函数参数的作用域
    ```javascript
      let x = 1;
      
      function f(y = x) {
        let x = 2;
        console.log(y);
      }
      
    //函数f传入参数为空，函数内部没有生成变量x，因此指向了全局变量x，如果此时全局环境也没有声明x变量，则会报错
      f() // 1
    ```
* rest 参数
  * `...变量名`，用于获取函数多余的参数，类别es5的arguments对象
  * 扩展运算符 `...`，相当于rest参数的逆运算，将一个数组转为用逗号分隔的参数序列
    ```javascript
        // ES5的写法
        var arr1 = [0, 1, 2];
        var arr2 = [3, 4, 5];
        Array.prototype.push.apply(arr1, arr2);
        
        // ES6的写法
        var arr1 = [0, 1, 2];
        var arr2 = [3, 4, 5];
        arr1.push(...arr2);
        
        //上面代码的ES5写法中，push方法的参数不能是数组，所以只好通过apply方法变通使用push方法。
        // 有了扩展运算符，就可以直接将数组传入push方法。
    ```
    
* 函数的length属性
    
    * 指定了默认值以后，函数的length属性，将返回没有指定默认值的参数个数。也就是说，指定了默认值后，length属性将失真。

* 箭头函数
    ```javascript
      //如果箭头函数的代码块部分多于一条语句，就要使用大括号将它们括起来，并且使用return语句返回。
      //由于大括号被解释为代码块，所以如果箭头函数直接返回一个对象，必须在对象外面加上括号。
      var getTempItem = id => ({ id: id, name: "Temp" });
    ```
    箭头函数有几个使用注意点。(箭头函数里面根本没有自己的this，而是引用外层的this。)
    
    （1）函数体内的this对象，就是定义时所在的对象，而不是使用时所在的对象。
    
    （2）不可以当作构造函数，也就是说，不可以使用new命令，否则会抛出一个错误。
    
    （3）不可以使用arguments对象，该对象在函数体内不存在。如果要用，可以用Rest参数代替。
    
    （4）不可以使用yield命令，因此箭头函数不能用作Generator函数。

* 函数尾递归
    
    * 函数调用时，会在内存中形成一个“调用记录”（调用帧），保存调用位置和调用变量等信息。
    * 如果在函数A的内部调用函数B，那么在A的调用帧上方，还会形成一个B的调用帧。等到B运行结束，将结果返回到A，B的调用帧才会消失。如果函数B内部还调用函数C，那就还有一个C的调用帧，以此类推。所有的调用帧，就形成一个“调用栈”（call stack）。
    * 尾调用由于是函数的最后一步操作，所以不需要保留外层函数的调用帧，因为调用位置、内部变量等信息都不会再用到了，只要直接用内层函数的调用帧，取代外层函数的调用帧就可以了。
    ```javascript
      function f() {
        let m = 1;
        let n = 2;
        return g(m + n);
      }
      f();
      
      // 等同于
      function f() {
        return g(3);
      }
      f();
      
      // 等同于
      g(3);
    ```
    * 上面代码中，如果函数g不是尾调用，函数f就需要保存内部变量m和n的值、g的调用位置等信息。
      但由于调用g之后，函数f就结束了，所以执行到最后一步，完全可以删除 f(x) 的调用帧，只保留 g(3) 的调用帧。
      
      这就叫做“尾调用优化”（Tail call optimization），即只保留内层函数的调用帧。
      如果所有函数都是尾调用，那么完全可以做到每次执行时，调用帧只有一项，这将大大节省内存。这就是“尾调用优化”的意义。
  
      
<h2 id="6">6 . 对象</h2>

* 对象：键值对的集合，键名的数据类型均为原始类型（字符串、数字），键值可以为任意数据类型

* 对象的Object()方法： 如果参数是原始类型的值，Object方法返回对应的包装对象的实例，如果Object方法的参数是一个对象，它总是返回原对象。

* 属性和方法的简写

    ```javascript
      //直接写入变量，变量名自动变为属性名，变量值即为变量本身。
      var foo = 'bar';
      var baz = {foo};
      baz // {foo: "bar"}
    
      //方法简写
      var o = {
        method() {
          return "Hello!";
        }
      };
      // 等同于
      var o = {
        method: function() {
          return "Hello!";
        }
      };
    
      //CommonJS模块输出变量，非常合适使用简洁写法
      module.exports = { getItem, setItem, clear };
      // 等同于
      module.exports = {
        getItem: getItem,
        setItem: setItem,
        clear: clear
      };
    ```
* Object.is(a,b) 
    
    判断两个值是否相等，修复了es5中-0与+0相等的问题，以及NaN与NaN自身不等的问题
* Object.assign(targetobj1,sourceobj2,sourceobj3)

    用于对象的合并，并返回合并之后的对象，属于浅拷贝，基于源对象的引用    
* Object.getOwnPropertyDescriptor

    对象的每个属性都有一个可描述对象，此方法就是获取该属性的描述对象
    ```javascript
      let obj = { foo: 123 };
      Object.getOwnPropertyDescriptor(obj, 'foo')
      //  {
      //    value: 123,
      //    writable: true,
      //    enumerable: true,
      //    configurable: true
      //  }
    ```
    
* 对象的解构赋值: 对象的属性没有次序，变量名必须与属性同名，才能取到正确的值。
    
    ```javascript
      //简写形态
      var { foo, bar } = { foo: "aaa", bar: "bbb" };
      foo // "aaa"
      bar // "bbb"
      //原始形态
      var { foo: foo, bar: bar } = { foo: "aaa", bar: "bbb" };
      // foo 是匹配的模式 ， foo：后的foo才是变量，真正被赋值的是变量
    
      //嵌套模式下的对象解构 (对象中的对象（狭义对象，数组，函数）)
      var obj = {
        p: [
          'Hello',
          { y: 'World' }
        ]
      };
          //注意，这时p是模式，不是变量，因此不会被赋值。
      var { p: [x, { y }] } = obj;
      x // "Hello"
      y // "World"
    ```

<h2 id="7">7 . Symbol</h2> 

* 防止命名冲突

    ```javascript
      let s = Symbol();
      
      typeof s
      // "symbol"
      //由于每一个Symbol值都是不相等的，
      // 这意味着Symbol值可以作为标识符，用于对象的属性名，
      // 就能保证不会出现同名的属性。
      // 这对于一个对象由多个模块构成的情况非常有用，能防止某一个键被不小心改写或覆盖。
    ```
    
<h2 id="8">8 . Set and Map</h2> 

* ES6提供了新的数据结构Set。它类似于数组，但是成员的值都是唯一的，没有重复的值。

* JavaScript的对象（Object），本质上是键值对的集合（Hash结构），但是传统上只能用字符串当作键。
    
    ```javascript
      var data = {};
      var element = document.getElementById('myDiv');
      
      data[element] = 'metadata';
      data['[object HTMLDivElement]'] // "metadata"
    
      上面代码原意是将一个DOM节点作为对象data的键，但是由于对象只接受字符串作为键名，所以element被自动转为字符串[object HTMLDivElement]。
      为了解决这个问题，ES6提供了Map数据结构。
      它类似于对象，也是键值对的集合，但是“键”的范围不限于字符串，各种类型的值（包括对象）都可以当作键。
      也就是说，Object结构提供了“字符串—值”的对应，Map结构提供了“值—值”的对应，是一种更完善的Hash结构实现。
      如果你需要“键值对”的数据结构，Map比Object更合适。
    ```

<h2 id="9">9 . 浏览器环境</h2>

* script
* window对象
* History对象
* cookie
* Web Storage
* AJAX 同源政策 跨域
* IndexDB


<h2 id="10">10 . 栈与堆</h2>

* 栈 ：有唯一编号的乒乓球，以及一个出口的圆筒乒乓球盒，栈的存取方式 根据乒乓球编号，依次拿出顶部乒乓球，直到拿到此编号的乒乓球 => 先进后出，后进先出

* 堆 ：水平放置于书架上的书，书架 => 书 （key=>value），堆的存取方式 根据书名取出此书即可，无序

* Js代码逐行执行时，执行上下文（当前代码的执行环境（1.全局上下文；2.当前函数上下文；3.eval()））进出栈详解：
    
    首先全局上下文入栈，其次遇到函数时，当前函数执行上下文入栈，
    函数中又遇到函数，继续将当前函数执行上下文入栈，以此类推
    直至全部函数执行完毕，
    根据栈的顺序，最顶层的函数上下文依次出栈(被浏览器垃圾回收机制回收)，（先进后出，后进先出）
    栈底就只有全局上下文，关闭浏览器时，全局上下文出栈

    * 单线程
    * 同步执行，只有栈顶的上下文处于执行中，其他上下文需要等待
    * 全局上下文只有唯一的一个，它在浏览器关闭时出栈
    * 函数的执行上下文的个数没有限制
    * 每次某个函数被调用，就会有个新的执行上下文为其创建，即使是调用的自身函数，也是如此。

1. 执行上下文都干了什么：
    
    简单描述：进入执行上下文后，首先创建变量对象，函数声明提升，变量声明（有值则跳过，无值则undefined），接着进入执行阶段，变量对象变为活动对象，活动对象中的属性及属性值能够访问，开始逐行执行代码，完成相关操作。
    
    当调用一个函数时（激活），一个新的执行上下文就会被创建。而一个执行上下文的生命周期可以分为两个阶段。
    * 创建阶段：在这个阶段中，执行上下文会分别创建`变量对象`，建立`作用域链`，以及确定`this的指向`

        * 变量对象：
            1. 建立arguments对象。检查当前上下文中的参数，建立该对象下的属性与属性值。

            2. 检查当前上下文的函数声明，也就是使用function关键字声明的函数。在变量对象中以函数名建立一个属性，属性值为指向该函数所在内存地址的引用。如果函数名的属性已经存在，那么该属性将会被新的引用所覆盖。

            3. 检查当前上下文中的变量声明，每找到一个变量声明，就在变量对象中以变量名建立一个属性，属性值为undefined。如果该变量名的属性已经存在，为了防止同名的函数被修改为undefined，则会直接跳过，原属性值不会被修改。

    * 代码执行阶段：创建完成之后，就会开始执行代码，这个时候，会完成`变量赋值`，`函数引用`，以及执行其他代码。

        * 进入执行阶段后，变量对象变为活动对象：里面的属性都能被访问了，然后开始进行执行阶段的操作。


2. 作用域链和闭包
    
    * 作用域：

        * 在JavaScript中，我们可以将作用域定义为一套规则,这套规则用来管理引擎如何在当前作用域以及嵌套的子作用域中根据标识符名称（变量名或者函数名）进行变量查找。

        * JavaScript中只有全局作用域与函数作用域(因为eval我们平时开发中几乎不会用到它)。

        * 作用域与执行上下文是完全不同的两个概念。

        JavaScript代码的整个执行过程，分为两个阶段，代码编译阶段与代码执行阶段。
        编译阶段由编译器完成，将代码翻译成可执行代码，这个阶段作用域规则会确定。
        执行阶段由引擎完成，主要任务是执行可执行代码，执行上下文在这个阶段创建。

    * 作用域链：是由当前环境与上层环境的一系列变量对象组成，它保证了当前执行环境对符合访问权限的变量和函数的有序访问。

        ```javascript
        var a = 20;

        function test() {
            var b = a + 10;

            function innerTest() {
                var c = 10;
                return b + c;
            }

            return innerTest();
        }

        test();
        ```

        ```javascript
        //  在上面的例子中，全局，函数test，函数innerTest的执行上下文先后创建。我们设定他们的变量对象分别为VO(global)，VO(test), VO(innerTest)。而innerTest的作用域链，则同时包含了这三个变量对象，所以innerTest的执行上下文可如下表示。
        innerTestEC = {
            VO: {...},  // 变量对象
            scopeChain: [VO(innerTest), VO(test), VO(global)], // 作用域链
            this: {}
        }
        ```

    * 闭包：当一个函数可以记住并访问所在的作用域（全局作用域除外），并在定义该函数的作用域之外执行时，该函数就可以称之为一个闭包。（假设函数A在函数B的内部进行定义了，并在函数B的作用域之外执行（不管是上层作用域，下层作用域，还有其他作用域），那么A就是一个闭包）
    
        ```javascript
        var fn = null;
        function foo() {
            var a = 2;
            function innnerFoo() { 
                console.log(a);
            }
            fn = innnerFoo; // 将 innnerFoo的引用，赋值给全局变量中的fn
        }

        function bar() {
            fn(); // 此处的保留的innerFoo的引用
        }

        foo();
        bar(); // 2
        //foo()执行完毕之后，按照常理，其执行环境生命周期会结束，所占内存被垃圾收集器释放。
        但是通过fn = innerFoo，函数innerFoo的引用被保留了下来，复制给了全局变量fn。
        这个行为，导致了foo的变量对象，也被保留了下来。
        于是，函数fn在函数bar内部执行时，依然可以访问这个被保留下来的变量对象。
        所以此刻仍然能够访问到变量a的值。

        //这样，我们就可以称fn为闭包。(fn本身的执行环境实在foo的函数上下文，实际的执行环境是在bar函数的上下文)

        虽然例子中的闭包被保存在了全局变量中，但是闭包的作用域链并不会发生任何改变。
        在闭包中，能访问到的变量，仍然是作用域链上能够查询到的变量。
        ```



    

