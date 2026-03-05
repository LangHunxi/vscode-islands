# Tabs Unified CSS Design (Editor Only)

## 背景与目标
- 解决 VS Code 顶部标签页在不同焦点状态下位置跳动、圆角缺失、与编辑区连接处出现缝隙的问题。
- 统一样式：不区分焦点状态，使用最高优先级规则强制覆盖。
- 仅影响**编辑器顶部标签**，不影响底部面板（终端/输出/问题）。

## 约束
- 清理现有与 `.tabs-container` / `.tab` 相关的布局类规则（仅布局，保留内部小样式）。
- 统一使用 `!important`。
- Active Tab 背景必须等于 `var(--vscode-editor-background)`。
- 隐藏 Active Tab 伪元素 `::before`/`::after`。
- Active Tab `border-bottom: none`，与编辑区无缝融合。
- Inactive Tab 背景使用 `var(--vscode-editorGroupHeader-tabsBackground)`，底部保留细线分隔。
- 顶部留白 `margin-top = 6px`。

## 方案
- 在 `custom-ui-style.stylesheet` 中添加编辑器范围选择器：
  - `.monaco-workbench .part.editor .tabs-container`
  - `.monaco-workbench .part.editor .tabs-container .tab`
  - `.monaco-workbench .part.editor .tabs-container .tab.active`
  - `.monaco-workbench .part.editor .tabs-container .tab.active::before/::after`
  - `.monaco-workbench .part.editor .tabs-container .tab:not(.active)`
  - `.monaco-workbench .part.editor .tabs-container .tab.tab-border-top/.tab-border-bottom`
- 移除旧的 `.tabs-container`/`.tab` 布局规则，避免冲突。

## 样式要点（概要）
- Tabs 容器：背景为 tabsBackground，去除底部分隔线。
- Tab 基础：上圆角、`margin-top: 6px`，去除上/左/右边框。
- Active Tab：背景与编辑区一致，隐藏伪元素，`border-bottom: none`。
- Inactive Tab：背景为 tabsBackground，底部 1px 细线。

## 验证
- 执行 `Custom UI Style: Reload` 与 `Developer: Reload Window`。
- 在编辑器与侧边栏/面板间切换焦点，确认：
  - Active Tab 位置不跳动
  - 左上角圆角稳定
  - 与编辑区无缝衔接
