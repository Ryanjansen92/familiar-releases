<!--
  Rendered from familiar's docs/releases-readme.template.md at release time.
  Counts, provider lists and prices are filled from the shipped README.md.
  Edit the template in the source repo, not this file: the next release overwrites it.
  Static facts to keep in step by hand when they change: the MCP client list
  (README.md clients table) and the Foundry version line (module.json compatibility).
-->

# Familiar AI Co-Pilot for Foundry VTT

Familiar is an AI-powered co-pilot module for Foundry VTT. It provides 230 tools across 26 domains, giving your AI assistant direct access to your game world, characters, combat, scenes, journals, audio, and more. It runs a published adventure you have imported; it does not invent the story.

## Quick Install

In Foundry VTT, go to **Add-on Modules** > **Install Module** > paste the manifest URL:

```
https://github.com/Ryanjansen92/familiar-releases/releases/latest/download/module.json
```

Click **Install**, then enable the module in your game world under **Manage Modules**.

**Beta channel** (optional): the next release ahead of time, for checking a reported fix. Same dialog, this manifest URL, then Foundry's Update button keeps you on the newest beta until the stable release overtakes it. Back up your world first; MCP clients run `npx -y familiar-vtt@beta`.

```
https://github.com/Ryanjansen92/familiar-releases/releases/download/beta/module.json
```

## Features

**Combat Automation (D&D 5e)**
- Resolve attacks, damage, saving throws, and spell effects with full rules enforcement
- Class features fire as written: Rage, Action Surge, an Extra Attack budget, all ten Metamagic options, the eldritch invocations, and the SRD subclass features
- Track initiative, conditions, legendary actions, death saves, and concentration
- Movement validation with speed enforcement and opportunity attack detection
- Enforcement is a world setting and can be switched off for tables that rule their own way

**AI Voices and Sound for NPCs**
- Text-to-speech for any NPC through any of the voice providers listed below, including your own OpenAI-compatible TTS server
- Assign persistent voices to characters, or let Familiar cast one from the provider's catalogue, so the AI speaks in character during play
- Short sound effects from your own playlists first, generated when nothing matches; ambience moods switch across your playlists as the scene changes
- Voice and sound play for the whole table by default, and each spoken line also lands in the chat under the speaker's name. Familiar settings, Voice tab, turns either broadcast off; music and filed tracks still play to everyone through Foundry's playlists
- Ask for a piece of music and Familiar composes an instrumental track on your ElevenLabs, fal.ai, NanoGPT, or OpenRouter key and files it in a playlist, without starting it

**Battle Map Generation**
- Generate battle maps and scene backgrounds using AI image providers
- Maps are requested at your scene grid's aspect ratio, so they land on the squares
- Turn a generated map into a scene in one click, then have the AI wall and light it
- Ask for scenes, tokens, lighting, walls, and tiles in plain words, and Familiar builds and changes them in your world

**Live Session Transcription**
- Real-time speech-to-text transcription of your game session
- Automatic session summaries and journal note creation

**Image Generation**
- Generate character portraits, token art, item icons, and handouts on demand, applied straight to the actor or item
- Familiar turns a still into a short looping clip on your fal.ai key: lay it over the scene as a moving map, or show it to your players
- Every image, clip, and music track Familiar makes files itself into Familiar Studio, a searchable in-world window. Browse, filter, and sort it, drag art onto the canvas, or type a prompt under the grid to make something new
- Edit any image you already made from the image itself, or point at the part that should change (OpenAI, fal.ai, OpenRouter)
- Providers: OpenAI (GPT Image), fal.ai, Leonardo AI, OpenRouter, NanoGPT, Custom (OpenAI-compatible)

**World Management**
- Create, read, update, and search actors, items, journals, playlists, macros, and more
- File many documents into a folder at once, in the sidebar or inside a compendium pack
- Move items between character sheets, and on D&D 5e move coin too: Familiar makes change and can check the price first
- Canvas control: drawings, weather, lighting, fog of war

**Flexible AI Access**
- Built-in chat window inside Foundry VTT with streaming responses
- MCP server for use with external AI clients (Claude Desktop, Claude Code, Codex CLI, the ChatGPT desktop app's Codex tab, Antigravity CLI and Editor, Grok Build CLI, Muse Code)
- Table Chat: on by default. Players talk to Familiar or to any NPC from the ordinary Foundry chat, under your approval mode, and Familiar posts a short how-to when the world loads. Name one player as the Solo Player and Familiar runs the table as their GM
- Works with 31 AI providers, from cloud APIs to a local model running on your own machine

## Supported Providers

**Chat**: OpenRouter, Anthropic, OpenAI, Google, Groq, Mistral, Together AI, DeepSeek, xAI, Cohere, Perplexity, Fireworks AI, Cerebras, SambaNova, NanoGPT, Local / custom server. The local / custom option takes any OpenAI-compatible server.

**Voice**: ElevenLabs, Cartesia, OpenAI TTS, OpenRouter TTS, NanoGPT TTS, Custom TTS

**Image**: OpenAI (GPT Image), fal.ai, Leonardo AI, OpenRouter, NanoGPT, Custom (OpenAI-compatible)

**Transcription**: Gladia, Deepgram, AssemblyAI

## Requirements

- Foundry VTT v13 or later (verified on v14)
- An API key for at least one supported AI provider
- A modern browser (Chrome, Firefox, Edge)
- Node.js 22 or later, for the MCP path only. The built-in chat needs nothing but Foundry
- A Familiar license: $6 a month or $48 a year, or $99 once. The first two weeks of a subscription are free, every feature unlocked. Subscribe at https://familiarvtt.com
- Game system: D&D 5e (2024) for the combat rules engine. Every other Foundry system gets the rest: story, NPCs, scenes, audio, music, voices, images, video clips, transcription, campaign memory, and character reads through your own system's sheet. Verified live on Pathfinder 2e, Dragonbane, and Troika.

## License

This module is licensed under the [PolyForm Shield License 1.0.0](LICENSE).

Familiar is an independent product. It is not affiliated with, endorsed, sponsored, or approved by Wizards of the Coast LLC. Dungeons & Dragons and D&D are trademarks of Wizards of the Coast LLC.

This work includes material from the System Reference Document 5.2.1 ("SRD 5.2.1") by Wizards of the Coast LLC, available at https://www.dndbeyond.com/srd. The SRD 5.2.1 is licensed under the Creative Commons Attribution 4.0 International License, available at https://creativecommons.org/licenses/by/4.0/legalcode.

## Support

- **Website and licensing**: https://familiarvtt.com
- **Bug reports and feature requests**: the [Discord](https://familiarvtt.com/discord) is the fastest route; every error in the chat carries a **Copy diagnostics** button that puts a redacted report on your clipboard. [GitHub Issues](https://github.com/Ryanjansen92/familiar-releases/issues) works too
- **Foundry VTT compatibility issues**: please include your Foundry version, browser, and any console errors

---

This is the releases repository for **Familiar**, the commercial AI co-pilot for Foundry VTT, published on npm as [`familiar-vtt`](https://www.npmjs.com/package/familiar-vtt). Source code is not included here; each release contains the compiled module ready for installation. Not affiliated with the unrelated `rayners/fvtt-foundry-familiar` module or the tabletop "familiar" creature.
