# 6. 远程仓库

到目前为止，我们所有的操作都发生在你自己的电脑上（本地仓库）。但 Git 的真正威力在于团队协作。这通常通过**远程仓库**（Remote Repository）来实现。

## 什么是远程仓库？

远程仓库是托管在网络服务器上的项目版本库。最著名的托管服务是 **GitHub**, **GitLab**, 和 **Bitbucket**。

*   它是一个所有团队成员都可以访问的**中央仓库**。
*   开发者可以从这里**克隆 (clone)** 项目的初始版本。
*   可以将自己的本地提交**推送 (push)** 到这里，与他人分享。
*   可以从这里**拉取 (pull)** 他人最新的更改，保持自己的本地仓库同步。

---

## 常用命令

### `git remote`：管理远程仓库连接

*   **查看你配置的远程仓库**:
    ```bash
    git remote
    ```
    通常，如果你是通过 `git clone` 创建的仓库，你会看到一个默认的名字 `origin`。`origin` 是 Git 为你克隆的那个远程 URL 起的别名。

*   **查看远程仓库的 URL**:
    ```bash
    git remote -v
    ```
    这会显示每个远程仓库别名对应的 URL。

*   **添加一个新的远程仓库**:
    ```bash
    git remote add <shortname> <url>
    ```
    例如，添加一个名为 `upstream` 的新远程仓库：
    ```bash
    git remote add upstream https://github.com/otheruser/repository.git
    ```

### `git push`：推送更改到远程仓库

当你想要分享你的本地提交时，你需要使用 `git push` 命令。

```bash
git push <remote-name> <branch-name>
```

*   `<remote-name>` 是远程仓库的别名，通常是 `origin`。
*   `<branch-name>` 是你想要推送到远程仓库的本地分支名。

**最常见的用法**:
```bash
# 将本地的 main 分支推送到 origin 远程仓库
git push origin main

# 将本地的 feature-login 分支推送到 origin 远程仓库
git push origin feature-login
```

第一次推送一个新创建的分支时，你可能需要使用 `-u` 选项来建立本地分支与远程分支的追踪关系：
```bash
git push -u origin feature-login
```
设置之后，未来在这个分支上推送时，你就可以简化为 `git push`。

### `git pull`：从远程仓库拉取更改

当你的队友向远程仓库推送了他的更改后，你需要将这些更改同步到你的本地仓库。这时就需要 `git pull`。

```bash
git pull <remote-name> <branch-name>
```

**最常见的用法**:
```bash
# 从 origin 远程仓库拉取 main 分支的最新更改，并合并到当前本地分支
git pull origin main
```

`git pull` 实际上是两个命令的组合：
1.  `git fetch`: 从远程仓库下载最新的提交历史和文件，但**不**会自动合并到你当前的工作中。
2.  `git merge`: 将 `fetch` 下来的远程分支合并到你的当前本地分支。

在简单的流程中，`git pull` 非常方便。在更复杂的场景下，一些开发者更喜欢使用 `git fetch` + `git merge` 的组合，以便在合并前先查看远程的更改。

---

**典型的协作工作流**:

1.  **开始一天的工作前**，先拉取主分支的最新代码：
    ```bash
    git checkout main
    git pull origin main
    ```
2.  **创建自己的功能分支**进行开发：
    ```bash
    git checkout -b my-new-feature
    ```
3.  **在分支上提交你的更改**：
    ```bash
    # ... work, work, work ...
    git add .
    git commit -m "完成新功能"
    ```
4.  **将你的功能分支推送到远程仓库**，以便他人可以看到或进行代码审查：
    ```bash
    git push origin my-new-feature
    ```
5.  **当功能被批准后**，将其合并到主分支（这通常在 GitHub 等平台上通过 "Pull Request" 或 "Merge Request" 完成），然后其他人就可以通过 `git pull` 获取你的贡献了。
