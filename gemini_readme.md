# SuperKP.github.io

这是我的个人博客网站 ([SuperKP.github.io](https://SuperKP.github.io)) 的源代码。

## ✨ 技术栈 (Technology Stack)

*   **框架**: [Hugo (Extended version)](https://gohugo.io/) - 一个用 Go 编写的快速静态网站生成器。
*   **内容**: Markdown。
*   **样式**: SCSS。
*   **持续集成/持续部署 (CI/CD)**: [GitHub Actions](https://github.com/features/actions)。
*   **开发环境**: [Dev Container](https://code.visualstudio.com/docs/devcontainers/containers) (Docker)。

## 📂 目录结构 (Directory Structure)

```
.
├── .github/workflows/  # GitHub Actions 工作流配置 (例如：自动部署)
├── assets/             # 存放需要 Hugo Pipes 处理的资源 (如 SCSS, JS)
├── config/             # 存放 Hugo 站点的所有配置
├── content/            # 网站的所有 Markdown 内容 (博客文章、页面等)
├── static/             # 存放静态文件 (图片、CSS、JS 等)，这些文件会原样复制到网站根目录
├── .devcontainer/      # Visual Studio Code 开发容器的配置
├── go.mod              # Go 模块定义文件，用于管理 Hugo 主题和模块
└── README.md           # 你正在阅读的这个文件
```

---

## 🚀 环境搭建与本地运行 (Setup and Local Development)

你可以通过以下两种方式在本地运行此网站。

### 方法一：使用 Dev Container (推荐)

这是最简单、最推荐的方法，可以确保环境的一致性。

1.  安装 [Docker Desktop](https://www.docker.com/products/docker-desktop/)。
2.  安装 [Visual Studio Code](https://code.visualstudio.com/)。
3.  在 VS Code 中安装 [Dev Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) 扩展。
4.  克隆此仓库并在 VS Code 中打开它。
5.  VS Code 右下角会弹出一个提示，询问你是否 "Reopen in Container"。点击它。
6.  等待容器构建完成。构建完成后，在 VS Code 的终端中运行以下命令启动本地服务器：

    ```bash
    hugo server -D
    ```

7.  在浏览器中打开 `http://localhost:1313` 即可预览网站。

### 方法二：本地安装

如果你不想使用 Docker，可以手动在你的机器上安装所需环境。

1.  **安装 Go**: 参考 [官方文档](httpshttps://go.dev/doc/install) 安装 Go 语言环境。
2.  **安装 Hugo**:
    *   **macOS/Linux**: 使用 Homebrew `brew install hugo`。
    *   **Windows**: 使用 Chocolatey `choco install hugo-extended` 或 Scoop `scoop install hugo-extended`。
    *   **注意**: 必须安装 **Extended** 版本，因为项目使用了 SCSS。
3.  **克隆仓库**:
    ```bash
    git clone https://github.com/SuperKP/SuperKP.github.io.git
    cd SuperKP.github.io
    ```
4.  **更新主题和模块**:
    ```bash
    hugo mod tidy
    ```
5.  **启动本地服务器**:
    ```bash
    hugo server -D
    ```
6.  在浏览器中打开 `http://localhost:1313` 即可预览网站。

## 🛠️ 构建与部署 (Build and Deployment)

### 构建

要将网站构建为静态 HTML 文件，请运行：

```bash
hugo
```

所有静态文件将被生成并存放在 `public/` 目录下。

### 部署

该项目已配置了通过 GitHub Actions 实现的自动化部署。当你将更改推送到 `main` 分支时，`.github/workflows/deploy.yml` 工作流会自动触发。

该工作流会执行以下操作：
1.  检出代码。
2.  设置 Hugo 环境。
3.  构建网站 (`hugo`)。
4.  将 `public/` 目录下的内容部署到 `gh-pages` 分支，从而更新你的 GitHub Pages 网站。
