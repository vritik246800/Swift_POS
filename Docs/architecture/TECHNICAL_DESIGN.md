# POSApp — Documentação Técnica

**Versão:** 1.0.0  
**Plataformas:** macOS + iPadOS  
**Linguagem:** Swift + SwiftUI  
**Base de dados:** SQLite3 (local)

---

## Índice

1. [[#Arquitetura]]
2. [[#Estrutura de Ficheiros]]
3. [[#Base de Dados]]
4. [[#Models]]
5. [[#ViewModels]]
6. [[#Views]]
7. [[#Services]]
8. [[#Fluxos Principais]]
9. [[#Configuração e Constantes]]

---

## Arquitetura

O projeto segue o padrão **MVVM** (Model-View-ViewModel):

- **Model** — estruturas de dados puras (`User`, `Product`, `Sale`, `SaleItem`, `Report`)
- **ViewModel** — lógica de negócio e estado (`AuthViewModel`, `ProductViewModel`, `SaleViewModel`, `ReportViewModel`)
- **View** — interface SwiftUI, reativa ao estado dos ViewModels
- **DatabaseManager** — singleton que centraliza todas as operações SQLite3
- **ReportService** — serviço de exportação CSV e PDF

A app usa `@StateObject` e `@EnvironmentObject` para partilha de estado entre views.

---

## Estrutura de Ficheiros

```
POSApp/
├── App/
│   └── POSAppApp.swift              — Ponto de entrada, gestão de ciclo de vida
├── Models/
│   ├── User.swift                   — Utilizador com roles (admin/cashier)
│   ├── Product.swift                — Produto com cálculo de preço final
│   ├── Sale.swift                   — Venda com status
│   ├── SaleItem.swift               — Item de venda
│   └── Report.swift                 — Registo de relatório exportado
├── ViewModels/
│   ├── AuthViewModel.swift          — Login, logout, hash PBKDF2-HMAC-SHA256 (migra hashes `sha256` antigos)
│   ├── ProductViewModel.swift       — CRUD produtos, pesquisa, stock
│   ├── SaleViewModel.swift          — Carrinho, finalização de venda
│   └── ReportViewModel.swift        — Agregação de dados para relatórios
├── Views/
│   ├── Auth/
│   │   └── LoginView.swift          — Ecrã de login (painel dividido, Liquid Glass, animação de entrada e de recusa)
│   ├── MainView.swift               — Navegação principal (sidebar macOS / tabs iPadOS)
│   ├── Products/
│   │   ├── ProductListView.swift    — Lista e pesquisa de produtos
│   │   └── ProductFormView.swift    — Formulário criar/editar produto
│   ├── Sales/
│   │   ├── SaleView.swift           — Interface de venda (carrinho)
│   │   └── InvoiceView.swift        — Fatura após venda concluída
│   ├── Reports/
│   │   ├── DailyReportView.swift    — Relatório diário
│   │   ├── MonthlyReportView.swift  — Relatório mensal
│   │   ├── ReportHistoryView.swift  — Histórico de relatórios exportados
│   │   └── ReportComponents.swift  — Componentes partilhados (cards, botões)
│   └── Settings/
│       ├── SettingsView.swift       — Definições e gestão de utilizadores
│       └── UserFormView.swift       — Formulário criar/editar utilizador
├── Database/
│   └── DatabaseManager.swift        — Singleton SQLite3, todas as operações CRUD
├── Services/
│   └── ReportService.swift          — Exportação CSV e PDF (macOS + iPadOS)
└── Utils/
    └── Constants.swift              — IVA padrão, nome da app, nome da BD
```

---

## Base de Dados

**Ficheiro:** `posapp.sqlite`  
**Localização:** `~/Library/Application Support/posapp.sqlite` (macOS)

### Tabelas

#### Users
| Campo | Tipo | Notas |
|---|---|---|
| id | INTEGER PK | Auto-incremento |
| name | TEXT | Nome completo |
| username | TEXT UNIQUE | Nome de utilizador |
| password_hash | TEXT | SHA256 da password |
| role | TEXT | `admin` ou `cashier` |

#### Products
| Campo | Tipo | Notas |
|---|---|---|
| id | INTEGER PK | Auto-incremento |
| name | TEXT | Nome do produto |
| price_base | REAL | Preço sem margem nem IVA |
| iva_rate | REAL | Taxa IVA em % (ex: 16.0) |
| profit_margin | REAL | Margem de lucro em % |
| price_final | REAL | Calculado automaticamente |
| stock | INTEGER | Unidades disponíveis |

#### Sales
| Campo | Tipo | Notas |
|---|---|---|
| id | INTEGER PK | Auto-incremento |
| user_id | INTEGER FK | Referência a Users |
| client_name | TEXT | Nome do cliente (opcional) |
| client_nif | TEXT | NIF do cliente (opcional) |
| total | REAL | Total da venda |
| date | TEXT | ISO8601 |
| status | TEXT | `completed` ou `cancelled` |

#### SaleItems
| Campo | Tipo | Notas |
|---|---|---|
| id | INTEGER PK | Auto-incremento |
| sale_id | INTEGER FK | Referência a Sales |
| product_id | INTEGER FK | Referência a Products |
| product_name | TEXT | Nome guardado no momento da venda |
| quantity | INTEGER | Quantidade vendida |
| unit_price | REAL | Preço unitário no momento da venda |
| subtotal | REAL | quantity × unit_price |

#### Reports
| Campo | Tipo | Notas |
|---|---|---|
| id | INTEGER PK | Auto-incremento |
| type | TEXT | `daily` ou `monthly` |
| period | TEXT | `yyyy-MM-dd` ou `yyyy-MM` |
| file_path | TEXT | Path absoluto do ficheiro |
| created_at | TEXT | ISO8601 |

---

## Models

### Product — Cálculo de preço

```swift
static func calculateFinalPrice(base: Double, profit: Double, iva: Double) -> Double {
    let withProfit = base * (1 + profit / 100)
    return withProfit * (1 + iva / 100)
}
```

Exemplo com `base = 10€`, `profit = 20%`, `iva = 16%`:
- Com margem: `10 × 1.20 = 12€`
- Com IVA: `12 × 1.16 = 13.92€`

### UserRole

```swift
enum UserRole: String, Codable {
    case admin = "admin"
    case cashier = "cashier"
}
```

---

## ViewModels

### AuthViewModel
- `login(username:password:)` — recusa entrada hostil (R18: vazio, > 64 caracteres no username, > 128 na password, caracteres de controlo) e só depois verifica credenciais com PBKDF2-HMAC-SHA256
- `logout()` — limpa sessão (`currentUser` no ViewModel e no `DatabaseManager`)
- `createUser(name:username:password:role:)` — cria utilizador com hash
- `hashPassword(_:)` / `verifyPassword(_:storedHash:)` — PBKDF2-HMAC-SHA256, 210 000 iterações, sal de 16 bytes por utilizador; hashes `sha256` antigos ainda validam e migram no primeiro login com sucesso
- `loginFailureCount` — contador de recusas, só para a UI animar (não guarda credenciais)
- `isAdmin` — computed property para verificar role

### ProductViewModel
- `loadProducts()` — carrega todos os produtos da BD
- `search()` — pesquisa por nome (LIKE)
- `createProduct(...)` — valida e insere na BD
- `updateProduct(_:)` — atualiza produto e recalcula preço final
- `deleteProduct(id:)` — remove da BD
- `previewFinalPrice(base:profit:iva:)` — cálculo em tempo real para o formulário
- `lowStockProducts` — produtos com stock < 5

### SaleViewModel
- `addToCart(product:quantity:)` — adiciona ao carrinho, verifica stock, agrupa duplicados
- `removeFromCart(productId:)` — remove item do carrinho
- `finalizeSale(userId:)` — cria venda na BD, baixa stock automaticamente
- `clearCart()` — limpa carrinho e dados do cliente
- `cartTotal` — soma dos subtotais
- `salesForDay(_:)` / `salesForMonth(_:)` — filtro por período

### ReportViewModel
- `loadDailySales(date:)` — vendas de um dia específico
- `loadMonthlySales(date:)` — vendas de um mês específico
- `total(for:)` / `totalItems(for:)` — agregações
- `topProduct(for:)` — produto mais vendido por quantidade
- `salesByHour(for:)` / `salesByDay(for:)` — agrupamento para gráficos

---

## Views

### Navegação
- **macOS** — `NavigationSplitView` com sidebar (Vendas, Produtos, Relatórios, Fecho de Caixa, Administração, Definições)
- **iPadOS** — `TabView` com tab bar em baixo
- Separado por `#if os(macOS)` / `#else`
- Perfil **Caixa** só tem Vendas e Fecho de Caixa (a barreira real está no `DatabaseManager`)

### Administração › Dashboard (`Views/Admin/AdminDashboardView.swift`)
- Período `Hoje · Mês · Ano · Total`: os três primeiros são relativos a hoje — `Calendar.isDate(_:equalTo:toGranularity:)` compara também as unidades maiores, por isso "Mês" é o mês do **ano actual** e nunca o mesmo mês de outros anos
- Em `Total` aparece a barra `Ano · Mês · Dia` ligada a `AdminViewModel.DateFilter`; "Mês" fica desactivado sem ano e "Dia" sem mês, e a lista de dias vem de `daysInSelectedMonth` (28/29/30/31 reais)
- Um só filtro manda em tudo o que está abaixo: KPIs, gráfico e os três painéis usam `sales(in:)`, e o subtítulo de cada painel é `periodLabel(_:)`
- Layout em duas colunas (`ViewThatFits`, igual ao padrão do `SettingsView`): coluna principal com o bloco de indicadores e o painel do gráfico; coluna lateral (340 pt) com as distribuições — top de produtos, receita por categoria e métodos de pagamento. Em janela estreita ou iPhone empilha tudo numa coluna
- O painel do gráfico tem um **seletor segmentado** (`ChartKind`: `Receita` · `Vendas por caixa`) no topo do conteúdo: um só painel e um só lugar no ecrã, muda o que lá está dentro. Título, ícone e subtítulo do `AdminPanel` seguem a escolha, a troca anima por opacidade (desligada com `Reduce Motion`) e o período do cabeçalho continua a mandar nos dois gráficos
- "Vendas por caixa" é um gráfico de **barras horizontais** (`BarMark` com `x` = total, `y` = nome), ordenado do maior total para o menor, com anotação `valor · nº de vendas` à direita de cada barra; o `chartXScale` abre até 1,45× o maior total para a anotação não sair do painel e a altura é `max(190, nº de caixas × 44)`. Os dados vêm de `AdminViewModel.cashierPerformance(in:)`, que aplica ao período a agregação pura `cashierPerformance(sales:users:)` (nº de vendas + total por utilizador, do maior para o menor). A lista de utilizadores é a `@Published var users` carregada no `load()` — nada de `fetchUsers()` por redesenho — e uma venda de utilizador já apagado conta na mesma, com o nome `Utilizador #<id>`, para a soma dos caixas bater certo com a receita do período
- Bloco de indicadores: uma grelha só, de colunas iguais (`GridItem(.flexible(minimum: 170))`), com a contagem escolhida por `ViewThatFits` entre **3 · 2 · 1** — divisores de seis, por isso a última linha nunca fica com buraco. A **Receita** é o primeiro cartão e o único `AdminKPICard(prominent: true)` (mesmo vidro `.regular`, tipografia e espaçamento maiores); o `AdminKPICard` estica a `maxHeight: .infinity` com `alignment: .topLeading` para o vidro dos cartões da mesma linha alinhar sem abrir vazio entre o rótulo e o valor
- O período aparece **uma só vez**, no cabeçalho ("Visão geral" + `periodLabel`); os painéis deixaram de repetir o rótulo no subtítulo — o do gráfico passou a ser só o total do período
- O gráfico usa `revenueSeries(in:)` — `RevenueSeries` traz os pontos com os intervalos vazios a zero e a `Calendar.Component` do eixo X (`.hour` num dia, `.day` num mês, `.month` num ano ou no total); o `unit` é lido para constante local antes do `Chart` e o eixo usa `.automatic(desiredCount: 6)` com o formato à medida da unidade

### Administração › Validade (`Views/Admin/AdminExpiryView.swift`)
- "Em risco" ordenado pelo prazo mais curto, com os dias que faltam por produto
- Uma barra repartida pelas faixas de validade + legenda (lotes, % e valor)
- Tocar num lote (em risco ou expirado) abre `BatchEditSheet` — quantidade e data de validade
- Tocar num produto de "Stock baixo" abre `StockEditSheet` — reposição de stock
- Ambos gravam por `AdminViewModel.updateBatch` / `updateStock` (validação no ViewModel, SQL preparado no `DatabaseManager`)
- As duas folhas partilham as peças privadas `EditSheetHeader` (ícone tingido pelo estado + selo), `StepperField` (`−` valor `+` em vidro) e `EditSheetFooter` (Cancelar / Guardar em vidro); o corpo é **um só** plano de vidro tingido (`.regular.tint(cor.opacity(0.10))`)
- `BatchEditSheet` mostra os dias exactos ("Faltam 12 dias", "Expirou há 3 dia(s)") em vez do rótulo genérico de `ExpiryStatus`, e o delta face à quantidade actual do lote

### Administração › Parados (`Views/Admin/StaleProductsView.swift`)
- Os três `AdminKPICard` usam o vidro neutro (`.regular`), igual ao Dashboard, Validade e Fechos — só o ícone e o valor levam a cor do indicador
- O `Picker` de meses vai com `.labelsHidden()`: o rótulo "Meses" era desenhado ao lado e partia em duas linhas; o texto descritivo é o "Sem venda há mais de" à esquerda

### Guia (`Views/Posguideview.swift`)
- `POSGuideView(isAdmin:)` — o Caixa só vê capítulos dos ecrãs que tem
- Visão Geral, Fecho de Caixa e Atalhos têm conteúdo diferente por perfil
- macOS: `POSGuideWindowController.open(isAdmin:)` refaz a janela se o perfil mudar

### ProductFormView
- Slider de IVA (0–30%, step 1)
- Slider de margem de lucro (0–200%, step 1)
- Previsão do preço final em tempo real
- Stepper para stock

### SaleView
- Layout de 2 colunas: produtos à esquerda, carrinho à direita
- Pesquisa em tempo real
- Stepper por produto para selecionar quantidade
- Produtos sem stock aparecem desativados
- Confirmação antes de limpar carrinho

### InvoiceView
- Exibida após finalização de venda
- Mostra ID da venda, data, cliente, NIF, itens e total

---

## Services

### ReportService

#### Exportação CSV
- Colunas: ID Venda, Data, Hora, Cliente, NIF, Produto, Quantidade, Preço Unit., Subtotal, Total Venda
- Começa com BOM UTF-8 (`csvBOM`) — sem ele o Excel perde os acentos
- Texto por `csvField` (escaping + anti-injeção de fórmula); valores monetários por `csvNumber` (número cru, ponto decimal, sem moeda) para o Excel os somar
- Ficheiro gravado permanentemente em `~/Documents/POSApp_Relatorios/`
- Partilhado via `NSWorkspace` (macOS) ou `UIActivityViewController` (iPadOS)

#### Exportação PDF
- **macOS** — `CGContext` com `NSAttributedString`
- **iPadOS** — `UIGraphicsPDFRenderer` com `UIMarkupTextPrintFormatter`
- Conteúdo: título, resumo (total, nº vendas, itens), tabela detalhada
- Todas as páginas levam rodapé com a origem (`Constants.appName`) e o número de página

#### Nomenclatura dos ficheiros
- Diário CSV: `relatorio_diario_yyyy-MM-dd.csv`
- Diário PDF: `relatorio_diario_yyyy-MM-dd.pdf`
- Mensal CSV: `relatorio_mensal_yyyy-MM.csv`
- Mensal PDF: `relatorio_mensal_yyyy-MM.pdf`

---

## Fluxos Principais

### Login
1. Utilizador insere username + password (Enter encadeia os campos)
2. `AuthViewModel.login()` recusa entrada hostil antes de tocar na base de dados (R18)
3. Deriva PBKDF2-HMAC-SHA256 com o sal do utilizador e compara em tempo constante — a derivação corre mesmo com utilizador inexistente, para o tempo não revelar se a conta existe
4. Falha: `errorMessage` + `loginFailureCount += 1` → `LoginView` abana o ecrã e dá o clarão vermelho; 5 falhas seguidas bloqueiam 30 s
5. Sucesso: `isLoggedIn = true` → `RootView` troca para `MainView` com animação (login encolhe, painel cresce)

### Criar Produto
1. Admin abre formulário de produto
2. Preenche nome, preço base, ajusta IVA e margem com sliders
3. Preço final é calculado em tempo real
4. Ao guardar → insere na BD com preço final calculado

### Realizar Venda
1. Caixa pesquisa produto
2. Seleciona quantidade com stepper → adiciona ao carrinho
3. Preenche dados do cliente (opcional)
4. Clica "Finalizar Venda"
5. BD insere venda + itens e baixa stock automaticamente
6. Fatura é mostrada

### Fecho da App
1. `scenePhase` muda para `.inactive` ou `.background`
2. `saveEndOfDayReport()` busca todas as vendas do dia
3. Se houver vendas → exporta CSV e PDF automaticamente
4. Se for o último dia do mês → exporta também relatório mensal

---

## Configuração e Constantes

```swift
// Utils/Constants.swift
enum Constants {
    static let defaultIVARate: Double = 16.0   // IVA padrão (%)
    static let appName: String = "POSApp"
    static let dbName: String = "posapp.sqlite"
}
```

### Pasta de relatórios
- **macOS:** `~/Documents/POSApp_Relatorios/`
- **iPadOS:** Pasta Documents da app (sandbox)

### Segurança
- Passwords nunca guardadas em texto simples
- Hash SHA256 via `CryptoKit` (framework Apple nativo)
- Utilizadores com role `cashier` não têm acesso às Definições

---

## Dependências

| Framework | Uso |
|---|---|
| SwiftUI | Interface de utilizador |
| SQLite3 | Base de dados local |
| CryptoKit | Hash SHA256 de passwords |
| Foundation | Formatação de datas, FileManager |
| AppKit (macOS) | NSWorkspace, NSFont, CGContext |
| UIKit (iPadOS) | UIActivityViewController, UIGraphicsPDFRenderer |

Todas as dependências são frameworks nativos Apple — sem packages externos.
