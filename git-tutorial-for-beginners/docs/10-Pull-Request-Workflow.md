# 10. Pull Request (PR) 工作流简介

到目前为止，我们学习的命令主要关注个人如何使用 Git。然而，在团队项目中，直接向主分支（如 `main`）推送代码通常是不被允许的。取而代之的是一种被称为 **Pull Request** (在 GitLab 中称为 **Merge Request**) 的协作模式。

Pull Request (PR) 是现代软件开发的核心，它是一种机制，让你在将代码合并到主分支前，能够通知团队成员你已经完成了更改，并请求他们进行**代码审查 (Code Review)**。

---

### 为什么使用 Pull Request？

*   **代码质量**: 你的代码在合并前会经过同事的审查，有助于发现潜在的 bug、逻辑问题和不好的编码风格。
*   **知识共享**: 团队成员通过审查代码，可以了解项目的其他部分正在发生什么变化，促进知识在团队内部的流动。
*   **讨论平台**: PR 提供了一个围绕具体代码变更进行讨论的平台。你可以在这里解释你的设计思路，同事也可以提出建议。
*   **自动化集成**: 大多数项目会集成自动化测试（CI/CD）。只有当你的 PR 通过了所有自动化检查（如单元测试、代码风格检查等）后，才允许被合并。

---

### 典型的 Pull Request 工作流

这个流程主要发生在像 GitHub 或 GitLab 这样的代码托管平台上。

#### 第 1 步：创建功能分支

永远不要在 `main` 分支上直接开发。首先，确保你的 `main` 分支是最新版本，然后创建一个描述性强的分支。

```bash
# 1. 切换到主分支并拉取最新代码
git checkout main
git pull origin main

# 2. 创建你的新功能分支
git checkout -b feature/user-profile-page
```

#### 第 2 步：编码和提交

在这个新分支上进行你的开发工作。进行原子性的、有意义的提交。

```bash
# ... 编写代码 ...
git add .
git commit -m "Feat: Create basic structure for profile page"

# ... 继续编写代码 ...
git add .
git commit -m "Feat: Add user avatar and details"
```

#### 第 3 步：推送你的分支

当你的功能开发完成，或者希望获得一些早期反馈时，将你的分支推送到远程仓库 (`origin`)。

```bash
git push origin feature/user-profile-page
```

#### 第 4 步：在 GitHub/GitLab 上创建 Pull Request

1.  推送到远程仓库后，访问 GitHub 或 GitLab 上的项目页面。
2.  通常，平台会自动检测到你刚刚推送的新分支，并显示一个醒目的按钮让你 `Compare & pull request`。
3.  点击这个按钮，你会进入一个表单页面。
    *   **标题 (Title)**: 简明扼要地描述你的 PR 是做什么的。例如：“添加用户个人资料页面”。
    *   **描述 (Description)**: 详细说明你为什么要做这个改动、你做了什么、以及审查者需要注意什么。如果这个 PR 修复了某个 issue，可以在这里链接它。
    *   **审查者 (Reviewers)**: 指定一或多位同事来审查你的代码。
4.  点击 `Create pull request`。

#### 第 5 步：代码审查和讨论

*   你的同事会收到通知，前来审查你的代码。
*   他们可能会在代码的特定行上留下评论，提出问题或建议。
*   你可能会需要根据反馈，在你的本地分支上做一些修改，然后再次推送到远程分支。新的提交会自动出现在同一个 PR 中。

#### 第 6 步：合并 Pull Request

一旦你的 PR 获得了批准（通常需要至少一个或多个同事点击 "Approve"），并且通过了所有自动化检查，项目维护者就可以点击 `Merge pull request` 按钮了。

这会将你的功能分支中的所有提交合并到 `main` 分支中。

#### 第 7 步：清理分支

合并后，你的功能分支的使命就完成了。保持仓库整洁是一个好习惯。

*   **在 GitHub/GitLab 上**: 合并后通常会有一个 `Delete branch` 的按钮。
*   **在本地**:
    ```bash
    # 切换回 main 分支
    git checkout main

    # 删除本地的功能分支
    git branch -d feature/user-profile-page
    ```

这个流程确保了所有进入主分支的代码都经过了审查，从而极大地提高了项目的稳定性和代码质量。
