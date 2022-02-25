# demo

### 1.添加该项目下的所有文件

　　$git add .   （注意这里有个点）

### 2.使用如下命令将文件添加到仓库中去

　　$ git commit -m '本次提交的说明'（说明信息为必填项，最好是信息有意义，便于后期理解）

### 3.将本地代码库与远程代码库相关联

　　$ git remote add origin https://gitee.com/qlqaq/projects/仓库名称

### 4.强制把远程仓库的代码跟新到当前分支上面。ps:如果仓库为空这一步可以跳过

    $ git pull --rebase origin master

### 5.将本地代码推送到指定远程的仓库中

　　$ git push -u origin master
