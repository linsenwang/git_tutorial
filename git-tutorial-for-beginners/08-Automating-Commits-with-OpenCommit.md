# 8. 使用 OpenCommit 自动生成提交信息

编写清晰、规范的 Git 提交信息（Commit Message）是一项非常重要的工程实践。好的提交信息能让协作者快速理解代码变更，也便于未来追溯历史。然而，每次都手动编写规范的提交信息有时会显得繁琐。

幸运的是，我们可以借助 AI 工具来自动化这个过程。**OpenCommit** 就是这样一款流行的工具，它能分析你暂存的（staged）代码改动，并自动生成符合[约定式提交规范](https://www.conventionalcommits.org/)（Conventional Commits）的提交信息。

---

### 1. 安装 OpenCommit

OpenCommit 是一个基于 Node.js 的包，所以你需要先确保你的电脑上已经安装了 **Node.js** 和 **npm**。

*   你可以在终端运行 `node -v` 和 `npm -v` 来检查它们是否已安装。
*   如果没有，请从 [Node.js 官网](https://nodejs.org/) 下载并安装。

安装完 Node.js 后，运行以下命令来全局安装 OpenCommit：

```bash
npm install -g opencommit
```

---

### 2. 配置 AI 模型

OpenCommit 需要使用 LLM（大语言模型）的 API 来分析代码并生成文本。你可以选择使用 OpenAI 的云服务，也可以选择在本地运行模型（例如通过 Ollama）。

#### **选项 A：配置 OpenAI API 密钥 (云端)**

1.  **获取密钥**：
    *   访问 [platform.openai.com/api-keys](https://platform.openai.com/api-keys)。
    *   使用你的 OpenAI 账号登录（**确保账户已绑定支付方式**，否则 API 无法使用）。
    *   点击 `Create new secret key`，然后复制生成的密钥。

2.  **配置密钥**：
    运行以下命令，将你刚刚复制的密钥配置到 OpenCommit 中。**（注意：命令是 `oco`，变量是 `OCO_API_KEY`）**

    ```bash
    # 校正了命令 oc -> oco 和变量名
    oco config set OCO_API_KEY=<你的API密钥>
    ```
    例如：`oco config set OCO_API_KEY=sk-xxxxxxxxxxxxxxxxxxxx`

    **⚠️ 重要安全提示**：
    *   **绝对不要**将你的 API 密钥泄露给他人，或提交到公共的 Git 仓库中。
    *   这个命令会将密钥保存在你本地用户目录下的 `~/.opencommit` 配置文件中，不会影响你的项目。

#### **选项 B：配置本地模型 Ollama (本地)**

如果你关心隐私或想节省 API費用，可以在本地运行模型。

1.  **安装并运行 Ollama**：根据 [Ollama 官网](https://ollama.com/) 指示进行安装。
2.  **拉取模型**：推荐使用 `llama3:8b` 或 `mistral`。
    ```bash
    ollama run llama3:8b
    ```
3.  **配置 OpenCommit 使用 Ollama**：
    ```bash
    # 设置提供商为 ollama
    oco config set OCO_AI_PROVIDER=ollama
    # 设置使用的模型
    oco config set OCO_MODEL=llama3:8b
    ```

---

### 3. 使用方法

使用 OpenCommit 非常简单，它可以替代你工作流中的 `git commit` 命令。

#### **标准流程**

1.  像往常一样修改你的代码。
2.  将你想要提交的更改添加到暂存区。**（此步骤可选，`oco` 会自动帮你暂存所有未暂存的改动）**
    ```bash
    # 暂存所有更改 (可选)
    git add .
    ```
3.  运行 OpenCommit 命令。**（注意：命令是 `oco`）**
    ```bash
    # 校正了命令 oc -> oco
    oco
    ```
    或者 `opencommit` 完整命令也可以。

4.  **确认提交信息**：
    *   OpenCommit 会连接 AI 服务，分析你的代码改动，然后生成一条提交信息并显示在终端上。
    *   它会询问你 `Accept commit message? (y/n)`。
    *   如果你对生成的提交信息满意，输入 `y` 并回车。OpenCommit 就会用这条信息为你创建一次提交。
    *   如果你不满意，输入 `n`，它会退出，你可以选择修改代码或重新运行。

#### **更佳实践：设置为 Git 钩子 (Hook)**

**这是官方推荐的“杀手级功能”**。通过设置 Git 钩子，你可以无缝地将 OpenCommit 集成到 `git commit` 命令中，无需再单独运行 `oco`。

1.  **设置钩子**：
    ```bash
    oco hook set
    ```
2.  **使用钩子**：
    现在，你的工作流就和以前完全一样了！
    ```bash
    git add .
    git commit
    ```
    当你执行 `git commit` 时，OpenCommit 会自动拦截，生成提交信息，并填充到你的编辑器中让你确认。这与 IDE 的 Git 工具（如 VS Code Source Control）能完美配合。

3.  **卸载钩子**（如果需要）：
    ```bash
    oco hook unset
    ```

---

### 4. 实战示例

让我们回到 `git-practice-project` 项目，模拟一次使用 OpenCommit 的过程。

1.  **做一个小修改**
    打开 `index.html` 文件，在底部添加一个页脚。
    ```html
    <!-- ... body 的其他内容 ... -->
    <footer>
        <p>&copy; 2025 我的实战项目</p>
    </footer>
    </body>
    </html>
    ```

2.  **使用 OpenCommit (已设置钩子)**
    ```bash
    # 暂存更改
    git add index.html
    # 正常执行 commit
    git commit
    ```
    此时，终端会调用 OpenCommit，并显示生成的提交信息等待你确认。

    **（未使用钩子）**
    ```bash
    # 直接运行 oco
    oco
    ```

3.  **查看结果**
    终端可能会显示类似下面的内容（**默认模型为 gpt-4o-mini，结果可能更优**）：
    ```
    feat: add project footer with copyright
    
    Adds a `<footer>` section to the `index.html` page.
    The new footer includes a paragraph with a copyright notice for the year 2025, enhancing the page's completeness.
    
    Accept commit message? (y/n)
    ```

4.  **确认提交**
    输入 `y` 并回车。提交就完成了！

5.  **验证**
    运行 `git log --oneline`，你就能看到刚刚由 OpenCommit 生成并提交的记录。

---

### **5. 更多常用配置**

OpenCommit 提供了丰富的配置项，你可以通过 `oco config set <key>=<value>` 来设置。

*   **更换模型**：在性能和成本之间做权衡。`gpt-4o` 效果最好，`gpt-3.5-turbo` 更经济。
    ```bash
    oco config set OCO_MODEL=gpt-4o
    ```
*   **添加 Emoji 前缀**：让你的提交历史更生动。
    ```bash
    oco config set OCO_EMOJI=true
    ```
*   **设置提交信息语言**：支持多种语言，如中文。
    ```bash
    oco config set OCO_LANGUAGE=zh-CN
    ```
*   **忽略文件**：创建一个 `.opencommitignore` 文件（类似 `.gitignore`），写入不需要 AI 分析的文件或路径，如 lock 文件或大型二进制文件。
    ```
    # .opencommitignore
    pnpm-lock.yaml
    **/*.lock
    dist/
    ```

通过这种方式，你不仅节省了时间，还能保证项目拥有一个非常整洁、专业且一致的提交历史。