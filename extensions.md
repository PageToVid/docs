---
title: Extensions
nav_order: 3.5
description: "PageToVid — Capture for Chrome and PageToVid Studio for VS Code: capture pages, film your app behind its login, and let Claude Code plan the flows worth filming."
---

# Extensions
{: .no_toc }

Two free extensions bring PageToVid to the browser and the editor. They work on their own and work
best together: **VS Code writes the capture plan from your code, Chrome records it**, and each recorded
step becomes a scene.
{: .fs-5 .fw-300 }

| | Install | Product page |
|---|---|---|
| **PageToVid — Capture** for Chrome | [Chrome Web Store](https://chromewebstore.google.com/detail/pagetovid-%E2%80%94-capture/oaiajdabfjpklohkinnacldlojbnjemd) | [pagetovid.com/extension/chrome](https://pagetovid.com/extension/chrome) |
| **PageToVid Studio** for VS Code, Cursor, Windsurf, VSCodium | [VS Code Marketplace](https://marketplace.visualstudio.com/items?itemName=pagetovid.pagetovid-capture) · [.vsix](https://pagetovid.com/extension/vscode) | [pagetovid.com/extension/vscode](https://pagetovid.com/extension/vscode) |

1. TOC
{:toc}

---

## Chrome

A side panel that captures everything a video needs from the page you are on, and sends it to your
media bank. Nothing leaves your browser until you press **Send**.

### Set up

1. Add the extension from the [Chrome Web Store](https://chromewebstore.google.com/detail/pagetovid-%E2%80%94-capture/oaiajdabfjpklohkinnacldlojbnjemd).
2. Sign in on [pagetovid.com](https://pagetovid.com) in the same browser. The extension connects by itself — no key to paste.
3. Open the side panel from the toolbar icon, or press **Alt+Shift+P**.

### What it captures

| | |
|---|---|
| **Create a video from this page** | Opens PageToVid with the page's address filled in, plus a brief you write. |
| **Screencasts** | The tab recorded with a dot, ring or spotlight cursor in your colour, click ripples included, as an MP4. |
| **Full-page screenshots** | The whole scrollable page in one image, sticky headers held in place. |
| **Elements, with their CSS** | Click a button, card or section: the shot is cropped to it, with its background, radius, font and shadow. |
| **The page's own images** | Every photo and illustration at its real size, sent to your media bank instead of screenshotted. |
| **Brand kit** | Colours, fonts, radius, button styles, logo and theme, sent to PageToVid or copied as JSON. |
| **Logged-in capture** | Your signed-in session handed to the cloud recorder, so the film shows your real app. |
| **Flows** | Bind to a tab and every page you open is captured as one route; flows planned in VS Code are recorded step by step. |
| **Auto capture** | A list of pages, or a map of the site, each banked as a full-page shot. |
| **AI reviews** | Brief, UX, copy, accessibility and conversion reviews on your own Gemini key — the image goes from your browser to Google, never through us. |

### Film your app behind its login

```text
Extension (your browser, logged in)
  └─ export cookies + localStorage
       └─ POST → PageToVid  (Playwright storageState)
            └─ headless Chromium loads the app as you
                 └─ record → render → MP4
```

A session is sent only when you press its button, is stored encrypted, is scoped to one origin and
expires within 24 hours. Once sent, it covers every render of that site — from the website, your AI
assistant or the API. Filming behind a login is on the **Scale plan and up**; every other capture is
free.

{: .warning }
A session grants access to your account. Only send sessions of accounts that are yours.

---

## VS Code

**PageToVid Studio** turns a project folder into a production seat: it connects the folder to its
PageToVid site and to Claude Code, and the editor becomes where the videos are directed. It never
captures anything itself and never runs your workspace code.

### Set up

1. Install from the [Marketplace](https://marketplace.visualstudio.com/items?itemName=pagetovid.pagetovid-capture)
   (Cursor, Windsurf and VSCodium: download the `.vsix` from [the extension page](https://pagetovid.com/extension/vscode)).
2. Command Palette → **PageToVid: Connect** and approve in your browser. The key comes back to the
   editor and stays in VS Code's secret storage.
3. Pick the site this folder belongs to.
4. **PageToVid: Install studio pack**, then start `claude` from the integrated terminal and approve
   the `pagetovid` server once. The `.mcp.json` it writes never contains your key.
5. Product behind a sign-in? **PageToVid: Connect a login for screencasts** (Scale plan and up).

### The slash commands

Every command previews before it spends a credit; nothing renders until you say so.

| Command | What it does |
|---|---|
| `/pagetovid-studio` | Checks the whole seat — credits, site, login, plan, shows — and says what is missing. Free. |
| `/pagetovid-capture-plan` | Reads the codebase and writes the flows worth recording; Chrome records them. |
| `/pagetovid-show` | Sets up a recurring show from what your repo publishes, and previews the first run. |
| `/pagetovid-format` | Writes or revises a video format, and previews a real episode before saving it. |
| `/pagetovid-howto` | Turns your docs into how-to videos filmed on the product. |
| `/pagetovid-assets` | Finds the repo's logos and product images and tells you which ones to send. |

The slash commands need the Claude Code extension or the `claude` CLI.

---

## Questions and bugs

- **Something broken?** [Open a bug report](https://github.com/PageToVid/docs/issues/new?template=bug_report.yml)
  and choose *Browser extension* or *VS Code extension*. Include the extension's version, never a key.
- **An idea?** [Open a feature request](https://github.com/PageToVid/docs/issues/new?template=feature_request.yml).
- **Security issue?** Report it [privately](https://github.com/PageToVid/docs/security/advisories/new).
