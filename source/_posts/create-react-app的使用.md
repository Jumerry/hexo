---
title: create-react-app的使用
date: 2020-04-10 18:59:50
tags:
cover: https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=3280663389,326638629&fm=26&gp=0.jpg
---

# 1.creat-react-app使用

<https://www.html.cn/create-react-app/docs/getting-started/>

`Create React App`是FaceBook的React团队官方出的一个构建`React`单页面应用的脚手架工具。它本身集成了`Webpack`，并配置了一系列内置的`loader`和默认的npm的脚本，可以很轻松的实现零配置就可以快速开发React的应用。

## 1.1 创建应用

```js
# 全局安装
npm install -g create-react-app
# 构建一个my-app的项目
npx create-react-app my-app
cd my-app

# 启动编译当前的React项目，并自动打开 http://localhost:3000/
npm start

# 如果你不能确保最新版本，可以先尝试卸载： npm uninstall -g create-react-app,然后再全局安装

# 解压默认的webpack配置到配置文件中
# react-scripts 是 create-react-app 的一个核心包，一些脚本和工具的默认配置都集成在里面，而 yarn eject 命令执行后会将封装在 create-react-app 中的配置全部反编译到当前项目，这样用户就能完全取得 webpack 文件的控制权。所以，eject 命令存在的意义就是更改 webpack 配置存在的啊！
npm run eject
npm install   //需要再次运行install命令安装
npm run start //然后才可以启动
```

	应用的目录结构：

```js
├── package.json
├── public                  # 这个是webpack的配置的静态目录
│   ├── favicon.ico
│   ├── index.html          # 默认是单页面应用，这个是最终的html的基础模板
│   └── manifest.json
├── src
│   ├── App.css             # App根组件的css
│   ├── App.js              # App组件代码
│   ├── App.test.js
│   ├── index.css           # 启动文件样式
│   ├── index.js            # 启动的文件（开始执行的入口）！！！！
│   ├── logo.svg
│   └── serviceWorker.js
└── yarn.lock

```

## 1.2 启用sass

react-scripts@2.0.0 以上版本才适用。

react-scripts主要设计原理是将配置好的如 `Webpack，Babel，ESLint` ，合并到 `react-scripts` 这npm包中，用户就可以开箱即用。很多开发者都在这基础上进行改造开发。注意 `react-scripts` 就是create-react-app脚手架的核心配置代码。

### 1.2.1 安装依赖

要使用Sass必须首先安装   `node-sass`

```sh
// yarn config set sass_binary_site http://cdn.npm.taobao.org/dist/node-sass -g

$ npm install node-sass --save
$ # or
$ yarn add node-sass
```

安装完之后，我们就可以直接把原来的CSS文件后缀直接改为 `.scss` 或者`.sass`,然后组件中导入的文件不再是 css文件而给我scss文件即可。

```js
import React, {Component} from 'react';
import store from './Store/Index';
import {AddNumCreator, MinusNumCreator} from './Store/ActionCreaters';
import './App.scss';

class App extends Component {
  render() {
    return (
      <div className="App">
        <header className="App-header">
          <h1>潇洒</h1>
        </header>
      </div>
    );
  }
}

export default App;
```

### 1.2.2 在sass文件中引入其他sass文件

```js
@import 'styles/colors.scss';   //这边路径以当前文件路径为参照
```

## 1.3 CSS Modules支持

导入CSS文件或者Sass文件的时候，可以用一个变量接收一下返回值。那么就可以直接通过它来访问CSS或者Sass中的内部样式类了。比如：

- button.module.css

```css
.error {
  background-color: red;
}
```

- Button.js

```js
import React, { Component } from 'react';
import styles from './button.module.css';     // Import css modules stylesheet as styles

class Button extends Component {
  render() {
    // reference as a js object
    return <button className={styles.error}>Error Button</button>;
  }
}
```

结果：

```html
<!-- This button has red background -->
<button class="Button_error_ax7yz">Error Button</button>

```

## 1.4 环境变量

巧妙的使用环境变量可以帮我们在项目中区分开生产环境还是编译环境，从而执行不同的代码。

### 1.4.1 添加自定义环境变量文件`.env` 

项目根目录下创建`.env`文件，文件内部添加 `key=value`的配置可以直接应用于项目的编译中。

```sh
REACT_APP_WEBSITE_NAME=myapp
REACT_APP_PUBLIC_URL=localhost:3000

```

> Note: 如果创建自定义的环境变量必须以`REACT_APP_`开头.

### 1.4.2 在项目中使用环境变量

在项目中可以直接用`process.env.XXX`访问我们的自定义的环境变量。比如：

- js中使用

```js
render() {
  return (
    <div>
      <small>You are running this application in <b>{process.env.NODE_ENV}</b> mode.</small>
      <form>
        <input type="text" defaultValue={process.env.REACT_APP_WEBSITE_NAME} />
        <img src={process.env.REACT_APP_PUBLIC_URL + '/img/logo.png'} />;
      </form>
    </div>
  );
}

```

```js
//再比如：判断是否是生产环境

if (process.env.NODE_ENV !== 'production') {
   console.log("development")
}

```

- HTML中使用

```
<title>%REACT_APP_WEBSITE_NAME%</title>

```

## 1.5 添加图片，字体和文件

使用 Webpack，添加图片和字体等静态资源的工作方式与 CSS 类似。

你可以 **直接在 JavaScript 模块中 import 文件**。 这会告诉 Webpack 将该文件包含在 bundle(包) 中。 与 CSS 导入不同，导入文件会为你提供字符串值。 此值是你可以在代码中引用的最终路径，例如 image 的 `src` 属性或链接到 PDF 的 `href` 属性。

要减少对服务器的请求数，导入小于 10,000 字节的图片将返回 [data URI](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/Data_URIs) 而不是路径。 这适用于以下文件扩展名：`bmp` ，`gif` ，`jpg` ，`jpeg` 和 `png` 。

```js
//例如：
import React from 'react';
import logo from './logo.png'; // 告诉 Webpack 这个 JS 文件使用了这个图片

console.log(logo); // /logo.84287d09.png

function Header() {
  // 导入结果是图片的 URL 
  return <img src={logo} alt="Logo" />;
}

export default Header;

```

```javascript
//这也适用于 CSS ：
.Logo {
  background-image: url(./logo.png);
}

```

```js
//字体图标的使用
//yarn add font-awesome
//引入样式
import 'font-awesome/css/font-awesome.css'
//使用样式
<i class="fa fa-address-book" aria-hidden="true"></i> 

//具体使用参照官网：http://www.fontawesome.com.cn/faicons/

```

## 1.6 使用Boostrap

从 npm 安装 reactstrap 和 Bootstrap 。 reactstrap 不包括 Bootstrap CSS 所以这也需要安装：

	yarn add reactstrap bootstrap@4.0.0  


在 `src/index.js` 文件的开头导入 Bootstrap CSS 和可选的 Bootstrap 主题 CSS ：

```js
import 'bootstrap/dist/css/bootstrap.css';
// 在下面放置任何其他导入，
// 以便组件中的CSS优先于默认样式。

```

在 `src/App.js` 文件或自定义组件文件中导入所需的 reactstrap 组件：

```js
import { Button } from 'reactstrap';

```

## 1.7 启用less、取别名

由于 create-react-app 脚手架中并没有配置关于 less 文件的解析，正常情况下我们也不会通过yarn reject暴露配置文件然后修改配置文件，我们可以在项目根目录下新建一个config-overrides.js配置文件，覆盖默认的配置

```jsx
1.	yarn add react-app-rewired customize-cra
2.	在项目根目录下创建一个config-overrides.js
3.  yarn add less less-loader
4.  修改package.json
    "scripts": {
        - "start": "react-scripts start",
        + "start": "react-app-rewired start",
        - "build": "react-scripts build",
        + "build": "react-app-rewired build",
        - "test": "react-scripts test",
        + "test": "react-app-rewired test",
    }

//  修改config-overrides.js文件
//  http://npm.taobao.org/package/customize-cra
//  https://blog.csdn.net/weixin_33850890/article/details/91372527

        
// 配置less和@符号
const path = require("path");
const {
    override,
    addWebpackAlias,
    addLessLoader
} = require("customize-cra");

module.exports = override(
    addLessLoader(),
    addWebpackAlias({
        ["@"]: path.resolve(__dirname, "src")
    }),
);

```

## 1.8 其他react的默认配置

- 直接可以使用sass（安装node-sass模块后）
- 直接可以使用css（import）
- 直接可以导入 图片、svg、字体文件等，已经配置好相应的loader
- ES67代码直接可以用 
  - class
  - 箭头函数
  - 私用变量
  - 静态属性
  - 继承
  - 装饰器（XXX不能用）

# 2.AntDesgin使用

```javascript
$ yarn add babel-plugin-import
$ yarn add antd

//修改config-overrides.js
+ const { override, fixBabelImports } = require('customize-cra');
+ module.exports = override(
+   fixBabelImports('import', {
+     libraryName: 'antd',
+     libraryDirectory: 'es',
+     style: 'css',
+   }),
+ );

```

然后移除前面在 `src/App.css` 里全量添加的 `@import '~antd/dist/antd.css';` 样式代码，并且按下面的格式引入模块。

```javascript
  // src/App.js
  import React, { Component } from 'react';
- import Button from 'antd/es/button';
+ import { Button } from 'antd';
  import './App.css';

  class App extends Component {
    render() {
      return (
        <div className="App">
          <Button type="primary">Button</Button>
        </div>
      );
    }
  }

  export default App;

```

最后重启 `yarn start` 访问页面，antd 组件的 js 和 css 代码都会按需加载

# 3.Flux和Redux

## 3.1 常用软件架构思想

### a) MVC

**Model**

> Model负责保存应用数组，和后端交互同步应用数据，或校验数据。Model主要与业务数据相关，与应用内交互状态无关

**View**

> View是Model的可视化，表示当前状态的视图。前端View负责构建和维护DOM元素。更新Model的实际任务是在Controller上。用户可以与View交互，包括读取和编辑Model，在Model中获取或设置属性值。*一个view通常对应一个model，所以在世实际开发过程中，会面临多个view对应多个model的状况*

**Controller**

> Controller负责连接view和model，model的任何变化会应用到view中，view的操作会痛殴controller应用到model中。

MVC有两个很明显的问题：

	1.m层和v层直接打交道，导致这两层耦合度高
	2.因为所有逻辑都写在c层，导致c层特别臃肿


![1553222527572](http://m.qpic.cn/psc?/V1497zRn1XyhLI/uUnjQtxoKSmXQ5.YSnl4gEgb4NQimyPKWp19A*AGOxTuyjada5SFEAg0L*v7r2gi1FHAlr63hxDhiDOaQEBJ2w!!/b&bo=iAJ0AYgCdAEDCSw!&rf=viewer_4)

### b) MVVM

近年来前端一个明显的开发趋势就是架构从传统的 MVC 模式向 MVVM 模式迁移。在传统的 MVC 下，当前前端和后端发生数据交互后会刷新整个页面，从而导致比较差的用户体验。因此我们通过 Ajax 的方式和网关 REST API 作通讯，异步的刷新页面的某个区块，来优化和提升体验。

![1553222636183](http://m.qpic.cn/psc?/V1497zRn1XyhLI/43eWRH6lLSncPe1pJhVzbc4UUbPGnQsIbB43D8pCUIB2MS27beZ7mb1xQb4rGIXtgNiiXEWPzuo3VRCggo8E1NhRwETHKcv5zI0p7uSriWY!/b&bo=qgIAAaoCAAEDGTw!&rf=viewer_4)

在 MVVM 框架中，View(视图) 和 Model(数据) 是不可以直接通讯的，在它们之间存在着 ViewModel 这个中间介充当着观察者的角色。当用户操作 View(视图)，ViewModel 感知到变化，然后通知 Model 发生相应改变；反之当 Model(数据) 发生改变，ViewModel 也能感知到变化，使 View 作出相应更新。这个一来一回的过程就是我们所熟知的双向绑定。

### c) Flux

Flux 是一种架构思想，专门解决软件的结构问题。它跟[MVC 架构](http://www.ruanyifeng.com/blog/2007/11/mvc.html)是同一类东西，但是更加[简单和清晰](http://www.infoq.com/news/2014/05/facebook-mvc-flux)。

首先，Flux将一个应用分成四个部分。

> - **View**： 视图层
> - **Action**（动作）：视图层发出的消息（比如mouseClick）。然后在mouseClick中将出现数据从应用程序发送到store的有效信息负载。可以将其理解为用户的某个操作而做出的反应，是改变store数据的唯一方法
> - **Dispatcher**（派发器）：用来接收Actions、执行回调函数
> - **Store**（数据层）：用来存放应用的状态，一旦发生变动，就提醒Views要更新页面

**Flux 的最大特点，就是数据的"单向流动"。**

> 1. 用户访问 View
> 2. View 发出用户的 Action
> 3. Dispatcher 收到 Action，要求 Store 进行相应的更新
> 4. Store 更新后，发出一个"change"事件
> 5. View 收到"change"事件后，更新页面

![1553222968163](http://m.qpic.cn/psc?/V1497zRn1XyhLI/43eWRH6lLSncPe1pJhVzbc05dt7kYMr.PS.Uegs5R8C*vKLOxhBwxGRHH5k2bJB79TXR0g.zVVSK*q*kwdEGe8XKX6XMN3XOPTQcJO.nAsk!/b&bo=WAK2AFgCtgADGTw!&rf=viewer_4)

![1553223019430](http://m.qpic.cn/psc?/V1497zRn1XyhLI/43eWRH6lLSncPe1pJhVzbfqolJ8OdQvDiFJTQzt65TlKcmvBI8saygf*srVUZSzI7vRlQEUiw00vVG1nJRa6hJFpvjVcc4koKoDnM8fRNyQ!/b&bo=3AKFAdwChQEDKQw!&rf=viewer_4)

## 3.2 Redux

http://cn.redux.js.org/

### a) Redux介绍

我们把Flux看做一个框架的理念的话，Redux是Flux的一种实现。Redux是SPA单页面应用程序中多个组件之间共享数据的一种方式。

Flux的基本原则是“单向数据流”，Redux在此基础上强调三个基本原则：
1.唯一数据源 ：唯一数据源指的是应用的状态数据应该只存储在唯一的一个Store上。
2.保持状态只读 ： 保持状态只读，就是说不能去直接修改状态，要修改Store的状态，必须要通过派发一个action对象完成。
3.数据改变只能通过纯函数完成 ：这里所说的纯函数就是把Reducer，Reducer描述了state状态如何修改。Redux这个名字的前三个字母Red代表的就是Reducer，其实Redux名字的含义就是Reducer+Flux。

![1553225378607](http://m.qpic.cn/psc?/V1497zRn1XyhLI/43eWRH6lLSncPe1pJhVzbdOf.Nk*em2bEeH32K58x4JVzccPBx6nveptqCSV86kK0crvJcsiee9hJ0H50rSZTZMpAI8g237*roNjpcwYY5k!/b&bo=*QLYAf0C2AEDGTw!&rf=viewer_4)

### b) Redux的基本使用

React和Redux事实上是两个独立的产品，一个应用可以使用React而不使用Redux，也可以使用Redux而不使用React，但是如果两者结合使用，没有理由不使用一个名为react-dedux的库，这个库能大大简化代码的书写。

```
npm install redux --save

```

```javascript
#1.main.js
import React from 'react'                        // 创建组件、虚拟DOM元素，生命周期
import ReactDOM from 'react-dom'      // 把创建好的 组件 和 虚拟DOM 放到页面上展示的
import { createStore } from 'redux'

import App from "./app.jsx"

/**
 * 1.创建reducer
    这是一个 reducer，形式为 (state, action) => state 的纯函数.。描述了 action 如何把 state 转变成下一个 state。
    state 的形式取决于你，可以是基本类型、数组、对象、甚至是 Immutable.js 生成的数据结构。惟一的要点是当 state 变化时需要返回全新的对象，而不是修改传入的参数。
 */
function counter(state = 0, action) {
    switch (action.type) {
        case 'ADD':
            return state + 1
        case 'MINUS':
            return state - 1
        default:
            return state
    }
}

//2.声明 actions
//action 是改变 state 的唯一途径，是一个普通的 javascript 对象，它描述了一个行为且是改变 state 的唯一途径。从用户UI操作事件、网络请求回调和 WebSocket 等其他地方获得的数据，最终都会通过 dispatch 函数调用一个 action，从而改变对应的数据。action 必须带有 type 指明具体的行为名称，且能附带上额外的信息。
function addFn() {
    return { type:'ADD' }
}
function minusFn() {
    return { type:'MINUS' }
}

// 3.创建 Redux store 来存放应用的状态。store对象的API 有 { subscribe, dispatch, getState }。
let store = createStore(counter)


// 4.订阅更新，监听state的变化
store.subscribe(() => console.log(store.getState()))

// 5.触发action
store.dispatch(addFn())  // 1
store.dispatch(addFn())  // 2
store.dispatch(minusFn())  // 1


// 6.渲染页面
function render() {
    ReactDOM.render(<App store={store} addFn={addFn} minusFn={minusFn}/>, document.getElementById('app'));
}
render()
// 每当state状态发生变化的时候，重新渲染页面
store.subscribe(render)
    
    
#2.app.jsx
import React, { Component } from 'react';

class App extends Component {
    constructor(props){
        super(props)
    }
    render() {
        const store=this.props.store
        const addFn=this.props.addFn
        const minusFn=this.props.minusFn
        const init=store.getState()
        return (
            <div className="App">
                <h1>你好吗？</h1>
                {<p>现在的总数是：{store.getState()}</p>}
                {<button onClick={ ()=>store.dispatch( addFn() ) }>加1</button>}
                {<button onClick={ ()=>store.dispatch( minusFn() ) }>减1</button>}
            </div>
        );
    }
}
export default App;

```

### c) redux异步处理

 redux默认情况下只处理同步，想要处理异步，需要上面安装的redux-thunk插件

```javascript
npm install redux-thunk -S

#1.修改main.js 代码 
import { createStore ,applyMiddleware } from 'redux';
import thunk from 'redux-thunk'
//使用applyMiddleware在创建store的时候开启中间件
const store=createStore(couter ,applyMiddleware(thunk))

function addFn() {
    return { type:'ADD' }
}
function minusFn() {
    return { type:'MINUS' }
}
function addAsynFn() {
    return dispatch=>{
        setTimeout(()=>{
            dispatch(addFn())
        },2000)
    }
}

function render() {
    ReactDOM.render(<App store={store} addFn={addFn} minusFn={minusFn} addAsyncFn={addAsynFn}/>, document.getElementById('app'));
}
                    
#2.修改app.jsx代码
render() {
        const store=this.props.store
        const addFn=this.props.addFn
        const minusFn=this.props.minusFn
        const addAsynFn=this.props.addAsyncFn
        console.log(addAsynFn)
        const init=store.getState()
        return (
            <div className="App">
                <h1>你好吗？</h1>
                {<p>现在的总数是：{store.getState()}</p>}
                {<button onClick={ ()=>store.dispatch( addFn() ) }>加1</button>}
                {<button onClick={ ()=>store.dispatch( minusFn() ) }>减1</button>}
                {<button onClick={ ()=>store.dispatch( addAsynFn() ) }>异步加1</button>}
            </div>
        );
    } 

```

### d) 抽离main.js中的reducer和actions到单独模块

```javascript
#1.reducers/index.js
//1.创建reducer,描述了如何根据action将state修改为下一个state
export function counter(state = 0, action) {
    switch (action.type) {
        case 'ADD':
            return state + 1
        case 'MINUS':
            return state - 1
        default:
            return state
    }
}

#2.actions/action.js
//2.声明 actions
export function addFn() {
    return { type:'ADD' }
}
export function minusFn() {
    return { type:'MINUS' }
}
export function addAsynFn() {
    return dispatch=>{
        setTimeout(()=>{
            dispatch(addFn())
        },2000)
    }
}

#3.main.js
import React from 'react'                        // 创建组件、虚拟DOM元素，生命周期
import ReactDOM from 'react-dom'      // 把创建好的 组件 和 虚拟DOM 放到页面上展示的
import { createStore,applyMiddleware  } from 'redux'
import thunk from 'redux-thunk'
import { counter } from './reducers/index'
import {addFn,minusFn,addAsynFn} from './actions/action'

import App from "./app.jsx"

// 3.创建 Redux store 来存放应用的状态。store对象的API 有 { subscribe, dispatch, getState }。
let store = createStore(counter,applyMiddleware(thunk))


// 4.订阅更新，监听state的变化
store.subscribe(() => console.log(store.getState()))

// 5.触发action
store.dispatch(addFn())  // 1
store.dispatch(addFn())  // 2
store.dispatch(minusFn())  // 1


// 6.渲染页面
function render() {
    ReactDOM.render(<App store={store} addFn={addFn} minusFn={minusFn} addAsyncFn={addAsynFn}/>, document.getElementById('app'));
}
render()
// 每当state状态发生变化的时候，重新渲染页面
store.subscribe(render)
    
#4. app.jsx 没有变化

```

### e) react和redux的结合使用

1.插件：react-redux

2.不适用subscribe发布事件

3.提供provider和connect两个接口

	provider作用：如果我们手动将state对象一层一层的传入容器组件应用。小还好说，大应用深层的组件简直累死了，绝对让你传到怀疑人生。react-redux提供了Provider组件让我们省了不少功夫，用法就是在我们根组件外部嵌套一层Provider，传入store （使用全局的store有风险）这样所以的子组件都可以开心地拿到state了 。
	
	Provider接受store作为其props，并声明为context的属性之一 。子组件在声明了contextTypes之后可以通过this.context.store访问到store。
	
	connect用于连接 React 组件与 Redux store。连接操作不会改变原来的组件类。反而返回一个新的已与 Redux store 连接的组件类。
	
	不过现在我们仅仅是通过展示组件生成了一个容器组件并且将它们连接了起来，但是容器组件中并没有数据和逻辑，只是一具空壳毫无意义，所以我们还需要向这个connect函数中传入两个参数。mapStateToProps负责将state的数据映射到展示组件的this.props。mapDispatchToProps负责定义发送action的函数映射到展示组件的this.props。


```
npm install react-redux --save

```

```javascript
#1.main.js

import React from 'react'                        // 创建组件、虚拟DOM元素，生命周期
import ReactDOM from 'react-dom'      // 把创建好的 组件 和 虚拟DOM 放到页面上展示的
import { createStore,applyMiddleware } from 'redux'
import thunk from 'redux-thunk'
import { counter } from './reducers/index'
import { Provider } from 'react-redux'

import App from "./app.jsx"

// 3.创建 Redux store 来存放应用的状态。store对象的API 有 { subscribe, dispatch, getState }。
let store = createStore(counter,applyMiddleware(thunk))

// 4.订阅更新，监听state的变化
store.subscribe(() => console.log(store.getState()))


ReactDOM.render(
    <Provider store={store}>
        < App />
    </Provider>
    , document.getElementById('app'));

#2.app.jsx
import React, { Component } from 'react';
import { connect } from 'react-redux'
import {addFn,minusFn,addAsynFn} from './actions/action'

class App extends Component {
    constructor(props){
        super(props)
    }
    render() {
        const num=this.props.num
        const addFn=this.props.addFn
        const minusFn=this.props.minusFn
        const addAsynFn=this.props.addAsynFn
        console.log(addAsynFn)
        return (
            <div className="App">
                <h1>你好吗？</h1>
                {<p>现在的总数是：{num}</p>}
                {<button onClick={ addFn }>加1</button>}
                {<button onClick={ minusFn }>减1</button>}
                {<button onClick={ addAsynFn }>异步加1</button>}
            </div>
        );
    }
}


//将state状态映射到属性里面,之后可以通过props获取
const mapStatetoProps=(state)=>{
    return {num:state}
}

//addFn 自动有了dispatch的功能 onClick={addFn} ; addFn  minusFn  minusFn会被映射到props里面
const mapDispatchToProps={addFn,minusFn,addAsynFn}


//为App组件提供数据和逻辑。mapStateToProps负责将state的数据映射到展示组件的this.props。mapDispatchToProps负责定义发送action的函数映射到展示组件的this.props
App=connect(mapStatetoProps,mapDispatchToProps)(App)
export default App;

#3.其他 reducers/index.js 和 actions/action.js 无变化

```

### f) 多个reducer之间的合并问题

```javascript
#1. reducers/counter.js

export default function counter(state = 0, action) {
    switch (action.type) {
        case 'ADD':
            return state + 1
        case 'MINUS':
            return state - 1
        default:
            return state
    }
}


#2. reducers/city.js
export default function location(state = '无锡', action) {
    switch (action.type) {
        case 'CHOOSECITY':
            return action.city
        default:
            return state
    }
}


#3. reducers/index.js

import {combineReducers} from 'redux'

//redux提供的用于多个reducer合并的方法
// 里面是个对象。罗列需要合并的reducer
import counter from './counter';  //项目中需要的reducer
import city from './city';   //项目中需要的reducer

console.log(combineReducers)

export default combineReducers({counter,city})


#4.actions/action.js
export function addFn() {
    return { type:'ADD' }
}
export function minusFn() {
    return { type:'MINUS' }
}

/*该action接收参数，在dispatch当前action的时候可以传递参数*/
export function changeCityFn(name) {
    return { type:'CHOOSECITY',city:name }
}

export function addAsynFn() {
    return dispatch=>{
        setTimeout(()=>{
            dispatch(addFn())
        },2000)
    }
}

#5. main.js
import React from 'react'                        // 创建组件、虚拟DOM元素，生命周期
import ReactDOM from 'react-dom'      // 把创建好的 组件 和 虚拟DOM 放到页面上展示的
import { createStore,applyMiddleware } from 'redux'
import thunk from 'redux-thunk'
import reducer from './reducers/index'
import { Provider } from 'react-redux'


import App from "./app.jsx"

let store = createStore(reducer,applyMiddleware(thunk))

store.subscribe(() => console.log(store.getState()))

ReactDOM.render(
    (<Provider store={store}>
        < App />
    </Provider>)
    , document.getElementById('app'));


#4. app.jsx 
import React from 'react'

import { connect } from 'react-redux'
import {addFn,minusFn,addAsynFn,changeCityFn} from '../actions/action'


class App extends React.Component {
    constructor(props, context) {
        super(props,context)
    }

    render() {
        const num=this.props.num
        const city = this.props.city
        const addFn=this.props.addFn
        const minusFn=this.props.minusFn
        const addAsynFn=this.props.addAsynFn
        const changeCityFn=this.props.changeCityFn
        return <div>
            <h1>你好吗？</h1>
            <h1>{city}</h1>
            {<p>现在的总数是：{num}</p>}
            {<button onClick={ addFn }>加1</button>}
            {<button onClick={ minusFn }>减1</button>}
            {<button onClick={ addAsynFn }>异步加1</button>}
            {/* 这里通过箭头函数dispatch对应的方法，并传递参数 */}
            {<button onClick={ ()=>{
                changeCityFn("苏州")
            } }>改变城市</button>}
            这是home
        </div>
    }
}

//将state状态映射到属性里面,之后可以通过props获取
const mapStatetoProps=(state)=>{
    return {num:state.counter,city:state.city}
}

//addFn 自动有了dispatch的功能 onClick={addFn} ; addFn  minusFn  minusFn会被映射到props里面
const mapDispatchToProps={addFn,minusFn,addAsynFn,changeCityFn}


//为App组件提供数据和逻辑。mapStateToProps负责将state的数据映射到展示组件的this.props。mapDispatchToProps负责定义发送action的函数映射到展示组件的this.props
App=connect(mapStatetoProps,mapDispatchToProps)(App)

export default App

```

## 3.3 redux不可变数据

**1.在ReactJS中的数据对象**

在ReactJS 中主要是props 和state：

```
//1.props是不可变的
props在子组件构造时由父组件传人子组件或自定义初始值，在子组件中不能改变props的值，只能读取：采用this.props.name。

//2.state是可变的
state是在组件内部运用的，在组件内部均可改变。但是我们永远不要直接改变state，而是要通过setState()方法来改变，因此请把 this.state 看作是不可变的，事实上有时候有人会搭配使用 Immutable来设置state，直接把state看成不可变的。

```

**2.如何在Reactjs中减少render**

那么如何在reactjs中减少render提高性能呢，主要还是从props和state入手。在Reactjs中只要state变化或者props变化,都会重新render，这里的变化并非值真变了，即使是相同的值，因为重新输入了，也会导致render。因此reactjs提供了shouldComponentUpdate和PureComponent来阻止。

```javascript
//方式一：使用shouldComponentUpdate方法
function shouldComponentUpdate (nextProps, nextState) {
    //我们需要在state和props有新值的时候进行判断，是否需要render，如果不需要，则返回false。
    return nextProps.id !== this.props.id;
}

//方式二：使用PureComponent类 
class ListOfWords extends React.PureComponent {
 render() {
     return <div>{this.props.words.join(',')}</div>;
 }
}

class WordAdder extends React.Component {
 constructor(props) {
     super(props);
     this.state = {
         words: ['marklar']
     };
     this.handleClick = this.handleClick.bind(this);
 }
 handleClick() {
     // This section is bad style and causes a bug
     const words = this.state.words;
     words.push('marklar');
     this.setState({words: words});
  
 }
 render() {
     return (
         <div>
             <button onClick={this.handleClick}>click</button>
             <ListOfWords words={this.state.words} />
         </div>
     );
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

**3.如何简单快捷的判断是否需要render**

从上面我们可以看出reactjs提供了阻止render的方法，但是如何快速判断是否需要render依然是个问题，因为判断一个复杂的数据对象是否跟之前的值是否相同并不容易。

Redux将这个问题极简化了，整个应用共用一个state。但也带来了更复杂的问题，就是state的结构可能非常复杂，如果判断是否更新呢？Redux又一次极简了，那就是采用不可变数据。

我们在判断数据是否相同时，并不需要深入判断数据对象的值是否相同，只需要浅比较即可，也就是判断是否为同一个数据对象地址，因为不可变数据对象在数据变化时均会重新创建一个新的数据对象，数据对象的地址不会相同。这也就是为什么在Reactjs，Redux中才有不可变数据对象。

# 4.react hook

*Hook* 是 React 16.8 的新增特性。它可以让你在不编写 class 的情况下使用 state 以及其他的 React 特性。

Hook 是一些可以让你在函数组件里“钩入” React state 及生命周期等特性的函数。Hook 不能在 class 组件中使用 —— 这使得你不使用 class 也能使用 React。

## 4.1 State Hook

`useState` 就是一个 *Hook* （等下我们会讲到这是什么意思）。通过在函数组件里调用它来给组件添加一些内部 state。React 会在重复渲染时保留这个 state。

`useState` 会返回一对值：**当前**状态和一个让你更新它的函数，你可以在事件处理函数中或其他一些地方调用这个函数。它类似 class 组件的 `this.setState`，但是它不会把新的 state 和旧的 state 进行合并。

> 1. 一般来说，一个函数组件，在函数退出后变量就会"消失"，但是 state 中的变量会被 React 保留。
> 2. 当我们点击按钮，调用setCount函数时，React会重新渲染这个组件，并把更新的count值传给这个组件
> 3. useState()接受一个参数为默认值，该方法返回一个数组，第一个值为定义data的值，第二个为更新data的方法，他们总是成对出现的，

```jsx
import React, { useState } from 'react'
function Demo1(props) {
    //count代表state的变量
    //setCount是一个function，如果我们要修改count变量，需要通过setCount来修改
    let [count, setCount] = useState(0)
    let [count2, setCount2] = useState(1)
    let [count3, setCount3] = useState(2)

    return (<div>
        {count}
        <button onClick={() => { setCount(++count) }}>点我修改count</button>
        <br />
        {count2}
        <button onClick={() => { setCount2(++count2) }}>点我修改count2</button>
        <br />
        {count3}
        <button onClick={() => { setCount3(++count3) }}>点我修改count3</button>
    </div>)
}

export default Demo1;

```

```jsx
//注意点：不要在循环，条件或嵌套函数中调用 Hook， 确保总是在你的 React 函数的最顶层调用他们。遵守这条规则，你就能确保 Hook 在每一次渲染中都按照同样的顺序被调用。这让 React 能够在多次的 useState 和 useEffect 调用之间保持 hook 状态的正确


function Form() {
    const [name1, setName1] = useState('111');
    if(name1!==''){
        const [name2, setName2] = useState('222');
    }
    const [name3, setName3] = useState('333');
    // ...
}

```

## 4.2 Effect Hook

`useEffect` 就是一个 Effect Hook，给函数组件增加了操作副作用的能力。它跟 class 组件中的 `componentDidMount`、`componentDidUpdate` 和 `componentWillUnmount` 具有相同的用途，只不过被合并成了一个 API。

在调用这个hook时，就是告诉React在完成对DOM的更改后运行这个hook,在这里你可以访问到state和props。

```javascript
- 纯函数：如果函数的调用参数相同，则永远返回相同的结果。它不依赖于程序执行期间函数外部任何状态或数据的变化，必须只依赖于其输入参数。
    function priceAfterTax(productPrice) { return (productPrice * 0.20) + productPrice;}

- 副作用：一个可以被观察的副作用是在函数内部与其外部的任意交互。这可能是在函数内修改外部的变量，或者在函数里调用另外一个函数等。
    var tax = 20;
    function calculateTax(productPrice) {
        return (productPrice * (tax/100)) + productPrice;
    }

```

```jsx
import React, { useState,useEffect  } from 'react'
import Child from './Child.jsx'

function Demo2(props) {
    //count代表state的变量
    //setCount是一个function，如果我们要修改count变量，需要通过setCount来修改
    let [count, setCount] = useState(0)
    let [count2, setCount2] = useState(1)

    //useEffect函数可以来模拟class组件的中指定生命周期的钩子函数 componentDidMount，componentDidUpdate，componentWillUnmount
    
    //相当于componentDidMount 、componentDidUpdate
    useEffect(()=>{
        console.log("xxxxxxxxxxx",count)
    })

    //相当于componentDidMount
    useEffect(()=>{
        console.log("yyyyyyyyy")
    },[])

    //当count2的值被改变之后执行当前的useEffect，其他值改变不会执行这个useEffect
    useEffect(()=>{
        console.log("zzzzzzzzzzzzz")
    },[count2])

    //useEffect函数中return的function会在组件重新渲染的时候以及组件卸载的时候执行
    useEffect(()=>{
        return ()=>{
            console.log('hello Hook')    
        }
    })

    return (<div>
        {count}
        <button onClick={() => { setCount(++count) }}>点我修改count</button>
        <br />
        <button onClick={() => { setCount2(++count2) }}>点我修改count2</button>
        <br />
        <Child></Child>
    </div>)
}

export default Demo2;

```

## 4.3 Ref Hook

> “ref”对象是一个通用容器，其current属性是可变的

### a) 保存dom

```javascript
function Test() {
  const t = useRef(null);
 
  useEffect(() => {
    console.log(t.current); // div
  });
 
  return (
    <div ref={t}> ... </div>
  );
}

```

### b) 保存事件程序

```javascript
function Test() {
  const t = useRef(null);
  function handleClick() {
    t.current = setTimeout(() => l(1), 2000);
  }
  function handleClear() {
    clearTimeout(t.current);
  }
 
  return (
    <>
      <button onClick={handleClick}>start</button>
      <button onClick={handleClear}>clear</button>
    </>
  );
}

```

### c) 存储以前的值

```javascript
function Test() {
  const t = useRef(null);
  const [name, setName] = useState("ajanuw");
  useEffect(() => {
    t.current = name;
  });
  const prevName = t.current;
  return (
    <div>
      <input value={name} onChange={e => setName(e.target.value)} />
      <h2>{name}</h2>
      <p>{prevName}</p>
    </div>
  );
}

```

## 4.4 memo\useMemo\useCallback

在介绍一下这两个hooks的作用之前，我们先来回顾一下react中的性能优化。在hooks诞生之前，如果组件包含内部state，我们都是基于class的形式来创建组件。当时我们也知道，react中，性能的优化点在于：

> 1. 调用setState，就会触发组件的重新渲染，无论前后的state是否不同
> 2. 父组件更新，子组件也会自动的更新

基于上面的两点，我们通常的解决方案是：

> 1. 使用immutable进行比较，在不相等的时候调用setState；
> 2. 在shouldComponentUpdate中判断前后的props和state，如果没有变化，则返回false来阻止更新。

在hooks出来之后，我们能够使用function的形式来创建包含内部state的组件。但是，使用function的形式，失去了上面的shouldComponentUpdate，我们无法通过判断前后状态来决定是否更新。而且，在函数组件中，react不再区分mount和update两个状态，这意味着函数组件的每一次调用都会执行其内部的所有逻辑，那么会带来较大的性能损耗。因此useMemo 和useCallback就是解决性能问题的杀手锏。

```javascript
import React, { useState, memo } from 'react';
import logo from './logo.svg';
import './App.css';

const Child = ()=>{
  const date = new Date();
  return (
    <div>
      {date.toLocaleString()}
    </div>
  )
}

const Parent = ()=>{
  const [count,setCount] = useState(0);
  return (
    <div>
      <div>数量为:{count}</div>
      <button onClick={()=>{setCount(count+1)}}>点我加1</button>
      <Child></Child>
    </div>
  )
}

function App() {
  return (
    <div className="App">
      <Parent></Parent>
    </div>
  );
}

export default App;

//案例存在的问题：每点击一次按钮，会重新渲染一次时间，说明父组件更新的时候，子组件也重新渲染了

```

### 4.4.1 使用memo组件

`React.memo()`是一个高阶函数，它与 [`React.PureComponent`](https://reactjs.org/docs/react-api.html#reactpurecomponent)类似，但是一个函数组件而非一个类。

React.memo()可接受2个参数，第一个参数为纯函数的组件，第二个参数用于对比props控制是否刷新，与[`shouldComponentUpdate()`](https://reactjs.org/docs/react-component.html#shouldcomponentupdate)功能类似

```javascript
//修改Child组件
const Child = memo(() => {
  const date = new Date();
  return (
    <div>
      {date.toLocaleString()}
    </div>
  )
}, (prev,next) => { console.log(prev.count,next.count); return prev.count==next.count })  //这边只要父亲传递给孩子的props发生了变化就应该刷新子组件(如果父亲没有给子组件传递props或者父亲给子组件传递的props没有改变，则子组件不应该刷新)

const Parent = () => {
  const [count, setCount] = useState(0);
  return (
    <div>
      <div>数量为:{count}</div>
      <button onClick={() => { setCount(count + 1) }}>点我加1</button>
      <Child count={count}></Child>
    </div>
  )
}

```

### 4.4.2 useMemo

#### a) 没有使用useMemo存在的问题

```javascript
import React, { useState, memo } from 'react';
import logo from './logo.svg';
import './App.css';

const Child = memo(() => {
  const date = new Date();
  return (
    <div>
      {date.toLocaleString()}
    </div>
  )
}, (prev,next) => { console.log(prev.obj,next.obj); return prev.obj==next.obj })

const Parent = () => {
  const [count, setCount] = useState(0);
  const obj = {
    name:"zhangsan"
  }
  return (
    <div>
      <div>数量为:{count}</div>
      <button onClick={() => { setCount(count + 1) }}>点我加1</button>
      <Child obj={obj}></Child>
    </div>
  )
}

function App() {
  return (
    <div className="App">
      <Parent></Parent>
    </div>
  );
}

export default App;

//案例存在的问题：每点击一次按钮，会重新渲染一次时间，但是每一次点击按钮的时候，父组件给子组件传递的都是相同的obj对象，为什么子组件还是会刷新呢?
//原因是每一次点击按钮的时候，会重新刷新父组件，父组件中的obj会重新被实例化，所以新实例化的obj和上一次实例化的obj不是同一个对象

```

#### b) useMemo hook

useMemo可以用来缓存一些变量，并指定哪些条件变化后重新计算缓存的变量。

```javascript
const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);

```

> useMemo第一个参数是一个 factory 函数，该函数的返回结果会通过useMemo缓存下来
>
> ​                  第二个参数是factory函数的依赖(deps)，当依赖(deps)改变时才重新执行 factory 函数，memoizedValue 才会被重新计算

也就是在依赖未改变时（或空数组无依赖时），memoizedValue 总是返回通过useMemo缓存的值。

```javascript
import React, { useState, memo,useMemo } from 'react';
import logo from './logo.svg';
import './App.css';

const Child = memo(() => {
  const date = new Date();
  return (
    <div>
      {date.toLocaleString()}
    </div>
  )
}, (prev,next) => { console.log(prev.obj===next.obj); return prev.obj===next.obj })

const Parent = () => {
  const [count, setCount] = useState(0);
  //使用useMemo将函数返回的结果返回
  const obj = useMemo(()=>{
    return {
      name:"zhangsan"
    }
  },[])
  return (
    <div>
      <div>数量为:{count}</div>
      <button onClick={() => { setCount(count + 1) }}>点我加1</button>
      <Child obj={obj}></Child>
    </div>
  )
}

function App() {
  return (
    <div className="App">
      <Parent></Parent>
    </div>
  );
}

export default App;

```

### 4.4.3 useCallback

#### a) 没有使用useCallback的问题

```javascript
import React, { useState, memo,useMemo } from 'react';
import logo from './logo.svg';
import './App.css';

const Child = memo((props) => {
  const date = new Date();
  return (
    <div>
      {date.toLocaleString()}
      <input type="text" onChange={props.onChange}></input>
    </div>
  )
})

const Parent = () => {
  const [text,setText] = useState("")
  const changeHandler = (event)=>{
    setText(event.target.value)
  }
  return (
    <div>
      <div>text文本为:{text}</div>
      <Child onChange={changeHandler}></Child>
    </div>
  )
}

function App() {
  return (
    <div className="App">
      <Parent></Parent>
    </div>
  );
}

export default App;

//上面代码中，我们在子组件中修改文本框的值，会触发子组件的onChange，从而触发父组件的changeHandler方法，在父组件中的changeHandler方法中修改了text文本，所以页面上的text值发生了改变。 
//但是除了我们发现页面上text文本改变之外，子组件中的时间也发生了改变 (说明每一次子组件输入内容的时候都会触发子组件的重新渲染)
//原因是每一次子组件输入内容，父组件的text文本发生变化，造成父组件被重新渲染，从而造成父组件传递给子组件的changeHandler方法(props)发生了变化，从而造成子组件的重新渲染

```

#### b) useCallback   hook

useMemo缓存的是值

useCallback缓存的是函数。有两个参数，第一个参数是需要缓存的函数，第二个参数是依赖项。

```javascript
import React, { useState, memo,useMemo,useCallback } from 'react';
import logo from './logo.svg';
import './App.css';

const Child = memo((props) => {
  const date = new Date();
  return (
    <div>
      {date.toLocaleString()}
      <input type="text" onChange={props.onChange}></input>
    </div>
  )
})

const Parent = () => {
  const [text,setText] = useState("")
  //使用useCallback来缓存函数
  const changeHandler = useCallback((event)=>{
    setText(event.target.value)
  },[])
  return (
    <div>
      <div>text文本为:{text}</div>
      <Child onChange={changeHandler}></Child>
    </div>
  )
}

function App() {
  return (
    <div className="App">
      <Parent></Parent>
    </div>
  );
}

export default App;


```

## 4.5 useReducer

useReducer提供类似 Redux 的功能。他接收两个参数，第一个参数是一个recuder(纯函数)，第二个参数是state的初始值。

他返回一个状态 state和 dispath，state是返回状态中的值，而 dispatch 是一个可以发布事件来更新 state 的。

```javascript
import React, { useReducer } from 'react';
import logo from './logo.svg';
import './App.css';

//声明一个reducer(纯函数，将action转换为state)
const reducer = (state=0,action)=>{
  switch(action.type){
    case 'ADD':
      return state+1;
      break;
    case 'SUB':
      return state-1;
      break;
    default:
      return state;
      break;
  }
}

const Child = (props) => {
  //使用useReducer提供状态
  const [count,dispatcher] = useReducer(reducer,10);
  return (
    <div>
      子组件
      数量:{count}<br/>
      <button onClick={()=>{dispatcher({type:"ADD"})}}>加1</button>
      <button onClick={()=>{dispatcher({type:"SUB"})}}>减1</button>
    </div>
  )
}

const Parent = () => {
  return (
    <div>
      <div>父组件</div>
      <Child></Child>
    </div>
  )
}

function App() {
  return (
    <div className="App">
      <Parent></Parent>
    </div>
  );
}

export default App;

```

## 4.6 useContext

接收一个 context 对象（`React.createContext` 的返回值）并返回该 context 的当前值。当前的 context 值由上层组件中距离当前组件最近的 `<MyContext.Provider>` 的 `value` prop 决定。

```jsx
#1.App.jsx
import React from 'react'
import Demo3 from '@/components/Demo3'

import MyContext from './context.js'

function App(){
    return (<MyContext.Provider value={{name:"zhangsan"}}>
        App
        <Demo3></Demo3>
    </MyContext.Provider>)
}

export default App;



#2/context.js
import React from 'react'
const MyContext = React.createContext(null);
export default MyContext;


#3.Child.jsx
import React,{useContext} from 'react'
import MyContext from '@/context.js'

export default function(props){
    //在子组件中获取父组件发布的数据
    const contextValue = useContext(MyContext);
    console.log(contextValue)
    return (<div>xx</div>)
}

```

## 4.7 useReducer和useContext提供全局状态管理

```javascript
import React, { useReducer,useContext } from 'react';
import logo from './logo.svg';
import './App.css';
import MyContext from './context.js'

//声明一个reducer(纯函数，将action转换为state)
const reducer = (state = 0, action) => {
  switch (action.type) {
    case 'ADD':
      return state + 1;
      break;
    case 'SUB':
      return state - 1;
      break;
    default:
      return state;
      break;
  }
}

const Child = (props) => {
  //使用useReducer提供状态
  

  const [count,dispatcher] = useContext(MyContext);

  return (
    <div>
      子组件
      数量:{count}<br />
      <button onClick={() => { dispatcher({ type: "ADD" }) }}>加1</button>
      <button onClick={() => { dispatcher({ type: "SUB" }) }}>减1</button>
    </div>
  )
}

const Parent = () => {
  const [count,dispatcher] = useContext(MyContext);
  return (
    <div>
      父组件：{count}
      <div>父组件</div>
      <Child></Child>
    </div>
  )
}

function App() {
  const [count, dispatcher] = useReducer(reducer, 10);
  return (
    <MyContext.Provider value={[count,dispatcher]}>
      <div className="App">
        <Parent></Parent>
      </div>
    </MyContext.Provider>

  );
}

export default App;

```

useReducer和useContext的出现并不是为了取代redux，redux是独立于任何第三方库，redux有优秀的中间件(异步数据流、debug)。当状态比较简单的时候，我们可以使用useReducer和useContext来实现组件之间的数据共享，但是当状态变得特别复杂的时候，建议使用redux。