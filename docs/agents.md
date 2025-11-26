# Agents Documentation - ABOV3: Genesis CodeForger
Configure specialized AI agents with specific tools, permissions, and behaviors in ABOV3.

Built-in Agents
---------------

###  Build Agent

**Type:** Primary Agent (default)

**Purpose:** Code generation, implementation, and technical tasks

**Best for:** Writing code, fixing bugs, implementing features, refactoring

✅ bash ✅ edit ✅ write ✅ read ✅ grep ✅ glob

###  Plan Agent

**Type:** Primary Agent

**Purpose:** Architecture, design, and planning tasks

**Best for:** System design, planning implementations, code reviews

❌ bash ❌ edit ❌ write ✅ read ✅ grep ✅ glob

###  General Agent

**Type:** Subagent

**Purpose:** General questions, explanations, and non-coding tasks

**Best for:** Explanations, documentation, general Q&A

❌ bash ❌ edit ❌ write ✅ read ✅ webfetch

Agent Configuration
-------------------

### Configuration Methods

1.  **JSON Configuration** - In `~/.config/abov3/abov3.json`
2.  **Markdown Files** - In `~/.config/abov3/agent/*.md`
3.  **Project-specific** - In `.abov3/agent/*.md`

### Configuration Options


|Option     |Type   |Description                          |Example                  |
|-----------|-------|-------------------------------------|-------------------------|
|description|string |Brief explanation of agent's purpose |"Handles security audits"|
|mode       |string |Agent type: primary, subagent, or all|"subagent"               |
|model      |string |Override default model               |"anthropic/claude-3-opus"|
|temperature|number |Response randomness (0.0-1.0)        |0.7                      |
|prompt     |string |Custom system prompt file            |"security-prompt.md"     |
|tools      |object |Enable/disable specific tools        |{"bash": false}          |
|permission |object |Tool permission levels               |{"edit": "ask"}          |
|disable    |boolean|Disable the agent                    |false                    |


Creating Custom Agents
----------------------

### Method 1: Markdown Configuration

Create a file in `~/.config/abov3/agent/security.md`:

```
---
description: Security audit specialist
mode: subagent
temperature: 0.3
tools:
  bash: false
  write: false
  edit: false
permission:
  read: allow
  webfetch: ask
---

You are a security expert specializing in code audits and vulnerability detection.

Focus on:
- Identifying security vulnerabilities
- Checking for exposed credentials
- Finding SQL injection risks
- Detecting XSS vulnerabilities
- Reviewing authentication flows

Always provide CVE references when applicable.
```


### Method 2: JSON Configuration

Add to `~/.config/abov3/abov3.json`:

```
{
  "agent": {
    "debugger": {
      "description": "Specialized debugging assistant",
      "mode": "primary",
      "model": "anthropic/claude-3-sonnet",
      "temperature": 0.5,
      "tools": {
        "bash": true,
        "read": true,
        "grep": true,
        "edit": false
      },
      "permission": {
        "bash": "ask"
      }
    }
  }
}
```


Tools and Permissions
---------------------

### Available Tools

#### File Operations

*   `read` - Read file contents
*   `write` - Create new files
*   `edit` - Modify existing files
*   `patch` - Apply patches
*   `glob` - Find files by pattern
*   `grep` - Search file contents
*   `list` - List directory contents

#### Other Tools

*   `bash` - Execute shell commands
*   `webfetch` - Fetch web content
*   `todowrite` - Manage task lists
*   `todoread` - Read task lists

### Permission Levels

*   `allow` - No restrictions, tool can be used freely
*   `ask` - Requires user confirmation before each use
*   `deny` - Tool is completely disabled

####  Security Best Practice

Set `bash: "ask"` for agents that don't need frequent shell access. This prevents unintended command execution.

Example Agents
--------------

###  Documentation Writer

```
---
description: Technical documentation specialist
mode: subagent
tools:
  bash: false
  edit: true
  write: true
---

You are a technical writer. Create clear, comprehensive documentation
following industry best practices. Use proper markdown formatting.
```


### 離 Test Generator

```
---
description: Unit test and integration test creator
mode: subagent
model: anthropic/claude-3-opus
tools:
  write: true
  read: true
  bash: true
permission:
  bash: ask
---

You specialize in creating comprehensive test suites.
Always aim for high code coverage and edge case handling.
```


###  Code Reviewer

```
---
description: Code review and best practices enforcer
mode: subagent
temperature: 0.3
tools:
  read: true
  grep: true
  edit: false
  write: false
---

You are a senior developer conducting code reviews.
Focus on code quality, performance, security, and maintainability.
```


Using Agents
------------

### In TUI

*   Switch agents with `Tab` / `Shift+Tab`
*   View available agents with `/agents`
*   Mention subagents with `@agent-name`

### In CLI

```
# Use specific agent
./abov3-linux-x64 run --agent debugger "Find the bug in this code"

# List available agents
./abov3-linux-x64 agent list
```


### Interactive Creation

```
# Create new agent interactively
./abov3-linux-x64 agent create
```


###  Agent Selection Strategy

*   **Build Agent** - When you need to write or modify code
*   **Plan Agent** - For architecture decisions and code reviews
*   **General Agent** - For explanations and documentation
*   **Custom Agents** - For specialized tasks in your workflow