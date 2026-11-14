<p align="center">
  <img src="https://dualrdp.com/assets/img/logo.png" alt="DualRDP" width="96">
</p>

<h1 align="center">DualRDP</h1>

<p align="center">Bureau à distance, tous les moteurs.<br>WebRTC, RDP natif tunnelisé, RDS Shadowing et RDP dans le navigateur — sans ouverture de ports.</p>

<p align="center">
  <a href="https://dualrdp.com"><img src="https://img.shields.io/badge/site-dualrdp.com-0A84FF" alt="site"></a>
  <a href="https://github.com/mavksoft/dualrdp-releases/releases/latest"><img src="https://img.shields.io/github/v/release/mavksoft/dualrdp-releases?label=derni%C3%A8re" alt="dernière release"></a>
  <img src="https://img.shields.io/badge/plateforme-Windows-black" alt="plateformes">
  <img src="https://img.shields.io/badge/licence-commerciale-orange" alt="licence commerciale">
</p>

<p align="center">🌍 <a href="README.es.md">🇪🇸 Español</a> · <a href="README.md">🇬🇧 English</a> · <a href="README.de.md">🇩🇪 Deutsch</a> · <strong>🇫🇷 Français</strong> · <a href="README.it.md">🇮🇹 Italiano</a> · <a href="README.pt.md">🇵🇹 Português</a></p>

> **Ce dépôt ne publie que les binaires officiels des releases** — le code source est privé. Téléchargements signés, checksums et flux d'auto-mise à jour.

## Téléchargement

| | |
|---|---|
| <img src='https://raw.githubusercontent.com/mavksoft/dualrdp-releases/main/icons/windows.svg' width='15' style='vertical-align:-2px' alt='windows'> **DualRDP (Windows)** | [DualRDP-Setup.exe](https://github.com/mavksoft/dualrdp-releases/releases/latest) — app de bureau : hôte distant **et** viewer dans un seul installateur |
| <img src='https://raw.githubusercontent.com/mavksoft/dualrdp-releases/main/icons/windows.svg' width='15' style='vertical-align:-2px' alt='windows'> **DualRDP Host (Windows)** | [DualRDP-Host-Setup.exe](https://github.com/mavksoft/dualrdp-releases/releases/latest) — installation headless en service pour machines autonomes |
| <img src='https://dualrdp.com/assets/img/logo.png' width='15' style='vertical-align:-2px'> **Console de flotte** | [remote.dualrdp.com](https://remote.dualrdp.com) — gérez machines, tunnels et sessions depuis le navigateur |
| <img src='https://dualrdp.com/assets/img/logo.png' width='15' style='vertical-align:-2px'> **Client RDP web** | [app.dualrdp.com](https://app.dualrdp.com) — sessions RDP dans le navigateur, sans installation |
| <img src='https://dualrdp.com/assets/img/logo.png' width='15' style='vertical-align:-2px'> **Site** | [dualrdp.com](https://dualrdp.com) — comptes, licences et téléchargements |

## De quoi s'agit-il

DualRDP est un produit de bureau à distance autonome : installez l'hôte sur les machines que vous administrez et rejoignez-les depuis l'app de bureau, la console web ou un simple navigateur. Chaque connexion sort en TLS/WebSocket vers notre relay — **sans ports ouverts, sans VPN, sans toucher au pare-feu** — avec TURN pour les réseaux restrictifs.

Quatre moteurs couvrent tous les cas : **WebRTC** pour un vidéo/input fluide, **RDP natif tunnelisé** vers `127.0.0.1` (mstsc / Windows App en pleine fidélité), **RDS Shadowing** pour rejoindre une session existante, et un **client RDP WASM dans le navigateur** quand rien ne peut être installé.

## Fonctionnalités

- **Sessions multi-moteur** — WebRTC P2P, RDP natif via un tunnel local chiffré, shadowing de sessions RDS et RDP dans le navigateur.
- **Zéro port ouvert** — les hôtes appellent `relay.dualrdp.com` en WSS/TLS ; TURN gère les NAT stricts.
- **Deux modes d'accès** — liez les machines à votre compte ou connectez-vous ad hoc par ID + mot de passe (mode standalone, sans compte).
- **Lobby des machines** — miniatures live, statut en ligne, connexion directe, regroupement par site/compte.
- **Gestionnaire de fichiers** — parcourez les disques distants, envoyez et recevez dans la session.
- **Console distante** — canal shell CMD/PowerShell par machine.
- **Énergie & présence** — Wake-on-LAN, redémarrage, caféine/anti-veille pour qu'un hôte endormi ne refuse jamais votre session.
- **Mises à jour de flotte** — chaque composant se met à jour via des manifestes signés Ed25519.
- **Six langues** — ES / EN / FR / IT / DE / PT.

## Mode d'emploi

1. Créez un compte sur [dualrdp.com](https://dualrdp.com).
2. Sur chaque machine à atteindre, installez **DualRDP** (ou **DualRDP Host** pour les machines headless) — elle s'enregistre sous votre compte avec un ID machine, ou reste standalone avec son propre ID + mot de passe.
3. Ouvrez la [console de flotte](https://remote.dualrdp.com) ou l'app de bureau — vos machines apparaissent avec statut et miniatures en direct.
4. Choisissez le moteur par session : bureau WebRTC, tunnel RDP natif, shadowing d'une session existante ou RDP navigateur.

## Contenu de ce dépôt

- `DualRDP-Setup-<version>.exe` — installateur de l'app de bureau Windows (hôte + viewer)
- `DualRDP-Host-Setup-<version>.exe` — installateur de l'hôte headless (service seul)
- `drdp_engine.exe`, `drdp_remote.exe`, `drdp_supervisor.exe`, `drdp_tray.exe` — binaires d'agent signés pour l'updater de flotte
- `dualrdp_app_ui.zip` — bundle de mise à jour pour l'updater intégré
- `fleet.json` — manifeste de version signé (Ed25519) lu par l'auto-updater
- `*.sha256` — checksums de chaque binaire

[Dernière release](https://github.com/mavksoft/dualrdp-releases/releases/latest)

## FAQ

**Le trafic est-il chiffré ?**
Oui — les sessions WebRTC utilisent DTLS-SRTP de bout en bout ; le trafic tunnel, console et RDP voyage en WebSocket TLS vers le relay, et le RDP natif ajoute sa propre couche NLA. Le relay ne fait que relayer des octets ; l'autorisation vient toujours du portail ou du mot de passe de l'hôte.

**Faut-il ouvrir des ports ou un VPN ?**
Non. L'hôte ne fait que des connexions sortantes (WSS/443 + TURN). Si le 443 sortant fonctionne, DualRDP fonctionne.

**App ou Host — quel installateur ?**
**DualRDP-Setup** est l'app complète sur le poste où vous êtes *et* sur les cibles (hôte + viewer). **DualRDP-Host-Setup** est le service minimal pour les endpoints headless/autonomes.

**Connexion sans compte ?**
Oui — mode standalone : l'hôte affiche un ID et vous fixez le mot de passe. Les sessions occasionnelles sont gratuites avec des limites quotidiennes ; les machines liées à un compte ont toutes les fonctions.

**Coexiste-t-il avec DynamicDNSPro ?**
Oui — ce sont des produits séparés : services, ports, chemins, clés de registre et infrastructure relay propres. Les deux tournent sur la même machine.

**Et le viewer macOS et les builds QuickSupport ?**
Sur la feuille de route — l'app de bureau Windows et l'hôte sortent d'abord.
