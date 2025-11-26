# Named Prompts System

Save and reuse frequently used prompts:
- **Create custom prompts** with name and instructions
- **List all saved prompts** in interactive dialog
- **Quick prompt execution** via `/prompts:use`
- **Persistent storage** in `~/.config/abov3/prompts.json`
- **Cross-platform support**: Windows, macOS, Linux
- **Use cases**: Code review, documentation, refactoring, testing

### Prompt Management

The following commands are used to access the named prompts section.

- `/prompts` - Show prompt management menu
- `/prompts:add` - Create new named prompt
- `/prompts:list` - List all saved prompts
- `/prompts:use <name>` - Use saved prompt in current session

The named prompts are stored in the ~/.config/abov3/prompts.json.  You may find it more convenient to edit the JSON for complex prompts.

The prompt is loaded into the prompt window, but not executed so it can be modified if necessary.
