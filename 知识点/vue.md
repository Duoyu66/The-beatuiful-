# day01
### 生命周期
* 生命周期的作用是：不同阶段通过对应的钩子函数来实现组件数据管理和DOM渲染两大重要功能。
#### 生命周期各个钩子的作用？
1. beforeCreate:这个时候，在实例被完成创建出来，el和data都没有初始化，不能访问data、method，一般在这个阶段不进行操作。
2. created:这个时候，vue实例中的data、method已被初始化，属性也被绑定，但是此时还是虚拟dom，真是dom还没生成，$el 还不可用。这个时候可以调用data和method的数据及方法，created钩子函数是最早可以调用data和method的，故一般在此对数据进行初始化。
3. beforemounted:此时模板已经编译完成，但还没有被渲染至页面中（即为虚拟dom加载为真实dom），此时el存在则会显示el。在这里可以在渲染前最后一次更改数据的机会，不会触发其他的钩子函数，一般可以在这里做初始数据的获取。
4. mounted:此时模板已经被渲染成真实DOM，用户已经可以看到渲染完成的页面，页面的数据也是通过双向绑定显示data中的数据。 这实例创建期间的最后一个生命周期函数，当执行完 mounted 就表示，实例已经被完全创建好了
5. beforeupdate:更新前状态（view层的数据变化前，不是data中的数据改变前），重新渲染之前触发，然后vue的虚拟dom机制会重新构建虚拟dom与上一次的虚拟dom树利用diff算法进行对比之后重新渲染。只有view上面的数据变化才会触发beforeUpdate和updated，仅属于data中的数据改变是并不能触发。
6. updated:数据已经更改完成，dom也重新render完成。
7. beforeDestory:销毁前执行（$destroy方法被调用的时候就会执行）,一般在这里善后:清除计时器、清除非指令绑定的事件等等…’)
8. destroyed:销毁后 （Dom元素存在，只是不再受vue控制）,卸载watcher，事件监听，子组件。
  ---
### 路由
#### 路由有哪些钩子函数？
1. **全局的路由钩子函数**
   1.1 beforeEach(全局前置钩子)意思是每次每一个路由改变的时候都要执行一遍
         它有三个参数：

        to： route：即将要进入的目标 路由对象

        from：route：当前导航正要离开的路由

        next：function：一定要调用该方法来resolve这个钩子。执行效果依赖next方法
   应用场景：
   (1)进行一些页面跳转前的处理，例如跳转到的页面需要进行登录才可以访问时，就会做登录的跳转
    (2). 进入页面登录判断、管理员权限判断、浏览器判断
   1.2 afterEach(全局后置钩子)
2. 单路由内的钩子函数
    2.1 beforeEnter: 可以直接在路由配置上直接定义beforeEnter，这些守卫与全局前置守卫的方法参数是一样的
3. 组件内的路由钩子
   beforeRouteEnter、beforeRouteUpdata、beforeRouteLeave
   应用场景:

        1、清除组件中的定时器

        2、当页面有未关闭的窗口，或未保存的内容时，阻止页面跳转

        3、保存相关内容到Vuex和Session中
#### 路由可以传递哪些参数
##### 前言
1）路由跳转有几种方式？

1：声明式导航：router-link（务必要带有to属性），可以实现路由的跳转
2：编程式导航：利用的是组件实例的$router.push | replace方法，可以实现路由的跳转。（还可以写一些自己的业务）
2）路由传参，参数有几种写法？

1：params参数：属于路径当中的一部分，需要注意，在配置路由的时候，需要占位
2：query参数：不属于路径当中的一部分，类似于ajax中的queryString /home?k=v&kv=,不需要占位
    原文链接 https://blog.csdn.net/bying666/article/details/126939220
     
---
#### 组件间通讯
1. 父->子 props
2. 子->父 父亲给儿子传递一个函数，儿子将参数放进函数带给父亲
3. 全局事件总线 接受用$on 给数据的组件用 $emit
4. Vuex
5. ref/$refs
6. $attrs与listeners
7. $parent/$children
8. 依赖注入(provide/inject)    **依赖注入所提供的属性是非响应式的**
9. 总结
1. 父子组件间通信

    * 子组件通过 props 属性来接受父组件的数据，然后父组件在子组件上注册监听事件，子组件通过 emit 触发事件来向父组件发送数据。
    * 通过 ref 属性给子组件设置一个名字。父组件通过 $refs 组件名来获得子组件，子组件通过 $parent 获得父组件，这样也可以实现通信。
    * 使用 provide/inject，在父组件中通过 provide提供变量，在子组件中通过 inject 来将变量注入到组件中。不论子组件有多深，只要调用了 inject 那么就可以注入 provide中的数据

2. 跨代组件间通信

跨代组件间通信其实就是多层的父子组件通信，同样可以使用上述父子组件间通信的方法，只不过需要多层通信会比较麻烦。
3. 兄弟组件间通信

通过 $parent + $refs 以父组件为中间人来获取到兄弟组件，也可以进行通信。
4. 任意组件间通信

使用 eventBus ，其实就是创建一个事件中心，相当于中转站，可以用它来传递事件和接收事件。它的本质是通过创建一个空的 Vue 实例来作为消息传递的对象，通信的组件引入这个实例，通信的组件通过在这个实例上监听和触发事件，来实现消息的传递。

#### action和action有什么区别？
1、流程顺序

“相应视图—>修改State”拆分成两部分，视图触发Action，Action再触发Mutation。

2、角色定位

基于流程顺序，二者扮演不同的角色。

Mutation：专注于修改State，理论上是修改State的唯一途径。

Action：业务代码、异步请求。

3、限制

角色不同，二者有不同的限制。

Mutation：必须同步执行。

Action：可以异步，但不能直接操作State。

---
### Others
#### v-show和v-if
##### 不同点
1. v-show：相当于dispaly:none; 占位   频繁切换使用v-show 有更高的初始渲染消耗
2. v-if:动态的向 DOM 树内添加或者删除 DOM 元素 有更高的切换消耗
* display:none是不为隐藏的对象保留其物理空间，俗称看不见也摸不着； --> 隐藏元素后,不占位;
* visible: hidden是为隐藏的对象保留其物理空间的，俗称看不见但摸得着。 --> 隐藏元素后占位.
  ##### 共同点：
1. 当表达式都为 false 时，都不会占据页面位置 
2. 当表达式结果为 true 时，都会占据页面的位置
   #### v-for为什么要用key？
  1. vue中列表循环需加:key=“唯一标识” 唯一标识尽量是item里面id等，因为vue组件高度复用增加Key可以标识组件的唯一性，为了更好地区别各个组件 key的作用主要是为了高效的更新虚拟DOM。

2. key主要用来做dom diff算法用的，diff算法是同级比较，比较当前标签上的key还有它当前的标签名，如果key和标签名都一样时只是做了一个移动的操作，不会重新创建元素和删除元素。

3. 没有key的时候默认使用的是“就地复用”策略。如果数据项的顺序被改变，Vue不是移动Dom元素来匹配数据项的改变，而是简单复用原来位置的每个元素。如果删除第一个元素，在进行比较时发现标签一样值不一样时，就会复用之前的位置，将新值直接放到该位置，以此类推，最后多出一个就会把最后一个删除掉。

4. 尽量不要使用索引值index作key值，一定要用唯一标识的值，如id等。因为若用数组索引index为key，当向数组中指定位置插入一个新元素后，因为这时候会重新更新index索引，对应着后面的虚拟DOM的key值全部更新了，这个时候还是会做不必要的更新，就像没有加key一样，因此index虽然能够解决key不冲突的问题，但是并不能解决复用的情况。如果是静态数据，用索引号index做key值是没有问题的。

5. 标签名一样，key一样这时候就会就地复用，如果标签名不一样，key一样不会复用。

#### 如何让css样式只在当前组件起作用？


vue为每个组件都生成了一个data-v-xxxxx属性，然后生成scoped css的时候，自动把这个属性加到了样式表里面。从而使得css样式只对当前组件生效。

#### vue的几种指令操作
vue常用指令有：v-once指令、v-show指令、v-if指令、v-else指令、v-else-if指令、v-for指令、v-html指令、v-text指令、v-bind指令、v-on指令、v-model指令等等。
#### v-on可以监听多个方法吗？
**可以**
#### v-model双向绑定是怎么实现的？
v-model实现双向绑定的语法糖，常用于表单与组件之间的数据双向绑定.
##### 表单实现双向绑定
1. 原理 分两步骤 v-bind绑定一个value属性 v-on指令给当前元素绑定input事件 可看出v-model绑定在表单上时，v-model其实就是v-bind绑定value和v-on监听input事件的结合体

    ```JavaScript 
    v-model = v-bind:value + v-on:input
    ```
2. 实现 用v-bind:value + v-on:input来模拟实现v-model

<input type="text" :value="username" @input="username = $event.target.value" />

例子解释： 通过 v-bind:value 绑定 username 变量，每次输入内容的时候触发input事件 通过事件对象参数 event.target.value 获得输入的内容，并且把这个内容赋值给username 此时更改username时input输入框会变化，更改input输入框时username变量会变，从而实现了v-model的双向绑定功能
##### 组件上的双向绑定
原理：v-model绑定在组件上的时候做了以下步骤 在父组件内给子组件标签添加 v-model ，其实就是给子组件绑定了 value 属性 子组件内使用 prop 创建 创建 value 属性可以拿到父组件传递下来的值，名字必须是 value。 子组件内部更改 value 的时候，必须通过 $emit 派发一个 input 事件，并携最新的值 v-model 会自动监听 input 事件，把接收到的最新的值同步赋值到 v-model 绑定的变量上
#### 有没有写过自定义指令？
输入框防抖

防抖这种情况设置一个v-throttle自定义指令来实现
```js



// 1.设置v-throttle自定义指令
Vue.directive('throttle', {
  bind: (el, binding) => {
    let throttleTime = binding.value; // 防抖时间
    if (!throttleTime) { // 用户若不设置防抖时间，则默认2s
      throttleTime = 2000;
    }
    let cbFun;
    el.addEventListener('click', event => {
      if (!cbFun) { // 第一次执行
        cbFun = setTimeout(() => {
          cbFun = null;
        }, throttleTime);
      } else {
        event && event.stopImmediatePropagation();
      }
    }, true);
  },
});
// 2.为button标签设置v-throttle自定义指令
<button @click="sayHello" v-throttle>提交</button>
```



// 2.为button标签设置v-throttle自定义指令
```js
<button @click="sayHello" v-throttle>提交</button>
```
图片懒加载
#### 如何封装组件？ 封装组件要注意什么？
1、使用Vue.extend()创建一个组件

2、使用Vue.component()方法注册组件

3、如果子组件需要数据，可以在props中接收定义

4、子组件修改好数据之后，想把数据传递给父组件，可以用emit()方法
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

#### 选择器有哪些？优先级？
!import >行内选择器>id选择器>类选择器>标签选择器
#### 行内元素和块内元素区别和分类
##### 行内元素会
1. **在一行上**显示，当此行上剩余的空间无法承载当前的行内元素时，此行内元素才会在新的一行上显示。每个元素是水平排列的
2.行内元素设置width无效，height无效(可以设置line-height)，margin上下无效。块级元素都可以设置。

3. **每个**块级元素各占据一行。每个元素时竖直方向排列的。
4. 块级元素可以包含行内元素和块级元素，宽度默认100%，即和浏览器同宽。行内元素不能包含块级元素，宽度无法设置，只和包含的内容有关。
   

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
#### 如何理解vue的渐进式开发？
你可以在原有大系统的上面，把一两个组件改用它实现；也可以整个用它全家桶开发；还可以用它的视图，搭配你自己设计的整个下层用。它只是个轻量视图而已，只做了自己该做的事，没有做不该做的事，仅此而已。没有多做职责之外的事，只做了自己该做的事。
#### nexttick做了什么事情？
* nextTick所指定的回调会在浏览器更新DOM完毕之后再执行。
* Vue 在更新 DOM 时是异步执行的。只要侦听到数据变化，Vue 将开启一个队列，并缓冲在同一事件循环中发生的所有数据变更。如果同一个 watcher 被多次触发，只会被推入到队列中一次。这种在缓冲时去除重复数据对于避免不必要的计算和 DOM 操作是非常重要的。然后，在下一个的事件循环“tick”中，Vue 刷新队列并执行实际 (已去重的) 工作。Vue 在内部对异步队列尝试使用原生的 Promise.then、MutationObserver 和 setImmediate，如果执行环境不支持，则会采用 setTimeout(fn, 0)代替。
#### Vue中Scoped原理
https://blog.csdn.net/qq_51368103/article/details/124557999
#### react中的useState原理
https://blog.csdn.net/qq_30632003/article/details/124940407
#### async里面await了一个接口，后面有个console.log(1),为什么console.log会等待await后的执行完？
https://blog.csdn.net/weixin_41784648/article/details/108334512
#### 图片懒加载的实现方案
https://blog.csdn.net/darabiuz/article/details/123151266
#### 讲讲jwt
https://blog.csdn.net/weixin_44736637/article/details/124005231
#### localsotrage sessionstorage cooike 数据超过5m如何存储？
https://blog.csdn.net/m0_37756431/article/details/123536611
#### let const var区别
https://blog.csdn.net/qq_45799465/article/details/122892209
#### 事件循环  及事件动态渲染在什么时候？

#### 宏任务 微任务

#### 前端跨域产生的原因

#### flex常用属性

#### css居中方案

#### margin:0 auto;有什么条件？

#### 圣杯布局的实现

#### flex:1;具体是什么意思？

#### JS中的事件捕获？

#### JS中的继承？

#### 组件库的Button怎么写的？

#### v8垃圾回收机制

#### vue.config.js里面的devServer有什么作用？

#### vue响应式

#### getter和setter的作用

#### 数组常用(排序)的方法 数组sort方法返回值不能可能是？

#### 两栏布局

#### 前端存储数据方式

#### 用过哪些组件库

#### vue的双向绑定

#### vue3新特性

#### 节流跟防抖以及应用场景

#### 垂直居中

#### position有哪些属性？

#### 脱离文档流和不脱离文档流会有什么不同的表现

#### rem 及背后原理 rem和em区别？

#### src和href的区别

#### html5语义化

#### ！DOCTYPE

#### 盒子模型

#### BFC

#### 作用域和作用域链

#### 闭包

#### 基本数据类型和引用数据类型

#### arguments

####  深拷贝和浅拷贝

#### 虚拟DOM

#### computed和watch

#### hash和history路由

#### 页面的渲染过程

#### defer和aync

#### loder和plugin webpack常用配置 webpack可以直接打包图片吗？

#### 性能优化

#### tcp和udp

#### 数据变更但是界面没有变更是什么原因？

#### $set

#### vue2和vue3的区别 为什么vue3使用proxy，不再使用Object.defineProperty?

#### 子组件如何监听父组件中变动的数据

#### 如何判定类型: type instanceof Object.prototype.toString.call()

#### keep-alive

#### useState是同步还是异步？

#### react和vue的区别 (响应式、mvvm mvc 单向数据流)

#### 浏览器缓存

#### Dns缓存 强制缓存和协商缓存 （304的过程）

#### git rebase 和git merge区别？ 如何解决git冲突？

#### ts ,type和interface的区别

#### es6新增 es6的import时同步还是异步？

#### 常见的http状态码

#### axios二次封装的好处 axios的特点 拦截器怎么内部实现拦截？ token放哪？webscoket怎么握手？

#### 用户鉴权都的完整流程

#### 为什么要把token存在localstorage不存在cookie或者其他地方呢？

#### 项目中无限滚动怎么实现的   项目的权限？

#### 无限滚动的列表数据时追加还是覆盖

#### 列表数据很多的时候会导致我们的页面卡顿怎么解决

#### 移动端如何适配的？

#### 根元素的字体大小是怎么算出来的？

#### 项目中最复杂的功能？

#### 用过什么loder和plugin

#### loder的主要作用

#### 构建玩的文件带哈希值，这个哈希值有什么作用？

#### vue 和 jq接触过吗？

#### vuex里面的数据和全局变量有什么区别？

#### get和post的区别，哪个率先你会丢失数据？

####  flex-shrink的作用

#### DNS解析过程

#### proxy和reflect搭配使用，讲一下reflect？

#### vue3响应式原理里的weapMap

#### chunkhash和contenthash区别

#### 了解过热更新吗？

#### pnpm，pnpm对比npm的优势？

#### js哪些地方用到了栈？（执行上下文栈）

#### 类型拓宽？

#### 介绍下https

#### 给一个空数组或空对象怎么判断为空?

#### 写一个react受控组件

#### 写一个promiseall

#### css3动画怎么做？

#### redux如何传数据？怎么接数据？什么时候会用到redux

#### 中后台项目都很类似，怎么提高开发效率？

#### cancas和cvg了解过吗？

#### html语义化如何理解？

#### 有哪些方式有助于SEO

#### 工作中遇到问题怎么办？

#### session重复登录问题

#### 滚动列表优化？

#### js检测数据类型的方法

#### vue的基本原理 双向绑定的原理

#### vue3性能优化

#### 手写flat

#### 手写发布订阅模式once

#### 断点续传怎么做的？

#### 秒传怎么实现？

#### ts Partial Omit怎么实现的？

#### map和forEach对于对象会不会改变？

#### Map和Ojectd的区别?

#### 单页应用怎么跨页面传参？ 权限怎么设计的？

#### 项目中的懒加载怎么做到的？

#### html中开启了relative会导致什么问题？

#### js执行机制？

#### 浮动方式？

#### 判断数组的方法？

#### 改变this的方式

#### 先bing函数在call函数最后this指向哪一个?

#### 连续两次bind的this指向哪一个this？

#### Promise和Asyn await有什么区别？

#### 事件循环？

#### generte函数用过吗？

#### 说下缓冲 ？ 缓冲中cache-control使用过哪些属性？

#### http和https的区别？

#### 三次握手为啥不是两次和四次？

#### 虚拟DOM是什么？主要作用？

#### 改变state用什么方法？ setState可以传对象吗？

#### webpack打包过程？

#### if(0=="")判断转换过程？

#### a==1 && a==2 && a=3满足这个表达式的a

#### css垂直居中几种方法？

#### 复杂表单中的细节？

#### 杭