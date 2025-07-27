# Git 实战练习项目

欢迎来到 Git 实战练习！本指南将引导您完成一个完整的开发流程，从创建项目到推送到远程仓库。

**请严格按照步骤操作，亲自输入每一个命令，以达到最佳学习效果。**

---

### 第 0 步：准备工作

首先，我们需要为这个练习项目创建一个全新的文件夹。

1.  打开你的终端或命令行工具。
2.  **在 `git_tutorial` 目录外面**创建一个新目录，并进入该目录。

```bash
# 回到上一级目录 (如果你当前在 git-tutorial-for-beginners 里)
cd ..

# 创建一个新文件夹用于练习
mkdir git-practice-project

# 进入这个新文件夹
cd git-practice-project
```
**之后的所有操作，都将在这个 `git-practice-project` 文件夹中进行。**

---

### 第 1 步：项目初始化与首次提交

1.  **初始化 Git 仓库**
```bash
git init
```
你会看到一条消息 `Initialized empty Git repository in ...`。

2.  **创建项目文件**
让我们创建两个初始文件：`index.html` 和 `README.md`。

*   创建一个 `README.md` 文件，内容如下：
```markdown
# 我的 Git 实战项目
这是一个用来练习 Git 命令的简单项目。
```
*   创建一个 `index.html` 文件，内容如下：
```html
<!DOCTYPE html>
<html>
<head>
    <title>实战项目</title>
</head>
<body>
    <h1>欢迎来到我的项目</h1>
</body>
</html>
```
*   *你可以使用任何文本编辑器来创建这些文件。*

3.  **检查状态并暂存文件**
```bash
# 查看状态，你会看到两个 "untracked" 文件
git status

# 暂存所有新文件
git add .
```

4.  **进行首次提交**
```bash
git commit -m "Initial commit: Add README and index page"
```

5.  **查看历史**
```bash
git log --oneline
```
你应该能看到你的第一次提交记录。

---

### 第 2 步：分支开发

现在，我们要开发一个“添加作者信息”的新功能。为此，我们将创建一个新分支。

1.  **创建并切换到新分支**
我们将分支命名为 `feature/add-author`。
```bash
git checkout -b feature/add-author
```

2.  **在新分支上进行开发**
修改 `index.html` 文件，在 `<h1>` 标签下面添加一行。
```html
<!DOCTYPE html>
<html>
<head>
<title>实战项目</title>
</head>
<body>
<h1>欢迎来到我的项目</h1>
<p>作者：(这里写你的名字)</p>
</body>
</html>
```

3.  **提交你的功能**
```bash
# 检查状态，你会看到 index.html 被修改了
git status

# 暂存更改
git add index.html

# 提交更改
git commit -m "Feat: Add author information to index page"
```

---

### 第 3 步：合并分支

功能开发完成！现在我们把它合并回 `main` 分支。

1.  **切换回主分支**
```bash
git checkout main
```
*注意：切换回来后，你会发现 `index.html` 恢复到了没有作者信息的旧版本。别担心，这是正常的！*

2.  **合并功能分支**
```bash
git merge feature/add-author
```
现在再查看 `index.html`，作者信息已经合并过来了！

3.  **删除已合并的分支**
保持仓库整洁是一个好习惯。
```bash
git branch -d feature/add-author
```

---

### 第 4 步：模拟并解决冲突

冲突是协作中常见的情况。让我们来模拟一次。

1.  **创建第一个分支并修改 README**
```bash
# 基于 main 分支创建并切换
git checkout -b style-update
```
修改 `README.md` 的第二行，改为：
```markdown
# 我的 Git 实战项目
这是一个用来练习 Git 命令的**超棒**项目。
```
然后提交它：
```bash
git add README.md
git commit -m "Style: Update project description"
```

2.  **创建第二个分支并从同一点修改 README**
```bash
# 首先，必须切回 main 分支
git checkout main

# 创建第二个分支
git checkout -b content-update
```
现在，再次修改 `README.md` 的**同一行**，但内容不同：
```markdown
# 我的 Git 实战项目
这是一个用来练习 Git 命令的**简单**项目。
```
然后提交它：
```bash
git add README.md
git commit -m "Doc: Clarify project description"
```

3.  **尝试合并，制造冲突**
```bash
# 切回 main 分支
git checkout main

# 先合并第一个分支，这会成功
git merge style-update

# 再尝试合并第二个分支，这里会发生冲突！
git merge content-update
```
你会看到终端提示 `CONFLICT (content): Merge conflict in README.md`。

4.  **解决冲突**
*   打开 `README.md` 文件，你会看到类似这样的冲突标记：
    ```markdown
    # 我的 Git 实战项目
    <<<<<<< HEAD
    这是一个用来练习 Git 命令的**超棒**项目。
    =======
    这是一个用来练习 Git 命令的**简单**项目。
    >>>>>>> content-update
    ```
*   **手动编辑文件**，删除这些标记，并决定最终你想要的内容。比如，我们决定两个都不要，改成一个新版本：
    ```markdown
    # 我的 Git 实战项目
    这是一个用来练习 Git 命令的很棒的、简单的项目。
    ```
*   **暂存已解决的文件**
    ```bash
    git add README.md
    ```
*   **完成合并提交**
    ```bash
    git commit
    ```
    （此时 Git 会自动生成一条提交信息，你无需修改，直接保存退出即可）。

---

### 第 5 步：连接到远程仓库 (以 GitHub 为例)

1.  **在 GitHub 上创建一个新仓库**
*   登录你的 GitHub 账号。
*   点击右上角的 `+` 号，选择 `New repository`。
*   给仓库取个名字（例如 `git-practice-project`）。
*   **不要**勾选 "Initialize this repository with a README" 或添加 `.gitignore`。我们要做一个空的仓库。
*   点击 `Create repository`。

2.  **将本地仓库与远程仓库关联**
*   在 GitHub 仓库页面上，复制 "…or push an existing repository from the command line" 下面的仓库 URL。它看起来像 `https://github.com/YourUsername/git-practice-project.git`。
*   在你的终端里运行：
    ```bash
    # 把下面的 URL 换成你自己的
    git remote add origin https://github.com/YourUsername/git-practice-project.git
    ```

3.  **推送你的代码**
```bash
# -u 参数会设置本地 main 分支追踪远程 origin/main 分支
# 只需要在第一次推送时使用
git push -u origin main
```

现在，刷新你的 GitHub 页面，你会看到你本地的所有文件和提交历史都已经被上传上去了！

**恭喜你完成了整个实战练习！** 你已经体验了独立开发者使用 Git 的完整核心流程。