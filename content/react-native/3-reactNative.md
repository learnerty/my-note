## 触摸事件

### 点击、长按事件
在用户点击操作时，可以使用`Touchable`开头的一系列组件。这些组件通过`onPress`属性接受一个点击事件的处理函数。在按下手指并且抬起手指没有移除组件外，此函数会被调用。这些组件下只能有一个根节点，如果有多个节点，需要包裹在一个根节点下。  
* TouchableWithoutFeedback：点击没有任何视觉反馈。
* TouchableHighlight：点击背景会变暗。
* TouchableOpacity：点击降低按钮的透明度，不会改变背景的颜色。
* TouchableNativeFeedback：只能在android中使用，会在点击时形成类似墨水涟漪的视觉效果。
```js
class MyButton extends Component {
  render() {
    return (
      <TouchableHighlight
        onPressIn={() => console.log("点击开始触发")}
        onPressOut={() => console.log("点击结束或离开触发")}
        onPress={() => console.log("单击触发")}
        onLongPress={() => console.log("长按触发")}
      >
        <Text>button</Text>
      </TouchableHighlight>
    );
  }
}
```

## 定时器
* `setTimeout(fn, n)`, `clearTimeout`：n毫秒后执行fn函数，只执行一次
* `setInterval(fn, n)`, `clearInterval`：每隔n毫秒执行一次
* `setImmediate`, `clearImmediate`：只执行一次，立即执行
* `requestAnimationFrame`, `cancelAnimationFrame`：每帧刷新之后执行一次，用来执行在一段时间内控制视图动画的代码  

原生应用感觉如此流畅的一个重要原因就是在互动和动画的过程中避免繁重的操作。在React Native里，我们目前受到限制，因为我们只有一个JavaScript执行线程。不过可以用InteractionManager来确保在执行繁重工作之前所有的交互和动画都已经处理完毕。应用可以通过以下代码来安排一个任务，使其在交互结束之后执行。

`InteractionManager`的一些属性方法,常用runAfterInteractions方法:
* runAfterInteractions(task)  静态方法,在用户交互和动画结束以后执行任务
* createInteractionHandle() 静态方法，创建一个句柄(处理器)，通知管理器，某个动画或者交互开始了
* clearInteractionHandle(handler:Handle)  静态方法，进行清除句柄，通知管理器，某个动画或者交互结束了。
* setDeadline(deadline:number) 静态方法, 设置延迟时间，该会调用setTimeout方法挂起并且阻塞所有没有完成的任务，然后在eventLoopRunningTime到设定的延迟时间后，然后执行setImmediate方法进行批量执行任务

```js
InteractionManager.runAfterInteractions(() => {
   // ...需要长时间同步执行的任务...
})


var handle = InteractionManager.createInteractionHandle();
// 执行动画... (`runAfterInteractions`中的任务现在开始排队等候)
// 在动画完成之后
InteractionManager.clearInteractionHandle(handle);
// 在所有句柄都清除之后，现在开始依序执行队列中的任务
```
当组件被卸载，一定要清除定时器!
```js
import React,{
  Component
} from 'react';

export default class Hello extends Component {
  componentDidMount() {
    this.timer = setInterval(
      () => { console.log('把一个定时器的引用挂在this上'); },
      500
    );
  }
  componentWillUnmount() {
    // 如果存在this.timer，则使用clearTimeout清空。
    // 如果你使用多个timer，那么用多个变量，或者用个数组来保存引用，然后逐个clear
    this.timer && clearTimeout(this.timer);
  }
};
```
