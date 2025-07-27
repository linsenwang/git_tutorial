# 4. 分支

分支（Branching）是 Git 最强大、最核心的功能之一。它允许你从主开发线上分离出来，在一个独立的环境里进行工作，而不会影响到主线。

## 什么是分支？

想象一下你的项目是一条正在向前延伸的铁路主干道（通常叫做 `master` 或 `main` 分支）。

当你要开发一个新功能或修复一个 bug 时，你不想在主干道上直接施工，因为这可能会导致主路（你的稳定代码）瘫痪。

于是，你从主干道上开辟出一条**支线**。你在这条支线上进行所有的开发工作。当功能开发完成、测试通过后，你再把这条支线**合并**（merge）回主干道。

这就是分支的理念。Git 的分支非常轻量，创建和切换分支几乎是瞬间完成的。

---

## 常用命令

### `git branch`：列出、创建、删除分支

*   **列出所有本地分支**:
    ```bash
    git branch
    ```
    当前所在的分支会用一个 `*` 标记出来。

*   **创建一个新分支**:
    ```bash
    git branch <branch-name>
    ```
    例如，创建一个名为 `feature-login` 的分支：
    ```bash
    git branch feature-login
    ```
    这只是创建了分支，你还没有切换过去。

*   **删除一个已经合并的分支**:
    ```bash
    git branch -d <branch-name>
    ```
    如果分支还没有被合并，但你确定要删除它，可以使用 `-D` (大写) 选项。

### `git checkout`：切换分支

当你创建了一个新分支后，你需要切换到那个分支上才能开始工作。

```bash
git checkout <branch-name>
```

例如，切换到我们刚才创建的 `feature-login` 分支：
```bash
git checkout feature-login
```

现在，你所有的 `git commit` 操作都将发生在这个新分支上，而不会影响 `main` 分支。

### 创建并切换分支 (常用快捷方式)

通常，我们创建分支后会立即切换过去。Git 提供了一个方便的快捷命令 `checkout -b`，它可以一步完成这两个操作。

```bash
git checkout -b <new-branch-name>
```

这等同于下面这两条命令：
```bash
git branch <new-branch-name>
git checkout <new-branch-name>
```

例如，创建并切换到一个名为 `bugfix-header` 的新分支：
```bash
git checkout -b bugfix-header
```

---

**分支开发的基本流程**:

1.  **从主分支（例如 `main`）创建一个新分支**。
    ```bash
    # 确保你在主分支上并且代码是最新
    git checkout main
    git pull # (如果和远程仓库协作)

    # 创建并切换到新分支
    git checkout -b new-feature
    ```

2.  **在新分支上进行开发**：修改、暂存、提交。
    ```bash
    # ... 写代码 ...
    git add .
    git commit -m "实现新功能的第一步"
    # ... 继续写代码 ...
    git add .
    git commit -m "新功能基本完成"
    ```

3.  **开发完成后，切换回主分支**，准备合并。
    ```bash
    git checkout main
    ```

4.  **将新分支合并到主分支** (我们将在下一节详细介绍)。
    ```bash
    git merge new-feature
    ```

善用分支是高效使用 Git 的关键！
