### 课下作业

实现下面的 TODO 应用：

![](http://digicity-1253322599.costj.myqcloud.com/todo.png)

提示：

- 使用 redux/combineReducers/mapStateToProps 等技术来实现
- 图标可以到  http://www.flaticon.com/ 下载 svg
- 每次点最下面的对勾，只显示已完成事项
- 点对勾右边的列表按钮，显示所有事项

### 第一步

创建一个文件夹，里面写一个 README.md 文件，然后把它上传到 github.com ，使用 create-react-app


- 代码： **create react app**

把所有不用的代码删除：

- 代码： **Hello World**


### 第二步

把各个大块功能合理分层，划分组件，然后页面上不要写内容，但是画出各自所占空间。

- 代码： **Main Layout**

### 写 todo 样式

- 代码：**todo style**
- 代码：**avoid body scroll**
- 已完成条目： **right tick for completed todo**

### form 样式

- **form styling**
- **more form styling**

### actions 样式

- **Actions styling**

### 展示所有的 todo 条目

- **show todoList**

注意：这一步里 Provider 的作用就是要让它所包裹的所有组件中的 mapStateToProps 中可以拿到 store 中的整个状态树，没有 Provider ，mapStateToProps 中的参数 state 就肯定为空了。

### Actions 部分功能

- **actions**

### 添加 todo

- **ADD_TODO**

### 最终代码

- 源码：https://github.com/happypeter/todo

- demo: https://happypeter.github.io/todo/

### 增强参考

- [更漂亮的一个版本](https://codepen.io/iamjoshellis/pen/zBjEpL) 学有余力的同学可以模仿做一下


### 部署项目


第一步，生成项目

```
create-react-app tt
```

第二步，进入项目，运行

```
npm run build
```

这时候，我们可以看到这样的输出：

```
The project was built assuming it is hosted at the server root.
To override this, specify the homepage in your package.json.
For example, add this to build it for GitHub Pages:

  "homepage" : "http://myname.github.io/myapp",

```

翻译：这个项目，假定会托管到服务器的根文件夹位置（Peter 注：如果我们把项目托管到 happypeter.github.io 就没有问题，但是，现在要托管到 happypeter.github.io/tt 就肯定不行）。要覆盖这个，可以在你的 package.json 文件之中指定你的主页地址。例如，可以添加下面的语句，来把为 github pages 服务进行编译输出：

所以，我们就进入下一步

### 修改 package.json 文件

添加这一行

```
"homepage" : "http://happypeter.github.io/tt",
```

然后运行：

```
npm run build
```

### 翻译一下输出信息

```
The build folder is ready to be deployed.
To publish it at http://happypeter.github.io/tt, run:

  npm install --save-dev gh-pages

Add the following script in your package.json.

    // ...
    "scripts": {
      // ...
      "predeploy": "npm run build",
      "deploy": "gh-pages -d build"
    }

Then run:

  npm run deploy
```

翻译：build/ 这个文件夹现在已经可以部署了。（ Peter 注：build/ 文件夹里面，已经有所有的文件了 css/js/index.html ，如果手动部署：第一步：创建 github.com/happypeter/tt 这个仓库；第二步：本地创建一个 gh-pages 分支，第三步：把 build/ 里面的文件，拷贝到 gh-pages 分支，第四步：运行 git push -u origin gh-pages ，把本地这些文件推送到 gtihub.com 上。于是，就可以到 happypeter.github.io/tt 这个位置看到项目了，但是这个过程非常繁琐。所以英文内容的下面步骤，就是帮我们自动化以上过程。）

如果要把上面的内容部署到 http://happypeter.github.io/tt 服务，运行

```
npm install --save-dev gh-pages
```

package.json 文件中，添加下面的脚本：

```
    // ...
    "scripts": {
      // ...
      "predeploy": "npm run build",
      "deploy": "gh-pages -d build"
    }
```

然后运行：

```
npm run deploy
```

Peter 注：deploy 的意思就是“部署”

翻译内容至此结束。

### 于是我们按照上面的步骤进行

先来装包：

```
npm install --save-dev gh-pages
```

再把

```
"predeploy": "npm run build",
"deploy": "gh-pages -d build"
```

粘贴到 package.json 文件的，scripts 一项之下。

然后，运行一下：

```
npm run deploy
```

注意：`npm run deploy` 会自动首先呼叫 `npm run build` 这个脚本。

此时的报错：

```
Failed to get remote.origin.url (task must either be run in a git repository with a configured origin remote or must be configured with the "repo" option).
```

基本意思是：找不着 remote.origin.url 。解决方法就是，下一步。


### 去 github.com 上创建 tt 这个仓库


然后，回到本地仓库中，运行：

```
git init
git add -A
git commit -a -m"hello"
git remote add origin git@github.com:happypeter/tt.git
git push -u origin master
```

这样，上一步所缺少的 remote.origin.url 就有了。



### 再次运行


```
npm run deploy
```

输出信息中，显示 `Published` 。然后一般还要等几分钟。这样，项目就运行到 http://happypeter.github.io/tt 了。以后项目有了修改，直接 `npm run deploy` 即可。

### 部署相关问题

**问题** 图片找不着

**解决方法** 不要把图片放到 public 文件夹，而要放到 src/img 文件夹下。[参考实际项目](https://github.com/happypeter/todo/tree/master/src/img)
