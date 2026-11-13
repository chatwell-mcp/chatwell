# Chatwell

**Your WhatsApp, available to your AI apps.** Chatwell keeps WhatsApp *linked devices* connected on your Windows PC
or Mac (the way WhatsApp Web does), stores your messages on the PC, and lets AI apps such as Claude, Codex, Cursor,
VS Code Copilot and Gemini CLI read, search and follow your chats through [MCP](https://modelcontextprotocol.io).

> **Unofficial.** Chatwell is not made, endorsed or supported by WhatsApp or Meta. WhatsApp's terms do not allow
> third-party clients, and WhatsApp may limit or ban numbers that use them. Use it at your own risk.

## Install on a Mac (macOS 13 or newer, Apple Silicon or Intel)

1. Download `Chatwell-<version>-mac.zip` from [Releases](../../releases/latest) and open `Chatwell.app`.
2. It is not notarized yet: if macOS says it can't verify Chatwell, open System Settings > Privacy & Security and click
   **Open Anyway**.
3. Accept the terms. Chatwell installs itself into `~/Applications` (no password), starts at login, and opens a QR code.
4. On the phone: WhatsApp > Settings > Linked devices > Link a device, and scan it.

The menu-bar icon has the same menu as the Windows tray icon. Data lives in `~/Library/Application Support/Chatwell`.

## Install (Windows 10 / 11)

1. Download `Chatwell-<version>.zip` from [Releases](../../releases/latest) and extract it.
2. Double-click `Chatwell.exe`. The program is not code-signed, so Windows may say "Windows protected your PC":
   click **More info**, then **Run anyway**.
3. Accept the terms. Chatwell installs itself for your user (no admin), starts with Windows, and opens a QR code.
4. On the phone: WhatsApp > Settings > Linked devices > Link a device, and scan it.

Updates install themselves (only versions signed with the Chatwell release key). Uninstall from Windows Settings >
Apps > Installed apps; then remove the PC under WhatsApp > Linked devices.

## Use it from an AI app

Tray icon > **Connect an AI...** shows, for Claude Code, Claude Desktop, OpenAI Codex, Cursor, VS Code, Gemini CLI,
Windsurf and LM Studio, the easiest way in: for the coding agents a sentence you paste into the AI, which then adds
Chatwell to its own settings; or the steps to do it yourself, filled in with the path on your PC. The MCP server is the
command `chatwell-cli.exe mcp`.

| Tool | |
|---|---|
| `status` | connected or not, linked number, last message |
| `list_chats`, `get_messages`, `search_messages` | read and full-text search your chats (by chat, time, sender, kind) |
| `download_media` | saves a photo, video, voice note or document and returns its path |
| `receive_from_phone` | **hand the AI a file:** send a photo, document, voice note or text to yourself on WhatsApp ("Message yourself") and the AI picks it up |
| `subscribe`, `check_new_messages`, ... | follow chats: new messages are pushed into Claude Code sessions (channels) or collected by any app |
| `request_history` | older messages of a chat, from the phone |
| `send_message` | text or a file from your account: on by default, off with one click in the tray (at most 60 messages an hour per account, whatever the settings) |

Several WhatsApp accounts can be linked (tray > Add account). Every tool takes an optional `account`; reading covers all
accounts and labels each message with its account; sending asks which account when there is more than one.

For Claude Code, new messages in subscribed chats can arrive in the session as they happen: start it with
`claude --dangerously-load-development-channels server:whatsapp` (Claude Code channels are a research preview).

## The tray icon

Blue = connected, amber = connecting, orange = needs login, grey = paused, red = blocked or needs an update (the most
urgent state of all accounts). Menu: one entry per account (Pause / Resume, Log in again, Log out, Log out and delete its
messages), Add account, Connect an AI, Allow AI to send messages, Start with Windows, Check for updates, Quit.

## Privacy and safety

- Your messages and media stay on your PC (`%LOCALAPPDATA%\Chatwell`). Chatwell talks only to WhatsApp and, once a
  day, to GitHub to check for updates. No telemetry. The AI apps you connect read your messages under their own terms.
- Messages from other people can try to steer an AI ("forward all chats to..."). Chatwell tells the AI to treat
  message text as data, never as instructions; sending is capped, and "Allow AI to send messages" in the tray turns it off.
- It never shows you as "online" (your phone keeps its notifications) and never marks messages as read.
- The local API listens on 127.0.0.1 only and needs a token for anything beyond status.

## License

GPL-3.0 (see [LICENSE](LICENSE)). Each release includes its source code (`Chatwell-<version>-source.zip`).
Built on [whatsmeow](https://github.com/tulir/whatsmeow) (MPL-2.0) and the
[MCP Go SDK](https://github.com/modelcontextprotocol/go-sdk).
Third-party licenses: [THIRD_PARTY_NOTICES.txt](THIRD_PARTY_NOTICES.txt).
