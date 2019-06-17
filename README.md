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
