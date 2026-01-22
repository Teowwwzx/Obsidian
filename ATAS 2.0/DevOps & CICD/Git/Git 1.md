## 1. 整理提交历史：Interactive Rebase (`rebase -i`)

在把代码合入 `master` 之前，如果提交历史太乱（比如一堆 "fix typo", "temp save"），你可以用交互式变基来重写历史。

- **命令：** `git rebase -i HEAD~5` （修改最近 5 次提交）
    
- **常用操作：**
    
    - `pick`: 保留该提交。
        
    - `reword`: 保留提交，但修改提交信息。
        
    - `squash`: 将该提交合并到前一个提交中（最常用，用于清理琐碎提交）。
        
    - `drop`: 删除该提交。
        

> **注意：** 永远不要对**已经 Push 到公共分支**的代码执行 Rebase。

---

## 2. 找回丢失的代码：Git Reflog

如果你不小心 `git reset --hard` 删掉了一个还没推送到远端的提交，或者在 Rebase 时搞砸了，`reflog` 是你的救命稻草。

- **原理：** Git 会记录你所有的操作（切换分支、提交、重置）。
    
- **命令：** `git reflog`
    
- **找回方法：** 找到那个提交的哈希值（hash），执行 `git reset --hard <hash>` 即可回到那个时刻。
    

---

## 3. 精准迁移代码：Cherry-pick

如果你在 `feature-A` 分支写了一个通用的工具类，想把它单独拿回 `master`，但又不想合并整个 `feature-A`。

- **命令：** `git cherry-pick <commit-hash>`
    
- **作用：** 把指定的某一个提交“复制”并应用到当前分支。
    

---

## 4. 深度使用 Git Worktree (你正在用的)

你在之前的提问中已经接触到了，它的核心价值在于：

- **并行任务：** 在 `ATAS_FYP` 开发功能时，无需 `stash` 即可在 `ATAS_FYP_event` 修复紧急 Bug。
    
- **多环境对比：** 同时打开两个文件夹，一个运行旧版本对比 UI，一个开发新版本。
    
- **清理命令：** `git worktree prune` （清理已经手动删除文件夹但 Git 还在追踪的 worktree）。
    

---

## 5. 快速排查 Bug：Git Bisect

如果你发现程序出 Bug 了，但不知道是哪次提交引入的，`bisect` 可以利用**二分查找法**帮你快速定位。

1. 开始：`git bisect start`
    
2. 标记坏提交：`git bisect bad` (当前的坏了)
    
3. 标记好提交：`git bisect good <hash>` (比如一周前那个版本是好的)
    
4. Git 会自动切换到中间的提交，你测试后告诉 Git `good` 还是 `bad`。
    
5. 反复几次，Git 会直接指出“罪魁祸首”是哪次提交。
    

---

## 6. 自动化你的流程：Git Hooks

作为有 DevOps 背景的开发者，你可以利用 Hooks 在本地执行自动化脚本。

- **位置：** `.git/hooks/`
    
- **常用场景：**
    
    - `pre-commit`: 提交前自动跑 Lint 或单元测试。如果失败，直接禁止提交。
        
    - `commit-msg`: 强制执行提交信息格式检查（如必须符合 [Conventional Commits](https://www.conventionalcommits.org/) 规范）。
        

---

## 7. 模块化管理：Git Submodules

如果你在 ATAS 项目中需要引用另一个独立的 Repo（比如一个通用的 UI 组件库），可以使用子模块。

- **添加：** `git submodule add <url> <path>`
    
- **更新：** `git submodule update --init --recursive`