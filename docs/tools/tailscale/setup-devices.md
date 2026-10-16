# Connect Windows, Android, and Raspberry Pi 5 with Tailscale

[Home](../../../README.md) · [Tailscale](README.md) · [Complete walkthrough](../../scenarios/windows-sunshine-tailscale.md)

- **Status:** Draft; no device installation or network route tested here.
- **Role:** Private connection between the host and clients.
- **Sources last checked:** 2026-10-16; current official stable-install instructions.

Use one personal Tailscale account on all your own devices. Its private device
network is called a **tailnet**. Follow the steps for all three devices; joining
the Pi alone does not connect the Android device or PC.

## Windows PC

1. On Windows, download Tailscale from the [official Windows page](https://tailscale.com/download/windows).
2. Run the installer and approve its administrator prompt. Open Tailscale from
   Start or its tray icon near the clock (it may be hidden behind the up arrow).
3. Choose **Log in**. Follow the browser sign-in, using the account you want to
   use on all three devices. If this is your first device, finish creating the
   Tailscale account. Protect that sign-in account with multifactor authentication.
4. Confirm Tailscale shows you as connected. In its tray menu, open
   **Preferences → Run unattended** and enable it. This keeps the private network
   available after a Windows sign-out or restart; it does not keep the PC awake,
   sign you into Windows, or create a usable game/display session by itself.
5. Open the [Tailscale device list](https://login.tailscale.com/admin/machines)
   in your browser. Find the Windows PC by its device name and copy its
   **Tailscale IPv4** address. It starts with `100.` and has four numbers separated
   by dots. Save it as “gaming PC Tailscale address.”

For example, `100.101.102.103` has the right shape, but it is **only an example**.
Use your PC's actual address. Do not copy the public internet address or its home
Wi-Fi/Ethernet address instead.

**Expected result:** the PC appears online in your Tailscale device list.

## Android

1. On the phone/tablet, install [Tailscale from Google Play](https://play.google.com/store/apps/details?id=com.tailscale.ipn).
   The current Tailscale app requires Android 8 or later.
2. Open it, choose **Get Started** / **Log in**, and use **the same account and
   sign-in method** you used on the PC. If offered a choice of tailnets, choose
   the same one containing the PC.
3. Accept Android's request to set up the VPN connection. This allows Tailscale
   to carry the private device traffic. Enable/connect Tailscale in the app.
   Keep its notifications enabled so reauthentication warnings are visible.
4. Confirm the device list contains the Windows PC. If a different VPN is active,
   disconnect it for this test; Android normally permits only one active VPN
   service at a time, including some VPN-based ad blockers.

Leave Tailscale connected when switching to Moonlight. No exit node is needed.

**Expected result:** Android is connected to Tailscale and the PC is in its list.

## Raspberry Pi 5

Use a Pi with the [prepared Raspberry Pi OS desktop](../../platforms/raspberry-pi/prepare-pi5.md).
Open its **Terminal** window. Run each command and wait for it to finish.

First, install the download utility if necessary:

```bash
sudo apt update
sudo apt install curl ca-certificates
```

The next command downloads and runs Tailscale's official Linux installer. It adds
the package source and installs the system service, using administrator privileges.
Enter your **Pi user password** if asked; nothing appears while typing it.

```bash
curl -fsSL https://tailscale.com/install.sh | sh
```

Join the private network:

```bash
sudo tailscale up
```

The command prints a sign-in link. Open it in a browser on the Pi, or use another
device to visit that exact link. Sign in with the same Tailscale account as the
PC and Android, and approve the Pi. Treat that one-time link as private.

Then run:

```bash
tailscale status
```

**Expected result:** the Pi is signed in and the device list includes the Windows
PC. Confirm all three devices also appear in the browser's
[Tailscale device list](https://login.tailscale.com/admin/machines).
If device approval is enabled for your tailnet, approve your own pending devices
there before continuing.

## Check the connection

On the **Pi**, run the following, replacing `PC_TAILSCALE_IP` with the Windows
PC's actual Tailscale address saved above. Do not type the placeholder literally.

```bash
tailscale ping PC_TAILSCALE_IP
```

A reply beginning with `pong` confirms a Tailscale path to the PC. A result using
`DERP` is a relay: traffic goes through an intermediate server. The first replies
may use a relay while a direct connection is being established. Run
`tailscale status` again after traffic has flowed to see `direct` or `relay` in
the PC's entry.

A direct connection is preferable for gaming. Relays remain encrypted, but
throughput and latency can be worse. A successful Tailscale ping **does not** prove
that Sunshine's streaming ports are allowed or that video/input work.

**Checkpoint:** all devices are in the same tailnet and the Pi gets replies.
Return to [install the Moonlight clients](../../scenarios/windows-sunshine-tailscale.md#4-install-moonlight-on-the-clients).

## Access scope and keeping access working

A new personal tailnet's initial policy normally allows its devices to reach one
another; on an existing tailnet, access rules may restrict that. This guide assumes
your own devices and an account you control. Do not replace a work/school access
policy with an allow-everything rule. If ping works but streaming fails, use
[the troubleshooting page](../../troubleshooting/sunshine-moonlight-tailscale.md).

Keep **Allow incoming connections** enabled on the Windows host if that option is
shown. A “shields up” setting blocks incoming application traffic.
Sunshine still requires Moonlight pairing independently of Tailscale membership.

If a device later shows an expired key or a sign-in warning, reauthenticate it
before relying on remote access. Keep expiry enabled for this first setup; any
decision to disable it for an unattended host should include a recovery and
revocation plan. Run unattended is a separate setting from key expiry.

## Disconnect or remove a device

- For a temporary pause, disconnect Tailscale in Android or Windows. On the Pi,
  `sudo tailscale down` disconnects it; `sudo tailscale up` reconnects it.
  Remote sessions using that connection will stop working while disconnected.
- To revoke a lost/retired device, open the browser's Tailscale device list,
  select that device's menu, and choose **Remove**. Revoke its Sunshine pairing
  too. A device that can sign in again can rejoin, so secure the sign-in account
  as well if it was compromised.
- Uninstall through Windows **Installed apps** or Android's app settings. On Pi,
  `sudo apt remove tailscale` removes the installed application/service but can
  leave package-source configuration and state behind. Device-list removal is
  separate from uninstalling.

## Sources

All checked 2026-10-16. Client versions and routes have not been tested here.

- [Windows installation](https://tailscale.com/docs/install/windows): installer, tray, and sign-in.
- [Android installation](https://tailscale.com/docs/install/android): Android 8+, VPN permission, and sign-in.
- [Linux installation](https://tailscale.com/docs/install/linux): installer, `tailscale up`, and authorization.
- [Unattended Windows access](https://tailscale.com/docs/how-to/run-unattended): background access and key expiry.
- [Connection types](https://tailscale.com/docs/reference/connection-types): direct/relayed paths and diagnostic output.
- [Access control](https://tailscale.com/docs/features/access-control): tailnet permissions.
- [Initial tailnet policy](https://tailscale.com/docs/reference/examples/acls#allow-all-default-acl): default device-to-device access.
- [Client preferences](https://tailscale.com/docs/features/client/manage-preferences): incoming-connection controls.
- [Android VPN behavior](https://developer.android.com/develop/connectivity/vpn): one active VPN service per user/profile.
- [Remove a device](https://tailscale.com/docs/features/access-control/device-management/how-to/remove): revocation and the difference from uninstalling.
- [Moonlight's Tailscale instructions](https://github.com/moonlight-stream/moonlight-docs/wiki/Setup-Guide#tailscale): manual host address and streaming integration. Prefer Tailscale's own current docs for connection behavior and account limits.
