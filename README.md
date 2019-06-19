# web interview(vue)

# ES6
  1.新增了块级作用域(let,const)：
    var变量提升（变量在声明之前就可以使用，值为undefined），const和let作用在代码块，暂时性死区（在声明变量前变量不可用，抛错）
    let不能在同一作用域重新声明，const必须赋值初始化

  2.新增了一种基本数据类型(Symbol)
  
  3.模板字面量：
    `$(vv.kk) have big eyes` 等同于  vv.kk + 'have big eyes'

  4.变量解构赋值：
    const point=[0,3,6];const [x,y,z]=point

  5.for...of循环：循环value,更适合循环 Array
    用于循环访问任何可迭代的数据类型（String，Array，Map，Set)，不包括 Object
    如果实在想用for...of来遍历普通对象的属性的话，可以通过和Object.keys()搭配使用
    for...in 循环key，更适合循环 Object

  6.展开运算符(...)

  7.箭头函数

  8.新增了模块化(import/export)
  
  9.新增了Set和Map数据结构


# JS
  call，apply，bind：
    改变函数运行时上下文
    call()接收的是参数列表，而apply()则接收参数数组。
    bind()是返回一个新函数，供以后调用，而apply()和call()是立即调用。
    
  this：指向调用函数的对象
    new绑定
    显式绑定：apply/call；硬绑定bind，创建新函数，this指向函数的第一个参数
    隐式绑定：XXX.fn()，存在绑定丢失问题
    默认绑定
    *箭头函数没有自己的 this, 它的this继承于上一层代码块的this
    
  event-loop(事件循环)：主线程循环不断地从任务队列按顺序取任务执行
  
  sessionStorage 和 localStorage 操作方法：setItem、getItem 以及 removeItem
  
  阻止button自动刷新：
    将<button></button>改为<input type="button">
    click事件中加 e.preventDefult();
    
  闭包：
    有权访问另一个函数作用域中的变量的函数，创建闭包最常用的方式就是在一个函数内部创建另一个函数。
    缺点：导致函数的变量一直保存在内存中，过多的闭包可能会导致内存泄漏
    
  *深拷贝浅拷贝：针对复杂数据类型
    深拷贝：复制变量值，对于非基本类型则递归至基本类型变量再复制，互不影响
    浅拷贝：复制对象属性，当对象属性是引用时，复制引用，当引用指向的值改变时也会跟着变化
    深拷贝最简单的实现是: JSON.parse(JSON.stringify(obj))，对象的属性值是函数时，无法拷贝
    
  防抖，节流：防止函数的多次调用
    防抖：n秒内函数只会执行一次，如果n秒内高频事件再次被触发，则重新计算时间（文本输入验证）
    节流：高频事件在规定时间内只会执行一次，执行一次后，只有大于设定的执行周期后才会执行第二次（拖拽）
    
  promise对象：解决回调地狱
    “承诺将来会执行”的对象，最大的好处是在异步执行的流程中，把执行代码和处理结果的代码清晰地分离了
    JS中所有代码单向执行，导致JavaScript的所有网络操作，浏览器事件，都必须是异步执行（回调）
      new Promise(test).then(function (result) {
          console.log('成功：' + result);
      }).catch(function (reason) {
          console.log('失败：' + reason);
      });
  Promise 是微任务，setTimeout 是宏任务，同一个事件循环中，promise.then总是先于 setTimeout 执行。
  
  async/await:是 Generator 的语法糖，使得异步操作变得更加方便，返回值是Promise
    async（异步）：作为关键字放在函数前，表明函数是异步函数，意味着该函数的执行不会阻塞后面代码的执行
      返回promise对象，要获取返回值，要用then方法
        async function timeout() {
          return 'hello world'
      }
      timeout().then(result => {
          console.log(result);
      })
      console.log('虽然在后面，但是我先执行');
      
      输出：
        虽然在后面，但是我先执行
        hello world
        
  *跨域：一是前端和服务器分开部署，接口请求需要跨域，二是我们可能会加载其它网站的页面作为iframe内嵌。
    1.jsonp： <script> 标签的 src 属性不会被同源策略所约，只支持get请求
    2.cors：服务器设置的Access-Control-Allow-Origin Header和请求来源匹配
    3.nginx反向代理
    4.WebSocket
    5.window.postMessage方法，允许跨窗口通信，不论这两个窗口是否同源。
  
  继承：主要是由原型链实现的
    1.prototype
    2.借用构造函数（call，apply）
    3.组合继承
    4.原型式继承　　
    5.寄生式继承
    6.寄生组合式继承
    
  柯里化（currying）：局部套用，只传递给函数一部分参数来调用它，让它返回一个函数去处理剩下的参数。
    bind的实现机制就是currying
    好处：1.参数复用，调用方便
         2.提前确认
         3.延迟运行
         
  Array.prototype.slice.call()方法：能够将一个具有length属性的对象转换为数组
  
  iframe缺点：1.会产生很多页面，不容易管理。
             2.代码复杂，不利于搜索引擎优化
             3.很多的移动设备（PDA 手机）无法完全显示框架，设备兼容性差
             4.增加服务器的http请求


# Vue
  UTC时间格式转标准时间：安装moment.js
  
  *生命周期（钩子）：创建前后（created），挂载前后（mounted），更新前后（updated），销毁前后（destroy）
  
  双向绑定原理：Vue内部通过Object.defineProperty方法属性拦截的方式，把data对象里每个数据的读写转化成getter/setter，当数据变化时通知视图更新
    ES中有两种属性: 数据属性和访问器属性,
    数据属性：一般用于存储数据数值
    访问器属性：对应的是set/get操作, 不能直接存储数据值
    Object.defineProperty()：这个方法接收三个参数: 属性所在对象, 属性的名字, 描述符对象;通过get()，set()拦截
    let car = {}
    let val = 3000
    Object.defineProperty(car, 'price', {
        get(){
            console.log('price属性被读取了')
            return val
        },
        set(newVal){
            console.log('price属性被修改了')
            val = newVal
        }
    })
    car.price // price属性被读取了  3000
    car.price=5000 //price属性被修改了  5000
     
   *实现数据的双向绑定，首先要对数据进行劫持监听，所以我们需要设置一个监听器Observer，用来监听所有属性。如果属性发上变化了，就需要告诉订阅者Watcher看是否需要更新。因为订阅者是有很多个，所以我们需要有一个消息订阅器Dep来专门收集这些订阅者，然后在监听器Observer和订阅者Watcher之间进行统一管理。
   
   父子传值：vuex，$emit
   
   
# Vuex（Vue状态管理）
  核心：仓库store，包含着你的应用中大部分的状态 (state)。
  
  与全局对象不同：1.Vuex的存储状态是响应式的
               2.不能直接改变 store 中的状态。改变 store 中的状态的唯一途径就是显式地提交 (commit) mutation
               
  Vuex 使用单一状态树，从 store 实例中读取状态最简单的方法就是在计算属性中返回某个状态
  1.State
  2.Getter: 可以认为是 store 的计算属性
  3.Mutation: 每个 mutation 都有一个字符串的 事件类型 (type) 和 一个 回调函数 (handler)。这个回调函数就是我们实际进行状态更改的地方，并且它会接受 state 作为第一个参数
  4.Action: 类似于 mutation，但Action 提交的是 mutation，而不是直接变更状态；可以包含任意异步操作。异步逻辑都应该封装到 action 里面
  5.Module: 将 store 分割成模块（module）防止臃肿。每个模块拥有自己的 state、mutation、action、getter
  
  
# Vue React 对比
  都使用'Virtual DOM'（虚拟DOM，是一个映射真实DOM的JS对象，当有变化产生时，一个新的VD会被创建并计算与旧的的差别，然后将差别应用在真实DOM上），React是JSX（JSX是使用xml语法编写javascript的一种语法糖），Vue是模板语法。
  
  mvvm即是model-view-viewmodel，model和view之间的衔接交互都是通过viewmodel来实现的。viewmodel就是创建一个vue实例，vue实例是作用于某一个dom元素上的。
  
  都是单项数据流，但是都可以进行 双向数据绑定
  提供了响应式和组件化的视图组件，都有脚手架（vuex，vue-router|react-router,react-redux），都有构建工具（vue-cli,Create React App (CRA))
  Vue：在渲染过程中，会跟踪每一个组件的依赖关系，不需要重新渲染整个组件树。
  React：当应用的状态被改变时，全部子组件都会重新渲染。可以通过shouldComponentUpdate这个生命周期方法来进行控制
  
  
# CSS
  盒模型：box-sizing: border-box（整个div宽高包括margin，border，padding）；content-box（不包括上述）
  
  单位：em（相对于父元素font-size）；rem（相对于根元素font-size）；rpx（小程序相对单位，1rpx = 屏幕宽度 / 750 px）
  
  选择器：#ID  .class
  
  *水平垂直居中：
    1.flex布局：弹性布局
    父：
      display: flex;
      /* 实现元素水平居中 */
      justify-content: center;
      /* 实现元素垂直居中 */
      align-items: center;
    2.margin: auto;
    
  水平居中：
    行内元素：display: inline-block; text-align: center;
    块级元素：margin: 0 auto;
    父 display: flex; justify-content: center;
    
  垂直居中：
    行高 = 元素高：line-height: height（盒模型，computed height）
    父 display: flex; align-items: center;
    absolute + transform
    行内元素：display: inline-block; text-align: center;
    
  CSS预处理器：变量 / 嵌套 / 自动前缀 / 条件语句 / 循环语句
  
  rem布局：通过js修改根元素的大小，达到整个页面的缩放。
  
  BFC(Block Fromatting Context)：块级格式上下文；是一个独立的布局环境，其中的元素布局是不受外界的影响
    创建条件：1、float的值不是none。
            2、position的值不是static或者relative。
            3、display的值是inline-block、table-cell、flex、table-caption或者inline-flex
            4、overflow的值不是visible
    用途：1、避免外边距折叠 ：BFC产生外边距折叠要满足一个条件：两个相邻元素要处于同一个BFC中。所以，若两个相邻元素在不同的BFC中，就能避免外边距折叠。
         2、包含浮动
         3、避免文字环绕
         
  三栏布局
  
  LESS：CSS预处理语言，动态 css 语言，使得css样式灵活作用于 html 标签，提高样式代码的可维护性
    less.js的作用就是编译 .less 文件，使它成为浏览器能读懂的 css 样式；
    在引用less.js之前，需要一个less变量，声明编译less的环境参数，less变量的声明必须要在less.js的引用之前
    变量计算，变量混合（继承，带参），嵌套，函数，条件判断，变量作用域，import

         
# 浏览器
   输入url到展示页面过程发生了什么？
     1.域名解析：DNS协议通过域名查找IP地址，域名解析就是在DNS记录一条信息记录
     2.建立TCP连接：三次握手，目的：为了防止已失效的连接请求报文段突然又传送到了服务端，从而产生错误
     3.发起http请求：请求报文由三部分组成：请求行，请求报头和空白行+请求正文
     4.服务器响应http请求：响应报文由三部分组成：响应行，响应报头和响应报文
     5.浏览器渲染页面：dom树，css规则树，渲染树（重排和重绘），根据渲染树计算每个节点信息，绘制页面，JS解析（一个主线程+一个任务队列）
     6.断开连接：TCP四次挥手
     
     
# 性能优化
  DOM操作太多:
      1. 合并多次的DOM操作为单次的DOM操作
      2. 设置具有动画效果的DOM元素的position属性为fixed或absolute
      3. 使用事件托管方式绑定事件
  
      
  性能检测：
      1.Performance API：使用浏览器提供的 window.performance 对象
      2.Profile工具：用于测试页面脚本运行时系统内存和CPU资源占用情况的API
      

# 算法
  遍历二叉树：前序遍历、中序遍历、后序遍历
  
  二分法查找：
    function getIndex(arr,num){
      var len = arr.length,
          st  = 0,
          end = len-1
          while(st<=end){
          var mid = Math.floor((st+end)/2)  //向下取整
          if(num==arr[mid]){
              return mid
          }else if(num>arr[mid]){
              st = mid+1
          }else{
              end = mid-1
          }
      }
      return arr;
    }
    
  冒泡排序：
    function bubbleSort(arr) {
      var len = arr.length;
      for (var i = 0; i < len; i++) {
          for (var j = 0; j < len - 1 - i; j++) {
              if (arr[j] > arr[j+1]) {        //相邻元素两两对比
                  var temp = arr[j+1];        //元素交换
                  arr[j+1] = arr[j];
                  arr[j] = temp;
              }
          }
      }
      return arr;
    }
    
    
    
    
    
