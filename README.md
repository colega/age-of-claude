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

## Enabling Sounds

Sounds are disabled by default. Use the included command to toggle:

```bash
/age-of-claude:sounds on    # Enable AoE sounds
/age-of-claude:sounds off   # Disable sounds
/age-of-claude:sounds       # Check current state
```

Or manually:

```bash
mkdir -p ~/.config/claude
echo "SOUND_MODE=aoe" > ~/.config/claude/sounds.conf
```

## Requirements

- macOS (uses `afplay` for audio playback)
- Ruby (for hook execution)

## Acknowledgments

Inspired by [aliparoya/age-of-claude](https://github.com/aliparoya/age-of-claude).

## License

MIT
