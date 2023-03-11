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
#### vue路由模式以及实现原理
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

#### action和mutation有什么区别？
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
#### v-show和v-if
##### 不同点
1. v-show：相当于dispaly:none;  频繁切换使用v-show 有更高的初始渲染消耗
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
2. 
   ```JavaScript 
    v-model = v-bind:value + v-on:input
    ```
4. 实现 用v-bind:value + v-on:input来模拟实现v-model

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

#### 如何理解vue的渐进式开发？
你可以在原有大系统的上面，把一两个组件改用它实现；也可以整个用它全家桶开发；还可以用它的视图，搭配你自己设计的整个下层用。它只是个轻量视图而已，只做了自己该做的事，没有做不该做的事，仅此而已。没有多做职责之外的事，只做了自己该做的事。
#### nexttick做了什么事情？
* nextTick所指定的回调会在浏览器更新DOM完毕之后再执行。
* Vue 在更新 DOM 时是异步执行的。只要侦听到数据变化，Vue 将开启一个队列，并缓冲在同一事件循环中发生的所有数据变更。如果同一个 watcher 被多次触发，只会被推入到队列中一次。这种在缓冲时去除重复数据对于避免不必要的计算和 DOM 操作是非常重要的。然后，在下一个的事件循环“tick”中，Vue 刷新队列并执行实际 (已去重的) 工作。Vue 在内部对异步队列尝试使用原生的 Promise.then、MutationObserver 和 setImmediate，如果执行环境不支持，则会采用 setTimeout(fn, 0)代替。
#### Vue中Scoped原理
https://blog.csdn.net/qq_51368103/article/details/124557999

#### 组件库的Button怎么写的？
https://zhuanlan.zhihu.com/p/560488554
#### vue.config.js里面的devServer有什么作用？
配置跨域
#### vue响应式
https://blog.csdn.net/weixin_48181168/article/details/120158346
#### getter和setter的作用
https://blog.csdn.net/weixin_48873376/article/details/108037944
#### 用过哪些组件库

#### vue3新特性
https://blog.csdn.net/jiang_ziY/article/details/123930027
#### 虚拟DOM 主要作用？
https://blog.csdn.net/yiyueqinghui/article/details/105468012
#### computed和watch
https://blog.csdn.net/m0_62118859/article/details/124455926
#### hash和history路由
https://blog.csdn.net/zj695133626/article/details/121107628
#### 数据变更但是界面没有变更是什么原因？
https://blog.csdn.net/weixin_47220950/article/details/116277828
#### $set
Vue.set(ttudent,'sex','男')
this.$set(ttudent,'sex','男')
https://blog.csdn.net/qq_45851085/article/details/125064876
#### vue2和vue3的区别
https://blog.csdn.net/weixin_54722719/article/details/123069837
####  为什么vue3使用proxy，不再使用Object.defineProperty?
https://blog.csdn.net/qq_39765048/article/details/121117167
#### 子组件如何监听父组件中变动的数据
https://blog.csdn.net/mouday/article/details/109910429
#### keep-alive
https://blog.csdn.net/ZYS10000/article/details/122480733
#### axios二次封装的好处 
* 二次封装axios主要是为了用到请求拦截器和响应拦截器
* 拦截请求：可以在请求之前处理一些业务(比如为每个请求带上相应的参数，时间戳等）
* 拦截响应：可以在服务器返回数据之后处理一些事情（比如对返回的状态进行判断，token是否过期等）

#### axios的特点 
（1）axios 是一个基于promise的HTTP库，支持promise所有的API

（2）浏览器端/node端（服务器端）都可以使用，浏览器中创建XMLHttpRequests

（3）支持请求／响应拦截器

（4）它可以转换请求数据和响应数据，并对响应回来的内容自动转换成 JSON类型的数据

（5）批量发送多个请求

（6）安全性更高，客户端支持防御XSRF

#### 拦截器怎么内部实现拦截？
https://blog.csdn.net/hannah2233/article/details/126646242

#### token放哪？
https://blog.csdn.net/ZDM_9999/article/details/128010403
#### vue 和 jq接触过吗？
http://www.gaodaima.com/69127.html
#### vuex里面的数据和全局变量有什么区别
vuex优点：
1、vuex的存储时响应式的，当组件vue中store更改，相应的组件用到的地方也会高效的更新
2、不能直接改变store里面的变量，需要通过dispatch调用action,然后action去commit（mutation），mutation会操作store里面的值，进行数据的改变
对比vuex和全局变量：
1、vuex做的就是状态管理，主要时管理状态的一个库，把项目中公用的一些数据进行存储，某一个组件更改了vuex中的数据，其他相关的组件也会得到快速更新，但是全局变量可以任意修改，不是很安全
2、全局变量可能操作命名污染，但是vuex不会，每个组件可以根据自己vuex的变量名引用不受影响
3、vuex处理项目负责，嵌套关系复杂的项目效果很明显，针对于demo或者小项目，全局变量也就够用了

#### proxy和reflect搭配使用，讲一下reflect？

#### vue3响应式原理里的weapMap

#### vue3性能优化
https://blog.csdn.net/qq_40434213/article/details/119896193
#### vue中后端没有给key怎么办？

#### vue视图是同步更新的吗？我想立刻拿到更新后的数据怎么办？
不是  解决方法： vm.$nextTick(() => { // …})
#### vue怎么更改data中的数据

#### vue2的data为什么写成函数形式
目的是为了防止多个组件实例对象之间共用一个data，产生数据污染。采用函数的形式，initData时会将其作为工厂函数都会返回全新data对象，有效规避多实例之间状态污染问题。
#### 写项目过程中怎么解决数据不同步更新

#### v-for遍历能否key做数组下标？vue2的动态数据是用es6的proxy？

#### 如何调试Vue、H5
vue用Vue-devtools H5用debugger

#### 为什么许多人用vue不用原生js？
**vue优点：**
1. 数据的自动绑定
2. 页面参数传递和页面状态管理。
3. 模块化开发、无刷新保留场景参数更新
4. 代码的可阅读性（模块化开发带来的）
5. 基于强大的nodejs，拥有npm包管理器，可以很好滴管理包的版本
6. 各子组件样式不冲突
7. 视图,数据,结构分离
8. 虚拟dom
9. 各种指令;过滤器
vue缺点：
* vue是单页面页面，对于搜索引擎不友好，影响seo。比如两个vue路由（页面），它的路径是这样的：index.html#aaa 和 index.html#bbb，但对于搜索引擎来说，都是同一个页面，就是index.html。这样搜索引擎就无法收录你的页面。
#### 插件 混入
#### vue底层源码的实现

#### setup介绍一下？ setup在beforecreate执行一次？

#### setup能拿到组件实例吗、能拿到this吗？

#### vue打包时怎么能让他自动识别时开发模式还是其他？

