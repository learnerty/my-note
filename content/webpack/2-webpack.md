这部分用来介绍webpack的使用。  
webpack可以在项目中安装或者全局安装，不过推荐使用项目内安装的方式。  
1. 首先，安装初始化一个node项目
```js
mkdir webpackTest
cs webpackTest
npm init -y
npm install --save-dev webpackTest
```
2. 如果想要在项目中使用import一个css文件或less等多种css样式文件，需要装一些包
```js
npm install --save-dev style-loader css-loader less-loader postcss-loader
```
 * 之后创建一个webpack.config.js文件,写入如下代码
 ```js
 const path = require('path');
 module.exports = {
   //入口文件
   entry: path.resolve(__dirname, 'src/index.js'),
   //输出
   output: {
     filename: 'bundle.js',
     path: path.resolve(__dirname, 'dist')
   },
   //loaders, postcss的功能是为css样式自动添加厂商前缀，解决兼容问题
   module: {
     rules: [
       {
         test: /\.css$/,
         use: [
           'style-loader',
           'postcss-loader',
           'css-loader'
         ]
       },
       {
         test: /\.less/,
         use: [
           'style-loader',
           'postcss-loader',
           'less-loader'
         ]
       }
     ]
   }
 };
 ```

 * 当然，我们一般都会使用`extract-text-webpack-plugin`插件抽离css样式，防止将样式打包在js中引起页面样式加载错乱的现象
 ```js
 首先安装该插件：
    npm install extract-text-webpack-plugin --save-dev
 该插件有三个参数：
    use:指需要什么样的loader去编译文件
    fallback:编译后用什么loader来提取css文件
    publicfile:用来覆盖项目路径,生成该css文件的文件路径
 如何使用：
 const ExtractTextPlugin = require("extract-text-webpack-plugin");
 module: {
    rules: [
      {
        test: /\.css$/,
        use: ExtractTextPlugin.extract({
          fallback: "style-loader",
          use: ["css-loader","postcss-loader"]
        })
      }
    ]
  }
 ```
3. 对图片和字体的处理我们可以使用`file-loader`  
`npm install --save-dev file-loader`
```js
module: {
  rules: [
    {
      test: /\.(png|svg|jpg|gif)$/,
      use: [
        'file-loader'
      ]
    },
    {
      test: /\.(woff|woff2|eot|ttf|otf)$/,
      use: [
        'file-loader'
      ]
    }
  ]
}
```
