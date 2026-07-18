# Content Guard

**A free, open-source, on-device content blocker for people who want adult content out of their lives — not just filtered, but genuinely hard to reach.**

> **This is the project's public landing page.** Content Guard is in active daily development in a private repository. The full source will be published here, free, under an OSI-approved license, at the first ship-ready release. Why not sooner? — see [Why the code is private (for now)](#why-the-code-is-private-for-now).

## What it is

Most content blockers are easy to uninstall, easy to bypass, and stop at a domain list. Content Guard is built for the person who *wants* to be protected from themselves in a weak moment:

- **System-level blocking on macOS** — a signed system extension (`NEFilterDataProvider`) filters network traffic beneath every app and browser: Safari, Chrome, Firefox, native apps — above VPNs and above browser DoH. Not a browser plugin you can switch off in two clicks.
- **On-device AI content classification** — a browser companion runs a trained image classifier entirely locally to blur the sexually provocative imagery that domain lists can never catch: the suggestive thumbnails, the "almost" content that pulls people back in — judged by pose, context, and intent, not by skin or clothing style.
- **Private by architecture** — no cloud, no account, no telemetry. Nothing you browse ever leaves your device, and the filter that sees your traffic is code you will be able to read.
- **Free, forever** — no subscription, no premium tier. This exists to help people, not to bill them.

## Who it's for

People fighting compulsive pornography use. Parents. Anyone who has decided this content should not have a path to them — and wants that decision to *hold*, the way someone quitting alcohol doesn't keep a bottle in the cupboard.

## Status & roadmap

| Stage | |
|---|---|
| ✅ In progress | macOS: system-wide network filter (live, wire-verified) + in-browser AI classifier (working builds, daily iteration) |
| ⬜ Next | Hardening & bypass red-teaming → **first public release, full source opens here** |
| ⬜ Then | iPhone & iPad, Android, Windows, Linux — old and new devices alike |

## Why the code is private (for now)

Content Guard is safety software. Its users install it sincerely — and some of them, in a weak moment, will turn around and search for holes in it. Publishing the blocklists, the classifier, and the bypass defenses while they are half-finished would hand out working bypass recipes before the defenses are complete, and would let unfinished builds circulate as if they were reliable protection. For a tool like this, a broken promise of safety is worse than none.

The moment the first release is ship-ready, everything opens here: the filter engine, the app, the classifier pipeline — under an OSI-approved license.

## Contact

Kevin Brooks Santana — kevbs.dev@gmail.com
Reviewers and collaborators: read access to the development repository is available on request.
