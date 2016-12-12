# Js-plan
a new understanding about javascript

1. [Js基本组成](#1)
2. [数据类型](#2)
3. [数组的解构赋值](#3)
4. [对象的解构赋值](#4)
5. [函数](#5)
6. [对象](#6)


<h2 id="1">1. Js 基本组成</h2>

* 基础语法 —— 语法、数据类型、数据类型转换、错误处理机制等
* 标准库 ——　各类广义对象及其携带的属性、方法
* DOM API
* 浏览器 API
* WEB API

<h2 id="2">Js 数据类型 —— 字符串、数值、布尔值、undefined、null、对象、Symbol</h2>

* 原始类型 —— 字符串、数值、布尔值
* 合成类型 ——　对象 （JavaScript的所有数据，都可以视为广义的对象）
    
    对象分为　——　狭义的对象（仅指Object）、数组、函数
      
* this
    
    this返回属性或方法“当前”所在的对象。

* 单线程
    
    一个程序运行之后便称为“进程”，进程中包含程序需要执行的各项任务，形成了任务队列，
    一般采用多线程来处理多项任务，线程中执行任务分为同步和异步。
    * 同步 ： 下一个任务等待上一个任务执行完成之后再执行
    * 异步 ： 任务提交请求之后，通过回调函数处理回应，从而继续执行任务，任务之间没有等待

<h2 id="3">数组的解构赋值</h2>

* 数组的元素是按照次序来排列的，变量的取值由它的位置来决定。

    `var [a, b, c] = [1, 2, 3];`
         
<h2 id="4">对象的解构赋值</h2>

* 对象的属性没有次序，变量名必须与属性同名，才能取到正确的值。
    
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

    
<h2 id="5">函数</h2>

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
    * 上面代码中，如果函数g不是尾调用，函数f就需要保存内部变量m和n的值、g的调用位置等信息。但由于调用g之后，函数f就结束了，所以执行到最后一步，完全可以删除 f(x) 的调用帧，只保留 g(3) 的调用帧。
      
      这就叫做“尾调用优化”（Tail call optimization），即只保留内层函数的调用帧。如果所有函数都是尾调用，那么完全可以做到每次执行时，调用帧只有一项，这将大大节省内存。这就是“尾调用优化”的意义。
  
      
<h2 id="6">对象</h2>
  
*  