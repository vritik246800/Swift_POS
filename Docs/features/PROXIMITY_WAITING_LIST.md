# Sistema de Sinalização "Aguardar Lista"

## 📋 Visão Geral

O sistema foi atualizado para permitir que dispositivos iOS/iPadOS sinalizem quando estão prontos para receber listas de stock. A app macOS pode então filtrar e identificar facilmente quais dispositivos estão à espera de dados.

## 🔄 Fluxo de Funcionamento

### 1️⃣ Dispositivo iOS/iPadOS (Receptor)

```swift
// Iniciar anúncio indicando que está à espera de lista
let service = POSProximityService.shared
service.startAdvertising(
    deviceName: UIDevice.current.name,
    waitingForList: true  // 👈 Sinaliza que está pronto para receber
)

// Verificar estado
print(service.isWaitingForList)  // true

// Atualizar estado dinamicamente (sem parar o serviço)
service.updateWaitingForListState(false)  // Deixa de aguardar
service.updateWaitingForListState(true)   // Volta a aguardar
```

### 2️⃣ Dispositivo macOS (Emissor)

```swift
// Descobrir dispositivos
let service = POSProximityService.shared
service.startDiscovery()

// Ver todos os dispositivos
print(service.availableDevices)  
// [POSDevice(name: "iPhone de João", ...), POSDevice(name: "iPad da Maria", ...)]

// Filtrar apenas os que estão à espera de lista
let waiting = service.devicesWaitingForList
print(waiting.count)  // 2

// Verificar estado individual
for device in service.availableDevices {
    if device.isWaitingForList {
        print("\(device.name) está à espera de lista 📋")
        print("Status: \(device.statusDescription)")  // "A aguardar lista 📋"
    }
}

// Enviar apenas para quem está à espera
for device in service.devicesWaitingForList {
    service.sendStockData(jsonData, to: device) { success in
        print("Enviado para \(device.name): \(success)")
    }
}
```

## 🎯 Propriedades e Métodos Novos

### POSProximityService

```swift
// PROPRIEDADES PUBLICADAS
@Published var isWaitingForList: Bool  // Estado do dispositivo local

// MÉTODOS
func startAdvertising(deviceName: String, waitingForList: Bool = true)
func updateWaitingForListState(_ waiting: Bool)

// PROPRIEDADES COMPUTADAS
var devicesWaitingForList: [POSDevice]  // Filtro de dispositivos à espera
```

### POSDevice

```swift
// PROPRIEDADES
var isWaitingForList: Bool        // true se está à espera de lista
var statusDescription: String     // "A aguardar lista 📋", "Online", ou "Offline"

// EXEMPLO DE USO
let device = POSDevice(...)
if device.isWaitingForList {
    // Enviar dados
}
```

## 💡 Casos de Uso

### Caso 1: Inicialização Automática no iOS

```swift
// ContentView.swift (iOS)
struct ContentView: View {
    @StateObject private var proximity = POSProximityService.shared
    
    var body: some View {
        StockListView()
            .onAppear {
                // Ao abrir a app, sinaliza que está pronto
                proximity.startAdvertising(
                    deviceName: UIDevice.current.name,
                    waitingForList: true
                )
            }
            .onDisappear {
                proximity.stopAdvertising()
            }
    }
}
```

### Caso 2: Toggle Manual no iOS

```swift
// SettingsView.swift (iOS)
struct SettingsView: View {
    @StateObject private var proximity = POSProximityService.shared
    
    var body: some View {
        Toggle("Aguardar lista de stock", isOn: .init(
            get: { proximity.isWaitingForList },
            set: { proximity.updateWaitingForListState($0) }
        ))
    }
}
```

### Caso 3: Envio Inteligente no macOS

```swift
// StockSyncView.swift (macOS)
struct StockSyncView: View {
    @StateObject private var proximity = POSProximityService.shared
    @State private var autoSend = true
    
    var body: some View {
        VStack {
            // Mostra apenas dispositivos à espera
            List(proximity.devicesWaitingForList) { device in
                HStack {
                    Text(device.name)
                    Spacer()
                    Text("📋 A aguardar")
                        .foregroundColor(.orange)
                }
            }
            
            Button("Enviar para todos") {
                sendToAllWaiting()
            }
        }
        .onChange(of: proximity.devicesWaitingForList) { devices in
            // Auto-envio quando detecta dispositivos à espera
            if autoSend && !devices.isEmpty {
                sendToAllWaiting()
            }
        }
    }
    
    func sendToAllWaiting() {
        for device in proximity.devicesWaitingForList {
            // Exportar e enviar
            if let data = exportStockData() {
                proximity.sendStockData(data, to: device) { success in
                    print("\(device.name): \(success ? "✅" : "❌")")
                }
            }
        }
    }
    
    func exportStockData() -> Data? {
        // Lógica de exportação
        return nil
    }
}
```

### Caso 4: Notificação ao Receber

```swift
// iOS - Após receber lista
NotificationCenter.default.addObserver(
    forName: .posStockDataReceived,
    object: nil,
    queue: .main
) { notification in
    // Dados recebidos, desativa o modo de espera
    POSProximityService.shared.updateWaitingForListState(false)
    
    // Mostra alerta
    showAlert("Lista de stock recebida!")
}
```

## 🧪 Exemplos de Interface

### iOS - Indicador Visual

```swift
struct WaitingIndicator: View {
    @ObservedObject var service: POSProximityService
    
    var body: some View {
        HStack {
            Circle()
                .fill(service.isWaitingForList ? Color.orange : Color.gray)
                .frame(width: 10, height: 10)
            
            Text(service.isWaitingForList 
                ? "A aguardar lista de stock..."
                : "Modo de espera desativado")
                .font(.caption)
        }
    }
}
```

### macOS - Lista de Dispositivos

```swift
struct DeviceList: View {
    @ObservedObject var service: POSProximityService
    
    var body: some View {
        VStack(alignment: .leading) {
            Text("Dispositivos à espera: \(service.devicesWaitingForList.count)")
                .font(.headline)
            
            ForEach(service.availableDevices) { device in
                HStack {
                    Image(systemName: device.isWaitingForList 
                        ? "bell.badge.fill" 
                        : "checkmark.circle")
                        .foregroundColor(device.isWaitingForList 
                        ? .orange 
                        : .green)
                    
                    Text(device.name)
                    Spacer()
                    Text(device.statusDescription)
                        .font(.caption)
                }
            }
        }
    }
}
```

## 📊 Metadata TXT Record

O serviço Bonjour agora inclui:

```
device: "iPhone de João"
platform: "iOS"
version: "1.0"
ready: "true"
waitingForList: "true"  // 👈 NOVO CAMPO
```

## ⚙️ Comportamento

1. **Ao iniciar anúncio**: 
   - `isWaitingForList` é definido pelo parâmetro `waitingForList`
   - Por defeito é `true`

2. **Ao atualizar estado**:
   - `updateWaitingForListState()` para e reinicia o serviço
   - Preserva o nome do dispositivo
   - Atualiza o TXT record no Bonjour

3. **Ao receber dados**:
   - O app pode optar por desativar automaticamente
   - Ou manter ativo para receber múltiplas listas

4. **Na descoberta**:
   - macOS detecta o campo `waitingForList` no metadata
   - Pode filtrar usando `devicesWaitingForList`
   - UI pode destacar dispositivos à espera

## 🎨 Recomendações de UI

### iOS/iPadOS
- ✅ Mostrar badge ou indicator quando está à espera
- ✅ Permitir toggle manual do estado
- ✅ Desativar automaticamente após receber dados
- ✅ Mostrar notificação quando recebe lista

### macOS
- ✅ Destacar dispositivos à espera com cor diferente (laranja)
- ✅ Mostrar contador de dispositivos à espera
- ✅ Filtro para mostrar apenas dispositivos à espera
- ✅ Envio em lote para todos os que aguardam

## 🔍 Debug

```swift
// Verificar estado do serviço
print("Advertising: \(service.isAdvertising)")
print("Waiting: \(service.isWaitingForList)")
print("Devices found: \(service.availableDevices.count)")
print("Devices waiting: \(service.devicesWaitingForList.count)")

// Listar dispositivos
for device in service.availableDevices {
    print("📱 \(device.name)")
    print("   Platform: \(device.platform)")
    print("   Ready: \(device.isReady)")
    print("   Waiting: \(device.isWaitingForList)")
    print("   Status: \(device.statusDescription)")
}
```

## ✨ Melhorias Futuras

- [ ] Timeout automático (ex: parar de aguardar após 5 minutos)
- [ ] Histórico de sincronizações
- [ ] Confirmação de recepção (ACK)
- [ ] Queue de envios pendentes
- [ ] Retry automático em caso de falha
