#### 箭头函数和普通函数有什么区别? 箭头函数为什么不能作为构造函数？
1. 箭头函数比普通函数更加简洁
2. 箭头函数没有自己的this
3. 箭头函数继承来的this指向永远不会改变
4.  call()、apply()、bind()等方法不能改变箭头函数中this的指向 
```js
var id = 'Global';
let fun1 = () => {
    console.log(this.id)
};
fun1();                     // 'Global'
fun1.call({id: 'Obj'});     // 'Global'
fun1.apply({id: 'Obj'});    // 'Global'
fun1.bind({id: 'Obj'})();   // 'Global'
```
5. 箭头函数不能作为构造函数使用 
6. 箭头函数没有自己的arguments
7.  箭头函数没有prototype
8.  箭头函数不同于传统JavaScript中的函数，箭头函数并没有属于⾃⼰的this，它所谓的this是捕获其所在上下⽂的 this 值，作为⾃⼰的 this 值，并且由于没有属于⾃⼰的this，所以是不会被new调⽤的，这个所谓的this也不会被改变。
9.  #### Promise相关面试题 用过哪些静态方法？ 讲一下all和allsettled区别？ promise有哪些作用？
 https://blog.csdn.net/qq_42033567/article/details/108129645

  #### 数组、函数、对象原型链之间的关系
https://blog.csdn.net/Linwang2020/article/details/109563218

##### 为什么字符串可以调用slice这些方法?
   这是因为js在执行字符串语句的时候，对字符串进行了一层包装，就是我们常说的包装类型
new String()生成一个示例，将这个实例用另一个变量储存，实例调用方法(对象的可扩展性)，执行完后，销毁这个实例
```js
var str = 'aaaaa'
str.substring(2)

// -----等价于：-----
var str = 'aaaaa'
var str1 = new String(str)
str1.substring(2)
str = str1
str1 = null
``` 
#### 原型/原型链的理解？ 继承？
https://blog.csdn.net/qq_45954420/article/details/123945118
#### node.js有个commonjs的规范，es6为什么又出现了esm规范？
在 ES6 之前，社区制定了一些模块加载方案，最主要的有 CommonJS 和 AMD 两种。前者用于服务器，后者用于浏览器。ES6 在语言标准的层面上，实现了模块功能，而且实现得相当简单，完全可以取代 CommonJS 和 AMD 规范，成为浏览器和服务器通用的模块解决方案。
ES6 模块的设计思想是尽量的静态化，使得编译时就能确定模块的依赖关系，以及输入和输出的变量。CommonJS 和 AMD 模块，都只能在运行时确定这些东西。
#### async里面await了一个接口，后面有个console.log(1),为什么console.log会等待await后的执行完？
https://blog.csdn.net/weixin_41784648/article/details/108334512
#### let const var区别
https://blog.csdn.net/qq_45799465/article/details/122892209

#### JS中的事件捕获？

#### JS中的继承？

#### 数组常用(排序)的方法 数组sort方法返回值不能可能是？

#### BFC

#### 作用域和作用域链

#### 闭包

#### 基本数据类型和引用数据类型

#### arguments

####  深拷贝和浅拷贝

#### defer和aync

#### 如何判定类型: type instanceof Object.prototype.toString.call()

#### ts ,type和interface的区别

#### es6新增 es6的import时同步还是异步？

#### js哪些地方用到了栈？（执行上下文栈）

#### 给一个空数组或空对象怎么判断为空?

#### 手写flat

#### js检测数据类型的方法

#### map和forEach对于对象会不会改变？

#### Map和Ojectd的区别?

#### 单页应用怎么跨页面传参？ 权限怎么设计的？

#### js执行机制？

#### 判断数组的方法？

#### 改变this的方式

#### 先bing函数在call函数最后this指向哪一个?


#### 连续两次bind的this指向哪一个this？

#### Promise和Asyn await有什么区别？

#### if(0=="")判断转换过程？

#### a==1 && a==2 && a=3满足这个表达式的a

#### typeof和instanceof区别

#### 判断数据类型的方法

#### fetch发请求不知道超没超时，怎么写一个功能让他和axios一样可以响应超时（promise）

#### 求数组sort(主要针对['100','500']这种字符串数组结果)

#### 使用Peomise、async、await实现红绿灯切换，并在控制台打印输出，红灯30s，黄灯5s，绿灯20s

##### 怎么劫持函数？（提示：call、apply、bind的区别）

#### tS比js有什么优势？

#### 树形转数组？

#### esm和cjs

#### 手写快排 十进制转十六进制

#### es的语法新规范？

#### 怎么继承类？

#### 怎么合并对象？

#### ts Partial Omit怎么实现的？

#### 类型拓宽？

#### 写一个promiseall

#### js继承 手搓son类 parent类

#### 手写js原生bind