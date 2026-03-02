# Personal Stack

A comprehensive guide to my containerized personal development and AI stack, with links to official repositories and documentation.

## Services Overview

| Service | Purpose | Port | Status | Docs |
|---------|---------|------|--------|------|
| [Ollama](#ollama) | Local LLM inference engine | 11434 | Running | [Repo](https://github.com/ollama/ollama) |
| [Open WebUI](#open-webui) | Web interface for Ollama & LLMs | 3000 | Running | [Repo](https://github.com/open-webui/open-webui) |
| [n8n](#n8n) | Workflow automation & API orchestration | 5678 | Running | [Repo](https://github.com/n8n-io/n8n) |
| [MCP Gateway](#mcp-gateway) | Docker's Model Context Protocol gateway | - | Running (×2) | [Repo](https://github.com/docker/mcp-gateway) |
| [Tailscale](#tailscale) | Secure mesh VPN | - | Running | [Repo](https://github.com/tailscale/tailscale) |

---

## Services

### Ollama
**Local LLM inference engine**

Ollama allows you to run large language models locally on your machine. Pull and run models like Llama, Mistral, Neural Chat, and more.

- **Image**: Official Ollama or CUDA variant
- **Port**: `11434`
- **Official Repo**: https://github.com/ollama/ollama
- **Docker Hub**: https://hub.docker.com/r/ollama/ollama
- **Use Cases**:
  - Local LLM inference without API calls
  - Private model serving
  - Integration with other services (Open WebUI, n8n)

**Quick Start**:
```bash
docker run -d --gpus=all -p 11434:11434 --name ollama ollama/ollama
```

---

### Open WebUI
**Web interface for Ollama & multiple LLM providers**

Open WebUI provides a ChatGPT-like interface for local and remote LLMs, including Ollama, OpenAI, Anthropic, and more.

- **Image**: `ghcr.io/open-webui/open-webui:cuda` (CUDA-enabled)
- **Port**: `3000`
- **Official Repo**: https://github.com/open-webui/open-webui
- **Docker Hub**: https://hub.docker.com/r/open-webui/open-webui
- **Use Cases**:
  - User-friendly chat interface for Ollama
  - Support for multiple LLM backends
  - Conversation history and knowledge base
  - Model management and settings

**Access**: `http://localhost:3000`

---

### n8n
**Workflow automation & API orchestration**

n8n is a low-code workflow automation platform for integrating services, APIs, and automating repetitive tasks.

- **Image**: `docker.n8n.io/n8nio/n8n`
- **Port**: `5678`
- **Official Repo**: https://github.com/n8n-io/n8n
- **Docker Hub**: https://hub.docker.com/r/n8nio/n8n
- **Use Cases**:
  - Workflow automation between tools
  - API orchestration and integration
  - Scheduled tasks and triggers
  - Data transformation and processing

**Access**: `http://localhost:5678`

---

### MCP Gateway
**Docker's Model Context Protocol gateway**

MCP Gateway enables communication between AI applications and tools/data sources via the Model Context Protocol. Supports LLMs to access external resources through standardized interfaces.

- **Image**: `docker/mcp-gateway`
- **Official Repo**: https://github.com/docker/mcp-gateway
- **Documentation**: https://docs.docker.com/ai/mcp-gateway/
- **Use Cases**:
  - Connect LLMs to external tools and data
  - Standardized context protocol for AI applications
  - Extensible gateway for model interactions
  - Bridge between Docker and AI models

---

### Tailscale
**Secure mesh VPN**

Tailscale creates a private mesh network between your devices, enabling secure remote access without port forwarding or complex networking setup.

- **Image**: `tailscale/tailscale:latest`
- **Official Repo**: https://github.com/tailscale/tailscale
- **Documentation**: https://tailscale.com/docs
- **Use Cases**:
  - Secure remote access to your stack
  - Private networking between devices
  - VPN without configuration hassle
  - Access Open WebUI and n8n remotely

---

## Quick Start

Clone this repository and start all services:

```bash
git clone <your-repo-url>
cd personal-stack
docker compose up -d
```

Access the services:
- **Open WebUI**: http://localhost:3000
- **n8n**: http://localhost:5678
- **Ollama**: http://localhost:11434

---

## Environment & Customization

Each service can be customized via environment variables or volume mounts. See `docker-compose.yml` for current configuration.

### Common Customizations:
- **Ollama models**: Pull models with `docker exec ollama ollama pull <model>`
- **Open WebUI settings**: Configure LLM backends via the web interface
- **n8n workflows**: Create workflows in the n8n UI
- **Tailscale auth**: Run `docker exec tailscale tailscale up` to authenticate

---

## Documentation Links

- **Ollama**: https://github.com/ollama/ollama
- **Open WebUI**: https://github.com/open-webui/open-webui
- **n8n**: https://github.com/n8n-io/n8n
- **MCP Gateway**: https://github.com/docker/mcp-gateway
- **Tailscale**: https://github.com/tailscale/tailscale

---

## License

This repository documents personal usage of open-source projects. See individual projects for their licenses.
