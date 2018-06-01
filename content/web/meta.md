整理的比较全的meta标签用法
## html的常用meta总结
1. Meta标签大全

```html
<!-- 声明文档使用的字符编码 -->
   <meta charset='utf-8'>

   <!-- 优先使用 IE 最新版本和 Chrome -->
   <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1"/>

   <!-- 页面描述 -->
   <meta name="description" content="不超过150个字符"/>

   <!-- 页面关键词 -->
   <meta name="keywords" content=""/>

   <!-- 网页作者 -->
   <meta name="author" content="name, email@gmail.com"/>

   <!-- 搜索引擎抓取 -->
   <meta name="robots" content="index,follow"/>

   <!-- 为移动设备添加 viewport -->
   <meta name="viewport" content="initial-scale=1, maximum-scale=3, minimum-scale=1, user-scalable=no">
   <!-- `width=device-width` 会导致 iPhone 5 添加到主屏后以 WebApp 全屏模式打开页面时出现黑边 http://bigc.at/ios-webapp-viewport-meta.orz -->


   <!-- iOS 设备 begin -->
       <!-- 添加到主屏后的标题（iOS 6 新增） -->
       <meta name="apple-mobile-web-app-title" content="标题">

       <!-- 是否启用 WebApp 全屏模式，删除苹果默认的工具栏和菜单栏 -->
       <meta name="apple-mobile-web-app-capable" content="yes"/>

       <!-- 添加智能 App 广告条 Smart App Banner（iOS 6+ Safari） -->
       <meta name="apple-itunes-app" content="app-id=myAppStoreID, affiliate-data=myAffiliateData, app-argument=myURL">

       <!-- 设置苹果工具栏颜色 -->
       <meta name="apple-mobile-web-app-status-bar-style" content="black"/>

       <!-- 忽略页面中的数字识别为电话，忽略email识别 -->
       <meta name="format-detection" content="telphone=no, email=no"/>


       <!-- 启用360浏览器的极速模式(webkit) -->
       <meta name="renderer" content="webkit">

       <!-- 避免IE使用兼容模式 -->
       <meta http-equiv="X-UA-Compatible" content="IE=edge">

       <!-- 不让百度转码 -->
       <meta http-equiv="Cache-Control" content="no-siteapp" />

       <!-- 针对手持设备优化，主要是针对一些老的不识别viewport的浏览器，比如黑莓 -->
       <meta name="HandheldFriendly" content="true">

       <!-- 微软的老式浏览器 -->
       <meta name="MobileOptimized" content="320">

       <!-- uc强制竖屏 -->
       <meta name="screen-orientation" content="portrait">

       <!-- QQ强制竖屏 -->
       <meta name="x5-orientation" content="portrait">

       <!-- UC强制全屏 -->
       <meta name="full-screen" content="yes">

       <!-- QQ强制全屏 -->
       <meta name="x5-fullscreen" content="true">

       <!-- UC应用模式 -->
       <meta name="browsermode" content="application">

       <!-- QQ应用模式 -->
       <meta name="x5-page-mode" content="app">

       <!-- windows phone 点击无高光 -->
       <meta name="msapplication-tap-highlight" content="no">


           <!-- iOS 图标 begin -->
               <!-- iPhone 和 iTouch，默认 57x57 像素，必须有 -->
               <link rel="apple-touch-icon-precomposed" href="/apple-touch-icon-57x57-precomposed.png"/>

               <!-- Retina iPhone 和 Retina iTouch，114x114 像素，可以没有，但推荐有 -->
               <link rel="apple-touch-icon-precomposed" sizes="114x114" href="/apple-touch-icon-114x114-precomposed.png"/>

               <!-- Retina iPad，144x144 像素，可以没有，但推荐有 -->
               <link rel="apple-touch-icon-precomposed" sizes="144x144" href="/apple-touch-icon-144x144-precomposed.png"/>
           <!-- iOS 图标 end -->


           <!-- iOS 启动画面 begin -->
               <link rel="apple-touch-startup-image" sizes="768x1004" href="/splash-screen-768x1004.png"/>

               <!-- iPad 竖屏 768 x 1004（标准分辨率） -->
               <link rel="apple-touch-startup-image" sizes="1536x2008" href="/splash-screen-1536x2008.png"/>

               <!-- iPad 竖屏 1536x2008（Retina） -->
               <link rel="apple-touch-startup-image" sizes="1024x748" href="/Default-Portrait-1024x748.png"/>

               <!-- iPad 横屏 1024x748（标准分辨率） -->
               <link rel="apple-touch-startup-image" sizes="2048x1496" href="/splash-screen-2048x1496.png"/>

               <!-- iPad 横屏 2048x1496（Retina） -->  
               <link rel="apple-touch-startup-image" href="/splash-screen-320x480.png"/>

               <!-- iPhone/iPod Touch 竖屏 320x480 (标准分辨率) -->
               <link rel="apple-touch-startup-image" sizes="640x960" href="/splash-screen-640x960.png"/>

               <!-- iPhone/iPod Touch 竖屏 640x960 (Retina) -->
               <link rel="apple-touch-startup-image" sizes="640x1136" href="/splash-screen-640x1136.png"/>
               <!-- iPhone 5/iPod Touch 5 竖屏 640x1136 (Retina) -->
           <!-- iOS 启动画面 end -->

   <!-- iOS 设备 end -->


   <!-- Windows 8 磁贴颜色 -->
   <meta name="msapplication-TileColor" content="#000"/>

   <!-- Windows 8 磁贴图标 -->
   <meta name="msapplication-TileImage" content="icon.png"/>

   <!-- 添加 RSS 订阅 -->
   <link rel="alternate" type="application/rss+xml" title="RSS" href="/rss.xml"/>

   <!-- 添加 favicon icon -->
   <link rel="shortcut icon" type="image/ico" href="/favicon.ico"/>

   <!-- 关闭chrome浏览器下  翻译   插件 -->
   <meta name="google" value="notranslate" />

   <!-- sns 社交标签 begin -->
       <!-- 参考微博API -->
       <meta property="og:type" content="类型" />
       <meta property="og:url" content="URL地址" />
       <meta property="og:title" content="标题" />
       <meta property="og:image" content="图片" />
       <meta property="og:description" content="描述" />
   <!-- sns 社交标签 end -->
```
2. IOS中Safari允许全屏浏览
```html
<meta content="yes" name="apple-mobile-web-app-capable">
```
3. IOS中Safari顶端状态条样式
```html
<meta content="black" name="apple-mobile-web-app-status-bar-style">
```
4. 忽略将数字变为电话号码
```html
<meta content="telephone=no" name="format-detection">
//一般情况下，IOS和Android系统都会默认某长度内的数字为电话号码，即使不加也是会默认显示为电话的，so，取消这个很有必要！
```
5. IOS中Safari设置保存到桌面图标,
这是IOS中Safari特有的meta，是在你保存某个页面到桌面的时候使用这张图作为桌面图标，所以尺寸和iphone上的一致，是57*57px
```html
<link rel="apple-touch-icon" href="custom_icon.png">
```
6. 这段代码指定了HTML页面使用的字符编码为gb2312，即国标汉字码，不同的语言对应不同的charset。
```html
<meta http-equiv="Content-Type" content="text/html; charset=gb2312" />
```
7. 这段代码让网页在指定的5秒内，跳转到所指定的页面，比如百度，或者用于网页的自动刷新。
```html
<meta http-equiv="Refresh" content="5; url=http://www.baidu.com" />
```
8. 这段代码可以用于设定网页的到期时间，一旦过期必须到服务器上重新调用（GMT时间格式）。
```html
<meta http-equiv="Expires" content="Mon,1,May 2015 00:00:00 GMT" />
```

9. 这段代码用于设定禁止浏览器从本地机的缓存中调阅页面内容，设定后一旦离开网页就无法从Cache中再调出。

```html
<meta http-equiv="Pragma" content="no-cache" />
```
10. 这段代码用于网页等级的评定，在IE的internet选项中有一项内容设置可以防止浏览一些受限制的网站，而网站的限制等级就是通过meta属性的设置。
```html
<meta http-equiv="Pics-label" content="" />
```
11. 这段代码可以强制页面在当前窗口中以独立页面显示，防止自己的网页被别人当成一个frame调用。Content选项：`_blank`、`_top`、`_self`、`_parent`
```html
<meta http-equiv="windows-Target" content="_top" />
```

## html标签中meta属性使用介绍
meta是html语言head区的一个辅助性标签。也许你认为这些代码可有可无。  
其实如果你能够用好meta标签，会给你带来意想不到的效果。  
meta标签的作用有：搜索引擎优化（SEO），定义页面使用语言，自动刷新并指向新的页面，实现网页转换时的动态效果，控制页面缓冲，网页定级评价，控制网页显示的窗口等！  
meta标签的组成：meta标签共有两个属性，它们分别是http-equiv属性和name属性，不同的属性又有不同的参数值，这些不同的参数值就实现了不同的网页功能。
### A、name属性
name属性主要用于描述网页，与之对应的属性值为content，content中的内容主要是便于搜索引擎机器人查找信息和分类信息用的
```html
<meta name="参数" content="具体的参数值">
```
name属性主要有以下几种参数：
#### a、Keywords(关键字)　
说明：keywords用来告诉搜索引擎你网页的关键字是什么。
```html
<meta name="keywords" content="meta总结,html meta,meta属性,meta跳转">
```
#### b、description(网站内容描述)
说明：description用来告诉搜索引擎你的网站主要内容。
```html
<meta name="description" content="haorooms博客,html的meta总结，meta是html语言head区的一个辅助性标签。">
```
#### c、robots(机器人向导)
说明：robots用来告诉搜索机器人哪些页面需要索引，哪些页面不需要索引。content的参数有all,none,index,noindex,follow,nofollow。默认是all。  
具体参数如下：  
* 信息参数为all：文件将被检索，且页面上的链接可以被查询；  
* 信息参数为none：文件将不被检索，且页面上的链接不可以被查询；  
* 信息参数为index：文件将被检索；  
信息参数为follow：页面上的链接可以被查询；  
* 信息参数为noindex：文件将不被检索，但页面上的链接可以被查询；  
* 信息参数为nofollow：文件将被检索，但页面上的链接不可以被查询；
```html
<meta name="robots" content="none">
```

#### d、author(作者)
说明：标注网页的作者
```html
<meta name="author" content="root,root@xxxx.com">
```
#### e、generator
说明：代表说明网站的采用的什么软件制作。
```html
<meta name="generator" content="信息参数"/>
```
#### f、copyright
说明：代表说明网站版权信息。
```html
<meta name="copyright" content="信息参数">
```
#### g、revisit-after
说明：代表网站重访,7days代表7天，依此类推。
```html
<meta name="revisit-after" content="7days">
```
### B、http-equiv属性
http-equiv顾名思义，相当于http的文件头作用，它可以向浏览器传回一些有用的信息，以帮助正确和精确地显示网页内容，与之对应的属性值为content，content中的内容其实就是各个参数的变量值。  
meta标签的http-equiv属性语法格式是：
```html
<meta http-equiv="参数"content="参数变量值">；
```
其中http-equiv属性主要有以下几种参数：
#### a、Expires(期限)
说明：可以用于设定网页的到期时间。一旦网页过期，必须到服务器上重新传输。注意：必须使用GMT的时间格式
```html
<meta http-equiv="expires"content="Fri,12Jan200118:18:18GMT">
```
#### b、Pragma(cache模式)
说明：禁止浏览器从本地计算机的缓存中访问页面内容。注意：这样设定，访问者将无法脱机浏览。
```html
<meta http-equiv="Pragma"content="no-cache">
```
#### c、Refresh(刷新)
说明：自动刷新并指向新页面。两秒后跳转到百度
```html
<meta http-equiv="Refresh"content="2;URL=http://www.baidu.com">
```
#### d、Set-Cookie(cookie设定)
说明：如果网页过期，那么存盘的cookie将被删除。注意：必须使用GMT的时间格式。
```html
<meta http-equiv="Set-Cookie"content="cookie value=xxx;expires=Friday,12-Jan-200118:18:18GMT；path=/">
```
#### e、Window-target(显示窗口的设定)
说明：强制页面在当前窗口以独立页面显示。用来防止别人在框架里调用自己的页面。
```html
<meta http-equiv="Window-target"content="_top">
```
#### f、content-Type(显示字符集的设定)
说明：设定页面使用的字符集。  
具体如下：  
* meta标签的charset的信息参数如GB2312时，代表说明网站是采用的编码是简体中文；
* meta标签的charset的信息参数如BIG5时，代表说明网站是采用的编码是繁体中文；
* meta标签的charset的信息参数如iso-2022-jp时，代表说明网站是采用的编码是日文；
* meta标签的charset的信息参数如ks_c_5601时，代表说明网站是采用的编码是韩文；
* meta标签的charset的信息参数如ISO-8859-1时，代表说明网站是采用的编码是英文；
* meta标签的charset的信息参数如UTF-8时，代表世界通用的语言编码；

#### g、content-Language（显示语言的设定）
```html
<meta http-equiv="Content-Language"content="zh-cn"/>
```
#### h、http-equiv=”imagetoolbar”
指定是否显示图片工具栏，当为false代表不显示，当为true代表显示。
```html
<meta http-equiv="imagetoolbar"content="false"/>
```
#### j、Content-Script-Type
W3C网页规范，指明页面中脚本的类型
```html
<Meta http-equiv="Content-Script-Type"Content="text/javascript"> 
```
