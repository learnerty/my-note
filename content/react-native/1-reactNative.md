#本文参考自[react-native中文网](https://reactnative.cn/docs/0.51/getting-started.html?_blank)
## ReactNative安装配置
这里不对安装步骤进行介绍，请参考[react-native中文网](https://reactnative.cn/docs/0.51/getting-started.html?_blank)完成准备工作

## 样式
在ReactNative中，仍然使用JavaScript来写样式。所有的核心组件都接受名为style的属性。这些样式名基本上是遵循了web上的CSS的命名，只是按照JS的语法要求使用了驼峰命名法，例如将background-color改为backgroundColor。  
在实际开发中，建议使用StyleSheet.create来集中定义组件的样式。如下实例：
```js
import React, { Component } from 'react';
import { AppRegistry, StyleSheet, Text, View } from 'react-native';

export default class LotsOfStyles extends Component {
  render() {
    return (
      <View>
        <Text style={styles.red}>just red</Text>
        <Text style={styles.bigblue}>just bigblue</Text>
        <Text style={[styles.bigblue, styles.red]}>bigblue, then red</Text>
        <Text style={[styles.red, styles.bigblue]}>red, then bigblue</Text>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  bigblue: {
    color: 'blue',
    fontWeight: 'bold',
    fontSize: 30,
  },
  red: {
    color: 'red',
  },
});

AppRegistry.registerComponent('LotsOfStyles', () => LotsOfStyles);
```
## 高度与宽度
宽高可以使用指定的固定的`width`和`height`，需要注意的是：ReactNative中的尺寸都是无单位的，表示的是与设备像素密度无关的逻辑像素点。或者使用弹性宽高(`Flex`)  
在组件样式中使用flex可以使其在可利用的空间中动态地扩张或收缩。一般而言我们会使用flex:1来指定某个组件扩张以撑满所有剩余的空间。如果有多个并列的子组件使用了flex:1，则这些子组件会平分父容器中剩余的空间。如果这些并列的子组件的flex值不一样，则谁的值更大，谁占据剩余空间的比例就更大（即占据剩余空间的比等于并列组件间flex值的比）。两种方式的书写见下：
```js
import React, { Component } from 'react';
import { AppRegistry, View } from 'react-native';

class FixedDimensionsBasics extends Component {
  render() {
    return (
      <View>
        <View style={{width: 50, height: 50, backgroundColor: 'powderblue'}} />
        <View style={{width: 100, height: 100, backgroundColor: 'skyblue'}} />
        <View style={{width: 150, height: 150, backgroundColor: 'steelblue'}} />
      </View>
    )
  }
}
class FlexDimensionsBasics extends Component {
  render() {
    return (
      // 去掉父View中的`flex: 1`。 则父View不再具有尺寸，因此子组件也无法再撑开。
      <View style={{flex: 1}}>
        <View style={{flex: 1, backgroundColor: 'powderblue'}} />
        <View style={{flex: 2, backgroundColor: 'skyblue'}} />
        <View style={{flex: 3, backgroundColor: 'steelblue'}} />
      </View>
    )
  }
}

AppRegistry.registerComponent('AwesomeProject', () => FlexDimensionsBasics)
```
## Flexbox布局
ReactNative中的`Flexbox`的工作原理和web上的CSS基本一致，当然也存在少许差异。首先是默认值不同：`flexDirection`的默认值是`column`而不是`row`，而flex也只能指定一个数字值。
### Flex Direction
在组件的style中指定`flexDirection`可以决定主轴沿着水平轴(`row`)方向排列，还是沿着竖直轴(`column`)方向排列，默认值是竖直轴(`column`)方向。
### Justify Content
在组件的style中指定`justifyContent`可以决定其子元素沿着主轴的排列方式。子元素是应该靠近主轴的起始端还是末尾段分布呢？亦或应该均匀分布？对应的这些可选项有：`flex-start`(起始位置)、`center`(居中)、`flex-end`(末尾位置)、`space-around`(每个项目两侧的间隔相等)以及`space-between`(两端对齐，项目之间的间隔都相等)。
### Align Items
在组件的style中指定`alignItems`可以决定其子元素沿着次轴（与主轴垂直的轴，比如若主轴方向为row，则次轴方向为column）的排列方式。子元素是应该靠近次轴的起始端还是末尾段分布呢？亦或应该均匀分布？对应的这些可选项有：`flex-start`、`center`、`flex-end`以及`stretch`。  
`注意：要使stretch选项生效的话，子元素在次轴方向上不能有固定的尺寸。以下面的代码为例：只有将子元素样式中的width: 50去掉之后，alignItems: 'stretch'才能生效。`
```js
import React, { Component } from 'react';
import { AppRegistry, View } from 'react-native';

class AlignItemsBasics extends Component {
  render() {
    return (
      <View style={{
        flex: 1,
        flexDirection: 'column',
        justifyContent: 'center',
        alignItems: 'center',
      }}>
        <View style={{width: 50, height: 50, backgroundColor: 'powderblue'}} />
        <View style={{width: 50, height: 50, backgroundColor: 'skyblue'}} />
        <View style={{width: 50, height: 50, backgroundColor: 'steelblue'}} />
      </View>
    );
  }
};

AppRegistry.registerComponent('AwesomeProject', () => AlignItemsBasics);
```
## 文本输入(TextInput)
`TextInput`是一个允许用户输入文本的基础组件。它有一个名为`onChangeText`的属性，此属性接受一个函数，而此函数会在文本变化时被调用。另外还有一个名为`onSubmitEditing`的属性，会在文本被提交后（用户按下软键盘上的提交键）调用。
```js
import React, { Component } from 'react';
import { AppRegistry, Text, TextInput, View } from 'react-native';

export default class PizzaTranslator extends Component {
  constructor(props) {
    super(props);
    this.state = {text: ''};
  }

  render() {
    return (
      <View style={{padding: 10}}>
        <TextInput
          style={{height: 40}}
          placeholder="将文字翻译成🍕"
          onChangeText={(text) => this.setState({text})}
        />
        <Text style={{padding: 10, fontSize: 42}}>
          {this.state.text.split(' ').map((word) => word && '🍕').join(' ')}
        </Text>
      </View>
    );
  }
}
```
## 滚动视图(ScrollView)
`ScrollView`是一个通用的可滚动的容器，你可以在其中放入多个组件和视图，而且这些组件并不需要是同类型的。`ScrollView`不仅可以垂直滚动，还能水平滚动（通过`horizontal`属性来设置）。`ScrollView`适合用来显示数量不多的滚动元素。放置在`ScollView`中的所有组件都会被渲染，哪怕有些组件因为内容太长被挤出了屏幕外。如果需要显示较长的滚动列表，那么应该使用功能差不多但性能更好的`ListView`组件。
```js
import React, { Component } from 'react';
import{ ScrollView, Image, Text, View } from 'react-native'

export default class IScrolledDownAndWhatHappenedNextShockedMe extends Component {
  render() {
      return(
        <ScrollView>
          <Text style={{fontSize:96}}>Scroll me plz</Text>
          <Image source={require('./img/favicon.png')} />
          <Image source={require('./img/favicon.png')} />
          <Image source={require('./img/favicon.png')} />
          <Image source={require('./img/favicon.png')} />
          <Image source={require('./img/favicon.png')} />
        </ScrollView>
    );
  }
}
```
## 长列表
`ReactNative`提供了几个适用于展示长列表数据的组件，一般而言我们会选用`FlatList`或是`SectionList`。  
`FlatList`组件用于显示一个垂直的滚动列表，其中的元素之间结构近似而仅数据不同。适于长列表数据，且元素个数可以增删。和`ScrollView`不同的是，`FlatList`并不立即渲染所有元素，而是优先渲染屏幕上可见的元素。`FlatList`组件必须的两个属性是`data`和`renderItem`。`data`是列表的数据源，而`renderItem`则从数据源中逐个解析数据，然后返回一个设定好格式的组件来渲染。
```js
import React, { Component } from 'react';
import { FlatList, StyleSheet, Text, View } from 'react-native';

export default class FlatListBasics extends Component {
  render() {
    return (
      <View style={styles.container}>
        <FlatList
          data={[
            {key: 'Devin'},
            {key: 'Jackson'},
            {key: 'James'},
            {key: 'Joel'},
            {key: 'John'},
            {key: 'Jillian'},
            {key: 'Jimmy'},
            {key: 'Julie'},
          ]}
          renderItem={({item}) => <Text style={styles.item}>{item.key}</Text>}
        />
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
   flex: 1,
   paddingTop: 22
  },
  item: {
    padding: 10,
    fontSize: 18,
    height: 44,
  },
})
```
而如果需要渲染的是一组需要分组的的数据，那么`SectionList`是个很好的选择
```js
import React, { Component } from 'react';
import { SectionList, StyleSheet, Text, View } from 'react-native';

export default class SectionListBasics extends Component {
  render() {
    return (
      <View style={styles.container}>
        <SectionList
          sections={[
            {title: 'D', data: ['Devin']},
            {title: 'J', data: ['Jackson', 'James', 'Jillian', 'Jimmy', 'Joel', 'John', 'Julie']},
          ]}
          renderItem={({item}) => <Text style={styles.item}>{item}</Text>}
          renderSectionHeader={({section}) => <Text style={styles.sectionHeader}>{section.title}</Text>}
        />
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
   flex: 1,
   paddingTop: 22
  },
  sectionHeader: {
    paddingTop: 2,
    paddingLeft: 10,
    paddingRight: 10,
    paddingBottom: 2,
    fontSize: 14,
    fontWeight: 'bold',
    backgroundColor: 'rgba(247,247,247,1.0)',
  },
  item: {
    padding: 10,
    fontSize: 18,
    height: 44,
  },
})
```

