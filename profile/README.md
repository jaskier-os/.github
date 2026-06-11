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

Rokid's software (daemons, services, apps) was almost completely removed in favor of better
optimization and reliability. That means it is fully **incompatible** with Rokid's
phone companion or CXR libraries — by design, to escape their technical debt.

## Highlights

**Glasses (rooted firmware + native daemons + Kotlin app)**

- **Custom rooted firmware** on the Qualcomm "neo" base — own `super_4.img` build (root,
  SELinux-permissive), a bind-mount "DIY overlay" engine to swap apps without reflashing, and QDL
  flash tooling.
- **Own Bluetooth stack** replacing Rokid's — a privileged app wrapping the hidden A2DP-sink /
  HFP reflection APIs, RFCOMM sockets, BLE wake, and auto-reconnect.
- **Mic-array beamforming** — directional capture (cardioid "face the speaker", omni, conference)
  via native audio scenes.
- **On-device wake word** ("sireneviy") — custom-trained ONNX models with a full Python training
  pipeline, Silero VAD, and speaker verification; inference offloaded to the Hexagon DSP via a
  custom SoundTrigger HAL.
- **Night-vision** UNet model powering a Night Vision tab.
- **Native power daemon** — fold/take-off suspend (s2idle), screen timeout, battery-charge LED.
- **Touchpad daemon** — grabs the PSoC touchpad and re-emits velocity-scaled scroll; suppresses
  Rokid's accidental AI triggers. Plus camera/HUD capture service, RGBW LED control, and a
  WiFi-P2P file/log sync server.

**Phone (Kotlin companion)**

- **Relay hub** — the glasses reach the backend *through* the phone, with WebRTC video/desktop
  relay and head-motion → Bluetooth-HID mouse control.
- **Navigation engine** with both **Google** and **Yandex** maps — journey planning, transit
  steps, ETA, and a glasses minimap HUD.

**Assistant & AI**

- **Agentic, voice-invokable device tools** — navigation/journeys, scheduled autonomous "jobs",
  alarms, todos, photo/audio/video + AR capture, live translation, person recognition, Telegram.
- **Real-time two-way translation** using two mics (inner = you, outer = the other person) with
  dual phone + glasses displays; a teleprompter; and an always-on "Copilot" conversation assistant.
- **Photo-grounded chat** — a photo taken in the last minute auto-attaches to your spoken query.

**Backend & infra (self-hosted)**

- **Orchestrator** with LLM intent classification; agents self-register over outbound WebSocket —
  no redeploy to add one. Agents: web-search, vision, clickup, security, chat-history, ReID, and a
  PC agent (natural-language → shell + remote control).
- **Speech/vision**: NLLB-200 translation, faster-whisper + Anthropic STT, Kokoro (EN) +
  Tera/GLaDOS (RU) TTS routed by language, OCR.
- **ReID pipeline**: YOLOv8 + SCRFD + ArcFace + OpenGait with FAISS matching — person/face/gait
  recognition and a recognized-people dashboard.
- **Self-hosted k3s** with an in-cluster registry, GitLab CI (buildx), and Flux GitOps.

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
