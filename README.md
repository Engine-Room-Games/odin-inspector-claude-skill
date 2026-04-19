# Odin Inspector Claude Skill

A [Claude Code](https://docs.claude.com/en/docs/claude-code) skill that configures Unity inspectors using [Odin Inspector](https://odininspector.com/)'s Visual Designer (`.ovdf` files) — without modifying your C# source.

## What It Does

Ask Claude to improve, organize, or decorate the inspector for any `MonoBehaviour` or `ScriptableObject` in your project. The skill:

- Reads your C# class (fields, methods, `[field: SerializeField]` auto-properties)
- Writes or updates a `.ovdf` file under `Assets/Plugins/Sirenix/Odin Inspector/Visual Designer/Saved/`
- Applies Odin attributes (tabs, groups, buttons, progress bars, etc.) purely through OVDF — your source files stay untouched
- Avoids known Odin crash traps: unverified `SdfIconType` values, read-only attribute properties, the `Get*` color-field pattern

Example prompts:

- "Improve the inspector for `PlayerController`"
- "Add a Button to the `Kill` method on `Enemy`"
- "Group health and mana fields in a box on `PlayerStats`"
- "Put Attack, Defense, Magic into tabs on `EnemyConfig`"

## Requirements

- A Unity project with [Odin Inspector](https://assetstore.unity.com/packages/tools/utilities/odin-inspector-and-serializer-89041) installed (Visual Designer ships with Odin)
- [Claude Code](https://docs.claude.com/en/docs/claude-code)

## Installation

**Per-project** (recommended — ships with the repo):

```sh
cd your-unity-project
mkdir -p .claude/skills
cp -r /path/to/odin-inspector-claude-skill/odin-visual-designer .claude/skills/
```

**Global** (available in every project):

```sh
mkdir -p ~/.claude/skills
cp -r /path/to/odin-inspector-claude-skill/odin-visual-designer ~/.claude/skills/
```

The skill activates automatically when you mention inspector-related keywords (inspector, button, group, improve, layout, tab, foldout…) or a class name in Claude Code.

## Optional: Make It the Project Default

Add a `CLAUDE.md` at your Unity project root so every request is routed through the skill:

```markdown
# My Unity Project

All requests about inspectors, scripts, layout, fields, buttons, groups, or
"making things look better" should be handled through the `odin-visual-designer`
skill. Do not add C# attributes to source files — always use OVDF files.
```

## How It Works

The skill is a single Markdown file (`SKILL.md`) plus two reference docs:

- `odin-visual-designer/SKILL.md` — entry point, default aesthetic, procedure, crash traps
- `odin-visual-designer/references/ovdf-format.md` — OVDF v1.1 file format spec
- `odin-visual-designer/references/attributes.md` — catalog of supported Odin attributes and their OVDF-safe parameters

Claude reads these on demand when the skill triggers.

## Video

Walkthrough of creating and using this skill: https://youtu.be/tNiGgmP6hFY

## License

[The Unlicense](LICENSE) — public domain. Do whatever you want with it.
