# 10. 在 VS Code 中使用 Git

虽然我们学习了所有核心的 Git 命令行操作，但在日常开发中，使用集成在代码编辑器中的图形化界面（GUI）通常更高效、更直观。Visual Studio Code 提供了世界一流的 Git 集成，让你可以轻松地在不离开编辑器的情况下完成大部分 Git 操作。

---

### 1. 源代码管理视图 (Source Control View)

VS Code 的核心 Git 功能都集中在“源代码管理”视图中。

*   **如何打开**:
    *   点击左侧活动栏中的第三个图标（看起来像一个分叉的树枝）。
    *   使用快捷键 `⌃⇧G` (Ctrl+Shift+G)。

当你对项目做出更改后，这个图标上会出现一个数字徽章，显示你当前有多少未提交的更改。

![VS Code Source Control View](https://code.visualstudio.com/assets/docs/sourcecontrol/overview/overview.png)

这个视图主要分为几个部分：
*   **Commit Message Input**: 顶部的输入框，用于填写提交信息。
*   **Changes**: 列出了所有被修改过但尚未暂存的文件。
*   **Staged Changes**: 列出了已经使用 `git add` 暂存、准备提交的文件。

---

### 2. 核心工作流

让我们看看如何在 VS Code 中完成“修改 -> 暂存 -> 提交”这个核心循环。

#### 查看更改 (Diff)
在“Changes”列表中单击任何一个文件，VS Code 会打开一个**差异 (Diff) 视图**。这个视图会并排显示文件的旧版本和新版本，清晰地标出你删除（红色）和添加（绿色）的行。

#### 暂存更改 (Stage)
*   **暂存单个文件**: 将鼠标悬停在“Changes”列表中的文件上，点击右侧出现的 `+` (加号) 图标。
*   **暂存所有文件**: 点击“Changes”标题栏右侧的总 `+` (加号) 图标。

暂存后，文件会从“Changes”列表移动到“Staged Changes”列表。

#### 提交更改 (Commit)
1.  在顶部的输入框中填写清晰的提交信息。
2.  点击输入框上方的**对勾 (✓) 图标**，或者使用快捷键 `⌘+Enter` (Ctrl+Enter)。

如果“Staged Changes”中有文件，VS Code 只会提交这些已暂存的更改。如果没有，它会提示你是否要暂存所有更改并直接提交。

---

### 3. 分支管理

在 VS Code 中管理分支非常方便，主要通过左下角的状态栏完成。

![VS Code Status Bar](https://code.visualstudio.com/assets/docs/sourcecontrol/overview/incoming-outgoing-changes.png)

*   **查看当前分支**: 状态栏左下角会显示你当前所在的分支名（例如 `main` 或 `feature/add-author`）。
*   **切换分支**: 点击分支名，VS Code 会在屏幕顶部弹出一个列表，显示所有本地和远程分支。选择一个即可切换。
*   **创建新分支**:
    1.  打开命令面板 `⇧⌘P` (Ctrl+Shift+P)。
    2.  输入 `Git: Create Branch` 并回车。
    3.  输入你的新分支名并回车。VS Code 会自动创建并切换到这个新分支。

---

### 4. 与远程仓库交互

*   **同步更改 (Sync Changes)**: 当你的本地分支与远程分支关联后，状态栏的分支名旁边会出现一个循环箭头图标。点击它，VS Code 会执行 `git pull` 拉取远程更新，然后再执行 `git push` 推送你的本地提交。这是一个非常方便的同步命令。
*   **发布分支 (Publish Branch)**: 如果你创建了一个新的本地分支，这个图标会变成一个云朵上传的图标。点击它，可以将你的新分支发布到 GitHub 等远程仓库。

---

### 5. 解决合并冲突

当 `git pull` 或 `git merge` 导致合并冲突时，VS Code 提供了非常出色的解决工具。

*   在“Changes”列表中，冲突文件会以特殊颜色标记。
*   打开冲突文件，你会看到冲突的代码块被高亮，并且在代码上方出现几个可点击的选项：
    *   `Accept Current Change`: 保留你自己的更改。
    *   `Accept Incoming Change`: 接受从远程拉取下来或从其他分支合并过来的更改。
    *   `Accept Both Changes`: 同时保留两边的更改。
    *   `Compare Changes`: 在 Diff 视图中更详细地比较。

![VS Code Merge Conflict](https://code.visualstudio.com/assets/docs/sourcecontrol/overview/merge-conflict.png)

你只需要根据需求点击这些按钮，VS Code 就会自动清理冲突标记。解决所有冲突后，暂存文件并提交，即可完成合并。对于更复杂的冲突，VS Code 还提供了一个**三向合并编辑器 (3-way merge editor)**。

---

将命令行操作与 VS Code 的图形化界面相结合，是成为高效开发者的关键。通常，你可以使用 VS Code 处理 95% 的日常任务，只在需要进行复杂变基（rebase）等高级操作时才回到命令行。
