# Installation Guide - ABOV3: Genesis CodeForger
Get ABOV3: Genesis CodeForger v0.1.8 running on your system in minutes.

###  Self-Installing Binary (New in v0.1.8!)

Download just **one file** - the binary contains everything including built-in install/update/uninstall commands. No additional scripts needed!

Download Pre-built Binaries
---------------------------

⚡ Self-Install Method (Recommended)
-----------------------------------

After downloading the binary, use the built-in install command to automatically configure your system:

### Linux & macOS

```
# Download and make executable
chmod +x abov3

# Run self-install (adds to PATH automatically)
./abov3 install

# Verify installation
abov3 --version
```


**✨ What this does:**

*   Copies binary to `~/.local/bin/` (or `/usr/local/bin/`)
*   Updates your shell configuration (.bashrc, .zshrc, etc.)
*   Makes `abov3` available from anywhere

### Windows

```
# Run self-install in PowerShell or Command Prompt
.\abov3.exe install

# Verify installation
abov3 --version
```


**✨ What this does:**

*   Copies binary to `%LocalAppData%\Programs\ABOV3\`
*   Adds directory to system PATH via registry
*   Makes `abov3` available from any terminal

⚡ Self-Management Commands
---------------------------

ABOV3 includes built-in commands to manage itself:

### Update to Latest Version

```
# Check for and install updates from GitHub
abov3 update
```


This will automatically download and install the latest release with atomic replacement (safe rollback on failure).

### Uninstall

```
# Remove ABOV3 from your system
abov3 uninstall
```


This will remove the binary and clean up PATH configuration.

### ⚡ Safe Update Process

Updates use atomic binary replacement with automatic rollback if anything goes wrong. Your current version is backed up before replacement.

Manual Installation (Alternative)
---------------------------------

###  Linux Manual Installation

#### Manual PATH Setup

```
# Download
wget https://github.com/ABOV3AI/abov3-genesis-codeforger/releases/download/v0.1.8/abov3
chmod +x abov3

# Move to system directory
sudo mv abov3 /usr/local/bin/

# Verify installation
abov3 --version
```


#### Desktop Entry (Optional)

```
# Create desktop entry for application menu
cat > ~/.local/share/applications/abov3.desktop << EOF
[Desktop Entry]
Name=ABOV3 Genesis CodeForger
Comment=AI-powered coding assistant
Exec=/usr/local/bin/abov3
Icon=terminal
Terminal=true
Type=Application
Categories=Development;
EOF
```


### 犯 Windows Manual Installation

** Download Tip:** For large binaries (150MB+), use `curl.exe` for more reliable downloads. If Invoke-WebRequest fails, try the alternative methods below.

#### Method 1: Using curl.exe (Recommended)

```
# curl.exe is included in Windows 10/11
curl.exe -L https://github.com/ABOV3AI/abov3-genesis-codeforger/releases/download/v0.1.8/abov3.exe -o "$env:ProgramFiles\ABOV3\abov3.exe"

# Add to PATH (requires Administrator)
[Environment]::SetEnvironmentVariable(
    "Path",
    $env:Path + ";$env:ProgramFiles\ABOV3",
    [EnvironmentVariableTarget]::Machine
)

# Verify installation (restart terminal first)
abov3 --version
```


#### Method 2: Using System.Net.WebClient

```
# More reliable for large files
New-Item -ItemType Directory -Force -Path "$env:ProgramFiles\ABOV3"
(New-Object System.Net.WebClient).DownloadFile(
    'https://github.com/ABOV3AI/abov3-genesis-codeforger/releases/download/v0.1.8/abov3.exe',
    "$env:ProgramFiles\ABOV3\abov3.exe"
)
```


#### Method 3: Using Invoke-WebRequest (if others fail)

```
# Disable progress bar for better performance
$ProgressPreference = 'SilentlyContinue'
$url = "https://github.com/ABOV3AI/abov3-genesis-codeforger/releases/download/v0.1.8/abov3.exe"
$output = "$env:ProgramFiles\ABOV3\abov3.exe"

New-Item -ItemType Directory -Force -Path "$env:ProgramFiles\ABOV3"
Invoke-WebRequest -Uri $url -OutFile $output -UseBasicParsing
$ProgressPreference = 'Continue'
```


#### Windows Terminal Integration

```
# Add to Windows Terminal settings.json
{
  "profiles": {
    "list": [
      {
        "name": "ABOV3",
        "commandline": "C:\\Program Files\\ABOV3\\abov3.exe",
        "icon": "烙"
      }
    ]
  }
}
```


###  macOS Manual Installation

#### Intel Macs

```
# Download
curl -L -o abov3 https://github.com/ABOV3AI/abov3-genesis-codeforger/releases/download/v0.1.8/abov3-x64

# Make executable and move to PATH
chmod +x abov3
sudo mv abov3 /usr/local/bin/

# If security warning appears
xattr -d com.apple.quarantine /usr/local/bin/abov3

# Verify installation
abov3 --version
```


#### Apple Silicon (M1/M2/M3)

```
# Download ARM version
curl -L -o abov3 https://github.com/ABOV3AI/abov3-genesis-codeforger/releases/download/v0.1.8/abov3-arm64

# Make executable and move to PATH
chmod +x abov3
sudo mv abov3 /usr/local/bin/

# If security warning appears
xattr -d com.apple.quarantine /usr/local/bin/abov3

# Verify installation
abov3 --version
```


Build from Source
-----------------

###  Prerequisites

*   Go 1.21 or later
*   Git
*   Make (optional)

###  Building ABOV3

```
# Clone the repository
git clone https://github.com/ABOV3AI/abov3-genesis-codeforger.git
cd abov3-genesis-codeforger

# Build for your platform
go build -o abov3 ./cmd/abov3

# Or use the build script
./scripts/build.sh

# Install globally
sudo mv abov3 /usr/local/bin/

# Verify
abov3 --version
```


#### Cross-Platform Build

```
# Build for all platforms
make build-all

# Or manually:
# Linux
GOOS=linux GOARCH=amd64 go build -o build/abov3-linux-x64 ./cmd/abov3

# Windows
GOOS=windows GOARCH=amd64 go build -o build/abov3.exe ./cmd/abov3

# macOS Intel
GOOS=darwin GOARCH=amd64 go build -o build/abov3-darwin-x64 ./cmd/abov3

# macOS ARM
GOOS=darwin GOARCH=arm64 go build -o build/abov3-darwin-arm64 ./cmd/abov3
```


System Requirements
-------------------


|Component |Minimum                             |Recommended                    |
|----------|------------------------------------|-------------------------------|
|OS        |Linux 3.10+, Windows 10, macOS 10.15|Latest stable OS version       |
|RAM       |512 MB                              |2 GB+                          |
|Disk Space|50 MB                               |200 MB                         |
|Terminal  |Any terminal with UTF-8 support     |Modern terminal with 256 colors|
|Network   |Internet for API providers          |Stable broadband connection    |


Post-Installation Setup
-----------------------

### 1️⃣ First Run

```
# Start ABOV3 TUI
abov3

# You'll be prompted to:
# - Choose a default model
# - Configure providers
# - Set up authentication
```


### 2️⃣ Configure Authentication

```
# For Anthropic OAuth (Claude Pro/Max users)
abov3 auth login

# For API keys, edit ~/.config/abov3/abov3.json
{
  "provider": {
    "anthropic": {
      "apiKey": "your-api-key"
    }
  }
}
```


### 3️⃣ Install Ollama (Optional)

```
# For local models
curl -fsSL https://ollama.com/install.sh | sh

# Pull a model
ollama pull qwen2.5-coder:14b

# Verify in ABOV3
abov3 models
```


### 4️⃣ Test Installation

```
# Quick test
abov3 run "Hello, ABOV3!"

# Check available models
abov3 models

# View configuration
abov3 config

# Start TUI
abov3
```


Updating ABOV3
--------------

###  Auto-Update

```
# Check for updates and upgrade
abov3 upgrade

# Upgrade to specific version
abov3 upgrade v1.2.3

# Check current version
abov3 --version
```


###  Manual Update

Simply download the latest binary and replace the existing one:

```
# Linux/macOS
curl -L -o /tmp/abov3-new [download-url]
chmod +x /tmp/abov3-new
sudo mv /tmp/abov3-new /usr/local/bin/abov3

# Windows (PowerShell)
Invoke-WebRequest -Uri [download-url] -OutFile "$env:ProgramFiles\ABOV3\abov3.exe"
```


####  Installation Tips

*   Add ABOV3 to your PATH for easy access from any directory
*   Create an alias: `alias a3="abov3"` for quicker typing
*   Use `abov3 --continue` to resume your last session
*   Configure your preferred model as default to save time
*   Install Ollama for offline coding assistance

Troubleshooting
---------------

### Permission Denied (Linux/macOS)

```
# Make executable
chmod +x abov3

# If in PATH issue
export PATH=$PATH:/path/to/abov3
echo 'export PATH=$PATH:/path/to/abov3' >> ~/.bashrc
```


### Security Warning (macOS)

```
# Remove quarantine attribute
xattr -d com.apple.quarantine abov3

# Or allow in System Preferences > Security & Privacy
```


### Command Not Found

```
# Check if ABOV3 is in PATH
which abov3

# Add to PATH (Linux/macOS)
export PATH=$PATH:/usr/local/bin

# Add to PATH (Windows)
setx PATH "%PATH%;C:\Program Files\ABOV3"
```
