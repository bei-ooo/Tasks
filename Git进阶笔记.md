# Git进阶笔记
## 1. 提交错了怎么办
### 1. 仅 `git add`，还没有 `commit`(文件进入暂存区，但还没有生成本地提交快照)
- (撤销单个文件暂存)git restore --staged hello.md
- (撤销全部文件暂存)git restore --staged .
(文件保留在本地，只是移出暂存区，不会被提交）

### 2. 已经 `git commit`，尚未 `push` 到远程 GitHub(提交记录只存在本地，GitHub 看不到）
1. 场景1：修改上一次提交备注 / 补充文件
- git commit --amend
2. 场景2：撤销本次提交，改动保留在本地
- git log
- git reset commit_id
3. 场景3：撤销本次提交，直接丢弃改动
- git reset --hard commit_id

### 3. 已经 `git push`，推送到远程仓库

1. **首选方案：git revert（多人协作安全）**
- 原理：新增一条反向提交抵消修改，**保留全部历史记录，不会影响其他人**
- git log
- git revert 错误的commit\_id
- git push origin main
2. **慎用方案：reset + 强制推送（仅单人仓库）**
- git reset --hard 目标commit_id
- git push origin main --force
(风险：强制覆盖远程历史，团队项目禁止使用，会覆盖别人提交)

## 2. 版本回滚
### 1. 本地未推送（安全）
- (查看提交记录，复制commit id)git log
- (回退到指定版本，--hard 丢弃后续所有改动)git reset --hard commit_id

### 2. 已经推送到远程（多人协作优先 revert）
- git revert 需要撤销的commit_id
- git push origin main
- `revert`：新增反向提交，历史记录完整，适合团队
- `reset --hard + --force`：删除历史，仅个人仓库使用

## 3、冲突解决
- 执行 merge 后出现提示：`Automatic merge failed; fix conflicts and then commit the merge.` 代表冲突
1. 打开冲突文件，Git 自动标记冲突区域
- <<<<<<< HEAD
- 当前分支（main）的内容
- =======
- 被合并分支（first_half_tasks）的内容
- >>>>>>> first_half_tasks
2. 手动编辑文件：删除 `<<<<<<<` `=======` `>>>>>>>` 标记，保留最终想要的内容，保存文件
3. 在 Git Bash 继续操作
- (将修改好的文件加入暂存)git add 冲突文件名
- (完成合并提交)git commit -m "merge: 合并分支，解决冲突"
- (推送到远程)git push origin main
4. 要点：冲突必须人工判断取舍，Git 不会自动选择内容。

## 4.拓展
### 1.代码合并（git merge）
- 作用：把一个分支的改动合并到当前所在分支
- 1. 先切换到【接收代码的目标分支】，例如 main
git checkout main
2. 将 first_half_tasks 分支合并到 main
git merge first_half_tasks
- 两种结果：
1. **快进合并（无冲突）**：自动完成合并，无需额外操作
2. **合并冲突**：两个分支修改了同一个文件同一位置，Git 无法自动判断，需要手动处理

### 2.分支管理
- 分支相当于项目的平行副本，适合并行开发、单独写任务（比如本次的 `first_half_tasks`）
- 1. (查看本地分支，* 代表当前所在分支）git branchy
2. (只创建新分支，不切换)git branch first_half_tasks
3. (创建分支并立刻切换到该分支)git checkout -b first_half_tasks
4. (切换到已有分支)git checkout first_half_tasks
5. (删除本地已经合并完成的分支)git branch -d first_half_tasks
6. (查看远程所有分支)git branch -r



