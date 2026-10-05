# Connect your AI app to Familiar: the full setup guide

> The in-app **MCP Setup Wizard** (Module Settings → Familiar → the **MCP / Subs** tab) shows these same steps with your secret already filled in; this guide is the linkable, printable, give-it-to-your-AI version. Vendor navigation labels and commands verified against official docs 2026-08-24, Muse Code 2026-10-01 (sources listed at the bottom); app menus change often, so if a label differs slightly on your machine, look for the closest match.

**What you'll get:** your Claude, ChatGPT, Google, or SuperGrok subscription, or your Meta account in Muse Code, driving your Foundry game through Familiar's 230 tools. The AI itself needs no API key; voice, images and other media still need their own provider keys ([What works where](#what-works-where)). Claude Desktop and apps Familiar doesn't recognize start with [a smaller set](#which-tools-your-app-loads) that leaves those media tools out until one `FAMILIAR_TOOL_BUNDLES` line brings them in; the built-in chat and the on-demand apps in this guide have them without it.

**How it works, in one paragraph.** Familiar ships a small helper program (the npm package `familiar-vtt`) that connects your AI app to your Foundry world. You never start it yourself. You tell your AI app about it once, and the app starts and stops it automatically from then on. The setup below is exactly that one-time introduction.

**Three ways to get through this guide:**

1. **Do it yourself.** Pick your app's section below and follow it step by step. Muse Code is the last one, Part 13.
2. **Let an AI talk you through it.** Every wizard card has a **Copy help prompt** button: paste that prompt into any AI chat (the free web ChatGPT or Claude is fine) and it walks you through these same steps, with your values filled in. You can also paste this whole guide into a chat and ask for help.
3. **Let an AI do it for you.** The Claude Code, Codex CLI, and Grok Build wizard cards have a **Copy setup prompt** button. Install the app and sign in first (that part stays yours), then paste that prompt into the app itself: it checks your setup, runs the registration command, and verifies, asking your approval along the way. This only works in a normal session on your own computer, not in a cloud or sandboxed one; if it can't run the commands there, it stops and sends you back to your wizard card and its **Copy help prompt** button.

Still stuck after that? Ask in [Discord](https://familiarvtt.com/discord). That's what it's for.

---

## What works where

Your AI app and Familiar's built-in chat drive the same game with the same tools. A few things only the built-in chat does.

| You want | In your AI app | In Familiar's built-in chat |
|---|---|---|
| Combatants that take their own turns (auto-pilot) | No: nothing in your app watches the combat | Yes, on D&D 5e worlds: every combatant no player owns plays itself, allies included, on a chat provider key or your Local / Custom server |
| Live transcription of the session | No | Yes, from your browser's microphone |
| Lore from your knowledge base, added without asking | When you ask: it searches with `search-lore`; Claude Desktop and unrecognized apps first need [one `FAMILIAR_TOOL_BUNDLES` line](#which-tools-your-app-loads) | Yes |
| Players asking `@familiar` in Foundry's chat | When you ask it to check the table | Answered automatically |
| Slash commands, approvals, the chat saved as a journal | Your app's own commands, approvals and history | Yes |
| Voice, images, music, video, sound effects | Yes, in Foundry, on the keys in Familiar's settings; Claude Desktop and unrecognized apps first need [one `FAMILIAR_TOOL_BUNDLES` line](#which-tools-your-app-loads) | Yes, on the same keys |

### Keys you still need

Your subscription pays for the AI's thinking, not for the voices, pictures or music it makes. Every media call runs in Foundry, in your browser, on the keys you enter in Familiar's settings, whichever AI asks for it.

- **Voice:** the Voice tab's key. An optional second slot gives your characters their own provider; left empty, they use the narrator's.
- **Sound effects and music:** sound effects reuse an ElevenLabs voice key or a fal.ai image key; music takes an ElevenLabs key (paid plan), a fal.ai image key, or a NanoGPT or OpenRouter key.
- **Images and video:** the Image tab's key. Video runs when that tab's provider is fal.ai.
- **Live transcription (built-in chat only):** the Transcription tab's key (Gladia, Deepgram or AssemblyAI).
- **Automatic session recaps and memory:** these run in the background on the Chat tab's key or your Local / Custom server. With only a subscription, they don't run.
- **Notes vault:** no AI key at all, only the token and address of Obsidian's Local REST API plugin.

Keys are saved per browser, not per world, so enter them in the browser you run Foundry in as GM. What each of these costs, and which route to pick: [MCP vs API: which to choose](https://familiarvtt.com/guides/mcp-vs-api). To run the AI with no subscription and no bill: [local models](https://familiarvtt.com/guides/local-models).

### Which model to use

Use your plan's flagship model or the model just below it. A combat turn is a chain of tool calls, and a stronger model lands more of them. A fast, cheap tier of a current model family handles everyday play; smaller models work but miss steps in combat. To choose, run the same fight with two models and compare what ended up on the character sheets.

**Thinking** starts on High in the built-in chat (Chat tab); Medium is enough outside a hard fight. In your AI app, the model and its thinking are both the app's own settings.

### Your Table Rules

Your Table Rules (System Rules tab) reach your app too: Familiar's instructions tell it to read them with `get-world-info` when a session starts. So don't copy them into your app's own instructions. The Core Prompt Override on the same tab, and the Chat tab's reply length, shape only the built-in chat.

### Which tools your app loads

Most apps load every Familiar tool. Claude Desktop, and any app Familiar doesn't recognize, load a smaller set so they stay within Claude Desktop's tool limit.

- **Every tool:** Claude Code, Codex CLI and the ChatGPT app's Codex tab, Antigravity CLI and the Antigravity 2.0 desktop app (Part 7), Grok Build, Muse Code (Part 13).
- **A few to start, more as needed:** the standalone Antigravity IDE (Part 7).
- **A smaller set:** Claude Desktop and unrecognized apps load the basics (dice, world, chat, characters, compendium) plus combat, combat automation, scenes and character editing, and leave everything else out, for example images (`image-generation`), voice (`voice-generation`), knowledge and memory (`knowledge`), macros (`macros`), journals (`journals`), the notes vault (`notes-vault`) and Studio (`studio`). Ask the AI to list the tool bundles to see every id.

To add bundles back, list their ids in `FAMILIAR_TOOL_BUNDLES` next to `FAMILIAR_WS_SECRET` in your app's config (comma-separated; `all` adds every bundle), keep the entries already in that `env` block, then fully quit and reopen the app:

```json
"env": { "FAMILIAR_WS_SECRET": "<your secret>", "FAMILIAR_TOOL_BUNDLES": "voice-generation,image-generation" }
```

On Claude Desktop, swap rather than add, because it can drop tools from a long list: start the value with `only:` and it loads the basics plus exactly the bundles you name, for example `"only:combat,combat-ai,scenes,voice-generation"` (voice in place of character editing). Asking the AI to switch a bundle on mid-session only works in apps that refresh their tool list (Claude Code and the standalone Antigravity IDE); everywhere else, use the setting above. A bundle your app leaves out still works in the built-in chat and the table chat.

---

## Part 1: Before you start

- **Foundry VTT is running** with the Familiar module enabled and your license active.
- **Find your secret.** Familiar protects the connection with a password called the WebSocket secret. Open **Module Settings → Familiar → the MCP / Subs tab** and click your app's card: the command or config shown there already contains it. Wherever this guide writes `<your secret>`, use that value. Copy from the wizard rather than typing it out.
- **The secret belongs to this world.** Each Foundry world generates its own. If you play in more than one world, either redo the setup per world or give every world the same value via Familiar's **WebSocket Secret** module setting.
- **Know what the app itself can do.** Claude Code, Codex, Antigravity CLI, Grok Build and Muse Code are coding assistants: besides Familiar's tools, they can read files on your computer and, depending on their settings, edit them and run commands. Start them from a normal terminal (not "Run as administrator") in an ordinary folder, never a system folder. Familiar's helper only listens for your Foundry tab on this computer, protected by your secret, and sends your license key to the license check; it never sends your API keys anywhere. What its tools return goes to your AI app, which sends it to its provider like the rest of your conversation.

## Part 2: Install Node.js (all apps need this)

The helper program runs on Node.js, a free program that lets JavaScript run outside a web browser. Every app in this guide needs it, even the ones that are not command-line tools.

1. Go to **[nodejs.org](https://nodejs.org)** and click the **LTS** download. Don't worry about the version number; any current LTS works.
2. Run the installer and accept the defaults. **Windows:** if the installer offers to "automatically install the necessary tools", leave that box **unchecked**. Familiar doesn't need those tools, and they pull in gigabytes you'll never use.
3. **Open a new terminal window** (Windows: press Start, type `PowerShell`, press Enter. Mac: open Terminal from Applications → Utilities). It must be a new window: terminals opened before the install can't see Node yet.
4. Type `node --version` and press Enter.

**Expected result:** a version number like `v24.19.0`. If you see "not recognized" or "command not found" instead, close every terminal window and try step 3 again; if it persists, reinstall Node.

---

## Part 3: Claude Code (terminal)

Works with a paid Claude plan (Pro, Max, or Team). The free Claude plan does not include Claude Code.

1. **Install Claude Code.** Open PowerShell (Mac: Terminal) and run:

   ```
   npm install -g @anthropic-ai/claude-code
   ```

   **Expected result:** the install finishes without red error text. Check with `claude --version` in a new terminal window.

2. **Add Familiar.** In the same terminal, run the command from your wizard card. It looks like this:

   ```
   claude mcp add familiar --scope user --env FAMILIAR_WS_SECRET=<your secret> -- npx -y familiar-vtt
   ```

   On Windows, add `--env NODE_USE_SYSTEM_CA=1` after the secret (the wizard's command already has it). Part 10 explains why.

   **Expected result:** a confirmation that `familiar` was added. That message means the entry was saved, not yet that it runs; the check comes in step 4.

3. **Sign in.** Open a new terminal window, type `claude` and press Enter. Choose **"Claude account with subscription"** (option 1) and finish the login in your browser.

   **Expected result:** the Claude Code prompt appears, showing the model and your folder.

4. **Verify.** In a terminal, run:

   ```
   claude mcp list
   ```

   **Expected result:** `familiar` with a green `✔ Connected`. The very first check can show `✘ Failed to connect` while the helper program downloads in the background; wait half a minute and run it again. Inside Claude Code, `/mcp` shows the same status, and Familiar's **MCP / Subs** tab now reads "Claude Code: Connected".

5. **Play.** With Foundry open, ask Claude Code: *Use Familiar's get-world-info tool.* If it names your world, you're done.

## Part 4: Codex CLI (terminal)

Works with a ChatGPT account. Paid plans (Plus, Pro, Team) get normal Codex usage; the free plan has a small allowance.

1. **Install Codex.** Open PowerShell (Mac: Terminal) and run:

   ```
   npm install -g @openai/codex
   ```

   **Expected result:** the install finishes without red error text. Check with `codex --version` in a new terminal window.

2. **Sign in.** In that new window, type `codex` and press Enter, then choose **Sign in with ChatGPT** and finish the login in your browser. When you see the Codex prompt, leave it (type `/quit`, or close the window).

3. **Add Familiar.** In a terminal (not inside Codex), run the command from your wizard card. On Windows it looks like this:

   ```
   codex mcp add familiar --env FAMILIAR_WS_SECRET=<your secret> --env NODE_USE_SYSTEM_CA=1 -- npx.cmd -y familiar-vtt
   ```

   On Mac and Linux, `npx` instead of `npx.cmd`, and without the `NODE_USE_SYSTEM_CA` part (Windows only; Part 10 explains it).

   **Expected result:** `codex mcp list` shows `familiar`.

4. **Tell Codex when to use Familiar.** Codex doesn't announce its tools to the model, so give it a standing note. Open the file `~/.codex/AGENTS.md` (Windows: `%USERPROFILE%\.codex\AGENTS.md`), create it if it doesn't exist, and add the short "Familiar (Foundry VTT)" note from your wizard card. Codex reads this file when a conversation starts, so save it before you open a new one.

5. **Verify.** Type `codex`, start a conversation, and ask: *Use Familiar's get-world-info tool.* If it names your world, you're connected. `/mcp` may list familiar with "Tools: (none)"; that's a known display quirk, asking is the real test.

**If Codex reports a startup timeout:** the first start downloads the helper program, and Codex only waits a few seconds by default. Open `~/.codex/config.toml` and add `startup_timeout_sec = 60` under the `[mcp_servers.familiar]` heading, then try again.

## Part 5: ChatGPT desktop app (the Codex tab)

Familiar works in the app's **Codex** tab. The Chat tab runs on OpenAI's servers and cannot reach programs on your computer, and neither can "ChatGPT Classic".

Already set up Codex CLI in Part 4? Skip to step 5: the app and the CLI share one configuration, so Familiar is already there.

1. **Install the app.** Download it from [openai.com/chatgpt/download](https://openai.com/chatgpt/download/), install, and sign in with your ChatGPT account.

2. **Open the add-server form.** Switch to **Codex** with the top-left switcher, then go to **Settings → Plugins → the MCPs tab → Add → Add MCP server**. The form is titled "Connect to a custom MCP". On older versions: Settings → MCP servers → Add server. (Labels checked in the English app; other languages translate them in the same order.)

3. **Fill in the form.** Your wizard card shows every value with a copy button next to it:
   - **Name:** `familiar`
   - **Type:** STDIO
   - **Command to launch:** only `npx.cmd` (Mac: `npx`). Nothing else in this field; the rest goes under Arguments.
   - **Arguments:** one row per value, in this order: `-y`, then `familiar-vtt`
   - **Environment variables** (not the "Environment variable passthrough" list below it): one row with key `FAMILIAR_WS_SECRET` and value `<your secret>`, and on Windows a second row with key `NODE_USE_SYSTEM_CA` and value `1`
   - Leave **Environment variable passthrough** and **Working directory** empty, then click **Save**.

4. **Restart.** The form has no restart button: fully quit the app and reopen it. The first start downloads the helper program in the background, so give it a minute. If the server shows as failed, quit and reopen once more.

5. **Verify.** Make sure the top-left switcher still says **Codex** (the ChatGPT side can't reach Familiar), start a new conversation, wait a few seconds, and ask: *Use Familiar's get-world-info tool.* If it names your world, you're connected. Add the `AGENTS.md` note from Part 4 step 4 too; both surfaces read the same file.

## Part 6: Antigravity CLI (terminal)

Works with a Google account; usage limits depend on your Google AI plan.

1. **Install the CLI.** Open PowerShell and run:

   ```
   irm https://antigravity.google/cli/install.ps1 | iex
   ```

   On Mac or Linux:

   ```
   curl -fsSL https://antigravity.google/cli/install.sh | bash
   ```

   **Expected result:** the installer reports where it put the `agy` program. Check with `agy --version` in a new terminal window.

2. **Sign in.** Open a **new** terminal window (the old one can't see `agy` yet), type `agy` and press Enter. In the "Select login method" menu, choose **1. Google OAuth** and sign in via your browser. Some setups show a code in the browser to paste back into the terminal. After the theme and trust questions, close the terminal window and open a new one for the next step (`Ctrl+C` does not reliably leave `agy`).

3. **Add Familiar.** Your wizard card generates a one-line command that writes the configuration for you, safely merging with anything already there. Copy it from the card and run it in a terminal. **Expected result:** no output at all; the command writes the file and stays quiet. Prefer to do it by hand? Open `~/.gemini/config/mcp_config.json` (Windows: `C:\Users\<you>\.gemini\config\mcp_config.json`), create it if needed, and make sure it contains:

   ```json
   {
     "mcpServers": {
       "familiar": {
         "command": "npx.cmd",
         "args": ["-y", "familiar-vtt"],
         "env": { "FAMILIAR_WS_SECRET": "<your secret>", "NODE_USE_SYSTEM_CA": "1" }
       }
     }
   }
   ```

   On Mac and Linux, `"npx"` instead of `"npx.cmd"`, and leave the `NODE_USE_SYSTEM_CA` entry out (Windows only; Part 10 explains it). Don't add a `"type"` field; Antigravity rejects it.

4. **Verify.** Type `agy`, then `/mcp`.

   **Expected result:** `familiar` listed as a connected server. Then ask: *Use Familiar's get-world-info tool.* If it names your world, you're done. The first time the AI actually uses a Familiar tool, Antigravity asks for approval; allow it.

**If familiar doesn't appear:** an older Antigravity may still read the previous config location, `~/.gemini/antigravity/mcp_config.json`. Put the same block there too.

## Part 7: Antigravity Editor (desktop IDE)

The Editor shares its configuration with Antigravity CLI. Did Part 6 already? Familiar is already configured; skip to step 4.

1. **Install the Editor.** Download it from [antigravity.google](https://antigravity.google), install, and sign in with your Google account.

2. **Open the config.** Click **Settings** (bottom left) → **Customizations**, scroll to **Installed MCP Servers** and click **Open MCP Config**. On the standalone Antigravity IDE the route is the Agent panel's **"…"** menu → **MCP Servers** → **Manage MCP Servers** → **View raw config**.

3. **Add Familiar.** Add the same `"familiar"` entry from Part 6 step 3. Does the file already list other servers? Press Enter at the end of the line `"mcpServers": {` and paste the entry on the new line (the wizard card's **Copy entry** button gives it with the comma). Is the file new, empty, or its `"mcpServers"` block empty (`{}`)? Paste the whole block. Save.

4. **Refresh.** Click the refresh icon next to **Installed MCP Servers** (standalone IDE: Manage MCP Servers → **Refresh**). If familiar still doesn't appear, fully quit and reopen Antigravity.

   **Expected result:** `familiar` with a green dot and its tool count, and Familiar's **MCP / Subs** tab reads "Antigravity Editor: Connected". Then start a new conversation and ask: *Use Familiar's get-world-info tool.* If it names your world, you're done.

## Part 8: Grok Build CLI (terminal)

Works with a SuperGrok subscription from xAI; you sign in with that account, no API key.

1. **Install Grok Build.** Open PowerShell and run:

   ```
   irm https://x.ai/cli/install.ps1 | iex
   ```

   On Mac or Linux:

   ```
   curl -fsSL https://x.ai/cli/install.sh | bash
   ```

   **Expected result:** the installer reports where it put the `grok` program (a `.grok/bin` folder in your home directory). Check with `grok --version` in a new terminal window.

2. **Sign in.** Open a **new** terminal window (the old one can't see `grok` yet), type `grok login` and press Enter, and finish the sign-in in the browser that opens. The terminal confirms when you're in.

3. **Add Familiar.** In a terminal (not inside Grok), run the command from your wizard card. On Windows it looks like this:

   ```
   grok mcp add familiar --env FAMILIAR_WS_SECRET=<your secret> --env NODE_USE_SYSTEM_CA=1 -- npx.cmd -y familiar-vtt
   ```

   On Mac and Linux, `npx` instead of `npx.cmd`, and without the `NODE_USE_SYSTEM_CA` part (Windows only; Part 10 explains it). Running the command again later replaces the entry instead of adding a second one.

   **Expected result:** `grok mcp list` shows `familiar`.

4. **Verify.** Run `grok mcp doctor familiar`. It starts the Familiar server once and reports what it found. (Keep the `familiar` at the end: without it, the doctor starts every server Grok knows about, including ones it picked up from other apps.)

   **Expected result:** `familiar` with `handshake OK` and a count of tools discovered. Then type `grok`, start a conversation, and ask: *Use Familiar's get-world-info tool.* If it names your world, you're connected.

**Already use Claude Code or Cursor on this computer?** Grok Build reads their MCP servers, skills, and hooks by default, so those servers show up inside Grok as well (Familiar included, if you set it up there; your Grok entry still wins for `familiar`). To keep them out of Grok's own server list, add this to `~/.grok/config.toml` (Windows: `%USERPROFILE%\.grok\config.toml`). One catch: `grok mcp doctor` without a server name still starts every server it can find, switched off or not, which is why step 4 names `familiar`.

```toml
[compat.claude]
mcps = false
skills = false
hooks = false

[compat.cursor]
mcps = false
skills = false
hooks = false
```

**If the doctor reports a startup timeout:** the first start downloads the helper program, and Grok waits 30 seconds by default. Open `~/.grok/config.toml` and add `startup_timeout_sec = 60` under the `[mcp_servers.familiar]` heading, then run `grok mcp doctor familiar` again.

## Part 9: Claude Desktop

Works with a paid Claude plan (Pro, Max, or Team). The simplest app to use, and the heaviest for Familiar: it loads a large fixed tool set at connect. If you also use Claude Code, prefer that.

1. **Install the app.** Download it from [claude.ai/download](https://claude.ai/download), install, and sign in. **Node.js from Part 2 is still required**; the app does not bring its own for this kind of server.

2. **Open the config file.** Click your profile icon (Mac: the Claude menu bar) → **Settings → Developer → Edit Config**. The file `claude_desktop_config.json` opens in your editor.

3. **Add Familiar.** If the file is new or empty, replace its contents with:

   ```json
   {
     "mcpServers": {
       "familiar": {
         "command": "npx.cmd",
         "args": ["-y", "familiar-vtt"],
         "env": { "FAMILIAR_WS_SECRET": "<your secret>", "NODE_USE_SYSTEM_CA": "1" }
       }
     }
   }
   ```

   On Mac, `"npx"` instead of `"npx.cmd"`, and leave the `NODE_USE_SYSTEM_CA` entry out (Windows only; Part 10 explains it). Already have other servers in the file? Add only the `"familiar"` entry: press Enter at the end of the line `"mcpServers": {` and paste it on the new line. The wizard card has a copy button for that entry alone, comma included.

4. **Restart.** Quit Claude Desktop completely (Windows: also right-click the tray icon and quit there; Mac: press Cmd+Q, closing the window leaves it running) and reopen it. The first start downloads the helper program, so give it a minute.

5. **Verify.** Back in **Settings → Developer**, familiar shows as **running** (the **+** button under the chat box lists it under Connectors too). Then ask: *Use Familiar's get-world-info tool.* If it names your world, you're done.

**To browse your generated art from Desktop**, add `"FAMILIAR_TOOL_BUNDLES": "only:combat,combat-ai,scenes,studio"` next to `FAMILIAR_WS_SECRET` in the config above and restart the app. That swaps Studio in for character editing, so Desktop stays within its tool limit. [Which tools your app loads](#which-tools-your-app-loads) lists the other bundles Desktop leaves out.

**Windows only, if familiar never appears:** some Windows installs open one config file but read another. Check whether this file exists and put the same content there: `%LOCALAPPDATA%\Packages\Claude_<random>\LocalCache\Roaming\Claude\claude_desktop_config.json`.

---

## Part 10: When something goes wrong

**"node is not recognized" / "command not found" right after installing Node.** Terminals only see Node in windows opened after the install. Close every terminal window and open a fresh one. See Part 2 step 3.

**PowerShell says "running scripts is disabled on this system".** Windows blocks `npm` and `npx` in PowerShell until you allow it once. Run this in the same window (no administrator needed):

```
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

Type `Y` if it asks to confirm, then run the failed command again; it works immediately. On a company-managed computer this can be locked by policy; in that case run the command in **Command Prompt** (cmd) instead of PowerShell.

**"spawn npx ENOENT", or the server never starts on Windows.** Windows needs the server launched as `npx.cmd`, not `npx`, in config files and app forms. The wizard's generated configs already do this. If you typed a config by hand, change `"command": "npx"` to `"command": "npx.cmd"`.

**The server shows "failed" or times out right after setup.** The very first start downloads the `familiar-vtt` package, which can take a minute on a slow connection, and some apps give up sooner than that. Wait a moment and check again; if the app has no retry, fully quit and reopen it once. Impatient? Pre-download it: run `npx -y familiar-vtt` in a terminal. It downloads the package and then stops with a message about `FAMILIAR_WS_SECRET`. That message is expected here (your AI app supplies the secret; a bare terminal doesn't), and the download is what you came for. Codex users can also raise the wait, see the end of Part 4; Grok Build users, the end of Part 8. In Muse Code, `/mcp` says `starting` while it waits and `failed` once the helper has quit.

**It worked before, but broke after a Familiar update.** Your computer may have cached an old version of the helper program. In a terminal, run:

```
npm cache npx ls
```

find the entry mentioning `familiar-vtt`, and remove it with `npm cache npx rm <key>`. Then restart your AI app.

**"MCP Server: Not running" in Familiar's settings while your AI app says connected.** These are two different lights: the server row means the helper program, the client row means your app. Give both a few seconds after starting your AI app; Foundry reconnects on its own, even if it was open during setup. Still red after a minute? Click **Reconnect** under the rows, or reload Foundry (F5).

**`FOUNDRY_DISCONNECTED` on every tool call.** Your app reached Familiar's helper, but no Foundry tab is connected to it as GM. Open your world in one browser tab and log in as the GM; a call can wait a few seconds for that tab before it fails. Still failing? Reload Foundry (F5). A second GM tab shows "Another Foundry client is already connected to the AI bridge." Close the extra tab.

**The built-in chat works, but every tool call from your AI app says "could not confirm an active licence" or "could not verify the licence server's certificate".** Familiar's server (the small Node program your AI app starts) checks your license on its own, and an antivirus that inspects HTTPS traffic (AVG and Avast are the ones we have seen; other web-shield products behave the same way) can block that check for programs it does not treat as browsers, while your browser passes. Node ignores the Windows certificate store unless told to. The fix is one environment variable for the server: `NODE_USE_SYSTEM_CA=1`. The wizard's Windows commands and configs already include it. If you registered Familiar by hand, or before this was added, put it next to `FAMILIAR_WS_SECRET`: a second `--env NODE_USE_SYSTEM_CA=1` on the command line, or a second line in the config's `env` block. Restart your AI app and ask again. The alternative is an exception for `node.exe` in the antivirus web shield. Needs Node 22.15 or newer; older Node ignores the variable.

**"Invalid secret" or the connection is refused.** The secret in your app's config doesn't match this world's. Copy the current value from the wizard card (Part 1) into your config, or set Familiar's **WebSocket Secret** module setting to the value your config carries. After changing the setting, reload Foundry (F5): the page reads the secret once when it loads, and **Reconnect** doesn't pick up a new one. Still refused when both match? A helper that was already running keeps the secret it started with, so fully quit your AI app and open it again.

**One app works, the other has no Familiar tools.** Two AI apps can use Familiar at the same time only when both carry the same `FAMILIAR_WS_SECRET`. With a different secret, or none, the second app's helper quits a few seconds after it starts, so that app shows the server as failed or lists no Familiar tools, and Foundry shows nothing. Copy the secret from the wizard card into every app's config, or close the other app, then fully quit and reopen the app that failed.

**Hosted Foundry (The Forge and friends).** The wizard detects hosted games and adds an extra `FAMILIAR_WS_ALLOWED_ORIGINS` entry to everything it generates; keep that entry when copying values by hand. Your browser also asks once whether the page may reach your local network: click **Allow**. Safari can't do this at all; use Chrome, Edge, or Firefox. On a hosted game the image tools answer your AI app with the new picture's web address instead of the picture itself; the image is in Foundry either way.

**Familiar says your Foundry login has ended.** Foundry ended this browser's login while your game kept running, so it won't save new files until you log in again. Open your game in a new browser tab and log in there: the first tab keeps running and keeps what it holds. Reloading the first tab also works, but it drops anything Familiar was keeping for you. Nothing on the page shows an ended login. Foundry ends one 24 hours after you log in, when its server restarts, and when another tab of the same browser opens the join screen. That is why Familiar checks before it pays for an image, a sound effect, a music track or a video. If the message says Familiar keeps an image or a sound effect for you, log in from the new tab and repeat the same request. It is saved at no new charge. A message that names a different user means someone logged in as that user in this browser: log in as yourself again, and keep a second login in a private window.

**Your AI app keeps asking before Familiar's tools run.** That question is your app's safety check, so keep it on: for some changes, such as switching combat rule enforcement off, it is the only "are you sure" there is. Approve read tools such as `roll-dice` or `get-world-info` for good; keep the question on for `update-familiar-setting` and any tool that deletes. To approve one tool for good:

- **Claude Code:** answer **Yes, and don't ask again**, or run `/permissions` and add the allow rule `mcp__familiar__<tool-name>`, for example `mcp__familiar__roll-dice`.
- **Claude Desktop:** click **Allow always** on that tool's approval.
- **Antigravity CLI:** run `/permissions` and add the allow rule `mcp(familiar/<tool-name>)`; it is saved in `~/.gemini/antigravity-cli/settings.json`.
- **Grok Build:** its approval menu has an option that remembers your answer for that one tool.
- **Muse Code:** per Meta's docs, Familiar's read tools need no approval to begin with: under on-request approvals a tool its server marks read-only runs without a question, and Familiar marks its read tools that way.
- **Codex:** per-tool approval lives under `[mcp_servers.familiar.tools.<tool-name>]` in `~/.codex/config.toml`; see [OpenAI's MCP guide](https://learn.chatgpt.com/docs/extend/mcp). Codex always asks before a tool marked destructive ([OpenAI's approvals guide](https://learn.chatgpt.com/docs/agent-approvals-security)).

Never approve the whole `familiar` server at once, and never switch the questions off: then nothing stops a delete you didn't mean.

**Your app answers from your Obsidian notes, but did Familiar do it?** An Obsidian vault is a plain folder, so Claude Code, Codex, Antigravity CLI, Grok Build and Muse Code can read it with their own file access, and a correct answer doesn't prove Familiar was used. The proof is a `familiar` tool call in the transcript (`read-vault-note`, `search-vault-notes`, `list-vault-notes` or `list-vault-tags`) whose result starts with `_source`. Or close Obsidian: Familiar's vault tools then stop answering.

**Support asked for the server log.** Familiar's helper program keeps its own log, and your AI app decides where that goes: Claude Code keeps it in a cache folder, others show it once or not at all. To hand it over, ask the helper to write it to a file. Add `FAMILIAR_LOG_FILE` next to `FAMILIAR_WS_SECRET` in your app's config, with a full path as the value, for example `C:\Users\you\familiar.log` on Windows or `/Users/you/familiar.log` on a Mac. Pick a folder outside Foundry's data folder: files in there are served to everyone in your game. Restart your AI app, do the thing that went wrong, then attach the file. The log never holds your API keys or your chat. It does carry file paths from your computer and the address of your game, so read it once before you send it. A path the helper cannot write to only prints a warning. For a first look there is a faster route: in Foundry, open Familiar's settings and click **Copy log bundle** at the bottom. That copies the browser's recent warnings and errors plus the helper's last log lines in one go, ready for a GitHub issue or an e-mail. It is too long for a Discord post; the smaller **Copy diagnostics** next to it is the one for Discord.

---

## Part 11: Keeping Familiar up to date

Familiar has two halves that update separately: the module in Foundry and the helper program your AI app starts. Update both after a release.

1. **The module.** On Foundry's setup screen (Return to Setup), open **Add-on Modules** and click **Update All**.
2. **The helper.** Your app starts it with `npx -y familiar-vtt`. After a Familiar release, fully quit your AI app and open it again, so it starts the helper fresh. If the check below still shows an older `Server`, your computer kept an old copy: "It worked before, but broke after a Familiar update" in [Part 10](#part-10-when-something-goes-wrong) clears it. If you ever installed it yourself with `npm install -g familiar-vtt`, npx keeps running that copy: remove it with `npm uninstall -g familiar-vtt`.
3. **Check.** In Foundry, open Familiar's settings and click **Report a bug / Copy diagnostics**; it opens a preview you can copy. The `Server` line should show the same version as the `Familiar` line or a newer one: a release that changes only the helper leaves the module where it is. An older `Server` means your app still runs an old helper; see "It worked before, but broke after a Familiar update" in [Part 10](#part-10-when-something-goes-wrong).

When the two halves can't talk to each other at all, Foundry shows a message that names the half to update. An older helper that still connects gets a note on the diagnostics `Server` line, beside its version: "older than this module: quit the AI app fully and reopen". Check that line after every release.

## Part 12: Your own MCP client (developers)

Familiar's helper is a standard MCP server over stdio, so any MCP client can drive it, and your Familiar license covers your own client like any other app. These are the details a hand-built client tends to get wrong.

- **stdio only**, no HTTP. Spawn `npx -y familiar-vtt` (Node 22 or newer; `npx.cmd` on Windows).
- **`FAMILIAR_WS_SECRET` is required.** Copy the `env` block the wizard writes for any app. The MCP SDK's stdio client passes only a short allowlist of environment variables to the child, so set every `FAMILIAR_*` variable explicitly.
- **Handshake first.** Send `initialize` and then `notifications/initialized` before `tools/list`; Familiar picks the tool set at `initialized`.
- **An unrecognized client name gets the smaller set.** Set `FAMILIAR_TOOL_BUNDLES=all` for every tool.
- **Use the server's `instructions`.** Put the string from `initialize` into your model's system prompt; the combat rules depend on it.
- **Spawn once and keep it running.** A respawn resets any bundle enabled during the session. To stop it, close its stdin; it exits within 2 seconds.
- **Foundry stays open.** Tools run in the logged-in GM's Foundry tab.
- **Some calls take minutes.** Most return quickly, but generation tools can run for minutes: send a `progressToken` (progress arrives every 5 seconds) and raise the SDK's 60-second default request timeout.
- **Retry only what says retryable.** Never retry `QUERY_TIMEOUT` automatically: the change may already have happened.
- **Calls are capped by concurrency, not per minute.** Past 50 in flight, a call returns a retryable `QUERY_OVERLOADED`. Nothing stops a runaway loop that makes one call at a time, so cap retries in your client.
- **stdout carries JSON-RPC only.** Logs are JSON lines on stderr: drain stderr, and never merge it into stdout.
- **Don't auto-approve everything.** Destructive tools and settings changes (`update-familiar-setting`) expect your client to ask the user first.
- **Several processes can share one Foundry** when they carry the same secret: the second attaches to the first as a peer, held to a few hundred messages a minute (`RATE_LIMITED`, retryable).

## Part 13: Muse Code (terminal)

Muse Code is Meta's coding agent for the terminal, not the Muse app. You sign in with a Meta account, no API key; it runs on a Muse Code subscription or on pay-as-you-go billing.

1. **Install Muse Code.** Open PowerShell and run:

   ```
   irm https://dev.meta.ai/install.ps1 | iex
   ```

   On Mac or Linux:

   ```
   curl -fsSL https://dev.meta.ai/install.sh | sh
   ```

   **Expected result:** the install finishes without red error text. Check with `muse --version` in a **new** terminal window (the old one can't see `muse` yet).

2. **Sign in.** In that new window, type `muse login` and press Enter. It shows a sign-in link and a code: press Enter again to open the link in your browser, check that the code there matches, and approve it with your Meta account. Back in the terminal it says **Logged in** and you are at the prompt again.

3. **Add Familiar.** Muse Code has no command that adds an MCP server, so your wizard card gives you one that does it for you: it adds Familiar to Muse Code's settings file, `~/.config/muse/settings.json` (Windows: `%USERPROFILE%\.config\muse\settings.json`). If the `XDG_CONFIG_HOME` variable is set on your computer, Muse Code keeps this file and `AGENTS.md` in the `muse` folder under it instead, and the command follows it. Quit Muse Code first, because it reads that file when it starts. Then copy the command from the card and run it in a terminal. Was Muse Code open while the command ran? Nothing is lost: quit it and start it again.

   **Expected result:** no output at all. The command keeps everything else in the file and saves the previous version beside it as `settings.json.bak`. If it can't read the file as Muse Code settings, it changes nothing and says so in one line: fix the file, then run the command again.

   Prefer to edit the file yourself? Add this entry under the file's servers key:

   ```json
   "familiar": {
     "transport": "stdio",
     "command": "npx.cmd",
     "args": ["-y", "familiar-vtt"],
     "mode": "optional",
     "env": { "FAMILIAR_WS_SECRET": "<your secret>", "NODE_USE_SYSTEM_CA": "1", "LOCALAPPDATA": "${LOCALAPPDATA}" }
   }
   ```

   Type the `LOCALAPPDATA` value exactly as shown: Muse Code fills it in. On Mac and Linux, `"npx"` instead of `"npx.cmd"`, and leave out the `NODE_USE_SYSTEM_CA` and `LOCALAPPDATA` entries (Windows only: Part 10 explains the first; Muse Code doesn't pass the second on to Familiar, which uses it to find Foundry's data folder).

   An existing file keeps all its own lines and the servers key it already has: `"mcpServers"`, or `"mcp_servers"` when the file uses that one. Never add the other spelling: with both, Muse Code says "MCP configuration error" and loads no server. Running the card's command again merges the two into one. A new file starts with `"schema_version": 1` and an `"mcpServers"` key, and a file that has no servers key yet gets `"mcpServers": { … }` around the entry the same way. That `schema_version` line stays in every file: without it every `muse` command stops.

4. **Tell Muse Code when to use Familiar.** Muse Code doesn't show the model Familiar's own instructions, so give it a standing note. Open the file `~/.config/muse/AGENTS.md` (Windows: `%USERPROFILE%\.config\muse\AGENTS.md`), create it if it doesn't exist, and add the short "Familiar (Foundry VTT)" note from your wizard card. Muse Code reads this file when a session starts, so save it before you start a new one.

5. **Verify.** Type `muse` and press Enter. If it first asks whether you trust this folder, choose **Trust and continue**. Inside Muse Code, run `/mcp`: `familiar` should show the status `connected`. Right after the start it can still say `starting`; run `/mcp` again. (There is no check command outside Muse Code.) Then ask: *Use Familiar's get-world-info tool.* If it names your world, you're connected.

**No Muse Code subscription?** Your account can start on Meta's Contributor model, which lets Meta train on everything Familiar reads from your world, your players' messages included. Type `/models` inside Muse Code to see which model you are on and pick a Standard one.

---

*Checked against: [code.claude.com/docs](https://code.claude.com/docs/en/mcp), [learn.chatgpt.com/docs](https://learn.chatgpt.com/docs/extend/mcp) (menu and form labels re-read from the English app itself, 26.820, 2026-08-26), [antigravity.google/docs](https://antigravity.google/docs/mcp/), [docs.x.ai/build](https://docs.x.ai/build/features/mcp-servers) (Grok Build, checked 2026-08-25), [dev.meta.ai/docs/muse-code](https://dev.meta.ai/docs/muse-code) (Muse Code, with its [configuration page](https://dev.meta.ai/docs/muse-code/configuration), checked 2026-10-01), [modelcontextprotocol.io](https://modelcontextprotocol.io/docs/develop/connect-local-servers), [nodejs.org](https://nodejs.org/en/download), and Microsoft's execution-policy documentation, 2026-08-24.*

*Approval and permission settings checked against: [code.claude.com/docs](https://code.claude.com/docs/en/permissions) (and its [security page](https://code.claude.com/docs/en/security)), [modelcontextprotocol.io](https://modelcontextprotocol.io/docs/2026-07-28/develop/connect-local-servers), [antigravity.google/docs](https://antigravity.google/docs/permissions/), [docs.x.ai/build](https://docs.x.ai/build/features/permissions), and [learn.chatgpt.com/docs](https://learn.chatgpt.com/docs/agent-approvals-security) (with its [MCP page](https://learn.chatgpt.com/docs/extend/mcp)), 2026-09-24; [dev.meta.ai/docs/muse-code](https://dev.meta.ai/docs/muse-code/extending) (Muse Code), 2026-10-01.*
