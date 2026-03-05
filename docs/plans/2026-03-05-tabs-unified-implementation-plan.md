# Editor Tabs Unified CSS Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** 统一编辑器顶部标签在所有焦点状态下的圆角、间距与无缝连接表现，消除跳动与缝隙。

**Architecture:** 在 `custom-ui-style.stylesheet` 中移除旧的 `.tabs-container/.tab` 布局规则，新增仅作用于编辑器区域的高优先级全局规则（全部 `!important`），不区分焦点状态。

**Tech Stack:** VS Code `Custom UI Style` 插件配置、JSON、CSS 选择器。

---

### Task 1: 清理旧的 Tabs 布局规则

**Files:**
- Modify: `settings.json`

**Step 1: 移除旧规则**

删除以下布局相关选择器的配置块：
- `.tabs-container`
- `.tab`
- `.tab.active`
- `.tab:not(.active)`
- `.tab.active:first-child`
- `.part.panel.bottom .tabs-container`

**Step 2: 保存文件**

无命令，仅确保 `settings.json` 语法合法。

**Step 3: Commit**

```bash
git add settings.json
git commit -m "style: remove legacy tab layout rules"
```

---

### Task 2: 添加统一的编辑器 Tabs 覆盖规则

**Files:**
- Modify: `settings.json`

**Step 1: 添加规则**

在 `custom-ui-style.stylesheet` 中加入以下规则（全部保留 `!important`）：

```jsonc
".monaco-workbench .part.editor .tabs-container": {
  "background-color": "var(--vscode-editorGroupHeader-tabsBackground) !important",
  "border-bottom": "none !important"
},
".monaco-workbench .part.editor .tabs-container .tab": {
  "margin-top": "6px !important",
  "border-top-left-radius": "var(--islands-item-radius) !important",
  "border-top-right-radius": "var(--islands-item-radius) !important",
  "border-top": "none !important",
  "border-left": "none !important",
  "border-right": "none !important",
  "background-color": "var(--vscode-editorGroupHeader-tabsBackground) !important"
},
".monaco-workbench .part.editor .tabs-container .tab.active": {
  "background-color": "var(--vscode-editor-background) !important",
  "border-bottom": "none !important",
  "box-shadow": "none !important",
  "z-index": "1 !important"
},
".monaco-workbench .part.editor .tabs-container .tab.active::before": {
  "display": "none !important",
  "content": "'' !important"
},
".monaco-workbench .part.editor .tabs-container .tab.active::after": {
  "display": "none !important",
  "content": "'' !important"
},
".monaco-workbench .part.editor .tabs-container .tab:not(.active)": {
  "background-color": "var(--vscode-editorGroupHeader-tabsBackground) !important",
  "border-bottom": "1px solid rgba(0,0,0,0.06) !important"
},
".monaco-workbench .part.editor .tabs-container .tab.tab-border-top": {
  "border-top": "none !important"
},
".monaco-workbench .part.editor .tabs-container .tab.tab-border-bottom": {
  "border-bottom": "none !important"
}
```

**Step 2: 保存文件**

无命令，仅确保 JSON 语法合法。

**Step 3: Commit**

```bash
git add settings.json
git commit -m "style: unify editor tabs css"
```

---

### Task 3: 手动验证（无自动化测试）

**Files:**
- None

**Step 1: 重新加载样式**

在 VS Code 中运行：
- `Custom UI Style: Reload`
- `Developer: Reload Window`

**Step 2: 验证结果**

检查：
- 点击侧边栏或切换焦点时，Active Tab 位置不跳动
- 左上角圆角始终存在
- Active Tab 与编辑器区域无缝连接，无缝隙/错位

**Step 3: 记录结果**

如果仍有跳动/缝隙，记录具体元素类名与截图，以便追加微调。
