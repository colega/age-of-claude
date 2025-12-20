# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Age of Claude is a Claude Code plugin marketplace containing a single plugin that plays Age of Empires II sound effects during Claude Code lifecycle events.

## Repository Structure

```
.claude-plugin/marketplace.json    # Marketplace manifest
age-of-claude-plugin/              # The actual plugin
├── .claude-plugin/plugin.json     # Plugin manifest
├── hooks/
│   ├── hooks.json                 # Hook event registration
│   ├── entrypoints/               # Ruby scripts called by Claude Code
│   ├── handlers/                  # Business logic classes
│   └── lib/sound_player.rb        # Cross-platform audio playback
├── lib/sound_config.rb            # Shared config reader
└── vendor/
    ├── claude_hooks/              # Vendored Ruby DSL for hooks
    └── sounds/                    # 46 AoE II .wav files
```

## Architecture

**Hook Flow:** Claude Code → entrypoint.rb → Handler class → SoundPlayer → afplay

Each hook event (SessionStart, Notification, Stop, SessionEnd) has:
1. **Entrypoint** (`hooks/entrypoints/*.rb`): Parses JSON from stdin, instantiates handler, calls `output_and_exit`
2. **Handler** (`hooks/handlers/*_handler.rb`): Extends `ClaudeHooks::*` base class, selects sound, calls `SoundPlayer.play`
3. **SoundPlayer** (`hooks/lib/sound_player.rb`): Resolves paths, checks config, executes platform-specific play command

**Sound Selection:**
- Handlers use either deterministic mapping (notification type → specific sound) or `play_random` for variety
- Sounds only play when `~/.config/claude/sounds.conf` contains `SOUND_MODE=aoe`

## Testing Hooks Locally

```bash
# Test a specific hook with sample input
echo '{"session_id":"test","hook_event_name":"Notification","message":"test","notification_type":"permission_prompt"}' | \
  CLAUDE_PLUGIN_ROOT=$(pwd)/age-of-claude-plugin \
  ruby age-of-claude-plugin/hooks/entrypoints/notification.rb

# Enable debug output
RUBY_CLAUDE_HOOKS_DEBUG=1 ruby ...

# Force sounds to play (bypasses config check)
echo "SOUND_MODE=aoe" > ~/.config/claude/sounds.conf
```

## Key Configuration

- **Sound mode config:** `~/.config/claude/sounds.conf` with `SOUND_MODE=aoe|glass|off`
- **Disable sounds env vars:** `CLAUDE_DISABLE_SOUNDS=1` or `SIMPLE_CLAUDE_DISABLE_SOUNDS=1`
- **Plugin root:** `CLAUDE_PLUGIN_ROOT` env var set by Claude Code at runtime

## Vendored Dependencies

The `claude_hooks` gem is vendored at `vendor/claude_hooks/` - no gem installation required. This is necessary because Claude Code's plugin cache copies plugins individually, breaking shared dependencies.
