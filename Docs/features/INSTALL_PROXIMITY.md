# Configuração de Transferência por Proximidade

## ✅ Implementação Completa

Foi adicionado ao app iOS **POS_Sale_list** a funcionalidade de receber arquivos CSV de dispositivos próximos usando **Multipeer Connectivity**.

## 📱 Como Usar

### No App iOS (POS_Sale_list)

1. **Abrir a opção de receber:**
   - Toque no menu "..." no canto superior direito
   - Selecione **"Receber de Dispositivo Próximo"**
   - Ou, se não houver dados, toque no botão **"Receber"** com o ícone de ondas

2. **Aguardar conexão:**
   - O app vai começar a procurar dispositivos na mesma rede Wi-Fi
   - Uma tela aparecerá com "Dispositivos iOS por Perto" e status "A procurar..."

3. **Receber o arquivo:**
   - Quando o dispositivo Mac enviar o CSV, o app iOS vai:
     - Aceitar automaticamente a conexão
     - Mostrar progresso da transferência
     - Importar o CSV automaticamente quando completo
     - Fechar a tela e mostrar os dados

### No App Mac (Enviador)

O app Mac precisa implementar o lado do **enviador** usando o mesmo framework Multipeer Connectivity.

## 🔧 Configurações Necessárias

### Info.plist

Adicione as seguintes chaves ao arquivo `Info.plist` do projeto:

```xml
<key>NSLocalNetworkUsageDescription</key>
<string>Este app precisa acessar a rede local para receber arquivos CSV de outros dispositivos.</string>

<key>NSBonjourServices</key>
<array>
    <string>_pos-csv-share._tcp</string>
    <string>_pos-csv-share._udp</string>
</array>
```

**Como adicionar:**
1. No Xcode, selecione o arquivo `Info.plist`
2. Clique no botão "+" para adicionar nova linha
3. Digite "Privacy - Local Network Usage Description"
4. No valor, coloque: "Este app precisa acessar a rede local para receber arquivos CSV de outros dispositivos."
5. Adicione outra linha para "Bonjour services"
6. Adicione os serviços `_pos-csv-share._tcp` e `_pos-csv-share._udp`

## 🏗️ Arquivos Criados

1. **ProximityManager.swift**
   - Gerencia a descoberta de dispositivos
   - Controla a sessão Multipeer Connectivity
   - Recebe arquivos e notifica o progresso

2. **ProximityReceiverView.swift**
   - Interface visual para receber arquivos
   - Mostra estados: descobrindo, conectado, recebendo, completo
   - Barra de progresso durante transferência

3. **ContentView.swift** (atualizado)
   - Adicionado botão "Receber" no menu
   - Adicionado botão "Receber" no estado vazio
   - Integração com ProximityManager

## 🔐 Segurança

- Usa criptografia obrigatória (`.required`)
- Apenas dispositivos na mesma rede Wi-Fi local podem se conectar
- Aceita automaticamente convites (pode ser modificado para confirmação manual)

## 🎨 Design

A interface segue o design da imagem fornecida:
- Ícone de iPhone com ondas
- Título "Dispositivos iOS por Perto"
- Estado de "A procurar..." com loading spinner
- Mensagem "Certifica-te que a app iOS está aberta e no mesmo Wi-Fi"
- Botão "Cancelar" na parte inferior

## 📊 Estados da Transferência

1. **Idle** - Aguardando início
2. **Discovering** - Procurando dispositivos na rede
3. **Connected** - Conectado a um dispositivo
4. **Receiving** - Recebendo arquivo com barra de progresso
5. **Completed** - Arquivo recebido com sucesso
6. **Failed** - Erro durante o processo

## 🧪 Testando

Para testar a funcionalidade:

1. Certifique-se de que ambos os dispositivos (iOS e Mac) estão na mesma rede Wi-Fi
2. No app iOS, abra "Receber de Dispositivo Próximo"
3. No app Mac, implemente o lado do enviador (exemplo abaixo)
4. Envie o arquivo CSV do Mac
5. O iOS deve receber e importar automaticamente

## 📤 Exemplo de Código para o Enviador (Mac)

```swift
import MultipeerConnectivity

class ProximitySender: NSObject, ObservableObject {
    private let serviceType = "pos-csv-share"
    private var peerID: MCPeerID
    private var session: MCSession
    private var browser: MCNearbyServiceBrowser?
    
    override init() {
        self.peerID = MCPeerID(displayName: Host.current().localizedName ?? "Mac")
        self.session = MCSession(peer: peerID, securityIdentity: nil, encryptionPreference: .required)
        super.init()
        self.session.delegate = self
    }
    
    func startBrowsing() {
        browser = MCNearbyServiceBrowser(peer: peerID, serviceType: serviceType)
        browser?.delegate = self
        browser?.startBrowsingForPeers()
    }
    
    func sendFile(at url: URL, to peer: MCPeerID) {
        session.sendResource(at: url, withName: url.lastPathComponent, toPeer: peer) { error in
            if let error = error {
                print("Erro ao enviar: \(error)")
            } else {
                print("Arquivo enviado com sucesso!")
            }
        }
    }
}
```

## ⚠️ Limitações

- Funciona apenas na mesma rede Wi-Fi local
- Ambos os dispositivos precisam ter o app aberto
- Transferência é peer-to-peer (sem servidor intermediário)

## 🎯 Próximos Passos

1. ✅ Adicionar permissões no Info.plist
2. ⬜ Implementar o lado do enviador no app Mac
3. ⬜ Testar transferência entre dispositivos
4. ⬜ (Opcional) Adicionar confirmação manual de convites para maior segurança
