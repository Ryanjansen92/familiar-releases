# Familiar AI Co-Pilot for Foundry VTT

Familiar is an AI-powered co-pilot module for Foundry VTT. It provides 185 tools across 24 domains, giving your AI assistant direct access to your game world, characters, combat, scenes, journals, audio, and more.

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
- Text-to-speech for any NPC using ElevenLabs, Cartesia, OpenAI TTS, or PlayHT
- Assign persistent voices to characters -- the AI speaks in character during play

**Battle Map Generation**
- Generate battle maps and scene backgrounds using AI image providers
- Create and manage scenes, tokens, lighting, walls, and tiles programmatically

**Live Session Transcription**
- Real-time speech-to-text transcription of your game session
- Automatic session summaries and journal note creation

**Image Generation**
- Generate character portraits, item art, and scene imagery on demand
- Providers: OpenAI GPT Image, fal.ai, Leonardo AI

**World Management**
- Create, read, update, and search actors, items, journals, playlists, macros, and more
- Bulk operations with batch support across all domains
- Canvas control: drawings, measured templates, weather, lighting, fog of war

**Flexible AI Access**
- Built-in chat window inside Foundry VTT with streaming responses
- MCP server for use with external AI clients (Claude Desktop, Claude Code, ChatGPT, Cursor, and others)
- Works with 26 AI providers -- from cloud APIs to fully local models

## Supported Providers

**Chat**: OpenRouter, Anthropic, OpenAI, Google Gemini, Groq, Mistral, Together AI, DeepSeek, xAI, Cohere, Perplexity, Fireworks, Cerebras, SambaNova, LM Studio, Ollama

**Voice**: ElevenLabs, Cartesia, OpenAI TTS, PlayHT

**Image**: OpenAI GPT Image, fal.ai, Leonardo AI

**Transcription**: Gladia, Deepgram, AssemblyAI

## Requirements

- Foundry VTT v13 or later (verified on v14)
- An API key for at least one supported AI provider
- A modern browser (Chrome, Firefox, Edge)

## License

This module is licensed under the [PolyForm Shield License 1.0.0](LICENSE).

## Support

- **Bug reports and feature requests**: [GitHub Issues](https://github.com/Ryanjansen92/familiar-releases/issues)
- **Foundry VTT compatibility issues**: please include your Foundry version, browser, and any console errors

---

This is the releases repository. Source code is not included here. Each release contains the compiled module ready for installation in Foundry VTT.
