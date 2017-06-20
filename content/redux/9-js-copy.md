前面一节，大家遇到的一个难点就是如何对 default state 的**拷贝**进行修改。这一节来专门补充一下这部分的基础知识。

### 先来处理对象

比如说，我们有一个对象

```
let oo = { a: 1, b:2 }
```

如果执行

```
oo.a = 2
```

那么我们修改的是 oo 对象本身


如果

```
let cc = oo
cc.a = 2
```

那么 cc 是 oo 的一个拷贝么？

答案是：不是。oo 一样会被修改。

所以上面的方法做拷贝是不灵的。

灵的方式有几种：

### Object.assign

- [Object.assign](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)

```
> let state = { a: 1, b: 2}
undefined
> let cc = Object.assign({}, state)
undefined
> cc
Object {a: 1, b: 2}
> cc.a = 100
100
> cc
Object {a: 100, b: 2}
> state
Object {a: 1, b: 2}
```

### 使用对象展开运算符

也就是 [...spread](http://cn.redux.js.org/docs/recipes/UsingObjectSpreadOperator.html) 也可以获得对象的拷贝。

对象展开运算符是 ES7 属性，chrome 中不支持，所以我们到 https://babeljs.io/repl/ 这里来测试

```
let state = {a: 1, b:2}
let aa = {...state}
console.log(aa)
aa.a = 100
console.log(aa)
console.log(state)
```

### 数组的拷贝方式

主要是用 .slice() 和 ...spread 来实现。
