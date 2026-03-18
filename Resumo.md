
# 🛡️ Hub de Mídia Seguro e Distribuição de Arquivos com Verificação de Integridade

Este projeto consiste em uma arquitetura **Cliente-Servidor** robusta, desenvolvida para o compartilhamento de arquivos e streaming de vídeo (VOD) com foco em segurança criptográfica e integridade de dados.

## 🏗️ Arquitetura do Sistema

O sistema é dividido em três camadas principais:

### 1. Processamento e Preparação (`batch-processor.js`)

* **Hashing SHA-256:** Varre o diretório `/files` e gera uma "assinatura digital" única para cada arquivo, armazenando-as no `integrity_map.json`.
* **Segmentação HLS (HTTP Live Streaming):** Utiliza o `FFmpeg` para converter vídeos `.mp4` em pequenos segmentos `.ts` e uma playlist `.m3u8`, permitindo streaming adaptativo e rápido.

### 2. Camada de Servidor (`server.js`)

* **Protocolo HTTPS/TLS:** Implementa segurança na camada de transporte usando certificados SSL/TLS (`key.pem` e `cert.pem`), garantindo que o tráfego seja cifrado.
* **Middleware de Segurança:** Configurado com headers `HSTS` (Strict-Transport-Security) e `X-Content-Type-Options: nosniff` para mitigar ataques de interceptação.
* **Interface LAN/WAN:** Configurado para escutar em `0.0.0.0`, permitindo acesso via rede local (IP Privado) ou túneis externos.

### 3. Interface do Cliente (`public/`)

* **Frontend Responsivo:** Interface em HTML5/CSS3 para navegação em dispositivos móveis e desktops.
* **Validação de Integridade Local:** O `script.js` realiza o download do arquivo e, via Web Crypto API, recalcula o hash SHA-256 no dispositivo do cliente, comparando-o com o mapa de integridade para garantir que o arquivo não foi alterado.

---

## 🚀 Funcionalidades Principais

* **Streaming de Vídeo:** Player integrado com a biblioteca `hls.js`.
* **Download Verificado:** Sistema de checagem de erros/alterações pós-download.
* **Acesso Multiplataforma:** Compatível com qualquer navegador moderno na mesma rede (LAN).
* **Resiliência a Firewall:** Estrutura preparada para rodar em portas alternativas (ex: 8443, 5500) para contornar bloqueios de sistema.

---

## 🛠️ Tecnologias Utilizadas

* **Runtime:** Node.js v23+
* **Framework Web:** Express.js
* **Segurança:** OpenSSL (Certificados), Web Crypto API (Client-side Hashing)
* **Processamento de Vídeo:** FFmpeg
* **Protocolos:** TCP/IP, HTTPS, HLS

---

## 📖 Como Executar

1. **Instalar dependências:** `npm install express`
2. **Preparar arquivos:** `node batch-processor.js`
3. **Iniciar Servidor:** `node server.js` (Executar como Administrador para porta 443)
4. **Acesso Local:** `https://localhost`
5. **Acesso na Rede:** `https://192.168.1.108` (ou seu IP atual)

---

### Notas de Redes de Computadores

> Este projeto demonstra a aplicação prática do modelo OSI, focando especialmente na **Camada de Transporte (4)** com o uso de sockets TCP seguros e na **Camada de Aplicação (7)** com os protocolos HTTP e HLS.

---

