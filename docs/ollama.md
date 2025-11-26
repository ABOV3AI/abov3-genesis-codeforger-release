# Ollama Local Models - ABO V3: Genesis CodeForger
Run AI models locally with Ollama integration. Complete privacy, no API costs, and full control over your AI assistant.

###  Why Use Local Models?

*   **Privacy First** - Your code never leaves your machine
*   **No API Costs** - Use models without per-token billing
*   **Offline Capable** - Work without internet connectivity
*   **Full Control** - Customize model parameters and behavior
*   **Enterprise Ready** - Meet strict security requirements

Quick Start
-----------

1.  **Install Ollama**  
    Download from [ollama.ai](https://ollama.ai/) or use package managers:
    
    ```
    # macOS brew install ollama # Linux curl -fsSL https://ollama.ai/install.sh | sh # Windows # Download installer from ollama.ai
    ```
    
2.  **Start Ollama Service**
    
    ```
    ollama serve
    ```
    
3.  **Pull a Model**
    
    ```
    # Recommended for coding ollama pull llama3.1:8b # Or for better performance (requires more RAM) ollama pull llama3.1:70b
    ```
    
4.  **Configure ABOV3**  
    ABOV3 automatically detects running Ollama models. No additional configuration needed!

Recommended Models
------------------

Best models for different use cases and hardware configurations:

### Code Generation & Development

| Ollama Model   |  Size     |  Description  |
|----------------|-----------|-------------------------------------------------------|
| Llama 3.1 8B Instruct | ~4.7GB Fast | Excellent balance of performance and speed. Great for general coding tasks, debugging, and documentation. |
| CodeLlama 13B Instruct | ~7.3GB Medium | Specialized for code generation. Superior for complex algorithms and multi-file projects. |
| Mistral 7B Instruct v0.3 | ~4.1GB Fast | Excellent reasoning capabilities. Good for architectural decisions and code review. |


### High Performance (16GB+ RAM)

| Ollama Model   |  Size     |  Description  |
|----------------|-----------|-------------------------------------------------------|
| Llama 3.1 70B Instruct | ~40GB Slow | State-of-the-art performance comparable to GPT-4. Best for complex reasoning and large codebases. |
| CodeLlama 34B Instruct | ~19GB Slow | Premium code model. Exceptional for enterprise-grade development and complex refactoring. |
| Mixtral 8x7B Instruct | ~26GB Medium | Mixture of experts model. Excellent performance with reasonable resource usage. |


### Lightweight (8GB RAM)

| Ollama Model   |  Size     |  Description  |
|----------------|-----------|-------------------------------------------------------|
| Llama 3.2 3B Instruct | ~2.0GB Fast | Ultra-fast responses. Good for quick questions and simple code generation. |
| Phi-3 Mini 4K | ~2.3GB Fast | Microsoft's efficient model. Excellent for code completion and small tasks. |
| Gemma 2B Instruct | ~1.4GB Fast | Google's compact model. Very fast inference for basic coding assistance. |


Installation & Setup
--------------------

### Installing Ollama

#### macOS

```
# Using Homebrew (recommended) brew install ollama # Or download from ollama.ai curl -fsSL https://ollama.ai/install.sh | sh
```

#### Linux

```
# Ubuntu/Debian curl -fsSL https://ollama.ai/install.sh | sh # Or manual installation sudo apt update sudo apt install ollama
```

#### Windows

```
# Download installer from ollama.ai # Or use Windows Subsystem for Linux (WSL) wsl --install # Then follow Linux instructions
```

### Starting Ollama

```
# Start the Ollama service ollama serve # Verify it's running curl http://localhost:11434
```

####  Auto-start on Boot

To start Ollama automatically on system boot:

```
# macOS brew services start ollama # Linux (systemd) sudo systemctl enable ollama sudo systemctl start ollama
```

Model Management
----------------

### Pulling Models

```
# Pull recommended coding model ollama pull llama3.1:8b # Pull specific versions ollama pull codellama:13b-instruct ollama pull mistral:7b-instruct-v0.3 # Pull quantized versions for lower memory usage ollama pull llama3.1:8b-q4_0 # 4-bit quantization ollama pull llama3.1:8b-q8_0 # 8-bit quantization
```

### Managing Models

```
# List installed models ollama list # Remove a model ollama rm llama3.1:8b # Show model information ollama show llama3.1:8b # Update a model ollama pull llama3.1:8b
```

### Model Formats


|Format        |Memory Usage|Speed    |Quality  |Use Case            |
|--------------|------------|---------|---------|--------------------|
|fp16 (default)|High        |Medium   |Best     |High-end hardware   |
|q8_0          |Medium      |Fast     |Excellent|Balanced performance|
|q4_0          |Low         |Fast     |Good     |Resource-constrained|
|q2_K          |Very Low    |Very Fast|Fair     |Minimal hardware    |


ABOV3 Integration
-----------------

### Automatic Discovery

ABOV3 automatically detects running Ollama models when you start the TUI or CLI:

```
# Start ABOV3 TUI - models appear automatically ./abov3-tui-linux-x64 # List available models (includes Ollama) /models
```

### Manual Configuration

Add Ollama provider explicitly in your ABOV3 configuration:

```
{ "providers": { "ollama": { "type": "ollama", "base_url": "http://localhost:11434", "enabled": true, "timeout": 120000, "max_retries": 3 } } }
```

### Model Selection

```
# In ABOV3 TUI /models # List all models F2 # Cycle through recent models <leader>m # Open model selector # Select Ollama model directly /model llama3.1:8b
```

Performance Optimization
------------------------

### Hardware Requirements


|Model Size|Minimum RAM|Recommended RAM|GPU Support |Typical Speed   |
|----------|-----------|---------------|------------|----------------|
|3B models |4GB        |8GB            |Optional    |10-20 tokens/sec|
|7B models |8GB        |16GB           |Recommended |5-15 tokens/sec |
|13B models|16GB       |32GB           |Required    |3-8 tokens/sec  |
|70B models|64GB       |128GB          |High-end GPU|1-3 tokens/sec  |


### GPU Acceleration

### NVIDIA GPU Support

Ollama automatically uses NVIDIA GPUs when available. Ensure you have CUDA drivers installed:

```
# Check GPU support nvidia-smi # Ollama will automatically use GPU ollama run llama3.1:8b "Hello, GPU!"
```

### Apple Silicon (M1/M2/M3)

Ollama natively supports Apple Silicon with excellent performance:

```
# Metal Performance Shaders acceleration is automatic ollama run llama3.1:8b
```

### Memory Management

```
# Set memory limits in Ollama export OLLAMA_MAX_LOADED_MODELS=2 export OLLAMA_MAX_VRAM=8GB # Configure model keep-alive time ollama run --keep-alive 5m llama3.1:8b
```

Advanced Configuration
----------------------

### Custom Modelfiles

Create specialized models for coding tasks:

```
# Create a Modelfile FROM llama3.1:8b PARAMETER temperature 0.1 PARAMETER top_p 0.9 PARAMETER stop "<|endoftext|>" SYSTEM """ You are an expert software developer assistant. Always: - Write clean, well-commented code - Follow best practices and conventions - Explain your reasoning - Consider edge cases and error handling """
```

```
# Build custom model ollama create coding-assistant -f ./Modelfile # Use in ABOV3 /model coding-assistant
```

### Environment Variables

```
# Ollama configuration export OLLAMA_HOST=0.0.0.0:11434 # Bind to all interfaces export OLLAMA_ORIGINS="*" # Allow all origins export OLLAMA_MODELS=/custom/path # Custom model directory export OLLAMA_KEEP_ALIVE=5m # Model cache time export OLLAMA_MAX_LOADED_MODELS=3 # Concurrent models export OLLAMA_NUM_PARALLEL=4 # Parallel requests export OLLAMA_MAX_QUEUE=512 # Request queue size
```

### Remote Ollama Server

Connect ABOV3 to a remote Ollama instance:

```
# ABOV3 configuration { "providers": { "ollama_remote": { "type": "ollama", "base_url": "http://192.168.1.100:11434", "enabled": true, "models": ["llama3.1:70b", "codellama:34b"] } } }
```

Troubleshooting
---------------

### Common Issues

#### ⚠️ Models not appearing in ABOV3

*   Ensure Ollama is running: `curl http://localhost:11434`
*   Check if models are pulled: `ollama list`
*   Restart ABOV3 TUI after pulling new models
*   Verify no firewall is blocking port 11434

#### ⚠️ Slow performance

*   Use quantized models (q4\_0, q8\_0) for better speed
*   Enable GPU acceleration if available
*   Increase system RAM or use smaller models
*   Close other memory-intensive applications

#### ⚠️ Out of memory errors

*   Switch to smaller models (3B or 7B instead of 13B+)
*   Use higher quantization (q4\_0 instead of fp16)
*   Reduce `OLLAMA_MAX_LOADED_MODELS`
*   Add swap memory to your system

### Debugging

```
# Check Ollama status ollama ps # View Ollama logs journalctl -u ollama # Linux brew services info ollama # macOS # Test model directly ollama run llama3.1:8b "Write a simple Python function" # Check ABOV3 connection /config doctor
```

### Performance Monitoring

```
# Monitor system resources htop nvidia-smi # For NVIDIA GPUs # Ollama API health check curl http://localhost:11434/api/version # Model memory usage ollama ps
```

####  Best Practices

*   **Start Small:** Begin with 7B models, then scale up based on your hardware
*   **Use Quantization:** q8\_0 provides excellent quality with reduced memory usage
*   **Keep Models Loaded:** Set appropriate keep-alive times to avoid reload delays
*   **Monitor Resources:** Watch RAM and GPU usage to optimize your setup
*   **Backup Configurations:** Save working Modelfiles and configurations
*   **Regular Updates:** Keep Ollama and models updated for best performance

Model Comparison
----------------

Choose the right model for your use case and hardware:


|Model        |Size |Code Quality|Speed    |Memory|Best For               |
|-------------|-----|------------|---------|------|-----------------------|
|Llama 3.1 8B |4.7GB|★★★★☆       |Fast     |8GB   |General development    |
|CodeLlama 13B|7.3GB|★★★★★       |Medium   |16GB  |Complex algorithms     |
|Mistral 7B   |4.1GB|★★★★☆       |Fast     |8GB   |Architecture, reasoning|
|Llama 3.1 70B|40GB |★★★★★       |Slow     |64GB  |Complex projects       |
|Phi-3 Mini   |2.3GB|★★★☆☆       |Very Fast|4GB   |Quick tasks, completion|
