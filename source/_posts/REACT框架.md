---
title: REACT框架
date: 2020-03-25 09:18:55
cover: https://ss3.bdstatic.com/70cFv8Sh_Q1YnxGkpoWK1HF6hhy/it/u=1900915343,2681931728&fm=26&gp=0.jpg
---

# 1. React简介

## 1.1 React介绍

+ React 是一个用于构建用户界面的 JAVASCRIPT库。React主要用于构建UI，很多人认为 React 是 MVC 中的 V（视图）。
+ React 起源于 Facebook 的内部项目，因为该公司对市场上所有 JavaScript MVC 框架都不满意，就决定自己写一套，用来架设 Instagram（照片交友） 的网站。做出来以后，发现这套东西很好用，**就在2013年5月开源了**。
+ React 拥有较高的性能，代码逻辑非常简单，越来越多的人已开始关注和使用它。由于 React 的**设计思想极其独特**，属于革命性创新，性能出众，代码逻辑却非常简单。所以，越来越多的人开始关注和使用，认为它可能是将来 Web 开发的主流工具。
+ 清楚两个概念：
  + library（库）：小而巧的库，只提供了特定的API；优点就是 船小好掉头，可以很方便的从一个库切换到另外的库；但是代码几乎不会改变；比如从jQuery切换到

  + Framework（框架）：大而全的是框架；框架提供了一整套的解决方案；所以如果在项目中间，想切换到另外的框架，是比较困难的；



## 1.2 前端三大主流框架

- Angular.js：出来**较早**的前端框架，学习曲线比较陡，NG1学起来比较麻烦，NG2 ~ NG5开始，进行了一系列的改革，也提供了组件化开发的概念；从NG2开始，也支持使用TS（TypeScript）进行编程；

+ Vue.js：**最火**（关注的人比较多）的一门前端框架，它是中国人开发的，对我们来说，文档要友好一些；

+ React.js：**最流行**（用的人比较多）的一门框架，因为它的设计很优秀；



## 1.3 React与Vue的对比

**1、监听数据变化的实现原理不同**

- Vue 通过 getter/setter 以及一些函数的劫持，能精确知道数据变化，不需要特别的优化就能达到很好的性能
- React 默认是通过比较引用地址的方式进行的，如果不优化（PureComponent/shouldComponentUpdate）可能导致大量不必要的VDOM的重新渲染

**2、数据流的不同**

![img](http://m.qpic.cn/psc?/V1497zRn1XyhLI/uUnjQtxoKSmXQ5.YSnl4gAk7dXwc4xb6JNA*btZsrXfUKhIY4Mlhhvk6QQqzzrxBHBrQT9uu61Cjk9O.HxVwvA!!/b&bo=OgOQAToDkAEDCSw!&rf=viewer_4)

大家都知道Vue中默认是支持双向绑定的。在Vue1.0中我们可以实现两种双向绑定：

1. 父子组件之间，props 可以双向绑定
2. 组件与DOM之间可以通过 v-model 双向绑定

在 Vue2.x 中去掉了第一种，也就是父子组件之间不能双向绑定了（但是提供了一个语法糖自动帮你通过事件的方式修改），并且 Vue2.x 已经不鼓励组件对自己的 props 进行任何修改了。所以现在我们只有 组件 <--–> DOM 之间的双向绑定这一种。

然而 React 从诞生之初就不支持双向绑定，React一直提倡的是单向数据流，他称之为 onChange/setState()模式。

不过由于我们一般都会用 Vuex 以及 Redux 等单向数据流的状态管理框架，因此很多时候我们感受不到这一点的区别了。

**3、模板渲染方式的不同**

在表层上， 模板的语法不同

- React 是通过JSX渲染模板
- 而Vue是通过一种拓展的HTML语法进行渲染

但其实这只是表面现象，毕竟React并不必须依赖JSX。在深层上，模板的原理不同，这才是他们的本质区别：

- React是在组件JS代码中，通过原生JS实现模板中的常见语法，比如插值，条件，循环等，都是通过JS语法实现的
- Vue是在和组件JS代码分离的单独的模板中，通过指令来实现的，比如条件语句就需要 v-if 来实现

**4、Vuex 和 Redux 的区别**

从表面上来说，store 注入和使用方式有一些区别。

在 Vuex 中，$store 被直接注入到了组件实例中，因此可以比较灵活的使用：

- 使用 dispatch 和 commit 提交更新
- 通过 mapState 或者直接通过 this.$store 来读取数据

在 Redux 中，我们每一个组件都需要显示的用 connect 把需要的 props 和 dispatch 连接起来。

另外 Vuex 更加灵活一些，组件中既可以 dispatch action 也可以 commit reducer，而 Redux 中只能进行 dispatch，并不能直接调用 reducer 进行修改。

从实现原理上来说，最大的区别是两点：

- Redux 使用的是不可变数据，而Vuex的数据是可变的。Redux每次都是用新的state替换旧的state，而Vuex是直接修改
- Redux 在检测数据变化的时候，是比较对象的引用地址；而Vuex其实和Vue的原理一样，是通过 getter/setter来比较的（如果看Vuex源码会知道，其实他内部直接创建一个Vue实例用来跟踪数据变化）

**5、总结**

React更偏向于构建稳定大型的应用，非常的科班化。相比之下，Vue更偏向于简单迅速的解决问题，更灵活，不那么严格遵循条条框框。因此也会给人一种大型项目用React，小型项目用 Vue 的感觉。

## 1.4 React中几个核心的概念

### 1.4.1 虚拟DOM（Virtual Document Object Model）

 + **DOM的本质是什么**：浏览器中的概念，用JS对象来表示页面上的元素，并提供了操作 DOM 对象的API；
 + **什么是React中的虚拟DOM**：是框架中的概念，是程序员用JS对象来模拟页面上的 DOM 和 DOM嵌套；
 + **为什么要实现虚拟DOM（虚拟DOM的目的）：**为了实现页面中DOM 元素的高效更新
 + **DOM和虚拟DOM的区别**：


![](http://m.qpic.cn/psc?/V1497zRn1XyhLI/43eWRH6lLSncPe1pJhVzbdWSqN.eymaP4Y0swybruZfE2pJw54iG4e.MLo.1sX41QK2eUtIf5xfRbZwZSm8tat9r8QuYzEoF*JIByABwl1c!/b&bo=OAXWAjgF1gIDGTw!&rf=viewer_4)

![1552877849641](http://m.qpic.cn/psc?/V1497zRn1XyhLI/uUnjQtxoKSmXQ5.YSnl4gP.OPjSV4OMh4MrirZA3ctsgoixiys28APiCkDiUdPuSOyw13*8XMbdg7ihJFWXi8Q!!/b&bo=KgLLACoCywADCSw!&rf=viewer_4)

### 1.4.2 react的Diff算法

![Diff算法图](http://m.qpic.cn/psc?/V1497zRn1XyhLI/uUnjQtxoKSmXQ5.YSnl4gIhXMGB7JUW9SA0AZyTppvWfdNC.OQD411Pm3QmE7b*gVdyuoUa1k*UafKghM13eYA!!/b&bo=4AKZAeACmQEDCSw!&rf=viewer_4)

其实传统diff算法就是对每个节点一一对比，循环遍历所有的子节点，然后判断子节点的更新状态。通过循环递归对节点进行依次对比，算法时间复杂度达到 O(n^3) ，n是树的节点数，这个有多可怕呢？——如果要展示1000个节点，得执行上亿次比较。即便是CPU快能执行30亿条命令，也**很难在一秒内**计算出差异。

React 通过制定大胆的策略，将 O(n^3) 复杂度的问题转换成 O(n) 复杂度的问题。react根据自己的特点，实现了部分代码的简化。

![1552878167661](http://m.qpic.cn/psc?/V1497zRn1XyhLI/uUnjQtxoKSmXQ5.YSnl4gLYniMHBf.WEdNItH3RZVetUwPp5L3GNVzpNcRpJGdTXXI3YCLocZ7*syN0osqiHPQ!!/b&bo=zAJAAcwCQAEDCSw!&rf=viewer_4)

#### a) tree diff

> （1）React通过updateDepth对Virtual DOM树进行层级控制。
> （2）对树分层比较，两棵树只对同一层次节点进行比较。如果该节点不存在时，则该节点及其子节点会被完全删除，不会再进一步比较。
> （3）只需遍历一次就能完成整棵DOM树的比较。

![1562723697592](http://m.qpic.cn/psc?/V1497zRn1XyhLI/uUnjQtxoKSmXQ5.YSnl4gILEZt2EwY85Z0*zuNjzuCuFZfJO*6lSJjwjZVCu2W6lhafJVTUk4sK*ciEex1ydIw!!/b&bo=vQEIAb0BCAEDCSw!&rf=viewer_4)

> 那么问题来了，如果DOM节点出现了跨层级操作,diff会咋办呢？
> 答：diff只简单考虑同层级的节点位置变换，如果是跨层级的话，只有创建节点和删除节点的操作。

![1562723819718](http://m.qpic.cn/psc?/V1497zRn1XyhLI/43eWRH6lLSncPe1pJhVzbQoF4KCfI7SWY.HVHttLf4ckLVIXComi64qWaO.9eEWivwh3UY6jl21WY4i2RYYw1HMKyrG.AtZFnT2Xd8ig4cc!/b&bo=cAIWAXACFgEDGTw!&rf=viewer_4)

> 如上图所示，以A为根节点的整棵树会被**重新创建，而不是移动**，因此 **官方建议不要进行DOM节点跨层级操作，可以通过CSS隐藏、显示节点，而不是真正地移除、添加DOM节点**。

#### b) component diff

React应用是基于组件构建的，对于组件的比较优化侧重于以下几点：

> 1. 同一类型组件遵从tree diff比较v-dom树
> 2. 不同类型组件，先将该组件归类为dirty component，替换下整个组件下的所有子节点
> 3. 同一类型组件Virtual Dom没有变化，React允许开发者使用shouldComponentUpdate()来判断该组件是否进行diff，运用得当可以节省diff计算时间，提升性能

![1562723945651](http://m.qpic.cn/psc?/V1497zRn1XyhLI/43eWRH6lLSncPe1pJhVzbZklJ*f3DGfU.Yfr4dYxg.tkjqF2bEUy3Vv3Kz8iRTcvk6Q9h7jZXGrMXKN*i7ml7*CoDdtCn0QraXzHp8GM9.g!/b&bo=*gHBAP4BwQADGTw!&rf=viewer_4)

如上图，当组件D → 组件G时，diff判断为不同类型的组件，虽然它们的结构相似甚至一样，diff仍然不会比较二者结构，会直接销毁D及其子节点，然后新建一个G相关的子tree，这显然会影响性能，官方虽然认定这种情况极少出现，但是开发中的这种现象造成的影响是非常大的。

#### c) element diff

对于同一层级的element节点，diff提供了以下3种节点操作：

> 1. INSERT_MARKUP 插入节点
> 2. MOVE_EXISING 移动节点
> 3. REMOVE_NODE 移除节点

![1562724094202](http://m.qpic.cn/psc?/V1497zRn1XyhLI/43eWRH6lLSncPe1pJhVzbVjbdFY3cwgD1XXkrfuQyx3SD9ukMui4Fx.lirLfRQdpbxg2arnmS2SI4xYCqKl8P2evBHZS9eVJJGr2c1MYtYI!/b&bo=CgLzAAoC8wADGTw!&rf=viewer_4)

一般diff在比较集合[A,B,C,D]和[B，A，D，C]的时候会进行全部对比，即按对应位置逐个比较，发现每个位置对应的元素都有所更新，则把旧集合全部移除，替换成新的集合，如上图，但是这样的操作在React中显然是复杂、低效、影响性能的操作，因为新集合中所有的元素都可以进行复用，无需删除重新创建，耗费性能和内存，只需要移动元素位置即可。

React对这一现象做出了一个高效的策略：允许开发者对同一层级的同组子节点添加唯一key值进行区分。意义就是代码上的一小步，性能上的一大步，甚至是翻天覆地的变化！

# 2. React入门案例

## 2.1 创建webpack应用

1. 运行`npm init -y` 快速初始化项目

2. 在项目根目录创建`src`源代码目录和`dist`产品目录

3. 在 src 目录下创建 `index.html和main.js`

4. 安装webpack和webpack-cli

   ```javascript
   npm install webpack@4.27.1 -d
   npm install webpack-cli -d       提供一些基本命令(比如webpack命令)
   ```

5. 创建webpack.config.js

   ```javascript
   const path = require("path")
   //webpack基于node构建的，所有用的是CommonJS模块化规范
   module.exports = {
       mode:"development",
       entry: path.join(__dirname, './src/main.js'),
       output: {
           path: path.join(__dirname, './dist'),
           filename: 'bundle.js'
       },
   }
   ```

6. index.html

   ```javascript
   <head>
       <meta charset="UTF-8">
       <title>Title</title>
   
       <script src="../dist/bundle.js"></script>
   </head>
   ```

7. 使用webpack命令打包项目，运行index.html查看结果

   ```
   webpack
   ```

8. 配置webpack-dev-server

   ```javascript
   #1.安装webpack-dev-serve
   npm install  webpack-dev-server -d
   
   #2.package.json的scripts添加dev
    "scripts": {
       "test": "echo \"Error: no test specified\" && exit 1",
       "dev": "webpack-dev-server --open --port 3000 --hot --host 127.0.0.1"
     },
   
    #3.npm run dev     webpack-dev-server将打包后的bundle.js托管到项目根路径下(内存中)，所以可以通过下面路径访问
     http://localhost:8080/bundle.js    
   
   #4.修改index.html中引入bundle.js的路径
   <head>
       <meta charset="UTF-8">
       <title>Title</title>
   
   	<!--使用webpack-dev-server打包后内存中的bundle.js-->
       <script src="../bundle.js"></script>
   </head>
   ```

9. 使用html-webpack-plugin将index.html配置到内存

   ```javascript
   #1.安装html-webpack-plugin
   npm i html-webpack-plugin@3.2.0 --save-dev
   
   #2.修改webpack.config.js配置
   // 导入自动生成HTMl文件的插件
   var htmlWebpackPlugin = require('html-webpack-plugin');
   
   module.exports = {
       entry: path.join(__dirname, './src/main.js'),
       output: { 
           path: path.join(__dirname, './dist'), 
           filename: 'bundle.js' 
       },
       plugins: [ 
           // 添加plugins节点配置插件
           new htmlWebpackPlugin({
               template:path.resolve(__dirname, 'src/index.html'),//模板路径
               filename:'index.html'//自动生成的HTML文件的名称
           })
       ],
   }
   ```

## 2.2 在webpack中使用 react

1. 运行 `npm install react react-dom -S` 安装包

   + react： 专门用于创建组件和虚拟DOM的，同时组件的生命周期都在这个包中
   + react-dom： 专门进行DOM操作的，最主要的应用场景，就是`ReactDOM.render()`

2. 在`index.html`页面中，创建容器：

   ```html
   <!-- 容器，将来，使用 React 创建的虚拟DOM元素，都会被渲染到这个指定的容器中 -->
   <div id="app"></div>
   ```

3. main.js导入包：

   ```js
   import React from 'react'                        // 创建组件、虚拟DOM元素，生命周期
   import ReactDOM from 'react-dom'      // 把创建好的 组件 和 虚拟DOM 放到页面上展示的
   ```

4. 创建虚拟DOM元素：

   ```jsx
   // 这是 创建虚拟DOM元素的 API    <h1 title="啊，五环" id="myh1">你比四环多一环</h1>
   //  第一个参数： 字符串类型的参数，表示要创建的标签的名称
   //  第二个参数：对象类型的参数， 表示 创建的元素的属性节点
   //  第三个参数： 子节点（包括 其它 虚拟DOM 获取 文本子节点）
   //  参数n :  其它子节点
   const myh1 = React.createElement('h1', { title: '啊，五环', id: 'myh1' }, '你比四环多一环')
   
   const mydiv = React.createElement('div', null, '这是一个div元素', myh1)
   
   ```


5. 渲染：

   ```js
   // 3. 渲染虚拟DOM元素
   // 参数1： 表示要渲染的虚拟DOM对象
   // 参数2： 指定容器,注意：这里不能直接放 容器元素的Id字符串，需要放一个容器的DOM对象
   ReactDOM.render(myh1, document.getElementById('app'))
   
   ```


## 2.3 JSX语法

> 什么是JSX语法：就是符合 xml 规范的 JS 语法；（语法格式相对来说，要比HTML严谨很多）

### 2.3.1 启用 JSX 语法

浏览器目前还不支持 ES6 模块，比如这种ES6语法在浏览器和node中都不被支持    `import fs from 'fs'`，为了现在就能使用，我们可以使用转码器(ES6-->ES5)，也可以使用Browserify。

知名度比较大的转码器有Traceur和babel，babel将ES6代码编译为大多数浏览器（包括IE9）支持的ES5代码。

+ 安装 `babel` 插件

  - 运行`npm i babel-core@6.26.3 babel-loader@7.1.5 babel-plugin-transform-runtime --save-dev`
  - 运行`npm i babel-preset-env babel-preset-stage-0 --save-dev`

+ 安装能够识别转换jsx语法的包 `babel-preset-react` 

  + 运行`npm i babel-preset-react -D`

+ 添加 `.babelrc` 配置文件

  ```json
  {
    "presets": ["env", "stage-0", "react"],
    "plugins": ["transform-runtime"]
  }
  
  ```

+ 添加babel-loader配置项：

  ```js
  module: { //要打包的第三方模块
      rules: [
        { test: /\.js|jsx$/, use: 'babel-loader', exclude: /node_modules/ }
      ]
  }
  
  ```


```javascript
# 在main.js中使用JSX语法 
const mydiv2 = <div><h1>哈哈</h1></div>;
ReactDOM.render(mydiv2, document.getElementById('app'))

```

### 2.3.2 JSX 语法

JSX语法的本质：并不是直接把 jsx 渲染到页面上，而是内部通过 createElement 再渲染到页面；

在 jsx 中混合写入 js 表达式：在 jsx 语法中，要把 JS代码写到    `{ }` 中

```javascript
// 1. 导入包
import React from 'react'
import ReactDOM from 'react-dom'

//2. JSX中使用数值、字符串、bool、数组等信息
let a = 10
let str = '你好，中国'
let boo = false
let title = '999'
const h1 = <h1>红火火恍恍惚惚</h1>
const arr = [
  <h2>这是h2</h2>,
  <h3>这是h3</h3>
]
const arrStr = ['毛利兰', '柯南', '小五郎', '灰原哀']

// 定义一个空数组，将来用来存放 名称 标签【方案1】
const nameArr = []
// 注意： React 中，需要把 key 添加给 被 forEach 或 map 或 for 循环直接控制的元素
arrStr.forEach(item => {
  const temp = <h5 key={item}>{item}</h5>
  nameArr.push(temp)
})

// 数组的 map 方法, map 中必须写 return
/* const result = arrStr.map(item => {
  return item + '~~'
})
console.log(result) */

// 3. 调用 render 函数渲染   JSX  XML 比 HTML 严格多了
// 在JSX要使用JS，则需要把 JS 代码写到 {} 中
ReactDOM.render(<div>
  {a + 2}
  <hr />
  {str}
  <hr />
  {boo ? '条件为真' : '条件为假'}
  <hr />
  <p title={title}>这是p标签</p>
  {h1}
  <hr />
  {/* {arr} */}
  {
    // 这是注释，你看不见我
  }
  <hr />
  {nameArr}
  <hr />
  {arrStr.map(item => <div key={item}><h3>{item}</h3>
  </div>)}
  <hr />

  <label htmlFor="ooo">11111</label>
</div>, document.getElementById('app'))
        
                
 #注意点：
1. 在 JSX 中 写注释：推荐使用{ /* 这是注释 */ }
2. 为 JSX 中的htmlFor替换label的for属性
3. 在 JSX 创建DOM的时候，所有的节点，必须有唯一的根元素进行包裹；
4. 在 JSX 语法中，标签必须成对出现，如果是单标签，则必须自闭和！

```

> 当 编译引擎，在编译JSX代码的时候，如果遇到了`<`那么就把它当作 HTML代码去编译，如果遇到了 `{}` 就把 花括号内部的代码当作普通JS代码去编译；

# 3. React中创建组件

## 3.1 使用构造函数来创建组件

> 如果要接收外界传递的数据，需要在构造函数的参数列表中使用`props`来接收；
>
> 必须要向外return一个合法的JSX创建的虚拟DOM；

### 3.1.1 创建组件

```jsx
// 第一种创建组件的方式 ： 注意构造函数首字母必须大写
function Hello (props) { 
    // 如果 在一个组件种 return 一个 null。则表示此组件是空的，什么都不会渲染
	// return null 
    // 在组件中，必须 返回一个 合法的 JSX 虚拟DOM元素
	return <div>Hello 组件</div>
}

```

### 3.1.2 为组件传递数据

```jsx
// 1. 导入包
import React from 'react'
import ReactDOM from 'react-dom'

function Hello(props) {
  // props.name = 'zs'     不论是 Vue 还是 React，组件中的 props 永远都是只读的；不能被重新赋值;
  console.log(props)
  return <div>这是 Hello 组件 --- {props.name} --- {props.age} --- {props.gender}</div>
}


const dog = {
  name: '大黄',
  age: 3,
  gender: '雄'
}

ReactDOM.render(<div>
  123
  {/* 直接把 组件的名称，以标签形式，丢到页面上即可 */}
  <Hello name={dog.name} age={dog.age} gender={dog.gender}></Hello>
  {/* 使用{...obj}属性扩散传递数据 */}
  <Hello {...dog}></Hello>
</div>, document.getElementById('app'))

```

```javascript
# 关于es6的展开运算符
var o2 = {
  age: 22,
  address: '中国北京',
  phone: '139999'
}

var o1 = {
  name: 'zs',
  ...o2
}

console.log(o1)

```

### 3.1.3 封装组件到独立文件

```javascript
#1. 新建Hello.jsx，并导出组件
import React from 'react'
// 第一种创建组件的方式
export default function Hello(props) {
  // 如果 在一个组件中 return 一个 null。则表示此组件是空的，什么都不会渲染
  // return null
  // 在组件中，必须 返回一个 合法的 JSX 虚拟DOM元素
  // props.name = 'zs'
  console.log(props)
  // 结论：不论是 Vue 还是 React，组件中的 props 永远都是只读的；不能被重新赋值；

  return <div>这是 Hello 组件 --- {props.name} --- {props.age} --- {props.gender}</div>
}

// 把组件暴露出去
// export default Hello

#2.导入Hello.jsx
  // 1. 导入包
  import React from 'react'
  import ReactDOM from 'react-dom'
  // 注意： 这里的 @ 符号，表示 项目根目录中的 src 这一层目录
  import Hello from '@/components/Hello.jsx'
  const dog = {
    name: '大黄',
    age: 3,
    gender: '雄'
  }

  ReactDOM.render(<div>
    123
    <Hello {...dog}></Hello>
  </div>, document.getElementById('app'))
                  
                  
#3.在导入组件的时候，如何省略组件的.jsx后缀名
// 打开 webpack.config.js ，并在导出的配置对象中，新增 如下节点：
  resolve: {
      extensions: ['.js', '.jsx', '.json'], // 表示，这几个文件的后缀名，可以省略不写
      alias: {
          '@': path.join(__dirname, './src')
      }
    }

```

##  3.2 使用 class 关键字来创建组件        

### 3.2.1 ES6的class关键字     

  ```javascript
// 创建了一个动物类
class Animal {
  // 每一个类中都有一个构造器，如果我们程序员没有手动指定构造器，那么，可以认为类内部有个隐形的、看不见的 空构造器，类似于 constructor(){}
  // 构造器的作用是每当 new 这个类的时候，必然会优先执行构造器中的代码
  constructor(name, age) {
    // 实例属性
    this.name = name
    this.age = age
  }

  // 在 class 内部，通过 static 修饰的属性，就是静态属性
  static info = "eee"

  // 这是动物的实例方法(挂载到原型对象上的实例方法)
  jiao() {
    console.log('动物的实例方法')
  }

  // 这是 动物 类的静态方法（今后用的不多）
  static show() {
    console.log('这是 Animal 的静态 show 方法')
  }
}

const a1 = new Animal('大黄', 3)
console.log(a1)
// console.log(a1.name)// 实例属性
// console.log(a1.age) // 实例属性
console.log(Animal.info) // info 是 Animal 的静态属性
a1.jiao() // 这是实例方法
Animal.show() // 静态方法

//其实静态属性和静态方法都挂载到了constructor上面，而构造器又指向了函数本身，所以可以直接通过函数名来调用静态属性和静态方法

  ```

ES6的class只是一个语法糖，其本质仍然是通过之前的构造函数来创建对象，而对应的实例属性、实例方法、静态属性、静态方法实质都是向对应的原型和constructor中新增属性和方法，没有实质的变化。

### 3.2.2 class继承

```javascript
// 这是父类 
class Person {
  constructor(name, age){
    this.name = name
    this.age = age
  }

  // 打招呼 的 实例方法
  sayHello(){
    console.log('大家好')
  }
}


class American extends Person {
  constructor(name, age){
    // super 是一个函数，它是父类的构造器；子类中的 super其实就是父类constructor 构造器的一个引用；
    super(name, age)
  }
}

const a1 = new American('Jack', 20)
console.log(a1)
a1.sayHello()


// 这是子类 中国人
class Chinese extends Person{
  // IDNumber 身份证号 【中国人独有的】，既然是独有的，就不适合 挂载到 父类上；
  constructor(name, age, IDNumber){
    super(name, age)
    // 语法规范：在子类中， this 只能放到 super 之后使用
    this.IDNumber = IDNumber
  }
}

const c1 = new Chinese('张三', 22, '130428******')
console.log(c1)
c1.sayHello()

```

### 3.2.3 基于class关键字创建组件

最基本的组件结构：

```jsx
//让自己的组件继承React.Compoent，重写render方法
class 组件名称 extends React.Component {
    render(){
        return <div>这是 class 创建的组件</div>
    }
}

```

```javascript
// 1. 导入包
import React from 'react'
import ReactDOM from 'react-dom'

// class 关键字创建组件
class Movie extends React.Component {
  // 构造器
  constructor() {
    // 由于 Movie 组件，继承了 React.Component 这个父类，所以自定义的构造器中必须调用 super()
    super()
    // 只有调用了 super() 以后，才能使用 this 关键字。这个 this.state = {} 就相当于 Vue 中的 data() { return { } }
    this.state = { 
      msg: '大家好，我是 class 创建的 Movie组件'
    }
  }

  // render 函数的作用，是 渲染 当前组件所对应的 虚拟DOM元素
  render() {
    return <div>
      {/* 注意：在 class 组件内部，this 表示 当前组件的实例对象。props数据不可以修改，state数据可以修改 */}
      这是 Movie 组件 -- {this.props.name} -- {this.props.age} -- {this.props.gender}
      <h3>{this.state.msg}</h3>
    </div>
  }
}


const user = {
  name: 'zs',
  age: 22,
  gender: '男'
}

// 3. 调用 render 函数渲染
ReactDOM.render(<div>
  123
  {/* 这里的 Movie 标签，其实，就是 Movie 类的一个实例对象 */}
  {/* <Movie name={user.name} age={user.age}></Movie> */}
  <Movie {...user}></Movie>

</div>, document.getElementById('app'))

```

### 3.2.4 state的修改

#### a) 不能直接修改 State

```javascript
this.state.comment = 'Hello';

 //可以这样修改State
this.setState({comment: 'Hello'});

```

#### b) State的更新可能是异步的

因为 `this.props` 和 `this.state` 可能会异步更新，所以你不要依赖他们的值来更新下一个状态。

```javascript
//调用setState，组件的state并不会立即改变，setState只是把要修改的状态放入一个队列中，React会优化真正的执行时机，并且React会出于性能原因，可能会将多次setState的状态修改合并成一次状态修改。所以不要依赖当前的State，计算下个State。
function add() {
  //Wrong
  this.setState({count: this.state.count + 1});
  this.setState({count: this.state.count + 1});
  this.setState({count: this.state.count + 1});
  //结果state的count为1
}

//Correct
add = () => {
    this.setState(state => ({
        count: state.count + 1
    }));
    this.setState(state => ({
        count: state.count + 1
    }));
    this.setState(state => ({
        count: state.count + 1
    }));
    //结果state的count为3
}


// Wrong   因为state和props的更新可能是异步的，所以并不能保证counter中所获取到的state和props是最新的
this.setState({
  counter: this.state.counter + this.props.increment,
});

// Correct    这边的state表示之前的state状态了
this.setState((state, props) => ({
  counter: state.counter + props.increment
}));

```

> state的更新既可能是同步的，也可能是异步的。 准确地说，在React内部机制能检测到的地方, setState就是异步的；在React检测不到的地方，例如setInterval、setTimeout里，setState就是同步更新的。

#### c) 获取更新之后的state数据

```javascript
this.setState(
    { data: newData },
    () => {
        //这里打印的是最新的state值
        console.log(this.state.data);
    }
);

```

## 3.3 两种创建组件方式的对比

1. 用**构造函数**创建出来的组件：叫做“无状态组件”，只有props，没有自己的私有数据和生命周期函数
2. 用**class关键字**创建出来的组件：叫做“有状态组件”，有私有数据和生命周期函数

> 有状态组件和无状态组件之间的**本质区别**就是：有无state属性！无状态组件由于没有私有数据和生命周期函数，运行效率会比有状态组件高一些。

## 3.4 条件渲染

### 3.4.1 通过if来进行条件渲染

<https://blog.csdn.net/crystalqy/article/details/79066347>

```javascript
function Greeting(props) {
  const isLoggedIn = props.isLoggedIn;
  if (isLoggedIn) {
    return <UserGreeting />;
  }
  return <GuestGreeting />;
}

ReactDOM.render(
  // Try changing to isLoggedIn={true}:
  <Greeting isLoggedIn={false} />,
  document.getElementById('root')
);

```

### 3.4.2 通过&&进行条件渲染

```javascript
function Mailbox(props) {
  const unreadMessages = props.unreadMessages;
  return (
    <div>
      <h1>Hello!</h1>
      {unreadMessages.length > 0 &&
        <h2>
          You have {unreadMessages.length} unread messages.
        </h2>
      }
    </div>
  );
}

const messages = ['React', 'Re: React', 'Re:Re: React'];
ReactDOM.render(
  <Mailbox unreadMessages={messages} />,
  document.getElementById('root')
);

```

### 3.4.3 三元运算符条件渲染

```javascript
render() {
  const isLoggedIn = this.state.isLoggedIn;
  return (
    <div>
      {isLoggedIn ? (
        <LogoutButton onClick={this.handleLogoutClick} />
      ) : (
        <LoginButton onClick={this.handleLoginClick} />
      )}
    </div>
  );
}

```

### 3.4.4 阻止组件渲染

在极少数情况下，你可能希望能隐藏组件，即使它已经被其他组件渲染。若要完成此操作，你可以让 `render` 方法直接返回 `null`，而不进行任何渲染。

```js
render() {
  const isLoggedIn = this.state.isLoggedIn;
  if (!isLoggedIn) {
    return null;
  }
  return (
    <div>
      <LoginButton onClick={this.handleLoginClick} />
    </div>
  );
}

```

## 3.5 列表渲染

```javascript
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    <li key={number.toString()}>
      {number}
    </li>
  );
  return (
    <ul>{listItems}</ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('root')
);

//key 帮助 React 识别哪些元素改变了，比如被添加或删除。因此你应当给数组中的每一个元素赋予一个确定的标识。
//一个元素的 key 最好是这个元素在列表中拥有的一个独一无二的字符串。通常，我们使用来自数据 id 来作为元素的 key。key在兄弟节点之间必须唯一
//当元素没有确定 id 的时候，万不得已你可以使用元素索引 index 作为 key：
const todoItems = todos.map((todo, index) =>
  // Only do this if items have no stable IDs
  <li key={index}>
    {todo.text}
  </li>
);

```

## 3.6 Fragment的使用

有时，语义化的 HTML 会被破坏。比如当在 JSX 中使用 `<div>` 元素来实现 React 代码功能的时候，又或是在使用列表（`<ol>`， `<ul>` 和 `<dl>`）和 HTML `<table>` 时。 在这种情况下，我们应该使用 [React Fragments](https://react.docschina.org/docs/fragments.html) 来组合各个组件。

```javascript
import React, { Fragment } from 'react';

function ListItem({ item }) {
  return (
    <Fragment>
      <dt>{item.term}</dt>
      <dd>{item.description}</dd>
    </Fragment>
  );
}

function Glossary(props) {
  return (
    <dl>
      {props.items.map(item => (
        <ListItem item={item} key={item.id} />
      ))}
    </dl>
  );
}

```

## 3.7 React组合

react组合类似于Vue中的slot(插槽)，子组件的内容由父组件来指定

```javascript
function FancyBorder(props) {
  return (
    <div className={'FancyBorder FancyBorder-' + props.color}>
      {/*子组件：占坑*/}
      {props.children}
    </div>
  );
}

function WelcomeDialog() {
  return (
    <FancyBorder color="blue">
      {/*父组件中填坑*/}
      <h1 className="Dialog-title">
        Welcome
      </h1>
      <p className="Dialog-message">
        Thank you for visiting our spacecraft!
      </p>
    </FancyBorder>
  );
}

```

少数情况下，你可能需要在一个组件中预留出几个“洞”。这种情况下，我们可以不使用 children，而是自行约定：将所需内容传入 props，并使用相应的 prop。

```javascript
function SplitPane(props) {
  return (
    <div className="SplitPane">
      <div className="SplitPane-left">
        {props.left}
      </div>
      <div className="SplitPane-right">
        {props.right}
      </div>
    </div>
  );
}

function App() {
  return (
    <SplitPane
      left={
        <Contacts />
      }
      right={
        <Chat />
      } />
  );
}

```

# 4. 评论列表案例

思路：父组件中套了若干个评论Item子组件，所以需要创建两个组件，分别是：CmtList和CmtItem

## 4.1 案例完成

```javascript
#1. CmtList组件

import React from 'react'

// 导入 评论项 组件
import CmtItem from '@/components/CmtItem'

export default class CmtList extends React.Component {
  constructor() {
    super()
    this.state = {
      CommentList: [ // 评论列表数据
        { id: 1, user: '张三', content: '哈哈，沙发' },
        { id: 2, user: '李四', content: '哈哈，板凳' },
        { id: 3, user: '王五', content: '哈哈，凉席' },
        { id: 4, user: '赵六', content: '哈哈，砖头' },
        { id: 5, user: '田七', content: '哈哈，楼下山炮' }
      ]
    }
  }

  render() {
    return <div>
      {/* 注意：在 JSX 中如果想写行内样式了，不能为 style 设置字符串的值 */}
      {/* 而是应该 这么写：    style={ { color: 'red' } } */}
      {/* 在 行内样式中，如果 是 数值类型的样式，则可以不用引号包裹，如果是 字符串类型的 样式值，必须使用 引号包裹 */}
      <h1 style={{ color: 'red', fontSize: '35px', zIndex: 3, fontWeight: 200, textAlign: 'center' }}>这是评论列表组件</h1>


      {this.state.CommentList.map(item => <CmtItem {...item} key={item.id}></CmtItem>)}
    </div>
  }
}
                                  
#2.CmtItem组件
import React from 'react'

// 第一层封装：将 样式对象 和 UI 结构分离
// const itemStyle = { border: '1px dashed #ccc', margin: '10px', padding: '10px', boxShadow: '0 0 10px #ccc' }
// const userStyle = { fontSize: '14px' }
// const contentStyle = { fontSize: '12px' }

// 第二层封装：合并成一个大的样式对象
// const styles = {
//   item: { border: '1px dashed #ccc', margin: '10px', padding: '10px', boxShadow: '0 0 10px #ccc' },
//   user: { fontSize: '14px' },
//   content: { fontSize: '12px' }
// }

// 第三层封装：抽离为单独的 样式表 模块
import styles from '@/components/styles'

export default function CmtItem(props) {
  return <div style={styles.item}>
    <h1 style={styles.user}>评论人：{props.user}</h1>
    <p style={styles.content}>评论内容：{props.content}</p>
  </div>
}

#3.styles.js 
export default {
  item: { border: '1px dashed #ccc', margin: '10px', padding: '10px', boxShadow: '0 0 10px #ccc' },
  user: { fontSize: '14px' },
  content: { fontSize: '12px' }
}

```

## 4.2 使用CSS样式表

1. 修改 `webpack.config.js`这个配置文件，为 `css-loader` 添加参数：

   ```js
   npm install  style-loader  css-loader -D
   
   { test: /\.css$/, use: ['style-loader', 'css-loader'] } 
   
   ```

2. 创建CmtList.css

   ```css
   .title{
     color: red;
     text-align: center;
     font-weight: 200;
   }
   
   h1{
     font-style: italic;
   } 
   
   ```

3. 在CmtList组件中`import`导入样式表，并接收模块化的 CSS 样式对象：

   ```js
   import cssObj from '../css/CmtList.css' 
   console.log(cssObj)   // 发现打印是空对象,因为它并不像js有模块化的导出
   
   ```

4. 在需要的HTML标签上，使用`className`指定模块化的样式：

   ```jsx
   //这边不能<h1 className={cssObj.title}>评论列表组件</h1> 这样用，因为cssObj是空对象，但是在webpack打包后title会成为全局样式，所以可以直接使用className="title"
   <h1 className="title">评论列表组件</h1>
   
   ```

5. 问题

   > 当我们在CmtList.css中指定了h1标签的样式的时候，我们发现  `import cssObj from '../css/CmtList.css'` 之后，CmtList和CmtItem中的h1标签都变成了倾斜，说明CmtList中的样式全局生效了。原因在于webpack进行打包的时候会将所有内容打包到一个js文件，所以打包后的样式会全局生效。

## 4.3 使用CSS模块化

```javascript
#1. webpack.config.js  修改css的rules规则，开启css的模块化
{ test: /\.css$/, use: ['style-loader', 'css-loader?modules'] }       //modules表示为css启动模块化(启动模块化之后就有模块作用域)

#2.修改CmtList.css
/* 注意： 被 :local() 包裹起来的类名会被模块化； 默认情况下所有的类和id选择器都会被模块化了； */
.title{
  color: red;
  text-align: center;
  font-weight: 200;
}

/* css 模块化只针对类选择器 和 Id选择器生效， 不会对标签选择器模块化 */
h1{
  font-style: italic;
} 

/* 注意：被 :global() 包裹起来的类名，不会被模块化，而是会全局生效； */ 
:global(.test){
  font-style: italic;
}

#3.CmtList组件
import cssObj from '../css/CmtList.css' 
console.log(cssObj)   // 发现开启css模块化之后，这边打印就有内容了

//所以在页面通过属性绑定指定样式
<h1 className={cssobj.title}>这是评论列表组件</h1>

//如果要指定多个样式，可以像下面这样使用，其实就是className = {'样式1'  '样式2'}
<h1 className={[cssobj.title, 'test'].join(' ')}>这是评论列表组件</h1>

```

## 4.4 CSS模块化注意事项

1. 使用`localIdentName`自定义生成的类名格式，可选的参数有：

   - [path]  表示样式表 `相对于项目根目录` 所在路径

   - [name]  表示 样式表文件名称

   - [local]  表示样式的类名定义名称

   - [hash:length]  表示32位的hash值

     ```javascript
     {
         test: /\.css$/,
         loader: 'style-loader',
     },
     {
         test: /\.css$/,
         loader: 'css-loader',
         options: {
             //'css-loader?modules'  表示开启css的模块化
             modules: {
                 //path:表示原样式文件路径
                 //name:表示原样式文件的名称
                 //local:原样式的名称
                 //hash:base64:5  : 使用hash的base64编码，保留5位
                 localIdentName: '[path][name]__[local]__[hash:base64:5]',
             }
         },
     },
     
     ```

   ![1562727326828](/REACT框架/1562727326828.png)

2. 使用 `:local()` 和 `:global()`

   - `:local()`包裹的类名，是被模块化的类名，只能通过`className={cssObj.类名}`来使用。`:local`可以省略
   - `:global()`包裹的类名，是全局生效的，不会被 `css-modules` 控制，定义的类名是什么，就是使用定义的类名`className="类名"`

3. 注意：只有`.title`这样的类样式或者id选择器，才会被模块化控制，类似于`body`这样的标签选择器，不会被模块化控制；

## 4.5 Bootstrap样式的使用

```javascript
npm install reactstrap bootstrap@4.0.0  
npm i url-loader file-loader --save-dev                   //url加载器

#CmtList.js中引入bootstrap样式
import bootcss from 'bootstrap/dist/css/bootstrap.css'

#使用bootstrap样式
import { Button } from 'reactstrap';
<!--下面这样用不行，因为bootstrap的css样式被模块化了-->
 <Button color="primary">primary</Button>{' '}
<!--下面这样用才行-->
<Button className={[bootcss.btn, bootcss['btn-primary']].join(' ')}>按钮</Button>

```

> 问题：如果都像上面那样使用bootstrap的样式，太麻烦了，我们期望引入bootstrap样式的时候还是<Button className="btn btn-primary">按钮啊</Button> 这样用，解决方案如下：

1. 把自己的样式表，定义为 `.less`文件

2. 第三方的 样式表，还是 以 `.css` 结尾

3. 我们只需要为自己的 .less文件，启用模块化即可；

4. 运行`npm i less less-loader -D` 安装能够解析`less`文件的loader

5. 添加loader规则：

   ```json
   //给less文件开启模块化
   {
       test: /\.less$/,
       use: [
           {
               loader: 'style-loader'
           },
           {
               loader: 'css-loader',
               options: {
                   modules: {
                       localIdentName: '[path][name]__[local]--[hash:base64:5]'
                   }
               }
           },
           {
               loader:'less-loader'
           }
       ]
   },
   
   ```

# 5.webpack配置详解

> 在实际开发中，一般会有两套项目方案：

- 一套是开发期间的项目，包含了测试文件、测试数据、开发工具、测试工具等相关配置，有利于项目的开发和测试，但是这些文件仅用于开发，发布项目时候需要剔除；
- 另一套是部署期间的项目，剔除了那些客户用不到的测试数据测试工具和文件，比较纯净，减少了项目发布后的体积，有利于安装和部署！

## 5.1 开发环境配置

```javascript
# 1.安装
npm init -y                                                       //项目初始化
npm install webpack@4.27.1 -d
npm install webpack-cli -d       提供一些基本命令(比如webpack命令)
npm install  webpack-dev-server -d
npm i html-webpack-plugin@3.2.0 --save-dev
npm install react react-dom -S
npm i babel-core@6.26.3 babel-loader@7.1.5 babel-plugin-transform-runtime --save-dev
npm i babel-preset-env babel-preset-stage-0 --save-dev
npm i babel-preset-react -D
npm install  style-loader  css-loader -D
npm i less-loader less                                             //less加载器
npm i sass-loader node-sass --save-dev               //sass加载器
npm i url-loader file-loader --save-dev      


#2.webpack.config.js
const path = require("path")
var htmlWebpackPlugin = require('html-webpack-plugin');
const webpack = require('webpack')


//webpack基于node构建的，所有用的是CommonJS模块化规范
module.exports = {
    mode: "development",
    entry: path.join(__dirname, './src/main.js'),
    output: {
        path: path.join(__dirname, './dist'),
        filename: 'bundle.js'
    },
    resolve: {
        // 表示，这几个文件的后缀名，可以省略不写
        extensions: ['.js', '.jsx', '.json'],
        alias: {
            '@': path.join(__dirname, './src')
        }
    },
    plugins: [
        // 添加plugins节点配置插件
        new htmlWebpackPlugin({
            template: path.resolve(__dirname, 'src/index.html'),//模板路径
            filename: 'index.html'//自动生成的HTML文件的名称
        }),
        //热更新的
        new webpack.HotModuleReplacementPlugin(), 
    ],
    module: { //要打包的第三方模块
        rules: [
            {
                test: /\.css$/,
                use: [
                    {
                        loader: 'style-loader'
                    },
                    {
                        loader: 'css-loader'
                    }
                ]
            },
            {
                test: /\.less$/,
                use: [
                    {
                        loader: 'style-loader'
                    },
                    {
                        loader: 'css-loader',
                        options: {
                            modules: {
                                localIdentName: '[path][name]__[local]--[hash:base64:5]'
                            }
                        }
                    },
                    {
                        loader: 'less-loader'
                    }
                ]
            },
            {
                test: /\.scss$/,
                use: [
                    {
                        loader: 'style-loader'
                    },
                    {
                        loader: 'css-loader',
                        options: {
                            modules: {
                                localIdentName: '[path][name]__[local]--[hash:base64:5]'
                            }
                        }
                    },
                    {
                        loader: 'sass-loader'
                    }
                ]
            },
            { test: /\.js|jsx$/, use: 'babel-loader', exclude: /node_modules/ },
            { test: /\.(png|jpg|gif|bmp|jpeg)$/, use: 'url-loader?limit=1024&name=[hash:8]-[name].[ext]' },
            { test: /\.(ttf|eot|svg|woff|woff2)$/, use: 'url-loader' }, // 处理 字体文件的 loader

        ]
    },
    devServer: {
        host: "127.0.0.1",
        open: true, // 自动打开浏览器
        port: 3000, // 设置启动时候的运行端口
        contentBase: 'src', // 指定托管的根目录
        hot: true // 启用热更新 的 第1步
    },
}

#3.项目入口文件  main.js
// 1. 导入包
import React from 'react'
import ReactDOM from 'react-dom'

import './css/index.css'


function Hello(props) {
    // props.name = 'zs'     不论是 Vue 还是 React，组件中的 props 永远都是只读的；不能被重新赋值;
    console.log(props)
    return <div><div className="box"></div>这是 Hello 组件 --- {props.name} --- {props.age} --- {props.gender}</div>
}

const dog = {
    name: '大黄',
    age: 3,
    gender: '雄'
}

ReactDOM.render(<div>
    {/* 使用{...obj}属性扩散传递数据 */}
    <Hello {...dog}></Hello>
</div>, document.getElementById('app'))

#4.index.html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <div id="app"></div>
</body>
</html>
                
#5.css/index.css
div{
    border: 1px solid red;
}

.box{
    width: 300px;
    height: 500px;
    background: url("../images/1.jpg");
} 

#6.package.json
 "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "dev": "webpack-dev-server --open --port 3000 --contentBase src --hot"
  }

#7.项目根目录 .babelrc
{
  "presets": ["env", "stage-0", "react"],
  "plugins": ["transform-runtime"]
}

```

## 5.2 生产环境配置文件

### a) 创建生产环境的配置文件

为了满足我们的发布策略，需要新建一个配置文件，命名为`webpack.publish.config.js`，将`webpack.config.js`的配置拷贝过去，剔除一些开发配置项即可：

- 将`devServer`节点和热更新插件删掉：

```javascript
devServer: {
    hot: true,
    open: true,
    port: 4321
}

new webpack.HotModuleReplacementPlugin()

```

1. 修改`url-loader`，将图片放入统一的images文件夹之下(**图片路径写在css文件中才会被打包，如果直接写在行内样式里面，不会被打包**)：

```javascript
{ test: /\.(png|jpg|gif)$/, use: 'url-loader?limit=5000&name=images/[hash:8]-[name].[ext]' }

```

2. 在`package.json`中的script节点下新增`dev`命令，通过`--config`指定webpack启动时要读取的配置文件：

```javascript
"pub": "webpack --config webpack.publish.config.js"

```

### b) 每次重新构建时候删除dist目录

1. 运行`npm i clean-webpack-plugin --save-dev`
2. 在头部引入这个插件：

```javascript
const {CleanWebpackPlugin } = require('clean-webpack-plugin');

```

3. 在`plugins`节点下使用这个插件：

```javascript
new CleanWebpackPlugin ()

```

### c) 分离第三方包

1. 和plugins节点平级添加下面配置：

```javascript
optimization: {
        splitChunks: {
            cacheGroups: {
                //自己写的代码打包 一个文件
                commons: {
                    name: "commons",
                    chunks: "initial",
                    //在分割之前，这个代码块最小应该被引用的次数
                    minChunks: 1,
                    //形成一个新代码块最小的体积
                    minSize: 0
                },
                //node_modules代码打包 一个文件
                vendor: {
                    chunks: "all",
                    test: /[\\/]node_modules[\\/]/,
                    name: "vendor",
                    minChunks: 1,
                    //入口最大的并行请求数
                    maxInitialRequests: 5,
                    // //形成一个新代码块最小的体积
                    minSize: 0,
                    //缓存组打包的先后优先级
                    priority: 100
                }
            }
        }
    },

```

3. `html-webpack-plugin`在生成`index.html`文件的时候，会自动将抽离的第三方包引入进去！

   ![1553329256785](http://m.qpic.cn/psc?/V1497zRn1XyhLI/uUnjQtxoKSmXQ5.YSnl4gADE*lKJuwJXfgL00DHe3h6pQvp0BSLU57YVQ2RS5nnAZCbGGVo2uchRbUF9Ak2ljA!!/b&bo=QgMoAEIDKAADCSw!&rf=viewer_4)

### d) 优化压缩HTML文件

在`plugins`节点下的`htmlWebpackPlugin`插件中，添加`minify`子节点：

```javascript
new htmlWebpackPlugin({
    template: path.join(__dirname, './src/index.html'),
    filename: 'index.html',
    //压缩合并html页面
    minify: {
        collapseWhitespace: true, // 合并多余的空格
        removeComments: true, // 移除注释
        removeAttributeQuotes: true // 移除 属性上的双引号
    }
}),

```

其他优化项请参考：[html-minifier - github](https://github.com/kangax/html-minifier#options-quick-reference)

![1553150762968](http://m.qpic.cn/psc?/V1497zRn1XyhLI/43eWRH6lLSncPe1pJhVzbTCGQApyh1bIUk2fsI73vShWr.HJ.IIjrTxEpTnABRoSAFcBA6FgVvWGUlQx4svXr.0zpzy8Vuy602YawXew8iw!/b&bo=VgKkAFYCpAADKQw!&rf=viewer_4)

### e) 抽取bundle.js中的CSS到指定文件

1. 运行`npm install extract-text-webpack-plugin@next `安装抽取CSS文件的插件。
2. 在配置文件中导入插件：

```javascript
const ExtractTextPlugin = require("extract-text-webpack-plugin");

```

3. 修改CSS和Sass的loader如下：

```json
{
    test: /\.css$/, use: ExtractTextPlugin.extract({
        fallback: "style-loader",
        use: ["css-loader"],
        publicPath: '../'         // 设置css背景图片的路径
    })
},
{
    test: /\.scss$/, use: ExtractTextPlugin.extract({
        fallback: "style-loader",
        use: [
            {
                loader: 'css-loader',
                options: {
                    modules: {
                        localIdentName: '[path][name]__[local]--[hash:base64:5]'
                    }
                }
            },
            {
                loader: 'sass-loader',
            }
        ],
        publicPath: '../'         // 设置css背景图片的路径
    })
},
{
    test: /\.less$/, use: ExtractTextPlugin.extract({
        fallback: "style-loader",
        use: [
            {
                loader: 'css-loader',
                options: {
                    modules: {
                        localIdentName: '[path][name]__[local]--[hash:base64:5]'
                    }
                }
            },
            {
                loader: 'less-loader',
            }
        ],
        publicPath: '../'         // 设置css背景图片的路径
    })
},

```

4. 在plugins节点下新增插件：

```javascript
new ExtractTextPlugin("css/styles.css"), // 抽取CSS文件的插件

```

### f) 压缩抽取出来的CSS文件

https://github.com/NMFR/optimize-css-assets-webpack-plugin

1. 运行`npm i optimize-css-assets-webpack-plugin --save-dev`安装插件到开发依赖。
2. 在配置文件头部导入插件：

```javascript
var OptimizeCssAssetsPlugin = require('optimize-css-assets-webpack-plugin');

```

3. 在plugins节点下新增插件：

```javascript
 new OptimizeCssAssetsPlugin() // 压缩CSS文件的插件

```

### g) 生产环境配置文件总结 

```javascript
# 新建webpack.pub.config.js

const path = require("path")

const htmlWebpackPlugin = require('html-webpack-plugin');
const {CleanWebpackPlugin } = require('clean-webpack-plugin');
const ExtractTextPlugin = require("extract-text-webpack-plugin");
const OptimizeCssAssetsPlugin = require('optimize-css-assets-webpack-plugin');

module.exports = {
    //生产环境
    mode:"production",
    entry: path.join(__dirname, './src/main.js'),
    output: {
        path: path.join(__dirname, './dist'),
        filename: 'bundle.js'
    },
    plugins: [ 
        // 添加plugins节点配置插件
        new htmlWebpackPlugin({
            template:path.resolve(__dirname, 'src/index.html'),//模板路径
            filename:'index.html',//自动生成的HTML文件的名称
            //压缩合并html页面
            minify: {
                collapseWhitespace: true, // 合并多余的空格
                removeComments: true, // 移除注释
                removeAttributeQuotes: true // 移除属性上的双引号
            }
        }),
        //每次发布项目的时候自动清除之前的dist目录
        new CleanWebpackPlugin (),
        new ExtractTextPlugin("css/styles.css"),
        new OptimizeCssAssetsPlugin() // 压缩CSS文件的插件
    ],
    module: { 
        rules: [
          { test: /\.(ttf|eot|svg|woff|woff2)$/, use: 'url-loader' }, 
          { test: /\.js|jsx$/, use: 'babel-loader', exclude: /node_modules/ },
          {
            test: /\.css$/, use: ExtractTextPlugin.extract({
                fallback: "style-loader",
                use: ["css-loader"],
                publicPath: '../'         // 设置css背景图片的路径
            })
          },
          {
            test: /\.scss$/, use: ExtractTextPlugin.extract({
                fallback: "style-loader",
                use: [
                    {
                        loader: 'css-loader',
                        options: {
                            modules: {
                            localIdentName: '[path][name]__[local]--[hash:base64:5]'
                            }
                        }
                    },
                    {
                        loader: 'sass-loader',
                    }
                ],
                publicPath: '../'         // 设置css背景图片的路径
            })
          },
          {
            test: /\.less$/, use: ExtractTextPlugin.extract({
                fallback: "style-loader",
                use: [
                    {
                        loader: 'css-loader',
                        options: {
                            modules: {
                            localIdentName: '[path][name]__[local]--[hash:base64:5]'
                            }
                        }
                    },
                    {
                        loader: 'less-loader',
                    }
                ],
                publicPath: '../'         // 设置css背景图片的路径
            })
          },

          //name=images/[hash:8]-[name].[ext]   发布项目的时候把图片都放到images文件夹下面去
          { test: /\.(png|jpg|gif|bmp|jpeg)$/, use: 'url-loader?limit=1024&name=images/[hash:8]-[name].[ext]' },
        ]
    },
    resolve: {
        extensions: ['.js', '.jsx', '.json'], // 表示这几个文件的后缀名，可以省略不写
        alias: {
            '@': path.join(__dirname, './src')
        }
    },
    optimization: {
        //分割代码块
        splitChunks: {
            cacheGroups: {
                //创建一个commons块，包含入口点共享的所有代码
                commons: {
                    name: "commons",
                    chunks: "initial",
                    //在分割之前，这个代码块最小应该被引用的次数
                    minChunks: 1,
                    //形成一个新代码块最小的体积
                    minSize: 0
                },
                //node_modules代码打包 一个文件
                vendor: {
                    chunks: "all",
                    test: /[\\/]node_modules[\\/]/,
                    name: "vendor",
                    minChunks: 1,
                    //形成一个新代码块最小的体积
                    minSize: 0
                }
            }
        }
    },
}

#package.json中新增
 "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "dev": "webpack-dev-server --open --port 3000 --contentBase src --hot",
    "pub": "webpack --config webpack.publish.config.js"
  }

```

# 6. React 事件处理

https://reactjs.org/docs/events.html

## 6.1 事件绑定

1. 事件的名称都是React的提供的，因此名称的首字母必须大写`onClick`、`onMouseOver`

2. 为事件提供的处理函数，必须是如下格式 

   ```javascript
   <button onClick={ function }>按钮</button>
   
   ```

3. 事件绑定方式：

   ```jsx
   #1.方式1：普通函数绑定
   <button onClick={ this.show }>按钮</button>
   
   // 事件的处理函数，需要定义为 一个箭头函数，然后赋值给 函数名称
   function show(){
       console.log("show方法")
       console.log(this)   //undefined
   }
   
   #2.方式2：箭头函数绑定(此种方式用的比较多)
   <button onClick={ () => this.show('传参') }>按钮</button>
   
   // 事件的处理函数，需要定义为 一个箭头函数，然后赋值给函数名称
   show = (arg1) => {
       console.log('show方法' + arg1)
       console.log(this)   //当前组件对象
   }
   
   ```



> 注意点：
>
> 1.在react中，箭头函数中的this就代表当前的组件对象，因为箭头函数的this其实质是定义函数时所在作用域中的this。
>
> 2.在react中，普通函数中的this是undefined。

## 6.2 修改事件的this并传递参数

```javascript
#方式1：使用bind修改普通函数中的this指向
import React, {Component} from 'react'

class Test extends React.Component {
    constructor (props) {
        super(props)
        this.state = {message: 'Allo!'}
    }

    handleClick (name, e) {
        console.log(this.state.message + name)
    }

    render () {
        return (
            <div>
                <button onClick={ this.handleClick.bind(this, '赵四') }>Say Hello</button>
            </div>
        )
    }
}


#方式2.在构造函数中通过bind修改this指向，返回新函数，然后在render中使用修改this指向后的新函数
import React, {Component} from 'react'

class Test extends React.Component {
    constructor (props) {
        super(props)
        this.state = {message: 'Allo!'}
        this.handleClick = this.handleClick.bind(this)
    }

    handleClick (e) {
        console.log(this.state.message)
    }

    render () {
        return (
            <div>
                <button onClick={ this.handleClick }>Say Hello</button>
            </div>
        )
    }
}


#方式3：使用箭头函数
class Test extends React.Component {
    constructor (props) {
        super(props)
        this.state = {message: 'Allo!'}
    }

    handleClick = (e) => {
        console.log(this.state.message)
    }

    render () {
        return (
            <div>
                <button onClick={ this.handleClick }>Say Hello</button>
            </div>
        )
    }
}


#注意：第二种和第三种方式如果这样用，<button onClick={ this.handleClick() }>Say Hello</button> ，此时会直接调用handleClick函数。如果想要点击按钮的时候才触发handleClick方法并且要给this.handleClick函数中传递参数，可以使用箭头函数<button onClick={ ()=>{this.handleClick('aa','bb')} }>Say Hello</button>。但一旦使用了箭头函数，那么箭头函数中的this就已经指向了当前的组件对象

```

## 6.3 绑定文本框与state中的值

1. 在Vue中提供了`v-model`指令，可以很方便的实现 `数据的双向绑定`；

2. 但是在React中只是`单向数据流`，也就是只能把state上的数据绑定到页面，无法把页面中数据的变化自动同步回 state ； 如果需要把页面上数据的变化保存到 state，则需要程序员手动监听`onChange`事件，拿到最新的数据，手动调用`this.setState({  })` 更改回去。 这种方式叫受控组件



### 6.3.1 表单受控组件

在 HTML 中，表单元素（如`<input>`、 `<textarea>` 和 `<select>`）之类的表单元素通常自己维护 state，并根据用户输入进行更新。而在 React 中，可变状态（mutable state）通常保存在组件的 state 属性中，并且只能通过使用 [`setState()`](https://zh-hans.reactjs.org/docs/react-component.html#setstate)来更新。

我们可以把两者结合起来，使 React 的 state 成为“唯一数据源”。渲染表单的 React 组件还控制着用户输入过程中表单发生的操作。被 React 以这种方式控制取值的表单输入元素就叫做“受控组件”。

```javascript
//如果文本框没有指定onChange事件，那么该文本框是只读的，不可以修改
render() {
    return (
        <input value="this.state.value" onChange={this.inputChange}/>
    )
}

inputChange = e => this.setState({value: e.target.value})  

```

### 6.3.2 表单非受控组件

在大多数情况下，我们推荐使用 [受控组件](https://zh-hans.reactjs.org/docs/forms.html#controlled-components) 来处理表单数据。在一个受控组件中，表单数据是由 React 组件来管理的。另一种替代方案是使用非受控组件，这时表单数据将交由 DOM 节点来处理。

```javascript
class NameForm extends React.Component {
  constructor(props) {
    super(props);
    this.handleSubmit = this.handleSubmit.bind(this);
    this.input = React.createRef();
  }

  handleSubmit(event) {
    alert('A name was submitted: ' + this.input.current.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Name:
          <input type="text" ref={this.input} />
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}

```

因为非受控组件将真实数据储存在 DOM 节点中，所以在使用非受控组件时，有时候反而更容易同时集成 React 和非 React 代码。如果你不介意代码美观性，并且希望快速编写代码，使用非受控组件往往可以减少你的代码量。否则，你应该使用受控组件。

### 6.3.3 受控组件和非受控组件

“受控”和“不受控制”的术语通常指的是表单输入，但他们还可以描述任何组件数据的位置。作为props传递进组件的数据可以被认为是**受控的**（因为父组件控制数据）。只存在于内部状态的数据可以被认为是**不受控制的**（因为父类不能直接更改它）。

## 6.4 React.createRef

### 6.4.1 为dom元素添加ref

`React.createRef` 创建一个能够通过 ref 属性附加到 React 元素的 [ref](https://zh-hans.reactjs.org/docs/refs-and-the-dom.html)。

```javascript
class CustomTextInput extends React.Component {
  constructor(props) {
    super(props);
    // 创造一个 textInput DOM 元素的 ref
    this.textInput = React.createRef();
  }
  render() {
    return (
      <input
        type="text"
        ref={this.textInput}
      />
    );
  }
  
   // 使用原始的 DOM API 显式地聚焦在 text input 上
   // 注意：我们通过访问 “current” 来获得 DOM 节点
   this.textInput.current.focus();
}

```

React 会在组件挂载时给 `current` 属性传入 DOM 元素，并在组件卸载时传入 `null` 值。`ref` 会在 `componentDidMount` 或 `componentDidUpdate` 生命周期钩子触发前更新。

### 6.4.2 为class组件添加ref

```javascript
class AutoFocusTextInput extends React.Component {
  constructor(props) {
    super(props);
    this.textInput = React.createRef();
  }

  componentDidMount() {
    this.textInput.current.focusTextInput();
  }

  render() {
    return (
      <CustomTextInput ref={this.textInput} />
    );
  }
}


class CustomTextInput extends React.Component {
  constructor(props) {
    super(props);
    // 创建一个 ref 来存储 textInput 的 DOM 元素
    this.textInput = React.createRef();
    this.focusTextInput = this.focusTextInput.bind(this);
  }

  focusTextInput() {
    // 直接使用原生 API 使 text 输入框获得焦点
    // 注意：我们通过 "current" 来访问 DOM 节点
    this.textInput.current.focus();
  }

  render() {
    // 告诉 React 我们想把 <input> ref 关联到
    // 构造器里创建的 `textInput` 上
    return (
      <div>
        <input
          type="text"
          ref={this.textInput} />
        <input
          type="button"
          value="Focus the text input"
          onClick={this.focusTextInput}
        />
      </div>
    );
  }
}

```

### 6.4.3 函数组件与ref

默认情况下，**你不能在函数组件上使用 ref 属性**，因为它们没有实例：

```javascript
function MyFunctionComponent() {
  return <input />;
}

class Parent extends React.Component {
  constructor(props) {
    super(props);
    this.textInput = React.createRef();
  }
  render() {
    // This will *not* work!
    return (
      <MyFunctionComponent ref={this.textInput} />
    );
  }
}

```

### 6.4.4 ref转发

如果要在函数组件中使用 `ref`，你可以使用 [`forwardRef`](https://zh-hans.reactjs.org/docs/forwarding-refs.html)，或者可以将该组件转化为 class 组件。

Ref 转发是一个可选特性，其允许某些组件接收 ref，并将其向下传递（换句话说，“转发”它）给子组件。

```javascript
const FancyButton = React.forwardRef((props, ref) => (
  <button ref={ref} className="FancyButton">
    {props.children}
  </button>
));

// 你可以直接获取 DOM button 的 ref：
const ref = React.createRef();
<FancyButton ref={ref}>Click me!</FancyButton>;


/*
    以下是对上述示例发生情况的逐步解释：
1.我们通过调用 React.createRef 创建了一个 React ref 并将其赋值给 ref 变量。
2.我们通过指定 ref 为 JSX 属性，将其向下传递给 <FancyButton ref={ref}>。
3.React 传递 ref 给 fowardRef 内函数 (props, ref) => ...，作为其第二个参数。
4.我们向下转发该 ref 参数到 <button ref={ref}>，将其指定为 JSX 属性。
5.当 ref 挂载完成，ref.current 将指向 <button> DOM 节点。
*/

```

## 6.5 ref回调

### 6.5.1 基本使用

不同于传递 `createRef()` 创建的 `ref` 属性，你会传递一个函数。这个函数中接受 React 组件实例或 HTML DOM 元素作为参数，以使它们能在其他地方被存储和访问。

```javascript
class CustomTextInput extends React.Component {
  constructor(props) {
    super(props);

    this.textInput = null;

    this.setTextInputRef = element => {
      this.textInput = element;
    };

    this.focusTextInput = () => {
      // 使用原生 DOM API 使 text 输入框获得焦点
      if (this.textInput) this.textInput.focus();
    };
  }

  componentDidMount() {
    // 组件挂载后，让文本框自动获得焦点
    this.focusTextInput();
  }

  render() {
    // 使用 `ref` 的回调函数将 text 输入框 DOM 节点的引用存储到 React
    // 实例上（比如 this.textInput）
    return (
      <div>
        <input
          type="text"
          ref={this.setTextInputRef}
        />
        <input
          type="button"
          value="Focus the text input"
          onClick={this.focusTextInput}
        />
      </div>
    );
  }
}

```

React 将在组件挂载时，会调用 `ref` 回调函数并传入 DOM 元素，当卸载时调用它并传入 `null`。在 `componentDidMount` 或 `componentDidUpdate` 触发前，React 会保证 refs 一定是最新的

### 6.5.2 父子之间传递回调ref

```javascript
function CustomTextInput(props) {
  return (
    <div>
      <input ref={props.inputRef} />
    </div>
  );
}

class Parent extends React.Component {
  render() {
    return (
      <CustomTextInput
        inputRef={el => this.inputElement = el}
      />
    );
  }
}

```

在上面的例子中，`Parent` 把它的 refs 回调函数当作 `inputRef` props 传递给了 `CustomTextInput`，而且 `CustomTextInput` 把相同的函数作为特殊的 `ref` 属性传递给了 `<input>`。结果是，在 `Parent` 中的 `this.inputElement` 会被设置为与 `CustomTextInput` 中的 `input` 元素相对应的 DOM 节点。

## 6.6 过时 API：String 类型的 Refs

如果你之前使用过 React，你可能了解过之前的 API 中的 string 类型的 ref 属性，例如 `"textInput"`。你可以通过 `this.refs.textInput` 来访问 DOM 节点。我们不建议使用它，因为 string 类型的 refs 存在 [一些问题](https://github.com/facebook/react/pull/8333#issuecomment-271648615)。它已过时并可能会在未来的版本被移除。

# 7 React组件的通信

## 7.1 父子组件的通信

### a) 父组件传递给子组件

```javascript
//父组件
<CMTItem key={i} {...item}</CMTItem>

//子组件通过this.props可以获取到父组件传递过来的数据

```

### b) 子组件传递给父组件

```javascript
//父组件
 <CMTBox reload={this.loadCmts}></CMTBox>

//子组件通过this.props.reload() 来调用父组件的方法，调用的时候可以传递参数

```

### c) 评论列表发表评论

```javascript
#1.CmtList.jsx
import React from 'react'
import CmtItem from './cmtItem'
import CmtBox from './cmtBox'

export default class CmtList extends React.Component {
    constructor() {
        super()
        this.state = {
            list: [
                { user: 'zs', content: '123' },
                { user: 'ls', content: 'qqq' },
                { user: 'xiaohong', content: 'www' }
            ]
        }
    }

    reload = (obj) => {
        this.setState((prev) => {
            return { list: [...prev.list, obj] }
        })
    }

    render() {
        return (<div>
            <h1>这是评论列表组件</h1>

            {
                this.state.list.map(item => (
                    <CmtItem key={item.user} {...item}></CmtItem>
                ))
            }

            <CmtBox reload={this.reload}></CmtBox>
        </div>)
    }
}

#2.CmtItem.jsx
import React from 'react'

export default (props) => {
    return (<div style={{ border: '1px solid #ccc', margin: '10px 0' }}>
        <h3>评论人：{props.user}</h3>
        <h5>评论内容：{props.content}</h5>
    </div>)
}

#3.CmtBox.jsx
import React from 'react'


export default class CmtBox extends React.Component {
    constructor(){
        super()
        this.state = {
            user:"",
            content:""
        }
    }

    //操作的是哪个文本框就去修改哪个文本框的数据
    changeHandler = (e)=>{
        var tag = e.currentTarget.id;
        this.setState({
            [tag]:e.currentTarget.value
        })
    }

    postComment = () => {
        if(this.state.user && this.state.content){
            this.props.reload({
                user: this.state.user,
                content: this.state.content
            })
            this.state.user = this.state.content = "" 
        }
    }

    render() {
        return (<div>
            <label htmlFor="user">用户名</label>
            <input id="user" type="text" value={this.state.user} onChange={this.changeHandler}></input>

            <label htmlFor="content">内容</label>
            <input id="content" type="text" value={this.state.content} onChange={this.changeHandler}></input>

            <input type="button" value="发表评论" onClick={() => this.postComment()} />
        </div>)
    }
}

```

## 7.2 使用Context实现跨组件通信

当你不想在组件树中通过逐层传递 `props`或者`state`的方式来传递数据时，可以使用`Context`来实现**跨层级**的组件数据传递。

### a) 父子组件传递数据的方式

![1553135155547](http://m.qpic.cn/psc?/V1497zRn1XyhLI/uUnjQtxoKSmXQ5.YSnl4gMjQsVgQLv*SL8WsrhSKMS8TfGYBtNiyMsQKS7PtlMOLUSHY7OnuH359QfPOG50HDA!!/b&bo=fwJjAX8CYwEDCSw!&rf=viewer_4)

### b) 使用Context跨级传递数据

![1553135231745](http://m.qpic.cn/psc?/V1497zRn1XyhLI/43eWRH6lLSncPe1pJhVzba2qafoyOfmrgSPvVD4cI9P*sWLN4PNv7O6xVecQzIWmPYIb8sr90nJ3BHG48VKwoepwid3zxEmPMwUNPzBa2C4!/b&bo=fQKlAX0CpQEDGTw!&rf=viewer_4)

```javascript
import React from 'react'

//创建一个Context对象
const ThemeContext = React.createContext("light")

export default class ContextComp extends React.Component {
    constructor() {
        super()
    }

    render() {
        //ThemeContext.Provider 数据的提供者，允许消费组件订阅context的变化
        //value就是给子组件暴露的数据
        return (<ThemeContext.Provider value={{name:"zhangsan"}}>
            <ThemedButton></ThemedButton>
        </ThemeContext.Provider>)
    }
}


class ThemedButton extends React.Component {
    //这能让你使用 this.context 来消费最近 Context 上的那个值
    static contextType = ThemeContext;
    render() {
        return <div>
            <Content></Content>
            <button>{this.context.name}</button>
        </div>
    }
}

//ThemeContext.Consumer 允许我们在函数组件中使用Context
//ThemeContext.Consumer中的箭头函数的入参就是最近一个Provider所暴露的数据
function Content() {
    return (<ThemeContext.Consumer>{
        obj => {
            return <div>{obj.name}</div>
        }
    }</ThemeContext.Consumer>)
}

```

## 7.3 使用自定义事件实现组件通讯

在没有嵌套关系的组件中，我们可以使用自定义事件的方式实现组件通信。

> 1.在componentDidMount事件中，订阅事件
>
> 2.在组件卸载的时候，在componentWillUnmount事件中取消事件的订阅;
>
> 3.以常用的发布/订阅模式，借用Node.js Events模块的浏览器版实现

```javascript
npm install events --save

```

在src下新建一个util目录里面建一个events.js

```javascript
import { EventEmitter } from 'events';

export default new EventEmitter();

```

list1.jsx

```javascript
import React, { Component } from 'react';
import emitter from '../util/events';

class List extends Component {
    constructor(props) {
        super(props);
        this.state = {
            message: 'List1',
        };
    }
    componentDidMount() {
        // 组件装载完成以后声明一个自定义事件
        this.eventEmitter = emitter.addListener('changeMessage', (message) => {
            this.setState({
                message,
            });
        });
    }
    componentWillUnmount() {
        emitter.removeListener(this.eventEmitter);
    }
    render() {
        return (
            <div>
                {this.state.message}
            </div>
        );
    }
}

export default List;

```

List2.jsx

```javascript
import React, { Component } from 'react';
import emitter from '../util/events';

class List2 extends Component {
    handleClick = (message) => {
        emitter.emit('changeMessage', message);
    };
    render() {
        return (
            <div>
                <button onClick={this.handleClick.bind(this, 'List2')}>点击我改变List1组件中显示信息</button>
            </div>
        );
    }
}

```

App.jsx

```javascript
import React, { Component } from 'react';
import List1 from './components/List1';
import List2 from './components/List2';


export default class App extends Component {
    render() {
        return (
            <div>
                <List1 />
                <List2 />
            </div>
        );
    }
}

```

自定义事件是典型的发布订阅模式,通过向事件对象上添加监听器和触发事件来实现组件之间的通信

# 8. React组件的生命周期

## 8.1 生命周期钩子函数介绍

- 生命周期的概念：每个组件的实例，从创建、运行、到销毁，在这个过程中会出发一些列事件，这些事件就叫做组件的生命周期函数；

- React组件生命周期(React 16.4+)分为三部分：

  - **组件创建阶段**：

  > static 开头的     只会执行一次
  >
  > constructor    构造器     只会执行一次
  >
  > getDerivedStateFromProps: 每次re-rendering之前被调用，作用：将传递的props映射到state里面       会执行多次
  >
  > render           构建虚拟dom，但是此时虚拟dom还没有渲染到页面        会执行多次
  >
  > componentDidMount:组建的虚拟dom已经挂载到页面                      只会执行一次

  - **组件运行阶段**：根据 props 属性 或 state 状态的改变，有选择性的执行0到多次

  > getDerivedStateFromProps:每次re-rendering之前被调用
  >
  > shouldComponentUpdate:组件是否需要被更新，返回值是true或者false。此时可以获取最新的props和state数据
  >
  > render: 重新更新渲染组件的虚拟dom
  >
  > getSnapshotBeforeUpdate：在最近一次渲染提交到 DOM 节点之前调用。它的含义是在React更新Dom元素之前，获取一个快照，它返回的结果将作为componentDidUpdate的第三个参数。一般的用法就是获取更新前的DOM。
  >
  > componentDidUpdate: 组件完成了更新，此时页面已经是最新的了

  - **组件卸载阶段**：只执行一次

  > componentWillUnmount: 当组件从 DOM 中移除时会调用如下方法，此时组件还可以被使用
  >
  > ![1574654437154](http://m.qpic.cn/psc?/V1497zRn1XyhLI/uUnjQtxoKSmXQ5.YSnl4gPjui2ExyNQ6tAUPSRsMPbxlUiO.Qhv31fANkIbypRGCpphlrTGDlQlFkiip.Vl8xg!!/b&bo=EAMYAhADGAIDCSw!&rf=viewer_4)

React生命周期的回调函数总结成表格如下：
![1574666830021](http://m.qpic.cn/psc?/V1497zRn1XyhLI/43eWRH6lLSncPe1pJhVzbUoFAroECW*jspuWyR2qPkgo7VIgkVQb1iR1NfiVjMAK9C3iY9W6wtHTFXmKyg3fyQ9ZBTmU*9Ah1K*pM8VNbjE!/b&bo=nQMwAp0DMAIDGTw!&rf=viewer_4)

## 8.2 defaultProps及类型校验

### 8.2.1 prop-types

```javascript
import PropTypes from 'prop-types';

MyComponent.propTypes = {
  // 你可以声明一个 prop 是一个特定的 JS 原始类型。 默认情况下，这些都是可选的。
  optionalArray: PropTypes.array,
  optionalBool: PropTypes.bool,
  optionalFunc: PropTypes.func,
  optionalNumber: PropTypes.number,
  optionalObject: PropTypes.object,
  optionalString: PropTypes.string,
  optionalSymbol: PropTypes.symbol,

  // 任何东西都可以被渲染:numbers, strings, elements,数组或者是包含这些类型的片段。
  optionalNode: PropTypes.node,

  // 一个 React 元素  例如 <MyComponent />
  optionalElement: PropTypes.element,

  // 你也可以声明一个 prop 是类的一个实例。 
  // 使用 JS 的 instanceof 运算符。
  optionalMessage: PropTypes.instanceOf(Message),

  // 你可以声明 prop 是特定的值，类似于枚举
  optionalEnum: PropTypes.oneOf(['News', 'Photos']),

  // 一个对象可以是多种类型其中之一
  optionalUnion: PropTypes.oneOfType([
    PropTypes.string,
    PropTypes.number,
    PropTypes.instanceOf(Message)
  ]),

  // 一个某种类型的数组
  optionalArrayOf: PropTypes.arrayOf(PropTypes.number),

  // 属性值为某种类型的对象
  optionalObjectOf: PropTypes.objectOf(PropTypes.number),

  // 一个特定形式的对象
  optionalObjectWithShape: PropTypes.shape({
    color: PropTypes.string,
    fontSize: PropTypes.number
  }),

  // 你可以使用 `isRequired' 链接上述任何一个，以确保在没有提供 prop 的情况下显示警告。
  requiredFunc: PropTypes.func.isRequired,

  // 任何数据类型的值
  requiredAny: PropTypes.any.isRequired,
}

```

### 8.2.2 defaultProps

```javascript
class Counter extends React.Component {
    //  组件创建的时候，会先执行static开头的属性和方法
    //  静态属性：设置props的初始值(在使用当前组件的时候，没有给当前组件传递props的时候，该初始值会生效)
    static defaultProps = {
        initcount: 1000
    }
    static propTypes = {
        // 使用 prop-types 包 来定义 initcount 为 number 类型
        // isRequired 表示这个props属性是必须要传递的
        initcount: ReactTypes.number.isRequired
    }
    ........
 }

```

## 8.3 生命周期函数详解

> 在组件创建之前，会先初始化默认的props属性，这是全局调用一次，严格地来说，这不是组件的生命周期的一部分。

```javascript
#1.Counter.jsx
import React from 'react'
import ReactTypes from 'prop-types'


export default class Counter extends React.Component {
    //-------------------------------组件创建阶段----------------------------------------
    //1.在组件的创建阶段：第一个执行的是static开头的属性
    //设定props的默认值：当父组件没有给子组件传递props的时候就会使用这个默认值
    static defaultProps = {
        initCount: 100
    }

    //约定props的类型
    //PropTypes.number 表示是一个数值类型
    //isRequired 表示必须要有一个初始值
    static propTypes = {
        initCount: PropTypes.number.isRequired
    }

    //2.在组件创建阶段，第二个执行的是构造函数 (创建一个组件对象执行一次)
    //构造函数的作用：主要就是用来创建组件对象
    //我们可以在构造函数中声明当前组件的state
    constructor() {
        super()
        console.log("constructor方法执行了")
        this.state = {
            msg: "张三"
        }

        //构造函数中只可以给state赋予初始值，不能够通过setState()来修改state的值
        // this.setState({
        //     msg:"李四"
        // })
    }

    //3.在组件的创建阶段，第三个执行的是getDerivedStateFromProps
    //这个方法的作用：就是将props映射到state中
    //在每一次re-render的时候执行
    /*
    static getDerivedStateFromProps(nextProps, prevState){

    }
    */

    //4.在组件的创建阶段，第四个执行的是render()方法。(在一个组件的各种生命周期阶段中，至少执行一次)
    //render()方法的主要作用：在内存中构建虚拟dom(此时虚拟dom还没有被挂载到页面)
    render() {
        return (<div>
            {
                // 在render()函数中不能通过setState()来修改state状态，因为这样会陷入死循环
                // 其实render()函数应该是一个纯函数，这个函数的作用本身就是给他什么数据，他就显示什么数据

                // this.setState({
                //     msg:"李四"
                // })
            }
            {console.log("render方法执行了")}
            这是counter组件 {this.state.msg}
            <p>当前数量:{this.props.initCount}</p>
        </div>)
    }

    //5.在组件的创建阶段，第五个执行的是componentDidMount。(创建一个组件对象执行一次)
    //componentDidMount执行的时候就表示内存中的虚拟dom已经挂载到页面了，此时页面是最新的
    //只有componentDidMount()钩子函数才可以通过setState()来修改state
    componentDidMount() {
        //componentDidMount()方法允许我们通过setState()来修改状态
        this.setState({
            msg: "李四"
        })
        console.log("componentDidMount方法执行了")
    }

    //-------------------------------组价的运行阶段-------------------------------
    //当前组件的状态发生改变之后，会进入组件的运行阶段
    //1.在组件运行阶段，第一个执行的函数是getDerivedStateFromProps
    /*
    static getDerivedStateFromProps(nextProps, prevState){

    }
    */

    //2.在组件的运行阶段，第二个执行的函数是shouldComponentUpdate。(在组件的各种生命周期阶段中，执行>=0次)
    //作用：让程序员手动控制是否要更新组件
    //如果这个方法返回false，就不会更新组件(后续的生命周期函数就不会执行了)；如果这个方法返回true，就会更新组件(后续的生命周期会执行)
    shouldComponentUpdate(nextProps, nextState) {
        // shouldComponentUpdate() 方法中也不能通过setState()来更改state，此时仍然会进入死循环
        // this.setState({
        //     msg:"王五"
        // })
        console.log("shouldComponentUpdate")
        return true;
    }

    //3.在组件的运行阶段，第三个执行的函数是render()函数
    //render()函数的作用：在内存中构建虚拟dom(此时虚拟dom还没有被挂载到页面)

    //4.在组件的运行阶段，第四个执行的函数是getSnapshotBeforeUpdate。(在组件的各种生命周期阶段中，执行>=0次)
    //主要作用：获取更新页面之前的dom信息
    //这个方法的返回值会作为componentDidUpdate()方法第三个参数入参
    //https://react.docschina.org/docs/react-component.html
    getSnapshotBeforeUpdate() {
        // getSnapshotBeforeUpdate() 方法中也不能通过setState()来更改state，此时仍然会进入死循环
        // this.setState({
        //     msg:"王五"
        // })
        console.log("getSnapshotBeforeUpdate")
        return { aa: 123 }
    }

    //5.在组件的运行阶段，第五个执行的函数是componentDidUpdate。(在组件的各种生命周期阶段中，执行>=0次)
    //主要作用：虚拟dom已经挂载到页面，此时页面是最新的
    componentDidUpdate(prevProps, prevState, snapshot) {
        // componentDidUpdate() 方法中也不能通过setState()来更改state，此时仍然会进入死循环
        // this.setState({
        //     msg: "王五"
        // })
        console.log("componentDidUpdate", snapshot)
    }

    //----------------------------组件的卸载阶段-----------------------------
    //可以在componentWillUnmount()方法中进行一些资源的释放工作。比如关闭定时器、移除事件监听。(卸载一个组件执行一次)
    componentWillUnmount() {
        console.log("componentWillUnmount")
    }
}



#App.jsx
import React from 'react'
import Counter from '@/components/counter'

export default class App extends React.Component {
    constructor(){
        super()
        this.state = {
            count:1
        }
    }

    handleClick = ()=>{
        this.setState(prev=>{
            return {
                count:++prev.count
            }
        })
    }

    render() {
        return (<div>
            这是App组件
            <Counter initCount={this.state.count}></Counter>
            <Counter></Counter>
            <button onClick={this.handleClick}>改变count</button>
        </div>)
    }
}

```

## 8.4 组件的重新渲染和优化

组件的重新渲染的执行时机：

> 1.组件重新被创建
>
> 2.当前组件的state发生变化
>
> 3.父组件的state发生变化

也就是说父组件和当前组件的state发生任何变化，都会引起组件的re-render，进而触发一系列的生命周期钩子(getDerivedStateFromProps\shouldComponentUpdate\render\getSnapshotBeforeUpdate\componentDidMount\componentDidUpdate)。

当我们在父组件修改了与子组件无关的state，发现子组件也会re-render，这个时候就需要借助shouldComponentUpdate钩子函数来做优化。

### 8.4.1 shouldComponentUpdate优化

```javascript
//作用：让程序员手动控制是否要更新组件
//如果这个方法返回false，就不会更新组件(后续的生命周期函数就不会执行了)；如果这个方法返回true，就会更新组件(后续的生命周期会执行)
shouldComponentUpdate(nextProps, nextState) {
    console.log("shouldComponentUpdate",nextProps,this.props)
    //如果下次传递过来的initCount和当前组件props中所保持的initCount一致的时候，此时就没有必要做组件re-render
    if(nextProps.initCount == this.props.initCount){
        return false;
    }
    return true;
}

```

### 8.4.2 PureComponent优化

```javascript
//方式二：使用PureComponent类 
import React from 'react'
class ListOfWords extends React.PureComponent {
    render() {
        return <div>
            {console.log("render")}
            {this.props.words.join(',')}
        </div>;
    }
}
export default ListOfWords


//App.js
import React from 'react'
import ListOfWords from '@/components/listOfWords'

export default class App extends React.Component {
    constructor() {
        super()
        this.state = {
            words: ['marklar']
        };
    }

    handleClick = () => {
        var words = this.state.words;
        words.push("marklar");

        //因为PureComponent对于引用类型而言，比较的是内存地址是否一致
        //所以我们修改state的时候，需要给words赋值一个新的数组，此时新数组和原来数组的内存地址肯定不一致，从而组件才可能更新
        this.setState({
            words:[...words] 
        })
    }

    render() {
        return (<div>
            这是App2组件
            <ListOfWords words={this.state.words}></ListOfWords>
            <button onClick={this.handleClick}>添加words</button>
        </div>)
    }
}
/*
1.继承PureComponent时，不能再重写shouldComponentUpdate
2.继承PureComponent时，进行的是浅比较，也就是说，如果是引用类型的数据，只会比较是不是同一个地址，而不会比较具体这个地址存的数据是否完全一致
3.上面代码中，无论你怎么点击按钮，ListOfWords渲染的结果始终没变化，原因就是WordAdder的word的引用地址始终是同一个。
4.我们可以这样修改state，此时页面会发生变化，因为给words赋值了一个新对象
   this.setState({words:[...words]});
*/

```

## 8.5 getDerivedStateFromProps存在的问题

```javascript
//getDerivedStateFromProps 函数会在每次re-rendering之前被调用

//为什么要用getDerivedStateFromProps？答案：组件接收的props数据是只读的，我们可以使用该方法将传递的props映射到state里面，实现修改(会有诸多问题)
//注意点：该方法是一个静态方法，方法中没有this，故而不可以直接通过this.setState()来改变状态，而是需要通过return来改变状态

//参数：
//1.nextProps外部传递过来的props属性
//2.prevState之前的state状态

static getDerivedStateFromProps(nextProps, prevState) {
    console.log("getDerivedStateFromProps", nextProps, prevState)
    //获取到父组件中传递过来的initcount值
    const { initcount } = nextProps;
    //当父组件中传递过来的initcount发生改变了
    if (initcount != prevState.prevCount) {
        //在方法中返回{count:initcount} 替换掉当前state中的 count值
        return {
            count: initcount,
            prevCount:initcount
        }
    }
    //如果props传入的内容不需要影响到你的state，那么就需要返回一个null
    return null
}


//问题：
1.当前组件的状态由多个源控制，父组件中控制列表数据，子组件中又控制了type这个state。
因此父组件state改掉之后，会触发子组件重新渲染；本身组件state改掉之后，会触发当前组件重新渲染

2.如果你的组件内部既需要修改自己的type，又需要接收从外部修改的type。逻辑非常混乱！getDerivedStateFromProps中你根本不知道该做什么。

if (initcount != prevState.prevCount) {
    //在方法中返回{count:initcount} 替换掉当前state中的 count值
    return {
        count: initcount,
        prevCount:initcount
    }
}

如果彻底解决这个问题呢？
答案：好好组织你的组件，在非必须的时候，摒弃这种写法(派生属性)。type要么由props驱动，要么完全由state驱动。

从这个生命周期的更新来看，react更希望将受控的props和state进行分离，就如同Redux作者Dan Abramov在redux文档当中写的一样Presentational and Container Components，将所有的组件分离称为展示型组件和容器型组件，一个只负责接收props来改变自己的样式，一个负责保持其整个模块的state。这样可以让代码更加清晰。但是在实际的业务逻辑中，我们有时很难做到这一点，而且这样可能会导致容器型组件变得非常庞大以致难以管理，如何进行取舍还是需要根据实际场景决定的

```

## 8.6 React老版本生命周期

![3284159097-5bbb08d17db33_articlex](/REACT框架/3284159097-5bbb08d17db33_articlex-1584956954768.png)

# 9. React-router

## 9.1 前端路由的两种实现方案

1. hash : hash原本的作用是为一个很长的文档页添加锚点信息，它自带不改变url刷新页面的功能，所以自然而然被用单页面应用程序中了。

2. history : 应该说history是主流的解决方案，浏览器的前进后退用的就是这个，它是window对象下的，以前的history提供的方法只能做页面之间的前进后退，如下：

   ```javascript
   history.go(number|URL) 可加载历史列表中的某个具体的页面
   history.forward() 可加载历史列表中的下一个 URL
   history.back() 可加载历史列表中的前一个 URL
   
   ```

   为了在不刷新浏览器的情况下，创建新的浏览记录并插入浏览记录队列中，html5新增了如下方法：

   ```
   1. history.pushState(state, title, url)
      添加一条历史记录， state用于传递参数，可以为空。title是设置历史记录的标题，可以为空。url是历史记录的URL，不可以为空。
   
   2.history.replaceState(state, title, url)
   将history堆栈中当前的记录替换成这里的url，参数同上。
   
   这个特性后来用到了单页面应用中比如：vue-router，react-router-dom里面。
   
   ```

## 9.2 Reac中的路由

`<Router>`是React中实现路由最外层的容器，一般情况下我们不再需要直接使用它，而是使用在它基础之上封装的几个适用于不同环境的组件，react-router-dom的Router有四种：

| Router                                                       | 适用情况                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [BrowserRouter](https://link.jianshu.com?t=https%3A%2F%2Freacttraining.com%2Freact-router%2Fweb%2Fapi%2FBrowserRouter) | react-router-dom扩展，利用HTML5 新增的history API (pushState, replaceState)，是web应用最常用的路由组件 |
| [HashRouter](https://link.jianshu.com?t=https%3A%2F%2Freacttraining.com%2Freact-router%2Fweb%2Fapi%2FHashRouter) | react-router-dom扩展，利用window.location.hash，适用于低版本浏览器或者一些特殊情境 |
| [MemoryRouter](https://link.jianshu.com?t=https%3A%2F%2Freacttraining.com%2Freact-router%2Fweb%2Fapi%2FMemoryRouter) | 继承自react-router ，用户在地址栏看不到任何路径变化，一般用在测试或者非浏览器环境开发中 |
| [StaticRouter](https://link.jianshu.com?t=https%3A%2F%2Freacttraining.com%2Freact-router%2Fweb%2Fapi%2FStaticRouter) | 继承自react-router，某些页面从渲染出来以后没有多的交互，所以没有状态的变化需要存储，就可以使用静态路由，静态路由适用于服务器端 |

一般我们很少会用到MemoryRouter和StaticRouter，在web应用中更多的是用   `react-router-dom`扩展出来的BrowserRouter和HashRouter，这两个就是我前面提到的前端路由的两种解决办法的各自实现。

## 9.3 HashRouter的基本使用

```javascript
npm install react-router-dom -S

#1.main.js 
// 1. 导入包
import React from 'react'
import ReactDOM from 'react-dom'

import App from './App.jsx'

// 使用 render 函数渲染 虚拟DOM
ReactDOM.render(<App></App>, document.getElementById('app'))
                

#2.App.jsx
import React from 'react'

// HashRouter 表示一个路由的跟容器，所有的路由相关的东西，都要包裹在 HashRouter 里面
// Route 表示一个路由规则， 在 Route 上有两个比较重要的属性：path   component
// Link 表示一个路由的链接 ，就好比 vue 中的 <router-link to=""></router-link>
import { HashRouter, Route, Link } from 'react-router-dom'

import Home from './components/Home.jsx'
import Movie from './components/Movie.jsx'
import About from './components/About.jsx'

export default class App extends React.Component {
  constructor(props) {
    super(props)
    this.state = {}
  }

  render() {
    // 当 使用 HashRouter 把 App 根组件的元素包裹起来之后，网站就已经启用路由了
    // 在一个 HashRouter 中，只能有唯一的一个根元素
    // 在一个网站中，只需要使用 唯一的一次 <HashRouter></HashRouter> 就行了
    return <HashRouter>
      <div>
        <h1>这是网站的APP根组件</h1>
      
        <Link to="/home">首页</Link>&nbsp;&nbsp;
        <Link to="/movie/top250/10">电影</Link>&nbsp;&nbsp;
        <Link to="/about">关于</Link>

        <hr />

        {/* Route 创建的标签，就是路由规则，其中 path 表示要匹配的路由，component 表示要展示的组件 */}
        {/* 在 vue 中有个 router-view 的路由标签专门用来放置匹配到的路由组件的，但是在 react-router 中并没有类似于这样的标签，而是直接把 Route 标签当作的坑（占位符） */}
        {/* Route 具有两种身份：1. 它是一个路由匹配规则； 2. 它是一个占位符，表示将来匹配到的组件都放到这个位置， 如果想让路由规则进行精确匹配，可以为 Route添加 exact 属性，表示启用精确匹配模式 */}
        <Route path="/home" component={Home}></Route>

        <hr />

        {/* 注意：默认情况下，路由中的规则是模糊匹配的，如果路由可以部分匹配成功，就会展示这个路由对应的组件 */}
        {/* 如果要匹配参数，可以在匹配规则中使用 : 修饰符，表示这个位置匹配到的是参数 */}
        <Route path="/movie/:type/:id" component={Movie} exact></Route>

        <hr />

        <Route path="/about" component={About}></Route>
      </div>
    </HashRouter>
  }
}

#3.components/Home.jsx    
import React from 'react'

export default class Home extends React.Component {
  constructor(props) {
    super(props)
    this.state = {}
  }

  render() {
    return <div>
      Home
    </div>
  }
}



#4. components/Movie.jsx 
import React from 'react'

export default class Movie extends React.Component {
  constructor(props) {
    super(props)
  }

  render() {
    console.log(this);
    // 如果想要从路由规则中，提取匹配到的参数进行使用，可以使用 this.props.match.params.*** 来访问
    return <div>
      Movie --- {this.props.match.params.type} --- {this.props.match.params.id}
    </div>
  }
}


#5. components/About.jsx
import React from 'react'

export default class About extends React.Component {
  constructor(props) {
    super(props)
    this.state = {}
  }

  render() {
    return <div>
      About
    </div>
  }
}

```

## 9.4 匹配规则

**默认：**

| 路径 | location.pathname | 是否匹配 |
| ---- | ----------------- | -------- |
| /one | /one              | 是       |
| /one | /one/             | 是       |
| /one | /one/111          | 是       |
| /one | /one/aaa/bbb      | 是       |

**exact配置：**exact属性为true时路径中的hash值必须和path完全一致才渲染对应的组件，如果为false则'/'也可以匹配'/xxx'

| 路径 | location.pathname | exact | 是否匹配 |
| ---- | ----------------- | ----- | -------- |
| /one | /one/two          | true  | 否       |
| /one | /one/two          | false | 是       |

**strict配置：**strict属性主要就是匹配反斜杠，规定是否匹配末尾包含反斜杠的路径，如果strict为true，则如果path中不包含反斜杠结尾，则他也不能匹配包含反斜杠结尾的路径

| 路径  | location.pathname | strict | 是否匹配 |
| ----- | ----------------- | ------ | -------- |
| /one/ | /one              | true   | 否       |
| /one/ | /one/             | true   | 是       |
| /one/ | /one/two          | true   | 是       |

## 9.5 Switch和Redirect

```javascript
import { HashRouter, Route, Link, Switch,Redirect} from 'react-router-dom'

render() {
        return (
            <HashRouter>
                {/*
                Switch表示路由互斥，如果没有Switch，会根据路由找到所有匹配的组件显示
                比如http://localhost:3000/#/user  会找到/、/user所匹配的路由(下面home没有找到是因为精确匹配了)
                */}
                <Switch>
                    {/*
                    path:/ 表示访问根路径的情况下默认载入home组件
                    exact精确匹配，为了给其他组件一个机会获取到url改变
                    */}
                    <Route path='/' exact  component={Home}/>
                    <Route path='/city' component={City}/>
                    {/*
                    strict 在确定路径是否与当前URL匹配时，将考虑路径后的斜线；
                    */}
                    <Route path='/login/' strict component={Login}/>
                    <Route path='/user' component={User}/>
                    <Route path='/search/:category/' strict component={Search}/>
                    <Route path='/detail/:id' component={Detail}/>
                    {/*没有匹配到路径的时候重定向到根路径*/}
                    <Redirect to="/" />
                </Switch>
            </HashRouter>
        )
    }

```

## 9.6 React中的编程式导航和路由传参

### 9.6.1 withRouter的使用

withRouter可以包装任何自定义组件，将react-router 的 history,location,match 三个对象传入。 

```javascript
 <Route exact path="/Home" component={Home}/>

```

>  1.只有包裹在Route组件里的才能使用`this.props.location`，
>  2.假如有个需求，是面包屑或者导航组件里需要拿到`this.props.location`（导航组件或者面包屑一般不会包裹在`Route`里），那么直接这么写显然就不行了。
>  这个时候`withRouter`修饰一下，就可以这么写了。

### 9.6.2 使用withRouter跳转页面

> 只有在 <Route> 包裹的组件中才能在 this.props 属性中找到 history 对象。但有些情况下我们就是希望在一个没被 <Route> 包裹的组件中用到 history 对象，我们可以这样用

```javascript
import { withRouter } from 'react-router-dom'

export default withRouter(YourComponent)

//此时就可以在组件中使用this.props.history跳转路由了
this.props.history.push({pathname:"/path/"});

```

### 9.6.3 路由传参

#### a) params方式传参

```javascript
<Route path='/path/:name' component={Path}/>

<Link to="/path/2">xxx</Link>
this.props.history.push({pathname:"/path/" + name});

读取参数用:this.props.match.params.name

```

优势 ： 刷新地址栏，参数依然存在
缺点  :   只能传字符串，并且如果传的值太多的话，url会变得长而丑陋。

#### b) query方式传参

```javascript
<Route path='/query' component={Query}/>

<Link to={{ pathname : ' /query' , query : { name : 'sunny' }}}>
this.props.history.push({pathname:"/query",query: { name : 'sunny' }});

读取参数用: this.props.location.query.name

```

优势：传参优雅，传递参数可传对象；
缺点：刷新地址栏，参数丢失

#### c) state方式传参

```javascript
<Route path='/sort ' component={Sort}/>

<Link to={{ pathname : ' /sort ' , state : { name : 'sunny' }}}> 
this.props.history.push({pathname:"/sort ",state : { name : 'sunny' }});

读取参数用: this.props.location.state.name 

```

优势：传参优雅，传递参数可传对象，state传的参数是加密的
缺点：刷新地址栏，参数丢失

#### d) search方式传参

```javascript
<Route path='/web/departManange ' component={DepartManange}/>

<link to="web/departManange?tenantId=12121212">xxx</Link>
this.props.history.push({pathname:"/web/departManange",search: 'tenantId=12121212'})

读取参数用: this.props.location.search


//search参数的解析
npm install --save url

httpUrl = this.props.location.search;
url.parse(httpUrl, true).query.tenantId;

```

优势 ： 刷新地址栏，参数依然存在

缺点  :   只能传字符串，并且如果传的值太多的话，url会变得长而丑陋。

## 9.7 组件懒加载

`React.lazy` 函数能让你像渲染常规组件一样处理动态引入（的组件）。

`React.lazy` 接受一个函数，这个函数需要动态调用 `import()`。它必须返回一个 `Promise`，该 Promise 需要 resolve 一个 `defalut` export 的 React 组件。

然后应在 `Suspense` 组件中渲染 lazy 组件(Suspense 就是实现所谓的延迟加载效果)，如此使得我们可以使用在等待加载 lazy 组件时做优雅降级（如 loading 指示器等）。

```javascript
import React, { Suspense } from 'react';

const OtherComponent = React.lazy(() => import('./OtherComponent'));

function MyComponent() {
  return (
    <div>
      <Suspense fallback={<div>Loading...</div>}>
        <OtherComponent />
      </Suspense>
    </div>
  );
}

```

## 9.8 基于路由的代码分割

```javascript
import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';
import React, { Suspense, lazy } from 'react';

const Home = lazy(() => import('./routes/Home'));
const About = lazy(() => import('./routes/About'));

const App = () => (
  <Router>
    //fallback 属性接受任何在组件加载过程中你想展示的 React 元素
    <Suspense fallback={<div>Loading...</div>}>
      <Switch>
        <Route exact path="/" component={Home}/>
        <Route path="/about" component={About}/>
      </Switch>
    </Suspense>
  </Router>
);

```

# 10.ReactTransitionGroup动画

<https://reactcommunity.org/react-transition-group/>

react-transition-group 一个官网提供的动画过度库。

```
# npm
npm install react-transition-group --save

# yarn
yarn add react-transition-group

```

而官方提供的四个组建`Transition`，`CSSTransition`，`SwitchTransiton`，`TransitonGroup`。

## 10.1 Transition

过渡组件(Transiton)允许您用一个简单的声明性API描述随着时间的推移从一个组件状态到另一个组件状态的转换。最常用的是用来动画一个组件的安装和卸载，但也可以用来描述在适当的过渡状态。默认情况下，该组件不会更改其呈现的组件的行为，它只跟踪组件的“进入”和“退出”的状态。由你来为这些状态定义效果。

```javascript
import React from 'react'
import { Transition } from 'react-transition-group';

export default class Fade extends React.Component {
    constructor(props) {
        super(props);
    }
    done = () => {
        console.log('结束了')
    }
    addEndListener = (node) => { //原生时间transition运动的事件
        node.addEventListener('transitionend', this.done, false);
    }

    // 三个进入状态的事件，可以做你想做的事情
    onEnter = (node, isAppearing) => {
        console.log(isAppearing, 'onEnter')
    }
    onEntering = (node, isAppearing) => {
        console.log(isAppearing, 'onEntering')
    }
    onEntered = (node, isAppearing) => {
        console.log(isAppearing, 'onEntered')
    }

    // 三个退出的状态的事件
    onExit = (node) => {
        console.log('onExit')
    }
    onExiting = () => {
        console.log('onExiting')
    }
    onExited = () => {
        console.log('onExited')
    }
    render() {
        const { in: inProp } = this.props;

        const defaultStyle = {
            transition: `transform ${300}ms ease-in-out, opacity ${300}ms ease-in-out`,
            transform: 'translateX(100px)',
            opacity: '0'
        }

        const transitionStyles = {
            entering: { transform: 'translateX(100px)', opacity: '0' },
            entered: { transform: 'translateX(0px)', opacity: '1' },
            exiting: { transform: 'translateX(0px)', opacity: '1' },
            exited: { transform: 'translateX(100px)', opacity: '0' }
        };

        const duration = {
            enter: 300,
            exit: 300,
        }

        // 上面的都是基本参数，样式的转变以及时间的设定，具体的可以看官网文档
        // 样式也可以写成className 例如<MyComponent className={`fade fade-${status}`} />
        return (
            <Transition
                onEnter={this.onEnter}
                onEntering={this.onEntering}
                onEntered={this.onEntered}

                onExit={this.onExit}
                onExiting={this.onExiting}
                onExited={this.onExited}

                addEndListener={this.addEndListener}
                in={inProp}
                unmountOnExit={false} // 为true 代表退出的时候移除dom
                appear={true}     // 为true 初始动画
                timeout={duration}
            >
                {
                    state => {
                        console.log(state, '###') //你可以很直观的看到组件加载和卸载时候的状态
                        return (
                            <div style={{
                                ...defaultStyle,
                                ...transitionStyles[state]
                            }}>
                                {this.props.children}
                            </div>
                        )
                    }
                }
            </Transition>
        );
    }
}

```

```javascript
import React from 'react'
import Fade from './Fade.js'

export default class Dnd extends React.Component {
    state = {
        flag:true
    }
    handle = () => {
        this.setState(prev => {
            return {
                flag: !prev.flag
            }
        })
    }

    render() {
        return (
            <div>
                <button onClick={() => this.handle()}>点击transition</button>
                <Fade in={this.state.flag}>
                    <div>动画</div>
                </Fade>
            </div>
        )
    }
}

```

## 10.2 CSSTransition

此组件是在转换的出现、进入、退出阶段应用一对类名(也就是className)，靠这个来激活CSS动画。所以参数和平时的className不同，参数为：`classNames`
参数：（主要）in, timeout, unmountOnExit, classNames, 用法同Transition。看如下例子：

```javascript
import React from 'react'
import './star.css'
import { CSSTransition } from 'react-transition-group';

export default class Star extends React.Component {
    state = {
        star: false
    }

    handleStar = ()=>{
        this.setState(prev=>{
            return {
                star:!prev.star
            }
        })
    }

    render() {
        return (<div>
            <button onClick={()=>{this.handleStar()}}>start</button>
            <CSSTransition
                in={this.state.star}
                timeout={300}
                classNames="star"
                unmountOnExit  //为true 代表退出的时候移除dom
            >
                {/*指定默认样式*/}   
                <div className="star">星星</div>
            </CSSTransition>
        </div>)
    }
}

```

```javascript
.star {
    display: inline-block;
    margin-left: 0.5rem;
    transform: scale(1.25);
}
.star-enter {
    opacity: 0.01;
    transform: translateY(-100%) scale(0.75);
}
.star-enter-active {
    opacity: 1;
    transform: translateY(0%) scale(1.25);
    transition: all 300ms ease-out;
}
.star-exit {
    opacity: 1;
    transform: scale(1.25);
}
.star-exit-active {
    opacity: 0;
    transform: scale(4);
    transition: all 300ms ease-in;
}

```

## 10.3 SwitchTransition

受vue过渡模式启发的过渡组件， 当您要控制状态转换之间的渲染时，可以使用它。SwitchTransition不提供任何形式的动画，具体的动画取决与你包裹的Transition || CSSTransition的动画。

```javascript
import React from 'react'
import { SwitchTransition, CSSTransition } from 'react-transition-group'
import './switch.css'

export default class SwitchAnim extends React.Component {
    constructor() {
        super()

        this.state = {
            flag: false
        }
    }

    toggle = () => {
        this.setState((prev) => {
            return {
                flag: !prev.flag
            }
        })
    }

    render() {
        return (<div>
            <button onClick={this.toggle}>点我切换组件</button>
            <SwitchTransition>
                <CSSTransition
                    key={this.state.flag ? "A" : "B"}
                    classNames="fade"
                    timeout={300}>
                    {this.state.flag ? <div>AAAA</div> : <div>BBBB</div>}
                </CSSTransition>
            </SwitchTransition>
        </div>
        )
    }
}

```

```javascript
.fade-enter {
    opacity: 0.01;  
}
.fade-enter-active {
    opacity: 1;
    transition: opacity 500ms ease-in;
}
.fade-exit {
    opacity: 1;
}
.fade-exit-active {
    opacity: 0.01;
    transition: opacity 500ms ease-in;
}

```

## 10.4 TransitionGroup

一看group就知道肯定是列表形态的动画了！但是看了官网后知道，TransitionGroup不提供任何形式的动画，具体的动画取决与你包裹的Transition || CSSTransition的动画，所以你可以在列表里面做出不同类型的动画出来。

```js
import React from 'react'
import { TransitionGroup, CSSTransition } from 'react-transition-group';
import './switch.css'

export default class ListAnim extends React.Component {
    constructor() {
        super()
        this.state = {
            items: [
                { id: 1, text: 'Buy eggs' },  //0
                { id: 2, text: 'Pay bills' },  //1
                { id: 3, text: 'Invite friends over' }, //2
                { id: 4, text: 'Fix the TV' },  //3
            ]
        }
    }

    handleAdd = () => {
        let items = this.state.items;
        items.unshift({ id: items.length + 1, text: "张三" });
        this.setState({
            items: [...items]
        })
    }

    handleRemove = (id) => {
        this.setState(prev => {
            return {
                items: prev.items.filter(item => item.id != id)
            }
        })
    }

    render() {
        const items = this.state.items;
        return (<div>
            <TransitionGroup>
                {
                    items.map(item => (
                        <CSSTransition
                            key={item.id}  //这边的key一定要能唯一标识当前元素
                            timeout={300}
                            classNames="fade"
                        >
                            <div style={{ background: "red" }}>
                                {item.text}
                                <button onClick={() => this.handleRemove(item.id)}>&times;</button>
                            </div>
                        </CSSTransition>
                    ))
                }
            </TransitionGroup>
            <button onClick={this.handleAdd}>添加元素</button>
        </div>)
    }
}

```

```js
.fade-enter {
    opacity: 0.01;  
}
.fade-enter-active {
    opacity: 1;
    transition: opacity 500ms ease-in;
}
.fade-exit {
    opacity: 1;
}
.fade-exit-active {
    opacity: 0.01;
    transition: opacity 500ms ease-in;
}

```

# 11.高阶组件

## 11.1 高阶函数

**高阶函数是一个函数，它接收函数作为参数或将函数作为输出返回**

- 举个栗子:

  - 接收函数作为参数

    ```
    function a(x) {
      x();
    }
    function b() {
      alert('hello');
    }
    
    a(b);
    
    ```

  - 将函数作为输出返回

    ```
    function a() {
      function b() {
        alert('hello');
      }
      return b;
    }
    
    a()();
    
    ```

- 以上函数a就是一个高阶函数, 用法非常简单, 那么实际开发中又有哪些是高阶函数呢？

  - Array 的 map 、reduce 、filter 等方法
  - Object 的 keys 、values 等方法

## 11.2 高阶组件

- 概念：**高阶组件就是一个函数，且该函数接受一个组件作为参数，并返回一个新的组件**

- 举个栗子：

  ```javascript
  import React from 'react';
  import logo from './logo.svg';
  import './App.css';
  
  class MyComponent extends React.Component{
     render(){
      return (<p>Hello React</p>)
     }
  }
              
  function HocComponent(WrappedComponent){
    return class extends React.Component{
      render(){
        return <WrappedComponent/>
      }
    }
  }
  
  const NewComponent = HocComponent(MyComponent)
  
  function App() {
    return (
      <NewComponent></NewComponent>
    );
  }
  
  export default App;
  
  ```

- HocComponent函数就是一个高阶组件。

> 高阶组件可以看做是装饰器模式(Decorator Pattern)在React的实现。即允许向一个现有的对象添加新的功能，同时又不改变其结构，属于包装模式(Wrapper Pattern)的一种。最大的特点就是重用组件逻辑

### 11.2.1 高阶组件的实现方式-属性代理

属性代理(Props Proxy)：`HOC`是包裹在普通组件外面的一层高阶函数，任何要传入普通组件内的`props` 或者 `state` 首先都要经过 `HOC`。

`props`和 `state`等属性原本是要流向 目标组件的腰包的，但是却被 雁过拔毛的`HOC`拦路打劫，那么最终这些 `props`和 `states`数据到底还能不能再到达 目标组件，或者哪些能到达以及到达多少就全由 `HOC`说了算了，也就是说，`HOC`拥有了提前对这些属性进行修改的能力。

属性代理的作用：

- 更改prop
- 通过refs获取组件实例
- 抽象state
- 把WrappedComponent与其他elements包装在一起

#### a) 属性代理-更改props

在高阶组件中添加新的 props，可以在 WrappedComponent 中通过 this.props.name访问到。

```javascript
import React from 'react';
import logo from './logo.svg';
import './App.css';

class MyComponent extends React.Component{
  render(){
  return (<p>Hello React {this.props.name}</p>)
  }
}
function HocComponent(WrappedComponent){
  return class extends React.Component{
    render(){
      return <WrappedComponent {...this.props}/>
    }
  }
}

const NewComponent = HocComponent(MyComponent)

function App() {
  return (
    <NewComponent name="zhangsan"></NewComponent>
  );
}

export default App;

```

#### b) 属性代理-通过refs获取组件实例

当我们包装WrappedComponent的时候，想获取到它的实例怎么办，可以通过引用(ref),在WrappedComponent组件挂载的时候，会执行ref的回调函数，在hoc中取到组件的实例。通过打印可以看到它的props、 state、方法都是可以取到的。

```javascript
import React from 'react';
import logo from './logo.svg';
import './App.css';

class MyComponent extends React.Component {
  say(){
    console.log("say say say .....")
  }
  render() {
    return (<p>Hello React {this.props.name}</p>)
  }
}
function HocComponent(WrappedComponent) {
  return class extends React.Component {
    //此处的instance会拿到被包装的组件实例，然后访问被包装的组件对象的属性和方法
    proc(instance) {
      instance.say();
      console.log(instance.props.name)
    }
    render() {
      return <WrappedComponent {...this.props} ref={this.proc} />
    }
  }
}

const NewComponent = HocComponent(MyComponent)

function App() {
  return (
    <NewComponent name="zhangsan"></NewComponent>
  );
}

export default App;

```

#### c) 属性代理-抽取state

```javascript
import React from 'react';
import logo from './logo.svg';
import './App.css';

class MyInput extends React.Component {
  constructor(props){
    super(props);
    this.state = {
      value:""
    }
    this.handleChange = this.handleChange.bind(this)
  }
  handleChange(event){
    this.setState({
      value:event.target.value
    })
  }
  render() {
    return (<input value={this.state.value} onChange={this.handleChange}></input>)
  }
}
class MyTextArea extends React.Component {
  constructor(props){
    super(props);
    this.state = {
      value:""
    }
    this.handleChange = this.handleChange.bind(this)
  }
  handleChange(event){
    this.setState({
      value:event.target.value
    })
  }
  render() {
    return (<textarea value={this.state.value} onChange={this.handleChange}></textarea>)
  }
}

function HocComponent(WrappedComponent) {
  return class extends React.Component {
    render() {
      return <WrappedComponent/>
    }
  }
}

const NewInput = HocComponent(MyInput)
const NewTextArea = HocComponent(MyTextArea)

function App() {
  return (
    <div>
      <NewInput></NewInput>
      <NewTextArea></NewTextArea>
    </div>
  );
}

export default App;

//这边代码存在的问题：MyInput和MyTextArea组件都有自己的state和change方法，代码重用性太大

```

```javascript
import React from 'react';
import logo from './logo.svg';
import './App.css';

class MyInput extends React.Component {
  render() {
    return (<input value={this.props.value} onChange={this.props.onChange}></input>)
  }
}
class MyTextArea extends React.Component {
  render() {
    return (<textarea value={this.props.value} onChange={this.props.onChange}></textarea>)
  }
}

function HocComponent(WrappedComponent) {
  return class extends React.Component {
    //将所有被包含组件的state和change都抽取到高阶组件中
    constructor(props) {
      super(props);
      this.state = {
        value: ""
      }
      this.handleChange = this.handleChange.bind(this)
    }
    handleChange(event) {
      this.setState({
        value: event.target.value
      })
    }
    render() {
      const newProps = {
        value: this.state.value,
        onChange: this.handleChange
      }
      return (
        //向被包含组件传递属性
        <WrappedComponent {...this.props} {...newProps} />
      )
    }
  }
}

const NewInput = HocComponent(MyInput)
const NewTextArea = HocComponent(MyTextArea)

function App() {
  return (
    <div>
      <NewInput></NewInput>
      <NewTextArea></NewTextArea>
    </div>
  );
}

export default App;

```

#### d) 属性代理-用其他元素包装组件

为了封装样式、布局或别的目的，可以用其它组件和元素包裹 WrappedComponent。

```javascript
import React from 'react';
import logo from './logo.svg';
import './App.css';

class MyComponent extends React.Component {
  render() {
    return (<p>被包裹组件</p>)
  }
}

function HocComponent(WrappedComponent) {
  return class extends React.Component {
    render() {
      return (
        <div style={{color:"red"}}>
          <WrappedComponent {...this.props} />
        </div>

      )
    }
  }
}

const NewComponent = HocComponent(MyComponent)

function App() {
  return (
    <div>
      <NewComponent></NewComponent>
    </div>
  );
}

export default App;

```

### 11.2.2 高阶组件的实现方式-反向继承

反向继承( Inheritance Inversion )：返回的 HOC 类（Enhancer）继承了 WrappedComponent。之所以被称为 Inheritance Inversion 是因为 WrappedComponent 被 Enhancer 继承了，而不是 WrappedComponent 继承了 Enhancer。在这种方式中，它们的关系看上去被反转（inverse）了。

通过继承WrappedComponent，除了一些静态方法，包括生命周期，state，各种function，我们都可以得到。

```javascript
function iiHOC(WrappedComponent) {
  return class Enhancer extends WrappedComponent {
    render() {
      return super.render()
    }
  }
}

```

反向继承的作用：

- 渲染劫持
- 操作state

#### a) 反向继承-渲染劫持

之所以被称为渲染劫持是因为 HOC 控制着 WrappedComponent 的渲染输出，可以用它做各种各样的事。通过渲染劫持可以：

- 在由 render输出的任何 React 元素中读取、添加、编辑、删除 props
- 读取和修改由 render 输出的 React 元素树
- 有条件地渲染元素树
- 把样式包裹进元素树（就像在 Props Proxy 中的那样）

```javascript
import React from 'react';
import logo from './logo.svg';
import './App.css';

class MyComponent extends React.Component {
  render() {
    return (<p name="pp">被包裹组件</p>)
  }
}

function iiHOC(WrappedComponent) {
  return class Enhancer extends WrappedComponent {
    render() {
      const elementsTree = super.render();
      //打印父组件的属性值
      console.log(elementsTree.props)
      //添加新的 属性返回
      let newProps = {style:{color:'red'}};
      const props = Object.assign({},elementsTree.props,newProps);
      const newElement = React.cloneElement(elementsTree, props, elementsTree.props.children)
      return newElement;
    }
  }
}

const NewComponent = iiHOC(MyComponent)

function App() {
  return (
    <div>
      <NewComponent></NewComponent>
    </div>
  );
}

export default App;

```

#### b) 反向继承-修改state

HOC 可以读取、编辑和删除 WrappedComponent 实例的 state，如果需要，也可以给它添加更多的 state。但是这会搞乱 WrappedComponent 的 state，可能会导致破坏某些东西，通常不建议使用高阶组件修改添加state。

下面通过访问 WrappedComponent 的 props 和 state 来做测试。

```javascript
export function IIHOCDEBUGGER(WrappedComponent) {
  return class II extends WrappedComponent {
    render() {
      return (
        <div>
          <h2>HOC Debugger Component</h2>
          <p>Props</p> <pre>{JSON.stringify(this.props)}</pre>
          <p>State</p><pre>{JSON.stringify(this.state)}</pre>
          {super.render()}
        </div>
      )
    }
  }
}

```

# 12. 相关文章

+ [2018 年，React 将独占前端框架鳌头？](https://mp.weixin.qq.com/s/gV-w_rRfdBVAqsOpBGZaVw)
+ [前端框架三巨头年度走势对比：Vue 增长率最高](https://mp.weixin.qq.com/s/0wXWqKIigaKzMSfy4vJMVw)


+ [React数据流和组件间的沟通总结](http://www.cnblogs.com/tim100/p/6050514.html)
+ [单向数据流和双向绑定各有什么优缺点？](https://segmentfault.com/q/1010000005876655/a-1020000005876751)
+ [怎么更好的理解虚拟DOM?](https://www.zhihu.com/question/29504639?sort=created)
+ [React中文文档 - 版本较低](http://www.css88.com/react/index.html)
+ [React 源码剖析系列 － 不可思议的 react diff](http://blog.csdn.net/yczz/article/details/49886061)
+ [深入浅出React（四）：虚拟DOM Diff算法解析](http://www.infoq.com/cn/articles/react-dom-diff?from=timeline&isappinstalled=0)
+ [一看就懂的ReactJs入门教程（精华版）](http://www.cocoachina.com/webapp/20150721/12692.html)
+ [CSS Modules 用法教程](http://www.ruanyifeng.com/blog/2016/06/css_modules.html)
+ [将MarkDown转换为HTML页面](http://blog.csdn.net/itzhongzi/article/details/66045880)
+ [win7命令行 端口占用 查询进程号 杀进程](https://jingyan.baidu.com/article/0320e2c1c9cf0e1b87507b26.html)
+ [类型校验](https://facebook.github.io/react/docs/typechecking-with-proptypes.html)

- [Animation Add-Ons](https://reactjs.org/docs/animation.html#high-level-api-reactcsstransitiongroup)

## 安装 React Developer Tools 调试工具

[React Developer Tools - Chrome 扩展下载安装地址](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=zh-CN)