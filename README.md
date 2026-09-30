# EMS — explain me shit

A small macOS menu bar app. Select some text anywhere — an editor, a browser, a database
client — press **⌥⌘E**, and a floating panel explains it in plain language. Press **⌥⌘S** to
drag a box on screen and explain a screenshot instead. You can ask follow-up questions in the
same panel.

What it explains is set by a **template** — a named instruction. Five ship built in (SQL, maths,
code, driving theory, plain English), all editable, and you can add your own.

**[⬇ Download the latest version](https://github.com/vadostuta/ems-releases/releases/latest)**

Requires macOS 14 (Sonoma) or newer. Runs on both Apple Silicon and Intel Macs.

---

## Setup — about three minutes

This is a personal project, not an App Store app, so a few steps are manual.

### 1. Install

Unzip and drag **EMS.app** into your **Applications** folder.

### 2. Get past the security warning

macOS blocks apps that aren't from the App Store or a paid Apple developer account. This is
neither, so you'll get a warning that the app "is damaged" or can't be opened. It isn't damaged —
that's just what macOS says about software it can't trace to a paid developer account.

**Easiest — Terminal.** Paste this and press Enter:

```bash
xattr -dr com.apple.quarantine /Applications/EMS.app
```

Nothing will appear to happen. That's correct. Now open the app normally.

**Or, without Terminal.** Double-click the app, let it get blocked, then go to
**System Settings → Privacy & Security**, scroll down, and click **Open Anyway**.

### 3. Grant two permissions

The app has no Dock icon — look for the **brain icon in the menu bar**, then open
**Setup Guide…**, which walks through the rest and has the buttons for both permissions.

- **Accessibility** — lets EMS read whatever text you currently have selected, by simulating ⌘C.
- **Screen Recording** — only for the ⌥⌘S screenshot hotkey.

After granting Screen Recording you may need to quit EMS and reopen it.

### 4. Add a free AI key

EMS has no AI of its own — it uses *your* account with a provider, so nobody is paying for anyone
else's usage. **Groq is free, takes a minute, and needs no credit card:**

1. Go to **https://console.groq.com/keys**
2. Sign in with Google or GitHub
3. Create a key and copy it — it's shown only once, and starts with `gsk_`

Paste it into the setup window and press Save. The model list fills in automatically.

*Alternative:* [Google Gemini](https://aistudio.google.com/apikey) is also free and can read
screenshots, which most Groq models can't. See the privacy note below.

---

## What EMS sends, and where

- **What you explain** goes to whichever provider you picked, using your own key. That's the point
  of the app, but it means the selected text or screenshot leaves your Mac. Don't point it at
  anything confidential without thinking about it. On **Google Gemini's free tier specifically,
  Google may use what you send to train their models** — Groq and Anthropic don't.
- **Once a day EMS asks GitHub whether a newer version exists.** That tells GitHub your IP address
  and macOS version, the same as visiting any web page. Nothing about what you explain is
  included. Turn it off in **Settings → Check for new versions automatically**.
- **Nothing else leaves your Mac.** Your key is in the macOS Keychain; history and templates are
  stored locally.

---

## Updating

EMS tells you when a new version is out and keeps a row in the menu until you update. Installing
is manual: download the new zip and drag it over the old app, replacing it. Your key, templates
and history all survive.

---

## If something goes wrong

| Problem | Fix |
|---|---|
| "Select some text first" | Accessibility permission isn't granted, or nothing was selected |
| Screenshot hotkey does nothing | Grant Screen Recording, then restart EMS |
| "can't read images" | Your model is text-only — pick one marked ◉ in Settings, or use Gemini |
| "No API key set" | Reopen Settings and check the key saved |
| Nothing happens at all | There's no Dock icon by design. Look for the brain icon in the menu bar |
| Want the setup steps again | Brain icon → **Setup Guide…** |
