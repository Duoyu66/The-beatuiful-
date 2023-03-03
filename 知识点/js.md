#### 箭头函数和普通函数有什么区别? 箭头函数为什么不能作为构造函数？
1. 箭头函数比普通函数更加简洁
2. 箭头函数没有自己的this
3. 箭头函数继承来的this指向永远不会改变
4. call()、apply()、bind()等方法不能改变箭头函数中this的指向 
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
 #### Promise和Asyn await有什么区别？
https://blog.csdn.net/weixin_44246717/article/details/118659810
    #### Promise相关面试题 
  #####  promise有哪些作用？
*  promise： 解决异步回调的问题
 https://blog.csdn.net/qq_42033567/article/details/108129645
* promise.then是微任务，会在所有的宏任务执行完之后才会执行
##### 用过哪些静态方法？  
Promise.all([promise1, promise2, promise3]) 等待原则, 是在所有promise都完成后执行, 可以用于处理一些并发的任务，如果Promise实例都进入Fulfilled状态，Promise.all返回的实例才会变成Fulfilled状态并将Promise实实例数组的所有返回值组成一个数组，传给Promise.all返回实例的回调函数；如果有某一个或者多个实例进入rejected状态，Promise.all返回的实例会立即变成Rejected状态并将第一个rejected的实例返回值传递给Promise.all返回实例的回调函数。
Promise.race([promise1, promise2, promise3]) 赛跑, 竞速原则, 只要三个promise中有一个满足条件, 就会执行.then(用的较少)，先执行到成功就返回成功的状态，返回失败就是失败状态
#### 讲一下all和allsettled区别？
* 它们所返回的数据不太一样，all()返回一个直接包裹resolve内容的数组，则allSettled()返回一个包裹着对象的数组。
* .all()方法，如果有一个Promise对象报错了，则all()无法执行，会报错你的错误，无法获得其他成功的数据。则allSettled()方法是不管有没有报错，把所有的Promise实例的数据都返回回来，放入到一个对象中。如果是resolve的数据则status值为fulfilled,相反则为rejected。

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
* 事件捕获（event capturing）： 当鼠标点击或者触发dom事件时（被触发dom事件的这个元素被叫作事件源），浏览器会从根节点 =>事件源（由外到内）进行事件传播。
* 事件冒泡（dubbed bubbling）： 事件源 =>根节点（由内到外）进行事件传播。
#### JS中的继承？  js继承 手搓son类 parent类
https://blog.csdn.net/qq_44746317/article/details/124171314
一、原型链继承
二、构造函数继承
三、原型链加构造函数继承
四、原型式继承
五、寄生组合式继承
#### 数组常用(排序)的方法 
https://blog.csdn.net/weixin_51338875/article/details/127820757
##### 改变原数组的方法：
1. push（） 末尾添加数据
2. pop（） 末尾出删除数据
3. unshift（） 头部添加数据
4. shift（） 头部删除数据
5. reverse（） 翻转数组
6. sort（） 排序
7. splice（）  截取数组
##### 不改变原数组的方法:
1. concat（）  合并数组
2. join（） 数组转字符串
3. slice（）截取数组的一部分数据
4. indexOf 从左检查数组中有没有这个数
5. lastIndexOf 从右检查数组中有没有这个数值
##### ES6新增的数组方法
1. forEach()   用来循环遍历的 for
2. map  映射数组的
3. filter  过滤数组
4. every  判断数组是不是满足所有条件
5. some（） 数组中有没有满足条件的
6. find（）用来获取数组中满足条件的第一个数据
7. reduce（）叠加后的效果
##### 数组sort方法返回值不能可能是？
???
#### BFC
https://blog.csdn.net/yigetutouzai/article/details/125615578
BFC: BFC(Block formatting context)直译为"块级格式化上下文"。它是一个独立的渲染区域，只有Block-level box参与， 它规定了内部的Block-level Box如何布局，并且与这个区域外部毫不相干。
#### 作用域和作用域链
https://blog.csdn.net/weixin_44247866/article/details/128043543
#### 闭包
https://blog.csdn.net/weixin_56266471/article/details/125225998
#### 基本数据类型和引用数据类型
基本数据类型：undefined boolean null number string bigInt Symbol
引用数据类型：Object Function 
相关API：
* isNaN() 检测是否是非数字
* parseFloat()取浮点数
* parseInt()取整
#### arguments
https://blog.csdn.net/fuhanghang/article/details/110930595
####  深拷贝和浅拷贝
https://blog.csdn.net/qq_39045645/article/details/121151205
手写深浅拷贝
https://blog.csdn.net/qq_39045645/article/details/121151205
#### defer和aync
https://blog.csdn.net/weixin_62765236/article/details/126649027
* 如果一个script加了defer属性，即使放在head里面，它也会在html页面解析完毕之后再去执行，也就是类似于把这个script放在了页面底部。
* 对于async，这个是html5中新增的属性，它的作用是能够异步的加载和执行脚本，不因为加载脚本而阻塞页面的加载。一旦加载到就会立刻执行
##### 两者的相同点

* 加载文件时不阻塞页面渲染。

* 对于inline的script无效。

* 使用这两个属性的脚本中不能调用document.write方法。

* 有脚本的onload的事件回调。
#### 如何判定类型: type instanceof Object.prototype.toString.call()  typeof和instanceof区别
https://blog.csdn.net/Alone_Endeavor/article/details/129230619
#### ts中type和interface的区别
https://juejin.cn/post/7066757947140866056
interface：接口，TS 设计出来主要用于定义【对象类型】，可以对【对象】的形状进行描述。

type ：类型别名，为类型创建一个新名称。它并不是一个类型，只是一个别名。
#### es6新增 es6的import时同步还是异步？ 异步
https://blog.csdn.net/jiangshen_a/article/details/126650406

https://blog.csdn.net/qq_36303110/article/details/110203557
#### js哪些地方用到了栈？（执行上下文栈）
https://blog.csdn.net/Ronychen/article/details/114007467
https://blog.csdn.net/weixin_43830624/article/details/123843563
#### 给一个空数组或空对象怎么判断为空?
https://blog.csdn.net/weixin_59025868/article/details/127627342

进阶
https://blog.csdn.net/CEZLZ/article/details/121153716
#### 手写flat
https://blog.csdn.net/qq_52180526/article/details/128181565
#### js检测数据类型的方法
https://blog.csdn.net/m0_64346035/article/details/125045424
#### map和forEach对于对象会不会改变？ <??>
https://blog.csdn.net/Ruiqi8/article/details/127418469
#### Map和Ojectd的区别?
https://blog.csdn.net/weixin_44730897/article/details/124836213
#### js执行机制？
https://blog.csdn.net/m0_64562972/article/details/126813253
#### 判断数组的方法？
https://blog.csdn.net/weixin_44066534/article/details/108549526
#### 改变this的方式
https://blog.csdn.net/weixin_47619284/article/details/126472468
#### 先bing函数在call函数最后this指向哪一个?
???

#### 连续两次bind的this指向哪一个this？
https://blog.csdn.net/qq_51368103/article/details/126309800

#### if(0=="")判断转换过程？
https://blog.csdn.net/andy_2/article/details/83771276
#### a==1 && a==2 && a=3满足这个表达式的a
https://blog.csdn.net/web22050702/article/details/124840706
#### fetch发请求不知道超没超时，怎么写一个功能让他和axios一样可以响应超时（promise）
https://blog.csdn.net/weixin_44286392/article/details/127517822
#### 求数组sort(主要针对['100','500']这种字符串数组结果)  (???)

#### 使用Peomise、async、await实现红绿灯切换，并在控制台打印输出，红灯30s，黄灯5s，绿灯20s

##### 怎么劫持函数？（提示：call、apply、bind的区别）
https://blog.csdn.net/m0_37911706/article/details/127461052
#### tS比js有什么优势？
更可靠：TS引入类型定义（进行类型检查）和编译器，可以避免JavaScript大多数runtime错误，更可靠，易维护； 更清晰：TS中显式类型声明可以提升代码可读性，代码校验可以全部交给编译器负责；

更广泛：TypeScript是JavaScript的超集，可以在TypeScript代码中混合使用任何JavaScript库和代码。
#### 树形转数组？

#### 手写快排 十进制转十六进制

#### 怎么合并对象？
方式一：扩展运算符 ...
方式二：Object.assign(目标对象，来源对象) 合并对象
方式三：for...in
#### 类型拓宽？ ^^^
https://blog.csdn.net/zxl1990_ok/article/details/125317703
#### 写一个promiseall
https://blog.csdn.net/weixin_43376417/article/details/126561767
#### 手写js原生bind
https://blog.csdn.net/weixin_48956280/article/details/126467632