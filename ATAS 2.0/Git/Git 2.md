## 1. 深度使用 Git Stash (临时存档)

你可能知道 `git stash`，但大多数人只用最基本的。在处理紧急 Bug 或切换分支时，它是你的“快速保存”键。

- **带备注的存档：** `git stash save "完成了一半的登录功能"`
    
    - _为什么要用：_ 存档多了以后，默认的 `WIP on master...` 根本分不清哪个是哪个。
        
- **查看存档内容：** `git stash list`（查看列表）和 `git stash show -p stash@{0}`（查看具体的改动）。
    
- **部分存档：** `git stash -p`
    
    - _场景：_ 你改了 5 个文件，但只想把其中 2 个存起来，剩下的继续留在工作区。
        
- **从 Stash 创建分支：** `git stash branch <name> stash@{0}`
    
    - _场景：_ 你的存档放了太久，现在的代码已经和存档冲突了。这个命令会创建一个新分支，并把存档应用上去，解决冲突更方便。
        

---

## 2. 代码取证：精准定位谁动了代码

在团队开发中（或回看自己半年前的代码），快速找到某一行代码的来龙去脉非常关键。

- **`git blame -L 10,20 <file>`**
    
    - 查看文件的第 10 到 20 行是谁在什么时候写的。
        
- **`git log -S "keyword"` (Pickaxe)**
    
    - _神器：_ 查找**代码内容**。比如你记得曾经有个变量叫 `atas_v1_config` 但被删了，用 `git log -S` 能搜出所有增加或删除过这个字符串的提交历史。
        
- **`git log --oneline --graph --all`**
    
    - 用字符画出分支合并图。在复杂的分支交叉中，这能让你一眼看出谁合入了谁。
        

---

## 3. 分支管理与远程清理

在大公司工作，分支非常多，保持本地环境的整洁是专业素养的体现。

- **清理无效的远程分支：** `git fetch -p` (or `prune`)
    
    - _场景：_ 同事在 GitHub 上删掉了一个分支，但你本地执行 `git branch -a` 还能看到。这个命令会自动清理掉本地那些在远程已经不存在的分支引用。
        
- **修改最后一次提交：** `git commit --amend --no-edit`
    
    - _场景：_ 刚提交完发现少加了一个文件，或者有个错别字。不需要再开一个新的提交，直接“合进”上一次。
        

---

## 4. 高级冲突解决：三路合并视角

冲突不可怕，可怕的是看不懂冲突。

当你遇到冲突时，Git 默认显示的是：

Plaintext

```
<<<<<<< HEAD (你的改动)
=======
>>>>>>> branch-b (别人的改动)
```

你可以通过配置，看到**共同祖先（Common Ancestor）**的内容，这能帮你理解为什么要改这段代码：

- **命令：** `git config --global merge.conflictstyle diff3`
    
- **效果：** 冲突中会多出一个 `||||||| merged common ancestors` 区域，显示改动前原有的样子。
    

---

## 5. 提升效率：Git Alias (别名)

别再一遍遍打冗长的命令了。在你的 `~/.gitconfig` 或通过命令行设置别名：

Bash

```
# 只要打 git st 就能看到状态
git config --global alias.st status

# 只要打 git last 就能看最后一次提交的详细内容
git config --global alias.last "log -1 HEAD --stat"

# 只要打 git br 就能看到简洁的分支列表
git config --global alias.br "branch --format='%(HEAD) %(color:yellow)%(refname:short)%(color:reset) - %(contents:subject) [%(authorname)]'"
```

---

## 6. 补丁与快速共享：Git Patch

有时候你写了一段代码，想发给同事看（或者在两个没关联的文件夹间传代码），但又不想提 PR 或创建分支。

- **导出补丁：** `git diff > my_changes.patch`
    
- **应用补丁：** `git apply my_changes.patch`
    
    - 这会把改动直接应用到对方的代码上，非常适合快速的技术讨论或离线代码传递。
        

---

### 💡 针对 ATAS_FYP 项目的建议

既然你在做 **ATAS Platform**，而且包含多个 Worktree（如 `ATAS_FYP_event`, `ATAS_FYP_submission`），建议你：

1. **统一 Git Config**：确保所有 Worktree 使用一致的 User Name 和 Email（尤其是如果你有公司和私人两个账号）。
    
2. **合理使用 `.gitignore`**：在多 Worktree 环境下，确保 `node_modules` 或 `venv` 等文件夹被正确忽略，否则磁盘空间会迅速爆炸。