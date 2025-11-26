![ABOV3 LOGO](./images/ABOV3_logo_transparent.png)

# ABOV3: Genesis CodeForger
The origin of a new coding era. An intelligent, multi‑agent coding partner that thinks in systems, not snippets — orchestrating teams of specialized AI agents, mastering deep code comprehension, and delivering rapid, iterative builds. From concept to deployment, it forges production‑ready solutions with the precision, speed, and adaptability you expect from the next generation of AI engineering.

*   LLM-powered code generation
*   Multi-agent orchestration
*   Secure deployable connectors
*   IDE & CI integrations

![ABOV3 Terminal Interface](assets/abov3_ss.png)

What ABOV3: Genesis CodeForger can do
-------------------------------------

### AI Code Generation

From prototypes to production-ready modules. Context-aware suggestions, idiomatic code, and multi-file scaffolding.

### Multi-Agent Orchestration

Chain specialized agents for analysis, testing, and refactor — orchestrated to solve complex engineering tasks.

### Live Debug & Fix

Realtime test-run feedback, automated patch proposals, and safe refactors with undo/redo support.

### Integrations

Out-of-the-box adapters for editors, CI systems, cloud providers, and VCS workflows.

### AI Providers

ABOV3 supports **50+ AI providers** out-of-the-box:

- **Anthropic**: Claude 3 family (Opus, Sonnet, Haiku)
- **OpenAI**: GPT-4, GPT-4 Turbo, GPT-3.5-turbo
- **Google**: Gemini Pro, Gemini Flash
- **Local Models**: Ollama with continuous monitoring
- **Hugging Face**: Open-source models
- **Together AI**: Fast inference
- **Mistral**: Mistral models
- **Groq**: Ultra-fast inference
- **Custom Providers**: API-compatible backends

**Features:**
- Automatic provider detection from environment variables
- OAuth flow for supported providers (Anthropic, Google)
- API key management and validation
- Model auto-discovery and caching
- Fallback provider selection

### Ollama Continuous Monitoring

Real-time local model detection:
- **30-second polling** for model changes
- **Auto-discovery**: Models appear when Ollama starts
- **Real-time removal**: Models disappear when Ollama stops
- **No phantom models**: Only shows actually available models
- **Background compatible**: Works with `ollama serve` and background instances
- **Zero configuration**: Automatic endpoint detection

### Session Management

Complete conversation session system:
- **Session creation and persistence**
- **Multi-turn conversations** with full history
- **Session listing and switching**
- **Session export** to JSON/Markdown
- **Session sharing** (cloud and local)
- **Session recovery** from backups
- **Context compaction** for large sessions
- **Child sessions** for branching conversations

### Local Network Sharing

Peer programming without cloud dependency:
- **LAN-based sharing**: Sessions shared within local networks
- **Secret-based authentication**: Each share has unique secret
- **Real-time collaboration**: Multiple developers per session
- **Read-only & write modes**: Permission control
- **Peer management**: View connected collaborators
- **Auto-discovery**: Peers can discover shared sessions


### Links

[Documentation](./docs/DocumentationRoot.md)

#### Getting Started

  - [Installation](./docs/installation.md)
  - [Configuration](./docs/configuration.md)
  - [Provders](./docs/providers.md)

#### Usage Guides

  - [Terminal TUI](./docs/tui.md)
  - [Command-Line](./docs/cli.md)
  - [Ollama Local Models](./docs/ollama.md)

#### Advanced

  - [Agents](./docs/agents.md)
  - [Custom Commands](./docs/commands.md)
  - [Keybindings](./docs/keybindings.md)
  - [Models](./docs/models.md)