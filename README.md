# Fatal Fury: Wild Ambition — PSX Recompilation

[![GitHub downloads](https://img.shields.io/github/downloads/omegakatana92/Fatal-Fury-Wild-Ambition-Recomp/total)](https://github.com/omegakatana92/Fatal-Fury-Wild-Ambition-Recomp/releases)
[![Latest release](https://img.shields.io/github/v/release/omegakatana92/Fatal-Fury-Wild-Ambition-Recomp)](https://github.com/omegakatana92/Fatal-Fury-Wild-Ambition-Recomp/releases/latest)
[![License: GPL-3.0](https://img.shields.io/badge/License-GPL--3.0-blue.svg)](LICENSE)

A native recompilation project for the North American PlayStation release of **Fatal Fury: Wild Ambition** (`SLUS-01001`), built with [mstan's PSXRecomp](https://github.com/mstan/psxrecomp) and the modern [recomp-ui](https://github.com/mstan/recomp-ui) launcher.

## Project status

The Windows build currently:

- Builds successfully with the PSXRecomp toolchain
- Opens through the recomp-ui launcher
- Accepts a legally obtained game disc image through the setup flow
- Launches the recompiled game successfully

Further compatibility and gameplay testing is ongoing. Please report reproducible problems through this repository's issue tracker.

## What is not included

This repository contains project code and configuration only. It does **not** include:

- The game ROM, BIN, CUE, ISO, CHD, or original PlayStation executable
- A PlayStation BIOS
- Prebuilt EXE or DLL files
- The local `build/`, `disc/`, or `generated/` directories
- Copyrighted game artwork, music, video, or other extracted assets

You must provide your own legally obtained copy of the game. Do not upload copyrighted game data when submitting issues or pull requests.

## Requirements

- Windows 10 or Windows 11
- Git
- CMake
- A compatible C/C++ toolchain
- A legally obtained North American disc image of *Fatal Fury: Wild Ambition*
- Any additional BIOS requirement presented by PSXRecomp

## Clone the project

The PSXRecomp framework and recomp-ui are Git submodules, so clone recursively:

```powershell
git clone --recursive https://github.com/omegakatana92/Fatal-Fury-Wild-Ambition-Recomp.git
cd Fatal-Fury-Wild-Ambition-Recomp
```

If you already cloned without the submodules:

```powershell
git submodule update --init --recursive
```

## Configure and build

Configure a full game runtime rather than a setup-host-only executable:

```powershell
cmake -S . -B build -DPSXRECOMP_FORCE_SETUP_HOST=OFF
cmake --build build --config Release --parallel
```

The resulting launcher is:

```text
build/Fatal_Fury_Wild_Ambition.exe
```

If the generated game sources are not present yet, use the setup flow provided by recomp-ui to select your legal game dump and generate the required local files. Those generated files remain ignored by Git.

## Important build note

If pressing **Play** produces an unknown-dispatch crash at `0x80016BF0`, the project was probably configured in setup-host-only mode. Reconfigure with:

```powershell
cmake -S . -B build -DPSXRECOMP_FORCE_SETUP_HOST=OFF
cmake --build build --config Release --parallel
```

The full-runtime configuration links the generated game functions and dispatch table into the executable.

## Repository layout

| Path | Purpose |
|---|---|
| `game.toml` | Game identity, disc metadata, and runtime settings |
| `game_options.toml` | User-facing runtime options |
| `seeds/` | Recompiler function-discovery seed addresses |
| `codegen_setup.c` | Setup and code-generation launcher integration |
| `scripts/` | Packaging and release helpers |
| `tools/` | Project maintenance utilities |
| `psxrecomp/` | PSXRecomp framework submodule |
| `recomp-ui/` | Launcher interface submodule |

## Credits

- **SNK** — original game
- **mstan and PSXRecomp contributors** — PSX recompilation framework
- **recomp-ui contributors** — launcher interface
- **OmegaKatana** — project setup, testing, and maintenance

## Legal notice

*Fatal Fury*, *Fatal Fury: Wild Ambition*, and all related names, characters, artwork, audio, and game content belong to their respective copyright and trademark owners. This is an unofficial preservation and compatibility project. It is not affiliated with or endorsed by SNK, Sony, or the original developers and publishers.

This repository does not distribute copyrighted game files. The project code is provided under the terms in [LICENSE](LICENSE).
