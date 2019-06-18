# Interview
  web interview(vue)

# ES6
  const 与 let:
    var变量提升，const和let作用在代码块，
    let不能在同一作用域重新声明，const必须赋值初始化

  模板字面量：
    `$(vv.kk) have big eyes` 等同于  vv.kk + 'have big eyes'

  解构：
    const point=[0,3,6];const [x,y,z]=point

  for...of循环：
    用于循环访问任何可迭代的数据类型（String，Array，Map，Set)，不包括Object

  展开运算符(...)

  箭头函数

  super和extends

# JS
  this：指向调用函数的对象
    new绑定
    显式绑定：apply，call，硬绑定bind
    隐式绑定：XXX.fn()，绑定丢失
    默认绑定 
  event-loop(事件循环)：主线程循环不断地从任务队列按顺序取任务执行
  阻止button自动刷新：
    将<button></button>改为<input type="button">
    click事件中加 e.preventDefult();

# Vue
  UTC时间格式转标准时间：安装moment.js
  生命周期（钩子）：初始化，运行中，销毁时
  
  
# Vue React 对比
  都使用'Virtual DOM'（虚拟DOM，是一个映射真实DOM的JS对象，当有变化产生时，一个新的VD会被创建并计算与旧的的差别，然后将差别应用在真实DOM上），React是JSX（JSX是使用xml语法编写javascript的一种语法糖），Vue是模板语法。
  mvvm即是model-view-viewmodel，model和view之间的衔接交互都是通过viewmodel来实现的。viewmodel就是创建一个vue实例，vue实例是作用于某一个dom元素上的。
  提供了响应式和组件化的视图组件，都有脚手架（vuex，vue-router|react-router,react-redux），都有构建工具（vue-cli,Create React App (CRA))
  Vue：在渲染过程中，会跟踪每一个组件的依赖关系，不需要重新渲染整个组件树。
  React：当应用的状态被改变时，全部子组件都会重新渲染。可以通过shouldComponentUpdate这个生命周期方法来进行控制
  
