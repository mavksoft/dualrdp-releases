<p align="center">
  <img src="https://dualrdp.com/assets/img/logo.png" alt="DualRDP" width="96">
</p>

<h1 align="center">DualRDP</h1>

<p align="center">Ambiente remoto, todos os motores.<br>WebRTC, RDP nativo em túnel, RDS Shadowing e RDP no navegador — sem abrir portas.</p>

<p align="center">
  <a href="https://dualrdp.com"><img src="https://img.shields.io/badge/site-dualrdp.com-0A84FF" alt="site"></a>
  <a href="https://github.com/mavksoft/dualrdp-releases/releases/latest"><img src="https://img.shields.io/github/v/release/mavksoft/dualrdp-releases?label=%C3%BAltima" alt="última release"></a>
  <img src="https://img.shields.io/badge/plataforma-Windows-black" alt="plataformas">
  <img src="https://img.shields.io/badge/licen%C3%A7a-comercial-orange" alt="licença comercial">
</p>

<p align="center">🌍 <a href="README.es.md">🇪🇸 Español</a> · <a href="README.md">🇬🇧 English</a> · <a href="README.de.md">🇩🇪 Deutsch</a> · <a href="README.fr.md">🇫🇷 Français</a> · <a href="README.it.md">🇮🇹 Italiano</a> · <strong>🇵🇹 Português</strong></p>

> **Este repositório publica apenas binários oficiais das releases** — o código-fonte é privado. Downloads assinados, checksums e feeds de auto-atualização.

## Descarregar

| | |
|---|---|
| <img src='https://raw.githubusercontent.com/mavksoft/dualrdp-releases/main/icons/windows.svg' width='15' style='vertical-align:-2px' alt='windows'> **DualRDP (Windows)** | [DualRDP-Setup.exe](https://github.com/mavksoft/dualrdp-releases/releases/latest) — app de desktop: host remoto **e** viewer num só instalador |
| <img src='https://raw.githubusercontent.com/mavksoft/dualrdp-releases/main/icons/windows.svg' width='15' style='vertical-align:-2px' alt='windows'> **DualRDP Host (Windows)** | [DualRDP-Host-Setup.exe](https://github.com/mavksoft/dualrdp-releases/releases/latest) — instalação headless como serviço para máquinas autónomas |
| <img src='https://dualrdp.com/assets/img/logo.png' width='15' style='vertical-align:-2px'> **Consola de frota** | [remote.dualrdp.com](https://remote.dualrdp.com) — gere máquinas, túneis e sessões no navegador |
| <img src='https://dualrdp.com/assets/img/logo.png' width='15' style='vertical-align:-2px'> **Cliente RDP web** | [app.dualrdp.com](https://app.dualrdp.com) — sessões RDP no navegador, sem instalar nada |
| <img src='https://dualrdp.com/assets/img/logo.png' width='15' style='vertical-align:-2px'> **Site** | [dualrdp.com](https://dualrdp.com) — contas, licenças e downloads |

## O que é

O DualRDP é um produto de ambiente remoto autónomo: instalas o host nas máquinas que administras e acedes a elas a partir da app de desktop, da consola web ou de um navegador qualquer. Cada ligação sai por TLS/WebSocket para o nosso relay — **sem portas abertas, sem VPN, sem mexer na firewall** — com TURN para redes restritivas.

Quatro motores cobrem todos os casos: **WebRTC** para vídeo/input fluidos, **RDP nativo em túnel** para `127.0.0.1` (mstsc / Windows App em plena fidelidade), **RDS Shadowing** para entrar numa sessão existente e um **cliente RDP WASM no navegador** quando não podes instalar nada.

## Funcionalidades

- **Sessões multi-motor** — WebRTC P2P, RDP nativo através de um túnel local cifrado, shadowing de sessões RDS e RDP no navegador.
- **Zero portas abertas** — os hosts ligam-se a `relay.dualrdp.com` por WSS/TLS; o TURN resolve NATs restritivos.
- **Duas formas de entrar** — vincula máquinas à tua conta ou liga ad hoc por ID + palavra-passe (modo standalone, sem conta).
- **Lobby de máquinas** — miniaturas ao vivo, estado online, ligação direta, agrupamento por sede/conta.
- **Gestor de ficheiros** — explora discos remotos, envia e recebe dentro da sessão.
- **Consola remota** — canal shell CMD/PowerShell por máquina.
- **Energia e presença** — Wake-on-LAN, reinício, cafeína/anti-suspensão para que um host a dormir nunca recuse a tua sessão.
- **Atualizações de frota** — cada componente se auto-atualiza com manifestos assinados Ed25519.
- **Seis idiomas** — ES / EN / FR / IT / DE / PT.

## Como usar

1. Regista-te em [dualrdp.com](https://dualrdp.com).
2. Em cada máquina a que queres aceder, instala o **DualRDP** (ou **DualRDP Host** em máquinas headless) — regista-se na tua conta com um ID de máquina, ou fica standalone com o seu próprio ID + palavra-passe.
3. Abre a [consola de frota](https://remote.dualrdp.com) ou a app de desktop — as tuas máquinas aparecem com estado e miniaturas ao vivo.
4. Escolhe o motor por sessão: desktop WebRTC, túnel RDP nativo, shadowing de uma sessão existente ou RDP no navegador.

## O que há neste repositório

- `DualRDP-Setup-<version>.exe` — instalador da app de desktop Windows (host + viewer)
- `DualRDP-Host-Setup-<version>.exe` — instalador do host headless (só serviço)
- `drdp_engine.exe`, `drdp_remote.exe`, `drdp_supervisor.exe`, `drdp_tray.exe` — binários de agente assinados para o updater de frota
- `dualrdp_app_ui.zip` — pacote de atualização para o updater in-app
- `fleet.json` — manifesto de versão assinado (Ed25519) lido pelo auto-updater
- `*.sha256` — checksums de cada binário

[Última release](https://github.com/mavksoft/dualrdp-releases/releases/latest)

## FAQ

**O tráfego é cifrado?**
Sim — as sessões WebRTC usam DTLS-SRTP ponta-a-ponta; o tráfego de túnel, consola e RDP viaja em WebSocket TLS para o relay, e o RDP nativo acrescenta a sua própria camada NLA. O relay só reenvia bytes; a autorização vem sempre do portal ou da palavra-passe do próprio host.

**Preciso de abrir portas ou VPN?**
Não. O host faz apenas ligações de saída (WSS/443 + TURN). Se a 443 de saída funciona, o DualRDP funciona.

**App ou Host — qual instalador?**
**DualRDP-Setup** é a app completa na máquina onde estás *e* nas de destino (host + viewer). **DualRDP-Host-Setup** é o serviço mínimo para endpoints headless/autónomos.

**Posso ligar sem conta?**
Sim — modo standalone: o host mostra um ID e defines a palavra-passe. As sessões ocasionais são grátis com limites diários; as máquinas vinculadas a uma conta têm o conjunto completo.

**Coexiste com o DynamicDNSPro?**
Sim — são produtos separados: serviços, portas, caminhos, chaves de registo e infraestrutura de relay próprios. Ambos correm na mesma máquina.

**E o viewer macOS e as builds QuickSupport?**
Na roadmap — primeiro saem a app de desktop Windows e o host.
