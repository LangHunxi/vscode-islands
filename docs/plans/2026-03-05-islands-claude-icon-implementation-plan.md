# Islands Claude Icon Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** 生成并添加 `icon.png`，用于 VS Code 扩展列表展示，风格为暖灰/奶油色、双弧互抱图形。

**Architecture:** 使用 ImageMagick 生成 512x512 PNG（圆角方底 + 双弧），保存为仓库根目录 `icon.png`，无需改动代码逻辑。

**Tech Stack:** ImageMagick `convert`、PNG。

---

### Task 1: 生成 icon.png

**Files:**
- Create: `icon.png`

**Step 1: 生成图标**

运行以下命令生成图标：

```bash
convert -size 512x512 xc:transparent \
  -fill '#F2EFEA' -draw "roundrectangle 32,32 480,480 96,96" \
  -stroke '#D97757' -strokewidth 44 -fill none -stroke-linecap round -stroke-linejoin round \
  -draw "arc 88,120 304,392 300,60" \
  -draw "arc 208,120 424,392 120,240" \
  icon.png
```

**Step 2: 验证尺寸**

```bash
identify icon.png
```

期望输出包含 `512x512`.

**Step 3: Commit**

```bash
git add icon.png
git commit -m "assets: add Islands Claude icon"
```

---

### Task 2: 本地验证（非自动化）

**Files:**
- None

**Step 1: 重新打包并安装**

使用 `npx @vscode/vsce package` 打包后安装 VSIX，或直接复制到扩展目录。

**Step 2: 验证点**
- 扩展列表显示图标
- 图标视觉符合“暖灰/奶油色 + 双弧互抱”

**Step 3: 记录结果**

如需微调颜色/线宽/弧度，记录截图与反馈。
