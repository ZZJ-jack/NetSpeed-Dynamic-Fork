# 欢迎来到 NetSpeed Dynamic Pro 贡献指南

首先，感谢你愿意花时间为 **NetSpeed Dynamic Pro (NSD)** 贡献力量！无论你是发现了 Bug、想到了新功能，还是想提交代码，我们都非常欢迎。

请花几分钟阅读以下指南，这会让你的贡献过程更加顺畅，也帮助我们更高效地协作。

---

## 目录

1.  [如何报告 Bug 或提出功能建议](#如何报告-bug-或提出功能建议)
2.  [开发环境搭建](#开发环境搭建)
3.  [贡献代码的流程](#贡献代码的流程)
4.  [代码风格与规范](#代码风格与规范)
5.  [提交信息与 Pull Request 规范](#提交信息与-pull-request-规范)
6.  [寻求帮助](#寻求帮助)

---

## 如何报告 Bug 或提出功能建议

在创建新 Issue 前，**请先搜索已有 Issues**，避免重复提交。

*   **报告 Bug**：请使用我们提供的 [Bug 报告模板](.github/ISSUE_TEMPLATE/bug-report.yml)，并尽量提供：
    *   操作系统版本（Windows 10/11）
    *   应用版本号
    *   详细的复现步骤
    *   相关的日志或截图
*   **提出功能建议**：请使用 [功能建议模板](.github/ISSUE_TEMPLATE/feature-request.yml)，清晰描述：
    *   你遇到了什么痛点
    *   你期望的解决方案
    *   是否有替代方案
    *   验收标准（如果可定义）

> 项目当前主要针对 Windows 平台，部分功能依赖系统 SMTC、WinAPI、COM 等，请在描述时说明你的 Windows 版本和浏览器信息（如果涉及音乐控制）。

---

## 开发环境搭建

NSD 是一个 Tauri 2 应用，前端使用 Vue 3 + TypeScript，后端使用 Rust。在开始之前，请确保你的开发机满足以下要求：

### 依赖要求

- **操作系统**：Windows 10 或 Windows 11（必需，因为依赖 WinAPI 和 SMTC）
- **Node.js**：18 或更高版本（[下载](https://nodejs.org/)）
- **Rust**：1.70 或更高版本（[安装](https://www.rust-lang.org/tools/install)）
- **Tauri 2 CLI**：安装完 Rust 后，运行 `cargo install tauri-cli`（建议安装）
- **Git**：用于版本控制

### 安装与运行步骤

```bash
# 1. 克隆仓库
git clone https://github.com/GEORGEWWWU/NetSpeed-Dynamic.git
cd NetSpeed-Dynamic

# 2. 安装前端依赖
npm install

# 3. 以开发模式运行（会自动启动 Tauri 窗口）
npm run tauri dev
```

如果一切顺利，你应该能看到应用主窗口和可拖拽的灵动岛悬浮窗。

### 构建发布版本

```bash
npm run tauri build
```

构建产物会输出到 `src-tauri/target/release/bundle/` 目录下。

---

## 贡献代码的流程

我们推荐使用 **Fork + Pull Request** 的标准流程，操作简单，无需创建额外的功能分支：

1.  **Fork 本仓库**：点击 GitHub 页面右上角的 “Fork” 按钮，将项目复制到你的个人账户下。
2.  **Clone 你的 Fork**：
    ```bash
    git clone https://github.com/你的用户名/NetSpeed-Dynamic.git
    cd NetSpeed-Dynamic
    ```
3.  **添加上游仓库（可选，便于同步更新）**：
    ```bash
    git remote add upstream https://github.com/GEORGEWWWU/NetSpeed-Dynamic.git
    ```
4.  **进行修改**：在本地直接修改代码或文档（默认在 `main` 分支上操作）。
    *   请确保新代码与现有风格保持一致（见下文“代码风格”）。
    *   如果新增了功能，请尽可能添加对应的测试。
    *   如果修改了用户可见的行为，请同步更新相关文档（README 或用户手册）。
5.  **测试你的改动**：
    *   在开发模式下运行 `npm run tauri dev`，手动测试你的改动是否生效，并确保没有破坏现有功能。
    *   如果涉及 Rust 后端，运行 `cargo check` 和 `cargo clippy` 确保没有编译错误和警告。
6.  **提交你的更改**：请遵循 [Conventional Commits](https://www.conventionalcommits.org/) 规范（见下节）。
7.  **推送到你的远程仓库**：
    ```bash
    git push origin main
    ```
8.  **创建 Pull Request (PR)**：
    *   在 GitHub 上，从你的 `main` 分支向本仓库的 `main` 分支提交 PR。
    *   在 PR 描述中，**务必关联相关的 Issue 编号**（例如 `Closes #123`）。
    *   清晰说明改动的动机、实现方式以及测试情况。
    *   如果涉及 UI 变化，请附上截图或 GIF 动图。

> 注意：如果你的 Fork 落后于上游仓库，建议先通过 `git pull upstream main` 同步更新，解决冲突后再提交 PR。

**关于 PR 的几点建议**：
- **尽量保持 PR 小而聚焦**：每个 PR 只解决一个明确的问题或实现一个单一功能，这样更容易审查和合并。
- **如果是大规模重构或重大功能**：请先在 Issues 中提出，并描述你的计划，征得维护者同意后再着手开发，避免因方向偏差导致 PR 被拒绝。

---

## 代码风格与规范

为了保持代码库的一致性和可维护性，请遵守以下规范：

### 前端（Vue 3 + TypeScript）

- **组件命名**：使用 PascalCase（如 `DynamicSet.vue`）。
- **TypeScript**：尽量为所有变量、函数和组件 props 提供明确的类型定义，避免使用 `any`。
- **Vue 组合式 API**：推荐使用 `<script setup>` 语法。

### 后端（Rust）

- **命名**：遵循 Rust 惯例，结构体、枚举使用 PascalCase，函数、变量使用 snake_case。
- **注释**：为重要的公共函数和模块添加文档注释（`///`）。

### 通用

- **原子化提交**：每个提交应只包含一个逻辑上的更改，不要混合多个不相关的改动。
- **新功能文档**：如果添加了新配置项或命令行参数，请同步更新 README 中的相关章节。

---

## 提交信息与 Pull Request 规范

### 提交信息格式

我们推荐使用 **[Conventional Commits](https://www.conventionalcommits.org/)** 规范，格式为：

```
<type>(<scope>): <subject>
```

- **type**：必须为以下之一：
  - `feat`：新功能
  - `fix`：Bug 修复
  - `docs`：文档更新
  - `style`：代码格式（不影响代码逻辑的修改）
  - `refactor`：代码重构（既不是新功能也不是修复）
  - `perf`：性能优化
  - `test`：增加或修改测试
  - `chore`：构建工具、依赖或辅助工具的变动
  - `ci`：CI 配置变更
- **scope**（可选）：表示影响的范围，例如 `music`、`notification`、`spectrum`、`settings` 等。
- **subject**：简洁的描述，不超过 50 个字符，使用现在时，首字母小写，结尾不加句号。

**示例**：
- `feat(music): 增加对酷狗音乐SMTC的识别支持`
- `fix(notification): 修复通知点击后无法打开应用的问题`
- `docs: 更新README中的安装步骤`
- `perf(spectrum): 优化FFT计算性能`

### Pull Request 描述规范

- **标题**：与提交信息风格一致，但可以更简明。
- **正文**：
  - **动机**：为什么需要这个改动？
  - **实现方式**：简要说明你是如何实现的。
  - **测试**：你做了哪些测试来验证改动？
  - **关联 Issue**：使用 `Closes #XXX` 或 `Related #XXX`。
  - **截图/GIF**（如有 UI 变化）：便于审查者直观理解。

---

## 寻求帮助

如果在贡献过程中遇到任何问题，可以通过以下方式联系我们：

- **QQ 群**：[1080730621](https://qm.qq.com/cgi-bin/qm/qr?k=i70z7rbl-VWpejQugvlXeARDUjwP7sIW&jump_from=webapi&authKey=b6Pj6zLuuCINDhafPJRttePdy3D45vvtWzcZ109LWoWYXkcKo8bNWI7fMhr+yV87)（实时交流）
- **GitHub Issues**：直接在相关 Issue 下留言讨论

我们非常乐意协助你解决任何开发或配置上的疑难！

---

再次感谢你的贡献！每一个 PR、每一条 Issue 都会让 NSD 变得更好。

> 如果你觉得这个项目有用，也欢迎通过 [微信](src/assets/wechat-pay.png)、[支付宝](src/assets/alipay.jpg) 或 [GitHub Sponsors](https://github.com/sponsors/GEORGEWWWU) 支持作者，但这完全不是必须的。