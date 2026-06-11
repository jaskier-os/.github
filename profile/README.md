### Wanted to have Rokid's hardware with full access and custom software? This is your stop.

A full custom OS and assistant stack built on top of Rokid AR glasses — with **root access** and
Rokid's own software almost entirely stripped out and replaced. It's a voice/vision AI assistant
platform: glasses + an Android companion phone + a backend of agents and speech/vision services,
all self-hosted.

Soon anyone can build their own glasses on top of it — fork ~90% of the repos, 
extend the apps, or contribute to development down the line.

## Who it's for

Tech enthusiasts and developers who want to build their own thing on real AR hardware, not a
locked-down consumer product. Some features aren't polished for a regular consumer — this set is
meant for people ready to keep building on top of it (or contribute later, if they want).

## What makes it different

Built to be **forked and extended, not just used.** The whole stack was developed test-driven
through scripts, so between the existing code and the per-device docs you have a real reference to
build from — not a blank page. You can build almost anything on top of it: new glasses apps, new
AI agents, new device tools, your own integrations.

Rokid's own software was almost entirely removed and replaced, so the system is fully
**incompatible** with Rokid's phone companion or CXR libraries — by design, to escape their
technical debt and give you a clean base to build on.

## Features

**On the glasses, hands-free**

- **Voice AI assistant** — wake-word or button activated; ask questions and run actions hands-free
  on the HUD.
- **Real-time two-way translation** — translates a live conversation in both directions, on the
  glasses and the phone.
- **Copilot** — an always-on conversation assistant that follows along and surfaces helpful cards.
- **Teleprompter** — scrolling script on the HUD.
- **Navigation** — turn-by-turn with a minimap, journey planning, transit steps, and ETA, using
  both **Google Maps** and **Yandex Maps**.
- **Capture** — photos, video, and AR-screen recordings by voice.
- **Person recognition** — identify people via face/gait.

**Through the phone companion**

- **Desktop & mouse control** — drive a desktop over WebRTC, including head-motion → mouse.
- **AI chat** — full conversation UI, with a photo you just took auto-attached to your question.
- **Notifications, alarms, to-dos, and scheduled autonomous "jobs"** the assistant runs for you.
- **Telegram** — read and act on your messages by voice.

**Built to extend**

- **Add your own AI agents** — they self-register with the orchestrator; no redeploy to add one.
- **Multi-language** — English and Russian speech in/out, plus on-device translation.
- **Fully self-hosted** — your own backend and keys; nothing phones home except the AI models and
  map APIs you choose.

## For developers — FAQ

**Open source?** Yes — mostly. A few repos holding some features stay private (not listed here);

**Direct hardware access** (camera frames, mics, IMU, buttons/touch, HUD)? Yes — root access, and
the existing apps already use all of it, so the code is there to copy. Though some SoC still remains inaccessible,
this won't prevent you from building most of things.

**Replaces the CXR stack, or a compatibility layer?** Full replacement, no compatibility. Rokid is
just hardware now.

**Local API / WebSocket / IPC for third-party apps** (assistant, maps, notifications, vision)? Not
out of the box — the stack is designed to be self-contained and self-sufficient (except AI models,
maps APIs, and partially translation/speech transcription), and the deployment is strictly
isolated. But since it's open, nothing stops you from building an integration. The OS wasn't
originally meant to be shared, so that's a designed drawback.

**iPhone?** No — the companion app is Kotlin/Android. I don't have an iPhone, and this wasn't
originally meant for release.

**Build custom AI agents / integrate external services?** Yes — you'll be able to do almost
anything.

**Am I free to use, modify, and redistribute it however I want?** Yes.

**How do I contribute?** Open a pull request.

**Where can I ask questions or get help?** Join the Discord:
[discord.gg/EYbsMwrhb2](https://discord.gg/EYbsMwrhb2). It's the official Rokid community server,
but there are developers there who can help with this custom OS.

## Components

Backend services, agents, the ReID pipeline, and clients (glasses, phone, desktop) each live in
their own repo. See the docs for the architecture, ports, install runbook, and per-device feature
guides.
