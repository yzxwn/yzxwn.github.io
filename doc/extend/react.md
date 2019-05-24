## React

#### 特点
```
1）专注视图层：专注于提供清晰、简洁的视图层解决方案，并且包括 View 和 Controller 的库（Redux）
2）Virtual DOM：提升性能，方便和其他平台集成（可以映射出对应的原生控件，react-native -> web、android、ios）
3）函数式编程：充分利用很多函数式方法去减少冗余代码
```

#### JSX
```
虚拟元素：构建与更新都是在内存中完成的，并不会真正渲染到 DOM 中去
1）DOM 元素：对应原生 DOM 元素，被表示成纯粹的 JSON 对象
2）组件元素：对应原生自定义元素，封装一种构建组件元素的公共方法，方法名对应 DOM 元素类型，参数对应 DOM 元素属性
JSX：将HTML语法直接加入到JavaScript代码中，再通过翻译器（Babel）转换为纯JavaScript由浏览器执行（省去了构建Json的烦琐过程，更易于阅读与开发）
1）基本语法：定义标签时，只允许被一个标签包裹；标签一定要闭合
2）元素类型：小写首字母对应 DOM 元素，大写首字母对应组件元素
3）元素属性：DOM 元素属性（标准规范属性，例外：class 改为 className、for 改为 htmlFor、style 值必须是对象），组件元素属性（由标准写法改为小驼峰写法，是完全自定义的属性，也可以理解为实现组件所需要的参数），属性转义（React避免转义：<div dangerouslySetInnerHTML={{__html: 'cc &copy; 2015'}} />）
```

#### React 组件
```
组成：属性（props）、状态（state）、生命周期方法
构建方法：React.createClass、ES6 class、无状态函数（无状态组件）
```

#### React 数据流
```
在 React 中，数据是自顶向下单向流动的，即从父组件到子组件
智能组件、木偶组件
state：只关心每个组件自己内部的状态，这些状态只能在组件内改变
props：如果顶层组件初始化 props，那么 React 会向下遍历整棵组件树，重新尝试渲染所有相关的子组件
```

#### React 生命周期
```
挂载：componentWillMount 方法在 render 方法之前执行，componentDidMount 方法在 render 方法之后执行，都只会在组件初始化时运行一次
卸载：componentWillUnmount 方法在卸载前执行
更新：
    自身 state 更新，会依次执行 shouldComponentUpdate（nextProps,nextState）、componentWillUpdate(nextProps,nextState)、render、componentDidUpdate(prevProps,prevState)
    父组件 props 更新，先执行 componentWillReceiveProps(nextProps) 方法
```

#### React 与 DOM
* **ReactDOM**：操作真实 DOM
    * **findDOMNode**：ReactDOM.findDOMNode((ReactComponent);返回 React 组件实例相应的 DOM 节点（只在 componentDidMount 和 componentDidUpdate 方法中用）
    * **unmountComponentAtNode**：进行卸载操作
    * **render**：ReactDOM.render(ReactElement,DOMElement);把 React 渲染的 Virtual DOM 渲染到浏览器的 DOM 当中，并且返回 element 的实例（只有在顶层组件才不得不使用 ReactDOM）
* **refs**：组件被调用时新建的一个该组件的实例
```
1）ref={(ref) => this.myComp = ref}
2）ref="myComp"  const myComp = this.refs.myComp;
为了防止内存泄漏，当卸载一个组件的时候，组件里所有的 refs 就会变为 null
findDOMNode 和 refs 都无法用于无状态组件中（无状态组件挂载时只是方法调用，没有新建实例）
```

#### 事件系统
```
合成事件:事件委派（使用一个统一的事件监听器）、自动绑定（绑定 this 为当前组件，并且缓存这种引用，在使用 ES6 classes 或者纯函数时，需要手动实现 this 的绑定）
```

#### 组件间通信
* **父组件向子组件通信**：props
* **子组件向父组件通信**：回调函数、自定义事件机制
* **跨级组件通信**：context（父：getChildContext(){return {color: 'red'}}，子：const myColor = this.context.color）
* **没有嵌套关系的组件通信**：发布/订阅模式（修改和查询外部模块）

#### 组件间抽象（一类功能需要被不同的组件公用）
* **mixin**
* **高阶组件**：接收原始组件并返回原始组件的增强/填充版本

#### 组件性能优化
* **PureRender**：组件满足纯函数的条件
```
重新实现了 shouldComponentUpdate 生命周期方法法，让当前传入的 props 和 state 与之前的作浅比较
会触发 PureRender 为 true 的情况：
    1）直接为 props 设置对象或数组
    2）设置 props 方法并通过事件绑定在元素上
    3）设置子组件
```
* **key**：如果每一个子组件是一个数组或迭代器的话，那么必须有一个唯一的 key

#### 原理
* **Virtual DOM 模型**：
* **setState 机制**：
* **diff 算法**：
```
1）tree diff：Web UI 中 DOM 节点跨层级的移动操作特别少，可以忽略不计（建议不要进行 DOM 节点跨层级的操作，可以通过 CSS 隐藏或显示节点，而不是真正地移除或添加 DOM 节点）
2）component diff：拥有相同类的两个组件将会生成相似的树形结构，拥有不同类的两个组件将会生成不同的树形结构（React 允许用户通过 shouldComponentUpdate() 来判断该组件是否需要进行 diff 算法分析）
3）element diff：对于同一层级的一组子节点，它们可以通过唯一 id 进行区分（插入、移动、删除，尽量减少类似将最后一个节点移动到列表首部的操作）
```

#### Flux
```
一款用于构建用户界面的应用程序架构思想
单向数据流：数据和逻辑永远单向流动
3大组成部分：
    dispatcher：负责分发事件（action）
    store：负责保存数据，同时响应事件并更新数据（store 对外只暴露 getter（读取器）而不暴露 setter（设置器））
    view：负责订阅（controller-view） store 中的数据，并使用这些数据渲染相应的页面（ Flux 中的 view 层不能直接修改数据，必须使用 dispatcher 分发一个 action）
action：一个普通的 JavaScript 对象，一般包含 type、payload 等字段，用于描述一个事件以及需要改变的相关数据
controller-view：进行 store 与 view 层之间的绑定，定义数据更新及传递的方式
actionCreator：用来创造 action
```

#### Redux
```
一个“可预测的状态容器”库
Redux 应用：指使用了 redux 这个 npm 包，并结合了视图层实现（如 React）及其他前端应用必备组件（路由库、Ajax 请求库）组成的完整的类 Flux 思想的前端应用
三大原则：单一数据源、state状态是只读的、状态修改均由纯函数完成
store：在 Redux 中只有一个 store，一旦 store 接收到动作，它会将当前状态和给定动作发送给 reducer 并要求其返回一个新的状态
reducers：决定数据如何改变的逻辑以纯函数的形式存在
reducer：是一个纯函数，它的职责是根据 previousState 和 action 计算出新的 state
高阶 reducer：指将 reducer 作为参数或者返回值的函数（作用：复用、增强）
```

