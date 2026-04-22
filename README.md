# buildstream-dashboard

A live web dashboard for monitoring [BuildStream](https://buildstream.build/) builds.

![screenshot placeholder](screenshot.png)

## Features

- Live progress bar with color-coded segments: cached · pulled · built · active · failed
- Active jobs panel with per-job elapsed timers
- Failures panel with clickable links to build logs
- Recent log tail with color-coded status lines
- Run / Stop build button
- Mobile-friendly responsive layout
- Accessible via [Tailscale Serve](https://tailscale.com/kb/1312/serve) + Caddy for HTTPS

## Usage

```bash
python3 bst-dashboard.py
```

Then open [http://localhost:8765](http://localhost:8765).

The dashboard tails `/var/tmp/aurora-build.log` by default. Set `LOG_FILE` at the top of the script to point at your build log.

### Tailscale + Caddy (optional, for remote access)

Tailscale Serve proxies `/` → `http://127.0.0.1:9000`. A Caddy instance on port 9000 strips the `/bst` prefix and forwards to `host.containers.internal:8765`. The dashboard handles both paths natively.

## Log format

Expects the BuildStream 2 log format:

```
[HH:MM:SS][HASH][   build:element.bst] STATUS message
```

and the unstructured `Pipeline Summary` block emitted at build end.

## Requirements

- Python 3.8+ (stdlib only)
- BuildStream 2

## License

MIT
