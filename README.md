# slow-kratos — Personal AI Stack

A containerized personal AI infrastructure stack for local LLM inference, workflow automation, and MCP-based tool integration.

> This is my home lab. For how I apply this stack in production ops workflows, see my [professional repos](https://github.com/arjkul#repos).

---

## Services Overview

| Service | Purpose |  Docs |
|---|---|---|---|---|
| [Ollama](#ollama) | Local LLM inference engine | [Repo](https://github.com/ollama/ollama) |
| [Open WebUI](#open-webui) | Web interface for Ollama & LLMs |  [Repo](https://github.com/open-webui/open-webui) |
| [n8n](#n8n) | Workflow automation & API orchestration |  [Repo](https://github.com/n8n-io/n8n) |
| [MCP Gateway](#mcp-gateway) | Docker's Model Context Protocol gateway | [Repo](https://github.com/docker/mcp-gateway) |
| [Tailscale](#tailscale) | Secure mesh VPN |  [Repo](https://github.com/tailscale/tailscale) |

---

## Why This Stack

This setup lets me:

- **Run models locally** — Llama, Mistral, Neural Chat and others via Ollama, without API costs or data leaving the machine
- **Prototype automations fast** — n8n connects to any API with minimal code; I use it to test workflow ideas before building them properly in Python
- **Experiment with MCP** — Docker's MCP Gateway gives me a local sandbox for testing Model Context Protocol integrations before deploying them in production (e.g. Claude Code + internal tools at work)
- **Access everything remotely** — Tailscale creates a private mesh so I can reach Open WebUI and n8n from anywhere without port forwarding

This is the infrastructure layer. The automation layer — where this thinking gets applied to real business problems — lives in [`ai-ops-tooling`](https://github.com/arjkul/ai-ops-tooling).

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
- **Use Cases**:
  - Workflow automation between tools
  - API orchestration and integration
  - Scheduled tasks and triggers
  - Data transformation and processing

**Access**: `http://localhost:5678`

> **Note**: n8n is where I prototype automations locally before rebuilding them as proper Python scripts for production use. See [`ai-ops-tooling`](https://github.com/arjkul/ai-ops-tooling) for the production versions.

---

### MCP Gateway

**Docker's Model Context Protocol gateway**

MCP Gateway enables communication between AI applications and tools/data sources via the Model Context Protocol.

- **Image**: `docker/mcp-gateway`
- **Official Repo**: https://github.com/docker/mcp-gateway
- **Documentation**: https://docs.docker.com/ai/mcp-gateway/
- **Use Cases**:
  - Connect LLMs to external tools and data
  - Standardized context protocol for AI applications
  - Local sandbox for MCP integration testing

> Running two instances to test different MCP server configurations in parallel.

---

### Tailscale

**Secure mesh VPN**

Tailscale creates a private mesh network between your devices, enabling secure remote access without port forwarding or complex networking setup.

- **Image**: `tailscale/tailscale:latest`
- **Official Repo**: https://github.com/tailscale/tailscale
- **Use Cases**:
  - Secure remote access to the full stack
  - Private networking between devices
  - Access Open WebUI and n8n from anywhere

---

## Quick Start

```bash
git clone https://github.com/arjkul/slow-kratos
cd slow-kratos
docker compose up -d
```

Access the services:
- **Open WebUI**: http://localhost:3000
- **n8n**: http://localhost:5678
- **Ollama API**: http://localhost:11434

---

## Environment & Customization

Each service can be customized via environment variables or volume mounts. See `docker-compose.yml` for current configuration.

### Common Customizations

- **Ollama models**: `docker exec ollama ollama pull <model>`
- **Open WebUI settings**: Configure LLM backends via the web interface
- **n8n workflows**: Create workflows in the n8n UI
- **Tailscale auth**: `docker exec tailscale tailscale up`

---

## How This Connects to Professional Work

This home stack directly informs how I build AI tooling professionally:

| Home (slow-kratos) | Production ([ai-ops-tooling](https://github.com/arjkul/ai-ops-tooling)) |
|---|---|
| Ollama + Open WebUI for local model testing | Claude API (Anthropic) for production LLM calls |
| n8n for rapid workflow prototyping | Python scripts for production automation |
| MCP Gateway (local sandbox) | Claude Code + Anthropic MCP in production |
| Tailscale for private access | Internal VPN / corporate network |

The pattern: prototype locally with open-source tools, validate the approach, then rebuild for production with the right reliability and security properties.

---

## Related Repos

- [`ai-ops-tooling`](https://github.com/arjkul/ai-ops-tooling) — Production AI automation (Claude/Gemini) for warehouse ops
- [`warehouse-ops-intelligence`](https://github.com/arjkul/warehouse-ops-intelligence) — BI system built on top of the same automation thinking
- [`pm-data-stack-templates`](https://github.com/arjkul/pm-data-stack-templates) — Frameworks including an AI tool evaluation template

---

## License

This repository documents personal usage of open-source projects. See individual projects for their licenses.
