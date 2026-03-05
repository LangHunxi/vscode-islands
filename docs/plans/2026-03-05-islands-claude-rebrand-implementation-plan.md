# Islands Claude Rebrand Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** 让扩展以新 ID 与名称（`langhunxi.islands-claude` / `Islands Claude`）出现在 VS Code 扩展列表中，并保持改动最小。

**Architecture:** 仅更新 `package.json`、`themes/islands-dark.json` 与 `README.md` 顶部信息，其他文件不改，避免冲突。

**Tech Stack:** VS Code 扩展清单（`package.json`）、主题 JSON、Markdown 文档。

---

### Task 1: 更新扩展元数据

**Files:**
- Modify: `package.json`

**Step 1: 修改字段**

将以下字段更新为：
- `publisher`: `langhunxi`
- `name`: `islands-claude`
- `displayName`: `Islands Claude`
- `description`: 改为描述暖灰/奶油色、低对比、阅读友好浅色主题
- `repository.url`: `https://github.com/LangHunxi/vscode-islands`
- `contributes.themes[0].label`: `Islands Claude`

**Step 2: 保存文件**

无命令，仅确保 JSON 语法合法。

**Step 3: Commit**

```bash
git add package.json
git commit -m "chore: rebrand extension metadata"
```

---

### Task 2: 更新主题名称

**Files:**
- Modify: `themes/islands-dark.json`

**Step 1: 修改字段**

更新：
- `name`: `Islands Claude`

**Step 2: 保存文件**

无命令，仅确保 JSON 语法合法。

**Step 3: Commit**

```bash
git add themes/islands-dark.json
git commit -m "chore: rename theme label"
```

---

### Task 3: README 顶部最小更新

**Files:**
- Modify: `README.md`

**Step 1: 更新顶部内容**

修改：
- 标题改为 `Islands Claude`
- 简短描述改为浅色暖灰方向
- 增加 Fork 说明（脚本/安装说明暂沿用上游，建议优先 VSIX 安装）

**Step 2: 保存文件**

**Step 3: Commit**

```bash
git add README.md
git commit -m "docs: update readme header for Islands Claude"
```

---

### Task 4: 本地验证（非自动化）

**Files:**
- None

**Step 1: 重新安装或重载扩展**

如需看到新名称，需重新安装新 ID 的扩展（可用 VSIX 或手动放置扩展目录）。

**Step 2: 验证点**
- 扩展列表显示 `Islands Claude`
- 主题列表出现 `Islands Claude`

**Step 3: 记录结果**

若名称仍未显示，记录扩展列表截图与 `code --list-extensions --show-versions` 输出。
