## Vue

#### 特点
```
vue2.0：Object.defineProperty()，重新定义对象get和set方法
vue3.0:Proxy，在目标对象之前架设一层“拦截”，外界对该对象的访问，都必须先通过这层拦截
1）简单小巧、渐进式技术栈
2）解耦视图与数据
3）可复用的组件
4）前端路由
5）状态管理
6）虚拟 DOM
```

#### 语法
```
//实例
new Vue({
    el: DOM节点,
    data: {动态数据},
    filters: {过滤器名称:函数}, //可以全局定义过滤器
    computed: {计算属性的getter}, //只在相关依赖发生改变时才会重新求值
    methods: {事件方法},
    watch:{侦听属性的回调方法}，
    components: {局部组件名:局部组件},
})
//组件（全局注册）
Vue.component({
    props: [父级属性]
    template: DOM元素,
    data: function(){return 动态数据},
})
//（局部注册）
var ComponentA = { /* ... */ }
```

#### Props
```
非字符串模板时，camelCase (驼峰命名法) 的 prop 名需要使用其等价的 kebab-case (短横线分隔命名) 命名
类型检查：
    type：String|Number|Boolean|Array|Object|Date|Function|Symbol|自定义的构造函数（通过 instanceof 检查）
指定元素继承父级属性：inheritAttrs: false 并且 v-bind="$attrs"
```

#### 自定义事件
```
推荐始终使用 kebab-case 的事件名
```

#### 组件通信
```
父->子：子组件props接收
子->父：子组件事件里 this.$emit(父组件事件，传参)

```

#### 插槽
```
<slot></slot>：子组件渲染父组件传入的内容
具名插槽：父<template slot="header"></template> 子<slot name="header"></slot>
作用域插槽（父访问子作用域）：父<template slot-scope="slotProps">{{slotProps.value}}</template>或<template slot-scope="{value}">{{value}}</template> 子<slot value="哈哈哈"></slot>
```

#### is
```
缓存动态组件
<keep-alive>
  <component v-bind:is="currentTabComponent"></component>
</keep-alive>
```

#### 生命周期
```
created：实例创建完成，尚未挂载（初始化处理数据）
mounted：el挂载到实例（处理第一个业务逻辑）
beforeDestroy：实例销毁前（用于解绑监听事件）
```

#### 指令
```
v-modal
v-bind:属性：动态更新 HTML 元素上的属性（缩写：:属性）
v-on:事件：绑定事件监听器（缩写：@事件）
v-if v-else-if v-else
v-show：始终会被渲染并保留在 DOM 中，只是简单地切换元素的 CSS 属性 display
v-for
v-html
v-pre
v-cloak
v-once
```

#### 过滤器
```
{{data | formatDate}}
```

#### 过渡和动画
```
<transition name="fade">
```

#### 混入
```
合并：组件数据优先，混入对象的钩子将在组件自身钩子之前调用
1）
// 定义一个混入对象
var myMixin = {
  created: function () {
    this.hello()
  },
  methods: {
    hello: function () {
      console.log('hello from mixin!')
    }
  }
}
// 定义一个使用混入对象的组件
var Component = Vue.extend({
  mixins: [myMixin]
})
var component = new Component() // => "hello from mixin!"
2）
var mixin = {
  data: function () {
    return {
      message: 'hello'
    }
  }
}
new Vue({
  mixins: [mixin],
  data: function () {
    return {
      message: 'goodbye'
    }
  }
})
3）全局混入
// 为自定义的选项 'myOption' 注入一个处理器。
Vue.mixin({
  created: function () {
    var myOption = this.$options.myOption
    if (myOption) {
      console.log(myOption)
    }
  }
})
new Vue({
  myOption: 'hello!'
})// => "hello!"
```

#### 自定义指令
```
钩子函数：
    bind：只调用一次，指令第一次绑定到元素时调用。在这里可以进行一次性的初始化设置。
    inserted：被绑定元素插入父节点时调用 (仅保证父节点存在，但不一定已被插入文档中)。
    update：所在组件的 VNode 更新时调用，但是可能发生在其子 VNode 更新之前。指令的值可能发生了改变，也可能没有。但是你可以通过比较更新前后的值来忽略不必要的模板更新 (详细的钩子函数参数见下)。
    componentUpdated：指令所在组件的 VNode 及其子 VNode 全部更新后调用。
    unbind：只调用一次，指令与元素解绑时调用
1）全局注册
// 注册一个全局自定义指令 `v-focus`
Vue.directive('focus', {
  // 当被绑定的元素插入到 DOM 中时……
  inserted: function (el) {
    // 聚焦元素
    el.focus()
  }
})
2）局部注册
// 组件中也接受一个 directives 的选项
directives: {
  focus: {
    // 指令的定义
    inserted: function (el) {
      el.focus()
    }
  }
```

#### 渲染函数 render
```
render: function (createElement) {
  return createElement(标签字符串, 包含模板相关属性的数据对象?, 子虚拟节点)
}
```

```
vue init webpack my-demo
```