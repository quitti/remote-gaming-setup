# Tools

[Home](../../README.md) · [Platforms](../platforms/README.md)

## Available draft guides

| Tool | Guides | Status |
| --- | --- | --- |
| [Sunshine](sunshine/README.md) | Windows host installation and controller options | Source-reviewed 2026-10-16; not hardware-tested |
| [Moonlight](moonlight/README.md) | Android and Raspberry Pi 5 clients | Source-reviewed 2026-10-16; not hardware-tested |
| [Tailscale](tailscale/README.md) | Private networking on Windows, Android, and Pi | Source-reviewed 2026-10-16; not hardware-tested |

For the complete first-time reading path, use
[Windows Sunshine to Android/Pi 5 through Tailscale](../scenarios/windows-sunshine-tailscale.md).

## Coverage areas

| Area | What its guides should cover |
| --- | --- |
| Game streaming | Host/server setup, client setup, pairing, audio/video, and input |
| Remote desktop administration | Desktop access, permissions, session behavior, and recovery |
| Remote networking | The chosen VPN/overlay or other connection method, access controls, and removal |
| Supporting utilities | Display handling, remote startup, controller/input helpers, or startup automation when required by a workflow |

Add official source and compatibility links when evaluating more tools. A
comparison page can follow once there are concrete findings to compare.

## Folder pattern

The following is a naming example, not a list of existing files:

```text
docs/tools/<tool>/
  README.md                 Purpose, official links, and documented combinations
  host-linux.md             Linux host/server setup, if applicable
  host-windows.md            Windows host/server setup, if applicable
  client-linux.md            Linux client setup, if applicable
  client-windows.md          Windows client setup, if applicable
  client-raspberry-pi.md      Board-specific client setup, if needed
  client-android.md          Android client setup, if applicable
  client-ios.md              iPhone/iPad client setup, if evaluated
```

Create only the pages needed. For a tool with a different model, such as a
networking utility, use descriptive names like `setup-linux.md` instead of
forcing it into host/client terminology. Shared instructions can remain in a
single page when they are genuinely identical across platforms.

A tool's README should list which guides exist and the exact combinations last
verified, including versions and dates. Use the [guide template](../../templates/guide.md)
for procedures and link general preparation from [Platforms](../platforms/README.md).
