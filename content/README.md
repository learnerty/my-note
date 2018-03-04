# 个人的学习笔记

## 使用gitbook编写
1. 先安装gitbook
`npm install gitbook-cli -g`
2. 初始化一个gitbook项目
`gitbook init my-note`  
会生成两个文件：README.md --内容会显示到书皮上。  SUMMARY.md --书籍目录
3. 启动服务器
`gitbook serve`
4. 把文件全部移动到content文件夹下，把my-note文件夹初始化为nodejs项目
5. 在package.json中添加,便可以运行npm start来查看
```js
"scripts": {
 "start": "gitbook serve ./content ./gh-pages",
 "build": "gitbook build ./content ./gh-pages",
 "deploy": "node ./scripts/deploy-gh-pages.js",
 "publish": "npm run build && npm run deploy",
 "port": "lsof -i :35729"
},
```
6. 书籍部署到`gh-pages`,使用`gh-pages`包来帮助完成，首先装包
`npm i --save gn-pages`
7. 然后创建my-note/scripts/deploy-gh-pages.js，内容是
```js
'use strict';

var ghpages = require('gh-pages');

main();

function main() {
    ghpages.publish('./gh-pages', console.error.bind(console));
}
```
8. 之后每次运行`npm run publish`就可以了

