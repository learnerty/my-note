接下来，看一看进阶的一些知识

## 使用导航器跳转页面
ReactNative中现有的几个导航组件，如果刚刚开始接触ReactNative，那么直接选择`React Navigation`就好。如果你只针对iOS平台开发，并且想和系统原生外观一致，那么可以选择`NavigatorIOS`。除了这两个外，还有`Navigator`，但现在这个老组件正在逐渐被`React Navigation`替代，不推荐使用，只需了解即可，还有一个已经完全被弃用的`NavigationExperimental`组件。

### React Navigation
这是主推的一个导航库，首先需要在项目中安装此库。  
`yarn add react-navigation`或`npm install react-navigation --save`  
该库包含三类组件：  
（1）StackNavigator：类似顶部导航条，用来跳转页面和传递参数  
（2）TabNavigator：类似底部导航栏，用来在同一屏幕下切换不同界面  
（3）DrawerNavigator：侧滑菜单导航栏，用于轻松设置带抽屉导航的屏幕

##### screenProps
`reactNavigation`自带的一个属性，属于`navigationOptions`的一个属性，可以全局控制`navigationOptions`中的某些值，比如说你想做换肤功能，修改这个属性绝对是最简单的方式。
```js
// 假设App就是项目中的入口文件，如果还不知道，可以看下Demo，在这里我将主题色通过screenProps属性修改成'red'
<App screenProps={{themeColor:'red'}}>

static navigationOptions = ({navigation,screenProps}) => ({
      // 这里面的属性和App.js的navigationOptions是一样的。
      headerStyle:{backgroundColor:screenProps?
      screenProps.themeColor:
      '#4ECBFC'},
    )
})
```

#### StackNavigator 基础用法/属性介绍
```js
const MyApp = StackNavigator({
    // 对应界面名称
    MyTab: {
        screen: MyTab,
    },
    Detail: {
        screen: Detail,
        navigationOptions:{
            headerTitle:'详情',
            headerBackTitle:null,
        }
    },
}, {
    headerMode: 'screen',
});
```

##### 导航配置
1. screen：对应界面名称，需要填入import之后的页面。
2. navigationOptions：配置StackNavigator的一些属性。
 * title：标题，如果设置了这个导航栏和标签栏的title就会变成一样的，所以不推荐使用这个方法。
 * header：可以设置一些导航的属性，当然如果想隐藏顶部导航条只要将这个属性设置为null就可以了。
 * headerTitle：设置导航栏标题，推荐用这个方法。
 * headerBackTitle：设置跳转页面左侧返回箭头后面的文字，默认是上一个页面的标题。可以自定义，也可以设置为null
 * headerTruncatedBackTitle：设置当上个页面标题不符合返回箭头后的文字时，默认改成"返回"。（上个页面的标题过长，导致显示不下，所以改成了短一些的。）
 * headerRight：设置导航条右侧。可以是按钮或者其他。
 * headerLeft：设置导航条左侧。可以是按钮或者其他。
 * headerStyle：设置导航条的样式。背景色，宽高等。如果想去掉安卓导航条底部阴影可以添加elevation: 0，iOS下用shadowOpacity: 0。
 * headerTitleStyle：设置导航条文字样式。安卓上如果要设置文字居中，只要添加alignSelf:'center'就可以了。在安卓上会遇到，如果左边有返回箭头导致文字还是没有居中的问题，最简单的解决思路就是在右边也放置一个空的按钮。
 * headerBackTitleStyle：设置导航条返回文字样式。
 * headerTintColor：设置导航栏文字颜色。总感觉和上面重叠了。
 * headerPressColorAndroid：安卓独有的设置颜色纹理，需要安卓版本大于5.0
 * gesturesEnabled：是否支持滑动返回手势，iOS默认支持，安卓默认关闭
 * gestureResponseDistance：对象覆盖触摸从屏幕边缘开始的距离，以识别手势。 它需要以下属性：  
 horizontal - number - 水平方向的距离 默认为25。  
 vertical - number - 垂直方向的距离 默认为135。
```js
// 设置滑动返回的距离
gestureResponseDistance:{horizontal:300},
```

##### 导航视觉效果
1. mode：定义跳转风格。
 * card：使用iOS和安卓默认的风格。
 * modal：iOS独有的使屏幕从底部画出。类似iOS的present效果。
2. headerMode：边缘滑动返回上级页面时动画效果。
 * float：iOS默认的效果，可以看到一个明显的过渡动画。
 * screen：滑动过程中，整个页面都会返回。
 * none：没有动画。
3. cardStyle：自定义设置跳转效果。
4. transitionConfig： 自定义设置滑动返回的配置。
5. onTransitionStart：当转换动画即将开始时被调用的功能。
6. onTransitionEnd：当转换动画完成，将被调用的功能。
7. path：路由中设置的路径的覆盖映射配置。
8. initialRouteName：设置默认的页面组件，必须是上面已注册的页面组件。
9. initialRouteParams：初始路由的参数。

>  path:path属性适用于其他app或浏览器使用url打开本app并进入指定页面。path属性用于声明一个界面路径，例如：【/pages/Home】。此时我们可以在手机浏览器中输入：app名称://pages/Home来启动该App，并进入Home界面。

#### TabNavigator 基础用法/属性介绍
```js
const MyTab = TabNavigator({
    ShiTu: {
        screen: ShiTu,
        navigationOptions:{
            tabBarLabel: '识兔',
            tabBarIcon: ({tintColor}) => (
                <Image
                    source={{uri : '识兔'}}
                    style={[tabBarIcon, {tintColor: tintColor}]}
                />
            ),
        },
    }, {
    tabBarPosition: 'bottom',
    swipeEnabled:false,
    animationEnabled:false,
    tabBarOptions: {
        style: {
            height:49
        },
        activeBackgroundColor:'white',
        activeTintColor:'#4ECBFC',
        inactiveBackgroundColor:'white',
        inactiveTintColor:'#aaa',
        showLabel:false,
    }
  }
});
```

##### 屏幕导航配置
1. screen：和导航的功能是一样的，对应界面名称，可以在其他页面通过这个screen传值和跳转。
2. navigationOptions：配置TabNavigator的一些属性
 * title：标题，会同时设置导航条和标签栏的title，还是不推荐这种方式。
 * tabBarVisible：是否隐藏标签栏。默认不隐藏(true)
 * tabBarIcon：设置标签栏的图标。需要给每个都设置。
 * tabBarLabel：设置标签栏的title。推荐这个方式。
 * tabBarOnPress：设置tabBar的点击事件，内部提供了两个属性，一个方法(obj)。
```js
tabBarOnPress:(obj)=>{
    console.log(obj);
    obj.jumpToIndex(obj.scene.index)
},
```

##### 标签栏配置
1. tabBarPosition：设置tabbar的位置，iOS默认在底部，安卓默认在顶部。（属性值：'top'，'bottom'）
2. swipeEnabled：是否允许在标签之间进行滑动。
3. animationEnabled：是否在更改标签时显示动画。
4. lazy：是否根据需要懒惰呈现标签，而不是提前制作，意思是在app打开的时候将底部标签栏全部加载，默认false,推荐改成true哦。
5. initialRouteName： 设置默认的页面组件
6. backBehavior：按 back 键是否跳转到第一个Tab(首页)， none 为不跳转
7. tabBarOptions：配置标签栏的一些属性

### 图片
#### 静态图片资源
`React Native`提供了一个统一的方式来管理`iOS`和`Android`应用中的图片。要往App中添加一个静态图片，只需把图片文件放在代码文件夹中某处，可以这样引用它：`<Image source={require('./img/check.png')} />`，图片文件的查找会和JS模块的查找方式一样。哪个组件引用了这个图片，Packager就会去这个组件所在的文件夹下查找check.png。并且，如果有check.ios.png和check.android.png，Packager就会根据平台而选择不同的文件。还可以使用@2x，@3x这样的文件名后缀，来为不同的屏幕精度提供图片。比如下面这样的代码结构：
```
.
├── button.js
└── img
    ├── check@2x.png
    └── check@3x.png
```
Packager会打包所有的图片并且依据屏幕精度提供对应的资源。譬如说，iPhone 5s会使用check@2x.png，而Nexus 5上则会使用check@3x.png。如果没有图片恰好满足屏幕分辨率，则会自动选中最接近的一个图片。  

这样会带来如下的一些好处:
1. iOS和Android一致的文件系统。
2. 图片和JS代码处在相同的文件夹，这样组件就可以包含自己所用的图片而不用单独去设置。
3. 不需要全局命名。你不用再担心图片名字的冲突问题了。
4. 只有实际被用到（即被require）的图片才会被打包到你的app。
5. 现在在开发期间，增加和修改图片不需要重新编译了，只要和修改js代码一样刷新你的模拟器就可以了。
6. 与访问网络图片相比，Packager可以得知图片大小了，不需要在代码里再声明一遍尺寸。
7. 现在通过npm来分发组件或库可以包含图片了。
>注意：为了使新的图片资源机制正常工作，require中的图片名字必须是一个静态字符串（不能使用变量！因为require是在编译时期执行，而非运行时期执行！）。

```js
// 正确
<Image source={require('./my-icon.png')} />
// 错误
var icon = this.props.active ? 'my-icon-active' : 'my-icon-inactive';
<Image source={require('./' + icon + '.png')} />
// 正确
var icon = this.props.active ? require('./my-icon-active.png') : require('./my-icon-inactive.png');
<Image source={icon} />
```
> 注意：通过这种方式引用的图片资源包含图片的尺寸（宽度，高度）信息，如果需要动态缩放图片（例如，通过flex），可能必须手动在style属性设置{ width: undefined, height: undefined }。

#### 网络图片
很多要在App中显示的图片并不能在编译的时候获得，又或者有时候需要动态载入来减少打包后的二进制文件的大小。这些时候，与静态资源不同的是，需要手动指定图片的尺寸。同时强烈建议使用https以满足iOS App Transport Security 的要求。
```js
<Image source={{uri: 'https://facebook.github.io/react/img/logo_og.png'}}
       style={{width: 400, height: 400}} />
```

#### 网络图片的请求参数
还可以在Image组件的source属性中指定一些请求参数
```js
<Image source={{
  uri: 'https://facebook.github.io/react/img/logo_og.png',
  method: 'POST',
  headers: {
    Pragma: 'no-cache'
  },
  body: 'Your Body goes here'
}}
style={{width: 400, height: 400}} />
```

#### 背景图片组件
我们常面对的一种需求就是类似web中的背景图（background-image）。要实现这一用例，只需简单使用<ImageBackground>组件，然后把需要背景图的子组件嵌入其中即可。
```js
<ImageBackground source={...}>
    <Text>背景图的子组件</Text>
</ImageBackground>
```

