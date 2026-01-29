# Moltbot Docker Image

Pre-built Docker image for [Moltbot](https://github.com/moltbot/moltbot) — run your AI assistant in seconds without building from source.

## One-Line Install (Recommended)

```bash
curl -fsSL https://raw.githubusercontent.com/phioranex/moltbot-docker/main/install.sh | bash
```

This will:
- ✅ Check prerequisites (Docker, Docker Compose)
- ✅ Download necessary files
- ✅ Pull the pre-built image
- ✅ Run the onboarding wizard
- ✅ Start the gateway

### Install Options

```bash
# Just pull the image (no setup)
curl -fsSL https://raw.githubusercontent.com/phioranex/moltbot-docker/main/install.sh | bash -s -- --pull-only

# Skip onboarding (if already configured)
curl -fsSL https://raw.githubusercontent.com/phioranex/moltbot-docker/main/install.sh | bash -s -- --skip-onboard

# Don't start gateway after setup
curl -fsSL https://raw.githubusercontent.com/phioranex/moltbot-docker/main/install.sh | bash -s -- --no-start

# Custom install directory
curl -fsSL https://raw.githubusercontent.com/phioranex/moltbot-docker/main/install.sh | bash -s -- --install-dir /opt/moltbot
```

## Manual Install

### Quick Start

```bash
# Pull the image
docker pull ghcr.io/phioranex/moltbot-docker:latest

# Run onboarding (first time setup)
docker run -it --rm \
  -v ~/.clawdbot:/home/node/.clawdbot \
  -v ~/clawd:/home/node/clawd \
  ghcr.io/phioranex/moltbot-docker:latest onboard

# Start the gateway
docker run -d \
  --name moltbot \
  --restart unless-stopped \
  -v ~/.clawdbot:/home/node/.clawdbot \
  -v ~/clawd:/home/node/clawd \
  -p 18789:18789 \
  ghcr.io/phioranex/moltbot-docker:latest gateway start --foreground
```

### Using Docker Compose

```bash
# Clone this repo
git clone https://github.com/phioranex/moltbot-docker.git
cd moltbot-docker

# Run onboarding
docker compose run --rm moltbot-cli onboard

# Start the gateway
docker compose up -d moltbot-gateway
```

## Configuration

During onboarding, you'll configure:
- **AI Provider** (Google AI, GitHub Copilot, Anthropic, etc.)
- **Channels** (Telegram, WhatsApp, Discord, etc.)
- **Gateway settings**

Config is stored in `~/.clawdbot/` and persists across container restarts.

## Available Tags

| Tag | Description |
|-----|-------------|
| `latest` | Latest stable release |
| `vX.Y.Z` | Specific version |
| `main` | Latest from main branch (may be unstable) |

## Volumes

| Path | Purpose |
|------|---------|
| `/home/node/.clawdbot` | Config and session data |
| `/home/node/clawd` | Agent workspace |

## Ports

| Port | Purpose |
|------|---------|
| `18789` | Gateway API + Dashboard |

## Links

- [Moltbot Docs](https://docs.molt.bot)
- [Moltbot GitHub](https://github.com/moltbot/moltbot)
- [Discord Community](https://discord.com/invite/clawd)

## YouTube Tutorial

📺 Watch the installation tutorial: [Coming Soon]

## License

This Docker packaging is provided by [Phioranex](https://phioranex.com).
Moltbot itself is licensed under its own terms — see the [original repo](https://github.com/moltbot/moltbot).
