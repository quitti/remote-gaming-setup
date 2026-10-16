# Troubleshooting

[Home](../../README.md) · [Shared reference](../reference/README.md)

## Available draft guidance

[Sunshine, Moonlight, and Tailscale](sunshine-moonlight-tailscale.md) covers the
first Windows/Android/Pi 5 setup, including pairing, scoped Windows Firewall
rules, video/input, and direct versus relayed connections. Sources reviewed
2026-10-16; diagnostic fixes have not been reproduced on project hardware.

## Further topics planned

The topics below are a backlog for observed failures and verified fixes.

| Proposed page | Starting symptom |
| --- | --- |
| `discovery-and-pairing.md` | The host is missing or pairing fails |
| `connection-fails.md` | The host is known but a session cannot start |
| `black-screen.md` | A session opens without a usable picture |
| `audio.md` | Sound is missing, routed incorrectly, or out of sync |
| `input.md` | Touch, mouse, keyboard, or controller input fails |
| `latency-and-quality.md` | Playback stutters, looks poor, or responds slowly |
| `outside-home.md` | The setup works locally but fails from another network |
| `startup-and-reconnect.md` | The setup stops working after sleep, logout, or reboot |

Each troubleshooting page should record the affected environment, a minimal
reproduction, checks in a useful order, expected results, and a verified fix or
workaround. Explain what each check establishes before suggesting a change.
Link to the canonical setup procedure when a setting needs correction. Keep a
failure unique to one tool in that tool's guide, with a link here if useful.
