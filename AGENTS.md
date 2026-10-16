# Agent instructions

These instructions apply throughout this repository. Follow explicit user
instructions when they change the scope or workflow.

## Project and scope

This is a Markdown-first collection of remote gaming and remote access guides.
Read [README.md](README.md), [CONTRIBUTING.md](CONTRIBUTING.md), and the relevant
section index before editing. Preserve the separation between scenarios,
platform preparation, tool procedures, shared reference, and troubleshooting.
Link to canonical instructions rather than copying them across guides.

Keep changes focused. Do not add a site generator, dependencies, automation, or
an exhaustive set of placeholder pages unless the work calls for them. iOS/iPadOS
coverage remains exploratory until a concrete combination has been evaluated.

## Research and evidence

- Research version-sensitive claims before publishing or updating them: install
  commands, package names, supported platforms/hardware, app availability,
  permissions, network settings, defaults, and known limitations.
- Prefer official documentation, project repositories, release notes, platform
  documentation, and upstream issue reports. Use sources for the exact version,
  OS, device, and role described. Search results and summaries are leads, not
  sufficient evidence by themselves; read the relevant source.
- Use community reports to investigate gaps or workarounds. Identify them as
  reports, include their environment, and avoid presenting one report as a
  universal limitation or verified fix.
- Put descriptive source links beside material claims or in a short Sources
  section that identifies what each source supports. Record when sources were
  checked. Prefer stable official links and version-specific references where
  the instructions depend on a release.
- Resolve conflicting advice using version, platform, and publication context.
  State unresolved uncertainty instead of inventing commands, compatibility,
  performance figures, or missing steps. If sources cannot be accessed, say what
  still needs checking and leave the affected material as Draft or Planned.
- Separate **source review** from **hands-on verification**. Never claim a setup
  was tested because upstream documents it or because Markdown checks pass.
  Record the actual tested hardware, versions, connection, date, and outcome;
  mark unchecked variants explicitly. A prose edit does not renew verification.
- Follow the status labels in CONTRIBUTING.md. Mark an affected guide Needs
  recheck when there is evidence its verified procedure no longer holds.
- Summarize sources in original wording. Keep quotations brief, attribute reused
  material, and check its terms before copying text, screenshots, or diagrams.

## Human-readable guides

- Lead with the outcome, the host/client roles, and what the reader needs. Assume
  a capable hobbyist who may be new to this particular tool or platform.
- Use plain language, short paragraphs, descriptive headings, and meaningful link
  text. Define unfamiliar terms on first use. Avoid filler, marketing language,
  unexplained acronyms, and claims such as "easy" or "just works."
- Give one clear path through a tested combination first. Put optional tuning
  and alternatives after the working baseline, with the reason to choose them.
- Use numbered steps for a sequence and bullets for independent requirements.
  Identify which device, account, application, and shell each action uses.
- Put commands in fenced blocks with a language label. Omit shell prompt symbols,
  explain placeholders before use, and keep expected output separate from input.
  State when privileges are required and what a consequential command changes.
- Name settings as they appear in the documented version. Screenshots supplement
  text; a reader should not need an image alone to identify the next action.
- Give observable expected results at useful checkpoints and an end-to-end
  acceptance check. Troubleshooting should start from a symptom, explain what
  each check establishes, and link to the relevant correction.
- Explain remote access scope, authentication, and revocation when access is
  enabled. Prefer restricted access and specific rules over blanket firewall or
  security disabling. Never include real credentials or private connection data.
- Include removal or rollback for configuration changes, and explain consequences
  for reconnecting or recovering an unattended host.

## Git workflow

- Work directly on `main` by default. Do not create development branches,
  worktrees, or pull requests unless the user asks for that workflow.
- When committing and pushing, use `main` and a normal `git push origin main`.
  No pull request or separate review branch is required by this project.
- Check the current branch, working tree, and diff before committing. Preserve
  unrelated edits; do not reset, discard, or silently include them. If the checkout
  is on another branch, inspect its state before switching and preserve its work.
- Keep commits focused and use short, descriptive messages, such as
  `docs: add Android client setup` or `docs: correct Linux prerequisites`.
  No elaborate commit-message scheme is required.
- Never force-push or rewrite shared history unless explicitly instructed. If a
  push is rejected because the remote moved, inspect and reconcile the changes
  before retrying a normal push.

## Before finishing

- Read the edited pages as a person following the guide. Check step order,
  prerequisites, host/client labels, commands, and expected results.
- Check relative links, code fences, and `git diff --check`. Update relevant
  indexes when adding or moving a page. Do not add test infrastructure for a
  prose-only change; use checks appropriate to the actual edits.
- Run a setup or script only when the environment and task authorize doing so.
  Hardware that is unavailable cannot be reported as tested.
- Report what changed, which checks were actually performed, and material gaps
  in verification. Preserve the CC BY-SA 4.0 license notices for original
  documentation, templates, and illustrations, along with third-party notices.
  Choose a separate software license before adding reusable scripts.
