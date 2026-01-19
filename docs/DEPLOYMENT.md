# Deployment Guide

## System Requirements

- **OS**: Linux (Ubuntu/Debian recommended)
- **Architecture**: amd64
- **Dependencies**: None (binary is static)

## 1. Installation

1. Clone the repository or download the release.
   ```bash
   git clone https://github.com/Belnsah3/lumeai-platform.git
   cd lumeai-platform
   ```
2. Copy the binary `lumeai-core` and `lumeai-management-center` assets (usually deployed to `static/`).

## 2. Systemd Service (Linux)

You can run LumeAi as a background service using `systemd`.

1. Create a service file (or use the provided `lumeai.service`):
   ```ini
   [Unit]
   Description=LumeAi Platform - Advanced AI Proxy
   Documentation=https://github.com/Belnsah3/lumeai-platform
   After=network.target network-online.target
   Wants=network-online.target

   [Service]
   Type=simple
   User=your_user
   Group=your_group
   WorkingDirectory=/path/to/lumeai
   ExecStart=/path/to/lumeai/lumeai-core
   Restart=always
   RestartSec=5
   Environment=HOME=/home/your_user

   [Install]
   WantedBy=multi-user.target
   ```
2. Install and start:
   ```bash
   sudo ln -sf /path/to/lumeai/lumeai.service /etc/systemd/system/lumeai.service
   sudo systemctl daemon-reload
   sudo systemctl enable lumeai
   sudo systemctl start lumeai
   ```

## 3. Nginx Reverse Proxy (Optional)

It is recommended to run LumeAi behind Nginx for SSL termination and static file serving.

```nginx
server {
    listen 80;
    server_name panel.lumeai.ru;

    # Serve the frontend
    location / {
        root /path/to/lumeai/static;
        try_files $uri /index.html;
    }

    # Proxy the Management API
    location /v0/management/ {
        proxy_pass http://127.0.0.1:8317/v0/management/;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
    
    # Proxy the AI API
    location /v1/ {
        proxy_pass http://127.0.0.1:8317/v1/;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```
