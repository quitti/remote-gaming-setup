# Platforms

[Home](../../README.md) · [Getting started](../getting-started.md)

Draft setup instructions are available for Windows, Android, and Pi 5 in the
[first walkthrough](../scenarios/windows-sunshine-tailscale.md). They have not been
hardware-tested. The table below describes overall intended coverage, not a tested
compatibility matrix.

| Platform | Initial documentation focus | Details guides should distinguish |
| --- | --- | --- |
| [Linux PC](linux/README.md) | Host and client | Distribution/version, desktop/session type, GPU and driver |
| [Windows PC](windows/README.md) | Host and client | Windows version, GPU and driver, session and startup behavior |
| [Raspberry Pi](raspberry-pi/README.md) | Client first | Board model, OS image/version, display and peripherals |
| [Android](android/README.md) | Phone and tablet clients | Device, Android version, app source, input and screen behavior |
| [iOS / iPadOS](ios/README.md) | Exploratory iPhone and iPad clients | Device, OS version, app availability and device-specific limits |

Each platform directory owns general preparation and device-specific notes.
Installation and configuration for a particular application belong in
[its tool directory](../tools/README.md). Link shared Linux preparation from
Raspberry Pi pages when it applies, and record board-specific exceptions there.

Add distribution- or device-specific pages only when they contain meaningful
differences. Neither a separate Linux distribution tree nor separate phone and
tablet trees are needed before those differences are established.
