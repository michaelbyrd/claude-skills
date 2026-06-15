# claude-skills

Personal [Claude Code](https://claude.ai/code) skills.

## Skills

| Skill | Trigger | Description |
|-------|---------|-------------|
| `diagram` | `/diagram` | Renders diagrams as ASCII art, or generates Excalidraw-compatible prose descriptions |
| `refresh` | `/refresh` | Syncs Claude's knowledge of files after manual edits |
| `ruby-init` | `/ruby-init` | Scaffolds a new Ruby project with RSpec, RuboCop, and Pry |
| `ruby-new-class` | `/ruby-new-class` | Scaffolds a Ruby class and spec file from a class name |
| `ruby-new-module` | `/ruby-new-module` | Scaffolds a Ruby module and spec file from a module name |

## External Skills

Skills I use but didn't author — install from their source repos:

| Skill | Source |
|-------|--------|
| `grill-me` | [mattpocock/skills](https://github.com/mattpocock/skills) |
| `handoff` | [mattpocock/skills](https://github.com/mattpocock/skills) |
| `teach` | [mattpocock/skills](https://github.com/mattpocock/skills) |

### Plugins

| Plugin | Install | Description |
|--------|---------|-------------|
| superpowers | `/plugin install superpowers@claude-plugins-official` | Structured agentic workflow: TDD, brainstorming, debugging, code review ([obra/superpowers](https://github.com/obra/superpowers)) |

## Usage

Skills live in `~/.claude/skills/` and are picked up automatically by Claude Code. To install:

```bash
git clone https://github.com/michaelbyrd/claude-skills ~/.claude/skills
```

> If you already have skills in `~/.claude/skills/`, clone somewhere else and copy the folders you want.
