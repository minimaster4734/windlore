# `WindLore` — Desktop launcher for a classic mobile game series

A runner built **specifically for this Heroes Lore: Wind Of Soltia** (Hands-On Mobile, v2.0.5, 320×240 build). Point it at your own, legally owned copy of the game and it runs natively on a desktop OS — no emulator suite, no Java installation required.

This is **not** a general-purpose J2ME emulator. It implements exactly the subset of the mobile API surface that this one game actually uses, which keeps it small, predictable, and fast.

The launcher ships **no game code and no game assets**. You supply your own copy of the game.

## Highlights

- **Runs your original game file, unmodified.** No repackaging, no patched files.
- **Nothing to install.** A self-contained build bundles an unmodified OpenJDK runtime.
- **Rebindable controls.** Every phone button maps to a desktop key, configurable in settings.
- **Display options.** Windowed, borderless fullscreen or exclusive fullscreen, integer or fractional zoom, crisp or smooth scaling, optional wider aspect presets.
- **Adjustable game speed.** A multiplier that scales the game clock without affecting audio playback.
- **Persistent configuration.** Settings, saves and screenshots live in standard per-user directories.
- **Optional decompiler helper.** A script that fetches a pinned, checksum-verified decompiler for modding research on your own copy.
- **Optional desktop integration.** Install or remove an application-menu shortcut from the command line.

## Scope

This is a **single-game runtime, not an emulator**. It is built around the exact API calls this one title makes. Other JARs are not supported and the launcher will refuse them rather than fail silently.

## Requirements

- A standard desktop Linux environment (X11, or Wayland through the X11 compatibility layer). The usual desktop libraries — windowing and font configuration — are expected to be present.
- If a required system library is missing, the launcher reports which package to install instead of crashing.

## Quick start

```bash
cd <APP>-linux-x64
./<APP> --jar /path/to/your_game_file   # the path is remembered
./<APP>                                  # every run after that
./<APP> --install-shortcut               # optional: add an applications-menu entry
```

The archive includes its own runtime, so no system Java is needed.

## Running from source

Without a bundled `runtime/` directory, the launcher falls back to a system Java 17+ installation that includes desktop support. Headless-only packages are not sufficient.

```bash
./build.sh    # rebuilds lib/<APP>.jar from src/
```

Building requires a JDK, or a JRE that includes the compiler module.

## Default controls

| Desktop key | Phone button |
|---|---|
| **W A S D** or arrow keys | Directional pad |
| **Space** | D-pad centre / confirm |
| **Enter** | Left soft key |
| **Tab** or **Backspace** | Right soft key |
| **E R F G C M** | Numeric keys |
| Number row and numpad | Matching phone digits |

All bindings are configurable in **Settings → Controls**, with two keys assignable per button; conflicts are resolved automatically.

## Window and settings

| Key | Action |
|---|---|
| **Esc** or **F10** | Open settings; the game is paused while open |
| **F11** or **Alt+Enter** | Toggle fullscreen |
| **F12** | Save a screenshot to the data folder |
| Right-click | Same options as the in-game menu |

Available settings include window mode, window size, scaling filter, integer zoom, frame-rate display, pause-on-focus-loss, audio and volume controls, speed multiplier, aspect-ratio presets, and save management.

## Frame rate and game speed

## Frame rate / game speed

The game runs at **14 fps in gameplay** (menus 20 fps, loading 5 fps). That is the game's own design, not a runner limit: its loop does exactly one logic update per frame, which means a higher frame rate produces a *faster* game rather than a smoother one. The launcher treats this as a first-class concept: a speed multiplier scales the game clock across a wide range, while music and sound effects continue to play at normal speed.

## Data, saves and configuration

- Settings: `~/.config/<APP>/settings.properties` (plain text)
- Saves and screenshots: `~/.local/share/<APP>/`
- Override the base directory for both with the `<APP>_HOME` environment variable.

## Decompiling (optional)

```bash
./decompile.sh /path/to/your_game_file [outdir]   # -> outdir/src, outdir/res
```

The helper downloads a checksum-verified decompiler on first use. Shipped game bytecode is frequently obfuscated, and some methods may not recompile cleanly as-is. That is exactly why the launcher executes the original bytecode rather than recompiled source — the decompiler output is for reading and modding research.

## Compatibility notes

- Some behaviour relies on handset-specific APIs that do not exist on a desktop JVM. Where that happens, the launcher compensates **at load time, in memory**. Your game file is never modified or copied.
- Localized text is loaded from the game's own resources; the launcher does not add, translate or replace game text.
- Aspect-ratio presets can reveal more of the game world on wide monitors. Maps narrower than the viewport will show empty space at the sides — this is a property of the game's own map data, not a rendering fault.
- Command-line overrides are available for one-off runs, including window size, speed, and a headless scripted mode for automated testing and screenshot capture.

## Legal

The launcher's own source contains **no code and no assets from the game**. Third-party components are used unmodified and are documented in `THIRD-PARTY.md`, including their licences and verification hashes. You are responsible for supplying your own legally obtained copy of the game.

## Status

Developed and verified primarily on Linux. The runtime is written in portable Java, so other desktop platforms are expected to work with an appropriate bundled runtime and launch script, but have not yet been validated.
