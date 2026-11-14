<p align="center">
  <img src="https://dualrdp.com/assets/img/logo.png" alt="DualRDP" width="96">
</p>

<h1 align="center">DualRDP</h1>

<p align="center">Desktop remoto, tutti i motori.<br>WebRTC, RDP nativo tunnelizzato, RDS Shadowing e RDP nel browser — senza aprire porte.</p>

<p align="center">
  <a href="https://dualrdp.com"><img src="https://img.shields.io/badge/sito-dualrdp.com-0A84FF" alt="sito"></a>
  <a href="https://github.com/mavksoft/dualrdp-releases/releases/latest"><img src="https://img.shields.io/github/v/release/mavksoft/dualrdp-releases?label=ultima" alt="ultima release"></a>
  <img src="https://img.shields.io/badge/piattaforma-Windows-black" alt="piattaforme">
  <img src="https://img.shields.io/badge/licenza-commerciale-orange" alt="licenza commerciale">
</p>

<p align="center">🌍 <a href="README.es.md">🇪🇸 Español</a> · <a href="README.md">🇬🇧 English</a> · <a href="README.de.md">🇩🇪 Deutsch</a> · <a href="README.fr.md">🇫🇷 Français</a> · <strong>🇮🇹 Italiano</strong> · <a href="README.pt.md">🇵🇹 Português</a></p>

> **Questo repository pubblica solo i binari ufficiali delle release** — il codice sorgente è privato. Download firmati, checksum e feed di auto-aggiornamento.

## Download

| | |
|---|---|
| <img src='https://raw.githubusercontent.com/mavksoft/dualrdp-releases/main/icons/windows.svg' width='15' style='vertical-align:-2px' alt='windows'> **DualRDP (Windows)** | [DualRDP-Setup.exe](https://github.com/mavksoft/dualrdp-releases/releases/latest) — app desktop: host remoto **e** viewer in un unico installer |
| <img src='https://raw.githubusercontent.com/mavksoft/dualrdp-releases/main/icons/windows.svg' width='15' style='vertical-align:-2px' alt='windows'> **DualRDP Host (Windows)** | [DualRDP-Host-Setup.exe](https://github.com/mavksoft/dualrdp-releases/releases/latest) — installazione headless come servizio per macchine non presidiate |
| <img src='https://dualrdp.com/assets/img/logo.png' width='15' style='vertical-align:-2px'> **Console di flotta** | [remote.dualrdp.com](https://remote.dualrdp.com) — gestisci macchine, tunnel e sessioni dal browser |
| <img src='https://dualrdp.com/assets/img/logo.png' width='15' style='vertical-align:-2px'> **Client RDP web** | [app.dualrdp.com](https://app.dualrdp.com) — sessioni RDP nel browser, senza installare nulla |
| <img src='https://dualrdp.com/assets/img/logo.png' width='15' style='vertical-align:-2px'> **Sito** | [dualrdp.com](https://dualrdp.com) — account, licenze e download |

## Cos'è

DualRDP è un prodotto di desktop remoto autonomo: installi l'host sulle macchine che gestisci e le raggiungi dall'app desktop, dalla console web o da un qualsiasi browser. Ogni connessione esce in TLS/WebSocket verso il nostro relay — **senza porte aperte, senza VPN, senza toccare il firewall** — con TURN per le reti restrittive.

Quattro motori coprono ogni caso: **WebRTC** per video/input fluidi, **RDP nativo tunnelizzato** su `127.0.0.1` (mstsc / Windows App alla massima fedeltà), **RDS Shadowing** per entrare in una sessione esistente e un **client RDP WASM nel browser** quando non puoi installare nulla.

## Funzionalità

- **Sessioni multi-motore** — WebRTC P2P, RDP nativo attraverso un tunnel locale cifrato, shadowing di sessioni RDS e RDP nel browser.
- **Zero porte aperte** — gli host escono verso `relay.dualrdp.com` in WSS/TLS; TURN gestisce i NAT rigidi.
- **Due modi di entrare** — collega le macchine al tuo account o connettiti ad hoc con ID + password (modalità standalone, senza account).
- **Lobby delle macchine** — miniature live, stato online, connessione diretta, raggruppamento per sede/account.
- **Gestore file** — sfoglia i dischi remoti, carica e scarica dentro la sessione.
- **Console remota** — canale shell CMD/PowerShell per macchina.
- **Energia e presenza** — Wake-on-LAN, riavvio, caffeina/anti-sospensione perché un host addormentato non rifiuti mai la tua sessione.
- **Aggiornamenti di flotta** — ogni componente si auto-aggiorna con manifesti firmati Ed25519.
- **Sei lingue** — ES / EN / FR / IT / DE / PT.

## Come si usa

1. Registrati su [dualrdp.com](https://dualrdp.com).
2. Su ogni macchina da raggiungere installa **DualRDP** (o **DualRDP Host** per le macchine headless) — si registra nel tuo account con un ID macchina, o resta standalone con il proprio ID + password.
3. Apri la [console di flotta](https://remote.dualrdp.com) o l'app desktop — le tue macchine compaiono con stato e miniature live.
4. Scegli il motore per sessione: desktop WebRTC, tunnel RDP nativo, shadowing di una sessione esistente o RDP nel browser.

## Cosa contiene questo repository

- `DualRDP-Setup-<version>.exe` — installer dell'app desktop Windows (host + viewer)
- `DualRDP-Host-Setup-<version>.exe` — installer dell'host headless (solo servizio)
- `drdp_engine.exe`, `drdp_remote.exe`, `drdp_supervisor.exe`, `drdp_tray.exe` — binari agent firmati per l'updater di flotta
- `dualrdp_app_ui.zip` — pacchetto di aggiornamento per l'updater in-app
- `fleet.json` — manifesto di versione firmato (Ed25519) letto dall'auto-updater
- `*.sha256` — checksum di ogni binario

[Ultima release](https://github.com/mavksoft/dualrdp-releases/releases/latest)

## FAQ

**Il traffico è cifrato?**
Sì — le sessioni WebRTC usano DTLS-SRTP end-to-end; il traffico di tunnel, console e RDP viaggia in WebSocket TLS verso il relay, e l'RDP nativo aggiunge il proprio strato NLA. Il relay inoltra solo byte; l'autorizzazione arriva sempre dal portale o dalla password dell'host stesso.

**Servono porte aperte o una VPN?**
No. L'host fa solo connessioni in uscita (WSS/443 + TURN). Se esce la 443, DualRDP funziona.

**App o Host — quale installer?**
**DualRDP-Setup** è l'app completa sia sulla macchina da cui lavori *sia* sulle destinazioni (host + viewer). **DualRDP-Host-Setup** è il servizio minimo per endpoint headless/non presidiati.

**Posso connettermi senza account?**
Sì — modalità standalone: l'host mostra un ID e tu imposti la password. Le sessioni occasionali sono gratis con limiti giornalieri; le macchine collegate all'account hanno tutte le funzioni.

**Coesiste con DynamicDNSPro?**
Sì — sono prodotti separati: servizi, porte, percorsi, chiavi di registro e infrastruttura relay propri. Entrambi girano sulla stessa macchina.

**E il viewer macOS e le build QuickSupport?**
Nella roadmap — prima escono l'app desktop Windows e l'host.
