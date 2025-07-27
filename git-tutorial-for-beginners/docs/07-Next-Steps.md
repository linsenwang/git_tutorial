# 7. 后续步骤与有用的技巧

恭喜你！你已经掌握了 Git 最核心、最常用的命令和概念。这些知识足以应对日常开发中 90% 的场景。

但这只是 Git 世界的开始。下面是一些能让你效率倍增的有用技巧和值得探索的进阶主题。

---

## `.gitignore` 文件

你的项目里通常会有一些不需要被 Git 追踪的文件，例如：
*   编译产生的文件（如 `.class`, `.o`）
*   依赖包目录（如 `node_modules/`）
*   IDE 或操作系统的配置文件（如 `.idea/`, `.DS_Store`）
*   包含敏感信息的日志或配置文件（如 `debug.log`, `config.local.js`）

你可以在项目根目录下创建一个名为 `.gitignore` 的文件，将这些不需要追踪的文件或目录名写进去，Git 就会自动忽略它们。

**一个简单的 `.gitignore` 示例**:
```
# 忽略所有 .log 文件
*.log

# 忽略 node_modules 目录
node_modules/

# 忽略一个特定的配置文件
dist/
.env
```
强烈建议在项目一开始就建立好 `.gitignore` 文件。你可以在 [gitignore.io](https://www.toptal.com/developers/gitignore) 这个网站上为你的项目类型生成一份推荐的 `.gitignore` 文件。

---

## `git stash`：临时保存工作

假设你正在一个功能分支上开发，突然需要紧急切换到 `main` 分支去修复一个 bug。但你当前的工作还没完成，不想为此创建一个新的提交。

这时 `git stash` 就派上用场了。

*   **`git stash`**: 将你当前工作区和暂存区的改动“储藏”起来，让你的工作目录变得干净（回到 `HEAD` 的状态）。
*   **`git stash pop`**: 恢复最近一次储藏的改动，并将其从储藏列表中删除。
*   **`git stash list`**: 查看所有储藏的列表。

**使用流程**:
```bash
# 1. 在 feature 分支上，储藏未完成的工作
git stash

# 2. 切换到 main 分支去修复 bug
git checkout main
# ... fix bug, commit, etc ...

# 3. 切回 feature 分支
git checkout feature

# 4. 恢复之前的工作，继续开发
git stash pop
```

---

## `git rebase`：变基

`git rebase` 是 `git merge` 之外的另一种合并分支的方法。它能让你的提交历史变得更整洁、更线性。

简单来说，`merge` 会在历史记录中创建一个新的“合并提交”节点，将两个分支连接起来。而 `rebase` 会把你当前分支的提交“移动”到目标分支的最新提交之后，看起来就像你是在目标分支最新版本的基础上进行开发的一样。

**警告**：**不要对已经推送到公共仓库的分支进行 rebase**，因为它会重写提交历史，可能会给协作者带来麻烦。它最适合用于整理你本地尚未分享的提交。

这是一个更高级的主题，当你对 Git 更加熟悉后，非常值得学习。

---

## 后续学习资源

*   **图形化工具 (GUI)**: 学习如何在 VS Code 中高效使用 Git，可以极大提升你的日常开发效率。
*   **Pro Git Book**: 官方的 Git 书籍，非常全面和深入。有免费的在线版本。
*   **Learn Git Branching**: 一个交互式的、游戏化的 Git 学习网站。
*   **GitHub Skills**: GitHub 官方提供的交互式学习课程。
*   **命令行工具**: 学习使用 `git log` 的各种选项，如 `--oneline`, `--graph`, `--decorate`，能让你更清晰地看懂历史。

不断练习，在真实项目中使用 Git，是成为 Git 高手的最佳途径。祝你使用愉快！

---
### 现代工具与团队协作
想让你的工作流再上一个台阶吗？学习如何使用 AI 工具，并掌握现代团队的协作模式：
*   **[8. 使用 OpenCommit 自动生成提交信息](./08-Automating-Commits-with-OpenCommit.md)**
*   **[9. 如何撤销操作](./09-Undoing-Things.md)**
*   **[10. Pull Request (PR) 工作流简介](./10-Pull-Request-Workflow.md)**
