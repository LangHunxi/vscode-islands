# Islands Claude Rebrand Design

## 目标
- 让扩展在 VS Code 扩展列表中以全新 ID 与名称出现。
- 保持改动范围最小，降低与上游更新的冲突风险。

## 范围与约束
- 采用 **B-最小范围**：
  - 更新 `package.json`（扩展 ID 与展示名称）
  - 更新 `themes/islands-dark.json`（主题显示名称）
  - 更新 `README.md` 顶部信息与仓库链接
- 不更新安装脚本、Nix、卸载脚本等其余文件。

## 设计方案
### 扩展元数据（必改）
- `publisher`: `langhunxi`
- `name`: `islands-claude`
- `displayName`: `Islands Claude`
- `description`: 描述暖灰/奶油色、低对比、阅读友好浅色主题
- `repository.url`: `https://github.com/LangHunxi/vscode-islands`
- `contributes.themes[0].label`: `Islands Claude`

### 主题名称（必改）
- `themes/islands-dark.json` 中：
  - `name`: `Islands Claude`

### README（最小更新）
- 标题改为 `Islands Claude`
- 简短描述改为浅色暖灰方向
- 增加一段 Fork 说明：基于 Islands Dark 分支，脚本/安装说明暂沿用上游，建议优先 VSIX 安装
- 其余内容保持不变，避免大范围替换

## 非目标
- 不修改安装脚本、卸载脚本、Nix 配置、截图与历史说明
- 不改变扩展功能行为，仅重命名与说明更新

## 验证标准
1. 扩展列表显示 `Islands Claude`
2. 扩展 ID 为 `langhunxi.islands-claude`
3. 主题列表出现 `Islands Claude`
