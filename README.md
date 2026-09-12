# alantushenko — Claude Code Skill

A personal [Claude Code](https://claude.com/claude-code) skill with Alex Lantushenko's coding style and conventions. Claude applies it automatically whenever it writes or edits code.

See [SKILL.md](SKILL.md) for the full conventions.

## Installation

Clone the repo and symlink `SKILL.md` into your Claude Code skills directory:

```bash
git clone git@github.com:lantushenko-alex/claude-skill.git
mkdir -p ~/.claude/skills/alantushenko
ln -sf "$(pwd)/claude-skill/SKILL.md" ~/.claude/skills/alantushenko/SKILL.md
```

The symlink keeps the installed skill in sync with the repo — edit or pull in the repo and changes take effect immediately.

If you want to load this skill in all your claude sessions - add it into ~/CLAUDE.md

## Design skill

The `design/` folder holds `alantushenko-design`, the user interface design rules (buttons, forms, controls). Claude applies it when it designs, builds, or reviews user interface elements.

### Enable the design skill

Run this from the root of the cloned repository:

```bash
mkdir -p ~/.claude/skills/alantushenko-design
ln -sf "$(pwd)/design/SKILL.md" ~/.claude/skills/alantushenko-design/SKILL.md
```

Start a new Claude Code session. Claude picks the skill when your request matches its description, and you can call it directly with `/alantushenko-design`.

## SDLC skills

The `sdlc/` folder holds three skills based on the [AI-Native SDLC Playbook](https://academy.claude.com/courses/ai-native-sdlc-playbook). Each one writes one artifact of the chain `intent.md` → `spec.md` → `plan.md`, and PR review later checks the diff against the spec and the plan.

| Skill | Stage | Writes | Input |
|---|---|---|---|
| `sdlc-intent` | Plan | `intent.md` | a brainstorm, ticket, or incident |
| `sdlc-spec` | Design | `spec.md` | approved `intent.md` |
| `sdlc-plan` | Build | `plan.md` | approved `spec.md`, run in plan mode |

By default each feature has one folder, `features/<feature-slug>/`, in the product repository. The three files live there together with everything else about the feature: mockups, decisions, notes.

### Enable the SDLC skills

Run this from the root of the cloned repository. It creates one symlink per skill in your Claude Code skills directory:

```bash
for skill in intent spec plan; do
  mkdir -p ~/.claude/skills/sdlc-$skill
  ln -sf "$(pwd)/sdlc/$skill/SKILL.md" ~/.claude/skills/sdlc-$skill/SKILL.md
done
```

Check the result:

```bash
ls -l ~/.claude/skills/sdlc-*/SKILL.md
```

Start a new Claude Code session. The skills load on demand: Claude picks `sdlc-intent`, `sdlc-spec`, or `sdlc-plan` when your request matches its description, and you can call one directly with `/sdlc-intent`, `/sdlc-spec`, or `/sdlc-plan`. Because the files are symlinks, pulling the repo updates the installed skills immediately.

To disable a skill, remove its folder from `~/.claude/skills/`.
