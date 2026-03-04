# ZeronimoOS

Bitcoin full node device **Nodin** — sovereign computing made simple.

## Repositories

| Repo | Description |
|------|-------------|
| [`zeronimo-os`](https://github.com/zeronimoOS/zeronimo-os) | Nodin OS monorepo — Salon API, zeronimo-ui, zeronimo-web, fanboy, Incus containers, deploy scripts |
| [`openclaw-bot`](https://github.com/zeronimoOS/openclaw-bot) | AI research assistant Telegram bot for Bitcoin ecosystem analysis |
| [`bitqna`](https://github.com/zeronimoOS/bitqna) | Bitcoin knowledge RAG chatbot powered by FastAPI |

## Architecture

Nodin runs on ODROID-M1S with a container-based architecture (Incus):

- **Core containers**: bitcoind, Salon (REST API), EPS (Electrum Personal Server)
- **Host services**: zeronimo-ui (QML touch), zeronimo-web (React dashboard), fanboy (fan control)
- **Access**: Local touch UI, LAN web dashboard, Tor remote access

All product code lives in the [`zeronimo-os`](https://github.com/zeronimoOS/zeronimo-os) monorepo.

---

> Each repository has an `AGENTS.md` with context for AI tools and contributors.
