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
