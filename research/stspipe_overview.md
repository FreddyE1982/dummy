# STS Pipe Remote Project Notes

The remote repository accessed via the mcp2term client contains the **StS Pipe** toolchain: a Slay the Spire mod that exposes the game's runtime over named pipes plus a Python SDK for automation.

Key observations from the remote documentation:

- `stspipe/__init__.py` introduces the package as the "Slay the Spire pipe client SDK" and re-exports the `Session` façade and plugin manager so downstream integrations can connect to the pipe interface with minimal imports.
- `stspipe/client/session.py` defines a `Session` context manager that opens pipe transports, performs the handshake defined by the mod, routes frames, manages service facades (cards, characters, decks, overlays, etc.), and integrates with a plugin runtime to surface telemetry.
- `API.md` documents the mod's line-delimited JSON protocol. It describes the handshake topic, lifecycle telemetry, and command semantics, clarifying that clients talk to FIFOs at `/tmp/stspipe/ipc-pipe.in` and `/tmp/stspipe/ipc-pipe.out`.
- `pythonclient_quickstart.md` showcases high-level helpers (`run`, `send_command`, `ensure_textures`, `register_character_simple`, etc.) that wrap `Session` usage for automation scripts, demonstrating capabilities like asset upload, character registration, deck indexing, and card/audio/localization management.

Together these sources paint the picture of a production-ready IPC bridge that allows tooling to create, register, and manage Slay the Spire content programmatically while streaming telemetry and lifecycle events for plugins.
