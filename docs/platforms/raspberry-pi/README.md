# Raspberry Pi

[Home](../../../README.md) · [All platforms](../README.md)

**Status:** Pi 5 client drafts available; hardware verification pending. Other
boards and host use remain outside the first walkthrough.

## Available draft guides

- [Prepare Pi 5 with Raspberry Pi OS 64-bit Desktop](prepare-pi5.md).
- [Install Tailscale on the Pi](../../tools/tailscale/setup-devices.md#raspberry-pi-5).
- [Install and launch Moonlight Qt](../../tools/moonlight/client-raspberry-pi.md).
- [Connect to the Windows gaming PC](../../scenarios/windows-sunshine-tailscale.md).

The baseline uses Trixie or Bookworm and a local screen, keyboard, and mouse.
Sources reviewed 2026-10-16; performance and peripherals have not been tested.

## Platform preparation to document

- Exact board model, OS image/version, architecture, and installed desktop.
- Power supply, cooling, network connection, display, and audio outputs.
- Controller and keyboard setup, startup behavior, and recovery access.

## Further coverage planned

- Preparing a tested board and OS image for use as a client.
- Tool-specific client setup, pairing, playback, and controller checks.
- A complete living-room workflow, including startup and reconnect testing.

Reuse [Linux preparation](../linux/README.md) when the instructions apply. Record
board-specific installation, graphics, or playback findings in the relevant
guide instead of implying that every Raspberry Pi behaves the same way.
