# Custom Commands Documentation - ABOV3: Genesis CodeForger
Create powerful slash commands with templates, dynamic arguments, and shell integration.

### ⚡ Quick Start

Custom commands appear as slash commands in the TUI. Type `/yourcommand` to execute them.

*   Store in `~/.config/abov3/command/` as `.md` files
*   Or configure in `~/.config/abov3/abov3.json`
*   Project-specific commands in `.abov3/command/`

Creating Commands
-----------------

### Method 1: Markdown Files

Create `~/.config/abov3/command/test.md`:

```
---
description: Run tests with coverage
agent: build
model: anthropic/claude-3-sonnet
---

Run the full test suite with coverage reporting.
Show any failing tests and suggest fixes.

$ARGUMENTS
```


Use in TUI: `/test unit tests for auth module`

### Method 2: JSON Configuration

Add to `~/.config/abov3/abov3.json`:

```
{
  "command": {
    "review": {
      "template": "Review this code for best practices:\n$ARGUMENTS",
      "description": "Code review assistant",
      "agent": "plan",
      "model": "anthropic/claude-3-opus"
    },
    "optimize": {
      "template": "Optimize this code for performance:\n$ARGUMENTS",
      "description": "Performance optimizer"
    }
  }
}
```


Command Configuration Options
-----------------------------


|Option     |Type   |Required|Description                              |
|-----------|-------|--------|-----------------------------------------|
|template   |string |✅ Yes   |The prompt template sent to the AI       |
|description|string |❌ No    |Brief explanation shown in help          |
|agent      |string |❌ No    |Specific agent to use (build, plan, etc.)|
|model      |string |❌ No    |Override default model                   |
|subtask    |boolean|❌ No    |Force execution as subagent              |


Template Features
-----------------

### Dynamic Variables

### $ARGUMENTS

Placeholder for user-provided arguments

```
---
template: |
  Debug this error:
  $ARGUMENTS
---
```


Usage: `/debug TypeError: Cannot read property 'x' of undefined`

### Shell Command Integration

### \`command\` - Shell Output

Execute shell commands and include output in prompt

```
---
template: |
  Analyze the current git status:
  `git status`

  Recent commits:
  `git log --oneline -5`

  $ARGUMENTS
---
```


### File Content Inclusion

### @filename - File Contents

Include file contents directly in the prompt

```
---
template: |
  Review this configuration:
  @package.json

  Check for:
  $ARGUMENTS
---
```


Example Commands
----------------

### /deploy

```
---
description: Deploy application to production
agent: build
model: anthropic/claude-3-opus
---

Deploy the application following these steps:
1. Run tests: `npm test`
2. Build: `npm run build`
3. Check deployment config: @deploy.config.js

$ARGUMENTS

Ensure all tests pass before deployment.
```


### /security

```
---
description: Security audit for current project
agent: plan
temperature: 0.3
---

Perform a security audit on:
`find . -name "*.js" -o -name "*.ts" | head -20`

Check for:
- Exposed credentials
- SQL injection vulnerabilities
- XSS risks
- Insecure dependencies: `npm audit`

$ARGUMENTS
```


### /refactor

```
---
description: Suggest refactoring improvements
agent: plan
model: anthropic/claude-3-sonnet
---

Analyze this code for refactoring opportunities:

$ARGUMENTS

Consider:
- Design patterns
- Code duplication
- Performance improvements
- Readability enhancements
- Modern JavaScript/TypeScript features
```


### /todo

```
---
description: Generate TODO list from code comments
subtask: true
---

Find all TODO comments in the codebase:
`grep -r "TODO\|FIXME\|HACK" --include="*.js" --include="*.ts"`

Organize them by:
1. Priority (FIXME > TODO > HACK)
2. File location
3. Estimated effort

$ARGUMENTS
```


Advanced Patterns
-----------------

### Conditional Logic

```
---
template: |
  Check environment: `echo $NODE_ENV`

  If production:
    - Verify backups
    - Check monitoring

  If development:
    - Enable debug mode
    - Skip optimizations

  $ARGUMENTS
---
```


### Multi-File Analysis

```
---
template: |
  Analyze the API structure:

  Routes: @src/routes/index.js
  Controllers: @src/controllers/index.js
  Models: @src/models/index.js

  Suggest improvements for: $ARGUMENTS
---
```


### Interactive Workflows

```
---
description: Create new feature
agent: build
---

Create a new feature: $ARGUMENTS

Steps:
1. Create feature branch
2. Generate boilerplate: `ls src/templates/`
3. Write tests first (TDD)
4. Implement the feature
5. Update documentation

Ask me questions if you need clarification.
```


Best Practices
--------------

####  Naming Conventions

*   Use lowercase for command names
*   Use hyphens for multi-word commands: `code-review.md`
*   Keep names short and memorable

####  Template Design

*   Be specific about expected output format
*   Include context from shell commands and files
*   Use `$ARGUMENTS` for flexibility
*   Specify agent and model for consistency

#### ⚡ Performance Tips

*   Cache expensive shell commands when possible
*   Limit file inclusions to relevant sections
*   Use `subtask: true` for quick operations
*   Choose appropriate models for task complexity

Command Discovery
-----------------

### In TUI

*   Type `/` to see all available commands
*   Use `/help` to see command descriptions
*   Tab completion works for command names

### Command Locations

Commands are loaded in this priority order:

1.  `.abov3/command/` - Project-specific
2.  `~/.config/abov3/command/` - User global
3.  `abov3.json` - Configuration file
4.  Built-in commands