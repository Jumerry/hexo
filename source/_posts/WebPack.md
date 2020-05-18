---
title: WebPack
date: 2020-04-7 18:53:54
tags:
cover: https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1586785399668&di=826cd4b9c45ffc7635dd68ef4943e5f2&imgtype=0&src=http%3A%2F%2Fstatic001.geekbang.org%2Fresource%2Fimage%2Ff9%2F04%2Ff909858b9ce8d2393f2488d272b03b04.jpg
---

# 1.Webpack

## 1.1 引入

### 1.1.1 网页中常见的静态资源

> - JS ： .js  .jsx  .coffee  .ts（TypeScript  类 C# 语言）
>
>
> - CSS ： .css  .less   .sass  .scss
>
>
> - Images ：  .jpg   .png   .gif   .bmp   .svg
>
>
> - 字体文件（Fonts）： .svg   .ttf   .eot   .woff   .woff2
>
>
> - 模板文件 ： .ejs   .jade  .vue【这是在webpack中定义组件的方式，推荐这么用】

### 1.1.2 静态资源带来的问题

1. 网页加载速度慢， 因为我们要发起很多的二次请求；
2. 要处理错综复杂的依赖关系

### 1.1.3 如何解决上述两个问题

1. 合并、压缩、精灵图、图片的Base64编码
2. 可以使用之前学过的requireJS、也可以使用webpack可以解决各个包之间的复杂依赖关系；

### 1.1.4 完美实现上述问题的2种解决方案

1. 使用Gulp， 是基于 task 任务的，是前端构建工具；
2. 使用browserify/Webpack， 是预编译的模块化方案；

### 1.1.5 gulp

	gulp是基于Node.js的前端自动化构建**工具**，能自动化地完成 JavaScript/sass/html/image/css 等文件的的测试、检查、合并、压缩混淆、格式化、浏览器自动刷新、部署文件生成等操作，同时可以对文件进行监听，如果文件有改动，可以自动处理生成新的文件。
	
	所以gulp解决了开发效率(修改代码后自动更新页面)、资源整合(代码的压缩合并)、代码质量(代码的检查 自动化测试)、代码转换(es6-->es5)等问题
	
	[官网](http://www.gulpjs.com)
	[中文网](http://www.gulpjs.com.cn)

#### a) gulp的核心方法

- gulp.task('任务名',function(){})     // 创建任务。
- gulp.src('./*.css')                            // 指定想要处理的文件
- gulp.dest()                                      // 指定最终处理后的文件的存放路径
- gulp.watch()                                   // 自动的监视文件的变化，然后执行相应任务。
- gulp.run('任务名')                          // 直接执行相应的任务。

#### b) 安装gulp使用

- 1.通过npm安装:`npm install gulp-cli -g`    安装全局的命令行，可以在终端中使用gulp相关命令


- 2.在当前项目中也要安装gulp: `npm install gulp --save`
- 3.还需要在当前项目中新建一个文件: gulpfile.js

```javascript
var gulp =  require('gulp');

// 创建任务
// 第一个参数: 任务名
// 第二个参数: 回调函数,当我们执行任务时就会执行这个函数
gulp.task('test', function(){
    console.log(123)
    return gulp.src('src/js2/*.js');
})

//执行任务: gulp 任务名
gulp test
```

#### c) 对js进行压缩混淆和合并

- `npm install gulp-uglify --save`     压缩混淆


- `npm install gulp-concat --save`   合并

```javascript
var gulp = require('gulp');
var uglify = require('gulp-uglify');
var concat = require('gulp-concat');
gulp.task('script', function(){
    // 1.要匹配到要处理的文件
    // 指定指定的文件:参数是匹配的规则
    // 参数也可以是数组，数组中的元素就是匹配的规则
    return gulp.src('src/js2/*.js')
   		 // concat 的参数是合并之后的文件名字
        .pipe(concat('index.js'))
    	// 压缩混淆
        .pipe(uglify())
    	// dest方法参数，指定输出文件的路径
        .pipe(gulp.dest('dist/js2'))
})
gulp.run('script')
```

#### d) 对css进行压缩操作

- `npm install gulp-cssnano --save`

```javascript
var concat = require('gulp-concat');
var cssnano = require('gulp-cssnano');
// 新建一个任务，对css进行处理
gulp.task('style', function(){
    // 对项目中的2个css文件进行合并，压缩操作
    // 1.匹配到要处理的文件
    return gulp.src('src/css/*.css')
    	// 2.合并文件
        .pipe(concat('index.css'))
   		 // 3.压缩操作
        .pipe(cssnano())
   		 // 4.输出到指定目录
        .pipe(gulp.dest('dist/css'))
})
gulp.run('style')
```

#### e) 对html进行压缩

- `npm install gulp-htmlmin --save`

```javascript
var htmlmin = require('gulp-htmlmin');
// 新建一个任务，对html进行压缩
gulp.task('html', function(){
    // 1.匹配到要处理的文件
    return gulp.src('src/index.html')
    	// 2.压缩操作
        .pipe(htmlmin({collapseWhitespace:true}))
   		 // 3.指定输出目录
        .pipe(gulp.dest('dist'))
})
gulp.run('html')
```

#### f) gulp对图片压缩

- `npm install gulp-imagemin `

```javascript
gulp.task('image',function(){
    return gulp.src('./images/*.*')
        .pipe(imageMin({progressive: true}))
        .pipe(gulp.dest('./dist/images'))
})
```

#### g) gulp.watch

- 监视文件的变化，然后执行相应的任务

```javascript
// gulp.watch 监视文件变化，执行相应任务
gulp.task('mywatch', function(){
    // 1.监视js文件的变化，然后执行script任务
    // 第一个参数：要监视的文件的规则
    // 第二个参数：是要执行的任务
    gulp.watch("src/js2/*.js",gulp.series("script"))
})

//然后使用gulp mywatch启动监听，然后一旦源文件修改了，会立刻同步编译新的目标文件
```

#### h) gulp解决浏览器缓存问题

- `npm install gulp-rev  gulp-rev-rewrite` 

```javascript
var rev = require('gulp-rev');
var revRewrite = require('gulp-rev-rewrite');

//给js文件重命名 并且输出到dist目录下
gulp.task('js', () =>
    gulp.src(['./js/c.js'])
        .pipe(gulp.dest('dist')) // 将源文件拷贝到打包目录
        .pipe(rev())  
        .pipe(gulp.dest('dist')) // 将生成的hash文件添加到打包目录
        .pipe(rev.manifest('js-rev.json'))
        .pipe(gulp.dest('dist')) // 将map映射文件添加到打包目录
);

//将html中的js文件用重名后的名字替换
gulp.task('html2', () => {
    const jsManifest = gulp.src('dist/js-rev.json'); //获取js映射文件
    return gulp.src('./html/a.html')
      .pipe(revRewrite({manifest: jsManifest})) // 把引用的js替换成有版本号的名字
      .pipe(gulp.dest('dist'))
});

//当c.js文件发生变化之后，会重新执行js和html2的任务
gulp.task('mywatch', function(){
    // 1.监视js文件的变化，然后执行script任务
    // 第一个参数：要监视的文件的规则
    // 第二个参数：是要执行的任务
    return gulp.watch("./js/c.js",gulp.series(['js','html2']))
})
```

#### i) gulp对requirejs的打包和压缩

```javascript
#1.初始化项目，安装gulp
npm init -y
npm install gulp
npm install gulp-requirejs-optimize    //gulp对于requireJS依赖处理

```

![1547520269520](http://m.qpic.cn/psc?/V1497zRn4J3Krp/uUnjQtxoKSmXQ5.YSnl4gABR0aI1ZMyeCd2hU5y4LngiQHBJUoPiaNAtLDo9BSxCutsRt1BKdZIFWHTE..rqaw!!/b&bo=NwE4ATcBOAEDCSw!&rf=viewer_4)

```javascript
#1.index.html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>requirejs-gulp</title>
</head>
<body>
    <h2>demo</h2>
    <div>相加的值：<span class="math"></span></div>
    <!--data-main指定js文件的入口-->
    <script src="./require.js" data-main="./js/entry.js"></script>
</body>
</html>

#2.math.js
//定义math模块，该模块依赖于jquery模块，入参$
define(['jquery'], function($){
    var math = {
        add: function(i,j){
            $('.math').text(i+j)
        }
    }
    //requireJS模块需要返回一个对象
    return math;
})

#3.entry.js
//require配置
require.config({
    paths: {
        "jquery": "./jquery",
        "math": "./math",
    },
    //requireJS加载非AMD规范的模块，需要用shim(AMD规范是用define和require定义和引入规范)
    shim: {
        "jquery": {
            //exports的值要与文件中暴露出全局变量名称一致
            exports: '$'
        }
    }
});

//入口文件引入math模块，function中的入参需要是模块名
require(['math'], function(math){
    math.add(3,5);
});

#4.项目中引入require.js，然后使用浏览器运行index.html
打开network，查看index.html的请求资源数

#5.使用gulp进行打包构建，在项目根目录下创建gulpfile.js

var gulp = require('gulp');
var requirejsOptimize = require('gulp-requirejs-optimize');

//要进行的任务
gulp.task('rjs', function(){
    //源文件
    return gulp.src('src/js/*.js')
    .pipe(
        requirejsOptimize({
            optimize: 'none', /*optimize: 'uglify',*/  /*uglify 压缩所有文件*/
            paths:{
                //.的含义是task任务所在的js文件路径，即生成模块的路径，所以.代表src/js目录，这里要用..
                "jquery": '../js/jquery',
                'entry': '../js/entry',
                'math': '../js/math',
            }
        }))
        //配置详解：https://blog.csdn.net/xuelang532777032/article/details/55096057
    .pipe(gulp.dest('dist/js/'));
});

#6.修改index.html中的请求资源路径，再查看浏览器中network中的请求资源数
    <script src="./require.js" data-main="../dist/js/entry.js"></script>

```

### 1.1.6 webpack

> webpack 是前端的一个项目构建工具，它是基于 Node.js 开发出来的一个前端工具；

- 借助于webpack这个前端自动化构建工具，可以完美实现资源的合并、打包、压缩、混淆等诸多功能。

```javascript
# 在没有使用webpack之前：
举个例子：index.html里面有一大堆的css和js文件，如a.js   b.js   c.js  d.js等等
（1）a.js要用到b.js里面的一个函数，则a.js要放在b.js后面
（2）c.js要用到a.js里面的一个函数，则c.js要放在a.js后面
（3）b.js又要用到d.js文件里面的函数，则b.js就要放在d.js后面
如果有N多个js文件，需要手动处理他们的关系，即容易出错。

# 使用webpack：
webpack的理念就是一切皆模块化，把一堆的css文件和js文件放在一个总的入口文件，通过require引入，剩下的事情webpack会处理，包括所有模块的前后依赖关系，打包、压缩、合并成一个js文件，公共代码抽离成一个js文件、某些自己指定的js单独打包，模块可以是css/js/images/font等等。

```

![1547006043567](http://m.qpic.cn/psc?/V1497zRn4J3Krp/43eWRH6lLSncPe1pJhVzbb*s7PIQ7gHDU8rcrixpu*Rtad.K2DtV3udjhLxISPEvqkxIZx0RKdH9bvlxiJNX112RWNaO0apdDEp.BE9WFE4!/b&bo=GASDARgEgwEDGTw!&rf=viewer_4)

### 1.1.7 Gulp和webpack对比

	gulp、grunt、webpack都是前端自动化构建工具。


#### a) gulp

> gulp 和 grunt 非常类似，gulp强调的是前端开发的工作流程，核心都是基于一个个的任务(task)进行项目构建，我们可以通过配置一系列的task，定义task处理的事务（例如文件压缩合并、雪碧图、启动server、版本控制等），然后定义执行顺序，来让gulp执行这些task，从而构建项目的整个前端开发流程。
>
> 只是grunt 会频繁进行 IO 操作，而 gulp 则不需要(**基于管道流**)，可以更高效的完成操作。
>
> PS：简单说就一个Task Runner

#### b) webpack

> Webpack与Gulp、Grunt没有什么可比性，它把项目看成一个整体，是一个前端模块化方案，更侧重模块打包，我们可以把开发中的所有资源（图片、js文件、css文件等）都看成模块，通过loader（加载器）和plugins（插件）对资源进行处理，打包成符合生产环境部署的前端资源。
>
> PS：webpack is a module bundle

## 1.2 webpack的安装

	[WebPack官网](http://webpack.github.io/)


1. 运行`npm i webpack@4.27.1 -g`全局安装webpack，这样就能在全局使用webpack的命令

   `npm i webpack-cli@3.1.2 –g` 全局安装webpack命令行工具

```
配置环境变量

```

2. 在项目根目录中运行`npm i webpack@4.27.1 --save-dev`安装到项目依赖中

```javascript
npm info webpack //查看npm上的webpack的信息

webpack -v   //查看当前安装的webpack的版本信息

```

## 1.3 webpack打包构建

https://webpack.docschina.org/guides/getting-started

### 1.3.1 webpack 列表隔行变色案例

1. 运行`npm init -y`初始化项目，使用npm管理项目中的依赖包

2. 创建项目基本的目录结构

   ![1545011845124](http://m.qpic.cn/psc?/V1497zRn4J3Krp/43eWRH6lLSncPe1pJhVzbR8.YT6VpZTHtFhmi3L6FN8*.VpnJ4YS4FpDpAhjIMyF.z9yJpCYEnI97ZnMHtGab.eBpWO8BDlvwaiNzToDg*k!/b&bo=6wDcAOsA3AADGTw!&rf=viewer_4)

3. 使用`npm i jquery --save`安装jquery类库

4. index.html

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		
		<!--不推荐这样用，这样使用会导致当前文件依赖于其他文件-->
		<!--<script type="text/javascript" src="../node_modules/jquery/jquery.js"></script>-->
		
		<!--所以我们把主要的逻辑代码写到main.js中，只要引入一个main.js就可以了-->
		<!--<script type="text/javascript" src="main.js"></script>-->
        
        <!--使用打包后的路径-->
        <script type="text/javascript" src="../dist/bundle.js"></script>
	</head>
	<body>
		<!--使用jquery实现隔行渐变-->
		<ul>
			<li>A</li>
			<li>B</li>
			<li>C</li>
			<li>D</li>
			<li>E</li>
			<li>F</li>
		</ul>
	</body>
</html>


```

5. 创建`main.js`并书写各行变色的代码逻辑：

```javascript
// 1. 导入 Jquery
// import *** from *** 是ES6中导入模块的方式
// 由于 ES6的代码，太高级了，浏览器解析不了，所以，这一行执行会报错
import $ from 'jquery'
//const $ = require('jquery')   express导包的语法，vue中使用es6导包的语法，import .. from ..

// 设置偶数行背景色，索引从0开始，0是偶数
$(function () {
  $('li:odd').css('backgroundColor', 'yellow')
  $('li:even').css('backgroundColor', function () {
    return '#' + 'D97634'
  })
})

```

6. 注意点

```javascript
1. 直接在页面上引用main.js会报错，因为浏览器不认识import这种高级的JS语法，需要使用webpack进行处理，webpack默认会把这种高级的语法转换为低级的浏览器能识别的语法；
2. 运行webpack 入口文件路径 输出文件路径对main.js进行处理：
    webpack ./src/main.js -o ./dist/bundle.js
3.webpack使用的是CommonJS模块化规范，即require引入模块，module.exports导出模块
   Vue中使用的是ES6的模块化规范，即import ** from **引入模块，export /export default导出模块

```

7. webstorm中的cmd

```javascript
点击左下角的Terminal
如果要运行package.json中的指令，可以选择tools-->run gulp/grunt/npm task

```

![1545021824702](http://m.qpic.cn/psc?/V1497zRn4J3Krp/43eWRH6lLSncPe1pJhVzbWuNT4MYGUWdwu7EC9*fWaRPGA9yRXQJ*FfUQrAW1DkjKJRFqF6nMgw4yZPQ5eUkf2Mc9GCyOz3Hlib*M94ssRY!/b&bo=EwIbARMCGwEDGTw!&rf=viewer_4)

### 1.3.2 webpack配置文件使用

1. 在项目根目录中创建`webpack.config.js`
2. 由于运行webpack命令的时候，webpack需要指定入口文件和输出文件的路径，所以，我们需要在`webpack.config.js`中配置这两个路径：

```javascript
// 导入处理路径的模块
var path = require('path');

// 导出一个配置对象，将来webpack在启动的时候，会默认来查找webpack.config.js，并读取这个文件中导出的配置对象，来进行打包处理
module.exports = {
    entry: path.resolve(__dirname, 'src/main.js'), // 项目入口文件
    output: { // 配置输出选项
        path: path.resolve(__dirname, 'dist'), // 配置输出的路径
        filename: 'bundle.js' // 配置输出的文件名
    }
}

```

3. 使用命令打包构建

```javascript
# 使用webpack命令即可打包项目、
webpack   //没有指定webpack打包的配置文件，默认使用项目根路径下的webpack.config.js文件
webpack --config webpack.config.js  //指定webpack打包的时候使用的配置文件

// 当我们在控制台，直接输入 webpack 命令执行的时候，webpack 做了以下几步：
//  1. 首先webpack 发现我们并没有通过命令的形式给它指定入口和出口
//  2. webpack 就会去项目的根目录中查找一个叫做 `webpack.config.js` 的配置文件
//  3. 当找到配置文件后，webpack会去解析执行这个配置文件，当解析执行完配置文件后，就得到了 配置文件中，导出的配置对象
//  4. 当 webpack拿到配置对象后，就拿到了配置对象中指定的入口和出口，然后进行打包构建；

```

### 1.3.3 webpack实时打包构建

1. 由于每次重新修改代码之后，都需要手动运行webpack打包的命令，比较麻烦，所以使用`webpack-dev-server`来实现代码实时打包编译，当修改代码之后，会自动进行打包构建。

2. 安装webpack-dev-server

   ```javascript
   npm i webpack-dev-server@3.1.9 --save-dev
   npm i webpack@4.27.1 --save-dev     //项目中安装webpack
   npm i webpack-cli@3.1.2
   
   ```

3. 安装完成之后，在命令行直接运行`webpack-dev-server`来进行打包，发现报错，因为它不是全局命令，不可以直接使用。

4. 我们借助于`package.json`文件中的指令来进行运行`webpack-dev-server`命令，在`scripts`节点下新增`"dev": "webpack-dev-server"`指令，发现可以进行实时打包

   ```javascript
     "scripts": {
       "test": "echo \"Error: no test specified\" && exit 1",
       "dev": "webpack-dev-server"
     }
   
   ```

5. 运行项目

   ```javascript
   npm run dev
   
   ```

   但是dist目录下并没有生成`bundle.js`文件，这是因为`webpack-dev-server`将打包好的文件放在了内存中。把bundle.js放在内存中的好处是：由于需要实时打包编译，所以放在内存中速度会非常快

   ```
   Project is running at  [1m [34mhttp://localhost:8084/ [39m[22m
   webpack output is served from /  
   
   ```

   	此时我们可以通过http://localhost:8083/bundle.js 文件，因为webpack-dev-server默认是将bundle.js文件打包到根路径，所以要能做到修改main.js之后页面也要同步变化，需要修改页面的script标签：
   

   ```
   <script type="text/javascript" src="../bundle.js"></script>
   
   ```

   6.指定启动参数：

   	为了能在访问http://localhost:8080/的时候直接访问到index首页，可以使用--contentBase src指令来修改dev指令，指定启动的根目录：
   

```javascript
 "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "dev": "webpack-dev-server --open --port 3001 --contentBase src --hot"
  },
  
  //  --open含义：构建完成自动打开浏览器
  //  --port 3001 : 指定运行的端口
  //  --contentBase src   :  指定运行的根目录是src，即认为src就是项目根目录
  //  --hot : 以补丁的方式修改文件，而不是修改全部文件

```

![1545024701179](http://m.qpic.cn/psc?/V1497zRn4J3Krp/43eWRH6lLSncPe1pJhVzbQMHtNdJffaeDy7gGwmET1DyxWN0NPN1jdOWbQYV8B.yNnlVgiDn9115mhM5VOeFSEIn5skOR4Go2aOviqNuCT0!/b&bo=TgJTAE4CUwADGTw!&rf=viewer_4)

	7.解决webpack4.0之后打包大小警告和热更新慢的问题
	
	https://cloud.tencent.com/developer/section/1477466


```javascript
#main.js 
const path = require('path')

module.exports = {
    //1.设置为开发模式，不然热更新会比较缓慢
    mode:"development",
    entry: path.resolve(__dirname, 'src/main.js'),
    output: {
        path: path.resolve(__dirname, 'dist'),
        filename: 'bundle.js'
    },
    //2.打包文件大小警告和错误的问题
    performance: {
        hints:false
    }
}

```

### 1.3.3 使用配置文件生成参数(了解)

```javascript
const path = require('path')
// 启用热更新的 第2步
const webpack = require('webpack')

module.exports = {
  entry: path.join(__dirname, './src/main.js'),
  output: { 
    path: path.join(__dirname, './dist'), 
    filename: 'bundle.js'
  },
  devServer: { 
    // 这是配置 dev-server 命令参数的第二种形式，相对来说，这种方式麻烦一些
    //  --open --port 3000 --contentBase src --hot
    open: true, // 自动打开浏览器
    port: 3000, // 设置启动时候的运行端口
    contentBase: 'src', // 指定托管的根目录
    hot: true // 启用热更新 的 第1步
  },
  plugins: [ // 配置插件的节点
    new webpack.HotModuleReplacementPlugin(), // new 一个热更新的 模块对象， 这是 启用热更新的第 3 步
  ],
}

```

### 1.3.4 html-webpack-plugin插件配置启动页面

	https://www.npmjs.com/package/html-webpack-plugin
	
	html-webpack-plugin插件可以**将指定页面配置生成到内存中**，并且可以**将打包的bundle.js配置到内存中生成的html页面中**，使用步骤如下：


1. 运行`npm i html-webpack-plugin@3.2.0 --save-dev`安装到开发依赖
2. 修改`webpack.config.js`配置文件如下：

```javascript
const path = require('path')
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

3. 修改`package.json`中`script`节点中的dev指令如下：

```javascript
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "dev": "webpack-dev-server --open --port 3001 --contentBase src --hot"
},

```

4. 将index.html中script标签注释掉，因为`html-webpack-plugin`插件会自动把bundle.js注入到index.html页面中！

### 1.3.5 使用webpack打包css文件

	一般情况下，我们并不推荐在html页面中直接引入其他css文件，这样会导致过多的请求。对应的，我们可以使用webpack来构建。使用步骤如下：


1. 运行 `npm i style-loader css-loader --save-dev`
2. main.js中引入index.css

```css
import "./css/index.css"

```

3. 修改`webpack.config.js`这个配置文件：

```javascript
// 用来配置第三方loader模块的
module: { 
    rules: [ 
        // 匹配以.css结尾的文件
        { test: /\.css$/, use: ['style-loader', 'css-loader'] }//处理css文件的规则
    ]
}

```

4. webpack 处理第三方文件类型的过程

```javascript
1. 发现这个要处理的文件不是JS文件，然后就去配置文件中，查找有没有对应的第三方 loader 规则
2. 如果能找到对应的规则， 就会调用对应的loader处理这种文件类型；
3. 在调用loader的时候，use中相关loader模块的调用顺序是从后向前调用的；
4. 当最后的一个loader调用完毕，会把处理的结果直接交给 webpack 进行打包合并，最终输出到  bundle.js 中去

```

### 1.3.6 使用webpack打包less文件

1. 运行`npm i less-loader less`，需要同时安装less-loader和less
2. main.js中引入index.less

```css
import "./css/index.less"

```

3. 修改`webpack.config.js`这个配置文件：

```javascript
module: { // 用来配置第三方loader模块的
    rules: [ // 文件的匹配规则
        { test: /\.css$/, use: ['style-loader', 'css-loader'] },//处理css文件的规则
        { test: /\.less$/, use: ['style-loader', 'css-loader', 'less-loader'] }
    ]
}

```

### 1.3.7 使用webpack打包sass文件

1. 运行`npm i sass-loader@7.3.1 node-sass --save-dev`
2. main.js中引入index.scss   

```javascript
//注意：文件名是scss结尾
import "./css/index.scss"

```

3. 在`webpack.config.js`中添加处理scss文件的loader模块：

```javascript
module: { // 用来配置第三方loader模块的
    rules: [ // 文件的匹配规则
        { test: /\.css$/, use: ['style-loader', 'css-loader'] },//处理css文件的规则
        { test: /\.less$/, use: ['style-loader', 'css-loader', 'less-loader'] },
        { test: /\.scss$/, use: ['style-loader', 'css-loader', 'sass-loader'] }
    ]
}

```

### 1.3.8 使用webpack处理css中的路径

1. 运行`npm i url-loader file-loader --save-dev`
2. 在`webpack.config.js`中添加处理url路径的loader模块：

```javascript
module: { // 用来配置第三方loader模块的
    rules: [ // 文件的匹配规则
        { test: /\.css$/, use: ['style-loader', 'css-loader'] },//处理css文件的规则
        { test: /\.less$/, use: ['style-loader', 'css-loader', 'less-loader'] },
        { test: /\.scss$/, use: ['style-loader', 'css-loader', 'sass-loader'] },
        { test: /\.(png|jpg|gif|bmp|jpeg)$/, use: 'url-loader' }
    ]
 }

```

3. index.css

```css
div{
    width: 600px;
    height: 450px;
    background-image: url(../images/1.jpg);
}

```

	注意点：url-loader默认情况下会将图片转换为base64编码的图片，好处是可以减少图片的二次请求。但是这种方式一般情况下适用于小图，如果是大图，我们可以像下面这样去使用：


```javascript
module: { // 用来配置第三方loader模块的
    rules: [ // 文件的匹配规则
        { test: /\.css$/, use: ['style-loader', 'css-loader'] },//处理css文件的规则
        { test: /\.less$/, use: ['style-loader', 'css-loader', 'less-loader'] },
        { test: /\.scss$/, use: ['style-loader', 'css-loader', 'sass-loader'] },
        { test: /\.(png|jpg|gif|bmp|jpeg)$/,
         		use: [
                    {
                        loader: 'url-loader',
                        options: {
                            limit: 8192,
                            name:'[hash:8]-[name].[ext]'
                        }
                    }
                ]
        }
    ]
}

//limit ： 当图片大小小于等于指定的值时会进行base64编码
//name =[name].[ext]： 不给图片重命名，还是使用原图名。如果没有这个属性，则默认会使用hashcode的方式来给图片重命名。
//给图片重命名的好处是：如果在多个不同的目录下有两张同名的图片(内容不同)，不会产生冲突。(默认情况下webpack会将图片也打包到根路径下)
//如果既想多个文件夹下的同名的图片被打包后不冲突，又想保留原来的图片名字，可以这样使用：name=[hash:8]-[name].[ext]  ，  [hash:8]表示保留8位hash值，然后再去追加原来的[name]

```

### 1.3.9 使用webpack处理字体图标

1.运行`npm i bootstrap@3.3.5`安装boostrap

2.main.js引入bootstrap

```javascript
//注意：这边import的时候不需要加上 node_modules目录，import前面没有路径的时候会自动从node_modules目录下去查找
import "bootstrap/dist/css/bootstrap.css"

```

3.index.html

```html
<span class="glyphicon glyphicon-heart-empty"></span>

```

4.webpack.config.js修改匹配规则。因为boostrap的字体文件中也使用了url，所以字体文件的路径一样要处理

```javascript
module: { // 用来配置第三方loader模块的
    rules: [ // 文件的匹配规则
        { test: /\.css$/, use: ['style-loader', 'css-loader'] },//处理css文件的规则
        { test: /\.less$/, use: ['style-loader', 'css-loader', 'less-loader'] },
        { test: /\.scss$/, use: ['style-loader', 'css-loader', 'sass-loader'] },
        {
                test: /\.(png|jpg|gif|bmp|jpeg)$/,
                use: [
                    {
                        loader: 'url-loader',
                        options: {
                            limit: 8192,
                            name:'[hash:8]-[name].[ext]'
                        }
                    }
                ]
            },
            {   test: /\.(ttf|eot|svg|woff|woff2)$/,
                use: [
                    {
                        loader:'url-loader'
                    }
                ]
            }, // 处理 字体文件的 loader
    ]
}

```

### 1.3.10 webpack中babel的配置

	在 webpack 中，默认只能处理一部分 ES6 的新语法；这时候就需要借助于第三方的 loader，来帮助webpack 处理这些高级的语法，当第三方loader可以把高级语法转为低级的语法，然后再把结果交给 webpack 去打包到 bundle.js 中


1. 运行`npm i babel-core@6.26.3 babel-loader@7.1.5 babel-plugin-transform-runtime --save-dev`安装babel的相关loader包 (babel的转换工具)
2. 运行`npm i babel-preset-env babel-preset-stage-0 --save-dev`安装babel转换的语法 (es6的语法和es5的语法的对应关系)
3. 在`webpack.config.js`中添加相关loader模块，其中需要注意的是，一定要把`node_modules`文件夹添加到排除项：

```javascript
module: { // 用来配置第三方loader模块的
    rules: [ // 文件的匹配规则
        { test: /\.css$/, use: ['style-loader', 'css-loader'] },//处理css文件的规则
        { test: /\.less$/, use: ['style-loader', 'css-loader', 'less-loader'] },
        { test: /\.scss$/, use: ['style-loader', 'css-loader', 'sass-loader'] },
        { test: /\.(png|jpg|gif|bmp|jpeg)$/, use: 'url-loader?limit=1024&name=[hash:8]-[name].[ext]' },
        { test: /\.(ttf|eot|svg|woff|woff2)$/, use: 'url-loader' }, // 处理 字体文件的 loader
        //配置 babel 的 loader规则的时候，必须 把 node_modules 目录，通过 exclude 选项排除掉
        { test: /\.js$/, use: 'babel-loader', exclude: /node_modules/ },
    ]
}

```

4. 在项目根目录中添加`.babelrc`文件，并修改这个配置文件如下(这个文件必须符合json的语法，不能有注释。字符串必须使用双引号)：

```javascript
{
  "presets": ["env", "stage-0"],
  "plugins": ["transform-runtime"]
}

```

**注意：之前用的比较多的语法插件`babel-preset-es2015`更新为`babel-preset-env`，它包含了所有的ES相关的语法；**

### 1.3.11 所有配置总结

```javascript
# 1.安装
npm i webpack@4.20.1 --save-dev                   //安装webpack
npm init -y                                                       //项目初始化
npm i webpack-dev-server@3.1.9 --save-dev      //实时打包构建
npm i webpack-cli@3.1.2      
npm i html-webpack-plugin@3.2.0 --save-dev      //配置内存页面
npm i style-loader css-loader --save-dev               //css加载器
npm i less-loader less                                             //less加载器
npm i sass-loader@7.3.1 node-sass --save-dev               //sass加载器
npm i url-loader file-loader --save-dev                 //url加载器
npm i babel-core@6.26.3 babel-loader@7.1.5 babel-plugin-transform-runtime --save-dev    //babel转换工具
npm i babel-preset-env babel-preset-stage-0 --save-dev           //babel转换的语法

#2.webpack.config.js
const path = require('path')
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
    module: { // 用来配置第三方loader模块的
        rules: [ // 文件的匹配规则
            { test: /\.css$/, use: ['style-loader', 'css-loader'] },//处理css文件的规则
            { test: /\.less$/, use: ['style-loader', 'css-loader', 'less-loader'] },
            { test: /\.scss$/, use: ['style-loader', 'css-loader', 'sass-loader'] },
            { test: /\.(png|jpg|gif|bmp|jpeg)$/, use: 'url-loader?limit=1024&name=[hash:8]-[name].[ext]' },
            { test: /\.(ttf|eot|svg|woff|woff2)$/, use: 'url-loader' }, // 处理 字体文件的 loader
            //配置 babel 的 loader规则的时候，必须 把 node_modules 目录，通过 exclude 选项排除掉
            { test: /\.js$/, use: 'babel-loader', exclude: /node_modules/ },
        ]
    }
}

#3.项目入口文件
import "./css/index.css"

console.log("ok");

class Person{
    constructor(name,age){
        this.name = name;
        this.age = age;
    }
    showInfo(){
        console.log(this.name);
    }
}
var p = new Person("xiaoming",18);
console.log(p.name);


#4.package.json
 "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "dev": "webpack-dev-server --open --port 3000 --contentBase src --hot"
  }

#5.项目根目录 .babelrc
{
  "presets": ["env", "stage-0"],
  "plugins": ["transform-runtime"]
}

```

## 1.4 相关文章

[babel-preset-env：你需要的唯一Babel插件](https://segmentfault.com/p/1210000008466178)
[Runtime transform 运行时编译es6](https://segmentfault.com/a/1190000009065987)

# 2.Vue结合webpack的使用

### 2.1 基本使用

```javascript
#1.安装vue
   运行npm i vue@2.3.4将vue安装为运行依赖
   
#2.main.js
/*
 注意：在webpack中使用 import Vue from 'vue'导入的Vue构造函数功能不完整，只提供了runtime-only的方式，并没有提供像网页中那样的使用方式；
 import Vue from 'vue' 导入包的规则：
   1. 找项目根目录中有没有 node_modules 的文件夹
   2. 在node_modules中根据包名，找对应的vue文件夹
   3. 在vue文件夹中，找一个叫做 package.json 的包配置文件
   4. 在package.json文件中，查找一个 main 属性【main属性指定了这个包在被加载时候的入口文件】，这里我们发现入口文件为vue.runtime.common.js，并不是vue.js文件

 解决方案有两种：
   1.在webpack.config.js下新增配置：
       resolve: {
            alias: {
                'vue$': 'vue/dist/vue.js'
            }
        }
        
        然后使用 import Vue from 'vue'  就可以了
        
   2.手动修改导包的路径为：import Vue from 'vue/dist/vue''，此时无需修改配置文件
*/

import Vue from 'vue'

var login = {
   template: '<h1>这是login组件，是使用网页中形式创建出来的组件</h1>'
}

var vm = new Vue({
    el: '#app',
    data: {
        msg: '123'
    },
    components:{
        login
    }
})

#3.index.html
<div id="app">
    <p>{{msg}}</p>
	<login></login>
</div>

#4.webpack.config.js
resolve: {
    alias: {
        'vue$': 'vue/dist/vue.js'
    }
}

#5.package.json、.babelrc还有webpack的所需要安装的内容和之前一致

```

### 2.2 使用.vue文件的方式生成组件

	vscode中安装vetur插件，可以格式化html、标准css（有分号 、大括号的那种）、标准js（有分号 、双引号的那种）、vue文件webstorm中支持vue文件的提示，需要安装插件

```javascript
#1. 新建login.vue文件

<template>
  <div>
    <h1>这是登录组件，使用 .vue 文件定义出来的 </h1>
  </div>
</template>


#2.main.js引入.vue文件，并使用
import Vue from 'vue'

import login from './login.vue'

var vm = new Vue({
    el: '#app',
    data: {
        msg: '123'
    },
    components:{
        login
    }
})

#3. index.html
<div id="app">
    <p>{{msg}}</p>
    <login></login>
</div>

#4.安装vue-loader和 vue-template-compiler(默认情况下不支持import方式引入.vue文件，需要安装下面两个文件)
npm i vue-loader@15.4.2 vue-template-compiler@2.3.4
//注意：这里vue-template-compiler版本需要和当前使用的vue版本一致

#5.webpack.config.js
const path = require('path')
var htmlWebpackPlugin = require('html-webpack-plugin');
//1.引入VueLoaderPlugin插件(在vue-loader15版本以后需要配置这个)
const VueLoaderPlugin = require('vue-loader/lib/plugin');

module.exports = {
    entry: path.join(__dirname, './src/main.js'),
    output: {
        path: path.join(__dirname, './dist'),
        filename: 'bundle.js'
    },
    plugins: [
        new htmlWebpackPlugin({
            template:path.resolve(__dirname, 'src/index.html'),//模板路径
            filename:'index.html'//自动生成的HTML文件的名称
        }),
        // 2.配置VueLoaderPlugin插件
        new VueLoaderPlugin()
    ],
    module: { 
        rules: [ 
            { test: /\.css$/, use: ['style-loader', 'css-loader'] },
            { test: /\.less$/, use: ['style-loader', 'css-loader', 'less-loader'] },
            { test: /\.scss$/, use: ['style-loader', 'css-loader', 'sass-loader'] },
            { test: /\.(png|jpg|gif|bmp|jpeg)$/, use: 'url-loader?limit=1024&name=[hash:8]-[name].[ext]' },
            { test: /\.(ttf|eot|svg|woff|woff2)$/, use: 'url-loader' }, 
            { test: /\.js$/, use: 'babel-loader', exclude: /node_modules/ },
            //3.处理 .vue 文件的 loader
            { test: /\.vue$/, use: 'vue-loader' } 
        ]
    },
    resolve: {
        alias: {
           'vue$': 'vue/dist/vue.js'
        }
    }
}

```

### 2.3 render渲染组件

```javascript
#main.js

import Vue from 'vue'

import login from './login.vue'

var vm = new Vue({
    el: '#app',
    data: {
        msg: '123'
    },
    render: c => c(login)
})

//注意：此种方式会替换页面内容

```

### 2.4 .vue组件中的数据

#### 2.4.1 模块的导出

   ES6语法：

> 1. 在ES6中使用 export default 和 export 导出模块中的成员;
>
> (Node中使用 module.exports 和 export导出成员)
>
> 2. 使用 import ** from ** 和 import '路径' 还有 import {a, b} from '模块标识' 导入其他模块

```javascript
#1. 新建test.js
// 在 ES6 中，使用 export default 和 export 向外暴露成员：
var info = {
  name: 'zs',
  age: 20
}

export default info

/* 注意：
   export default 向外暴露的成员，可以使用任意的变量来接收
   在一个模块中，export default 只允许向外暴露1次
   在一个模块中，可以同时使用 export default 和 export 向外暴露成员
*/


export var title = '小星星'
export var content = '哈哈哈'

/*注意：
     使用 export 向外暴露的成员，只能使用 { } 的形式来接收，这种形式叫做 【按需导出】
     export 可以向外暴露多个成员， 同时如果某些成员在我们import 的时候不需要，则可以不在 {}  中定义
     使用 export 导出的成员，必须严格按照导出时候的名称来使用  {}  按需接收；
     使用 export 导出的成员，如果想换个名称来接收，可以使用 as 来起别名；
*/

#2. main.js
import minfo3, { title as title123, content } from './test.js'
console.log(minfo3)    //这里的minfo3就是test.js中所暴露出来的default info
console.log(title123 + ' --- ' + content)

```

#### 2.4.2 .vue中的数据导出

```javascript
#login.vue

<template>
  <div>
    <h1>这是登录组件，使用 .vue 文件定义出来的 --- {{msg}}</h1>
    <button @click="show">点我</button>
  </div>
</template>

<script>
  export default {
    data() {
      // 注意：组件中的 data 必须是 function
      return {
        msg: "123321"
      };
    },
    methods: {
      show() {
        console.log("调用了 login.vue 中的 show 方法");
      }
    }
  };
</script>

```

### 2.5 vue-router使用

	[vue-router官网](https://router.vuejs.org/)


#### 2.5.1 基本使用

```javascript
#1. 安装路由模块
npm install vue-router --save

#2.login.vue
<template>
  <div>
    <h1>这是登录组件，使用 .vue 文件定义出来的 --- {{msg}}</h1>
    <button @click="show">点我</button>
  </div>
</template>

<script>
  export default {
    data() {
      // 注意：组件中的 data 必须是 function
      return {
        msg: "123321"
      };
    },
    methods: {
      show() {
        console.log("调用了 login.vue 中的 show 方法");
      }
    }
  };
</script>

<style>
</style>

#3.register.vue
<template>
    <div>
        <h1>这是注册组件</h1>
    </div>
</template>

#4.main.js
import Vue from 'vue'

//1.导入VueRouter并且安装
import VueRouter from 'vue-router'
Vue.use(VueRouter)

//2.导入组件
import login from './login.vue'
import register from './register.vue'

//3.创建路由对象
var router = new VueRouter({
    routes: [
        { path: '/', redirect: '/login' },
        { path: '/login', component: login },
        { path: '/register', component: register }
    ]
});


var vm = new Vue({
    el: '#app',
    data: {
        msg: '123'
    },
    //4.挂载路由
    router:router
})

#5.index.html
<div id="app">
    <router-link to="/login">登陆</router-link>
    <router-link to="/register">注册</router-link>
    <router-view></router-view>
</div>

#6.webpack.config.js参照之前的配置

```

#### 2.5.2 vue-router和render结合使用

```javascript
# 在上面案例的基础上
#1.新增account.vue
<template>
    <div>
        <h1>账户组件</h1>
		<!--组件中的路由-->
        <router-link to="/login">登陆</router-link>
        <router-link to="/register">注册</router-link>
        <router-view></router-view>
    </div>
</template>

#2.main.js
import account from './account.vue'
var vm = new Vue({
    el: '#app',
    data: {
        msg: '123'
    },
    //渲染组件替换el
    render:e=>e(account),
    router:router
})

#3.index.html
<div id="app">

</div>

```

#### 2.5.3 路由嵌套

```javascript
# 在上面案例的基础上
#1. 新建subcom/findpwd.vue
<template>
    <div>
        <h1>找回密码</h1>
    </div>
</template>

#2. 新建subcom/thirdpartlogin.vue
<template>
    <div>
        <h1>微信登陆</h1>
    </div>
</template>

#3.修改login.vue
<template>
  <div>
    <h1>这是登录组件，使用 .vue 文件定义出来的 --- {{msg}}</h1>
    <button @click="show">点我</button>

    <router-link to="/login/findpwd">找回密码</router-link>
    <router-link to="/login/thirdpartlogin">第三方登陆</router-link>
    <router-view></router-view>
  </div>
</template>

<script>
  export default {
    data() {
      // 注意：组件中的 data 必须是 function
      return {
        msg: "123321"
      };
    },
    methods: {
      show() {
        console.log("调用了 login.vue 中的 show 方法");
      }
    }
  };
</script>

#4.在main.js中配置子路由
var router = new VueRouter({
    routes: [
        { path: '/', redirect: '/login' },
        { path: '/login',
          component: login,
          children:[
              {path:'findpwd',component:findpwd},
              {path:'thirdpartlogin',component:thirdpartlogin}
          ]
        },
        { path: '/register', component: register }
    ]
});

```

### 2.6 组件样式

```javascript
# 在上面代码的基础上
#login.vue新增样式
<style scoped>
  /*scoped作用域，如果不加scoped，则h1的样式会默认使用为全局而非当前组件*/
  h1{
    color: red;
  }
</style>

#account.vue新增样式
<style lang="scss" scoped>
    /*要编译sass只需要lang="scss"就可以
      scoped 推荐使用*/
    body{
        h1{
            background-color: blue;
        }
    }
</style>


//scoped的原理：scoped实际上是给当前组件的所有元素加上data-v-f626523的属性来实现的样式隔离

```

### 2.7 抽离路由为单独的模块

```javascript
#1.main.js
import Vue from 'vue'
//导入VueRouter并且安装
import VueRouter from 'vue-router'
Vue.use(VueRouter)

import account from './account.vue'
//导入路由模块
import router from './router.js'

var vm = new Vue({
    el: '#app',
    data: {
        msg: '123'
    },
    render:e=>e(account),
    //挂载路由
    router:router
})


#2.router.js
import VueRouter from 'vue-router'
//导入组件
import login from './login.vue'
import register from './register.vue'

import findpwd from './subcom/findpwd.vue'
import thirdpartlogin from './subcom/thirdpartlogin.vue'

//创建路由对象
var router = new VueRouter({
    routes: [
        { path: '/', redirect: '/login' },
        { path: '/login',
          component: login,
          children:[
              {path:'findpwd',component:findpwd},
              {path:'thirdpartlogin',component:thirdpartlogin}
          ]
        },
        { path: '/register', component: register }
    ]
});

//导出路由对象
export default router;

```

# 3.vuex介绍

## 3.1 vuex概念

	https://vuex.vuejs.org/zh/installation.html
	
	vuex 是 Vue 配套的 公共数据管理工具，它可以把一些共享的数据保存到 vuex 中，方便 整个程序中的任何组件直接获取或修改我们的公共数据；

## 3.2 vuex的基本使用

```javascript
#1.拷贝原项目中除了node_modules之外的其他信息，运行npm install安装模块 

#2.安装vuex
 npm i vuex -S

#3.main.js
import Vue from 'vue'
import Vuex from 'vuex'

// 注册vuex到vue中
Vue.use(Vuex)

// new Vuex.Store()实例，得到一个数据仓储对象
// 可以在组件中通过this.$store.state.xx 来访问store中的数据
var store = new Vuex.Store({
    //state相当于组件中的data
    state: {
        count: 0
    },
    //如果要修改store中state的值，需要调用 mutations提供的方法，可以通过this.$store.commit('方法名')来调用
    mutations: {
        increment(state) {
            state.count++
        },
        //mutations函数参数列表中最多支持两个参数，其中参数1是state； 参数2是通过commit提交过来的参数；
        subtract(state, obj) {
            console.log(obj)
            state.count -= obj.step;
        }
    },
    getters: {
        //这里的getters只负责对外提供数据，不负责修改数据，如果想要修改 state 中的数据需要在mutations中修改
        optCount: function (state) {
            return '当前最新的count值是：' + state.count
        }
    }
})

// 总结：
// 1. state中的数据，不能直接修改，如果想要修改，必须通过 mutations
// 2. 如果组件想要直接 从 state 上获取数据： 需要 this.$store.state.***
// 3. 如果组件想要修改数据，必须使用 mutations 提供的方法，需要通过 this.$store.commit('方法的名称'， 唯一的一个参数)
// 4. store中state上的数据在对外提供的时候建议做一层包装，推荐使用 getters。调用的时候则用this.$store.getters.***


import App from './App.vue'

const vm = new Vue({
    el: '#app',
    render: c => c(App),
    //将vuex创建的store挂载到VM实例上，只要挂载到了 vm 上，任何组件都能使用store来存取数据
    store
})

#4.index.html
<body>
    <div id="app"></div>
</body>

#5.App.vue
<template>
    <div>
        <h1>这是 App 组件</h1>
        <hr>
        <counter></counter>
        <hr>
        <amount></amount>
    </div>
</template>

<script>
    import counter from "./components/counter.vue";
    import amount from "./components/amount.vue";

    export default {
        data() {
            return {};
        },
        components: {
            counter,
            amount
        }
    };
</script>

#6.components/amount.vue
<template>
  <div>
    <h3>{{ $store.getters.optCount }}</h3>
  </div>
</template>

#7.components/counter.vue
<template>
  <div>
    <input type="button" value="绑定事件-减少" @click="sub">
    <input type="button" value="绑定事件-增加" @click="add">
    <br>
    <input type="text" v-model="$store.state.count">
  </div>
</template>

<script>
export default {
  data() {
    return {
    };
  },
  methods: {
    add() {
       this.$store.commit("increment");
    },
    sub() {
      this.$store.commit("subtract",{ step:3});
    }
  }
};
</script>

```

## 3.3 vuex异步修改状态

	mutation的使用局限：mutation必须是同步函数，如果有异步操作，可以在actions完成


```javascript
#main.js中给store添加actions的方法
var store = new Vuex.Store({
    // state相当于组件中的data
    state: {
        count: 0
    },
    // 如果要修改store中state的值，需要调用 mutations提供的方法，可以通过this.$store.commit('方法名')来调用
    mutations: {
        increment (state) {
            state.count++
        },
        // mutations函数参数列表中最多支持两个参数，其中参数1是state； 参数2是通过commit提交过来的参数；
        subtract (state, obj) {
            console.log(obj)
            state.count -= obj.step
        }
    },
    getters: {
        // 这里的getters只负责对外提供数据，不负责修改数据，如果想要修改 state 中的数据需要在mutations中修改
        optCount: function (state) {
            return '当前最新的count值是：' + state.count
        }
    },
    actions: {
        // action中的方法允许异步事件
        increment ({ commit }) {
            setTimeout(() => {
                // 提交mutations中的increment方法
                commit('increment')
            }, 1000)
        },
        subtract ({ commit }, obj) {
            // 返回一个Promise，以便做回调
            return new Promise((resolve, reject) => {
                setTimeout(() => {
                    commit('subtract', obj)
                    resolve()
                }, 1000)
            })
        }
    }
})

#components/counter.vue
methods: {
    add () {
        // dispatch 触发指定的action
        this.$store.dispatch("increment")
    },
        sub () {
            this.$store.dispatch("subtract", { step: 3 })
                .then(() => {
                console.log("减少操作完成")
            })
        }
}

```

## 3.4 vuex的模块

```javascript
#1.使用Vuex.Store中的modules声明多个模块
const moduleA = {
  state: {
    count: 1
  },
  mutations: {

  }
}

const moduleB = {
  state: {
    count: 11
  },
  mutations: {

  }
}

const store = new Vuex.Store({
  modules: {
    a: moduleA,
    b: moduleB
  }
})

#2.使用不同模块中的数据
<div>
    <h3>{{ $store.state.a.count }}</h3>
    <h3>{{ $store.state.b.count }}</h3>
</div>

```

## 3.5 刷新网页时vuex缓存

https://blog.csdn.net/weixin_42233917/article/details/82217596

# 4.vue中UI框架

## 4.1 常用框架介绍

PC桌面端UI框架：

```javascript
1. iview          （用户评分高功能多炫酷，解决和避免了其他UI框架出现的一些小问题）
2. bootstrap  （使用用户最多）
3. ElementUI  （饿了么团队研发，使用较多不过里还有些小bug）

```

手机端UI框架：

```javascript
1.BUI       
   http://www.easybui.com/docs/  很不错官网有视频介绍。视频里有介绍非常非常实用的工具，建议去看官网视频。
这个框架有现成的模板只需要一个创建模板的命令就可以创建一个大致的具有交互功能的页面。
2.vux  
  vux 基于WeUI和Vue(2.x)开发的移动端UI组件库
  基于webpack+vue-loader+vux可以快速开发移动端页面，配合vux-loader方便你在WeUI的基础上定制需要的样式。
3.Mint UI
  Mint UI 由饿了么前端团队推出的，Mint UI 是一个基于 Vue.js 封装的移动端组件库

```

## 4.2 MintUI 框架介绍

[Github 仓储地址](https://github.com/ElemeFE/mint-ui)

[Mint-UI官方文档](http://mint-ui.github.io/#!/zh-cn)

### 4.2.1 css组件使用

```javascript
1.安装MintUI
   npm install mint-ui -S

2.main.js 导入MintUI，并注册到Vue
  import Vue from 'vue'
  import Mint from 'mint-ui';
  import app from "./app.vue"

  Vue.use(Mint);

  var vm = new Vue({
    el: '#app',
    data: {
        msg: '123'
    },
    render:e=>e(app)
  })
  
3.main.js 导入MintUI的样式
  import 'mint-ui/lib/style.css'
  
4.app.vue
<template>
    <div>
        <h1>app组件</h1>
        <mt-button type="primary" size="large" plain>primary</mt-button>
        <mt-button type="danger" size="small" disabled>danger</mt-button>

        <mt-button type="danger" icon="more" @click="show">more</mt-button>
    </div>
</template>

```

### 4.2.2 js组件使用-toast

```javascript
#在上面代码的基础上
#app.vue
<template>
    <div>
        <h1>app组件</h1>
        <mt-button type="primary" size="large" plain>primary</mt-button>
        <mt-button type="danger" size="small" disabled>danger</mt-button>

        <mt-button type="danger" icon="more" @click="show">more</mt-button>
    </div>
</template>

<script>
    // 按需导入 Toast 组件
    import { Toast } from "mint-ui";

    export default {
        data() {
            return {
                toastInstanse: null
            };
        },
        created() {
        },
       methods:{
            show(){
                if(this.toastInstanse){
                    return;
                }
                this.toastInstanse = Toast({
                    message: "这是消息",
                    duration: -1, // 如果是 -1 则弹出之后不消失
                    position: "top",
                    iconClass: "glyphicon glyphicon-heart", // 设置 图标的类
                    className: "mytoast" // 自定义Toast的样式，需要自己提供一个类名
                });
                setTimeout(()=>{
                    this.toastInstanse.close();
                    this.toastInstanse = null;
                },1000)
            }
        }
    };
</script>

<!--注意：这边style不需要加scoped，scoped样式只能作用于当前组件，不能作用于当前组件的子组件-->
<style>
    .mytoast{
        color: red!important;
    }
</style>

#注意：toast中不自带字体图标，所以我们使用bootstrap中的字体图标
//1.安装
   npm install bootstrap@3.3.5
//2.main.js中引入boostrap样式
   import 'bootstrap/dist/css/bootstrap.css'

```

### 4.2.3 按需导入组件

	如果完全导入Maint UI，打包后的bundle.js有将近1.5M，为了减少打包后的体积，我们可以进行按需导入。


http://mint-ui.github.io/docs/#/zh-cn2/quickstart

```javascript
//1.安装babel-plugin-component插件
	npm install babel-plugin-component -D
//2.修改babel的配置文件
	{
      "presets": ["env", "stage-0"],
      "plugins": ["transform-runtime",
        ["component", [
          {
            "libraryName": "mint-ui",
            "style": true
          }
        ]]]
    }
 //3.修改main.js
 import Vue from 'vue'
 //按需导入button
 import { Button} from 'mint-ui'

 import 'mint-ui/lib/style.css'
 import 'bootstrap/dist/css/bootstrap.css'
 import app from "./app.vue"
 //注册button
 Vue.component(Button.name, Button)

 var vm = new Vue({
    el: '#app',
    data: {
        msg: '123'
    },
    render:e=>e(app)
 })

```

## 4.3 使用 MUI 组件

[官网首页](http://dev.dcloud.net.cn/mui/)

[文档地址](http://dev.dcloud.net.cn/mui/ui/)

### 4.3.1 MUI和Mint-UI区别

	MUI不同于Mint-UI，MUI只是一套开发出来的代码片段，配套了样式和html代码，类似于bootstrap。而Mint-UI是真正的vue组件，可以无缝的和vue项目集成开发。因此从体验上，Mint-UI体验更好，因为这是已经封装好的vue组件。理论上，任何项目都可以使用bootstrap和MUI，而Mint-UI只适用于vue


### 4.3.2 MUI的使用

	MUI不能使用npm进行下载，需要手动下载然后导入到项目。
	
	    由于MUI不是vue组件，因此不需要导入组件库然后注册组件，只需要导入样式之后就可以在页面使用了。


```javascript
#1. 将MUI下的fonts\css\js文件放入到项目的lib目录下
#2.main.js引入MUI的样式	
	import "../lib/mui/css/mui.css"
#3.app.vue中使用MUI的组件
<template>
    <div>
        <h1>app组件</h1>
        <mt-button type="primary" size="large" plain>primary</mt-button>
        <mt-button type="danger" size="small" disabled>danger</mt-button>

        <mt-button type="danger" icon="more" @click="show">more</mt-button>

        <!--引入MUI组件-->
        <form class="mui-input-group">
            <div class="mui-input-row">
                <label>用户名</label>
                <input type="text" class="mui-input-clear" placeholder="请输入用户名">
            </div>
            <div class="mui-input-row">
                <label>密码</label>
                <input type="password" class="mui-input-password" placeholder="请输入密码">
            </div>
            <div class="mui-button-row">
                <button type="button" class="mui-btn mui-btn-primary" >确认</button>
                <button type="button" class="mui-btn mui-btn-danger" >取消</button>
            </div>
        </form>
    </div>
</template>

#注意点：MUI中有字体图标，所以需要在webpack.config.js中添加下面的url加载规则
{ test: /\.(png|jpg|gif|ttf)$/, use: 'url-loader' }

```
