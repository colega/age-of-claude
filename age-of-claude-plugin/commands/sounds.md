---
description: Toggle Age of Empires sounds on or off
argument-hint: "[on|off]"
allowed-tools: ["Bash", "Read", "Write"]
---

# Age of Claude Sound Control

Toggle Age of Empires II sound effects for Claude Code events.

Config file: `~/.config/claude/sounds.conf`

$ARGUMENTS

## Instructions

1. First, read current state: `cat ~/.config/claude/sounds.conf 2>/dev/null || echo "(not set - sounds disabled)"`

2. If argument provided:
   - `on` → Write `SOUND_MODE=aoe` to config file
   - `off` → Write `SOUND_MODE=off` to config file
   - Create `~/.config/claude` directory if needed

3. If no argument, just report current state.

Example responses:
- "Age of Empires sounds enabled - wololo!"
- "Age of Empires sounds disabled"
- "Current: sounds are enabled (SOUND_MODE=aoe)"
- "Current: sounds are disabled (SOUND_MODE=off)"
