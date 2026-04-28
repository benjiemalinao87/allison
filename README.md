# Allison

**Your AI sidekick that lives in your Mac's menu bar — sees what you see, hears what you ask, and answers out loud.**

Hold a hotkey, ask anything. Allison takes a screenshot, sends it to Claude, and replies in your ear. She can also point — literally point, with an animated blue cursor that flies across your screen — at the exact button, paragraph, or pixel you're asking about.

[Download Allison](https://github.com/benjiemalinao87/allison/releases/latest/download/Allison.dmg) · Notarized by Apple · macOS 14.2+

---

## What you can do with Allison

Allison is a general-purpose copilot that turns your *whole computer* into context. Here's what people use her for:

### Learn anything in real time
You're using a tool you've never seen before. Press Control+Option, ask *"what is this whole left panel doing?"* — Allison reads the screen, explains it, and points at the controls she's describing.

### Code reviews while you code
Open a tricky function. Ask *"what's wrong with this loop?"* — Allison reads your editor, spots the bug, and walks you through the fix.

### Document & PDF analysis without uploads
Open the doc on your screen. Ask *"summarize the risks section,"* *"compare clause 4 with clause 12,"* *"find anything that contradicts page 3."* No upload, no copy-paste, no separate web app.

### Visual debugging
Stuck on a layout? *"Why is this button overlapping the form?"* Allison sees your CSS and your rendered page side-by-side and tells you which value to change.

### Hands-free flow with Conversation Mode
Toggle Conversation Mode and Allison auto-listens after every reply. Have a real back-and-forth dialogue while you work — no clicking, no hotkey, just talk. Auto-quiets after a stretch of silence.

### Capture knowledge into Obsidian
Pick a notes folder once. Every conversation becomes a Markdown note in that folder, organized and ready to link from your second brain.

### Connect your own tools
Allison's HTTP Context Tool lets you wire her up to *any* HTTPS API you control — your CRM, your monitoring dashboard, your internal stats endpoint. Tell her what trigger phrases to listen for ("check inventory for X") and she'll fetch the data and feed it to Claude as context. Build your own copilot for your stack.

### Email summaries to your future self
At the end of a conversation, Allison can generate a clean Markdown summary and email it to you (or anyone you choose). Wake up tomorrow with yesterday's brainstorm in your inbox.

---

## Features

| Capability | Detail |
|------------|--------|
| **Voice in** | Push-to-talk with Control + Option, real-time streaming transcription via AssemblyAI |
| **Voice out** | Natural-sounding speech via ElevenLabs (`eleven_flash_v2_5`) |
| **Vision** | Multi-monitor screenshots via ScreenCaptureKit — Allison sees every connected display |
| **Models** | Claude Sonnet 4.6 (default, fast and sharp) or Claude Opus 4.6 (deeper reasoning) — toggle from the panel |
| **Pointing** | Claude can target UI elements with `[POINT:x,y:label:screenN]` tags — animated blue cursor flies to the spot on the right monitor |
| **Conversation Mode** | Hands-free continuous dialogue with auto-endpointing |
| **Notes** | One Markdown note per conversation, written to a folder of your choice (Obsidian-friendly) |
| **HTTP Tools** | Wire your own HTTPS APIs in as on-demand context for Claude |
| **Email summaries** | Optional Markdown summary of a conversation, delivered via email |
| **Auto-updates** | Silent in-app updates via Sparkle (EdDSA-signed, Apple-notarized) |

---

## Install

1. **Download** → [Allison.dmg](https://github.com/benjiemalinao87/allison/releases/latest/download/Allison.dmg)
2. **Open** the DMG, drag **Allison** to **Applications**
3. **Launch** from Spotlight (Cmd+Space → "Allison")
4. Grant the four permissions Allison asks for: Microphone, Screen Recording, Accessibility, Input Monitoring (these are macOS-required for voice + screen-awareness)
5. **Sign up** with your email — you'll receive a 6-digit code, enter it, and you're in
6. **Hold ⌃⌥** (Control + Option) and start talking

The Allison icon lives in your menu bar — there's no dock icon and no main window. Click the menu bar icon any time to open the panel.

---

## Activation & quotas

Allison is in beta, so signups are gated by either an invite code or a direct signup with a smaller daily quota.

| Path | Daily turns | Bonus | How to get it |
|------|-------------|-------|---------------|
| **Direct signup** | 20 chat turns/day | — | Just download Allison and enter your email |
| **Invited signup** | **50 chat turns/day** | **+10 welcome bonus** | A friend sends you their personal invite code from inside Allison |

Once you're in, you can mint your own invite codes from the panel. Every friend who activates with your code gives **you +10 bonus turns** *and* gives them +10 — so the more you share Allison, the more she works for you.

Bonus turns roll over forever. Daily turns reset at midnight UTC.

---

## How Allison works

**The whole pipeline**, top to bottom:

1. You hold **⌃⌥** (or Conversation Mode auto-listens)
2. **AssemblyAI** transcribes your voice in real time — streaming, low latency
3. **ScreenCaptureKit** grabs labeled screenshots of every connected display
4. The transcript + screenshots are sent to **Claude** (via a Cloudflare Worker proxy — no API keys ever ship in the app)
5. Claude streams a response. Inline `[POINT:...]` tags get parsed out and turned into cursor animations on the right monitor
6. **ElevenLabs** speaks the response while it streams
7. Transcripts, summaries, and notes are saved locally — your data stays on your Mac

### Privacy

- **Zero background recording.** Allison only takes a screenshot when you press the hotkey (or when Conversation Mode is actively running).
- **No API keys in the app.** Everything routes through a Cloudflare Worker that holds the keys server-side. The app only ever has an opaque session token in your Keychain.
- **Your screenshots aren't stored.** The Worker logs request metadata (sizes, byte counts) but never the screenshot images themselves.
- **Local notes & sessions.** Markdown notes and conversation transcripts live in folders on *your* disk, under your control.

---

## System requirements

- **macOS 14.2** (Sonoma) or later
- **Apple Silicon or Intel** — universal binary, runs natively on both
- **Internet connection** for Claude / TTS / STT
- **Microphone**, **Screen Recording**, **Accessibility**, and **Input Monitoring** permissions

---

## Updates

Once installed, Allison checks for updates automatically (typically once a day on launch). When a new version is available you'll see a small "Update available" prompt — one click to install. Updates are EdDSA-signed and Apple-notarized end-to-end.

To check manually: click the Allison menu bar icon, then look for the version line in the panel.

---

## Releases

See [Releases](https://github.com/benjiemalinao87/allison/releases) for the changelog and direct downloads of every version.

---

## Feedback

Found a bug? Have an idea? Want a feature? The Allison panel has a **DM me** button that opens a feedback channel directly to the developer. Every message gets read.

---

## Built with

- **SwiftUI + AppKit** (menu bar panel, multi-monitor cursor overlay)
- **Claude** (Anthropic) — Sonnet 4.6 / Opus 4.6 vision + streaming
- **AssemblyAI** (`u3-rt-pro` real-time streaming model)
- **ElevenLabs** (`eleven_flash_v2_5`)
- **Cloudflare Workers + D1** (proxy, auth, quotas, referrals)
- **Sparkle** (signed auto-updates)
- **ScreenCaptureKit** (multi-monitor capture)

---

*Allison is in beta. Quotas, features, and the activation flow may evolve. Existing installs auto-update silently. If you hit a wall, ping the DM button — fixes ship fast.*
