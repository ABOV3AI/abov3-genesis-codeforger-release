# Models Documentation - ABOV3: Genesis CodeForger
Choose from the best AI models for your coding needs - from Claude's deep reasoning to fast local models.

###  Quick Model Selection

*   **Best Overall:** Claude 3 Opus (complex tasks) or Sonnet (balanced)
*   **Best Free:** Ollama with Qwen2.5-Coder or Mistral
*   **Fastest:** Claude 3 Haiku or GPT-3.5 Turbo
*   **Privacy-First:** Any Ollama model (runs locally)

Anthropic Claude Models
-----------------------

RECOMMENDED

###  Claude 3 Opus

**Model ID:** `anthropic/claude-3-opus`

**Context:** 200,000 tokens

**Strengths:** Complex reasoning, large codebases, architecture design

**Best for:** Major refactoring, system design, complex debugging

**Speed:** ★★★☆☆ | **Quality:** ★★★★★

```
./abov3-linux-x64 run -m anthropic/claude-3-opus "Your complex task"
```


BALANCED

### ⚡ Claude 3 Sonnet

**Model ID:** `anthropic/claude-3-sonnet`

**Context:** 200,000 tokens

**Strengths:** Fast responses with high quality, great for iterative development

**Best for:** Daily coding tasks, code reviews, documentation

**Speed:** ★★★★☆ | **Quality:** ★★★★☆

```
./abov3-linux-x64 run -m anthropic/claude-3-sonnet "Your task"
```


FASTEST

###  Claude 3 Haiku

**Model ID:** `anthropic/claude-3-haiku`

**Context:** 200,000 tokens

**Strengths:** Lightning fast, cost-effective, good for simple tasks

**Best for:** Quick queries, simple refactoring, syntax questions

**Speed:** ★★★★★ | **Quality:** ★★★☆☆

```
./abov3-linux-x64 run -m anthropic/claude-3-haiku "Quick question"
```


OpenAI GPT Models
-----------------

POWERFUL

### 易 GPT-4

**Model ID:** `openai/gpt-4`

**Context:** 128,000 tokens

**Strengths:** General knowledge, creative solutions, multi-modal

**Best for:** Creative coding, architectural decisions, complex algorithms

**Speed:** ★★★☆☆ | **Quality:** ★★★★★

```
./abov3-linux-x64 run -m openai/gpt-4 "Your task"
```


### ⚡ GPT-4 Turbo

**Model ID:** `openai/gpt-4-turbo`

**Context:** 128,000 tokens

**Strengths:** Faster than GPT-4, same quality

**Best for:** Balanced performance and speed needs

**Speed:** ★★★★☆ | **Quality:** ★★★★★

BUDGET

###  GPT-3.5 Turbo

**Model ID:** `openai/gpt-3.5-turbo`

**Context:** 16,000 tokens

**Strengths:** Very fast, low cost, good for simple tasks

**Best for:** Quick answers, boilerplate code, simple scripts

**Speed:** ★★★★★ | **Quality:** ★★★☆☆

Ollama Local Models
-------------------

FREE & LOCAL CODING

###  Qwen2.5-Coder

**Model IDs:**

*   `ollama/qwen2.5-coder:1.5b` - Tiny, very fast
*   `ollama/qwen2.5-coder:7b` - Balanced
*   `ollama/qwen2.5-coder:14b` - Best quality
*   `ollama/qwen2.5-coder:32b` - Professional

**Strengths:** Specialized for coding, excellent performance

**Requirements:** 4GB+ VRAM (7B), 8GB+ VRAM (14B)

```
# Install and use
ollama pull qwen2.5-coder:14b
./abov3-linux-x64 run -m ollama/qwen2.5-coder:14b "Generate code"
```


FREE & LOCAL

### 蓮 Llama 3

**Model IDs:**

*   `ollama/llama3:8b` - Fast, general purpose
*   `ollama/llama3:70b` - Powerful (needs 32GB+ RAM)

**Strengths:** Well-rounded, good reasoning

```
ollama pull llama3:8b
./abov3-linux-x64 run -m ollama/llama3:8b "Your task"
```


FREE & LOCAL

###  Mistral

**Model IDs:**

*   `ollama/mistral:7b` - Fast and efficient
*   `ollama/mixtral:8x7b` - MoE architecture, powerful

**Strengths:** Efficient, good for general tasks

```
ollama pull mistral:7b
./abov3-linux-x64 run -m ollama/mistral:7b "Your task"
```


FREE & LOCAL

###  CodeLlama

**Model IDs:**

*   `ollama/codellama:7b` - Code generation
*   `ollama/codellama:13b` - Better quality
*   `ollama/codellama:34b` - Best quality

**Strengths:** Specialized for code, supports many languages

Model Comparison
----------------


|Model            |Context|Speed    |Quality  |Cost|Best Use Case     |
|-----------------|-------|---------|---------|----|------------------|
|Claude 3 Opus    |200K   |Medium   |Excellent|$$ |Complex tasks     |
|Claude 3 Sonnet  |200K   |Fast     |Very Good|$  |Daily coding      |
|Claude 3 Haiku   |200K   |Very Fast|Good     |$   |Quick queries     |
|GPT-4            |128K   |Medium   |Excellent|$$ |Creative solutions|
|GPT-3.5 Turbo    |16K    |Very Fast|Good     |$   |Simple tasks      |
|Qwen2.5-Coder 14B|32K    |Fast*    |Very Good|Free|Local coding      |
|Llama 3 8B       |8K     |Fast*    |Good     |Free|General local     |


\* Local model speed depends on hardware

Choosing the Right Model
------------------------

####  Model Selection Guide

##### For Code Generation:

*   **Best:** Claude 3 Opus or Sonnet
*   **Local:** Qwen2.5-Coder 14B+
*   **Budget:** Claude 3 Haiku

##### For Debugging:

*   **Best:** Claude 3 Opus (complex bugs)
*   **Fast:** Claude 3 Sonnet
*   **Local:** Qwen2.5-Coder or CodeLlama

##### For Documentation:

*   **Best:** GPT-4 or Claude 3 Sonnet
*   **Fast:** GPT-3.5 Turbo
*   **Local:** Llama 3 or Mistral

##### For System Design:

*   **Best:** Claude 3 Opus or GPT-4
*   **Balanced:** Claude 3 Sonnet

Using Models
------------

### Setting Default Model

```
# In config file
{
  "defaultModel": "anthropic/claude-3-sonnet"
}

# Via environment variable
export ABOV3_MODEL="ollama/qwen2.5-coder:14b"

# Via command line
./abov3-linux-x64 -m openai/gpt-4
```


### Switching Models

```
# In TUI
/model anthropic/claude-3-opus

# For single command
./abov3-linux-x64 run -m ollama/mistral:7b "Quick task"

# List available models
./abov3-linux-x64 models
```


### Model-Specific Settings

```
{
  "models": {
    "anthropic/claude-3-opus": {
      "temperature": 0.7,
      "maxTokens": 4096
    },
    "ollama/qwen2.5-coder:14b": {
      "temperature": 0.3,
      "topP": 0.9
    }
  }
}
```


Performance Tips
----------------

###  Optimizing Model Usage

*   **Use faster models for simple tasks:** Don't use Opus for syntax questions
*   **Local models for iteration:** Use Ollama during development to save costs
*   **Streaming for feedback:** Enable streaming for better UX
*   **Context management:** Clear context when switching tasks
*   **Temperature tuning:** Lower (0.3) for code, higher (0.7) for creative tasks

###  Cost Optimization

*   **Development:** Use local Ollama models
*   **Testing:** Use Haiku or GPT-3.5 Turbo
*   **Production:** Use Sonnet for balance
*   **Complex tasks:** Reserve Opus for when needed
*   **OAuth:** Use Anthropic OAuth if you have Claude Pro/Max

###  Pro Tips

*   Start with Sonnet as your default - it's well-balanced
*   Install Qwen2.5-Coder for offline coding assistance
*   Use model-specific agents for consistent behavior
*   Monitor token usage to control costs
*   Test prompts with cheap models first