<p align="center">
  <img src="https://dualrdp.com/assets/img/logo.png" alt="DualRDP" width="96">
</p>

<h1 align="center">DualRDP</h1>

<p align="center">Remote-Desktop, alle Engines.<br>WebRTC, natives getunneltes RDP, RDS-Shadowing und RDP im Browser — ohne Portfreigabe.</p>

<p align="center">
  <a href="https://dualrdp.com"><img src="https://img.shields.io/badge/website-dualrdp.com-0A84FF" alt="Website"></a>
  <a href="https://github.com/mavksoft/dualrdp-releases/releases/latest"><img src="https://img.shields.io/github/v/release/mavksoft/dualrdp-releases?label=latest" alt="neuestes Release"></a>
  <img src="https://img.shields.io/badge/plattform-Windows-black" alt="Plattformen">
  <img src="https://img.shields.io/badge/lizenz-kommerziell-orange" alt="kommerzielle Lizenz">
</p>

<p align="center">🌍 <a href="README.es.md">🇪🇸 Español</a> · <a href="README.md">🇬🇧 English</a> · <strong>🇩🇪 Deutsch</strong> · <a href="README.fr.md">🇫🇷 Français</a> · <a href="README.it.md">🇮🇹 Italiano</a> · <a href="README.pt.md">🇵🇹 Português</a></p>

> **Dieses Repository veröffentlicht ausschließlich offizielle Binär-Releases** — der Quellcode ist privat. Signierte Downloads, Prüfsummen und Auto-Update-Feeds.

## Download

| | |
|---|---|
| <img src='https://raw.githubusercontent.com/mavksoft/dualrdp-releases/main/icons/windows.svg' width='15' style='vertical-align:-2px' alt='windows'> **DualRDP (Windows)** | [DualRDP-Setup.exe](https://github.com/mavksoft/dualrdp-releases/releases/latest) — Desktop-App: Remote-Host **und** Viewer in einem Installer |
| <img src='https://raw.githubusercontent.com/mavksoft/dualrdp-releases/main/icons/windows.svg' width='15' style='vertical-align:-2px' alt='windows'> **DualRDP Host (Windows)** | [DualRDP-Host-Setup.exe](https://github.com/mavksoft/dualrdp-releases/releases/latest) — Headless-Installation als Dienst für unbeaufsichtigte Rechner |
| <img src='https://dualrdp.com/assets/img/logo.png' width='15' style='vertical-align:-2px'> **Fleet-Konsole** | [remote.dualrdp.com](https://remote.dualrdp.com) — Rechner, Tunnel und Sitzungen im Browser verwalten |
| <img src='https://dualrdp.com/assets/img/logo.png' width='15' style='vertical-align:-2px'> **Web-RDP-Client** | [app.dualrdp.com](https://app.dualrdp.com) — RDP-Sitzungen im Browser, ganz ohne Installation |
| <img src='https://dualrdp.com/assets/img/logo.png' width='15' style='vertical-align:-2px'> **Website** | [dualrdp.com](https://dualrdp.com) — Konten, Lizenzen und Downloads |

## Was ist das

DualRDP ist ein eigenständiges Remote-Desktop-Produkt: Installiere den Host auf den Rechnern, die du verwaltest, und erreiche sie über die Desktop-App, die Web-Konsole oder einen beliebigen Browser. Jede Verbindung läuft ausgehend über TLS/WebSocket zu unserem Relay — **ohne offene Ports, ohne VPN, ohne Firewall-Änderungen** — mit TURN für strikte Netzwerke.

Vier Engines decken jeden Fall ab: **WebRTC** für flüssiges Desktop-Video/Input, **natives getunneltes RDP** nach `127.0.0.1` (mstsc / Windows App in voller Qualität), **RDS-Shadowing** zum Beitritt in eine bestehende Sitzung und ein **WASM-RDP-Client im Browser**, wenn du nichts installieren kannst.

## Features

- **Multi-Engine-Sitzungen** — WebRTC P2P, natives RDP über einen verschlüsselten lokalen Tunnel, RDS-Sitzungs-Shadowing und RDP im Browser.
- **Keine Portfreigabe** — Hosts wählen sich per WSS/TLS bei `relay.dualrdp.com` ein; TURN meistert harte NATs.
- **Zwei Zugänge** — Rechner ans Konto binden oder ad-hoc per ID + Passwort verbinden (Standalone-Modus, kein Konto nötig).
- **Maschinen-Lobby** — Live-Thumbnails, Online-Status, Direktverbindung, Gruppierung nach Standort/Konto.
- **Dateimanager** — Remote-Laufwerke durchsuchen, Uploads und Downloads innerhalb der Sitzung.
- **Remote-Konsole** — CMD/PowerShell-Shell-Kanal pro Rechner.
- **Energie & Präsenz** — Wake-on-LAN, Neustart, Koffein/Wachhalten, damit ein schlafender Host die Sitzung nie ablehnt.
- **Fleet-Updates** — jede Komponente aktualisiert sich über Ed25519-signierte Manifeste.
- **Sechs Sprachen** — ES / EN / FR / IT / DE / PT.

## So wird es genutzt

1. Auf [dualrdp.com](https://dualrdp.com) registrieren.
2. Auf jedem Zielrechner **DualRDP** installieren (oder **DualRDP Host** für Headless-Systeme) — er registriert sich unter deinem Konto mit einer Maschinen-ID oder bleibt standalone mit eigener ID + Passwort.
3. Die [Fleet-Konsole](https://remote.dualrdp.com) oder die Desktop-App öffnen — deine Rechner erscheinen mit Live-Status und Thumbnails.
4. Pro Sitzung die Engine wählen: WebRTC-Desktop, nativer RDP-Tunnel, Shadowing einer bestehenden Sitzung oder Browser-RDP.

## Inhalt dieses Repositories

- `DualRDP-Setup-<version>.exe` — Windows-Desktop-Installer (Host + Viewer)
- `DualRDP-Host-Setup-<version>.exe` — Headless-Host-Installer (nur Dienst)
- `drdp_engine.exe`, `drdp_remote.exe`, `drdp_supervisor.exe`, `drdp_tray.exe` — signierte Agent-Binaries für den Fleet-Updater
- `dualrdp_app_ui.zip` — Update-Paket für den In-App-Updater
- `fleet.json` — signiertes Versionsmanifest (Ed25519) für den Auto-Updater
- `*.sha256` — Prüfsummen für jedes Binary

[Neuestes Release](https://github.com/mavksoft/dualrdp-releases/releases/latest)

## FAQ

**Ist der Verkehr verschlüsselt?**
Ja — WebRTC-Sitzungen laufen Ende-zu-Ende über DTLS-SRTP; Tunnel-, Konsolen- und RDP-Verkehr reist in TLS-WebSocket zum Relay, und natives RDP legt seine eigene NLA-Schicht obendrauf. Das Relay reicht nur Bytes weiter; die Autorisierung kommt immer vom Portal oder vom Passwort des Hosts selbst.

**Brauche ich offene Ports oder ein VPN?**
Nein. Der Host baut nur ausgehende Verbindungen auf (WSS/443 + TURN). Wenn ausgehendes 443 geht, geht DualRDP.

**App oder Host — welcher Installer?**
**DualRDP-Setup** ist die Voll-App auf dem Rechner, an dem du sitzt, *und* auf den Zielen (Host + Viewer). **DualRDP-Host-Setup** ist der minimale Dienst für Headless-/unbeaufsichtigte Endpunkte.

**Verbinden ohne Konto?**
Ja — Standalone-Modus: Der Host zeigt eine ID, du vergibst ein Passwort. Gelegentliche Sitzungen sind kostenlos mit Tageslimits; kontogebundene Rechner bekommen den vollen Funktionsumfang.

**Koexistiert es mit DynamicDNSPro?**
Ja — es sind getrennte Produkte: eigene Dienste, Ports, Pfade, Registry-Schlüssel und Relay-Infrastruktur. Beide laufen auf demselben Rechner.

**Wo sind der macOS-Viewer und QuickSupport-Builds?**
Auf der Roadmap — zuerst erscheinen die Windows-Desktop-App und der Host.
