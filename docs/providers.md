# Providers Documentation - ABOV3: Genesis CodeForger
Connect ABOV3 to multiple AI providers for maximum flexibility and model selection.

###  Quick Setup

Most providers work out of the box. Just run `./abov3-linux-x64 auth login` for Anthropic OAuth, or add API keys to your configuration.

Supported Providers
-------------------

### Anthropic (Claude)

Recommended

**Models:** Claude 3 Opus, Sonnet, Haiku

**Authentication:** OAuth (Claude Pro/Max) or API Key

#### OAuth Setup (Recommended)

```
# Login with your Claude Pro/Max account
./abov3-linux-x64 auth login

# This will:
# 1. Open browser for authentication
# 2. Save credentials securely
# 3. Auto-refresh tokens as needed
```


#### API Key Setup

```
# Add to ~/.config/abov3/abov3.json
{
  "provider": {
    "anthropic": {
      "apiKey": "sk-ant-api03-..."
    }
  }
}
```


### Ollama (Local Models)

Free & Private

**Models:** Llama, Mistral, Qwen, CodeLlama, and more

**Requirements:** Ollama installed and running locally

#### Setup

```
# Install Ollama
curl -fsSL https://ollama.com/install.sh | sh

# Start Ollama service
ollama serve

# Pull models you want
ollama pull qwen2.5-coder:14b
ollama pull mistral:7b
ollama pull llama3:8b

# Use in ABOV3
./abov3-linux-x64 run -m ollama/qwen2.5-coder:14b "Your prompt"
```


#### Remote Ollama

```
# Connect to remote Ollama instance
export OLLAMA_BASE_URL="http://192.168.1.100:11434"

# Or add to config
{
  "provider": {
    "ollama": {
      "baseUrl": "http://192.168.1.100:11434"
    }
  }
}
```


###  OpenAI (GPT)

**Models:** GPT-4, GPT-4 Turbo, GPT-3.5 Turbo

**Authentication:** API Key required

#### Setup

```
# Add to ~/.config/abov3/abov3.json
{
  "provider": {
    "openai": {
      "apiKey": "sk-..."
    }
  }
}

# Or use environment variable
export OPENAI_API_KEY="sk-..."
```


### Azure OpenAI

**Models:** GPT-4, GPT-3.5 (via Azure deployment)

**Authentication:** Azure credentials

#### Setup

```
{
  "provider": {
    "azure": {
      "apiKey": "your-azure-key",
      "endpoint": "https://your-resource.openai.azure.com",
      "deployment": "gpt-4"
    }
  }
}
```


### Google (Gemini)

Beta

**Models:** Gemini Pro, Gemini Ultra

**Authentication:** API Key

#### Setup

```
{
  "provider": {
    "google": {
      "apiKey": "your-gemini-api-key"
    }
  }
}
```


Provider Configuration
----------------------

### Global Configuration

Edit `~/.config/abov3/abov3.json`:

```
{
  "defaultModel": "anthropic/claude-3-sonnet",
  "provider": {
    "anthropic": {
      "apiKey": "sk-ant-...",
      "maxTokens": 4096,
      "temperature": 0.7
    },
    "openai": {
      "apiKey": "sk-...",
      "organization": "org-..."
    },
    "ollama": {
      "baseUrl": "http://localhost:11434"
    }
  }
}
```


### Environment Variables

```
# Anthropic
export ANTHROPIC_API_KEY="sk-ant-..."

# OpenAI
export OPENAI_API_KEY="sk-..."

# Ollama (if not localhost)
export OLLAMA_BASE_URL="http://192.168.1.100:11434"

# Azure
export AZURE_OPENAI_KEY="..."
export AZURE_OPENAI_ENDPOINT="https://..."

# Google
export GOOGLE_API_KEY="..."
```


Model Comparison
----------------


|Provider |Model            |Context|Speed     |Cost|Best For                          |
|---------|-----------------|-------|----------|----|----------------------------------|
|Anthropic|Claude 3 Opus    |200K   |Medium    |$$ |Complex reasoning, large codebases|
|Anthropic|Claude 3 Sonnet  |200K   |Fast      |$  |Balanced performance              |
|Anthropic|Claude 3 Haiku   |200K   |Very Fast |$   |Quick tasks, high volume          |
|OpenAI   |GPT-4            |128K   |Medium    |$$ |General purpose, creative tasks   |
|OpenAI   |GPT-3.5 Turbo    |16K    |Very Fast |$   |Simple tasks, prototyping         |
|Ollama   |Qwen2.5-Coder:14b|32K    |Fast*     |Free|Code generation, local development|
|Ollama   |Mistral:7b       |8K     |Very Fast*|Free|General purpose, privacy-sensitive|


\* Speed depends on local hardware

Managing Providers
------------------

### List Available Models

```
# Show all models from configured providers
./abov3-linux-x64 models

# Output includes:
# - Provider name
# - Model ID
# - Availability status
```


### Switch Between Providers

```
# Use specific model for a session
./abov3-linux-x64 -m anthropic/claude-3-opus

# One-off with different model
./abov3-linux-x64 run -m ollama/mistral:7b "Your prompt"

# Set default in config
{
  "defaultModel": "anthropic/claude-3-sonnet"
}
```


### Test Provider Connection

```
# Test with simple prompt
./abov3-linux-x64 run --print-logs "Hello, are you working?"

# Check authentication status
./abov3-linux-x64 auth list
```


#### Provider Tips

*   **Anthropic OAuth:** Best for Claude Pro/Max users - no API costs
*   **Ollama:** Perfect for offline work and privacy-sensitive projects
*   **Multiple Providers:** Configure all providers for maximum flexibility
*   **Model Selection:** Use faster models for simple tasks, powerful models for complex work
*   **Cost Management:** Monitor API usage and use local models when possible

Troubleshooting
---------------

### Authentication Failed

```
# Check credentials
./abov3-linux-x64 auth list

# Re-authenticate Anthropic
./abov3-linux-x64 auth logout
./abov3-linux-x64 auth login

# Verify API keys in config
cat ~/.config/abov3/abov3.json | grep apiKey
```


### Ollama Connection Issues

```
# Check if Ollama is running
curl http://localhost:11434/api/tags

# Restart Ollama
systemctl restart ollama  # Linux with systemd
ollama serve              # Manual start

# Check available models
ollama list
```


### Rate Limiting

If you encounter rate limits:

*   Switch to a different provider temporarily
*   Use local Ollama models for development
*   Implement retry logic in scripts
*   Consider upgrading your API plan