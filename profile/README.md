# jaskier-os

### Wanted to have Rokid's hardware with full access and custom software? This is your stop.

A full custom OS and assistant stack built on top of Rokid AR glasses — with **root access** and
Rokid's own software almost entirely stripped out and replaced. It's a voice/vision AI assistant
platform: glasses + an Android companion phone + a backend of agents and speech/vision services,
all self-hosted.

Soon I'm releasing my own OS built on Rokid's base, so anyone can build their own glasses on top
of it — fork ~90% of the repos, extend the apps, or contribute to development down the line.

## Who it's for

Tech enthusiasts and developers who want to build their own thing on real AR hardware, not a
locked-down consumer product. Some features aren't polished for a regular consumer — this set is
meant for people ready to keep building on top of it (or contribute later, if they want).

## What makes it different

Rokid's software (daemons, services, apps) was almost completely removed in favor of better
optimization and reliability. The deeper I went, the more their libs and apps turned out to be
redundant and in the way of building a proper system — so I gradually replaced them with my own.
**At this point Rokid is just the hardware.** That means it is fully **incompatible** with Rokid's
phone companion or CXR libraries — by design, to escape their technical debt.

For example: Rokid hosts content over Bluetooth through a single RFCOMM channel, which can crash
the BT stack. So I built a second channel just for audio, which meant rewriting much of the BT
communication and writing my own alternative to Rokid's CXR glasses services.

## Highlights

- **Root access** to the glasses, with apps already using the directional / omni-directional
  microphones, buttons, touchpad, and IMU — copy the code from them.
- Custom glasses UI (currently one app with tabs — normally you'd extend it), HUD rendering,
  camera/photo/video capture, real-time translation overlay, navigation, teleprompter, and a
  hands-free AI assistant.
- A backend of AI agents and speech/vision services you can extend with your own.
- Maps: both **Yandex Maps** and **Google Maps** (handy for Russian devs).

## For developers — FAQ

**Open source?** Yes — mostly. A few repos holding some features stay private (not listed here);
I may open those to people I trust.

**Direct hardware access** (camera frames, mics, IMU, buttons/touch, HUD)? Yes — root access, and
the existing apps already use all of it, so the code is there to copy.

**Replaces the CXR stack, or a compatibility layer?** Full replacement, no compatibility. Rokid is
just hardware now.

**Install custom Android apps?** Yes (though I hope you'll extend the existing UI app instead).

**Local API / WebSocket / IPC for third-party apps** (assistant, maps, notifications, vision)? Not
out of the box — the stack is designed to be self-contained and self-sufficient (except AI models,
maps APIs, and partially translation/speech transcription), and the deployment is strictly
isolated. But since it's open, nothing stops you from building an integration. The OS wasn't
originally meant to be shared, so that's a designed drawback.

**iPhone?** No — the companion app is Kotlin/Android. I don't have an iPhone, and this wasn't
originally meant for release.

**Build custom AI agents / integrate external services?** Yes — you'll be able to do almost
anything.

## Components

Backend services, agents, the ReID pipeline, and clients (glasses, phone, desktop) each live in
their own repo. See the docs for the architecture, ports, install runbook, and per-device feature
guides.
