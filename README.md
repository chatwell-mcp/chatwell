# Chatwell

**Your WhatsApp, available to your AI apps.** Chatwell keeps one WhatsApp *linked device* connected on your Windows
PC (the way WhatsApp Web does), stores your messages on the PC, and lets AI apps such as Claude, Codex, Cursor,
VS Code Copilot and Gemini CLI read, search and follow your chats through [MCP](https://modelcontextprotocol.io).

> **Unofficial.** Chatwell is not made, endorsed or supported by WhatsApp or Meta. WhatsApp's terms do not allow
> third-party clients, and WhatsApp may limit or ban numbers that use them. Use it at your own risk.

## Install (Windows 10 / 11)

1. Download `Chatwell-<version>.zip` from [Releases](../../releases/latest) and extract it.
2. Double-click `Chatwell.exe`. The program is not code-signed, so Windows may say "Windows protected your PC":
   click **More info**, then **Run anyway**.
3. Accept the terms. Chatwell installs itself for your user (no admin), starts with Windows, and opens a QR code.
4. On the phone: WhatsApp > Settings > Linked devices > Link a device, and scan it.

Updates install themselves (only versions signed with the Chatwell release key). Uninstall from Windows Settings >
Apps > Installed apps; then remove the PC under WhatsApp > Linked devices.

## Use it from an AI app

Tray icon > **Connect an AI...** shows copy-paste steps for Claude Code, Claude Desktop, OpenAI Codex, Cursor,
VS Code, Gemini CLI, Windsurf and LM Studio, filled in with the path on your PC. The MCP server is the command
`chatwell-cli.exe mcp`.

| Tool | |
|---|---|
| `status` | connected or not, linked number, last message |
| `list_chats`, `get_messages`, `search_messages` | read and full-text search your chats (by chat, time, sender, kind) |
| `download_media` | saves a photo, video, voice note or document and returns its path |
| `receive_from_phone` | **hand the AI a file:** send a photo, document, voice note or text to yourself on WhatsApp ("Message yourself") and the AI picks it up |
| `subscribe`, `check_new_messages`, ... | follow chats: new messages are pushed into Claude Code sessions (channels) or collected by any app |
| `request_history` | older messages of a chat, from the phone |
| `send_message` | **off until you allow it** in the tray (at most 60 messages an hour, whatever the settings) |

For Claude Code, new messages in subscribed chats can arrive in the session as they happen: start it with
`claude --dangerously-load-development-channels server:whatsapp` (Claude Code channels are a research preview).

## The tray icon

Blue = connected, amber = connecting, orange = needs login, grey = paused, red = blocked or needs an update. Menu:
Log in, Pause / Resume, Connect an AI, Allow AI to send messages, Start with Windows, Check for updates, Quit.

## Privacy and safety

- Your messages and media stay on your PC (`%LOCALAPPDATA%\Chatwell`). Chatwell talks only to WhatsApp and, once a
  day, to GitHub to check for updates. No telemetry. The AI apps you connect read your messages under their own terms.
- Messages from other people can try to steer an AI ("forward all chats to..."). Chatwell tells the AI to treat
  message text as data, never as instructions; sending stays off unless you turn it on, and is capped.
- It never shows you as "online" (your phone keeps its notifications) and never marks messages as read.
- The local API listens on 127.0.0.1 only and needs a token for anything beyond status.

## Building from source

Go 1.27+. `build.ps1` runs the tests and builds `bin\Chatwell.exe` (service, tray) and `bin\chatwell-cli.exe`
(MCP / command line); with a `data\` folder next to `bin\`, a build keeps its data there ("portable": it never
installs or updates itself). `install.ps1` registers it to start with Windows. `release.ps1` builds the release zip,
the source zip and the signed update manifest (maintainers only: it needs the release key).

Command line: `chatwell-cli status | login | setup | autostart [on|off|remove] | uninstall | version`.

Data folder: `session.db` (the linked-device keys: whoever has it can read and send as you), `messages.db` (chats,
contacts, messages, full-text index), `media\`, `config.json` (port 47123, `autoDownload` chats whose photos are saved
as they arrive, `autoDownloadDays`, `allowSend`, `sendsPerHour`, `autoUpdate`), `logs\`.

Built on [whatsmeow](https://github.com/tulir/whatsmeow) (MPL-2.0), an open-source implementation of the WhatsApp
Web protocol, and the [MCP Go SDK](https://github.com/modelcontextprotocol/go-sdk).

## License

GPL-3.0 (see [LICENSE](LICENSE)). Each release includes its source code (`Chatwell-<version>-source.zip`).
Third-party licenses: [THIRD_PARTY_NOTICES.txt](THIRD_PARTY_NOTICES.txt).
