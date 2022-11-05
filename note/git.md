git remote -v： 查看当前远程仓库

git remote add origin <url>: 绑定远程仓库名和url



git config user.name "pjr"  当前库的名,全局加--global

git config user.email "dfkd@123.com"  当前库的email



git reset --hard: 丢弃当前本地的修改



从远程上下载和更新本地的代码

$ git fetch --all
$ git fetch --tags
$ git reset --hard origin/master  