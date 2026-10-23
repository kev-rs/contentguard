# Content Guard

**A free content filter for macOS that blocks adult websites in every browser and app, even when a VPN is on.**

Content Guard is for parents and for anyone who has decided this content shouldn't be one click away. Most free blockers are a browser add-on or a list of sites in a settings file, and they're easy to get around. Content Guard filters traffic at the system level, underneath every app, so switching browsers, turning on a VPN or changing DNS settings doesn't get around it.

> The source code is private while the app is in development. This page describes what it does and how it works.

## Status

| | |
|---|---|
| ✅ Working | System-level network filter, signed and running on macOS 26. Tested blocking in Safari, Chrome, Firefox and other apps, and in Safari with a VPN on |
| 🔧 In progress | Older macOS versions (macOS 14 still lets one kind of traffic through), an on-device image classifier, the settings app |
| ⬜ Planned | First public release, then iPhone, Android, Windows and Linux |

## How it works

Content Guard uses Apple's content-filter system extension (`NEFilterDataProvider`). macOS shows it every new network connection and asks "allow or block?" before any data moves. Because that check happens below the browser and above the VPN, it doesn't matter how the browser looked up the site.

It checks each connection three ways:

1. **The site name** the app asked for, when macOS provides it.
2. **The site name inside the encrypted connection's first message** (the TLS "SNI" field), for apps that connect straight to an IP address.
3. **Fail-closed:** a connection to the public internet that can't be identified is blocked, not allowed.

## Ways around a blocker, and how it handles them

Before the app, I ran a script-based version on my own Mac and tried to break it. Each item below is a real leak found that way, and the app's design closes it.

| Way around it | Why simpler blockers miss it | How Content Guard handles it |
|---|---|---|
| Browser "secure DNS" (DNS-over-HTTPS) | Chrome and Firefox look up sites themselves, skipping the system's DNS and hosts file | Filters the connection itself, not the DNS lookup |
| Turning on a VPN | The VPN brings its own DNS server, which doesn't filter anything | The filter sits above the VPN tunnel |
| Safari under a VPN | Safari follows the VPN's DNS and ignores the hosts file | Same filter for every app, Safari included |
| Browser cache | A site visited before the block loads again from the cache, with no new connection | Clear the caches once at setup (done by the script version; coming to the app's installer) |
| Changing the hosts file or DNS | Anyone with admin rights can edit them | The app doesn't depend on either |

One honest limit: an admin can still turn a content filter off in System Settings. Content Guard makes getting around it hard, not impossible.

## What I learned

- **DNS:** how names become IP addresses, the hosts file, DNS caching (`killall mDNSResponder` to flush it on macOS), and how DNS-over-HTTPS gets around all of it
- **VPNs:** how a VPN changes routing and DNS, and why a system VPN can't be stopped from a script
- **Configuration profiles** (`.mobileconfig`): locking browser settings, the same way IT teams manage Macs through MDM
- **Ports and protocols:** TCP vs. UDP, and why QUIC (UDP port 443) needs its own rule
- **macOS security:** system extensions, Full Disk Access, System Integrity Protection, code signing
- **Background services:** `launchd` jobs that check and repair the setup on a schedule

## How it was built

Content Guard is built with **Claude Code**, Anthropic's AI coding tool. Claude wrote the code. I picked the problem, decided what it had to do, ran every build on my own Mac, and tested it by trying to get around it. Several of the leaks above are ones I found while testing.

## Contact

Kevin Brooks Santana · kevbs.dev@gmail.com
