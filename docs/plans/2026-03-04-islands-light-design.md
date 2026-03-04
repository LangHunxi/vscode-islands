# Islands Light Theme Design

Date: 2026-03-04

## Summary
Add a new light theme variant that matches the Claude warm-gray palette while keeping syntax highlighting aligned with GitHub Light Default. Minimize upstream merge conflicts by adding new files and minimal edits to existing metadata/docs.

## Goals
- Provide a new `Islands Light` theme with `uiTheme: "vs"`.
- Base syntax highlighting on GitHub Light Default, then apply small UI overrides to match Claude colors.
- Keep existing `Islands Dark` unchanged to reduce conflicts.
- Provide a light-specific UI stylesheet settings file for Custom UI Style users.

## Non-goals
- Rebranding the extension name or publisher.
- Large refactors of scripts or build tooling.
- Replacing the existing dark theme.

## Constraints
- Change surface area must be small to reduce upstream merge conflicts.
- Use the provided Claude palette: `#fdfdf7` (canvas), `#e4e4df` (surface), `#d97757` (accent) with neutral grays/blacks.
- Syntax highlighting should remain close to GitHub Light Default.

## Options Considered
1. Add a new light theme + settings file (recommended).
2. Convert the existing dark theme in place.
3. Use only user `workbench.colorCustomizations` without changing the extension.

Chosen: Option 1 because it preserves the dark theme and keeps edits limited to a few files.

## Architecture
- Theme files are static JSON under `themes/`.
- Extension metadata is in `package.json` under `contributes.themes`.
- Custom UI Style CSS is configured via `settings.json` and will be duplicated into a `settings-light.json` with light colors.

## Components / Files
- New: `themes/islands-light.json`
  - Source base: GitHub Light Default theme JSON (colors + tokenColors).
  - Overrides: UI background/surface/accent/borders to match Claude palette.
- New: `settings-light.json`
  - Copy of `settings.json` with light palette variables and softened borders/shadows.
- Modified: `package.json`
  - Add a new theme entry: label `Islands Light`, `uiTheme: "vs"`, path `./themes/islands-light.json`.
- Modified: `README.md`
  - Document how to enable the light theme and the light settings file.

## Data Flow
No runtime data flow. VS Code loads the selected theme JSON and applies it. The Custom UI Style extension reads the user settings JSON to apply CSS.

## Error Handling
- Validate JSON syntax for new theme and settings files.
- Ensure `uiTheme` matches light theme (`vs`) and colors are valid hex strings.

## Testing / Verification
- Confirm `themes/islands-light.json` parses as valid JSON.
- Confirm `package.json` contribution includes the new theme.
- Manual sanity check in VS Code (if available) to verify readability and contrast on key UI elements.

## Rollout / Migration
- No migration needed. Users can opt into the light theme by selecting it in VS Code and optionally applying `settings-light.json`.
