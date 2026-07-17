# CDP Images

Docker image for headless Chromium, published to [Docker Hub](https://hub.docker.com/r/brightsec/nextools-chrome) and AWS ECR.

## Image

`brightsec/nextools-chrome` - Multi-arch (amd64 + arm64) headless Chromium for CDP automation.

- Base: `debian:bookworm-slim`
- Browser: Chromium from Debian apt (pinned version)
- Mode: `--headless=new`
- Port: 9222 (CDP)

## Usage

```bash
docker run -d -p 9222:9222 brightsec/nextools-chrome
curl http://localhost:9222/json/version
```

## Build locally

```bash
cd chromium
make build-local
make test
```
