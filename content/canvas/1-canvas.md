canvas是一个基于状态的绘制环境
### 创建一个画布
`<canvas id="myCanvas" width="400" height="400"></canvas>`
### 绘制图像
```
  首先获得canvas元素
var canvas=document.getElementById("myCanvas")
  然后创建context对象
var context=canvas.getContext("2d")
getContext("2d") 对象是内建的 HTML5 对象，拥有多种绘制路径、矩形、圆形、字符以及添加图像的方法。context是一个2d的绘图上下文环境，canvas绘图的所有接口都是由context提供的。
至此我们就得到了一个可以作图的canvas画布了。
```
### 路径
```
context.beginPath(); 代表开始一个全新的绘制
context.closePath(); 代表当前的路径要封闭以及结束
由于canvas是基于状态绘制图形的，当要画多条宽度且样式不同的线段时，canvas会自动基于最后一次的状态绘制，所以此时要使用beginPath()来重新开始一个新绘制；而当绘制多边形时，结合beginPath()和closePath()可以绘制出正确且完整的封闭图形。
```
### 直线
#### 线段
```
context.moveTo(x,y) 定义线条开始坐标（指将笔尖移到某个地方）
context.lineTo(x,y) 定义线条结束坐标（指画线到某个地方）
context.stroke() 描边
  线条的基本属性：
context.lineWidth 设置线条宽度（取值为数值）
context.strokeStyle 设置线条样式（一般取值为颜色值）
context.lineCap 设置线条的两头的样式（取值有butt(default)[默认]、round[圆]、square[方]）
context.lineJoin 设置线条的两头的样式（取值有miter(default)[默认]、bevel[斜接]、round[圆]）
当设置context.miterLimit的时候，如果尖角的宽度大于这个值时，会以bevel的形式显示。
```
#### 矩形
```
context.rect(x,y,width,height) x,y代表矩形的起始的坐标，width代表宽度，height代表高度
context.fillRect(x,y,width,height) 可以直接绘制出填充的矩形
strokeRext(x,y,width,height) 可以直接绘制出描边的矩形
context.clearRect(x,y,width,height) 可以清空一个矩形区域，多用在动画的绘制中
```
### 曲线
#### 圆形
```
context.arc(x,y,r,start,stop,anticlockwise(可选)) x,y代表圆心的坐标，r代表半径，start,stop代表圆弧的起始和结束的位置，anticlockwise是一个可选参数，设置绘图是否按逆时针方向，默认为false即顺时针方向绘制。
context.arc(150, 150, 100, 0, 0.3 * Math.PI, true)
注意这里圆弧的起始位置，0PI在x轴的正方向（右），0.5PI在y轴正方向（下），1PI在x轴负方向（左），1.5PI在y轴负方向（上），2PI又回到x轴正方向（右）。且不论顺时针绘制还是逆时针绘制 0-2PI的位置是不变的。
```
#### 弧形
```
context.moveTo(x0,y0)
context.arcTo(x1,y1,x2,y2,radius)
x0、y0指的是圆弧的起始点；x1、y1，x2、y2指的切线的两个点。而这三个点行程的两条线则是圆弧的两条切线，但切点不一定在这两条辅助线上。
```
#### 二次贝塞尔曲线
```
context.moveTo(x0,y0)
context.quadraticCurveTo(x1,y1,x2,y2)
此方法和画弧线的方法类似，不同的是(x0,y0)就是曲线的起点，而(x2,y2)就是曲线的终点。因为这个方法也比acrTo()更灵活更实用
```
#### 三次贝塞尔曲线
```
context.moveTo(x0,y0)
context.bezierCurveTo(x1,y1,x2,y2,x3,y3)
此方法里(x1,y1)和(x2,y2)是两个控制点，而(x0,y0)和(x3,y3)则是起始点和结束点
```
### 填充
```
context.fill()
  填充的基本属性：
context.fillStyle设置填充样式
注意当需要绘制既有填充也有描边的图案的时候，需要先填充后描边，否则描边的一般宽度会被填充覆盖
```
#### 线性渐变
```
var gradient = context.createLinearGradient(xstart,ystart,xend,yend)
gradient.addColorStop(stop,color)
xstart、ystart和xend、yend形成两个坐标点，而其连成的一条线为渐变线，渐变线表示的是颜色沿着这条线渐变；而stop参数的取值为0-1之间的一个浮点数，表示的是color这个颜色所在的位置
```
#### 径向渐变：
```
var gradient = context.createRadialGradient(x0,y0,r0,x1,y1,r1)
gradient.addColorStop(stop,color)
径向渐变和线性渐变的原理很像，x0,y0,r0和x1,y1,r1形成了两个圆，而径向渐变就是按着这两个圆渐变的，第二个方法与线性渐变相同
```
#### 图片、画布、视频填充
```
var pattern = context.createPattern(img,repeat-style);
repeat-style有四个参数：no-repeat、repeat-x、repeat-y、repeat
注意这里的第一个参数img除了用img还可以用canvas、video进行填充。同时这里使用的填充方式也可以使用在strokeStyle()方法上
```
### 图形变换
```
  图形变换一般分不开三个方法：
context.translate(x,y)
context.rotate(deg)
context.scale(sx,sy)
注意在canvas中图形变换的效果是叠加的，所以第二次变换相对则不是从初始状态开始，这样造成了一些麻烦。但是用context.save()和context.restore()可以保存变换的状态，使其中一个变换不影响其他变换。同时注意scale变换会影响起始点坐标以及边框的宽度。
  还有一个高级方法：
context.transform(a,b,c,d,e,f)
其中的a,b,c,d,e,f实际上是一个单位矩阵中的值
|a,c,e|
|b,d,f|
|0,0,1|
a,d代表水平、垂直缩放;b,c代表水平、垂直倾斜;e,f代表水平、垂直位移
当出现变换次数过多，已经不知道怎么恢复时可以使用context.setTransform()方法，代表了首先恢复原始状态，然后按设置的状态进行变换
```
### 文字
```
context.font = "bold 40px Arial"
context.fillText(string,x,y,[maxlen]) 实心字体
context.strokeText(string,x,y,[maxlen]) 空心字体
可选参数[manxlen]表示绘制这一段文字的最长宽度，单位是px。

  字体的基本属性：
context.font设置文字样式
context.font = "font-style font-variant font-weight font-size font-family"，默认值为"20px san-serif"。
font-style默认值为normal[default]，可选italic[斜体]，oblique[倾斜字体]。
font-variant默认值为normal[default]，可选small-caps[小型大写字体]（在英文中才有效果）。
font-weight默认值为normal[default]，可选lighter[更细]，bold[粗],bolder[更粗]。还可以使用100-900来控制，100-400是normal，500-700是bold。
font-size、font-family和CSS类似就不多做介绍了。

context.textAlign设置文字左右对齐方式（取值有left,center,right）
context.textBaseLine设置文字的上下对其方式（取值有top,middle,bottom,alphabeticdefault,ideographic(基于方块文字的基准线),hanging(基于印度语的基准线)）
context.measureText(string).width可以得到整个文字的宽度
```
### 图片
```
var img = new Image();
img.src = "***.jpg";
context.drawImage(img,x,y)
```
### 其他
#### 阴影
```
context.shadowColor 设置阴影颜色
context.shadowOffsetX 设置阴影水平位移距离
context.shadowOffsetY 设置阴影垂直位移距离
context.shadowBlur 设置阴影模糊距离
```
#### 合成
```
globalAlpha设置全局透明度（默认值为1，取值范围0-1）
globalCompositeOperation设置图像在重叠时的状态（取值有sourse-overdefault，destination-over(先绘制的在后绘制的上面)，一共有九种取值：sourse-over,sourse-atop,sourse-in,sourse-out,destination-over,destination-atop,destination-in,destination-out,lighter,copy,xor）
```
#### 剪辑区域
```
context.clip()设置接下来的绘制区域在被剪辑的区域内
```
#### 点击检测
```
context.isPointInPath(x,y)检测这个点是否在当前规划的路径内
  标准的获取鼠标在canvas画布内的点击位置的方法：
var x=event.clientX - canvas.getBoundingClientRect().left;
var y=event.clientY - canvas.getBoundingClientRect().top;
```
#### 将自己的方法加入context上下文对象中
```
anvasRenderingContext2D.prototype.你自己定义的方法 = function(){}
```
