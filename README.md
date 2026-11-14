<p align="center">
  <img src="https://dualrdp.com/assets/img/logo.png" alt="DualRDP" width="96">
</p>

<h1 align="center">DualRDP</h1>

<p align="center">Remote desktop, every engine.<br>WebRTC, native tunneled RDP, RDS Shadowing and in-browser RDP — without opening ports.</p>

<p align="center">
  <a href="https://dualrdp.com"><img src="https://img.shields.io/badge/website-dualrdp.com-0A84FF" alt="website"></a>
  <a href="https://github.com/mavksoft/dualrdp-releases/releases/latest"><img src="https://img.shields.io/github/v/release/mavksoft/dualrdp-releases?label=latest" alt="latest release"></a>
  <img src="https://img.shields.io/badge/platform-Windows-black" alt="platforms">
  <img src="https://img.shields.io/badge/license-commercial-orange" alt="commercial license">
</p>

<p align="center">🌍 <a href="README.es.md">🇪🇸 Español</a> · <strong>🇬🇧 English</strong> · <a href="README.de.md">🇩🇪 Deutsch</a> · <a href="README.fr.md">🇫🇷 Français</a> · <a href="README.it.md">🇮🇹 Italiano</a> · <a href="README.pt.md">🇵🇹 Português</a></p>

> **This repository publishes official binary releases only** — the source code is private. Signed downloads, checksums and auto-update feeds.

## Download

| | |
|---|---|
| <img src='https://raw.githubusercontent.com/mavksoft/dualrdp-releases/main/icons/windows.svg' width='15' style='vertical-align:-2px' alt='windows'> **DualRDP (Windows)** | [DualRDP-Setup.exe](https://github.com/mavksoft/dualrdp-releases/releases/latest) — desktop app: remote host **and** viewer in one install |
| <img src='https://raw.githubusercontent.com/mavksoft/dualrdp-releases/main/icons/windows.svg' width='15' style='vertical-align:-2px' alt='windows'> **DualRDP Host (Windows)** | [DualRDP-Host-Setup.exe](https://github.com/mavksoft/dualrdp-releases/releases/latest) — headless service install for unattended machines |
| <img src='https://dualrdp.com/assets/img/logo.png' width='15' style='vertical-align:-2px'> **Fleet console** | [remote.dualrdp.com](https://remote.dualrdp.com) — manage your machines, tunnels and sessions from the browser |
| <img src='https://dualrdp.com/assets/img/logo.png' width='15' style='vertical-align:-2px'> **Web RDP client** | [app.dualrdp.com](https://app.dualrdp.com) — RDP sessions in the browser, no install |
| <img src='https://dualrdp.com/assets/img/logo.png' width='15' style='vertical-align:-2px'> **Website** | [dualrdp.com](https://dualrdp.com) — accounts, licensing and downloads |

## What it is

DualRDP is a self-contained remote-desktop product: install the host on the machines you manage and reach them from the desktop app, the web console or a plain browser. Every connection rides outbound-only TLS/WebSocket to our relay — **no open ports, no VPN, no firewall changes** — with TURN for strict networks.

Four engines cover every case: **WebRTC** for fluid desktop video/input, **native RDP tunneled** to `127.0.0.1` (mstsc / Windows App at full fidelity), **RDS Shadowing** to join an existing session, and a **WASM RDP client in the browser** when you can't install anything.

## Features

- **Multi-engine sessions** — WebRTC P2P, native RDP through an encrypted local tunnel, RDS session shadowing and in-browser RDP.
- **Zero port forwarding** — hosts dial out to `relay.dualrdp.com` over WSS/TLS; TURN handles locked-down NAT.
- **Two ways in** — link machines to your account, or connect ad-hoc by ID + password (standalone mode, no account needed).
- **Machine lobby** — live thumbnails, online status, direct connect, grouping by site/account.
- **File manager** — browse remote drives, upload and download inside the session.
- **Remote console** — CMD/PowerShell/SSH-style shell channel per machine.
- **Power & presence** — Wake-on-LAN, reboot, caffeine/keep-awake so a sleeping host never refuses your session.
- **Fleet updates** — every component auto-updates from Ed25519-signed manifests.
- **Six languages** — ES / EN / FR / IT / DE / PT.

## How to use it

1. Sign up at [dualrdp.com](https://dualrdp.com).
2. On each machine you want to reach, install **DualRDP** (or **DualRDP Host** for headless boxes) — it registers under your account with a machine ID, or stays standalone with its own ID + password.
3. Open the [fleet console](https://remote.dualrdp.com) or the desktop app — your machines appear with live status and thumbnails.
4. Pick the engine per session: WebRTC desktop, native RDP tunnel, shadow an existing session, or browser RDP.

## What's in this repository

- `DualRDP-Setup-<version>.exe` — Windows desktop app installer (host + viewer)
- `DualRDP-Host-Setup-<version>.exe` — headless host installer (service only)
- `drdp_engine.exe`, `drdp_remote.exe`, `drdp_supervisor.exe`, `drdp_tray.exe` — signed agent binaries for the fleet updater
- `dualrdp_app_ui.zip` — update bundle for the in-app updater
- `fleet.json` — signed version manifest (Ed25519) read by the auto-updater
- `*.sha256` — checksums for every binary

[Latest release](https://github.com/mavksoft/dualrdp-releases/releases/latest)

## FAQ

**Is the traffic encrypted?**
Yes — WebRTC sessions use DTLS-SRTP end to end; tunnel, console and RDP traffic travels inside TLS WebSocket to the relay, and native RDP adds its own NLA layer on top. The relay only forwards bytes; authorization always comes from the portal or the host's own password.

**Do I need to open ports or a VPN?**
No. The host only makes outbound connections (WSS/443 + TURN). If outbound 443 works, DualRDP works.

**App or Host — which installer?**
**DualRDP-Setup** is the full desktop app on the machine you sit at *and* the machines you reach (host + viewer). **DualRDP-Host-Setup** is the minimal service for headless/unattended endpoints.

**Can I connect without an account?**
Yes — standalone mode: the host shows an ID and you set a password. Occasional sessions are free with daily limits; account-linked machines get the full feature set.

**Does it coexist with DynamicDNSPro?**
Yes — they're separate products: own services, ports, paths, registry keys and relay infrastructure. Both can run on the same machine.

**Where are the macOS viewer and QuickSupport builds?**
On the roadmap — the Windows desktop app and host ship first.
