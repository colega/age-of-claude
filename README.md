# Age of Claude

Age of Empires sound effects for Claude Code events. Wololo your way through coding sessions.

## Installation

```bash
# Add the marketplace
claude plugin marketplace add https://github.com/kylesnowschwartz/age-of-claude

# Install the plugin
claude plugin install age-of-claude
```

Or from within Claude Code:

```bash
/plugin marketplace add https://github.com/kylesnowschwartz/age-of-claude
/plugin install age-of-claude
```

## What It Does

Plays Age of Empires II sound effects during Claude Code events:

| Event | Sounds |
|-------|--------|
| **Session Start** | Villager select sounds, "Start the game already!" |
| **Notification** | Priest wololo, "Hey I'm in your town!" |
| **Stop** | Villager work sounds, "I just got some satisfaction" |
| **Session End** | Soldier death sounds, crowd wailing |

46 authentic AoE II sound files included.

## Configuration

If you're also using `sc-hooks` from SimpleClaude, you can switch between sound modes:

```bash
# Age of Empires sounds (this plugin)
/sc-hooks:sc-sounds aoe

# macOS notification sounds (sc-hooks)
/sc-hooks:sc-sounds glass

# Disable all sounds
/sc-hooks:sc-sounds off
```

Config file: `~/.config/claude/sounds.conf`

## Requirements

- macOS (uses `afplay` for audio playback)
- Ruby (for hook execution)

## License

MIT
