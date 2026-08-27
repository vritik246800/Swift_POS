# POS Stock Proximity Sharing

## Visão Geral

Sistema de partilha directa de dados de stock baixo entre aplicações macOS/iPadOS (desktop) e iOS (dispositivo móvel) através da rede local, usando **Bonjour** para descoberta e **Network.framework** para transferência peer-to-peer.

---

## Funcionalidades Implementadas

### ✅ Desktop (Mac/iPad)

1. **Exportação de Stock Baixo**
   - Exporta produtos com stock ≤ 10
   - Formatos: `.posstock` (CSV customizado) e `.posstock.json` (JSON estruturado)
   - Inclui: barcode, nome, stock actual, quantidade a encomendar, preço base

2. **Descoberta de Dispositivos iOS**
   - Detecta automaticamente apps iOS prontas na mesma rede
   - Interface visual com lista de dispositivos disponíveis
   - Estado em tempo real (Online/Pronto)

3. **Envio Directo**
   - Transferência peer-to-peer via TCP
   - Protocolo customizado com header de tamanho + payload JSON
   - Feedback visual durante envio
   - Confirmação de sucesso/falha

### ✅ iOS (iPhone/iPad Companion)

1. **Anúncio de Presença**
   - Anuncia via Bonjour (`_posapp._tcp`) ao abrir a app
   - TXT record com metadata (nome do dispositivo, plataforma, estado)
   - Indicador visual de estado online

2. **Recepção Automática**
   - Escuta ligações TCP na porta dinâmica
   - Processa JSON recebido automaticamente
   - Feedback háptico na recepção
   - Actualização imediata da UI

3. **Visualização de Dados**
   - Lista de produtos com stock baixo
   - Código de barras, nome, stock, quantidade a encomendar
   - Filtro de pesquisa
   - Cards de resumo (total produtos, total a encomendar)

4. **Exportação Local**
   - Partilha via ShareLink (AirDrop, email, etc.)
   - Cópia para clipboard
   - Formato CSV compatível com Excel

---

## Configuração do Projeto

### Requisitos

- **macOS 14+** (para Network.framework peer-to-peer)
- **iOS 16+** (para Network.framework e Bonjour)
- Targets separados no Xcode:
  - `POSApp` (macOS/iPadOS)
  - `POSStockReceiver` (iOS)

### Passo 1: Configurar Info.plist

#### Desktop (macOS/iPadOS)

Adiciona ao `Info.plist`:

```xml
<key>NSLocalNetworkUsageDescription</key>
<string>A app precisa de acesso à rede local para detectar e enviar dados de stock para dispositivos iOS.</string>

<key>NSBonjourServices</key>
<array>
    <string>_posapp._tcp</string>
</array>
```

#### iOS Companion

Adiciona ao `Info.plist`:

```xml
<key>NSLocalNetworkUsageDescription</key>
<string>A app precisa de acesso à rede local para receber dados de stock do Mac ou iPad.</string>

<key>NSBonjourServices</key>
<array>
    <string>_posapp._tcp</string>
</array>

<key>UIBackgroundModes</key>
<array>
    <string>processing</string>
</array>
```

### Passo 2: Configurar Capabilities

#### Desktop
1. Xcode → Target POSApp → Signing & Capabilities
2. Adiciona **"Network"** capability (se disponível)
3. Em "Hardened Runtime", activa:
   - ☑️ Outgoing Connections (Client)
   - ☑️ Incoming Connections (Server)

#### iOS
1. Xcode → Target POSStockReceiver → Signing & Capabilities
2. Adiciona **"Background Modes"**
3. Activa: ☑️ Background fetch

### Passo 3: Adicionar Ficheiros ao Projeto

Adiciona estes ficheiros aos respectivos targets:

**Desktop Target:**
- `LowStockExportService.swift`
- `POSProximityService.swift`
- `LowStockView.swift` (já existente, actualizado)
- `Posguideview.swift` (actualizado)

**iOS Target:**
- `POSStockReceiverApp.swift`
- `POSProximityService.swift` (partilhado)

### Passo 4: Registar Tipo de Ficheiro Customizado

No `Info.plist` do **Desktop**, adiciona:

```xml
<key>UTExportedTypeDeclarations</key>
<array>
    <dict>
        <key>UTTypeConformsTo</key>
        <array>
            <string>public.data</string>
            <string>public.content</string>
        </array>
        <key>UTTypeDescription</key>
        <string>POS Stock Export</string>
        <key>UTTypeIconFiles</key>
        <array/>
        <key>UTTypeIdentifier</key>
        <string>com.posapp.stock-export</string>
        <key>UTTypeTagSpecification</key>
        <dict>
            <key>public.filename-extension</key>
            <array>
                <string>posstock</string>
            </array>
            <key>public.mime-type</key>
            <array>
                <string>application/x-posstock</string>
            </array>
        </dict>
    </dict>
</array>
```

---

## Como Usar

### Desktop (macOS/iPad)

1. Vai a **Produtos** → **Stock Baixo**
2. Selecciona produtos (ou deixa todos)
3. Opções de partilha:
   - **"Partilhar lista"**: AirDrop, email, ficheiros (tradicional)
   - **"Enviar para iOS"**: Transferência directa via rede local

#### Envio Directo:
1. Clica em **"Enviar para iOS"**
2. Aguarda detecção de dispositivos (1-3 segundos)
3. Selecciona o dispositivo iOS da lista
4. Confirmação automática após envio

### iOS (iPhone/iPad)

1. Abre a app **POS Stock Receiver**
2. Verifica que o indicador está **verde (Online)**
3. Aguarda recepção de dados
4. Quando chegar:
   - Vibração de confirmação
   - Lista aparece automaticamente
5. Para exportar:
   - Toca em **"Exportar Lista de Encomenda"**
   - Escolhe destino (AirDrop, email, clipboard, etc.)

---

## Arquitetura Técnica

### Descoberta (Bonjour)

```swift
// iOS: Anuncia serviço
let params = NWParameters.tcp
params.serviceRegistration = .service(
    name: deviceName,
    type: "_posapp._tcp",
    domain: "local",
    txtRecord: ["platform": "iOS", "ready": "true"]
)

// Desktop: Descobre serviços
let browser = NWBrowser(
    for: .bonjour(type: "_posapp._tcp", domain: "local"),
    using: params
)
```

### Transferência de Dados

Protocolo customizado:
1. **Header**: 4 bytes (UInt32 big-endian) com tamanho do payload
2. **Payload**: JSON estruturado

```json
{
  "version": "1.0",
  "exportDate": "2026-04-13T10:30:00Z",
  "source": "POS Desktop",
  "products": [
    {
      "id": 42,
      "barcode": "1234567890123",
      "name": "Produto X",
      "stock": 2,
      "orderQty": 10,
      "priceBase": 150.00,
      "ivaRate": 16.0,
      "profitMargin": 25.0
    }
  ]
}
```

### Fluxo de Comunicação

```
┌─────────────────┐                    ┌─────────────────┐
│   iOS Device    │                    │  macOS/iPadOS   │
│  (Receiver)     │                    │   (Sender)      │
└────────┬────────┘                    └────────┬────────┘
         │                                      │
         │ 1. startAdvertising()                │
         ├─────────────────────────────────────>│
         │    (Bonjour: _posapp._tcp)           │
         │                                      │
         │              2. startDiscovery()     │
         │<─────────────────────────────────────┤
         │                                      │
         │ 3. Browse Results                    │
         ├─────────────────────────────────────>│
         │    (Device list with metadata)       │
         │                                      │
         │              4. User selects device  │
         │              5. NWConnection.init()  │
         │<─────────────────────────────────────┤
         │                                      │
         │ 6. Connection established            │
         │<────────────────────────────────────>│
         │                                      │
         │              7. Send size (4 bytes)  │
         │<─────────────────────────────────────┤
         │                                      │
         │              8. Send JSON payload    │
         │<─────────────────────────────────────┤
         │                                      │
         │ 9. Process & notify UI               │
         ├─────────────────────────────────────>│
         │                                      │
         │ 10. Haptic feedback                  │
         │ 11. Update product list              │
         │                                      │
         │              12. Connection closed   │
         │<────────────────────────────────────>│
         │                                      │
```

---

## Resolução de Problemas

### Dispositivo iOS não aparece na lista

**Causas possíveis:**
- Dispositivos em redes Wi-Fi diferentes
- App iOS não está aberta ou em background
- Permissões de rede local negadas

**Soluções:**
1. Verifica que ambos estão na **mesma rede Wi-Fi**
2. Abre a app iOS e confirma indicador verde
3. iOS: Definições → Privacidade → Rede Local → activa para a app
4. Reinicia a descoberta no desktop

### Envio falha constantemente

**Causas possíveis:**
- Firewall bloqueando conexões
- App iOS foi para background durante envio
- Problema temporário de rede

**Soluções:**
1. Mantém a app iOS em foreground durante envio
2. macOS: Preferências do Sistema → Rede → Firewall → permite a app
3. Reinicia ambas as apps
4. Usa cable/AirDrop como alternativa

### iOS não vibra ao receber

- Modo silencioso activado
- Feedback háptico desactivado nas definições
- Dispositivo não suporta Taptic Engine

Solução: Os dados são recebidos mesmo sem vibração — verifica a lista.

### JSON corrompido ou erro de parsing

- Transferência interrompida
- Versão incompatível entre apps

Solução: Actualiza ambas as apps para a mesma versão.

---

## Extensões Futuras

### 🔮 Possíveis Melhorias

1. **Autenticação**
   - Token de segurança partilhado
   - Pairing inicial via QR Code

2. **Compressão**
   - GZIP para payloads grandes (>100KB)
   - Delta encoding para actualizações incrementais

3. **Sincronização Bidirecional**
   - iOS envia encomendas confirmadas de volta
   - Desktop actualiza stock automaticamente

4. **Histórico de Transferências**
   - Log de envios/recepções
   - Retry automático em caso de falha

5. **Suporte para Multiple Recipients**
   - Enviar para vários dispositivos simultaneamente
   - Broadcast na rede local

6. **Background Transfer (iOS)**
   - Usar `URLSession` para downloads em background
   - Push notification quando recebe dados

---

## Licença e Créditos

Este código é parte do sistema **Sales POS** e usa:
- **Network.framework** (Apple)
- **Bonjour/mDNS** (Apple)
- **SwiftUI** (Apple)

© 2026 - Implementado para partilha de dados de inventário em redes locais.
