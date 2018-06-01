## less(css预处理器)
[参考资料](https://less.bootcss.com/#)
### 安装
`npm install -g less`
### 命令行使用
```
安装完成后，可以从命令行调用编译器，如下所示：
lessc styles.less
这将输出编译后的CSS。要将CSS结果保存到您选择的文件，请使用：
lessc styles.less styles.css
要输出缩小，你可以使用CSS clean-css插件。当安装插件时，缩小的CSS输出用--clean-css选项指定：
lessc --clean-css styles.less styles.min.css
```

### less的基础
#### 变量
```css
@nice-blue: #5B83AD;
@light-blue: @nice-blue + #111;

#header {
  color: @light-blue;
}
```
#### 混合（Mixins）
> 混合是一种将一组属性从一个规则集合（另一个规则集合）（“混入”）的方式

```css
.bordered {
  border-top: dotted 1px black;
  border-bottom: solid 2px black;
}
.bordered-02 (@border-left) {
  border-left: solid @border-left black;
}
.bordered-03 (@border-right:4px) {
  border-right: solid @border-right black;
}
#menu a {
  color: #111;
  .bordered;
  .bordered-02(3px);
  .bordered-03();
}
```
#### 匹配模式
```css
.triangele (top,@w:5px,@c:#ccc){
  border-width: @w;
  border-color: @c transparent transparent transparent;
  border-style: solid dashed dashed dashed;
}
.triangele (botoom,@w:5px,@c:#ccc){
  border-width: @w;
  border-color: transparent transparent @c transparent;
  border-style: dashed dashed solid dashed;
}
// @_不论匹配到上面哪个，都会执行
.triangele (@_,@w:5px,@c:#ccc){
  width: 0;
  height: 0;
  overflow: hidden;
}
.diaoyong{
  .triangele(top)
  //传入top就调上面的，传入bottom就调下面的
}
```

#### 嵌套（Nesting）
$代表当前父代选择器
```css
.clearfix {
  display: block;
  zoom: 1;
  &:after {
    content: " ";
    display: block;
    font-size: 0;
    height: 0;
    clear: both;
    visibility: hidden;
  }
}
```
> 嵌套的规则和冒泡

* 像规则一样，@media或者@supports可以像选择器一样嵌套。规则放在顶部，相对规则集中的其他元素的相对顺序保持不变。这叫做冒泡。

```css
.component {
  width: 300px;
  @media (min-width: 768px) {
    width: 600px;
    @media  (min-resolution: 192dpi) {
      background-image: url(/img/retina2x.png);
    }
  }
  @media (min-width: 1280px) {
    width: 800px;
  }
}
编译为：
.component {
  width: 300px;
}
@media (min-width: 768px) {
  .component {
    width: 600px;
  }
}
@media (min-width: 768px) and (min-resolution: 192dpi) {
  .component {
    background-image: url(/img/retina2x.png);
  }
}
@media (min-width: 1280px) {
  .component {
    width: 800px;
  }
}
```
#### 运算（Operations）
```css
@conversion-1: 5cm + 10mm;
结果：6cm
@conversion-2: 2 - 3cm - 5mm;
结果：-1.5cm
@incompatible-units: 2 + 5px - 3cm;
结果：4px
@base: 5%;
@filler: @base * 2;
结果：10%
@other: @base + @filler;
结果：15%
@base: 2cm * 3mm;
结果：6cm
@color: #224488 / 2;
结果：#112244
background-color: #112244 + #111;
结果：#223355
```
#### calc() 特例

> 为了与 CSS 保持兼容，calc() 并不对数学表达式进行计算，但是在嵌套函数中会计算变量和数学公式的值。

```css
@var: 50vh/2;
width: calc(50% + (@var - 20px));
结果：calc(50% + (25vh - 20px))
```
#### 转译（避免编译）
```css
.test{
    width:~'calc(300px - 30px);' //会原封不动在css中输出calc(300px - 30px)
}
```

#### 命名空间和访问器
>  有时候，可能想要将你的mixin分组，或为了组织目的，或者只是提供一些封装。在Less中可以很直观地做到这一点。

```css
#bundle () {
  .button {
    display: block;
    border: 1px solid black;
    background-color: grey;
    &:hover {
      background-color: white
    }
  }
  .tab {
    color: #ccc;
  }
}
.button{
  #bundle .button
}
a{
  #bundle .tab
}
```

#### @import（导入）
```css
@import './a.less'; //引入less文件，可以省略后缀
@import './a.css';  //编译时不会编译到css文件中
@import (less) './a.css';  //编译时会编译到css文件中
```

##### 注释
```
// 不会被编译
/*会被编译*/
```
