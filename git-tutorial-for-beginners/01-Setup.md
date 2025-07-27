# 1. Git 安装与配置

在使用 Git 之前，你需要先在你的电脑上安装它，并进行一些基础配置。

## 安装 Git

Git 支持所有主流操作系统，包括 Windows, macOS 和 Linux。

*   **Windows**:
    *   访问 [git-scm.com/download/win](https://git-scm.com/download/win) 下载安装程序。
    *   运行安装程序，按照默认选项完成安装即可。

*   **macOS**:
    *   最简单的方式是安装 Xcode Command Line Tools。打开终端并运行：
        ```bash
        xcode-select --install
        ```
    *   你也可以使用 [Homebrew](https://brew.sh/) 包管理器来安装：
        ```bash
        brew install git
        ```

*   **Linux (Debian/Ubuntu)**:
    *   打开终端并运行：
        ```bash
        sudo apt-get update
        sudo apt-get install git
        ```

安装完成后，你可以在终端（或 Windows 的 Git Bash）里输入以下命令来验证是否安装成功：

```bash
git --version
```

如果它显示了 Git 的版本号（例如 `git version 2.30.1`），说明你已经成功安装了！

## 首次运行 Git 前的配置

安装完 Git 后，第一件要做的事就是设置你的**用户名**和**邮箱地址**。这非常重要，因为你的每一次提交（commit）都会使用这些信息。

在终端里运行以下命令，并换成你自己的信息：

```bash
git config --global user.name "Your Name"
git config --global user.email "youremail@example.com"
```

`--global` 选项表示你这台电脑上所有的 Git 仓库都会使用这个配置。如果你希望某个特定的项目使用不同的配置，可以在那个项目目录里不加 `--global` 选项再运行一次。

你可以用下面的命令来检查你的配置：

```bash
git config --list
```

它会列出所有的 Git 配置，确保 `user.name` 和 `user.email` 是正确的。

完成这些步骤后，你的 Git 环境就准备就绪了！
