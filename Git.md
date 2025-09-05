#### Git常用命令
- 设置用户签名 ———— git config --global user.name 用户名
- 设置用户签名 ———— git config --global user.email 邮箱
- 初始化本地库 ———— git init
- 查看本地库状态 ———— git status
- 添加到暂存区 ———— git add 文件名
- 提交到本地库 ———— git commit-m "日志信息" 文件名
- 查看历史记录 ———— git reflog/git log
- 版本穿梭 ———— git reset --hard 版本号
#### 分支操作
- 创建分支 ———— git branch 分支名
- 查看分支 ———— git branch -v
- 切换分支 ———— git checkout 分支名
- 把指定的分支合并到当前分支上 ———— git merge 需要合并的分支名
#### 从远程库拉取文件
- 初始化 ————  git init
- 链接仓库 ———— git remote add origin https://gitee.com/shallow-winds/test.git
- 拉取项目 ———— git pull origin master
#### 将文件上传到远程库
- 添加到暂存区 ———— git add 文件名
- 提交到本地库 ———— git commit-m "feat：提交代码"
- 提交到码云 ———— git push origin (master/创建分支的名字)
