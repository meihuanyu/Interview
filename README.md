# Interview
  web interview(vue)

# ES6
  1.新增了块级作用域(let,const)：
    var变量提升（变量在声明之前就可以使用，值为undefined），const和let作用在代码块，暂时性死区（在声明变量前变量不可用，抛错）
    let不能在同一作用域重新声明，const必须赋值初始化

  2.新增了一种基本数据类型(Symbol)
  
  3.模板字面量：
    `$(vv.kk) have big eyes` 等同于  vv.kk + 'have big eyes'

  4.变量解构赋值：
    const point=[0,3,6];const [x,y,z]=point

  5.for...of循环：
    用于循环访问任何可迭代的数据类型（String，Array，Map，Set)，不包括Object

  6.展开运算符(...)

  7.箭头函数

  8.新增了模块化(import/export)
  
  9.新增了Set和Map数据结构

# JS
  this：指向调用函数的对象
    new绑定
    显式绑定：apply/call，两者传参不同，apply的第二个参数是数组或类数组。硬绑定bind，创建新函数，this指向函数的第一个参数
    隐式绑定：XXX.fn()，存在绑定丢失问题
    默认绑定
    *箭头函数没有自己的 this, 它的this继承于上一层代码块的this
    
  event-loop(事件循环)：主线程循环不断地从任务队列按顺序取任务执行
  
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
      ---------------------------------------
      输出：
        虽然在后面，但是我先执行
        hello world

# Vue
  UTC时间格式转标准时间：安装moment.js
  *生命周期（钩子）：初始化，运行中，销毁时
  
  
# Vue React 对比
  都使用'Virtual DOM'（虚拟DOM，是一个映射真实DOM的JS对象，当有变化产生时，一个新的VD会被创建并计算与旧的的差别，然后将差别应用在真实DOM上），React是JSX（JSX是使用xml语法编写javascript的一种语法糖），Vue是模板语法。
  mvvm即是model-view-viewmodel，model和view之间的衔接交互都是通过viewmodel来实现的。viewmodel就是创建一个vue实例，vue实例是作用于某一个dom元素上的。
  都是单项数据流，但是都可以进行 双向数据绑定
  提供了响应式和组件化的视图组件，都有脚手架（vuex，vue-router|react-router,react-redux），都有构建工具（vue-cli,Create React App (CRA))
  Vue：在渲染过程中，会跟踪每一个组件的依赖关系，不需要重新渲染整个组件树。
  React：当应用的状态被改变时，全部子组件都会重新渲染。可以通过shouldComponentUpdate这个生命周期方法来进行控制
  
