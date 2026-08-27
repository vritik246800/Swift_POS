# Visão Geral do Projeto — Sales POS (Documentação Completa)

---

## 1. Visão Geral do Projeto

**Nome:** POS App (Sales POS)
**Plataformas:** macOS + iOS (SwiftUI universal)
**Base de Dados:** SQLite3 nativo (sem bibliotecas externas)
**Linguagem da UI:** Português (PT)
**Moeda:** MT (Metical Moçambicano) nas vendas, € nos relatórios/faturas
**Versão:** 1.1.0

O Sales POS é um sistema de ponto de venda completo que permite:
- Gerir produtos com preço base, margem de lucro e IVA automáticos
- Processar vendas com carrinho, dados de cliente e múltiplos métodos de pagamento
- Gerar faturas/recibos em PDF
- Fecho de caixa diário e mensal com exportação (CSV/PDF)
- Relatórios diários e mensais com pesquisa e exportação
- Gestão de utilizadores com dois perfis (Admin / Caixa)
- Scanner de códigos de barras (câmara nativa + Continuity Camera no Mac)
- Sistema de subscrição mensal via StoreKit 2 com trial de 15 dias

---

## 2. Estrutura de Pastas e Ficheiros

```
Sales_Project/
├── Database/
│   └── DatabaseManager.swift          ← Singleton SQLite3 (todas as operações CRUD)
├── Models/
│   ├── Product.swift                  ← Produto (id, nome, barcode, preços, stock)
│   ├── Sale.swift                     ← Venda (id, userId, cliente, total, data, status)
│   ├── SaleItem.swift                 ← Item de venda (produto, quantidade, subtotal)
│   ├── Payment.swift                  ← Pagamento (método, valor, referência)
│   ├── User.swift                     ← Utilizador (nome, username, hash, role)
│   ├── DayClose.swift                 ← Fecho de caixa (totais por método, notas)
│   └── Report.swift                   ← Relatório guardado (tipo, período, caminho)
├── Utils/
│   └── Constants.swift                ← Constantes globais (IVA, nome app, nome BD)
├── ViewModels/
│   ├── AuthViewModel.swift            ← Login/Logout, hash SHA256, gestão de sessão
│   ├── ProductViewModel.swift         ← CRUD produtos, pesquisa, stock baixo
│   └── SaleViewModel.swift            ← Carrinho, finalizar venda, histórico
├── Views/
│   ├── POSAppApp.swift                ← @main — Entry point real da app
│   ├── LoginView.swift                ← Ecrã de login
│   ├── MainView.swift                 ← Layout principal (sidebar macOS / tabs iOS)
│   ├── Posguideview.swift             ← Guia de utilizador integrado (8 capítulos)
│   ├── Sales/
│   │   ├── SaleView.swift             ← Ecrã de vendas (catálogo + carrinho)
│   │   ├── PaymentView.swift          ← Modal de pagamento (5 métodos, pagamento misto)
│   │   └── InvoiceView.swift          ← Fatura/Recibo após venda concluída
│   ├── Products/
│   │   ├── ProductListView.swift      ← Lista de produtos com pesquisa e stock
│   │   ├── ProductFormView.swift      ← Formulário criar/editar produto
│   │   └── BarcodeScannerView.swift   ← Scanner de códigos de barras (iOS + macOS)
│   ├── DayClose/
│   │   └── DayCloseView.swift         ← Fecho diário, mensal, histórico, exportação
│   ├── Reports/
│   │   ├── DailyReportView.swift      ← Relatório diário com métricas e lista
│   │   ├── MonthlyReportView.swift    ← Relatório mensal com métricas e lista
│   │   ├── ReportHistoryView.swift    ← Histórico de relatórios exportados
│   │   ├── ReportComponents.swift     ← Componentes reutilizáveis dos relatórios
│   │   ├── SaleReportRowView.swift    ← Linha expansível de venda nos relatórios
│   │   ├── ReportViewModel.swift      ← ViewModel dos relatórios
│   │   ├── ReportService.swift        ← Geração de CSV e PDF (CoreGraphics)
│   │   └── CloseExportService.swift   ← Exportação específica de fechos (CSV/PDF)
│   ├── Settings/
│   │   ├── SettingsView.swift         ← Definições (sessão, subscrição, utilizadores, app)
│   │   └── UserFormView.swift         ← Formulário criar/editar utilizador
│   └── Subscription/
│       ├── SubscriptionManager.swift  ← Gestão StoreKit 2 (compra, estado, listener)
│       ├── TrialManager.swift         ← Gestão do trial de 15 dias (UserDefaults)
│       ├── PaywallView.swift          ← Ecrã de subscrição (paywall)
│       └── CancellationReason.swift   ← Feedback de cancelamento + razões
├── Sales_Project/
│   ├── Sales_ProjectApp.swift         ← Entry point original (desativado, @main comentado)
│   ├── ContentView.swift              ← View placeholder (não usada)
│   └── Assets.xcassets/               ← Assets da app
└── Sales_Project.xcodeproj/           ← Projeto Xcode
```

---

## 3. Entry Point e Fluxo de Arranque

**Ficheiro:** `Views/POSAppApp.swift` (marcado com `@main`)

### Fluxo de arranque:
1. `POSAppApp` cria dois `@StateObject`: `AuthViewModel` e `SubscriptionManager`
2. `TrialManager.shared.registerFirstLaunchIfNeeded()` regista a data do primeiro lançamento
3. **Gate de acesso:**
   - Se `!subscriptionManager.hasAccess` → mostra `PaywallView`
   - Se `authViewModel.isLoggedIn` → mostra `MainView`
   - Senão → mostra `LoginView`
4. Quando a app vai para background → `saveEndOfDayReport()` gera CSV + PDF do dia
5. Quando a app volta ao primeiro plano → verifica estado da subscrição

**Nota:** `Sales_ProjectApp.swift` tem `@main` comentado e não é o entry point ativo. Cria um user admin default na init.

---

## 4. Base de Dados (SQLite3)

**Ficheiro:** `Database/DatabaseManager.swift`
**Padrão:** Singleton (`DatabaseManager.shared`)
**Localização BD:** `ApplicationSupport/posapp.sqlite`

### Tabelas:

| Tabela | Colunas | Descrição |
|--------|---------|-----------|
| **Users** | id, name, username, password_hash, role | Utilizadores (admin/cashier) |
| **Products** | id, name, barcode, price_base, iva_rate, profit_margin, price_final, stock | Catálogo de produtos |
| **Sales** | id, user_id, client_name, client_nif, total, date, status | Vendas registadas |
| **SaleItems** | id, sale_id, product_id, product_name, quantity, unit_price, subtotal | Itens de cada venda |
| **Payments** | id, sale_id, method, amount, reference | Pagamentos por venda |
| **DayCloses** | id, date, total_sales, total_cash, total_card, total_bank_transfer, total_mpesa, total_emola, num_sales, notes, closed_by, closed_at | Fechos de caixa |
| **Reports** | id, type, period, file_path, created_at | Metadados de relatórios exportados |

### Migrações:
- `migrateAddBarcode()` — Adiciona coluna `barcode` à tabela Products se não existir + índice único
- `migrateAddPaymentsTable()` — Cria tabela Payments se não existir
- `migrateAddDayClosesTable()` — Cria tabela DayCloses se não existir

### Operações disponíveis:
- **Users:** createUser, fetchUsers, fetchUserByUsername, updateUser, deleteUser
- **Products:** createProduct, fetchProducts, searchProducts, fetchProductByBarcode, updateProduct, updateStock, deleteProduct
- **Sales:** createSale (cria venda + items + desconta stock), fetchSales, fetchSaleItems, fetchSalesByDate, fetchSalesByMonth
- **Payments:** createPayments, fetchPayments, fetchPaymentsByDate
- **DayCloses:** saveDayClose (INSERT OR REPLACE), fetchDayClose, fetchDayCloses, isDayAlreadyClosed
- **Reports:** saveReport, fetchReports

---

## 5. Modelos de Dados

### Product (`Models/Product.swift`)
```
id, name, barcode, priceBase, ivaRate, profitMargin, priceFinal, stock
```
- Preço final calculado: `base × (1 + margem/100) × (1 + IVA/100)`
- Método estático `calculateFinalPrice(base:profit:iva:)`

### Sale (`Models/Sale.swift`)
```
id, userId, clientName, clientNIF, items: [SaleItem], total, date, status
```
- Status: `completed` | `cancelled` (enum `SaleStatus`)

### SaleItem (`Models/SaleItem.swift`)
```
id, saleId, productId, productName, quantity, unitPrice, subtotal
```

### Payment (`Models/Payment.swift`)
```
id, saleId, method, amount, reference
```
- Métodos: `cash`, `card`, `bank_transfer`, `mpesa`, `emola` (enum `PaymentMethod`)
- M-Pesa e e-Mola são `isMobile` e exigem referência obrigatória
- Cada método tem `label` (PT) e `icon` (SF Symbol)

### User (`Models/User.swift`)
```
id, name, username, passwordHash, role
```
- Roles: `admin` | `cashier` (enum `UserRole`)

### DayClose (`Models/DayClose.swift`)
```
id, date, totalSales, totalCash, totalCard, totalBankTransfer, totalMpesa, totalEmola, numSales, notes, closedBy, closedAt
```
- Propriedade computada `grandTotal` = soma de todos os métodos

### Report (`Models/Report.swift`)
```
id, type, period, filePath, createdAt
```
- Tipos: `daily` | `monthly` (enum `ReportType`)

---

## 6. ViewModels

### AuthViewModel (`ViewModels/AuthViewModel.swift`)
- **Estado:** `currentUser`, `isLoggedIn`, `errorMessage`
- **Login:** Busca user por username → compara hash SHA256
- **Hash:** `CryptoKit.SHA256` → hex string
- **Propriedades:** `isAdmin`, `users`, `userCount`

### ProductViewModel (`ViewModels/ProductViewModel.swift`)
- **Estado:** `products`, `searchResults`, `searchQuery`, `errorMessage`
- **Propriedade:** `lowStockProducts` (stock < 5)
- **Operações:** loadProducts, search, createProduct, updateProduct, deleteProduct, findByBarcode

### SaleViewModel (`ViewModels/SaleViewModel.swift`)
- **Estado:** `cartItems`, `clientName`, `clientNIF`, `errorMessage`, `lastSaleId`, `salesHistory`
- **Propriedade:** `cartTotal`
- **Carrinho:** addToCart (verifica stock, soma quantidades se duplicado), removeFromCart, clearCart
- **Finalizar:** `finalizeSaleWithPayments(userId:payments:)` — cria venda + guarda pagamentos
- **Histórico:** loadSalesHistory, salesForDay, salesForMonth, totalFor

---

## 7. Views — Descrição Detalhada

### 7.1 LoginView (`Views/LoginView.swift`)
- Ecrã de login com campos username e password
- Validação: ambos campos obrigatórios
- Mostrar/ocultar password
- Mensagem de erro inline
- Atalho: Enter para submeter
- Adaptação macOS/iOS (`nsColor` vs `uiColor`)

### 7.2 MainView (`Views/MainView.swift`)
- **macOS:** `NavigationSplitView` com sidebar (Vendas, Produtos, Relatórios, Fecho, Definições)
- **iOS:** `TabView` com as mesmas tabs
- Definições só visíveis para admin
- Botão "Guia" na sidebar (macOS) ou floating button (iOS)
- Alerta automático de "Fecho de Caixa Pendente" se há vendas sem fecho
- Enum `AppTab`: sales, products, reports, dayClose, settings

### 7.3 SaleView (`Views/Sales/SaleView.swift`)
- Layout split: catálogo à esquerda, carrinho à direita (340pt)
- **Catálogo:** Lista filtrada por nome/barcode, scanner de código, contador de resultados
- **Carrinho:** Campos cliente (nome + NIF), lista de items, total, botões Limpar/Pagar
- **Sheets:** PaymentView, InvoiceView, BarcodeScannerView
- **Sub-views:** `ProductSaleRowView` (stepper + botão add), `CartItemRowView` (quantidade + remove)
- Stock: cor verde/laranja/vermelho conforme nível; produtos sem stock desativados

### 7.4 PaymentView (`Views/Sales/PaymentView.swift`)
- Modal de pagamento com 5 métodos (grid 2x2)
- Entrada de valor com botão "Restante" para preencher automaticamente
- Campo de referência obrigatório para M-Pesa e e-Mola
- Suporte a pagamento misto (múltiplas entradas)
- Resumo financeiro: Total Pago, Restante, Troco (se numerário > total)
- Botão "Confirmar Venda" activo quando `paidTotal >= total`
- Modelo interno `PaymentEntry` (UUID, method, amount, reference)

### 7.5 InvoiceView (`Views/Sales/InvoiceView.swift`)
- Exibe fatura após venda concluída
- Header de sucesso (checkmark verde)
- Dados do cliente, lista de artigos, total
- Botão "Partilhar PDF" — gera PDF via `ReportService().exportGroupPDF()`
- Toolbar: botão Fechar (vermelho) + Partilhar PDF (laranja)

### 7.6 ProductListView (`Views/Products/ProductListView.swift`)
- Lista de produtos com pesquisa por nome/barcode
- Alerta de stock baixo (< 5 unidades)
- Tap para editar, swipe para apagar
- Botão "+" para novo produto
- `ProductRowView`: mostra nome, preço base, IVA, margem, barcode, preço final, stock

### 7.7 ProductFormView (`Views/Products/ProductFormView.swift`)
- Formulário para criar/editar produto
- Campos: Nome, Código de Barras (com scanner), Preço Base, Stock
- Sliders: IVA (0-30%) e Margem de Lucro (0-200%)
- Resumo de preços em tempo real: Base → Com Margem → IVA → Preço Final
- Componentes privados: `FormCard`, `CardHeader`, `SummaryRow`

### 7.8 BarcodeScannerView (`Views/Products/BarcodeScannerView.swift`)
- **iOS:** `UIViewRepresentable` com `AVCaptureSession` + `AVCaptureMetadataOutput`
- **macOS:** `NSViewRepresentable` com `MacCameraManager` (suporta Continuity Camera)
- Overlay com viewfinder animado (corners amarelos + scan line)
- Formatos: EAN-8, EAN-13, UPC-E, Code 128, Code 39, QR, PDF417, Interleaved 2of5
- macOS: selector de câmara (múltiplos dispositivos), modo manual (teclado)
- Auto-dismiss após scan bem sucedido

### 7.9 DayCloseView (`Views/DayClose/DayCloseView.swift`)
Contém 3 tabs internas + ViewModel + modelos:

#### DayCloseTabView (Fecho do Dia)
- DatePicker para selecionar data
- Badge de estado: verde (fechado), laranja (vendas após fecho), nenhum (não fechado)
- Cards de resumo por método (`ClosePaymentSummary`)
- Campo de notas/observações
- Botão "Fazer Fecho" ou "Actualizar Fecho" (nova sessão)
- Exportação Excel/PDF + ShareLink
- Só admin pode fazer fecho

#### MonthCloseTabView (Fecho do Mês)
- DatePicker + label do mês em PT
- Cards de resumo + gráfico animado de distribuição (`AnimatedBreakdownChart`)
- Exportação Excel/PDF

#### CloseHistoryView (Histórico)
- Lista de todos os fechos com data, hora, total, nº vendas

#### DayCloseViewModel
- `loadDay(date:)` e `loadMonth(month:)` — busca vendas + pagamentos → `buildSummary()`
- `isDayClosed(date:)` — verifica se há registo de fecho
- Exportação: `exportDayExcel/PDF`, `exportMonthExcel/PDF`

#### CloseSummary
- totalSales, totalCash, totalCard, totalBankTransfer, totalMpesa, totalEmola, numSales

### 7.10 Relatórios (`Views/Reports/`)

#### DailyReportView
- Selecção de data + pesquisa inline por data/hora
- Cards: Total do Dia, Nº Vendas, Itens Vendidos
- Banner "Mais Vendido"
- Lista de vendas agrupadas por cliente (expandíveis)
- Exportar CSV/PDF

#### MonthlyReportView
- Selecção de mês + pesquisa inline
- Mesmos cards e lista que o diário, mas para o mês inteiro

#### ReportHistoryView
- Filtro por tipo (Todos/Diários/Mensais)
- Lista de relatórios guardados com ícone (PDF vermelho / CSV verde)
- ShareLink para partilhar ficheiro
- Swipe para apagar

#### ReportViewModel
- Carrega vendas diárias/mensais
- Exporta CSV/PDF via `ReportService`
- Utilitários: total, totalItems, topProduct, salesByHour, salesByDay

#### ReportService
- **CSV:** `buildCSV()` genérico → `exportDailyCSV`, `exportMonthlyCSV`, `exportGroupCSV`
- **PDF:** `renderPDF()` com CoreGraphics (sem UIKit/WKWebView)
  - Título + subtítulo + cards de resumo + tabela por venda
  - Paginação automática (nova página quando sem espaço)
  - Rodapé com data de geração
- Diretório: `Documents/POSApp_Relatorios/`
- Guarda metadados na tabela Reports

#### CloseExportService
- **Excel (CSV):** Resumo por método + detalhe de vendas com métodos de pagamento
- **PDF:** Resumo por método em cards + total geral + tabela de vendas
- Diretório: `Documents/POSApp_Fechos/`

#### ReportComponents
- `MonthSelectorHeader` — Selector de mês estilizado
- `PrimaryMetricCard` — Card grande com total em destaque
- `SecondaryMetricCard` — Card com ícone + valor + label
- `TopProductBanner` — Banner do produto mais vendido
- `EmptySalesView` — Estado vazio
- `ExportButton` — Botão de exportação
- `SalesSearchField` — Campo de pesquisa inline com Escape para limpar

#### SaleReportRowView
- Linha expansível: cliente + data + total
- Ao expandir: botões CSV e PDF com ShareLink após geração

### 7.11 SettingsView (`Views/Settings/SettingsView.swift`)
- **Secção "Sessão Atual":** Mostra user logado + botão logout
- **Secção "Subscrição":** Card com estado (ativo/trial/cancelado), barra de progresso trial, botões subscrever/reativar/cancelar
- **Secção "Utilizadores"** (só admin): Lista de users com role badge, editar, apagar, adicionar
- **Secção "Aplicação":** Versão, nome da BD, botão abrir pasta da BD
- Componentes: `SectionHeader`, `RoleBadge`, `InfoRow`, `SubscriptionStatusCard`

### 7.12 UserFormView (`Views/Settings/UserFormView.swift`)
- Formulário para criar/editar utilizador
- Campos: Nome, Username, Password (com confirmação), Role (Caixa/Admin)
- Validação: password ≥ 6 chars, passwords coincidem
- Na edição: password em branco mantém a atual
- Componente `RoleOption`: seleção visual do perfil

### 7.13 POSGuideView (`Views/Posguideview.swift`)
- Guia de utilizador completo integrado na app
- **macOS:** Abre em janela separada (`POSGuideWindowController`)
- **iOS:** Abre como sheet + floating button
- 8 capítulos: Visão Geral, Vendas, Pagamentos, Fecho de Caixa, Produtos, Relatórios, Definições, Atalhos
- Componentes reutilizáveis: `POSGuideText`, `POSStepSection`, `POSInfoBlock`, `POSWarning`, `POSNote`, `POSFlowDiagram`

---

## 8. Sistema de Subscrição

### SubscriptionManager (`Views/Subscription/SubscriptionManager.swift`)
- Singleton `@MainActor` com StoreKit 2
- Product ID: `com.posapp.subscription.monthly`
- **Estado:** `isSubscribed`, `expirationDate`, `isCancelled`, `products`, `isLoading`
- **hasAccess:** `isSubscribed || TrialManager.shared.isTrialActive`
- **Fluxo:** loadProducts → purchase → checkSubscriptionStatus
- Listener em tempo real para `Transaction.updates`
- Detecta cancelamento via `renewalInfo.willAutoRenew`

### TrialManager (`Views/Subscription/TrialManager.swift`)
- Regista data do primeiro lançamento em `UserDefaults`
- Trial de 15 dias
- Propriedades: `daysRemaining`, `isTrialActive`, `isTrialExpired`

### PaywallView (`Views/Subscription/PaywallView.swift`)
- Design dark com gradientes e animações
- Badge estado trial (ativo/expirado)
- Lista de features incluídas
- Card do plano: €9,99/mês com destaques
- Botão CTA com gradiente roxo
- "Restaurar compra anterior"
- Extensão `Color(hex:)` para cores hex

### CancellationFeedbackView (`Views/Subscription/CancellationReason.swift`)
- 7 razões de cancelamento (enum `CancellationReason`)
- Formulário com seleção de razão + comentário adicional
- Envia feedback por email (`mailto:`)
- Redireciona para App Store para gerir subscrição
- Ecrã de confirmação após envio

---

## 9. Fluxo Principal de Utilização

```
1. App abre → Verifica subscrição/trial
   ├── Sem acesso → PaywallView
   └── Com acesso → LoginView
       └── Login OK → MainView
           ├── Vendas: Pesquisar produto → Adicionar ao carrinho → Pagar → Fatura
           ├── Produtos: Criar/Editar/Apagar produto
           ├── Relatórios: Diário/Mensal/Histórico + Exportar
           ├── Fecho de Caixa: Diário/Mensal/Histórico + Exportar
           └── Definições (Admin): Utilizadores + Subscrição + Info app
```

---

## 10. Métodos de Pagamento Suportados

| Método | Chave BD | Label PT | Ícone SF | Referência |
|--------|----------|----------|----------|------------|
| Numerário | `cash` | Numerário | banknote | Não |
| Cartão | `card` | Cartão | creditcard | Não |
| Transferência | `bank_transfer` | Transferência Bancária | building.columns | Não |
| M-Pesa | `mpesa` | M-Pesa | phone.fill | **Obrigatória** |
| e-Mola | `emola` | e-Mola | phone.badge.waveform.fill | **Obrigatória** |

---

## 11. Cálculo de Preços

```
Preço com Margem = Preço Base × (1 + Margem / 100)
Preço Final      = Preço com Margem × (1 + IVA / 100)
```

Exemplo: Base = 100 MT, Margem = 20%, IVA = 16%
- Com Margem = 100 × 1.20 = 120 MT
- Preço Final = 120 × 1.16 = 139.20 MT

IVA padrão: 5% (definido em `Constants.defaultIVARate` — nota: comentário diz 16%)

---

## 12. Perfis de Utilizador

| Funcionalidade | Admin | Caixa |
|---------------|-------|-------|
| Vendas | ✅ | ✅ |
| Produtos | ✅ | ✅ |
| Relatórios Diários | ✅ | ✅ |
| Relatórios Mensais | ✅ | ✅ |
| Fecho de Caixa | ✅ | ❌ (só visualiza) |
| Definições | ✅ | ❌ |
| Gestão Utilizadores | ✅ | ❌ |

---

## 13. Exportação de Ficheiros

### CSV (compatível Excel/Numbers)
- Relatórios: `Documents/POSApp_Relatorios/relatorio_diario_YYYY-MM-DD.csv`
- Fechos: `Documents/POSApp_Fechos/fecho_YYYY-MM-DD.csv`
- Vendas individuais: `Documents/POSApp_Relatorios/venda_CLIENTE_TIMESTAMP.csv`

### PDF (CoreGraphics nativo)
- Gerado sem UIKit/WKWebView — usa `CGContext`, `NSAttributedString`, `NSFont`
- Formato A4 (595 × 842 pt)
- Paginação automática
- Inclui: título, cards resumo, tabela detalhada, rodapé

---

## 14. Atalhos de Teclado (macOS)

| Acção | Atalho |
|-------|--------|
| Vendas | ⌘ 1 |
| Produtos | ⌘ 2 |
| Relatórios | ⌘ 3 |
| Fecho de Caixa | ⌘ 4 |
| Definições | ⌘ 5 |
| Pesquisar produto | ⌘ F |
| Pagar | ⌘ ↩ |
| Cancelar carrinho | ⌘ ⌫ |
| Novo produto | ⌘ ⇧ N |
| Abrir Guia | ⌘ ? |
| Logout | ⌘ ⇧ Q |

---

## 15. Dependências e Frameworks

| Framework | Uso |
|-----------|-----|
| SwiftUI | Toda a UI |
| SQLite3 | Base de dados (import direto, sem wrapper) |
| CryptoKit | Hash SHA256 para passwords |
| AVFoundation | Scanner de códigos de barras |
| CoreGraphics + CoreText | Geração de PDFs |
| AppKit (macOS) | NSWindow para guia, NSWorkspace, NSFont para PDFs |
| StoreKit 2 | Subscrição mensal in-app |
| Combine | `@Published` nos ViewModels |

**Zero dependências externas** — tudo usa frameworks nativos da Apple.

---

## 16. Notas Técnicas

- **Concorrência:** DatabaseManager é síncrono no main thread (não usa async/DispatchQueue dedicada neste projeto, ao contrário do Note_Grafo)
- **Datas:** ISO8601 para armazenamento, DateFormatter para display
- **Pesquisa:** SQL `LIKE %query%` no DatabaseManager; filtro local em SwiftUI para as views
- **Stock:** Descontado automaticamente ao finalizar venda; alerta visual em < 5 unidades
- **Fecho de Caixa:** `INSERT OR REPLACE` permite actualizar fecho existente (nova sessão)
- **Scanner macOS:** Suporta múltiplas câmaras incluindo Continuity Camera (iPhone)
- **Trial:** 15 dias, armazenado em UserDefaults, independente da subscrição
- **Subscrição:** Verificação automática ao voltar ao primeiro plano
