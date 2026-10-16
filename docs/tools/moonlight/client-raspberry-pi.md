# Install Moonlight on a Raspberry Pi 5

[Home](../../../README.md) · [Moonlight](README.md) · [Complete walkthrough](../../scenarios/windows-sunshine-tailscale.md)

- **Status:** Draft; not hardware-tested.
- **Role:** Client.
- **Sources last checked:** 2026-10-16.
- **Research scope:** Pi 5, Raspberry Pi OS 64-bit Desktop Trixie/Bookworm;
  Moonlight Qt `v6.2.0` release and official Pi package instructions.

## What you need

Complete [Pi 5 preparation](../../platforms/raspberry-pi/prepare-pi5.md) and
[Tailscale installation](../tailscale/setup-devices.md#raspberry-pi-5).
Keep a keyboard and mouse connected to the Pi, and keep the Windows PC's
Tailscale IPv4 address handy. Use **Moonlight Qt**, the graphical client.

The upstream installation page has “Raspberry Pi 4” in its title, but its current
requirements cover Raspberry Pi 2 and later on Raspberry Pi OS 12 (Bookworm) or
later. This guide narrows that to your Pi 5 and the 64-bit Desktop OS. It does not
cover Ubuntu, other Pi Linux distributions, or Raspberry Pi OS Lite.

## 1. Open a terminal on the Pi

Open the desktop's **Terminal** application. A terminal is a window where you type
commands. Copy each command below and press Enter; wait for it to finish before
running the next. If a password is requested, use your **Pi user password**.
It is normal for nothing to appear while typing a password.

Refresh the list of available software and install the small download/version
utilities used by the official installer:

```bash
sudo apt update
sudo apt install curl ca-certificates lsb-release
```

Read the proposed changes and press `Y`, then Enter, if prompted to continue.

## 2. Add the official Moonlight package source

The next command downloads and runs the repository setup script linked by the
Moonlight project. It needs administrator privileges to add a package source and
its signing configuration. The `$(lsb_release -cs)` part selects your OS release
automatically; copy the whole line unchanged.

```bash
curl -1sLf 'https://dl.cloudsmith.io/public/moonlight-game-streaming/moonlight-qt/setup.deb.sh' | distro=raspbian codename=$(lsb_release -cs) sudo -E bash
```

Then install the client:

```bash
sudo apt update
sudo apt install moonlight-qt
```

**Expected result:** installation finishes without errors. If the repository
script fails or the package is not found, stop and check your OS/version and the
[upstream instructions](https://github.com/moonlight-stream/moonlight-docs/wiki/Installing-Moonlight-Qt-on-Raspberry-Pi-4).
Do not substitute an old OS codename just to make the command succeed.

## 3. Launch it from the Pi's local text console

The Pi 5 has an HEVC/H.265 video decoder. HEVC is a video compression format;
the PC encodes it and the Pi decodes it. Upstream recommends a text-console launch
for performance and documents that the Pi HEVC path needs Moonlight outside the
desktop. This guide uses that launch method rather than changing boot settings.

1. Finish any work on the Pi desktop. Keep the Pi connected to its screen,
   keyboard, and mouse; these steps are done **at the Pi**, not through SSH.
2. Press **Ctrl+Alt+F3** to switch to a text login screen. On a compact keyboard,
   you may also need its `Fn` key. If F3 is already occupied, try F2 or F4.
3. Log in with the Pi username and password you created when setting up its OS.
   This is not your Windows, Sunshine, or Tailscale login. The password is hidden
   while typing.
4. At the command prompt, run:

```bash
moonlight-qt
```

**Expected result:** the graphical Moonlight window opens on the Pi's display.
Tailscale keeps running in the background. If you get a display or decoder error,
check [the troubleshooting guide](../../troubleshooting/sunshine-moonlight-tailscale.md#pi-display-or-decoder-error).

## 4. Choose starting settings

Use Moonlight's gear/settings button. For the first attempt choose:

| Setting | Suggested first value |
| --- | --- |
| Resolution | 1280 × 720 / 720p |
| Frame rate | 30 FPS |
| Video bitrate | 5 Mbps |
| Video codec | HEVC / H.265 |
| Video decoder | Automatic |
| HDR | Off |
| Audio | Stereo |

HEVC also needs support on the Windows host. If Moonlight reports that the host
does not support it, try **H.264** at these modest settings. On the Pi 5 that is a
software-decoding fallback, so performance can be worse; it is not evidence that
hardware HEVC worked. Keep AV1 and HDR out of the first setup.

These starting values are suggestions awaiting hardware testing. A wired network
and successful HEVC decoding are better foundations for tuning than raising
resolution immediately.

**Checkpoint:** Moonlight is open and configured. Continue with
[add and pair the PC](../../scenarios/windows-sunshine-tailscale.md#5-add-and-pair-the-windows-pc).

## Controls and returning to the Pi

Use the Pi's mouse and keyboard during the stream. Connect a controller to the
Pi with USB for the first controller check, then complete
[Windows controller support](../sunshine/host-windows.md#optional-controller-support).
Bluetooth can be added later using the controller maker's pairing instructions.

**Ctrl+Alt+Shift+Q** disconnects a Moonlight stream while leaving the game running
on Windows. Close the game first if you want it to stop. Quit Moonlight itself
to return to the text console. Switch back to the desktop with **Ctrl+Alt+F1** or
**Ctrl+Alt+F7**; the desktop's console number varies by image (F2 is another
possibility). There is no need to change the Pi's default boot mode.

## Update or remove

On the Pi, this refreshes package lists and updates just Moonlight and Tailscale
when newer packages are available:

```bash
sudo apt update
sudo apt install --only-upgrade moonlight-qt tailscale
```

To uninstall the Moonlight application:

```bash
sudo apt remove moonlight-qt
```

Removing the application leaves the package source and some user settings behind.
Revoke Sunshine pairing and Tailscale access separately if retiring this client.

## Sources

All checked 2026-10-16; no Pi installation or stream has been tested here.

- [Official Raspberry Pi installation instructions](https://github.com/moonlight-stream/moonlight-docs/wiki/Installing-Moonlight-Qt-on-Raspberry-Pi-4): supported OS, package commands, console launch, and updates.
- [Official decoding notes](https://github.com/moonlight-stream/moonlight-docs/wiki/Fixing-Hardware-Decoding-Problems): Pi HEVC outside the desktop. Its older MMAL/gpu-memory advice should not be copied indiscriminately to a Pi 5.
- [Pi 5 specifications](https://www.raspberrypi.com/products/raspberry-pi-5/): HEVC decoder.
- [Raspberry Pi's software explanation](https://www.raspberrypi.com/news/optimising-raspberry-pi-5s-software-environment/): Pi 5 H.264 software decoding.
- [Moonlight Qt release](https://github.com/moonlight-stream/moonlight-qt/releases/tag/v6.2.0): researched release; the package repository may deliver another version.
- [Moonlight controls](https://github.com/moonlight-stream/moonlight-docs/wiki/Setup-Guide): disconnect shortcut and input.
