# Troubleshoot Sunshine, Moonlight, and Tailscale

[Home](../../README.md) · [Troubleshooting](README.md) · [Setup walkthrough](../scenarios/windows-sunshine-tailscale.md)

- **Status:** Draft diagnostic guidance; fixes have not been reproduced on project hardware.
- **Sources last checked:** 2026-10-16.
- **Scope:** Windows Sunshine host, Android/Pi 5 clients, default Sunshine ports.

Work through the checks for your symptom. Change one setting at a time. Keep the
Windows monitor and a local keyboard available while testing.

## The PC is missing, offline, or cannot be added

1. Make sure the PC is powered on and awake. On the PC, open
   [Sunshine's local settings](https://localhost:47990/). If that fails, resolve
   the [host setup](../tools/sunshine/host-windows.md) before changing networking.
2. Check Tailscale is connected on **both** devices, under the same account and
   tailnet. Resolve any sign-in, expiry, or device-approval warning.
3. Add the PC manually in Moonlight using **the Windows PC's Tailscale IPv4**.
   Automatic discovery and your home `192.168…` address are not the basis of
   this guide's remote connection.
4. Use the [Tailscale connection check](../tools/tailscale/setup-devices.md#check-the-connection).
   No reply points to a network/account/device problem. A reply confirms a
   Tailscale path, but does not establish that Sunshine can accept a stream.
5. If Tailscale works but Moonlight cannot connect, check incoming connections
   are allowed on Tailscale's Windows client and inspect the firewall below.
   On an existing managed tailnet, its owner may need to permit client-to-PC
   streaming traffic. Keep the existing policy intact.

## Pairing PIN fails or the settings page is inaccessible from the client

Enter the **current client's** PIN on the **Windows PC**, in Sunshine's **PIN**
page. Request a new PIN if it expired. The Sunshine local username/password is
not the Tailscale login or the pairing PIN.

This guide limits the settings page to localhost. Opening
`https://PC_TAILSCALE_IP:47990` from a client can therefore be denied even when
streaming works. Enter the code locally; do not enable internet-wide web UI
access to fix a pairing problem.

## Check Windows Firewall without turning it off

Sunshine's installer normally creates firewall rules. Check those first. Do not
disable Windows Firewall or add router port forwarding for this Tailscale setup.

If the installed rules do not permit traffic from the clients' Tailscale addresses,
you can add the two scoped rules below. They allow only Sunshine's default
streaming ports from the **specific client IPs** you list. These are Windows
host rules, not router settings. Administrator access is required.

1. Copy the Android and Pi **Tailscale IPv4 addresses** from the Tailscale device
   list. These are the clients' addresses, unlike the PC address used in Moonlight.
2. On Windows, open Start, type `wf.msc`, and open **Windows Defender Firewall
   with Advanced Security**. Select **Inbound Rules → New Rule → Custom**.
3. For **Program**, select **This program path** and browse to your installed
   `sunshine.exe`, normally under `C:\Program Files\Sunshine`. Select the actual
   executable; the install location may differ.
4. For **Protocol and Ports**, choose **TCP**, set **Local port → Specific Ports**
   to `47984,47989,48010`, and leave the remote port as **All Ports**.
5. On **Scope**, leave the local address selection unchanged. Under **remote IP
   addresses**, choose **These IP addresses** and add each client's Tailscale
   IPv4 address. Check these are the two devices you intend to allow.
6. Choose **Allow the connection**. Apply it to Domain, Private, and Public
   profiles so a network-profile change does not break this address-scoped rule.
   Name it `Sunshine Tailscale TCP` and finish.
7. Repeat the custom rule with the same program and remote IP scope, choosing
   **UDP** and local ports `47998,47999,48000,48002,48010`.
   Name it `Sunshine Tailscale UDP`.
8. Retry adding the PC/starting Desktop. If an explicit block rule or managed
   security product is involved, an allow rule may not override it; consult its
   administrator or documentation rather than switching the product off.

Port `47990` administers Sunshine and is intentionally omitted. Discovery port
`5353` is not needed for manually adding the Tailscale address. If you changed
Sunshine's base port, the list above no longer applies; restore defaults or consult
its configuration documentation. Remove these two named rules to undo this
change. If a client's Tailscale address changes after reinstall/re-enrollment,
update the scope. Existing broader rules are not restricted by adding these rules.

## The stream starts but the picture is black or closes

Confirm the Windows monitor is connected, enabled, and awake, and that the desktop
is usable locally. Test **Desktop** instead of a particular game. Check Sunshine's
**Troubleshooting** logs for display/encoder errors. Update the GPU driver using
the manufacturer's tools, and keep HDR off during the baseline test.

A working desktop with one failing game points to that game's capture/input
behavior; a failed desktop points to the host/streaming path. This guide does not
set up virtual displays or fix unsupported graphics hardware.

## Pi display or decoder error

Check you installed the native `moonlight-qt` package on **Raspberry Pi OS 64-bit**
Trixie or Bookworm. Launch it **at the Pi's local text console**, following
[the Pi client guide](../tools/moonlight/client-raspberry-pi.md#3-launch-it-from-the-pis-local-text-console),
rather than an SSH terminal or the desktop. If the problem mentions unsupported
HEVC on the **host**, try H.264 at 720p/30 FPS as a diagnostic fallback; the Pi 5
will use software decoding for H.264.

Use normal OS updates before adopting old workarounds. Do not blindly add Pi 4
MMAL, legacy graphics-driver, or `gpu_mem` settings to a Pi 5. If the package
repository rejects the OS release, stop and check upstream's supported images.

## Picture works but sound or controls do not

- **No sound:** play audio on Windows locally first. Confirm Moonlight is not
  muted, the client volume is up, and the correct client audio output is selected.
  On the Pi, test the TV/HDMI output outside Moonlight too. Sunshine normally
  captures the host's default audio device; check its audio configuration if
  Windows is playing to a different device than intended.
- **No mouse/typing:** start with Desktop and an ordinary application. Check
  keyboard/mouse input is enabled in Sunshine. Android touch mode and game input
  can differ; confirm the basic touch mouse first.
- **No controller:** connect the controller to the **client**, complete the
  [host driver setup](../tools/sunshine/host-windows.md#optional-controller-support),
  and test it in Windows `joy.cpl` during a stream. If it appears there, investigate
  the game's controller settings. If absent there, investigate driver/backend
  selection and client detection before changing game settings.

## Works at home but fails away, or feels slow

Check the away client has internet access and Tailscale is connected, and that
Moonlight uses the PC's `100.…` address. On Android, another VPN/ad blocker can
occupy the VPN slot. Try a different external network to distinguish a network
restriction from a PC problem.

Use [Tailscale's connection check](../tools/tailscale/setup-devices.md#check-the-connection).
`direct` is the preferred gaming path; `relay`/`DERP` can impose additional
latency or limit throughput. A relay is not proof of a broken account or an
unencrypted connection. Follow [Tailscale's connectivity documentation](https://tailscale.com/docs/reference/device-connectivity)
if a relay persists; there is no guaranteed low-latency result on every network.

Return to 720p/30 FPS/5 Mbps, test one client, and pause large downloads. Prefer
Ethernet or a strong 5 GHz link. For away play, the home connection's **upload**
and the client's **download** both matter, as does delay. Increase picture quality
only after picture, sound, and input remain reliable at the baseline.

## Sources

All checked 2026-10-16. Diagnostic suggestions still need reproduction/testing.

- [Moonlight setup and firewall ports](https://github.com/moonlight-stream/moonlight-docs/wiki/Setup-Guide): pairing, protocol ports, input. This guide uses scoped rules instead of upstream's broad firewall-testing examples.
- [Microsoft firewall configuration](https://learn.microsoft.com/en-us/windows/security/operating-system-security/network-security/windows-firewall/configure): custom rules, program/port restrictions, IP scopes, and profiles.
- [Sunshine configuration](https://docs.lizardbyte.dev/projects/sunshine/v2026.914.233613/md_docs_2configuration.html): origin, port offsets, input, and audio.
- [Sunshine initial setup and logs](https://docs.lizardbyte.dev/projects/sunshine/v2026.914.233613/md_docs_2getting__started.html): display capture, logs, pairing, and Windows drivers.
- [Tailscale connection types](https://tailscale.com/docs/reference/connection-types): ping/status, direct versus relayed connections.
