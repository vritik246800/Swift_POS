# 📱 Guia Visual - Transferência por Proximidade

## Interface do App iOS

### 1️⃣ Estado Vazio (Sem Dados)

```
┌─────────────────────────────────────┐
│  Stock Manager              ⋮      │
├─────────────────────────────────────┤
│                                     │
│          🔍                          │
│     (ícone grande)                  │
│                                     │
│   Nenhum CSV importado              │
│                                     │
│   Importa um ficheiro CSV           │
│        para começar                 │
│                                     │
│  ┌──────────────┐  ┌─────────────┐ │
│  │📥 Importar CSV│  │📡 Receber   │ │
│  │   (azul)      │  │ (roxo/rosa) │ │
│  └──────────────┘  └─────────────┘ │
│                                     │
└─────────────────────────────────────┘
```

### 2️⃣ Menu de Opções (Com Dados)

```
┌─────────────────────────────────────┐
│  Stock Manager              ⋮      │◄── Tocar aqui
├─────────────────────────────────────┤
│                    ┌──────────────────────────────┐
│                    │ 📥 Importar CSV do Sistema   │
│                    │ 📡 Receber de Dispositivo    │
│                    │    Próximo                   │
│                    ├──────────────────────────────┤
│                    │ 📤 Exportar Todos            │
│                    │ 🚩 Exportar Red Flags (5)    │
│                    │ ✅ Exportar Confirmados (12) │
│                    └──────────────────────────────┘
```

### 3️⃣ Tela de Descoberta (Procurando Dispositivos)

```
┌─────────────────────────────────────┐
│ ← Dispositivos iOS por Perto       │
├─────────────────────────────────────┤
│                                     │
│           ⭕                         │
│          (círculo roxo claro)       │
│           📱📡                       │
│    (ícone iPhone + ondas)           │
│                                     │
│  Dispositivos iOS por Perto         │
│                                     │
│  ┌───────────────────────────────┐  │
│  │                               │  │
│  │         ⌛ Loading...         │  │
│  │                               │  │
│  │  A procurar dispositivos iOS  │  │
│  │     na rede local...          │  │
│  │                               │  │
│  │  Certifica-te que a app iOS   │  │
│  │  está aberta e no mesmo Wi-Fi │  │
│  │                               │  │
│  └───────────────────────────────┘  │
│                                     │
│                                     │
│                                     │
│           ┌─────────────┐           │
│           │  Cancelar   │           │
│           └─────────────┘           │
│                                     │
└─────────────────────────────────────┘
```

### 4️⃣ Conectado (Aguardando Transferência)

```
┌─────────────────────────────────────┐
│ ← Dispositivos iOS por Perto       │
├─────────────────────────────────────┤
│                                     │
│  ┌───────────────────────────────┐  │
│  │                               │  │
│  │           ✅                   │  │
│  │      (verde, grande)          │  │
│  │                               │  │
│  │        Conectado              │  │
│  │                               │  │
│  │  Aguardando transferência...  │  │
│  │                               │  │
│  └───────────────────────────────┘  │
│                                     │
│           ┌─────────────┐           │
│           │  Cancelar   │           │
│           └─────────────┘           │
│                                     │
└─────────────────────────────────────┘
```

### 5️⃣ Recebendo Arquivo (Com Progresso)

```
┌─────────────────────────────────────┐
│ ← Dispositivos iOS por Perto       │
├─────────────────────────────────────┤
│                                     │
│  ┌───────────────────────────────┐  │
│  │                               │  │
│  │   ▓▓▓▓▓▓▓▓▓▓░░░░░░░░          │  │
│  │   (barra de progresso roxa)   │  │
│  │                               │  │
│  │     Recebendo arquivo...      │  │
│  │                               │  │
│  │            67%                │  │
│  │                               │  │
│  └───────────────────────────────┘  │
│                                     │
│           ┌─────────────┐           │
│           │  Cancelar   │           │
│           └─────────────┘           │
│                                     │
└─────────────────────────────────────┘
```

### 6️⃣ Arquivo Recebido (Sucesso)

```
┌─────────────────────────────────────┐
│ ← Dispositivos iOS por Perto       │
├─────────────────────────────────────┤
│                                     │
│  ┌───────────────────────────────┐  │
│  │                               │  │
│  │           ✅                   │  │
│  │    (verde, extra grande,      │  │
│  │      com animação bounce)     │  │
│  │                               │  │
│  │    Arquivo Recebido!          │  │
│  │                               │  │
│  │    Importando CSV...          │  │
│  │                               │  │
│  └───────────────────────────────┘  │
│                                     │
│     (fecha automaticamente em 1.5s) │
│                                     │
└─────────────────────────────────────┘
```

### 7️⃣ Erro (Se Houver Problema)

```
┌─────────────────────────────────────┐
│ ← Dispositivos iOS por Perto       │
├─────────────────────────────────────┤
│                                     │
│  ┌───────────────────────────────┐  │
│  │                               │  │
│  │           ⚠️                   │  │
│  │      (laranja, grande)        │  │
│  │                               │  │
│  │           Erro                │  │
│  │                               │  │
│  │   A conexão foi perdida       │  │
│  │                               │  │
│  └───────────────────────────────┘  │
│                                     │
│           ┌─────────────┐           │
│           │  Cancelar   │           │
│           └─────────────┘           │
│                                     │
└─────────────────────────────────────┘
```

## 🎨 Cores e Estilos

### Cores Principais
- **Roxo/Rosa Gradient**: `LinearGradient(colors: [.purple, .pink])`
- **Azul Accent**: `Color.accentColor`
- **Verde Sucesso**: `Color.green`
- **Vermelho Erro**: `Color.red`
- **Laranja Warning**: `Color.orange`

### Ícones SF Symbols
- 📡 `iphone.gen3.radiowaves.left.and.right`
- 📥 `square.and.arrow.down`
- 📤 `square.and.arrow.up`
- ✅ `checkmark.circle.fill`
- ⚠️ `exclamationmark.triangle.fill`
- 🔍 `doc.text.magnifyingglass`

## 🔄 Fluxo de Uso

```
Início
  │
  ├─→ Usuário toca em "Receber" ou menu "..."
  │
  ├─→ Abre ProximityReceiverView
  │
  ├─→ Estado: DISCOVERING (procurando...)
  │
  ├─→ Mac envia convite
  │
  ├─→ Estado: CONNECTED (conectado)
  │
  ├─→ Mac envia arquivo CSV
  │
  ├─→ Estado: RECEIVING (recebendo com %)
  │
  ├─→ Arquivo recebido completamente
  │
  ├─→ Estado: COMPLETED (sucesso ✅)
  │
  ├─→ Chama vm.importCSV(from: url)
  │
  ├─→ Aguarda 1.5 segundos
  │
  └─→ Fecha tela e mostra dados importados
```

## 📋 Checklist de Implementação

- ✅ ProximityManager.swift criado
- ✅ ProximityReceiverView.swift criado
- ✅ ContentView.swift atualizado
- ✅ Menu com opção "Receber de Dispositivo Próximo"
- ✅ Botão "Receber" no estado vazio
- ✅ Estados visuais (discovering, receiving, completed)
- ✅ Barra de progresso durante transferência
- ✅ Importação automática após recebimento
- ⬜ Adicionar permissões no Info.plist
- ⬜ Implementar enviador no app Mac
- ⬜ Testar transferência real

## 🎯 Resultado Final

Quando tudo estiver configurado:

1. Usuário abre o app iOS
2. Toca em "Receber de Dispositivo Próximo"
3. App mostra "A procurar dispositivos iOS na rede local..."
4. No Mac, usuário clica em "Enviar para iOS"
5. Mac descobre o iPhone e envia o CSV
6. iPhone aceita automaticamente
7. Mostra progresso da transferência (0% → 100%)
8. Quando completo, importa o CSV automaticamente
9. Fecha a tela e mostra os produtos na lista

**Tudo pronto! 🚀**
