#### Git常用命令
- 设置用户签名 ———— git config --global user.name litao
- 设置用户签名 ———— git config --global user.email 964374951@qq.com
- 初始化本地库 ———— git init
- 查看本地库状态 ———— git status
- 添加到暂存区 ———— git add .
- 提交到本地库 ———— git commit -m "feat:日志信息"
- 查看历史记录 ———— git reflog/git log
- 版本穿梭 ———— git reset --hard 版本号
#### 分支操作
- 创建分支 ———— git branch 分支名
- 查看分支 ———— git branch -v（r 远程、a 所有、v 本地）
- 切换分支 ———— git checkout 分支名
- 把指定的分支合并到当前分支上 ———— git merge 需要合并的分支名
- 创建并切换到新分支 ———— git checkout -b new-feature
- 切换到远程分支 ———— git checkout -t origin/feature-branch
- 恢复文件 ———— git checkout HEAD -- file.txt
- 删除分支 ———— git branch -d 分支名
- 重命名分支 ———— git branch -m <old-branch> <new-branch>
#### 从远程库拉取文件
- 初始化 ————  git init
- 链接仓库 ———— git remote add origin https://github.com/under328/hollow-knight-pixel.git
- 拉取项目 ———— git pull origin master
#### 将文件上传到远程库
- 添加到暂存区 ———— git add .
- 提交到本地库 ———— git commit -m "feat：提交代码"
- 创建分支（第一次） ———— git branch -M main
- 链接仓库（第一次） ———— git remote add origin https://github.com/under328/hollow-knight-pixel.git
- 关联并提交代码到分支（第一次） ———— git push -u origin main
- 提交代码 ———— git push
#### 克隆项目
- git clone https://github.com/under328/hollow-knight-pixel.git
#### 日志类型
- feat ： 新功能
- fix ： 修补bug
- docs：文档
- style：格式
- refactor：重构
- test ： 增加测试
- chore：构建过程或辅助工具的变动
