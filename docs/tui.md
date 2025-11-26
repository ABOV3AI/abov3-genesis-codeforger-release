# TUI Documentation - ABOV3: Genesis CodeForger
Terminal User Interface (TUI)
-----------------------------

The interactive terminal interface for ABOV3 with auto-completion, syntax highlighting, and real-time streaming responses.

###  Key Features

*   **Zero Configuration** - Automatically starts and manages embedded server
*   **Beautiful Interface** - Syntax highlighting and formatted output
*   **Keyboard Shortcuts** - Vim-like keybindings for power users
*   **Multi-line Editing** - Full text editor capabilities
*   **Session Management** - Continue conversations across sessions
*   **Real-time Streaming** - See responses as they're generated

Starting the TUI
----------------

```
# Linux
./abov3-tui-linux-x64

# macOS Intel
./abov3-tui-darwin-x64

# macOS Apple Silicon
./abov3-tui-darwin-arm64

# Windows
.\abov3-tui-windows-x64.exe
```


The TUI automatically:

1.  Finds an available port
2.  Starts the embedded ABOV3 server
3.  Connects to the server
4.  Cleans up when you exit

Slash Commands
--------------

Type these commands in the chat input to access features quickly:

### Configuration Commands

| Command | Description  |
|------------|------------------------------------------------------------------------|
| /config | Open the configuration menu |
| /config show | Display current configuration settings |
| /config doctor | Run system health check and diagnostics |
| /config validate | Validate your configuration file |
| /config provider:list | List all configured AI providers | 
| /config provider:add | Add a new AI provider |
| /config provider:edit | Edit, enable, or disable providers |
| /config mcp:list | List Model Context Protocol servers
| /config mcp:add | Add a new MCP server |
| /config mcp:edit | Edit or manage MCP servers |

### Session Management

| Command | Description  |
|------------|------------------------------------------------------------------------|
| /new | Start a new chat session |
| /sessions | View and switch between sessions |
| /clear | Clear the current conversation | 

### Other Commands

| Command | Description  |
|------------|------------------------------------------------------------------------|
| /help | Show all available commands and shortcuts | 
| /models | List all available AI models |
| /agents | Manage AI agents (Build, Plan, General) |
| /exit or /quit | Exit the TUI (also cleans up server) |

Keyboard Shortcuts
------------------

ABOV3 TUI uses a leader key system (default: ctrl+x) for commands:


|Category               |Shortcut                  |Action                 |
|-----------------------|--------------------------|-----------------------|
|Application            |<leader>h                 |Show help dialog       |
|ctrl+c or <leader>q    |Exit the application      |                       |
|<leader>e              |Open external editor      |                       |
|Sessions               |<leader>n                 |Create new session     |
|<leader>l              |List all sessions         |                       |
|<leader>g              |Show session timeline     |                       |
|<leader>s              |Share current session     |                       |
|ctrl+right             |Next child session        |                       |
|ctrl+left              |Previous child session    |                       |
|Models & Agents        |<leader>m                 |List available models  |
|f2                     |Cycle to next recent model|                       |
|<leader>a              |List agents               |                       |
|tab / shift+tab        |Switch between agents     |                       |
|Navigation             |pgup / pgdown             |Scroll messages by page|
|ctrl+alt+u / ctrl+alt+d|Scroll by half page       |                       |
|ctrl+g                 |Go to first message       |                       |
|ctrl+alt+g             |Go to last message        |                       |
|<leader>y              |Copy message              |                       |
|<leader>u              |Undo last message         |                       |
|<leader>r              |Redo message              |                       |
|<leader>c              |Compact the session       |                       |
|esc                    |Interrupt current session |                       |
|Input                  |enter                     |Submit prompt          |
|shift+enter or ctrl+j  |Insert newline            |                       |
|ctrl+v                 |Paste from clipboard      |                       |
|ctrl+c                 |Clear input field         |                       |
|View                   |<leader>t                 |List available themes  |
|<leader>d              |Toggle tool details       |                       |
|<leader>b              |Toggle thinking blocks    |                       |


####  Leader Key

The leader key is ctrl+x by default. Press it, then press the second key. For example, <leader>h means press ctrl+x then h.

Interface Features
------------------

### Chat Interface

*   **Syntax Highlighting** - Code blocks are automatically highlighted
*   **Markdown Rendering** - Proper formatting for lists, headers, etc.
*   **Streaming Responses** - See AI responses as they're generated
*   **Multi-line Input** - Use Shift+Enter for multi-line prompts
*   **Copy Code** - Easy code block copying

### Model Selection

*   Quick switch with /models command
*   Recent models accessible with F2
*   Shows token usage and costs
*   Automatic Ollama model detection

### Session Management

*   Automatic session persistence
*   Continue previous conversations
*   Branch conversations (child sessions)
*   Export sessions as JSON
*   Share sessions with others

Tips and Tricks
---------------

####  Quick Model Switching

Use F2 to quickly cycle through your recently used models without opening the model selector.

####  Multi-line Input

For complex prompts, use Shift+Enter to add new lines. This is perfect for pasting code snippets or writing detailed instructions.

####  Agent Switching

Quickly switch between Build and Plan agents using Tab. Build agent is optimized for code generation, while Plan agent excels at architecture and design.

####  Session Branching

Create child sessions with Ctrl+Right to explore different approaches without losing your main conversation thread.

#### ⚡ Custom Commands

Create your own slash commands by adding them to `~/.config/abov3/command/`. They'll appear automatically in the TUI.

Configuration
-------------

The TUI respects all settings in your ABOV3 configuration:

```
# Main config file
~/.config/abov3/abov3.json

# Custom keybindings example:
{
  "keybinds": {
    "leader": "ctrl+a",     // Change leader key
    "app_exit": "ctrl+q",   // Custom exit shortcut
    "session_new": "alt+n"  // Custom new session
  }
}
```


Troubleshooting
---------------

### TUI won't start

*   Ensure the binary has execute permissions: `chmod +x abov3-tui-linux-x64`
*   Check if port is available (TUI auto-finds free ports)
*   Run with debug logging: `LOG_LEVEL=DEBUG ./abov3-tui-linux-x64`

### Models not showing

*   Check provider authentication: `/config provider:list`
*   For Ollama, ensure it's running: `ollama serve`
*   Verify API keys in configuration

### Keyboard shortcuts not working

*   Some terminal emulators may intercept certain key combinations
*   Try customizing keybindings in config
*   Use slash commands as alternatives