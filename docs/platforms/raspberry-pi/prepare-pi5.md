# Prepare a Raspberry Pi 5 for Moonlight

[Home](../../../README.md) · [Raspberry Pi](README.md) · [Complete walkthrough](../../scenarios/windows-sunshine-tailscale.md)

- **Status:** Draft; not hardware-tested.
- **Sources last checked:** 2026-10-16.
- **Target:** Pi 5, Raspberry Pi OS 64-bit **Desktop**, Trixie or Bookworm.

This page prepares the Pi itself. Install games and Sunshine on the Windows PC;
the Pi will display the stream using Moonlight.

## If Raspberry Pi OS is already installed

Open **Terminal** on the Pi desktop and run:

```bash
cat /etc/os-release
uname -m
```

Look for Raspberry Pi OS/Debian version **13 / trixie** or **12 / bookworm**, and
`aarch64` for the running 64-bit system. Debian wording alone does not establish
that an image is Raspberry Pi OS; check how it was installed. If this is Ubuntu,
another distribution, a 32-bit image, or a text-only Lite installation, the
following Moonlight Desktop workflow is not its installation procedure.

If you have the right OS and a usable desktop, **keep it** and skip OS writing.
Open a website to check networking, and check that your chosen audio output works.
Then continue to [the walkthrough's Sunshine step](../../scenarios/windows-sunshine-tailscale.md#2-set-up-sunshine-on-the-windows-pc).

## If you need to install the OS

You need a blank/spare microSD card or other suitable Pi boot storage, a way to
connect it to another computer, and the Pi's keyboard, mouse, and screen.
**Writing an OS image erases the selected storage. Back up anything you need and
double-check the chosen card; do not select the Windows PC's system drive.**

1. On your Windows PC or another computer, download and install
   [Raspberry Pi Imager](https://www.raspberrypi.com/software/).
2. Connect the blank/spare card and open Imager. Choose **Raspberry Pi 5** as the
   device, **Raspberry Pi OS (64-bit)** with the desktop as the OS, and the card
   as storage. Current images use **Trixie**; an existing Bookworm Desktop image
   is also within this guide's scope. Do not choose Lite.
3. In Imager's customization steps, set your username/password, country,
   keyboard/time zone, and Wi-Fi details if using Wi-Fi. Record the username and
   password: you will use them for the console launch later. You do not need SSH
   or Raspberry Pi Connect for this local-screen setup.
4. Review the device/OS/storage summary, write the image, and wait for verification
   to finish. Safely eject the card.
5. With the Pi powered off, insert the card. Connect keyboard, mouse, and your
   TV/monitor with a micro-HDMI cable. Select that HDMI input on the display.
   Connect Ethernet if available, then connect the Pi's power supply.
6. Complete the first-boot prompts and any offered updates. Restart if requested.
   Open a website to verify internet access.
7. Select the intended audio output using the desktop's sound controls, and test
   it. For a TV setup, choose the HDMI display's audio output rather than an
   unrelated USB or Bluetooth device.

Use a power supply suitable for the Pi 5 and cooling suitable for sustained use.
See the official hardware guide below for power, display, and accessory details.

**Checkpoint:** the Pi has a working desktop, internet access, picture and sound,
and you know its username/password. Return to
[step 2 of the walkthrough](../../scenarios/windows-sunshine-tailscale.md#2-set-up-sunshine-on-the-windows-pc).

## Undo

Skip OS writing entirely if you want to preserve the installed system. An image
write cannot be undone with an uninstall command; recovery requires your backup
or original card. Later Moonlight/Tailscale removal does not require rewriting
the OS.

## Sources

All checked 2026-10-16; the image-writing and hardware steps have not been tested.

- [Raspberry Pi getting started and Imager instructions](https://www.raspberrypi.com/documentation/computers/getting-started.html): writing boot media, account/network setup, hardware connections.
- [Raspberry Pi 5 specifications and OS compatibility](https://www.raspberrypi.com/products/raspberry-pi-5/): Trixie/Bookworm compatibility and power/cooling.
- [Moonlight Pi requirements](https://github.com/moonlight-stream/moonlight-docs/wiki/Installing-Moonlight-Qt-on-Raspberry-Pi-4): Raspberry Pi OS Bookworm or later.
