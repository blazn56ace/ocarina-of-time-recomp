# Private Windows build inputs

The upstream project requires game-derived ExeFS, RomFS and generated C. **Do not commit or upload these files to a public fork or a public GitHub Actions artifact.** Public workflow artifacts can expose the game data even if they are short-lived.

## Recommended procedure

1. Clone this fork on your Windows PC.
2. Install the toolchain documented in `docs/plan.md` (Windows Python, MSYS2 UCRT64 Clang/Ninja, .NET and required libraries).
3. Extract the NUP locally with `tools/extract_nup.py` using the arguments shown by `python tools/extract_nup.py --help`.
4. Run the local ZBIC, shader translator and game generation steps as documented in `docs/plan.md`.
5. Compile locally using `python tools/build_game.py --jobs 4`.
6. Keep `build/`, `generated/`, ExeFS, RomFS and all game dumps untracked.

GitHub Actions in this public fork should be used for **source-only checks** and, when configured, runtime-only builds. A complete `oot.exe` cannot be built from public source alone: it needs game-specific generated code and hashes.

If a remotely hosted full build is necessary, use a **self-hosted Windows runner** under your control, with game files stored only on that machine, and do not upload resulting game-derived artifacts to public workflow artifacts. Self-hosted runners should not accept untrusted pull requests.

This document intentionally contains no game keys or assets.
