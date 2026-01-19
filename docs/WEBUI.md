# Web UI Guide

The **LumeAi Management Center** is the graphical interface for controlling your proxy.

## Access

By default, the panel is available at:
`http://localhost:8317/management.html`

If you are using Nginx as configured in the Deployment Guide, it maps to your domain root (e.g. `https://panel.lumeai.ru`).

## Features

### Dashboard
Provides an overview of:
- Server status
- Active AI Providers
- Recent activity / usage

### API Keys
Manage the keys (`sk-lumeai...`) that you distribute to your users or clients.

### AI Providers
Configure upstream API keys for services like:
- OpenAI
- Anthropic (Claude)
- Google (Gemini)
- OpenRouter, DeepSeek, etc.

### Usage Statistics
View charts and tables showing token usage and costs over time.

### Logs Viewer
Real-time inspection of requests passing through the proxy. Useful for debugging prompt injection or errors.
