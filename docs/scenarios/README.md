# Scenarios

[Home](../../README.md) · [Getting started](../getting-started.md)

## Available walkthrough

| Guide | Coverage | Status |
| --- | --- | --- |
| [Windows Sunshine → Android / Pi 5 through Tailscale](windows-sunshine-tailscale.md) | Downloads, device installation, pairing, first game, and away-from-home checks | Draft; sources reviewed 2026-10-16, hardware tests pending |

## Workflow backlog

Scenarios answer “How do I achieve this?” Each one should identify a documented
host/client/tool combination, list the steps in order, link to their canonical
guides, and finish with an end-to-end acceptance check.

| Planned page | Goal | Dependencies |
| --- | --- | --- |
| `play-at-home.md` | Stream a game to another device on the local network | Host setup, client setup, pairing, audio and input checks |
| `play-away-from-home.md` | Use an existing setup from another network | Working local setup, remote networking and access controls |
| `living-room-client.md` | Use a Raspberry Pi or another device as a dedicated TV client | Client setup, display/audio, controller, startup and reconnect |
| `phone-or-tablet-client.md` | Play on a portable device | Client setup, touch/controller choices, display and connection checks |
| `remote-administration.md` | Maintain the gaming host remotely | Administration tool, permissions, reconnect after reboot |
| `unattended-host.md` | Operate a host without routine physical access | Startup, display strategy, administration and recovery |

The first walkthrough combines local and away-from-home checks for one tool
combination. Verify it before marking it supported. Split future workflows when
their steps materially differ. Refer to [platforms](../platforms/README.md),
[tools](../tools/README.md), and [shared reference](../reference/README.md) for the
underlying material.
