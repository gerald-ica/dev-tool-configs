# Dev Tool Configs

Configuration files for development tools, synced across machines.

## Tools Included

| Directory | Tool | What's Included |
|-----------|------|-----------------|
| `cursor/` | [Cursor](https://cursor.com) | Settings, MCP config, hooks, extensions list |
| `antigravity/` | [Antigravity](https://antigravity.dev) | Settings, extensions list |
| `gemini/` | [Gemini CLI](https://github.com/google-gemini/gemini-cli) | Settings, agents, commands, hooks, rules, skills |
| `qwen/` | [Qwen CLI](https://github.com/QwenLM/qwen-code) | Settings, agents, commands, rules |
| `pencil/` | [Pencil.dev](https://pencil.dev) | App config |
| `sketch/` | [Sketch](https://sketch.com) | Presets |
| `xcode/` | [Xcode](https://developer.apple.com/xcode/) | Themes, key bindings, snippets |

## Setup

1. Clone this repo
2. Copy configs to their respective locations:

```bash
# Cursor
cp cursor/argv.json ~/.cursor/
cp cursor/mcp.json ~/.cursor/
cp cursor/hooks.json ~/.cursor/
cp cursor/user-settings.json ~/Library/Application\ Support/Cursor/User/settings.json

# Antigravity
cp antigravity/argv.json ~/.antigravity/
cp antigravity/user-settings.json ~/Library/Application\ Support/Antigravity/User/settings.json

# Gemini CLI
cp -r gemini/* ~/.gemini/

# Qwen CLI
cp -r qwen/* ~/.qwen/

# Pencil.dev
cp pencil/config.json ~/Library/Application\ Support/Pencil/

# Sketch
cp sketch/*.sketchpreset ~/Library/Application\ Support/com.bohemiancoding.sketch3/
```

3. Replace `YOUR_*` placeholders in settings files with your actual API keys.

## Secrets

API keys and tokens have been replaced with `YOUR_*` placeholders. Update these after cloning:

- `YOUR_BRIGHTDATA_TOKEN` - BrightData MCP token
- `YOUR_OPENROUTER_API_KEY` - OpenRouter API key
- `YOUR_OPENAI_API_KEY` - OpenAI API key
- `YOUR_ANTHROPIC_API_KEY` - Anthropic API key
- `YOUR_RUNWARE_API_KEY` - Runware API key
- `YOUR_BAILIAN_API_KEY` - Alibaba Bailian API key
- `YOUR_API_KEY` - Semgrep API key
