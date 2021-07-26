---
title: zhaoo - 主题文档
image: https://picsum.photos/400/300.jpg
---
# Vue知识 & 问题记录

## **1、**vue-pdf插件加载本地PDF预览

**问题描述：**

在使用vue-pdf插件加载本地PDF文件进行预览时，报如下错误：

'Warning: Ignoring invalid character "33" in hex string'

'Warning: Ignoring invalid character "79" in hex string'...

**解决方法：**

 在vue-cli3脚手架搭建的项目中，读取本地的PDF文件需要放到public文件夹中，在引用时，不能使用相对路径，且‘/’即表示public文件夹(需略去public)

## 2、eslint报错： Expected linebreaks to be 'LF' but found 'CRLF'

**问题描述：**

VUE项目中eslint报错： Expected linebreaks to be 'LF' but found 'CRLF'

**解决方法：**右下角或者修改默认配置

Windows系统下文本文件的换行符是： 回车+换行CR/LF即 \r\n或^M\n

linux/unix系统下文本文件的换行符是：换行LF即 \n

Mac OS系统下文本文件的换行符：回车CR即 \r或^M

## 3、使用常量替代 Mutation 事件类型

使用常量替代 mutation 事件类型在各种 Flux 实现中是很常见的模式。这样可以使 linter 之类的工具发挥作用，同时把这些常量放在单独的文件中可以让你的代码合作者对整个 app 包含的 mutation 一目了然

```js
// mutation-types.js 
export const SOME_MUTATION = 'SOME_MUTATION' 
// store.js 
import Vuex from 'vuex' 
import { SOME_MUTATION } from './mutation-types' 
const store = new Vuex.Store({  
	state: { ... },
	mutations: {    
	// 我们可以使用 ES2015 风格的计算属性命名功能来使用一个常量作为函数名    
	[SOME_MUTATION] (state) {
    	// mutate state    
    }
  } 
})
```

同理，对于Action，会经常用到 ES2015 的 [参数解构 (opens new window)](https://github.com/lukehoban/es6features#destructuring)来简化代码（特别是我们需要调用 commit很多次的时候）

```
actions: {
  increment ({ commit }) {
    commit('increment')
  }
}
```

## 4、MQTT使用：

通过协议指定使用的连接方式 

// ws 未加密 WebSocket 连接 

// wss 加密 WebSocket 连接 

 // mqtt 未加密 TCP 连接

 // mqtts 加密 TCP 连接

 // wxs 微信小程序连接  

// alis 支付宝小程序连接



## 5.关于Vue中 style的scoped用法：

发现使用的组件设置的样式在页面中不起作用，被层叠覆盖

当一个style标签拥有scoped属性时候，它的css样式只能用于当前的Vue组件，可以使组件的样式不相互污染。如果一个项目的所有style标签都加上了scoped属性，相当于实现了样式的模块化。

scoped看起来很好用，当时在Vue项目中，当我们引入第三方组件库时(如使用vue-awesome-swiper实现移动端轮播)，需要在局部组件中修改第三方组件库的样式，而又不想去除scoped属性造成组件之间的样式覆盖。这时我们可以通过特殊的方式穿透scoped。

## **6，this.$v是使用vuelidate后注册到vue中的**

可以打印出来看看，注意使用

## 7、Unexpected token u in JSON at position 0：

我出现这个错误的原因是：我使用localStorage或者sessionStorage存入本地数据时，

存入了一个值为 Undefined ,当我在去取出来转换为JSON对象的时候，就是出现 Unexpected token u in JSON at position 0 报错

所以，当你存入数据和使用JSON.parse转换时需要判断一下，这个值不能为Undefined，才能进行JSON.parse

本质上的问题就是json转换的对象时个空的

## 7.value.push is not a function  ：

在使用el-select 和el-option时，注意， el-select绑定的值，如果是多选，一定要是个数组，同时注意在请求后台数据时，如果赋值成了字符串，就会出现这个错误

## 8、请求头问题

blog测试开发过程中，发现put修改一直没有结果，发现是后端没有获取到数据，因为后端是Query获取拼接到url后面的参数，而我们的请求头是 application/json;charset=UTF-8，以payload的形式，所有取不到，故修改后端代码s

## 9、渲染问题

 Error in render: "TypeError:Cannot read property xxx of undefined"

模板在渲染时候，读取对象中的某个对象的属性值时，这个对象不存在

原因：

vue渲染机制中：

异步数据先显示初始数据，再显示带数据的数据，所以上来加载时还是一个空对象，没有从后台取到数据

解决：

在前面加v-if判断条件，如果取不到则不加载即可，（注意，不能用v-show，v-show的机制是加载后，根据条件判断是否显示）

## 10、vue中的transition

Vue 提供了 transition 的封装组件，在下列情形中，可以给任何元素和组件添加进入/离开过渡

1. 条件渲染 (使用 v-if)
2. 条件展示 (使用 v-show)
3. 动态组件
4. 组件根节点

## 11、ref 写在标签上时：this.$refs.名字  获取的是标签对应的dom元素

​     ref 写在组件上时：这时候获取到的是 子组件（比如counter）的引用

## 12、scss中引用图片路径，可以这么写

```
background: url("~@/assets/img/footer.jpg") no-repeat;
```

## 13、vue的 nextTick

## 14、js中如果想用变量值来做对象的属性名，用中括号 []：如下示例

```
 for (const item of temp) {
        const index = item.pid
        if (index in data) {
          data[index].push(item)
        } else {
          data[index] = []
          data[index].push(item)
        }
      }
```

## 15、axios默认不带cookie，开启需要在 配置中加：withCredentials: true

## 16、样式穿透示例、内容换行

```
.el-table{
  ::v-deep .cell {
    white-space: pre-line !important;/*保留换行符*/
  }
}
```

