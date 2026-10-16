# Play Windows PC games on Android or a Raspberry Pi 5 through Tailscale

[Home](../../README.md) · [Scenarios](README.md)

- **Status:** Draft — researched against official documentation; not hardware-tested.
- **Sources last checked:** 2026-10-16.
- **Hardware verification:** Pending on both clients. No performance result is claimed.

Your Windows PC runs the game. Sunshine sends its picture and sound to Moonlight
on your phone, tablet, or Raspberry Pi 5. Moonlight sends your button presses back.
Tailscale gives the devices a private, encrypted connection, including when you
are away from home. Its private network is called a **tailnet**.

```text
Windows gaming PC                         Choose either client
Sunshine + Tailscale <---- Tailscale ----> Android: Moonlight + Tailscale
                                         Pi 5: Moonlight Qt + Tailscale
```

Set up both clients if you want, but test one at a time. They control the same
Windows desktop; this guide does not create separate gaming PCs or user sessions.

## Before you start

Have the Windows PC and your clients beside you for the first setup. You will
need to enter a pairing code on the Windows PC. Keep its monitor connected and
Windows signed in while learning the setup.

| Device or requirement | What this guide assumes |
| --- | --- |
| Gaming PC | Windows 11 on an Intel/AMD x64 PC, administrator access, an up-to-date graphics driver, and a game that already runs locally |
| PC display | A connected, enabled monitor; unattended/headless display setup is outside this first guide |
| Android | A phone or tablet with Android 8 or newer and Google Play access |
| Raspberry Pi | **Raspberry Pi 5**, with Raspberry Pi OS **64-bit Desktop**, Trixie or Bookworm; other Linux images need different instructions |
| Pi accessories | Suitable power supply and cooling, microSD/boot storage, monitor/TV and micro-HDMI cable, keyboard and mouse |
| Network | Internet access on every device; use Ethernet for the PC and Pi where possible, or good 5 GHz Wi-Fi |
| Account | One personal Tailscale account, used on all three devices |
| Controls | Android touch controls or a keyboard/mouse on the Pi for the first check; a controller is optional |

For the Pi's preferred HEVC video format, the PC must also be able to encode
HEVC. The Pi client guide includes a lower-performance fallback if it cannot.
Sunshine supports other Windows versions, but this walkthrough uses Windows 11
menus. It does not cover Windows on ARM.

## Downloads at a glance

Use these official sources. You do not need a GitHub account to download a release.

| Program | Install on | Official source |
| --- | --- | --- |
| Sunshine | Windows PC | [Stable releases](https://github.com/LizardByte/Sunshine/releases/latest) — select `Sunshine-Windows-AMD64-installer.msi` |
| Tailscale | Windows PC | [Windows download](https://tailscale.com/download/windows) |
| Tailscale | Android | [Google Play: Tailscale](https://play.google.com/store/apps/details?id=com.tailscale.ipn) |
| Tailscale | Pi 5 | [Official Linux installation](https://tailscale.com/docs/install/linux); commands in the Tailscale guide below |
| Moonlight Game Streaming | Android | [Google Play: Moonlight](https://play.google.com/store/apps/details?id=com.limelight) |
| Moonlight Qt | Pi 5 | [Official Raspberry Pi package instructions](https://github.com/moonlight-stream/moonlight-docs/wiki/Installing-Moonlight-Qt-on-Raspberry-Pi-4); commands in the Pi client guide below |
| Raspberry Pi Imager, only if you need an OS | Another computer | [Raspberry Pi software downloads](https://www.raspberrypi.com/software/) |

## 1. Prepare the Raspberry Pi, if needed

Follow [Prepare a Raspberry Pi 5](../platforms/raspberry-pi/prepare-pi5.md).
If it already has the right OS and a working desktop, use the version check there
and skip the OS installation. **Writing an OS image erases the selected storage.**

**Checkpoint:** the Pi opens a desktop, reaches the internet, and plays sound
through your chosen speakers or TV.

## 2. Set up Sunshine on the Windows PC

Follow [Install Sunshine on Windows](../tools/sunshine/host-windows.md) through
its setup checkpoint. It covers the installer, the local settings page, and
keeping the PC available. Return here before starting pairing.

**Checkpoint:** Sunshine's settings open on the PC, you have created its local
username/password, and the Applications list includes **Desktop**.

## 3. Put all three devices on Tailscale

Follow [Connect Windows, Android, and Pi to Tailscale](../tools/tailscale/setup-devices.md).
Install it on **every** device, sign into the same account, and copy the Windows
PC's Tailscale IPv4 address. It looks like `100.x.x.x`.

Keep that address handy. Both clients will use the **PC's** address, not their own.
You do not need router port forwarding, a Tailscale exit node, or subnet routing
for this arrangement. Leave Sunshine's UPnP setting disabled.

**Checkpoint:** all three devices appear in your Tailscale device list, and the
Pi can reach the PC using the connection check in that guide.

## 4. Install Moonlight on the clients

- On the phone/tablet, follow [Moonlight on Android](../tools/moonlight/client-android.md).
- On the Pi, follow [Moonlight on Raspberry Pi 5](../tools/moonlight/client-raspberry-pi.md).

Each guide ends when Moonlight is open with conservative starting settings. You
can complete one client and come back for the other later.

## 5. Add and pair the Windows PC

Do this on Android first, then repeat it separately on the Pi:

1. Check that Tailscale is connected on the PC and the client you are using.
2. In **Moonlight on the client**, choose **Add PC** or the **+** button.
3. Enter the Windows PC's Tailscale IPv4 address from step 3. Enter only the
   address, without `https://` or a port number. Add it even if another PC tile
   was found automatically on your home network.
4. Select the PC tile. Moonlight displays a pairing PIN. Leave it on screen.
5. On the **Windows PC**, open [Sunshine's local settings](https://localhost:47990/)
   and sign in with the Sunshine username/password created in step 2.
6. Select **PIN**, enter the code shown by this client, give it a name such as
   `Android phone` or `Pi 5`, and submit it.
7. Back in Moonlight, the PC should now open a list of applications, including
   **Desktop**. If the PIN expired, request a fresh one and repeat the entry.

The Tailscale sign-in, Sunshine settings password, and Moonlight pairing PIN are
three different things. Your clients do not need the Sunshine settings password.
Approve only pairing requests you started yourself.

Moonlight may merge the manually entered address into an existing PC tile and
prefer a reachable local address while at home. Keep the Tailscale address saved;
the different-network check below is what verifies away-from-home connectivity.

**Checkpoint:** each client shows the PC's application list after adding its
Tailscale address. Automatic PC discovery is not required.

## 6. Try the desktop, then a game

1. In Moonlight, choose **Desktop**. You should see the same desktop as the PC's
   monitor. On Android, swipe to move the mouse and tap to click; a three-finger
   tap opens the keyboard. On the Pi, use its keyboard and mouse.
2. Open an ordinary application and try typing. Play something with sound on the
   PC and check that sound reaches the client.
3. Launch your game through the streamed desktop, as you would when sitting at
   the PC. Start with a game you already know works locally.
4. If you want a controller, connect it to the **client** and complete the
   [Windows controller setup](../tools/sunshine/host-windows.md#optional-controller-support).
   Streaming a desktop with mouse input can work even when controller support
   has not been installed.
5. Play briefly and check picture, sound, and input. Start with 720p, 30 frames
   per second, and 5 Mbps; then increase one setting at a time. These are suggested
   starting values, not a tested performance guarantee.
6. Close the game from inside the game. On the Pi, **Ctrl+Alt+Shift+Q** disconnects
   the stream. On Android, use Home to leave the stream, reopen Moonlight, and
   use **Quit Session** from its application list if a session remains active.

Disconnecting alone can leave a game running on Windows. Close or save it before
quitting the session. Test that you can reconnect before moving to the other client.

## 7. Test away-from-home access before relying on it

Do this only after the same-network setup above works with the Tailscale address.

1. Leave the PC switched on, awake, connected to the internet, and signed into
   Windows. Keep Sunshine and Tailscale running.
2. On an Android phone with mobile data, switch **Wi-Fi off**, check Tailscale is
   connected, and open the same PC tile in Moonlight. Streaming uses mobile data;
   keep this first check short.
3. Open Desktop, test sound/input, disconnect, then turn Wi-Fi back on. A tablet
   without mobile data can use another network instead.
4. For the Pi, move it to a different internet connection or a phone hotspot and
   repeat the test. Disconnect its home Ethernet cable if testing via a hotspot.
   Leave Tailscale connected and use the same PC address. A hotspot can relay the
   connection or perform differently; results depend on both networks.

**Success:** both clients can independently stream picture, sound, and input,
disconnect, and reconnect. Passing a home-network check does not verify an
away-from-home route; record the result for each one you actually try.

## Next time you want to play

1. Make sure the PC is awake with Sunshine and Tailscale running.
2. Connect Tailscale on the chosen client, then open Moonlight.
3. Select the PC and Desktop, then start the game. Pairing normally stays saved.

This setup does not wake a powered-off PC. Keep physical access or a trusted
person available until restart, sleep, and recovery behavior have been tested.

## If something fails

Use [Troubleshoot this setup](../troubleshooting/sunshine-moonlight-tailscale.md)
for missing PCs, pairing failures, firewall checks, black screens, sound, and
slow connections. Change one thing at a time and retest the failing checkpoint.

## Remove access or undo the setup

For a lost client, remove it from Tailscale's device list and revoke its Sunshine
pairing. Merely deleting a PC tile in Moonlight is not access revocation. The
[Sunshine](../tools/sunshine/host-windows.md#remove-access-or-uninstall),
[Tailscale](../tools/tailscale/setup-devices.md#disconnect-or-remove-a-device),
and client guides explain removal. Restore any Windows sleep settings you changed
if you no longer need the PC available remotely.

## Research basis and verification record

This walkthrough combines the official procedures linked from each tool page.
The combination has not been run on project hardware. App stores and package
repositories can supply different versions from the release pages.

| Component | Research scope on 2026-10-16 | Hands-on result |
| --- | --- | --- |
| Sunshine | Stable release `v2026.914.233613`, Windows AMD64 installer and configuration docs | Not tested |
| Android client | Moonlight Android `v12.2` release and Play listing; Tailscale Android 8+ instructions | Not tested |
| Pi client | Moonlight Qt `v6.2.0` release; official Raspberry Pi OS 12+ package instructions | Not tested |
| Pi platform | Pi 5, 64-bit Raspberry Pi OS Desktop, Trixie/Bookworm | Not tested |
| Network | Current Tailscale installation and connection-type documentation | Local and away-from-home paths not tested |

Official starting points: [Moonlight setup and Tailscale integration](https://github.com/moonlight-stream/moonlight-docs/wiki/Setup-Guide),
[Sunshine installation](https://docs.lizardbyte.dev/projects/sunshine/v2026.914.233613/md_docs_2getting__started.html),
and [Tailscale quickstart](https://tailscale.com/docs/how-to/quickstart).
