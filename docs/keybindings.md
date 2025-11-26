# Keybindings - ABOV3: Genesis CodeForger
Keyboard Shortcuts & Customization
----------------------------------

Master ABOV3's keyboard shortcuts for efficient navigation and workflow acceleration. Customize keybindings to match your preferences.

###  Leader Key System

ABOV3 uses a leader key system inspired by Vim. The default leader key is ctrl+x, which you press followed by another key to trigger commands. This prevents conflicts with system shortcuts and provides a consistent command prefix.

Complete Keyboard Reference
---------------------------

All keyboard shortcuts available in the ABOV3 TUI interface:


|Category           |Shortcut               |Action                             |Context        |
|-------------------|-----------------------|-----------------------------------|---------------|
|Application Control|                       |                                   |               |
|App                |<leader>h              |Show help dialog with all shortcuts|Global         |
|App                |ctrl+c or <leader>q    |Exit the application               |Global         |
|App                |<leader>e              |Open external editor               |Input focused  |
|App                |esc                    |Interrupt current session/operation|Global         |
|Session Management |                       |                                   |               |
|Session            |<leader>n              |Create new session                 |Global         |
|Session            |<leader>l              |List all sessions                  |Global         |
|Session            |<leader>g              |Show session timeline              |Global         |
|Session            |<leader>s              |Share current session              |Global         |
|Session            |ctrl+right             |Next child session                 |Global         |
|Session            |ctrl+left              |Previous child session             |Global         |
|Session            |<leader>c              |Compact the session                |Global         |
|Models & Agents    |                       |                                   |               |
|Model              |<leader>m              |List available models              |Global         |
|Model              |f2                     |Cycle to next recent model         |Global         |
|Agent              |<leader>a              |List agents                        |Global         |
|Agent              |tab                    |Switch to next agent               |Global         |
|Agent              |shift+tab              |Switch to previous agent           |Global         |
|Navigation         |                       |                                   |               |
|Scroll             |pgup / pgdown          |Scroll messages by page            |Message area   |
|Scroll             |ctrl+alt+u / ctrl+alt+d|Scroll by half page                |Message area   |
|Jump               |ctrl+g                 |Go to first message                |Message area   |
|Jump               |ctrl+alt+g             |Go to last message                 |Message area   |
|Copy               |<leader>y              |Copy current message to clipboard  |Message focused|
|History            |<leader>u              |Undo last message                  |Global         |
|History            |<leader>r              |Redo message                       |Global         |
|Input & Editing    |                       |                                   |               |
|Submit             |enter                  |Submit prompt                      |Input focused  |
|Newline            |shift+enter or ctrl+j  |Insert newline                     |Input focused  |
|Paste              |ctrl+v                 |Paste from clipboard               |Input focused  |
|Clear              |ctrl+c                 |Clear input field                  |Input focused  |
|History            |up / down              |Navigate input history             |Input focused  |
|Word Nav           |ctrl+left / ctrl+right |Move cursor by word                |Input focused  |
|Line Nav           |home / end             |Move to start/end of line          |Input focused  |
|View & Interface   |                       |                                   |               |
|Theme              |<leader>t              |List available themes              |Global         |
|Tools              |<leader>d              |Toggle tool details visibility     |Global         |
|Thinking           |<leader>b              |Toggle thinking blocks visibility  |Global         |
|Focus              |f1                     |Focus input field                  |Global         |
|Zoom               |ctrl+plus / ctrl+minus |Increase/decrease font size        |Global         |


Customizing Keybindings
-----------------------

You can customize all keyboard shortcuts by editing your ABOV3 configuration file:

### Configuration File Location

```
# Linux/macOS
~/.config/abov3/abov3.json

# Windows
%APPDATA%\abov3\abov3.json
```


### Keybinding Configuration

```
{
  "keybinds": {
    // Leader key (default: ctrl+x)
    "leader": "ctrl+a",

    // Application shortcuts
    "app_help": "f1",
    "app_exit": "ctrl+q",
    "app_external_editor": "ctrl+e",
    "app_interrupt": "esc",

    // Session management
    "session_new": "<leader>n",
    "session_list": "<leader>l",
    "session_timeline": "<leader>g",
    "session_share": "<leader>s",
    "session_next_child": "ctrl+right",
    "session_prev_child": "ctrl+left",
    "session_compact": "<leader>c",

    // Model and agent shortcuts
    "model_list": "<leader>m",
    "model_cycle": "f2",
    "agent_list": "<leader>a",
    "agent_next": "tab",
    "agent_prev": "shift+tab",

    // Navigation shortcuts
    "nav_page_up": "pgup",
    "nav_page_down": "pgdown",
    "nav_half_up": "ctrl+alt+u",
    "nav_half_down": "ctrl+alt+d",
    "nav_first": "ctrl+g",
    "nav_last": "ctrl+alt+g",
    "nav_copy": "<leader>y",
    "nav_undo": "<leader>u",
    "nav_redo": "<leader>r",

    // Input shortcuts
    "input_submit": "enter",
    "input_newline": "shift+enter",
    "input_newline_alt": "ctrl+j",
    "input_paste": "ctrl+v",
    "input_clear": "ctrl+c",

    // View shortcuts
    "view_themes": "<leader>t",
    "view_tools": "<leader>d",
    "view_thinking": "<leader>b",
    "view_focus": "f1",
    "view_zoom_in": "ctrl+plus",
    "view_zoom_out": "ctrl+minus"
  }
}
```


Key Notation Guide
------------------


|Notation    |Meaning                     |Example                  |
|------------|----------------------------|-------------------------|
|<leader>    |Leader key (default: ctrl+x)|<leader>h = ctrl+x then h|
|ctrl+       |Control key modifier        |ctrl+c                   |
|shift+      |Shift key modifier          |shift+enter              |
|alt+        |Alt key modifier            |alt+n                    |
|plus / minus|Plus/minus keys             |ctrl+plus                |
|f1, f2, etc.|Function keys               |f2                       |
|space       |Spacebar                    |ctrl+space               |
|backspace   |Backspace key               |ctrl+backspace           |


Context-Specific Shortcuts
--------------------------

### Input Field Focused

These shortcuts only work when the input field has focus:

*   enter - Submit prompt
*   shift+enter - Add new line
*   ctrl+c - Clear input
*   up/down - Navigate input history
*   <leader>e - Open external editor

### Message Area Focused

These shortcuts work when browsing messages:

*   pgup/pgdown - Scroll by page
*   ctrl+g - Go to first message
*   ctrl+alt+g - Go to last message
*   <leader>y - Copy current message

####  Pro Tips

*   **Leader Key Timing:** Press and release the leader key, then press the command key. No need to hold both simultaneously.
*   **Terminal Compatibility:** Some terminal emulators may intercept certain key combinations. Try using alternative shortcuts or customize them.
*   **Vim Users:** Consider changing the leader key to match your Vim configuration for consistency.
*   **Quick Reference:** Use <leader>h to see a quick help overlay with the most common shortcuts.
*   **Slash Commands:** All shortcuts have equivalent slash commands (e.g., `/help` instead of <leader>h).

Advanced Customization
----------------------

### Creating Custom Shortcuts

```
{
  "keybinds": {
    // Custom shortcuts for frequently used commands
    "custom_clear_session": "ctrl+alt+c",
    "custom_quick_save": "ctrl+s",
    "custom_toggle_mode": "f3"
  },

  // Map custom shortcuts to slash commands
  "custom_commands": {
    "ctrl+alt+c": "/clear",
    "ctrl+s": "/sessions save",
    "f3": "/agents toggle"
  }
}
```


####  Configuration Validation

After modifying keybindings, use `/config validate` to check for conflicts or syntax errors. Restart the TUI to apply changes.

Troubleshooting
---------------

### Common Issues

*   **Shortcuts not working:** Check if your terminal emulator is intercepting the key combination
*   **Leader key conflicts:** Change the leader key in configuration if it conflicts with other applications
*   **Key notation errors:** Ensure proper syntax in the configuration file (use quotes around key combinations)
*   **Reset to defaults:** Remove the keybinds section from config to restore default shortcuts

### Testing Shortcuts

*   Use `/config show` to view current keybinding configuration
*   Press <leader>h to see active shortcuts
*   Try alternative slash commands if shortcuts fail
*   Check terminal documentation for intercepted key combinations