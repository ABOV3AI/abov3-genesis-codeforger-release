# CLI Documentation - ABOV3: Genesis CodeForger
Command Line Interface (CLI)
----------------------------

ABOV3's powerful command-line interface for automation, scripting, and headless operation.

```
█▀▀█ █▀▀▄ █▀▀█ █  █ ▀▀█ █▀▀█ ▀█▀
█▄▄█ █▀▀▄ █░░█ █  █ ▀▀█ █▄▄█ ░█░
▀  ▀ ▀▀▀  ▀▀▀▀  ▀▀  ▀▀▀ ▀  ▀ ▄█▄
```

** Commands:
| Command    | Descripton |
|------------|------------|
| abov3 [project] | start abov3 tui   [default] |
| abov3 run [message..] | run abov3 with a message.  Example: `abov3 run "Explain async/await in JavaScript"` |
| abov3 auth | manage credentials |
| abov3 config | manage ABOV3 configuration |
| abov3 agent  | manage agents |
| abov3 upgrade [target] | upgrade abov3 to the latest or a specific version |
| abov3 serve | starts a headless abov3 server |
| abov3 models | list all available models |
| abov3 export [sessionID] | export session data as JSON |
| abov3 github | manage GitHub agent |
| abov3 prompts | manage named prompts |
| abov3 prompts:add | add a new named prompt |
| abov3 prompts:list | list all named prompts |
| abov3 prompts:use <name> | use a named prompt (sends it to the LLM) |
| abov3 list-prompts | list all named prompts |
| abov3 recover-context | recover compressed context from backups |
| abov3 prompts:add | add a new named prompt |
| abov3 prompts:list | list all named prompts |
| abov3 prompts:use <name> | use a named prompt (sends it to the LLM) |
| abov3 list-prompts | list all named prompts |
| abov3 recover-context | recover compressed context from backups |

```
Options:
      --help        show help                                          [boolean]
  -v, --version     show version number                                [boolean]
      --print-logs  print logs to stderr                               [boolean]
      --log-level   log level
                            [string] [choices: "DEBUG", "INFO", "WARN", "ERROR"]
  -m, --model       model to use in the format of provider/model        [string]
  -c, --continue    continue the last session                          [boolean]
  -s, --session     session id to continue                              [string]
  -p, --prompt      prompt to use                                       [string]
      --agent       agent to use                                        [string]
      --port        port to listen on                      [number] [default: 0]
  -h, --hostname    hostname to listen on        [string] [default: "127.0.0.1"]
```

Linux:
`~/.cache/abov3/bin/abov3-cli {opts}`


# Continue last session
`abov3 --continue`


 Self-Management Commands
-------------------------------------------

ABOV3 includes built-in commands to manage its own installation. All functionality is compiled into the single binary - no external scripts needed!

### abov3 install

Install ABOV3 to your system PATH automatically. Configures PATH based on your platform.

```
# Linux/macOS
./abov3 install

# Windows
.\abov3.exe install

# After installation, abov3 is available from anywhere
abov3 --version
```


#### ✨ What this does:

*   **Linux/macOS:** Copies to `~/.local/bin/` and updates shell config
*   **Windows:** Copies to `%LocalAppData%\Programs\ABOV3\` and updates registry PATH

### abov3 update

Check for and install the latest version from GitHub releases. Performs atomic binary replacement with automatic rollback on failure.

```
# Check for updates and install
abov3 update

# Shows:
# - Current version
# - Latest available version
# - Changelog highlights
# - Download progress
# - Installation status
```


#### Example Output:

```
🚀 Installing ABOV3 Genesis CodeForger...

📦 Installing to: C:\Users\russe\AppData\Local\Programs\ABOV3\abov3.exe
✓ Binary installed
📦 Extracting embedded CLI...
Updating embedded CLI: XXXXXXX\AppData\Local\abov3\bin\abov3-cli.exe
Embedded CLI extracted successfully: XXXXXXX\AppData\Local\abov3\bin\abov3-cli.exe (size: 129467904)
✓ CLI extracted to: XXXXXXX\AppData\Local\abov3\bin\abov3-cli.exe
✓ Already in PATH

✨ Installation complete!

🎯 Quick start:
   1. Run: abov3
   2. Start chatting with AI!

📚 Common commands:
   abov3 auth login   - Authenticate with providers
   abov3 models       - List available AI models
   abov3 update       - Update to latest version
   abov3 uninstall    - Remove installation

📍 Installed to: XXXXXXX\AppData\Local\Programs\ABOV3\abov3.exe
```


### abov3 uninstall

Remove ABOV3 from your system, including binary and PATH configuration.

```
# Remove ABOV3
abov3 uninstall

# Cleans up:
# - Binary file
# - PATH configuration
# - Shell config entries (Linux/macOS)
# - Registry entries (Windows)
```


Main Commands
-------------

### abov3 \[project\]

Start ABOV3 Terminal User Interface (TUI). This is the default command when no arguments are provided.

```
# Start TUI in current directory
abov3

# Start TUI in specific project directory
abov3 /path/to/project
```


### abov3 run \[message..\]

Run ABOV3 with a single message or prompt. Useful for one-off queries or automation.

```
# Ask a question
abov3 run "What is the difference between let and const?"

# Request code generation
abov3 run "Create a REST API with Express.js"

# With specific model
abov3 run -m anthropic/claude-3-opus "Optimize this function"
```


### abov3 auth

Manage authentication and credentials for AI providers.

```
# Login to a provider (supports Anthropic OAuth)
abov3 auth login

# List configured providers
abov3 auth list

# Logout from a provider
abov3 auth logout
```


####  Anthropic OAuth

ABOV3 supports OAuth login for Anthropic Claude Pro/Max accounts. Run `auth login` to authenticate with your Claude account.

[Example](example_auth.md)

### abov3 serve

Start a headless ABOV3 server. Useful for running ABOV3 as a backend service.

```
# Start server on default port
abov3 serve

# Start on specific port
abov3 serve --port 4096

# Specify hostname and port
abov3 serve --hostname 0.0.0.0 --port 8080
```


### abov3 models

List all available AI models from configured providers.

```
# List all models
abov3 models

# Shows models from:
# - Anthropic (Claude models)
# - OpenAI (GPT models)
# - Ollama (local models)
# - Other configured providers
```


####  Ollama Continuous Monitoring (New in v0.1.8)

ABOV3 now continuously monitors Ollama every 30 seconds. Models automatically appear when Ollama starts and disappear when it stops. No manual refresh needed!

### abov3 config

Manage ABOV3 configuration settings.

```
# Open configuration menu
above config

# Configuration is stored in:
# ~/.config/abov3/abov3.json
```


### abov3 agent

Manage AI agents (Build, Plan, General, and custom agents).

```
# Manage agents
abov3-cli agent

# Agents are configured in:
# ~/.config/abov3/agent/
```


### abov3 export \[sessionID\]

Export session data as JSON for backup or analysis.

```
# Export current session
abov3-cli export

# Export specific session
abov3-cli export session_12345
```


### abov3 upgrade \[target\]

Upgrade ABOV3 to the latest version or a specific version.

```
# Upgrade to latest
abov3-cli upgrade

# Upgrade to specific version
abov3-cli upgrade v1.2.3
```


Global Options
--------------


|Option      |Short|Description                             |Example                   |
|------------|-----|----------------------------------------|--------------------------|
|--model     |-m   |Specify the AI model to use             |-m anthropic/claude-3-opus|
|--continue  |-c   |Continue the last session               |./abov3 -c                |
|--session   |-s   |Continue a specific session by ID       |-s session_123            |
|--agent     |     |Specify which agent to use              |--agent build             |
|--prompt    |-p   |Provide initial prompt                  |-p "Help me debug this"   |
|--port      |     |Port for server mode                    |--port 4096               |
|--hostname  |-h   |Hostname for server mode                |-h 127.0.0.1              |
|--print-logs|     |Print logs to stderr                    |--print-logs              |
|--log-level |     |Set log level (DEBUG, INFO, WARN, ERROR)|--log-level DEBUG         |
|--version   |-v   |Show version number                     |./abov3 -v                |
|--help      |     |Show help information                   |./abov3 --help            |


Common Workflows
----------------

#### Quick Code Generation

```
# Generate a Python function
abov3-cli run "Create a Python function to parse CSV files"

# Generate with specific model
abov3-cli run -m ollama/qwen2.5-coder:14b "Create a REST API"
```


#### Continuous Development Session

```
# Start a new session with a specific model
abov3-cli -m anthropic/claude-3-sonnet

# Continue your last session
abov3-cli --continue

# Continue a specific session
abov3-cli --session session_20240315_142350
```


#### Using Local Models with Ollama

```
# First, ensure Ollama is running
ollama serve

# List available models (including Ollama)
abov3-cli models

# Use a local Ollama model
abov3-cli run -m ollama/mistral:7b "Explain closures"
```


#### Debugging and Troubleshooting

```
# Enable debug logging
./abov3 --log-level DEBUG --print-logs

# Check provider authentication
./abov3 auth list

# Test with a simple prompt
./abov3 run --print-logs "Hello, are you working?"
```


Environment Variables
---------------------

```
# Set default model
export ABOV3_MODEL="anthropic/claude-3-opus"

# Set Ollama base URL (if not localhost)
export OLLAMA_BASE_URL="http://192.168.1.100:11434"

# Enable debug logging
export LOG_LEVEL="DEBUG"

# Set config directory
export ABOV3_CONFIG_DIR="$HOME/.config/abov3"
```


Configuration Files
-------------------

ABOV3 uses the following configuration files:

*   `~/.config/abov3/abov3.json` - Main configuration
*   `~/.config/abov3/agent/*.md` - Agent configurations
*   `~/.config/abov3/command/*.md` - Custom commands
*   `~/.local/share/abov3/auth.json` - Authentication tokens
*   `.abov3/` - Project-specific configuration

####  Pro Tips

*   Use `--continue` to resume your last conversation without losing context
*   The TUI (`abov3-tui`) provides a better interactive experience than CLI
*   Combine with shell scripts for powerful automation workflows
*   Use `--print-logs` when debugging issues
*   Local Ollama models work offline and have no API costs