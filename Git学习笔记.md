# Git学习笔记 
## 1. Git 是什么 
- Git 是一种分布式版本控制系统，核心作用是帮助个人或团队高效管理文件版本、
协作开发，并保障代码安全。 

## 2. Git 的作用 
1. 版本管理与回溯 Git 会记录每一次修改的快照。
- 你可以随时回退到任意历史版本，对比差异或恢复误删内容。
- 每次提交（commit）都会保存修改内容、作者、时间和说明，方便追踪问题来源。
- 1. git add file.txt 
  2. git commit -m "新增功能模块" 
  3. git log --oneline # 查看历史版本 
  4. git checkout <commit-id> # 回到指定版本 
3. 多人协作与冲突管理
- 在团队开发中，Git 允许多人同时在不同分支工作，避免互相覆盖修改。
- 自动合并不同成员的更改，若有冲突会标记出来，方便人工处理。
- 每个人都能独立开发，最后统一合并到主分支。
- 1. git branch feature/login 
  2. git switch feature/login 
  3. git merge feature/login 
5. 本地与远程仓库配合
Git 支持本地离线开发，并通过远程仓库（如 GitHub、Gitee、GitLab）实现同步与备份。
- push：将本地修改上传到远程仓库
- pull：拉取远程最新版本到本地
- clone：从远程复制完整项目及历史记录 
- 1. git remote add origin https://github.com/user/repo.git 
  2. git push -u origin main 
  3. git pull origin main
  4. git clone https://github.com/user/repo.git 
4. 分支与实验
分支让你可以在不影响主线的情况下尝试新功能或修复 bug。
- 开发完成后可合并到主分支 - 不满意可直接删除分支，主线不受影响
- git checkout -b test-feature 开发测试 
6. 代码安全与自动化
- 远程仓库提供异地备份，防止本地数据丢失
- 可与 CI/CD 工具结合，实现自动测试、构建与部署 

## 3. Git 基本流程 
1. clone（克隆）
- 作用：把远程仓库（比如 GitHub、GitLab 上的项目）完整地复制到你的本地电脑上。
- 常用命令：git clone <仓库地址>
- 场景：加入新项目或者换新电脑时，第一件事就是 clone 代码下来。 
2. add（暂存）
- 作用：把你在本地修改的代码（新建、修改、删除的文件）添加到 Git 的“暂存区”（Staging Area），告诉 Git：“我要把这些改动记录下来”。 
- 常用命令：git add <文件名> 或 git add .（添加所有修改）。
- 场景：改完了一段代码，准备提交前。 
3. commit（提交）
- 作用：把暂存区里的改动，正式保存为本地仓库的一个“历史版本”（快照）。每次提交都需要写一句说明（commit message），比如“修复登录Bug”。
- 常用命令：git commit -m "你的修改说明"
- 场景：完成一个小功能或修好一个 Bug 后，提交到本地历史。 
4. push（推送）
- 作用：把本地仓库里的提交（commit），上传到远程服务器（如 GitHub/Gitee）。这样别人才能看到你的代码。
- 常用命令：git push（通常需要指定远程分支，如 git push origin main）
- 场景：本地开发完毕并 commit 后，同步给团队 
5. pull（拉取）
- 作用：从远程仓库（如 GitHub/Gitee）获取最新的代码，并自动与你的本地代码进行合并。
- 常用命令：git pull（通常直接使用，或指定远程和分支：git pull origin main）。
- 场景：1. 每天开始工作前：先拉取一下，确保自己基于最新的代码进行开发。 
        2. 准备 push 之前：如果在你开发期间，同事提交了新代码，你必须先 pull 把
           同事的代码合并到本地。如果出现冲突（两人改了同一行代码），需要手动解决冲突，重新 add 和 commit 后，再 push，否则远程仓库会拒绝你的推送。

## 4. 文档完整提交流程
1. 先在官网安装Git，安装成功后桌面上就出现了Git Bash然后点开
2. 输入 cd Desktop进入桌面然后回车
3. 输入 mkdir git-homework在桌面新建一个文件夹然后回车
4. 输入 cd git-homework进入新建的文件夹里面然后回车
5. 输入 git init 把该文件夹初始化成Git仓库（建仓库）然后回车
6. 输入 echo "#Hello 李汶蓓">hello.md创建hello.md文档
7. 输入 git status查看仓库当前状态
8. 输入git add hello.md把选中的文件放入暂存区
9. 输入 git status检查是否进入暂存区
10. 输入git commit -m "add hello.md,新增hello文档"将暂存区的内容永远保存到电脑本地的版本库，也就是保存在Git仓库
11. 输入git remote add origin https://github.com/bei-ooo/Tasks.git绑定远程GitHub仓库
12. 输入 git remote -v验证是否绑定成功
13. - 输入 git push origin main推送上传
      - 弹出GitHub页面
      - 确认授权（Authorize）输入密码
      - 出现Authentication Succeeded认证成功
14. 发现没有出现想要的文档
15. 发现是因为GitHub这个仓库创建的时候勾选了「Add a README file」，GitHub远程仓库自带了一份README，远程仓库有提交记录，但是本地仓库（Git仓库）是全新空仓库，两者历史完全不沾边，Git默认不让直接推送，会静默拒绝。
15. 输入 git pull origin main --allow-unrelated-histories允许两个本来毫无关系的仓库历史合并
16. Git调出来了Vim编译器，按esc键以及输入：wq退出编译器回到Git Bash
17. 再次输入 git push origin main
18. 成功将文档远程输送到了GitHub仓库
 
## 5. 我认为使用Git Bash提交有点麻烦，我搜索到一些更方便更有效率的方式
1. VS Code 内置 Git（同一个 GitHub 仓库，无缝切换）
直接在 VS Code 打开本地仓库文件夹，不需要重新 clone。
- 左侧源代码管理面板，自动识别你本地已经关联好 GitHub 的仓库
- 可以直观看到哪个文档改动了、预览差异
- 勾选文档 → 输入提交信息 → 点击推送，一键完成
2. TortoiseGit（Windows，文件夹右键提交文档）
（适合经常修改 Word、PDF、Markdown 这类文档，不想开终端)
- 安装后，直接在仓库文件夹右键
- TortoiseGit → Commit，勾选改动的文档，填写备注
- 点击 Push，推送到你现有的 GitHub 远程仓库 
（读取的就是本地仓库 `.git` 配置，远程地址沿用之前 Git Bash 设置好的，不用重新配置 remote）
3. GitHub Desktop
导入现有的本地仓库，自动识别已经配置好的 GitHub 远程
- 可视化看到文档改动对比
- 勾选文档、填写提交信息、Push 一键完成
（适合文档类项目，上手最简单，高级 Git 操作偏弱）

## 6. Bash 基础命令（文件 / 文件夹操作，和 Git 无关）
1. `cd`    
- 作用： 切换文件夹   
- 示例：`cd ./my-repo` 进入仓库；`cd ..` 返回上一级 
2. `pwd` 
- 作用： 查看当前所在路径  
- 示例：`pwd` 
3. `ls`   
- 作用：列出当前文件夹文件  
- 示例：`ls -a` 查看包含隐藏文件（`.git`） 
4. `touch`  
- 作用：新建空白文件 
- 示例： `touch hello.md` 
5. `mkdir`  
- 作用：新建文件夹
- 示例： `mkdir git-idea` 
6. `cat` 
- 作用：在终端查看文件内容  
- 示例：`cat hello.md` 
7. `rm` 
- 作用：删除文件 
- 示例： `rm hello.md` 
8. `clear` 
- 作用：清空终端屏幕 
- 示例： `clear` 

## 7. Git 核心命令（版本控制，提交到 GitHub）
1. 初始化 / 拉取仓库
- git init     （在当前文件夹初始化本地Git仓库，生成隐藏.git文件夹）
- git clone '仓库地址'       (把GitHub远程仓库下载到本地）
- git config --global user.name '姓名'  (全局配置用户名)
- git config --global user.email '邮箱' [全局配置邮箱（提交记录会带上)]
2. 提交标准流程（就是 hello.md 的标准流程）
- git status              [查看文件状态（红色未暂存、绿色已暂存]
- git add hello.md         (指定单个文件加入暂存区)
- git add .                [当前目录所有改动文件加入暂存区（慎用，容易误提交]
- git commit -m '备注信息'  (把暂存区提交到本地仓库，生成版本快照)
- git push origin main     (推送到远程GitHub main分支)
- git pull origin main    (从远程拉取别人最新改动到本地，防止冲突)
3. 查看历史、撤销操作（选做任务：回滚）
- git log                 [查看所有提交记录，拿到commit id（哈希串]
- git diff                 (查看文件改了哪些内容)
- git reset --hard commit_id  [版本回滚到指定记录（谨慎!)]
- git restore --staged hello.md  (把文件从暂存区拿出来，不提交)
4. 分支命令
- git branch                   (查看所有本地分支，*代表当前分支)
- git branch first_half_tasks  (创建新分支)
- git checkout first_half_tasks  (切换到指定分支)
- git checkout -b test        (创建并且立刻切换到test分支)
- git merge '分支名'             (把别的分支合并到当前分支)
5. 远程仓库相关
- git remote -v               (查看已经绑定的远程仓库地址)
- git remote add origin 地址   (绑定本地仓库到GitHub远程仓库)

## 8. 小总结
- 不带 `git` 的（`cd`、`ls`、`touch`…）：**Bash 系统命令，操作电脑文件**
- 带 `git` 开头的：**Git 程序命令，管理版本、同步 GitHub 远程仓库**
- 必须先用 `cd` 进入仓库目录，git 命令才能识别到 `.git` 仓库

