# Install Sunshine on a Windows gaming PC

[Home](../../../README.md) · [Sunshine](README.md) · [Complete walkthrough](../../scenarios/windows-sunshine-tailscale.md)

- **Status:** Draft; not hardware-tested.
- **Role:** Host — this PC runs the games.
- **Sources last checked:** 2026-10-16.
- **Research version:** Sunshine `v2026.914.233613`, Windows AMD64 installer.

## What you need

Use a Windows 11 Intel/AMD x64 PC where the game already works. You need an
administrator account to install Sunshine. Keep a monitor connected and enabled,
and update the graphics driver through your PC/GPU manufacturer's official tools.
Windows on ARM, a PC without a monitor, and multiple-display tuning are outside
this guide.

## 1. Download and install

1. On the PC, open the [official stable release](https://github.com/LizardByte/Sunshine/releases/latest).
2. Find **Assets** or the download table, and choose
   **`Sunshine-Windows-AMD64-installer.msi`**. AMD64 means ordinary 64-bit Intel
   **or** AMD PCs; it does not mean you need an AMD graphics card. Avoid the
   source archives, debugging files, and lite ZIP for this guide.
3. Open the downloaded file and follow the installer. Approve the Windows
   administrator prompt for this installation. Keep the Sunshine background
   service and its Windows Firewall integration enabled if offered. A service
   keeps the program running in the background.
4. Read optional component descriptions before selecting them. A paid Virtual
   HID Driver is optional; see [controller support](#optional-controller-support)
   before installing additional drivers. Reboot if requested by the installer.

The current official instructions prefer MSI. If you already installed an older
Sunshine using a different installer type, follow the official migration note:
uninstall that installation before changing installer types. Save your settings
first; this guide otherwise assumes a fresh setup.

**Expected result:** Sunshine is installed. The Windows installer normally runs
it as a service; do not start a second copy if it is already running.

## 2. Create the Sunshine settings login

1. On the **Windows PC**, open a browser and enter
   [https://localhost:47990/](https://localhost:47990/). `localhost` means this PC.
   You can also use **Open Sunshine** from Sunshine's tray icon near the clock.
2. Sunshine uses a certificate it created itself, so a browser privacy/certificate
   warning is expected at **this exact local address**. Check the address, then
   use the browser's **Advanced** option to continue to localhost. This exception
   is only for your local Sunshine page.
3. Create a Sunshine username and a strong, unique password. Store them in your
   password manager. This local login is separate from Windows and Tailscale.
4. Sign in. Open **Applications** and confirm **Desktop** exists. If you removed
   it, add an application named `Desktop` with no launch command and save it.

**Expected result:** you can open Sunshine settings and see the Desktop entry.
There is no need to add individual games for the first test; launch them from
the streamed desktop.

## 3. Keep the first setup reachable

1. In Sunshine **Configuration → Network**, leave **UPnP** disabled. Keep the
   default ports and leave the external-IP field at its default. Tailscale will
   provide the connection address.
2. Set the web UI access/origin option (`origin_web_ui_allowed`) to **Only
   localhost** / `pc`, then save and apply/restart Sunshine if requested. Pairing
   codes will be entered on this PC. This restricts the administration page;
   it does not disable Moonlight streaming.
3. In Windows **Settings → System → Power** (or **Power & battery**), find the
   screen/sleep timeouts. Note the current values, then set **sleep when plugged
   in** to **Never** for the initial test. Menu wording differs between Windows
   updates. Keep a laptop on power with its lid open.
4. For the first test, leave Windows signed in, the PC unlocked, and its monitor
   on. Do not disconnect the monitor or introduce automatic-login changes.

**Checkpoint:** settings work on the PC, Desktop is listed, and the PC remains
awake. Return to [step 3 of the walkthrough](../../scenarios/windows-sunshine-tailscale.md#3-put-all-three-devices-on-tailscale).

## Pair a client

Once Moonlight and Tailscale are ready, follow
[the walkthrough's pairing steps](../../scenarios/windows-sunshine-tailscale.md#5-add-and-pair-the-windows-pc).
Each client displays its own PIN; submit it through the **PIN** page on the PC.

## Optional controller support

Connect your controller to the **Android device or Pi**, using USB for the first
check where possible. A controller plugged into the PC is not a remote client
controller. Sunshine needs a Windows driver to present remote controller input
to games as a local gamepad.

The current Sunshine documentation offers two choices:

| Choice | What to know |
| --- | --- |
| Virtual HID Driver | Actively supported by LizardByte; an optional **paid per-machine license** is required for driver-backed input. Follow the linked official driver instructions if choosing it. |
| ViGEmBus | Free legacy fallback for Xbox 360/PS4 controller emulation, but **retired and no longer maintained**. It does not provide the newer driver's full features. |

Keyboard/mouse desktop testing can be completed before choosing either driver.
For the free legacy controller path documented by Sunshine:

1. On Windows, check **Settings → Apps → Installed apps** for ViGEm Bus Driver.
   If absent, use the installer under **Assets** in
   [Nefarius's official ViGEmBus 1.22.0 release](https://github.com/nefarius/ViGEmBus/releases/tag/v1.22.0).
   Install it and restart Windows. This installs a system driver; use the upstream
   download rather than a repackaged driver site.
2. Open Sunshine **Configuration → Input**. For the virtual gamepad driver
   (`gamepad_driver`), choose **only ViGEmBus** (`vigembus`). Save/apply the setting.
   Set the emulated controller type (`gamepad`) to **Xbox 360** (`x360`) for this
   baseline and leave controller input enabled.
3. Connect a gamepad to your client and start a Moonlight stream. On the streamed
   Windows desktop, open Start, type `joy.cpl`, and open it. Select the virtual
   controller and its properties, then test buttons and sticks.
4. If that works, launch your game and select its controller input mode if
   necessary. Games can have their own controller restrictions.

For the paid path, use the **Virtual HID Driver** link in
[Sunshine's Windows initial-setup documentation](https://docs.lizardbyte.dev/projects/sunshine/v2026.914.233613/md_docs_2getting__started.html).
The researched Sunshine release requires driver version `2026.914.1218.10` or
newer. Confirm its current installation/license instructions before buying.

**Expected result:** the client gamepad responds in the Windows controller test
and in the game. A working mouse alone does not verify controller forwarding.

## If setup fails

If the local settings page will not open, use the Start menu to open **Services**
and check that the Sunshine service is running. Avoid launching multiple copies.
For connection, display, or driver problems, see
[the setup troubleshooting guide](../../troubleshooting/sunshine-moonlight-tailscale.md).
Sunshine's **Troubleshooting** page contains logs; inspect them locally before
sharing, as logs can contain device and network details.

## Remove access or uninstall

- To revoke a client pairing, use Sunshine's client removal controls on the
  **Troubleshooting** page. If the installed version offers only **Unpair All**,
  it revokes every client; the clients you keep will need to pair again.
- For a lost device, also [remove it from Tailscale](../tailscale/setup-devices.md#disconnect-or-remove-a-device).
- To remove Sunshine, open **Settings → Apps → Installed apps**, choose Sunshine,
  and uninstall it. Restore the sleep timeout you recorded. Remove optional
  controller drivers only if no other application uses them.

## Sources

All sources checked 2026-10-16. None replaces hands-on verification.

- [Sunshine stable release](https://github.com/LizardByte/Sunshine/releases/tag/v2026.914.233613): researched release and installer assets.
- [Versioned installation and initial setup](https://docs.lizardbyte.dev/projects/sunshine/v2026.914.233613/md_docs_2getting__started.html): Windows service, local settings, Desktop, pairing, and driver choices.
- [Versioned configuration](https://docs.lizardbyte.dev/projects/sunshine/v2026.914.233613/md_docs_2configuration.html): web UI origin, UPnP, controller backend and emulation.
- [ViGEmBus release](https://github.com/nefarius/ViGEmBus/releases/tag/v1.22.0): legacy driver and end-of-life status.
