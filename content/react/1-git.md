`sudo apt-get install git curl atom`   下载git, curl, atom软件
`sudo apt-get update`   更新

### git命令
`git clone [url]`   克隆到本地  
`git status`    查看仓库状态  
`git log`     查看仓库日志  
`git pull`   拉取远端更新

修改后上传更新  
`git add .`  添加到git 暂时保存下来  
`git commit -m 'message'`  做版本  
`git push`   提交

atom 装包命令  
`apm install [packagename]`
```
装的一些包
emmet  
open-in-browser  
autocomplete-paths  
language-babel
```

#### 手动创建.gitignore里面写名称,忽略不想上传的文件或文件夹


#### 本地上传
`ssh-keygen`命令，生成电脑钥匙 `.put`公有,将里面内容复制到github的SSH and GPG keys  
`git init` 初始化成一个仓库  
`git remote add origin` 地址  
`git push -u origin master`  提交的master分支
