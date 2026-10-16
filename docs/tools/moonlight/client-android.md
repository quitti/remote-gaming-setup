# Install Moonlight on an Android phone or tablet

[Home](../../../README.md) · [Moonlight](README.md) · [Complete walkthrough](../../scenarios/windows-sunshine-tailscale.md)

- **Status:** Draft; not hardware-tested.
- **Role:** Client.
- **Sources last checked:** 2026-10-16.
- **Research scope:** Moonlight Android `v12.2` release and official Play listing;
  Android 8+ is required by the Tailscale part of this setup.

## Before installing

Complete [Tailscale setup on Android](../tailscale/setup-devices.md#android).
Keep the Windows PC's Tailscale IPv4 address ready. Sunshine should already be
running on that PC. You do not install Sunshine on the phone or tablet.

## 1. Get Moonlight

1. On Android, open [Moonlight Game Streaming in Google Play](https://play.google.com/store/apps/details?id=com.limelight).
   You can also reach this listing through [Moonlight's official website](https://moonlight-stream.org/).
2. Install and open it. No separate Moonlight account is required.
3. If Android asks for nearby-device or local-network access for discovery/input,
   read the prompt and allow the access needed by your chosen controls. Manually
   adding the PC through Tailscale is covered in the walkthrough.

**Expected result:** Moonlight opens to its PC list. An empty list is fine.

## 2. Use modest starting settings

Open Moonlight's gear/settings button before starting a stream. Setting names
can vary by release; use the matching resolution, frame-rate, and bitrate controls.

| Setting | Suggested first value |
| --- | --- |
| Resolution | 1280 × 720 / 720p |
| Frame rate | 30 FPS |
| Video bitrate | 5 Mbps |
| Video codec | Automatic |
| HDR | Off |
| Audio | Stereo |

Resolution controls picture detail; FPS means frames per second; bitrate controls
how much video data is sent. These are conservative troubleshooting starting
values, not a measured recommendation for your particular phone or network.

## 3. Prepare your controls

You can test Desktop with the touch screen. In Moonlight's trackpad-style touch
mode, swipe to move the PC mouse, tap once to click, and tap with three fingers
to show the keyboard. Use that mode for this first check if you have changed
touch options previously.

For a physical controller, connect it to Android with USB or pair it in Android's
Bluetooth settings. Follow the controller maker's pairing instructions. Also
complete [Sunshine's Windows controller setup](../sunshine/host-windows.md#optional-controller-support).
Moonlight's on-screen gamepad likewise needs working host-side controller support.

**Checkpoint:** Tailscale is connected and Moonlight is open with the starting
settings. Continue with [add and pair the PC](../../scenarios/windows-sunshine-tailscale.md#5-add-and-pair-the-windows-pc).

## Disconnect, update, or remove

Use Android Home to leave a stream, then reopen Moonlight and use **Quit Session**
from its application list if the session is still active. Save and close the game
first if you want it to stop running on the PC.

Update Moonlight through Google Play. Uninstall it through Android's app settings
if no longer needed. To remove remote access as well, revoke its Sunshine pairing
and [remove the device from Tailscale](../tailscale/setup-devices.md#disconnect-or-remove-a-device).

For an offline PC or failed connection, see
[troubleshooting](../../troubleshooting/sunshine-moonlight-tailscale.md).

## Sources

All checked 2026-10-16; installation and playback have not been tested here.

- [Official Moonlight website](https://moonlight-stream.org/): Android download source.
- [Google Play listing](https://play.google.com/store/apps/details?id=com.limelight): app identity and distribution.
- [Android release](https://github.com/moonlight-stream/moonlight-android/releases/tag/v12.2): researched client release.
- [Moonlight setup guide](https://github.com/moonlight-stream/moonlight-docs/wiki/Setup-Guide): touch input, controllers, and session handling.
