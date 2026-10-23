# `WindLore`
A decompilation launcher **specifically for the Heroes Lore series** ('Heroes Lore: Wind of Soltia', 'Heroes Lore 2: The Knight of Frozen Sea' and 'Heroes Lore: Zero' by Hands-On Mobile, versions 2.0.5, 1.0.2, and 4.4.47 respectfully, 320×240). Point it at your legally owned copy of the game and it runs natively on a desktop OS or Android — no emulator suite, no Java installation required.

![Screenshot 1](https://github.com/minimaster4734/windlore/blob/main/assets/screenshot_001.png)
![Screenshot 2](https://github.com/minimaster4734/windlore/blob/main/assets/screenshot_000.png)
![Screenshot 3](https://github.com/minimaster4734/windlore/blob/main/assets/screenshot_002.png)


This is **not** a general-purpose J2ME emulator. It implements exactly the subset of the mobile API surface that this one game actually uses, which keeps it small, predictable, and fast.

The launcher ships **no game code and no game assets**. You supply your own copy of the game.

## Highlights

- **Play it on different resolution scales** — ultrawide, widescreen, fullscreen or original.
- **Gamepad or keyboard**, fully rebindable.
- **Turbo mode available** automatically repeats attack input.
- **Picture filters** which apply to the original look at any size.
- **Nothing to install.** A self-contained build, no system Java needed.
- **Mods section** — create your own modifications or install community-made ones.


## Scope

This is a **decompilation tailored for this series of games only, not an emulator**. It is built around the exact API calls this one series makes. Other JARs are not supported and the launcher will refuse them rather than fail silently.

## Requirements

**Linux x86_64:**
- A standard desktop Linux environment (X11, or Wayland through the X11 compatibility layer). The usual desktop libraries — windowing and font configuration — are expected to be present.
- If a required system library is missing, the launcher reports which package to install instead of crashing.

**Android:**
- Android 5.0 and up, multiple architecture support (armv7l, arm64, x86, x86_64)

**Windows:**
-Supports both x86 and x64 systems. Windows 10 or newer.

## Getting started

Unpack the archive and run the binary. A launcher window opens.

```
bash

tar xzf windlore-linux-x64.tar.gz
cd windlore-linux-x64
./windlore
```

The archive carries its own runtime, so no system Java is needed. 

    Click Browse… and pick your legally owned copy of the game.

    Optionally open Settings… to adjust screen shape, window or fullscreen mode, scaling, keys, speed and more.

    Press Play.

The first time you add a game it is decompiled, repaired, rebuilt and stored in your library (about a minute on desktop, a few minutes on Android). After that the original file isn’t needed, there is no fallback to the original, and “Remove from library” deletes only the rebuilt copy.

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

The game runs at **14 fps in gameplay** (menus 20 fps, loading 5 fps). That is the game's own design, not a runner limit: its loop does exactly one logic update per frame, which means a higher frame rate produces a *faster* game rather than a smoother one. The launcher treats this as a first-class concept: a speed multiplier scales the game clock across a wide range, while music and sound effects continue to play at normal speed.

## Data, saves and configuration

On Linux, they are saved inside ~/.config/windlore/settings.properties, ~/.local/share/windlore/ and WINDLORE_HOME
On Windows, they are inside %APPDATA%\WindLore. 
On Android, saves and settings stay in the app, with export and import inside it.


## Compatibility notes
- Aspect-ratio presets can reveal more of the game world on wide monitors. Maps narrower than the viewport will show empty space at the sides — this is a property of the game's own map data, not a rendering fault.
- Command-line overrides are available for one-off runs, including window size, speed, and a headless scripted mode for automated testing and screenshot capture.

## Legal

The launcher's own source contains **no code and no assets from the game**. Third-party components are used unmodified and are documented in `THIRD-PARTY.md`, including their licences and verification hashes. You are responsible for supplying your own legally obtained copy of the game. The project is unofficial and unaffiliated with Hands-On Mobile, with the game names used only to identify compatible files.

## Status

Developed and verified primarily on Linux, other platforms have had limited testing. The runtime is written in portable Java, so other platforms are expected to work with an appropriate bundled runtime and a launch script.

## Known limitations.

- Online features are not available.
- Game 3’s in-game purchase fails like a phone with no signal.
