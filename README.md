# Frontmatters Telegram

> Fork of [`@llblab/pi-telegram`](https://github.com/llblab/pi-telegram) (which is itself a fork of [`badlogic/pi-telegram`](https://github.com/badlogic/pi-telegram) by Mario Zechner). Rebranded for the Frontmatters stack. See [`LICENSE`](./LICENSE) for attribution.

**Telegram DM bridge for Pi.** Turns a private Telegram chat into a mobile operator surface for live Pi sessions. Send prompts from your phone, watch Pi work, get final replies + artifacts delivered — without running a second bot loop or remote terminal.

## Install (local fork)

```bash
pi install ./path/to/pi-frontmatters-telegram
# or absolute:
pi install /absolute/path/to/pi-frontmatters-telegram
```

## Configure

### 1. Telegram bot

Create your own bot via [@BotFather](https://t.me/BotFather) — `/newbot`, pick a name and username, copy the bot token.

Store the token in your macOS Keychain via [secrets-helper](https://github.com/frontmatters/secrets-helper):

```bash
secrets add dev-config TELEGRAM_BOT_TOKEN "<your-bot-token>"
```

### 2. Pi setup

Start Pi, then run:

```text
/telegram-setup
```

Paste the bot token when prompted. Config is stored in `~/.pi/agent/telegram.json` (mode 0o600).

> Tip — prefill from keychain:
> ```bash
> TELEGRAM_BOT_TOKEN=$(secrets get dev-config TELEGRAM_BOT_TOKEN) pi
> ```
> `/telegram-setup` will pick it up automatically.

### 3. Connect this Pi session

```text
/telegram-connect
```

The connected Pi instance owns Telegram polling.

### 4. Pair your Telegram account

Open the DM with **your bot** in Telegram and send:

```text
/start
```

The first Telegram user to message the bot becomes the allowed owner. Other users are ignored.

## Commands

| In Pi TUI                  | Purpose                                  |
| -------------------------- | ---------------------------------------- |
| `/telegram-setup`          | Configure token                          |
| `/telegram-connect`        | Start polling in this session            |
| `/telegram-disconnect`     | Stop polling in this session             |
| `/telegram-status`         | Check current state                      |

| In Telegram DM             | Purpose                                  |
| -------------------------- | ---------------------------------------- |
| `/start`                   | Pair / open menu                         |
| `/compact`                 | Compact current session                  |
| `/next`                    | Force next turn                          |
| `/continue`                | Queue continue prompt                    |
| `/abort`                   | Abort Pi                                 |
| `/stop`                    | Abort Pi + clear queue                   |

## Differences from upstream

This fork:

- Removed upstream artifacts (`AGENTS.md`, `BACKLOG.md`, `CHANGELOG.md`, `banner.png`, `.github/`, `.agents/`).
- Added explicit `LICENSE` with attribution to both upstream authors.
- Rebranded user-visible strings ("Pi Telegram" → "Frontmatters").
- Made the package `private: true` (local use only, not published).
- Kept the singleton lock key `@llblab/pi-telegram` to remain compatible with upstream's locking semantics if both are ever installed.

## Compatibility

Built and tested against `@earendil-works/pi-coding-agent@0.80.x`. Should work with any 0.80+ release that exposes the same extension API.

## License

MIT — see [`LICENSE`](./LICENSE).
