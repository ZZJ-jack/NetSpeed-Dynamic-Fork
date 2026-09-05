# Welcome to the NetSpeed Dynamic Pro Contribution Guide

First of all, thank you for taking the time to contribute to **NetSpeed Dynamic Pro (NSD)**! Whether you have found a bug, have a feature idea, or want to submit code, you are very welcome.

Please take a few minutes to read the following guide. It will make your contribution process smoother and help us collaborate more efficiently.

---

## Table of Contents

1.  [How to Report a Bug or Suggest a Feature](#how-to-report-a-bug-or-suggest-a-feature)
2.  [Setting Up the Development Environment](#setting-up-the-development-environment)
3.  [Code Contribution Workflow](#code-contribution-workflow)
4.  [Code Style and Guidelines](#code-style-and-guidelines)
5.  [Commit Messages and Pull Request Guidelines](#commit-messages-and-pull-request-guidelines)
6.  [Getting Help](#getting-help)

---

## How to Report a Bug or Suggest a Feature

Before creating a new Issue, **please search existing Issues** to avoid duplicates.

- **Reporting a Bug**: Please use our [Bug Report template](.github/ISSUE_TEMPLATE/bug-report.yml) (if configured) and provide as much detail as possible:
  - Operating system version (Windows 10/11)
  - Application version number
  - Detailed steps to reproduce
  - Relevant logs or screenshots
- **Suggesting a Feature**: Please use our [Feature Request template](.github/ISSUE_TEMPLATE/feature-request.yml) (if configured) and clearly describe:
  - The pain point you encountered
  - Your expected solution
  - Any alternative approaches you have considered
  - Acceptance criteria (if definable)

> The project is currently tailored for the Windows platform, and some features rely on system SMTC, WinAPI, COM, etc. When describing your issue, please mention your Windows version and browser information if music control is involved.

---

## Setting Up the Development Environment

NSD is a Tauri 2 application with a Vue 3 + TypeScript frontend and a Rust backend. Before you start, make sure your development machine meets the following requirements:

### Prerequisites

- **Operating System**: Windows 10 or Windows 11 (required, as we rely on WinAPI and SMTC)
- **Node.js**: 18 or higher ([Download](https://nodejs.org/))
- **Rust**: 1.70 or higher ([Install](https://www.rust-lang.org/tools/install))
- **Tauri 2 CLI**: After installing Rust, run `cargo install tauri-cli` (recommended)
- **Git**: For version control

### Installation and Running Steps

```bash
# 1. Clone the repository
git clone https://github.com/GEORGEWWWU/NetSpeed-Dynamic.git
cd NetSpeed-Dynamic

# 2. Install frontend dependencies
npm install

# 3. Run in development mode (automatically launches the Tauri window)
npm run tauri dev
```

If everything goes well, you should see the main application window and the draggable Dynamic Island floating window.

### Building a Release Version

```bash
npm run tauri build
```

The build artifacts will be output to `src-tauri/target/release/bundle/`.

---

## Code Contribution Workflow

We recommend the standard **Fork + Pull Request** workflow, which is simple and does not require creating separate feature branches:

1.  **Fork this repository**: Click the "Fork" button in the upper right corner of the GitHub page to copy the project to your personal account.
2.  **Clone your fork**:
    ```bash
    git clone https://github.com/your-username/NetSpeed-Dynamic.git
    cd NetSpeed-Dynamic
    ```
3.  **Add the upstream remote (optional, but useful for syncing updates)**:
    ```bash
    git remote add upstream https://github.com/GEORGEWWWU/NetSpeed-Dynamic.git
    ```
4.  **Make your changes**: Modify the code or documentation directly in your local repository (by default, on the `main` branch).
    - Please ensure that new code is consistent with the existing style (see "Code Style and Guidelines" below).
    - If you add new functionality, please add corresponding tests if possible.
    - If you change user‑visible behaviour, please update the relevant documentation (README or user manual).
5.  **Test your changes**:
    - Run `npm run tauri dev` in development mode to manually test that your changes work and do not break existing functionality.
    - If you modify the Rust backend, run `cargo check` and `cargo clippy` to ensure there are no compilation errors or warnings.
6.  **Commit your changes**: Follow the [Conventional Commits](https://www.conventionalcommits.org/) specification (see below).
7.  **Push to your remote repository**:
    ```bash
    git push origin main
    ```
8.  **Create a Pull Request (PR)**:
    - On GitHub, submit a PR from your `main` branch to this repository's `main` branch.
    - In the PR description, **make sure to link the related Issue** (e.g., `Closes #123`).
    - Clearly explain the motivation, implementation approach, and testing performed.
    - If there are UI changes, please attach screenshots or GIFs for easier review.

> Note: If your fork is behind the upstream repository, we recommend syncing it first with `git pull upstream main`, resolving any conflicts, and then submitting the PR.

**Suggestions regarding PRs**:
- **Keep PRs as small and focused as possible**: Each PR should address a single clear issue or implement one specific feature, making it easier to review and merge.
- **For large‑scale refactoring or major features**: Please open an Issue first to describe your plan and get maintainer approval before starting development, to avoid PR rejection due to misalignment.

---

## Code Style and Guidelines

To maintain consistency and maintainability across the codebase, please adhere to the following guidelines:

### Frontend (Vue 3 + TypeScript)

- **Component naming**: Use PascalCase (e.g., `DynamicSet.vue`).
- **TypeScript**: Provide explicit type definitions for all variables, functions, and component props as much as possible, avoiding `any`.
- **Vue Composition API**: Prefer `<script setup>` syntax.

### Backend (Rust)

- **Naming**: Follow Rust conventions: PascalCase for structs and enums, snake_case for functions and variables.
- **Comments**: Add documentation comments (`///`) for important public functions and modules.

### General

- **Atomic commits**: Each commit should contain only one logical change; do not mix unrelated modifications.
- **Documentation for new features**: If you add new configuration options or command‑line parameters, update the relevant sections in the README accordingly.

---

## Commit Messages and Pull Request Guidelines

### Commit Message Format

We recommend using the **[Conventional Commits](https://www.conventionalcommits.org/)** specification, with the following format:

```
<type>(<scope>): <subject>
```

- **type**: Must be one of the following:
  - `feat`: New feature
  - `fix`: Bug fix
  - `docs`: Documentation update
  - `style`: Code style changes (no logic changes)
  - `refactor`: Code refactoring (neither a new feature nor a bug fix)
  - `perf`: Performance improvement
  - `test`: Adding or modifying tests
  - `chore`: Changes to build tools, dependencies, or auxiliary tools
  - `ci`: CI configuration changes
- **scope** (optional): The affected area, e.g., `music`, `notification`, `spectrum`, `settings`, etc.
- **subject**: A concise description, not exceeding 50 characters, in the present tense, starting with a lowercase letter, and without a trailing period.

**Examples**:
- `feat(music): add support for Kugou music SMTC recognition`
- `fix(notification): fix issue where clicking notification fails to open the app`
- `docs: update installation steps in README`
- `perf(spectrum): optimize FFT computation performance`

### Pull Request Description Guidelines

- **Title**: Follow the same style as commit messages, but it can be more concise.
- **Body**:
  - **Motivation**: Why is this change needed?
  - **Implementation**: Briefly describe how you implemented it.
  - **Testing**: What tests did you run to verify the change?
  - **Related Issue**: Use `Closes #XXX` or `Related #XXX`.
  - **Screenshots/GIFs** (if UI changes): Help reviewers understand the visual impact.

---

## Getting Help

If you encounter any problems during the contribution process, you can reach us through the following channels:

- **QQ Group**: [1080730621](https://qm.qq.com/cgi-bin/qm/qr?k=i70z7rbl-VWpejQugvlXeARDUjwP7sIW&jump_from=webapi&authKey=b6Pj6zLuuCINDhafPJRttePdy3D45vvtWzcZ109LWoWYXkcKo8bNWI7fMhr+yV87) (real‑time discussion)
- **GitHub Issues**: Leave a comment directly on the relevant Issue

We are happy to help you with any development or configuration questions!

---

Thank you again for your contribution! Every PR and every Issue makes NSD better.

> If you find this project useful, you are also welcome to support the author via [WeChat](src/assets/wechat-pay.png), [Alipay](src/assets/alipay.jpg), or [GitHub Sponsors](https://github.com/sponsors/GEORGEWWWU). This is entirely optional, of course.