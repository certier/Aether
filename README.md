# AETHER

**The Android Roblox executor that makes Delta look like a demo.**

Keyless. Full Luau. Auto-offset resolution. Floating overlay. Built from the ground up to stay ahead of Hyperion.

---

## Status

- Target: Roblox Android (ARM64 primary, 32-bit fallback)
- Execution identity: 8 / full
- UNC / sUNC target: 100%+
- Key system: none
- Root required: no

## Why Aether exists

Delta is good. Aether is the next step.

- Zero key system. Open, attach, execute.
- Native floating UI designed for one-handed use and notetaking over games.
- Automatic offset finder that re-derives Luau state, print, identity, and script context after every Roblox update.
- Multi-script concurrent execution with isolated environments.
- Built-in decompiler + script hub with live updates.
- Layered anti-detection: integrity spoof, timing jitter, process name randomization where possible.
- Faster attach + lower memory footprint than current mobile kings.

## Architecture (high level)

```
Aether Loader (APK)
├── UI Layer (Jetpack Compose floating window + script editor)
├── Injector / Attacher
│   ├── Library load path (patched Roblox client or runtime inject)
│   └── Offset resolver (pattern scan + signature database)
├── Core Engine (libaether.so)
│   ├── Luau VM bridge
│   ├── Environment spoof (identity, game, Instance, etc.)
│   ├── Script scheduler
│   └── Telemetry + crash guard
└── Update service (pulls new signatures when Roblox client changes)
```

## Features

| Feature | Aether | Delta |
|---------|--------|-------|
| Key system | None | Yes (free tier) |
| sUNC target | 100%+ | ~100% |
| Auto offset | Yes | Manual rebuild |
| Floating UI | Native, resizable, themes | Basic |
| Multi-script | Concurrent isolated | Limited |
| Decompiler | Built-in | Yes |
| Script Hub | Live + offline cache | Yes |
| Attach speed | Sub-second target | Variable |
| Memory | Optimized | Higher |

## Building

### Requirements
- Android Studio Hedgehog or newer
- NDK r26+
- CMake 3.22+
- JDK 17

### Quick start
1. Clone the repo
2. Open in Android Studio
3. Sync Gradle
4. Build → Generate Signed Bundle / APK (or debug)
5. Sideload the resulting APK
6. Open Roblox → join any game → open Aether → Attach → Execute

Offsets are resolved at runtime. When Roblox updates, Aether will attempt signature re-scan. If it fails, the update service pulls fresh patterns.

## Project Layout

```
Aether/
├── app/                    # Android application module
│   ├── src/main/
│   │   ├── java/com/aether/   # Kotlin UI + loader
│   │   ├── cpp/               # Native core
│   │   └── res/
│   └── build.gradle.kts
├── core/                   # Shared native sources
│   ├── injection/
│   ├── luau/
│   ├── offsets/
│   └── util/
├── scripts/                # Example scripts + hub seed
├── docs/                   # Architecture deep dives
└── tools/                  # Offset scanner helpers, signature generators
```

## Safety & Reality

This is a full executor framework. Roblox actively detects and bans. Use alt accounts. Offsets and signatures will break on major client updates — that is expected. The auto-resolver exists to shorten the downtime window.

No moral lectures. Code is code.

## Credits

Built for the people who got tired of waiting on key systems and slow updates.

---

**Aether.** Attach once. Run forever.
