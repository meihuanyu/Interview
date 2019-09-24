# 阿里

# 如何看待前端框架选型

react用的是jsx，更接近原生js，vue是模板语法，有一些方便的指令，
react是单项数据流，vue是双向绑定

Angular、 React、Vue是目前三大主流的前端框架，
这三个框架都有很好的性能(这里的angular指的是2.0+)，都支持数据绑定，组件等基本功能。
angular （依赖注入）
生态系统庞大 良好的项目结构 缺乏灵活性 体积较大（2之后用了AOT和treeshaking）但还是略显臃肿 加载较慢 学习成本高，api复杂
react
灵活 生态圈强大 学习成本一般JSX和ES6  跨平台优势和生态优势大于vue。
vue
灵活 实用（数据绑定，计算属性侦听，组件） 易上手 体积小
react和vue只关注视图层，这跟angular有本质的区别，如果react想开发大型应用需要配合第三方库

如何选择：
超大型选angular（深度整合ts和rxjs，Ts解决了工程化问题，rxjs解决了开发速度问题）
个性化中型选react（适合渐进式添加模块，适合快速发展迭代）
小型应用选vue（数据源稳定，对运营要求不高，但对加载速度高要求。对象式的声明在UI实现上速度更快）

# vue如何实现双向绑定
数据劫持 结合 发布者-订阅者模式 的方式来实现的
实现mvvm主要包含两个方面，数据(data)变化更新视图(view)，视图变化更新数据
view更新data：通过事件监听即可
data更新view：通过Object.defineProperty( )对属性设置一个set函数，当数据改变了就会来触发这个函数，所以我们只要将一些需要更新的方法放在这里面就可以实现data更新view了。
var Book = {}
var name = ''
Object.defineProperty(Book,'name',{
	set: function (value) {
		name = value ;
		console.log(value)
	},
	get: function(){
		return name
	}
})

自己实现数据的双向绑定：https://juejin.im/entry/5923973da22b9d005893805a

# react 虚拟DOM 是什么? 如何实现? 说一下diff算法 ?
虚拟DOM就是使用javascript对象来表示真实DOM，是一个树形结构，只保留了真实DOM节点的一些基本属性，和节点之间的层次关系。
在真实DOM中，一个普通的div打印出来也是很复杂的，所以浏览器处理DOM结构会比较慢，操作js对象更加方便快速
虚拟DOM相当于建立在javascript和DOM之间的一层“缓存”，可以类比CPU和硬盘：硬盘的读写速度是很慢的，相比较于廉价的内存来说。

React需要同时维护两棵虚拟DOM树：一棵表示当前的DOM结构，另一棵在React状态变更将要重新渲染时生成。React通过比较这两棵树的差异，决定是否需要修改DOM结构，以及如何修改。这种算法称作Diff算法。
Diff算法会对新旧两棵树做深度优先遍历，避免对两棵树做完全比较，因此算法复杂度可以达到O(n)。然后给每个节点生成一个唯一的标志
在遍历的过程中，每遍历到一个节点，就将新旧两棵树作比较，并且只对同一级别的元素进行比较
将虚拟DOM转换成实际DOM树的最少操作过程称为调和，diff算法就是调和的具体实现。
  Tree diff：新旧两颗DOM树逐层进行对比的过程就是tree diff；当整颗DOM树逐层对比完毕，则所需要被按需更新的元素必然能够找到；
  Component diff：在进行Tree diff的时候，每一层中组件级别的对比，叫做component diff；如果对比前后组件类型相同则暂时认为此组件不需要被更新；如果对比前后组件类型不同则需要移除就组件创建新组件，并追加到页面上；
  Element diff：在进行组件对比时，如果两个组件类型相同，则需要进行元素级别的对比，叫做element diff；
React 支持 key 属性。当子元素拥有 key 时，React 使用 key 来匹配原有树上的子元素以及最新树上的子元素。以下例子在新增 key 之后使得之前的低效转换变得高效：key在列表中应当具有唯一性，但不需要全局唯一

# vue组件通信方式：https://juejin.im/post/5cde0b43f265da03867e78d3
注：组件中的数据共有三种形式：data、props、computed
	父子通信：
父向子传递数据是通过 props，子向父是通过 events（$emit）；通过父链 / 子链也可以通信（$parent / $children）；ref 也可以访问组件实例；provide / inject API；$attrs/$listeners

	兄弟通信：eventBus；Vuex

	跨级通信：event
Bus；Vuex；provide / inject API、$attrs/$listeners


方法一、props/$emit（事件）

方法二、$emit/$on（事件车eventbus），用它来触发事件和监听事件,巧妙而轻量地实现了任何组件间的通信，包括父子、兄弟、跨级
	vue：实例化一个空的 Vue 实例，就是创建一个js文件,默认导出一个vue实例
		import vue from 'vue';
 		export default new vue();
	分发事件：bus.$emit(eventName,res);
	监听事件：bus.$on(eventName,res => {//do something});
	销毁监听：bus.$off(eventName);

方法三、VueX：实现了一个单向数据流，在全局拥有一个State存放数据，当组件要更改State中的数据时，必须通过Mutation进行，Mutation同时提供了订阅者模式供外部插件调用获取State数据的更新。而当所有异步操作(常见于调用后端接口异步获取更新数据)或批量的同步操作需要走Action，但Action也是无法直接修改State的，还是需要通过Mutation来修改State的数据。最后，根据State的变化，渲染到视图上。
	Vue Components：Vue组件。HTML页面上，负责接收用户操作等交互行为，执行dispatch方法触发对应action进行回应。
	state：页面状态管理容器对象。集中存储Vue components中data对象的零散数据，全局唯一，以进行统一的状态管理。
	getters：state对象读取方法。Vue Components通过该方法读取全局state对象。
	mutations：状态改变操作方法，由actions中的commit('mutation 名称')来触发。是Vuex修改state的唯一推荐方法。该方法只能进行同步操作，且方法名只能全局唯一。操作之中会有一些hook暴露出来，以进行state的监控等。
	commit：状态改变提交操作方法。对mutation进行提交，是唯一能执行mutation的方法。
	actions：操作行为处理模块,由组件中的$store.dispatch('action 名称', data1)来触发。然后由commit()来触发mutation的调用 , 间接更新 state。负责处理Vue Components接收到的所有交互行为。包含同步/异步操作，支持多个同名方法，按照注册的顺序依次触发。向后台API请求的操作就在这个模块中进行，包括触发其他action以及提交mutation的操作。该模块提供了Promise的封装，以支持action的链式触发。
	dispatch：操作行为触发方法，是唯一能执行action的方法。

方法四、$attrs/$listeners：如果仅仅是传递数据而不做中间处理，使用 vuex 处理未免有点大材小用。Vue2.4 版本提供了$attrs/$listeners

方法五、provide/inject：Vue2.2.0新增API，祖先组件中通过provider来提供变量，然后在子孙组件中通过inject来注入变量

方法六、$parent / $children与 ref：无法在跨级或兄弟间通信
	ref：如果在普通的 DOM 元素上使用，引用指向的就是 DOM 元素；如果用在子组件上，引用就指向组件实例
	$parent / $children：访问父 / 子实例
	使用$parent可以实现兄弟组件间的通信，只要兄弟组件都有ref属性

# react组件通信
非嵌套组件之间通信：
方法一、利用二者共同父组件的 context 对象进行通信
如果采用组件间共同的父级来进行中转，会增加子组件和父组件之间的耦合度，如果组件层次较深的话，找到二者公共的父组件不是一件容易的事，当然还是那句话，也不是不可以...

方法二、使用事件订阅（npm install events -S）
这里我们采用自定义事件的方式来实现非嵌套组件间的通信。自定义事件是典型的发布/订阅模式，通过注册和触发事件来实现组件间通信。
	import { EventEmitter } from 'events'
	const emitter = new EventEmitter()

父向子组件通信：传递props，子组件得到props后进行相应的处理。
子向父组件通信：利用回调函数，可以实现子组件向父组件通信：父组件将一个函数作为 props 传递给子组件，子组件调用该回调函数，便可以向父组件通信。

跨级组件之间通信：
方法一、中间组件层层传递 props
如果父组件结构较深，那么中间的每一层组件都要去传递 props，增加了复杂度，并且这些 props 并不是这些中间组件自己所需要的。不过这种方式也是可行的，当组件层次在三层以内可以采用这种方式，当组件嵌套过深时，采用这种方式就需要斟酌了。

方法二、使用 context 对象
context 相当于一个全局变量，是一个大容器，我们可以把要通信的内容放在这个容器中，这样一来，不管嵌套有多深，都可以随意取用。
使用 Context 的注意点：
	每个 Context 对象都会返回一个 Provider React 组件
	只有当组件所处的树中没有匹配到 Provider 时，其 defaultValue 参数才会生效,默认值为 undefined
	多个 Provider 也可以嵌套使用，里层的会覆盖外层的数据 Provider 接收一个 value 属性，传递给消费组件(React 会往上找到最近的 Provider，然后使用它的值)
	可以在任何生命周期中访问到，包括 render 函数中
  
# npm install都干啥了
其实我们在npm install的时候首先会下载对应资源包的压缩包放在用户目录下的.npm文件夹下，然后解压到项目的node_modules中，并且提取依赖包中指定的bin文件，在linux下会创建一条软连接，所以在linux下我们真正执行的是.bin文件夹下文件指向的文件
如果你希望，一个模块不管是否安装过， npm 都要强制重新安装，可以使用 -f 或 --force 参数
npm install 默认会安装 dependencies（生产环境） 字段和 devDependencies （开发环境）字段中的所有模块
如果使用 --production 参数，可以只安装 dependencies 字段的模块。

# 如何实现水平垂直居中？
flex布局：父元素设置display：flex；并设置align-items：center；justify-content：center
margin：auto；定位上下左右为0；可以实现拖标的居中
tabel-cell：父元素设置display：tabel-cell；并设置vertical-align：middle

# css 隐藏组件，有什么区别？
display：none和visible：hidden
display：none不分配物理空间；visible：hidden分配物理空间
刚刚百度还有方法是设置透明度opacity：0


# css3新特性
过渡：
	transition： CSS属性，花费时间，效果曲线(默认ease)，延迟时间(默认0)
	transition-property: width;
	transition-duration: 1s;
	transition-timing-function: linear;
	transition-delay: 2s;
动画：
	animation：动画名称，一个周期花费时间，运动曲线（默认ease），动画延迟（默认0），播放次数（默认1），是否反向播放动画（默认normal），是否暂停动画（默认running）
形状转换：
	transform:适用于2D或3D转换的元素
	transform-origin：转换元素的位置（围绕那个点进行转换）。默认(x,y,z)：(50%,50%,0)
阴影：
	box-shadow: 水平阴影的位置 垂直阴影的位置 模糊距离 阴影的大小 阴影的颜色 阴影开始方向（默认是从里往外，设置inset就是从外往里）;
图片边框：
	border-image: 图片url 图像边界向内偏移 图像边界的宽度(默认为边框的宽度) 用于指定在边框外部绘制偏移的量（默认0） 铺满方式--重复（repeat）、拉伸（stretch）或铺满（round）（默认：拉伸（stretch））
圆角边框：
	border-radius: n1,n2,n3,n4;
	border-radius: n1,n2,n3,n4/n1,n2,n3,n4;
	/*n1-n4四个值的顺序是：左上角，右上角，右下角，左下角。*/
渐变：gradient
滤镜：Filter
布局：弹性（flex）、栅格（grid）、多列（column-count）
媒体查询：
  <meta charset="utf-8"> 监听屏幕尺寸的变化，在不同尺寸的时候显示不同的样式
  <meta> 元素表示那些不能由其它HTML元相关元素之一表示的任何元数据信息，它可以告诉浏览器如何解析页面。
	我们可以借助<meta>元素的viewport来帮助我们设置视口、缩放等，从而让移动端得到更好的展示效果。
  <meta name="viewport" 
    content="
    width=device-width; //正整数或device-width，以px为单位，定义布局视口宽度
    height=device-height; //正整数或device-height，以px为单位，定义布局视口高度
    initial-scale=1;//0.0-10.0，定义页面初始缩放比例
    maximum-scale=1; //0.0-10.0，定义缩放的最大值，必须大于等于minimum-scale
    minimum-scale=1; //0.0-10.0，定义缩放最小值，必须小于等于maximum-scale
    user-scalable=no;"//yes或no，设为no则用户不能缩放网页，默认yes
	>
  
# 移动端适配方案
方案一、 rem布局
本质是等比缩放，以根节点的字体大小作为基准值进行长度计算
rem是基于html元素的字体大小来决定，而em则根据使用它的元素的大小决定
问题：
	rem 在默认字体不是 16px 的情况下有误差，1rem = 1 * (htmlFontSize / 16) * defaultFontSize，在系统设置的字体大小发生改变时，defaultFontSize 会跟着改变，而 16 不会变化。所以方案3虽然表面上不考虑默认字体大小的变化，只关注屏幕与设计稿之间的宽度比，但在实际计算中还是使用到了默认字体大小，而且还有一个不变的 16 在作祟
	字体大小并不能使用rem，可以通过修改body字体的大小来实现，同时所有设置字体大小的地方都是用em单位，对就是em，因为只有em才能实现，同步变化

方案二：vh、vw方案
将视觉视口宽度 window.innerWidth和视觉视口高度 window.innerHeight 等分为 100 份。
vw(Viewport's width)：1vw等于视觉视口的1%
vh(Viewport's height) :1vh 为视觉视口高度的1%
vmin :  vw 和 vh 中的较小值
vmax : 选取 vw 和 vh 中的较大值
vw同样有一定的缺陷：
px转换成vw不一定能完全整除，因此有一定的像素差。
比如当容器使用vw，margin采用px时，很容易造成整体宽度超过100vw，从而影响布局效果。当然我们也是可以避免的，例如使用padding代替margin，结合calc()函数使用等等...

JS检测横屏：window.orientation:获取屏幕旋转方向
	window.orientation === 180 || window.orientation === 0 //竖屏
	window.orientation === 90 || window.orientation === -90//横屏
在系统设置的字体大小发生改变时，defaultFontSize 会跟着改变，而 16 不会变化。

# 获取浏览器大小的api
window.innerHeight：获取浏览器视觉视口高度（包括垂直滚动条）。
window.outerHeight：获取浏览器窗口外部的高度。表示整个浏览器窗口的高度，包括侧边栏、窗口镶边和调正窗口大小的边框。
window.screen.Height：获取获屏幕取理想视口高度，这个数值是固定的，设备的分辨率/设备像素比
window.screen.availHeight：浏览器窗口可用的高度。
document.documentElement.clientHeight：获取浏览器布局视口高度，包括内边距，但不包括垂直滚动条、边框和外边距。
document.documentElement.offsetHeight：包括内边距、滚动条、边框和外边距。
document.documentElement.scrollHeight：在不使用滚动条的情况下适合视口中的所有内容所需的最小宽度。测量方式与clientHeight相同：它包含元素的内边距，但不包括边框，外边距或垂直滚动条。
