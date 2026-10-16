# Remote Gaming Setup

Markdown guides for setting up game streaming, remote access, and the supporting
tools across Linux PCs, Windows PCs, Raspberry Pi, Android phones and tablets,
and potentially iPhone and iPad.

**Project status:** the first researched setup guide is available as a draft.
Hardware verification is still pending; the remaining topic indexes describe
planned coverage. A platform or topic appearing here does not imply verified
compatibility.

## First setup guide

[Play Windows games on Android or Raspberry Pi 5 through Tailscale](docs/scenarios/windows-sunshine-tailscale.md)
walks through Sunshine on Windows, Moonlight on each client, and Tailscale on all
devices. It includes official downloads, installation steps, pairing, a first
game, away-from-home checks, troubleshooting, and removing access. Written for
first-time users; Raspberry Pi instructions target **Pi 5 with Raspberry Pi OS
64-bit Desktop (Trixie or Bookworm)**.

## Find your starting point

- **New to remote gaming?** Start with [Getting started](docs/getting-started.md)
  for the host/client model and the information to gather before setup.
- **Have a goal in mind?** Browse [Scenarios](docs/scenarios/README.md), such as
  playing elsewhere at home or connecting while away.
- **Have a device in mind?** Browse [Platforms](docs/platforms/README.md).
- **Already chose software?** Browse [Tools](docs/tools/README.md).
- **Need background?** Browse [Shared reference](docs/reference/README.md).
- **Something is failing?** Browse [Troubleshooting](docs/troubleshooting/README.md).

## Repository layout

```text
README.md                      Project entry point and roadmap
CONTRIBUTING.md                 Writing conventions and verification requirements
AGENTS.md                       Research, writing, and Git instructions for agents
LICENSE                         CC BY-SA 4.0 legal text
docs/
  getting-started.md            Roles, scope, and choosing a reading path
  scenarios/                   Goal-based walkthroughs linking to setup guides
    README.md
  platforms/                   Device entry points and OS-specific preparation
    README.md
    linux/README.md
    windows/README.md
    raspberry-pi/README.md
    android/README.md
    ios/README.md
  tools/                       Canonical installation and configuration guides
    README.md
  reference/                   Shared networking, security, and hardware topics
    README.md
  troubleshooting/             Symptom-based diagnosis and fixes
    README.md
templates/
  guide.md                     Starting point for a tested setup guide
```

As content is written, a tool gets its own folder under `docs/tools/`, with pages
such as `README.md`, `host-linux.md`, and `client-android.md`. Add only the
combinations that have useful content; there is no need to create an empty page
for every tool, role, and platform.

Platform pages collect relevant links and platform preparation. Scenario pages
connect the steps into a complete workflow. Both link to the same tool guides so
installation instructions stay in one place.

## Suggested writing order

1. Verify the [first Windows/Android/Pi 5 guide](docs/scenarios/windows-sunshine-tailscale.md)
   on real hardware and record versions, picture, audio, input, and reconnect results.
2. Add Linux host coverage and other client/device variants, reusing shared material.
3. Verify the Tailscale away-from-home steps after local streaming works, then
   document additional networking methods only when needed.
4. Cover remote desktop administration, startup and recovery, display handling,
   controllers, and performance tuning as needed by tested setups.
5. Evaluate iPhone/iPad coverage and publish device-specific findings before
   presenting it as supported.

## Contributing and maintenance

Start with [Contributing](CONTRIBUTING.md) and the [guide template](templates/guide.md).
Agents should also follow [AGENTS.md](AGENTS.md) for research, human-readable
instructions, and repository workflow.

Use current primary sources, cite the facts they support, and distinguish
documentation research from a setup actually tested on hardware. Write for a
reader following the steps on their own: identify the device, explain unfamiliar
terms, and show what success looks like.

Work directly on `main` by default. Commits and pushes go to `main`; development
branches and pull requests are only needed when explicitly requested. Use small,
focused commits and ordinary pushes without rewriting shared history.

The project needs no documentation generator for now. Relative links and ordinary
Markdown keep it usable in a repository browser or a local editor.

## License

Except where otherwise noted, the original documentation, Markdown templates,
and original illustrations in this repository are licensed under
[Creative Commons Attribution-ShareAlike 4.0 International (CC BY-SA 4.0)](https://creativecommons.org/licenses/by-sa/4.0/).
See [LICENSE](LICENSE) for the full terms.

You may copy, modify, and reuse this material commercially with attribution and
indication of changes. Distributed adaptations must use the same or a compatible
license. Credit the Remote Gaming Setup contributors and include links to
[this project](https://github.com/quitti/remote-gaming-setup) and the license.

Third-party material retains its own terms and should be marked accordingly.
Choose a software license separately if reusable scripts are added;
[Creative Commons recommends software-specific licenses for code](https://creativecommons.org/faq/#can-i-apply-a-creative-commons-license-to-software).
