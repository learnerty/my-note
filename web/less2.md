## less函数

### 杂项功能
#### 颜色
color()  
分析颜色，将表示颜色的字符串变成颜色。例：`color("#aaa")` 输出：`#aaa`
#### 图片
> 注意：这个功能需要由每个环境来实现。它目前仅在节点环境中可用。

* 图片大小:image-size()  
从文件中获取图像尺寸。例：`image-size("file.png")` 输出：`10px(宽) 10px(高)`
* 图片宽度:image-width()  
从文件中获取图像尺寸。例：`image-width("file.png")` 输出：`10px(宽)`
* 图片高度:image-height()  
从文件中获取图像尺寸。例：`image-height("file.png")` 输出：`10px(高)`
#### 兑换
convert()  
将数字从一个单位转换为另一个单位。第一个参数包含一个带有单位的数字，第二个参数包含单位。如果这些单位是兼容的，那么该号码将被转换。如果它们不兼容，则第一个参数将不加修改地返回。

```
兼容单元组：
长度：m，cm，mm，in，pt和pc，
时间：s和ms，
角度：rad，deg，grad和turn。

例：
convert(9s, "ms")
convert(14cm, mm)
convert(8, mm)
输出：
9000ms
140mm
8
```
