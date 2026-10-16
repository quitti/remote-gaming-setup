# Getting started

[Home](../README.md) · [Platforms](platforms/README.md) · [Tools](tools/README.md)

Start with [Windows Sunshine to Android/Pi 5 through Tailscale](scenarios/windows-sunshine-tailscale.md)
if that matches your devices. It is a researched draft awaiting hardware tests.
This page explains the roles; section indexes distinguish available guides from
planned topics.

## Describe the two ends

- The **host** runs the game or desktop session you want to access.
- The **client** is the device you use to view that session and send input.

A Linux PC or Windows PC might be either end. The initial focus for Raspberry Pi,
Android, and possible iOS coverage is their use as clients. These are planning
priorities; individual guides will state which combinations they support.

Think of a setup as a path:

```text
Host running the game <-- network connection --> Client with screen and input
```

Game streaming, remote desktop administration, and remote startup are related
jobs, but each needs its own checks. A working streamed game does not by itself
verify that you can recover the host after a reboot or administer its desktop.

## Decide what you want to do

1. **Play elsewhere on the same local network.** This is the first workflow to
   document and verify for a new host/client combination.
2. **Play while away from home.** Add an outside-the-home networking guide to the
   working local setup, including how access is restricted and revoked.
3. **Use a device as a dedicated gaming client.** Include startup, display,
   controller, and reconnect behavior in the chosen scenario.
4. **Manage the host remotely.** Include a separate administration and recovery
   path, especially if the host will run unattended.

The [scenario index](scenarios/README.md) tracks these workflows.

## Gather your setup details

Before choosing or writing a guide, note:

| Area | Details to record |
| --- | --- |
| Host | OS/distribution and version, GPU and driver, connected or virtual display |
| Client | Device model, OS/version, screen, connected peripherals |
| Connection | Local or outside-the-home access, wired/Wi-Fi/mobile links at each end |
| Input and audio | Keyboard/mouse/controller, touch input, speakers/headset, microphone needs |
| Target experience | Games or desktop tasks, resolution, frame rate, acceptable responsiveness |
| Operations | Who can access it, startup/reboot needs, recovery if the connection fails |

Start at your [platform page](platforms/README.md) for device preparation and
relevant tool guides. Once a tested combination is documented, the scenario page
will link the pieces into an ordered setup with a final acceptance check.
