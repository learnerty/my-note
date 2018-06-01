## 学习一下webpack的一些知识

### 概述
Webpack 是当下最热门的前端资源模块化管理和打包工具。它可以将许多松散的模块按照依赖和规则打包成符合生产环境部署的前端资源。还可以将按需加载的模块进行代码分隔，等到实际需要的时候再异步加载。通过 loader 的转换，任何形式的资源都可以视作模块。webpack 是一个现代 JavaScript 应用程序的模块打包器(module bundler)。当 webpack 处理应用程序时，它会递归地构建一个依赖关系图(dependency graph)，其中包含应用程序需要的每个模块，然后将所有这些模块打包成少量的 bundle - 通常只有一个，由浏览器加载。  
它是高度可配置的，但是，在开始前需要先理解四个核心概念：入口(entry)、输出(output)、loader、插件(plugins)。  

首先看一个简单的例子，然后再来学习四个核心概念，创建一个`webpack.config.js`文件，这是webpack的配置文件。这个小例子中，包含了四个核心的概念，让我们一起看一看
```js
const HtmlWebpackPlugin = require('html-webpack-plugin'); //installed via npm
const webpack = require('webpack'); //to access built-in plugins
const path = require('path');

const config = {
  entry: path.resolve(__dirname, 'src/index.js'), //入口文件是当前项目下src文件夹下的index.js文件
  output: {
    path: path.resolve(__dirname, 'dist'), //输出的路径是dist文件夹
    filename: 'webpack.bundle.js' //输出的文件名是webpack.bundle.js
  },
  module: {
    rules: [ //这里定义了loader,需要注意的是，loader是定义在module.rules中的，必须包含test和use两个属性，下面的含义是当碰到「在 require()/import 语句中被解析为 '.txt' 的路径」时，在对它打包之前，先使用 raw-loader 转换一下。
      { test: /\.txt$/, use: 'raw-loader' }
    ]
  },
  plugins: [ //插件，使用了html-webpack-plugin，更多详细用法这里不做介绍
    new webpack.optimize.UglifyJsPlugin(),
    new HtmlWebpackPlugin({template: './src/index.html'})
  ]
};

module.exports = config;
```

下面来仔细的学习下webpack的四个核心概念
#### 入口（entry）
##### 单个入口文件的写法
`(webpack.config.js)`
```js
const config = {
  entry: './path/to/my/entry/file.js'
};
module.exports = config;
是下面的简写形式,我们一般采用上面的方法
const config = {
  entry: {
    main: './path/to/my/entry/file.js'
  }
};
```
##### 多个入口文件的写法（对象语法）
```js
const config = {
  entry: {
    app: './src/app.js',
    vendors: './src/vendors.js'
  }
};
```
#### 输出（output）
##### 单个文件入口的输出
```js
output: {
  filename: 'bundle.js',
  path: '/home/proj/public/assets'
}
```
##### 多个入口文件的输出
```js
output: {
  filename: '[name].js', //【name】为占位符，输出的名称为入口文件的名称
  path: __dirname + '/dist'
}
```
#### 加载器(Loaders)
loader 用于对模块的源代码进行转换。loader 可以使你在 import 或"加载"模块时预处理文件。  

有三种使用 loader 的方式：配置、内联、CLI,但是推荐使用配置的方式进行处理，这里也只会介绍这一种。  

module.rules 允许你在 webpack 配置中指定多个 loader。下面的事例是对css文件进行转换的loader。下面介绍了两种方式，先执行的放在后面。
```js
module: {
  rules: [
    {
      test: /\.css$/,
      use: [
        { loader: ['style-loader'](/loaders/style-loader) },
        {
          loader: ['css-loader'](/loaders/css-loader),
          options: {
            modules: true
          }
        }
      ]
    }
  ]
}

module: {
  rules: [
    {
      test: /\.css$/,
      use: ['style-loader', 'css-loader']
    }
  ]
}
```
#### 插件(Plugins)
插件是 wepback 的支柱功能。插件目的在于解决 loader 无法实现的其他事。由于插件可以携带参数/选项，必须在 webpack 配置中，向 plugins 属性传入 new 实例。
```js
const HtmlWebpackPlugin = require('html-webpack-plugin'); //通过 npm 安装
const webpack = require('webpack'); //访问内置的插件
const path = require('path');

const config = {
  entry: './path/to/my/entry/file.js',
  output: {
    filename: 'my-first-webpack.bundle.js',
    path: path.resolve(__dirname, 'dist')
  },
  module: {
    loaders: [
      {
        test: /\.(js|jsx)$/,
        use: 'babel-loader'
      }
    ]
  },
  plugins: [
    new webpack.optimize.UglifyJsPlugin(),
    new HtmlWebpackPlugin({template: './src/index.html'})
  ]
};
module.exports = config;
```
