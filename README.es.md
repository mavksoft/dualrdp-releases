<p align="center">
  <img src="https://dualrdp.com/assets/img/logo.png" alt="DualRDP" width="96">
</p>

<h1 align="center">DualRDP</h1>

<p align="center">Escritorio remoto, todos los motores.<br>WebRTC, RDP nativo tunelado, RDS Shadowing y RDP en el navegador — sin abrir puertos.</p>

<p align="center">
  <a href="https://dualrdp.com"><img src="https://img.shields.io/badge/web-dualrdp.com-0A84FF" alt="web"></a>
  <a href="https://github.com/mavksoft/dualrdp-releases/releases/latest"><img src="https://img.shields.io/github/v/release/mavksoft/dualrdp-releases?label=%C3%BAltima" alt="última release"></a>
  <img src="https://img.shields.io/badge/plataforma-Windows-black" alt="plataformas">
  <img src="https://img.shields.io/badge/licencia-comercial-orange" alt="licencia comercial">
</p>

<p align="center">🌍 <strong>🇪🇸 Español</strong> · <a href="README.md">🇬🇧 English</a> · <a href="README.de.md">🇩🇪 Deutsch</a> · <a href="README.fr.md">🇫🇷 Français</a> · <a href="README.it.md">🇮🇹 Italiano</a> · <a href="README.pt.md">🇵🇹 Português</a></p>

> **Este repositorio publica solo binarios oficiales de las releases** — el código fuente es privado. Descargas firmadas, checksums y feeds de auto-actualización.

## Descargas

| | |
|---|---|
| <img src='https://raw.githubusercontent.com/mavksoft/dualrdp-releases/main/icons/windows.svg' width='15' style='vertical-align:-2px' alt='windows'> **DualRDP (Windows)** | [DualRDP-Setup.exe](https://github.com/mavksoft/dualrdp-releases/releases/latest) — app de escritorio: host remoto **y** visor en un solo instalador |
| <img src='https://raw.githubusercontent.com/mavksoft/dualrdp-releases/main/icons/windows.svg' width='15' style='vertical-align:-2px' alt='windows'> **DualRDP Host (Windows)** | [DualRDP-Host-Setup.exe](https://github.com/mavksoft/dualrdp-releases/releases/latest) — instalación headless como servicio para equipos desatendidos |
| <img src='https://dualrdp.com/assets/img/logo.png' width='15' style='vertical-align:-2px'> **Consola de flota** | [remote.dualrdp.com](https://remote.dualrdp.com) — gestiona equipos, túneles y sesiones desde el navegador |
| <img src='https://dualrdp.com/assets/img/logo.png' width='15' style='vertical-align:-2px'> **Cliente RDP web** | [app.dualrdp.com](https://app.dualrdp.com) — sesiones RDP en el navegador, sin instalar nada |
| <img src='https://dualrdp.com/assets/img/logo.png' width='15' style='vertical-align:-2px'> **Web** | [dualrdp.com](https://dualrdp.com) — cuentas, licencias y descargas |

## Qué es

DualRDP es un producto de escritorio remoto autocontenido: instalas el host en los equipos que gestionas y accedes a ellos desde la app de escritorio, la consola web o un navegador cualquiera. Toda conexión sale por TLS/WebSocket hacia nuestro relay — **sin abrir puertos, sin VPN, sin tocar el firewall** — con TURN para redes restrictivas.

Cuatro motores cubren cada caso: **WebRTC** para vídeo/entrada fluidos, **RDP nativo tunelado** a `127.0.0.1` (mstsc / Windows App a máxima fidelidad), **RDS Shadowing** para unirte a una sesión existente y un **cliente RDP WASM en el navegador** cuando no puedes instalar nada.

## Características

- **Sesiones multi-motor** — WebRTC P2P, RDP nativo a través de un túnel local cifrado, shadowing de sesiones RDS y RDP en el navegador.
- **Cero apertura de puertos** — los hosts salen hacia `relay.dualrdp.com` por WSS/TLS; TURN resuelve los NAT estrictos.
- **Dos formas de entrar** — vincula equipos a tu cuenta o conecta al momento por ID + contraseña (modo standalone, sin cuenta).
- **Lobby de equipos** — miniaturas en vivo, estado online, conexión directa, agrupación por sede/cuenta.
- **Gestor de archivos** — explora unidades remotas, sube y descarga dentro de la sesión.
- **Consola remota** — canal shell CMD/PowerShell por equipo.
- **Energía y presencia** — Wake-on-LAN, reinicio, cafeína/anti-suspensión para que un equipo dormido nunca rechace tu sesión.
- **Actualización de flota** — cada componente se auto-actualiza con manifiestos firmados Ed25519.
- **Seis idiomas** — ES / EN / FR / IT / DE / PT.

## Cómo se usa

1. Regístrate en [dualrdp.com](https://dualrdp.com).
2. En cada equipo al que quieras acceder, instala **DualRDP** (o **DualRDP Host** en equipos headless) — se registra en tu cuenta con un ID de máquina, o queda standalone con su propio ID + contraseña.
3. Abre la [consola de flota](https://remote.dualrdp.com) o la app de escritorio — tus equipos aparecen con estado y miniaturas en vivo.
4. Elige el motor por sesión: escritorio WebRTC, túnel RDP nativo, shadowing de una sesión existente o RDP en el navegador.

## Qué hay en este repositorio

- `DualRDP-Setup-<version>.exe` — instalador de la app de escritorio Windows (host + visor)
- `DualRDP-Host-Setup-<version>.exe` — instalador del host headless (solo servicio)
- `drdp_engine.exe`, `drdp_remote.exe`, `drdp_supervisor.exe`, `drdp_tray.exe` — binarios firmados del agente para el updater de flota
- `dualrdp_app_ui.zip` — paquete de actualización para el updater in-app
- `fleet.json` — manifiesto de versión firmado (Ed25519) que lee el auto-updater
- `*.sha256` — checksums de cada binario

[Última release](https://github.com/mavksoft/dualrdp-releases/releases/latest)

## FAQ

**¿El tráfico va cifrado?**
Sí — las sesiones WebRTC usan DTLS-SRTP de extremo a extremo; el tráfico de túnel, consola y RDP viaja dentro de WebSocket TLS hacia el relay, y RDP nativo añade su propia capa NLA encima. El relay solo reenvía bytes; la autorización siempre la da el portal o la contraseña del propio equipo.

**¿Hace falta abrir puertos o VPN?**
No. El host solo hace conexiones salientes (WSS/443 + TURN). Si sale el 443, DualRDP funciona.

**¿App u Host — qué instalador?**
**DualRDP-Setup** es la app completa tanto en el equipo desde el que te sientas como en los que accedes (host + visor). **DualRDP-Host-Setup** es el servicio mínimo para equipos headless/desatendidos.

**¿Puedo conectar sin cuenta?**
Sí — modo standalone: el host muestra un ID y tú fijas la contraseña. Las sesiones ocasionales son gratis con límites diarios; los equipos vinculados a cuenta tienen el conjunto completo.

**¿Convive con DynamicDNSPro?**
Sí — son productos separados: servicios, puertos, rutas, claves de registro e infraestructura de relay propios. Ambos pueden correr en la misma máquina.

**¿Y el visor macOS y las builds QuickSupport?**
En el roadmap — primero salen la app de escritorio Windows y el host.
