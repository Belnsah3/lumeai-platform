# Configuration Guide

The main configuration file is `config.yaml`. This file controls network settings, authentication, and integrations.

## 1. Network Settings

```yaml
# Host address to bind to. "0.0.0.0" opens access to the network. "127.0.0.1" for local only.
host: "0.0.0.0"
# Port to listen on.
port: 8317
```

## 2. File Paths

```yaml
# Directory to store OAuth tokens (e.g. Google/Antigravity credentials).
auth-dir: "auths"
```

## 3. Proxy API Keys

These keys are used by clients (VS Code, Cursor, etc.) to authenticate requests to the proxy.

```yaml
api-keys:
  - "sk-lumeai_be1lnash3"
  - "sk-my-client-key"
```

## 4. Web Management Panel

Settings for the `lumeai-management-center` web interface.

```yaml
remote-management:
  allow-remote: true         # Allow access from other IPs
  secret-key: hashed_secret  # Password hash (bcrypt)
  disable-control-panel: false
  panel-github-repository: "https://github.com/Belnsah3/lumeai-platform"
```

## 5. TLS / SSL

Native TLS support. Usually, it's better to use Nginx as a reverse proxy instead.

```yaml
tls:
  enable: false
  cert: ""
  key: ""
```

## 6. Advanced Settings

```yaml
debug: false
logging-to-file: true        # Save logs to 'logs/' directory
incognito-browser: true      # Open browser automatically on start (desktop mode)
routing:
  strategy: "round-robin"    # Load balancing strategy

# Fallback behaviors when quota is exceeded
quota-exceeded:
  switch-project: true
  switch-preview-model: true

usage-statistics-enabled: true
request-retry: 10
ws-auth: false
force-model-prefix: true     # Enforce model naming conventions
```

## 7. Model Providers & Compatibility

Configure upstream providers here.

```yaml
openai-compatibility:
  - name: openrouter.ai
    base-url: https://openrouter.ai/api/v1
    api-key-entries:
      - api-key: sk-or-...
    models:
      - name: remote-model-name
        alias: "local-alias"
```
