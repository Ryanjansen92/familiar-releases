# Familiar AI Co-Pilot for Foundry VTT

Familiar is an AI-powered co-pilot module for Foundry VTT. It provides 194 tools across 24 domains, giving your AI assistant direct access to your game world, characters, combat, scenes, journals, audio, and more. It runs a published adventure you have imported; it does not invent the story.

## Quick Install

In Foundry VTT, go to **Add-on Modules** > **Install Module** > paste the manifest URL:

```
https://github.com/Ryanjansen92/familiar-releases/releases/latest/download/module.json
```

Click **Install**, then enable the module in your game world under **Manage Modules**.

## Features

**Combat Automation**
- Resolve attacks, damage, saving throws, and spell effects with full rules enforcement
- Track initiative, conditions, legendary actions, death saves, and concentration
- Movement validation with speed enforcement and opportunity attack detection

**AI Voices for NPCs**
- Text-to-speech for any NPC using ElevenLabs, Cartesia, OpenAI TTS, OpenRouter TTS, or your own OpenAI-compatible TTS server
- Assign persistent voices to characters so the AI speaks in character during play

**Battle Map Generation**
- Generate battle maps and scene backgrounds using AI image providers
- Create and manage scenes, tokens, lighting, walls, and tiles programmatically

**Live Session Transcription**
- Real-time speech-to-text transcription of your game session
- Automatic session summaries and journal note creation

**Image Generation**
- Generate character portraits, item art, and scene imagery on demand
- Providers: OpenAI GPT Image, fal.ai, Leonardo AI, OpenRouter

**World Management**
- Create, read, update, and search actors, items, journals, playlists, macros, and more
- Bulk operations with batch support across all domains
- Canvas control: drawings, measured templates, weather, lighting, fog of war

**Flexible AI Access**
- Built-in chat window inside Foundry VTT with streaming responses
- MCP server for use with external AI clients (Claude Desktop, Claude Code, Codex CLI and Desktop, Antigravity CLI and Editor, LM Studio; ChatGPT connects through Codex)
- Works with 28 AI providers, from cloud APIs to local models over MCP

## Supported Providers

**Chat**: OpenRouter, Anthropic, OpenAI, Google Gemini, Groq, Mistral, Together AI, DeepSeek, xAI, Cohere, Perplexity, Fireworks AI, Cerebras, SambaNova, NanoGPT, Custom (any OpenAI-compatible server)

**Voice**: ElevenLabs, Cartesia, OpenAI TTS, OpenRouter TTS, Custom TTS (OpenAI-compatible)

**Image**: OpenAI GPT Image, fal.ai, Leonardo AI, OpenRouter

**Transcription**: Gladia, Deepgram, AssemblyAI

## Requirements

- Foundry VTT v13 or later (verified on v14)
- An API key for at least one supported AI provider
- A modern browser (Chrome, Firefox, Edge)

## License

This module is licensed under the [PolyForm Shield License 1.0.0](LICENSE).

Familiar is an independent product. It is not affiliated with, endorsed, sponsored, or approved by Wizards of the Coast LLC. Dungeons & Dragons and D&D are trademarks of Wizards of the Coast LLC.

This work includes material from the System Reference Document 5.2.1 ("SRD 5.2.1") by Wizards of the Coast LLC, available at https://www.dndbeyond.com/srd. The SRD 5.2.1 is licensed under the Creative Commons Attribution 4.0 International License, available at https://creativecommons.org/licenses/by/4.0/legalcode.

## Support

- **Website and licensing**: https://familiarvtt.com
- **Bug reports and feature requests**: [GitHub Issues](https://github.com/Ryanjansen92/familiar-releases/issues)
- **Foundry VTT compatibility issues**: please include your Foundry version, browser, and any console errors

---

This is the releases repository for **Familiar**, the commercial AI co-pilot for Foundry VTT, published on npm as [`familiar-vtt`](https://www.npmjs.com/package/familiar-vtt). Source code is not included here; each release contains the compiled module ready for installation. Not affiliated with the unrelated `rayners/fvtt-foundry-familiar` module or the tabletop "familiar" creature.
