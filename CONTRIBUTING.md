# Writing guides

The aim is a small set of reproducible guides that can be combined into different
remote gaming setups. Keep instructions close to the tool or platform that owns
them, and link to shared material instead of copying it.

## Where content belongs

| Location | Owns | Links to |
| --- | --- | --- |
| `docs/scenarios/` | A complete workflow for a user goal and its acceptance checks | Platform preparation, tool procedures, shared reference |
| `docs/platforms/` | Device/OS preparation, limitations, and navigation | Relevant host and client guides |
| `docs/tools/` | Tool installation, pairing, configuration, updating, and removal | Platform prerequisites and shared concepts |
| `docs/reference/` | Cross-cutting explanations and reusable procedures | Tool-specific details where needed |
| `docs/troubleshooting/` | Diagnosis by symptom and recovery steps | The procedure or setting that needs correction |

If a step could belong in two places, choose one canonical page and link to it.
For example, a scenario should link to a tool's pairing procedure instead of
repeating it. Platform preparation should be independent of a particular tool;
tool-specific OS settings belong with the tool's setup guide.

## Page and directory conventions

- Use lowercase, hyphen-separated names and relative Markdown links.
- Use `README.md` as each directory's index. Keep the root README short enough to
  serve as the main entry point.
- Use stable tool slugs, such as `docs/tools/<tool>/host-linux.md` and
  `docs/tools/<tool>/client-android.md`. Split a page when the steps materially
  differ, rather than making readers interpret several operating systems at once.
- Keep Raspberry Pi under its own entry point because board, OS image, and display
  setup may matter. Link to Linux instructions when they genuinely apply.
- Keep Android phone/tablet and iPhone/iPad coverage together initially. Split it
  only when their instructions differ enough to justify separate pages.
- Put images and small supporting files in an `assets/` directory beside the page
  that uses them. Prefer text instructions; screenshots should supplement them.
- Add scripts only when a guide needs them. Put reusable scripts under a root
  `scripts/` directory, and document what they change and how to undo it.

## Scope and status

Use these plain-text status labels near the top of a guide:

- **Planned:** an outline or backlog item; instructions are not ready to follow.
- **Draft:** instructions exist but have not been verified end to end.
- **Verified:** the documented setup passed its checks on the listed hardware and
  versions, on the stated date.
- **Needs recheck:** a known change or failure has made earlier verification
  unreliable; say which part needs attention.

Verification applies to the recorded combination, not every device in the same
platform family. Keep planned topics in an index until there is enough material
for a useful page. Do not create empty directories or links to nonexistent guides.

## What a setup guide should contain

Start from [the guide template](templates/guide.md). State the intended outcome,
the host and client roles, requirements, and exact tested environment. Include
commands with their shell and target device identified, expected results, a
usable end-to-end check, common failures, and undo/removal instructions.

For commands that require elevated privileges or change firewall, network,
account, or startup settings, explain the effect before the command. Describe
the scope of remote access and relevant access controls in guides that enable it.
Use obvious placeholders for addresses and credentials; never commit real
secrets, device identifiers, or private connection details.

Link to official installation, compatibility, and release documentation where
possible. Record the date a guide was actually checked; editing prose alone does
not refresh its verification date. Distinguish observations from assumptions and
call out any steps or device variants that were not tested.

For version-sensitive facts, read the relevant primary sources and record their
scope and the date reviewed. Keep this research date separate from the date of
hands-on verification. Agent contributors must follow the detailed research and
human-readable writing guidelines in [AGENTS.md](AGENTS.md); these are also a
useful checklist for human authors.

Before submitting, follow the guide on the stated setup, check its links and code
blocks, and ensure readers can tell whether they have succeeded. Screenshots
should omit private details and match the documented versions.

## Git conventions

Work directly on `main` and push commits to `main`. Development branches,
worktrees, and pull requests are only needed when explicitly requested. Keep
commits focused with descriptive messages, check the diff and links before
committing, and preserve unrelated work. Use ordinary pushes; do not force-push
or rewrite shared history unless explicitly instructed.

## Licensing

Original documentation, Markdown templates, and original illustrations are
licensed under CC BY-SA 4.0, as described in the [README](README.md#license) and
[LICENSE](LICENSE). Contributions to these materials must be available under
the same license.

Attribute third-party material, mark its license or applicable permission, and
preserve its notices; linking to a source does not grant permission to copy it.
Choose a separate software license before adding reusable scripts.
