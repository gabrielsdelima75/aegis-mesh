# Project: AegisMesh Anticheat (CS2)

## Português Brasileiro
### A Forensic & Peer-Validated Integrity System

AegisMesh é uma solução de anticheat híbrida (Client-Server-Peer) desenvolvida especificamente para comunidades privadas de Counter-Strike 2.  
Diferente de soluções comerciais focadas em banimentos automáticos, o AegisMesh foca em fundamentação forense e consenso de rede para apoiar decisões de Overwatch comunitário.

---

## 🚀 Visão Geral
O projeto baseia-se em três pilares fundamentais:

- **Peer-to-Peer Trust Mesh**: Uma corrente de integridade onde os 10 jogadores validam os *heartbeats* uns dos outros, tornando o bypass via emulação virtualmente impossível.  
- **Forensic Evidence Gathering**: Coleta de snapshots (Desktop Duplication API), logs de processos e assinaturas de drivers em tempo real.  
- **Live Admin Dashboard**: Interface web para intervenção imediata, auditoria de processos e inspeção visual *on-demand*.  

---

## 🛠️ Arquitetura Técnica

### 1. Game Server Plugin (C# / CounterStrikeSharp)
- **Gatekeeper**: Gerencia o *handshake* inicial e valida o ingresso apenas de clientes autenticados.  
- **Relay de Consenso**: Atua como o nó central que coordena os desafios aleatórios entre os clientes (*Trust Mesh*).  
- **Telemetria de Partida**: Cruza eventos do jogo (ex: kills através de fumaça) com solicitações automáticas de snapshots no cliente.  

### 2. Desktop Client (C# / .NET 8)
- **Integrity Engine**: Monitora a memória do `cs2.exe`, lista de processos e módulos carregados.  
- **Silent Capture**: Captura de tela via GPU para detecção de overlays externos (ESP/Wallhack).  
- **Consensus Node**: Participa da corrente de hashes da partida, validando a presença de outros nós ativos na rede.  

### 3. Web Admin Panel (ASP.NET Core / SignalR / React)
- **Live Feed**: Visualização em tempo real da "saúde" da rede (*Trust Mesh*).  
- **Snapshot Trigger**: Comando remoto para captura instantânea da tela de qualquer jogador.  
- **Process Explorer**: Lista detalhada de processos, caminhos de executáveis e hashes de arquivos dos clientes conectados.  

---

## 🔒 O Protocolo "Trust Mesh" (Diferencial)
O AegisMesh não confia apenas no reporte do cliente para o servidor.

- Cada cliente gera um hash de integridade que é enviado para o servidor e replicado para *pares* (outros jogadores).  
- O servidor solicita desafios cruzados: “Jogador A, valide o Checksum do Jogador B”.  
- A imprevisibilidade desses desafios impede que um cheat intercepte e falsifique todas as respostas simultaneamente sem causar latência detectável.  

---

## 📂 Estrutura do Repositório
```
├── src/
│   ├── Aegis.Client/          # Aplicação Desktop (WPF/Console)
│   ├── Aegis.Plugin/          # Plugin para CounterStrikeSharp
│   ├── Aegis.Web/             # Painel Administrativo & API SignalR
│   └── Aegis.Shared/          # Modelos de dados e lógica de criptografia
├── docs/                      # Documentação técnica e forense
└── tools/                     # Scripts de auxílio e build
```

---

## 📝 Roadmap de Desenvolvimento
- [ ] **Fase 1**: Handshake básico entre Plugin C# e Cliente .NET.  
- [ ] **Fase 2**: Implementação da Desktop Duplication API para snapshots.  
- [ ] **Fase 3**: Sistema de batimento (*Heartbeat*) e integração com SignalR para comandos web.  
- [ ] **Fase 4**: Implementação da lógica de consenso Peer-to-Peer (*Trust Mesh*).  
- [ ] **Fase 5**: Módulo de Overwatch (Galeria de evidências para julgamento).  

---

## ⚖️ Licença e Ética
Este projeto é destinado estritamente para o uso em comunidades privadas e competitivas, visando a integridade competitiva.  
O AegisMesh coleta dados do sistema para fins de auditoria; o uso implica no consentimento dos jogadores da comunidade.

> **Nota:** Este projeto está em fase de *brainstorm* técnico e prototipagem.

---
## English
---
# Project: AegisMesh Anticheat (CS2)
### A Forensic & Peer-Validated Integrity System

AegisMesh is a hybrid (Client-Server-Peer) anticheat solution developed specifically for private Counter-Strike 2 communities.
Unlike commercial solutions focused on automatic bans, AegisMesh focuses on forensic evidence and network consensus to support community-based Overwatch decisions.

---

## 🚀 Overview
The project is based on three fundamental pillars:

- **Peer-to-Peer Trust Mesh**: An integrity chain where the 10 players validate each other's *heartbeats*, making bypassing via emulation virtually impossible.
- **Forensic Evidence Gathering**: Collection of snapshots (Desktop Duplication API), process logs, and driver signatures in real time.
- **Live Admin Dashboard**: Web interface for immediate intervention, process auditing, and on-demand visual inspection.

---

## 🛠️ Technical Architecture
### 1. Game Server Plugin (C# / CounterStrikeSharp)
- **Gatekeeper**: Manages the initial handshake and validates the entry only of authenticated clients.
- **Consensus Relay**: Acts as the central node that coordinates random challenges between clients (Trust Mesh).
- **Match Telemetry**: Cross-references game events (e.g., kills via smoke) with automatic snapshot requests on the client.

### 2. Desktop Client (C# / .NET 8)
- **Integrity Engine**: Monitors the memory of `cs2.exe`, list of processes, and loaded modules.
- **Silent Capture**: Screenshot capture via GPU for detection of external overlays (ESP/Wallhack).
- **Consensus Node**: Participates in the match's hash stream, validating the presence of other active nodes on the network.

### 3. Web Admin Panel (ASP.NET Core / SignalR / React)
- **Live Feed**: Real-time visualization of the network's "health" (*Trust Mesh*).
- **Snapshot Trigger**: Remote command for instant screen capture of any player.
- **Process Explorer**: Detailed list of processes, executable paths, and file hashes of connected clients.

---

## 🔒 The "Trust Mesh" Protocol (Differential)
AegisMesh does not rely solely on client reporting to the server.

- Each client generates an integrity hash that is sent to the server and replicated to *peers* (other players). - The server requests cross-challenges: “Player A, validate Player B’s checksum.”

- The unpredictability of these challenges prevents a cheat from intercepting and falsifying all responses simultaneously without causing detectable latency.

---

## 📂 Repository Structure
```
├── src/
│ ├── Aegis.Client/ # Desktop Application (WPF/Console)
│ ├── Aegis.Plugin/ # Plugin for CounterStrikeSharp
│ ├── Aegis.Web/ # Administrative Panel & SignalR API
│ └── Aegis.Shared/ # Data models and cryptography logic
├── docs/ # Technical and forensic documentation
└── tools/ # Helper and build scripts
```

---

## 📝 Development Roadmap
- [ ] **Phase 1**: Basic handshake between C# Plugin and .NET Client.
- [ ] **Phase 2**: Implementation of the Desktop Duplication API for snapshots.
- [ ] **Phase 3**: Heartbeat system and SignalR integration for web commands.
- [ ] **Phase 4**: Implementation of Peer-to-Peer consensus logic (Trust Mesh).
- [ ] **Phase 5**: Overwatch module (evidence gallery for judgment).

---

## ⚖️ License and Ethics
This project is strictly intended for use in private and competitive communities, aiming for competitive integrity.

AegisMesh collects system data for auditing purposes; its use implies the consent of the community players.

> **Note:** This project is in the technical brainstorming and prototyping phase.
