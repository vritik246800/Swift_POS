# CHANGELOG — POS Sales_Project

Histórico dos ciclos de `Docs/TODO.md` já fechados. Cada secção é um ciclo completo: tarefas implementadas, testadas e documentadas. Regra em `CLAUDE.md` §1.6.

## Índice

| Data       | Título                                                                                                     | Linha | Ligação                                                                                                                                   |
| ---------- | ---------------------------------------------------------------------------------------------------------- | ----- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| 2026-08-14 | Categorias, lotes/FIFO, alertas de validade e frontend completo (Partes 1 e 2)                             | 34    | [[CHANGELOG#2026-08-14 — Categorias, lotes/FIFO, alertas de validade e frontend completo (Partes 1 e 2)\|ir]]                             |
| 2026-08-15 | Relatório anual, cards de factura e correcção do texto invertido nos PDF                                   | 373   | [[CHANGELOG#2026-08-15 — Relatório anual, cards de factura e correcção do texto invertido nos PDF\|ir]]                                   |
| 2026-08-15 | Histórico de relatórios pesquisável, Fecho do Ano, Definições redesenhadas (+ wizard) e Guia actualizado   | 421   | [[CHANGELOG#2026-08-15 — Histórico de relatórios pesquisável, Fecho do Ano, Definições redesenhadas (+ wizard) e Guia actualizado\|ir]]   |
| 2026-08-16 | Impressão de facturas (80 mm/A4), redesenho de painéis e novos gráficos                                    | 504   | [[CHANGELOG#2026-08-16 — Impressão de facturas (80 mm/A4), redesenho de painéis e novos gráficos\|ir]]                                    |
| 2026-08-16 | Gráficos do fecho a toda a altura e partilha na fatura                                                     | 620   | [[CHANGELOG#2026-08-16 — Gráficos do fecho a toda a altura e partilha na fatura\|ir]]                                                     |
| 2026-08-16 | Nome do programa configurável, cards de venda maiores, stepper no carrinho, documentos e layout do fecho   | 639   | [[CHANGELOG#2026-08-16 — Nome do programa configurável, cards de venda maiores, stepper no carrinho, documentos e layout do fecho\|ir]]   |
| 2026-08-16 | Validade a bloquear a venda, promoções, gráficos e painéis animados                                        | 677   | [[CHANGELOG#2026-08-16 — Validade a bloquear a venda, promoções, gráficos e painéis animados\|ir]]                                        |
| 2026-08-16 | UX de vendas: filtro com scroll, pagamento em duas colunas, botão Imprimir com cor                         | 733   | [[CHANGELOG#2026-08-16 — UX de vendas: filtro com scroll, pagamento em duas colunas, botão Imprimir com cor\|ir]]                         |
| 2026-08-16 | Painel de perda real, filtro unificado, cor nos cartões e fim do fundo cinzento do Fecho                   | 751   | [[CHANGELOG#2026-08-16 — Painel de perda real, filtro unificado, cor nos cartões e fim do fundo cinzento do Fecho\|ir]]                   |
| 2026-08-16 | Reordenar categorias por drag + redesenho do gestor de categorias                                          | 776   | [[CHANGELOG#2026-08-16 — Reordenar categorias por drag + redesenho do gestor de categorias\|ir]]                                          |
| 2026-08-16 | Produtos: chips de categoria maiores, painéis Perda/Risco separados, stock dos lotes                       | 813   | [[CHANGELOG#2026-08-16 — Produtos: chips de categoria maiores, painéis Perda/Risco separados, stock dos lotes\|ir]]                       |
| 2026-08-16 | Área de Administração (dashboard, validade, produtos parados, fecho por caixa) e correcções nas categorias | 847   | [[CHANGELOG#2026-08-16 — Área de Administração (dashboard, validade, produtos parados, fecho por caixa) e correcções nas categorias\|ir]] |
| 2026-08-16 | Fecho da própria caixa, Guia por perfil e edição de lotes/stock na Administração                           | 950   | [[CHANGELOG#2026-08-16 — Fecho da própria caixa, Guia por perfil e edição de lotes/stock na Administração\|ir]]                           |
| 2026-08-16 | Folhas de lote e stock em Liquid Glass, selector de meses e cartões tingidos em Parados                    | 1025  | [[CHANGELOG#2026-08-16 — Folhas de lote e stock em Liquid Glass, selector de meses e cartões tingidos em Parados\|ir]]                    |
| 2026-08-16 | Regra UX antes de UI com PLAN.md, animação/transição e Liquid Glass obrigatórios                           | 1047  | [[CHANGELOG#2026-08-16 — Regra UX antes de UI com PLAN.md, animação/transição e Liquid Glass obrigatórios\|ir]]                           |
| 2026-08-16 | Filtro de data no Dashboard da Administração                                                               | 1069  | [[CHANGELOG#2026-08-16 — Filtro de data no Dashboard da Administração\|ir]]                                                               |
| 2026-08-16 | Cartões de "Parados" com o vidro neutro da Administração                                                   | 1109  | [[CHANGELOG#2026-08-16 — Cartões de "Parados" com o vidro neutro da Administração\|ir]]                                                   |
| 2026-08-17 | Segurança em três rondas, SECURITY_POLICY, TESTING.md e ERRORS.md                                          | 1133  | [[CHANGELOG#2026-08-17 — Segurança em três rondas, SECURITY_POLICY, TESTING.md e ERRORS.md\|ir]]                                          |
| 2026-08-17 | Validação em cinco rondas (V1–V5) e portões P1–P8                                                          | 1209  | [[CHANGELOG#2026-08-17 — Validação em cinco rondas (V1–V5) e portões P1–P8\|ir]]                                                          |
| 2026-08-19 | Seletor de gráfico no Dashboard (Receita · Vendas por caixa) e indicadores em grelha de colunas iguais     | 1267  | [[CHANGELOG#2026-08-19 — Seletor de gráfico no Dashboard (Receita · Vendas por caixa) e indicadores em grelha de colunas iguais\|ir]]     |
| 2026-08-19 | Ecrã de login redesenhado — painel dividido, Liquid Glass, animação de entrada, de recusa e de transição   | 1354  | [[CHANGELOG#2026-08-19 — Ecrã de login redesenhado — painel dividido, Liquid Glass, animação de entrada, de recusa e de transição\|ir]]   |
| 2026-08-19 | Login a recusar credenciais certas — sqlite3_bind_text com SQLITE_STATIC (E23)                             | 1397  | [[CHANGELOG#2026-08-19 — Login a recusar credenciais certas — sqlite3_bind_text com SQLITE_STATIC (E23)\|ir]]                             |

---

## 2026-08-14 — Categorias, lotes/FIFO, alertas de validade e frontend completo (Partes 1 e 2)

# TODO — POS Sales_Project

Decisões fechadas:
- Categorias: **CRUD completo na BD** (tabela `Categories`, ícone SF Symbol + cor por categoria)
- Validade: **por lote** (tabela `Batches`), stock = soma dos lotes
- Liquid Glass: **API nativa `.glassEffect()`**, target macOS 26 / iOS 26
- Popout relatórios: **menu de escolha de formato** (CSV ou PDF), exporta direto e revela no Finder
- Cards de venda: **card quadrado com stepper** dentro
- Alerta de validade: **sheet no arranque + badge** na sidebar
- Perdas: **dois valores separados** — "Perda real" (expirado) e "Em risco" (a expirar)
- Formulário de produto: **wizard de 2 passos**, janela larga

---

# PARTE 1 — BACKEND

Nada de UI nesta parte. Ordem obrigatória: 1.0 → 1.1 → 1.2 → 1.3 → 1.4 → 1.5.

> **Regra transversal (CLAUDE.md §2):** toda a tarefa abaixo que crie, altere ou remova um fluxo, ViewModel, serviço ou ecrã fecha com a atualização do diagrama correspondente em `Docs/architecture/SYSTEM_DESIGN.md` (Mermaid). Sem isso a tarefa não é `[x]`.

## 1.0 — Fundações (bloqueante)

Nada da 1.1 em diante arranca antes de a 1.0 fechar.

### 1.0.1 — Correções de segurança da auditoria

Origem: `Docs/security/SECURITY.md`, secção 9. Ordem por severidade: A → M → B. Cada correção fecha com o teste indicado em `POSAppTests/`.

**Severidade A — corrigir já**

- [x] **S1** SQL por interpolação no filtro de mês — `Database/DatabaseManager.swift:592`: passar a `LIKE ?` com bind de `month + "%"`. Teste: `SQLInjectionTests`.
- [x] **S2** Password em SHA-256 sem sal — `ViewModels/AuthViewModel.swift:41-45`: PBKDF2-HMAC-SHA256 via `CommonCrypto` (framework do sistema, sem dependências externas), sal de 16 bytes por utilizador, ≥210 000 iterações, formato `pbkdf2$sha256$<iter>$<sal>$<hash>` na coluna existente. Hashes antigos ficam com prefixo `sha256$` e migram no primeiro login com sucesso. Teste: `PasswordHashTests`.
- [x] **S3** Autorização só na UI — mover a verificação de perfil para `ViewModels`/`DatabaseManager` em: apagar/editar utilizador, apagar produto, alterar preço, reabrir fecho de caixa, apagar venda. O último Admin não pode ser apagado nem despromovido. Teste: `AuthorizationTests`.
- [x] **S4** Venda sem transação — `Database/DatabaseManager.swift:387-411` + `ViewModels/SaleViewModel.swift:60-83`: envolver Sales + SaleItems + stock + Payments em `BEGIN IMMEDIATE` / `COMMIT` / `ROLLBACK`. Acrescentar `PRAGMA foreign_keys = ON;` no arranque (**S13**). Teste: `TransactionTests`.
- [x] **S5** Proximidade sem TLS nem autenticação — `List_Storage/ProximityManager.swift:96,211` e `Views/POSProximityService.swift:38,164`: `NWParameters(tls:)` com PSK derivada de código de emparelhamento de 6 dígitos + confirmação explícita do utilizador antes de aceitar a ligação.
- [x] **S6** Password de Admin em código — `Sales_Project/Sales_ProjectApp.swift:16-21`: substituir por ecrã de criação do primeiro Admin no arranque inicial.

**Severidade M — antes da próxima versão**

- [x] **S7** Payload de rede sem limite nem timeout — `List_Storage/ProximityManager.swift:263-308`: recusar acima de 10 MB antes de alocar memória, timeout de 30 s, uma ligação de cada vez. Teste: `ProximityPayloadTests`.
- [x] **S8** CSV sem escaping — criar `csvField(_:)` única (escapa `"`, vírgula e nova linha; neutraliza `= + - @` contra injeção de fórmula) e usá-la em `Views/Reports/ReportService.swift:19-40` e `Views/LowStockExportService.swift:36`. Teste: `CSVEscapingTests`.
- [x] **S9** Nome de ficheiro a partir do nome do cliente — `Views/Reports/ReportService.swift:73-76`: sanitizar para alfanuméricos + `_`, máximo 40 caracteres. Teste: `FilenameSanitizationTests`.
- [x] **S10** Login expõe existência de conta — `ViewModels/AuthViewModel.swift:13-26`: mensagem única "Credenciais inválidas.", KDF calculado mesmo com utilizador inexistente, comparação em tempo constante, bloqueio de 30 s após 5 falhas.
- [x] **S11** Ficheiro da BD sem proteção — `Database/DatabaseManager.swift:17-29`: permissões `0o600`, diretoria de relatórios `0o700`, `FileProtectionType.completeUntilFirstUserAuthentication` em iOS.
- [x] **S12** Logs com dados sensíveis — envolver os `print` de diagnóstico em `#if DEBUG` e retirar caminho da BD e conteúdo de transferências (`Database/DatabaseManager.swift:25`, `List_Storage/ProximityManager.swift`).

**Severidade B — dívida assumida**

- [x] **S14** Período de teste em `UserDefaults` (`Views/Subscription/TrialManager.swift:10-17`) → Keychain ou data da primeira transação StoreKit.
- [x] **S15** TOCTOU de stock (`ViewModels/SaleViewModel.swift:19-23`) → revalidar stock dentro da transação da venda. Encaixa na tarefa 1.3 (FIFO).
- [x] **S16** `NSBonjourServices` do `List-Storage-Info.plist` (`_pos-csv-share._tcp`) não corresponde ao `serviceType` do código (`_posapp._tcp`); falta `NSLocalNetworkUsageDescription`.
- [x] **S17** Criar `.gitignore` na raiz com `*.sqlite*`, `POSApp_Relatorios/`, `*.csv`, `*.pdf`.
- [x] Acrescentar tabela `AuditLog` (`user_id`, `action`, `entity`, `entity_id`, `timestamp`) para login falhado, gestão de utilizadores, alteração de preço, remoção de venda e fecho/reabertura de caixa. Atualiza `Docs/database/DATABASE.md` (`erDiagram` + relações).
- [x] Marcar `[x]` os pontos correspondentes no quadro da secção 9 de `Docs/security/SECURITY.md` à medida que forem corrigidos.

### 1.0.2 — `Docs/architecture/SYSTEM_DESIGN.md` passa a cobrir o sistema inteiro

Hoje o ficheiro só documenta a partilha por proximidade. Nenhuma tarefa deste TODO toca proximidade, logo sem este passo o diagrama nunca reflete o trabalho feito.

- [x] Renomear o título: `# Diagrama do Sistema — POS Sales_Project`, e mover o conteúdo atual para uma secção `## Partilha por Proximidade` (conteúdo mantém-se, só desce um nível)
- [x] Nova secção `## Arquitetura Geral` — `flowchart TD` com `subgraph` por camada: Views → ViewModels → DatabaseManager → Models, mais `Utils/AppTheme.swift` e `Views/Reports/ReportService.swift` (espelha `Docs/architecture/ARCHITECTURE.md`, não inventa camadas novas)
- [x] Nova secção `## Fluxo de Venda` — `sequenceDiagram`: SaleView → SaleViewModel → DatabaseManager (transação, `consumeStockFIFO`, `syncProductStock`) → InvoiceView. Fica pronto para a tarefa 1.3 preencher o FIFO.
- [x] Nova secção `## Ciclo de Vida de um Lote` — `stateDiagram-v2`: recebido → em stock → a expirar (dias/1m/2m/3m) → expirado → consumido (FIFO). Alinhado com `Models/ExpiryStatus.swift` da tarefa 1.2.
- [x] Nova secção `## Alerta de Validade no Arranque` — `stateDiagram-v2` com `shouldShowExpiryAlert()` e "Dispensar hoje" (tarefa 1.4)
- [x] Nova secção `## Exportação de Relatórios` — `flowchart LR`: escolha CSV/PDF → `ReportService` → revelar no Finder (macOS) / `ShareSheet` (iOS)
- [x] Converter para Mermaid o ASCII art que sobrar nas secções de proximidade (secção 9 do CLAUDE.md proíbe ASCII aqui). Exceção: wireframes de "Estados da Interface" ficam ASCII **e** ganham ao lado o `stateDiagram-v2` dos estados.
- [x] "Performance Metrics" e "Packet Structure" passam a tabela Markdown se ainda estiverem em caixas ASCII (dados tabulares não são diagramas)
- [x] Verificar que todos os blocos renderizam no Obsidian antes de marcar `[x]`

## 1.1 — Categorias (BD + modelo + ViewModel)

### `Database/DatabaseManager.swift`
- [x] `createCategoriesTable()`
  ```sql
  CREATE TABLE IF NOT EXISTS Categories (
      id INTEGER PRIMARY KEY AUTOINCREMENT,
      name TEXT NOT NULL UNIQUE,
      icon TEXT NOT NULL DEFAULT 'cube.box.fill',   -- SF Symbol
      color_hex TEXT NOT NULL DEFAULT '5856D6',
      sort_order INTEGER NOT NULL DEFAULT 0
  );
  ```
- [x] `migrateAddCategoryToProducts()` — mesmo padrão de `migrateAddBarcode()` (`PRAGMA table_info(Products)`):
  ```sql
  ALTER TABLE Products ADD COLUMN category_id INTEGER REFERENCES Categories(id);
  CREATE INDEX IF NOT EXISTS idx_products_category ON Products(category_id);
  ```
  `category_id` fica NULL nos produtos existentes = "Sem categoria".
- [x] `seedDefaultCategories()` — só corre se a tabela estiver vazia:
  - Bebidas · `cup.and.saucer.fill` · `007AFF`
  - Alimentos · `carrot.fill` · `FF9500`
  - Limpeza · `bubbles.and.sparkles.fill` · `34C759`
  - Higiene · `drop.fill` · `5AC8FA`
  - Papelaria · `pencil.and.ruler.fill` · `AF52DE`
  - Outros · `shippingbox.fill` · `8E8E93`

- [x] CRUD: `fetchCategories() -> [Category]`, `createCategory(...)`, `updateCategory(_:)`, `deleteCategory(id:)`
- [x] `deleteCategory` faz `UPDATE Products SET category_id = NULL WHERE category_id = ?` antes de apagar (nunca apagar produtos)
- [x] Chamar `createCategoriesTable()`, `migrateAddCategoryToProducts()`, `seedDefaultCategories()` dentro de `createTables()`

### `Models/Category.swift` (novo)
- [x] `struct Category: Identifiable, Codable, Hashable { id, name, icon, colorHex, sortOrder }`
- [x] `var color: Color { Color(hex: colorHex) }` — em extensão dentro de `Utils/AppTheme.swift`, não no modelo (modelo sem SwiftUI)

### `ViewModels/CategoryViewModel.swift` (novo)
- [x] `@Published categories: [Category]`, `loadCategories()`, `create/update/delete`, `errorMessage`
- [x] `func category(for id: Int?) -> Category?` — devolve `nil` para "Sem categoria"
- [x] Registar como `@EnvironmentObject` em `Sales_Project/Sales_ProjectApp.swift`

### `Models/Product.swift` + `ViewModels/ProductViewModel.swift`
- [x] Adicionar `var categoryId: Int?` ao `Product`
- [x] Actualizar `createProduct(...)` / `updateProduct(...)` / mapeamento SQL em `DatabaseManager` (SELECT, INSERT, UPDATE) com a nova coluna
- [x] `ProductViewModel`: `func products(inCategory id: Int?) -> [Product]` (nil = todos)

## 1.2 — Lotes e validade (tabela Batches)

⚠️ Esta é a mudança estrutural maior: `Products.stock` deixa de ser a fonte de verdade e passa a ser derivado da soma dos lotes. Fazer a migração num commit isolado e testar antes de avançar.

### `Database/DatabaseManager.swift`
- [x] `createBatchesTable()`
  ```sql
  CREATE TABLE IF NOT EXISTS Batches (
      id INTEGER PRIMARY KEY AUTOINCREMENT,
      product_id INTEGER NOT NULL,
      quantity INTEGER NOT NULL DEFAULT 0,
      price_base REAL NOT NULL,          -- preço base pago neste lote (base do cálculo de perdas)
      expiry_date TEXT,                  -- ISO8601 yyyy-MM-dd; NULL = não expira
      received_at TEXT NOT NULL,
      FOREIGN KEY(product_id) REFERENCES Products(id) ON DELETE CASCADE
  );
  CREATE INDEX IF NOT EXISTS idx_batches_product ON Batches(product_id);
  CREATE INDEX IF NOT EXISTS idx_batches_expiry ON Batches(expiry_date);
  ```
- [x] `migrateStockToBatches()` — corre uma vez: para cada produto com `stock > 0` e **sem** lotes, cria um lote inicial (`quantity = stock`, `price_base = price_base`, `expiry_date = NULL`, `received_at = agora`). Sem isto o stock existente desaparece do ecrã.
- [x] CRUD: `fetchBatches(productId:)`, `fetchAllBatches()`, `createBatch(...)`, `updateBatch(_:)`, `deleteBatch(id:)`
- [x] `func consumeStockFIFO(productId: Int, quantity: Int) -> Bool` — desconta dos lotes por `expiry_date ASC` (NULL por último), apaga lotes que chegam a 0, e no fim faz `syncProductStock(productId:)`
- [x] `func syncProductStock(productId: Int)` — `UPDATE Products SET stock = (SELECT COALESCE(SUM(quantity),0) FROM Batches WHERE product_id = ?)`. `Products.stock` fica como cache de leitura (evita reescrever todos os SELECTs e a UI de stock existente).
- [x] Chamar `syncProductStock` após **qualquer** escrita em Batches
- [x] `updateStock(productId:newStock:)` existente (usado por `LowStockView`): reencaminhar para ajuste de lote, não escrever `Products.stock` diretamente — senão o valor é apagado no próximo sync
- [x] Chamar `createBatchesTable()` + `migrateStockToBatches()` em `createTables()`

### `Models/Batch.swift` (novo)
- [x] `struct Batch: Identifiable, Codable { id, productId, quantity, priceBase, expiryDate: Date?, receivedAt: Date }`
- [x] `var lostValue: Double { Double(quantity) * priceBase }`

### `Models/ExpiryStatus.swift` (novo) — fonte única das faixas
- [x] ```swift
  enum ExpiryStatus: Int, CaseIterable {
      case expired, days, oneMonth, twoMonths, threeMonths, safe, none
  }
  ```
  Regra a partir de dias restantes: `< 0` expired · `0...30` days · `31...60` oneMonth · `61...90` twoMonths · `91...120` threeMonths · `> 120` safe · `expiryDate == nil` none
- [x] Propriedades `label` (PT), `icon`, `severity`. Cores ficam em `AppTheme` (modelo sem SwiftUI).
- [x] `static func from(expiryDate: Date?, now: Date = .now) -> ExpiryStatus`

  ✅ **Teste obrigatório** — `POSAppTests/ExpiryStatusTests.swift`: uma data por faixa + fronteiras (0, 30, 31, 90, 91) + `nil`. É a lógica que alimenta alertas e perdas.

### `ViewModels/BatchViewModel.swift` (novo)
- [x] `loadBatches()`, `create/update/delete`, `batches(for productId:)`
- [x] `var expiringGroups: [ExpiryStatus: [Batch]]` — para o alerta do arranque
- [x] `var realLoss: Double` — soma `lostValue` dos lotes `.expired`
- [x] `var riskValue: Double` — soma `lostValue` dos lotes `.days/.oneMonth/.twoMonths/.threeMonths`
- [x] `var riskBreakdown: [ExpiryStatus: Double]` — valor por faixa

## 1.3 — Vendas com FIFO

### `ViewModels/SaleViewModel.swift`
- [x] `finalizeSaleWithPayments(...)`: substituir a descida de stock atual por `consumeStockFIFO(productId:quantity:)`
- [x] `addToCart`: validar contra o stock somado dos lotes (não contra lote individual)
- [x] Manter a venda numa transação SQL — se o FIFO falhar a meio, `ROLLBACK` (senão o stock fica dessincronizado da venda)

  ✅ **Teste obrigatório** — `POSAppTests/FIFOTests.swift`: produto com 3 lotes (validades diferentes), vender quantidade que atravessa 2 lotes, verificar que o lote mais antigo esvazia primeiro e a soma bate certo.

## 1.4 — Estado do alerta de arranque

- [x] `Utils/Constants.swift` ou `@AppStorage`: chave `expiryAlertDismissedDate` (String `yyyy-MM-dd`)
- [x] `func shouldShowExpiryAlert() -> Bool` — true se houver lotes fora de `.safe/.none` **e** a data guardada não for hoje
- [x] "Dispensar hoje" grava a data de hoje

## 1.5 — Exportação (backend dos relatórios)

### `Views/Reports/ReportService.swift`
- [x] Já existe `exportDailyCSV/PDF` e `exportMonthlyCSV/PDF` — reutilizar, **não** escrever novos exportadores
- [x] Falta só: `func revealInFinder(_ url: URL)` (macOS `NSWorkspace.shared.activateFileViewerSelecting`) e, em iOS, devolver a URL para `ShareSheet` (já existe em `List_Storage/ShareSheet.swift`)

---

## Correções pós-teste (Parte 1)

Registadas ao compilar e correr os testes depois de fechar a Parte 1. Ciclo compilar → testar → corrigir repetido até `xcodebuild build` e `xcodebuild test` passarem nos dois alvos.

- [x] **Referências mortas a `.md` no `project.pbxproj`** — `Sales_Project.xcodeproj/project.pbxproj`: `Docs/architecture/SYSTEM_DESIGN.md`, `Docs/features/FEATURE_LOW_STOCK_SHARING.md`, `Docs/features/FEATURE_PROXIMITY.md` e `Docs/features/PROXIMITY_WAITING_LIST.md` estavam na fase *Resources* com caminho em `Views/`, mas os ficheiros vivem em `Docs/`. O build completo falhava com `No such file or directory`. Referências removidas (documentação não é recurso da app).
- [x] **Ficheiros novos por registar no alvo** — `Sales_Project.xcodeproj/project.pbxproj`: o alvo `Sales_Project` usa lista explícita de ficheiros (não pasta sincronizada). Acrescentados `Models/Batch.swift`, `Models/Category.swift`, `Models/ExpiryStatus.swift`, `Utils/CSVField.swift`, `ViewModels/BatchViewModel.swift`, `ViewModels/CategoryViewModel.swift` ao alvo da app, `Utils/CSVField.swift` também ao alvo `List_Storage` (o `ProximityManager` usa `csvField`), e os 9 ficheiros de teste novos ao alvo `POSAppTests`.
- [x] **Alvo de testes sem scheme nem plataforma correcta** — `Sales_Project.xcodeproj/xcshareddata/xcschemes/Sales_Project.xcscheme` + `project.pbxproj`: `POSAppTests` não estava em nenhum `Testables` (nunca corria) e tinha `SDKROOT = iphoneos` / `IPHONEOS_DEPLOYMENT_TARGET = 16.0`, incompatível com a app multiplataforma. Passou a `SDKROOT = auto`, alvos 26.0, e foi acrescentado ao scheme.
- [x] **`POSAppTests/ProximityTests.swift` não compilava** (já antes desta ronda): faltava `import Network` e o argumento `priceFinal` em 5 chamadas a `Product(...)`. Corrigido.
- [x] **`illegal multi-threaded access to database connection`** — `Database/DatabaseManager.swift`: `sqlite3_open` abria a ligação sem mutex e os testes rebentavam a app. Passou a `sqlite3_open_v2` com `SQLITE_OPEN_FULLMUTEX` (modo serializado). Corrige também o acesso à BD a partir das filas de rede da proximidade.
- [x] **Testes em paralelo a partilhar o singleton `DatabaseManager`** — `Sales_Project.xctestplan` (novo) + scheme: transações `BEGIN IMMEDIATE` concorrentes na mesma ligação e `currentUser` pisado entre suites davam 12 falhas. Test plan com `parallelizable: false`.
- [x] **S5 sem UI (transferência nunca completava)** — `List_Storage/ProximityReceiverView.swift`: mostra o `pairingCode` e apresenta "Aceitar / Recusar" quando há `pendingPeerName`, com Liquid Glass e transições animadas. `Views/Products/LowStockView.swift`: campo de 6 dígitos no `DevicePickerSheet`, dispositivos só seleccionáveis com código válido, `sendStockData(..., code:)` passa o código.
- [x] **Quadro da secção 9 do `Docs/security/SECURITY.md`** — S1, S2, S3, S4, S10, S11, S12, S13 e S15 marcados `[x]`; notas de S5 e S12 reescritas para o estado real.

**Resultado final:** `xcodebuild build` OK no alvo `Sales_Project` (macOS) e no alvo `List_Storage` (iOS); `xcodebuild test` — 64 testes em 15 suites, todos a passar.

---

# PARTE 2 — FRONTEND

Só arrancar depois da Parte 1 compilar e os testes passarem.

## 2.1 — Gestão de categorias

### `Views/Products/CategoryManagerView.swift` (novo)
- [x] Lista de categorias com ícone + cor + nome, swipe/menu para editar e apagar
- [x] Botão "Nova categoria" abre `CategoryFormView`
- [x] Aviso ao apagar: "Os X produtos desta categoria ficam sem categoria."

### `Views/Products/CategoryFormView.swift` (novo)
- [x] Campos: nome, seletor de ícone, seletor de cor
- [x] Grelha de ~30 SF Symbols pré-selecionados (comida, bebida, limpeza, higiene, ferramentas, papelaria...) em `Utils/CategoryIcons.swift` — grelha simples, **não** um browser de todos os SF Symbols
- [x] Cores: paleta fixa de 10 swatches (reutilizar tons de `AppTheme`)
- [x] Pré-visualização ao vivo do chip da categoria

### `Views/Products/ProductListView.swift`
- [x] Coluna/chip de categoria em cada linha, com o ícone e cor próprios
- [x] Barra de filtro por categoria no topo (chips scrolláveis: "Todos" + cada categoria)
- [x] Entrada para `CategoryManagerView` (botão na toolbar)

## 2.2 — Vendas: grelha de cards quadrados

### `Views/Sales/SaleView.swift`
- [x] Substituir `List(filteredProducts)` por `ScrollView` + `LazyVGrid(columns: [GridItem(.adaptive(minimum: 150), spacing: 12)])`
- [x] Barra de filtro por categoria acima da grelha: chips horizontais "Todos" + categorias, chip ativo usa a cor da categoria
- [x] Filtro combinado: `searchText` **E** categoria selecionada, com `.animation(.easeInOut, value: filteredProducts.count)` para os cards se reorganizarem suavemente ao escrever
- [x] Contador de resultados já existe — manter, mostrar também quando há filtro de categoria ativo

### `Views/Sales/ProductCardView.swift` (novo — extrair de `ProductSaleRowView`)
- [x] Card quadrado (`aspectRatio(1, contentMode: .fit)`), ordem vertical:
  1. Ícone da categoria em círculo colorido (fallback `cube.fill` cinzento se sem categoria)
  2. Nome (2 linhas máx)
  3. Preço final a destaque
  4. Badge de stock (verde/laranja/vermelho — regra já existente em `ProductSaleRowView`)
  5. Badge de validade se o lote mais próximo não for `.safe/.none`
  6. Stepper compacto (−/qty/+) + botão "Adicionar"
- [x] `stock == 0`: card a 40% de opacidade, stepper e botão desativados (comportamento já existente)
- [x] Apagar `ProductSaleRowView` depois de migrado — não deixar as duas versões

## 2.3 — Alerta de validade no arranque

### `Views/Products/ExpiryAlertView.swift` (novo)
- [x] Sheet apresentado por `Views/MainView.swift` no `.onAppear`, condicionado a `shouldShowExpiryAlert()`
- [x] Secções por faixa, da mais grave para a menos: Já expirado · Expira em dias · 1 mês · 2 meses · 3 meses
- [x] Cada linha: nome do produto, quantidade do lote, data de validade, valor em risco desse lote
- [x] Cabeçalho com o total: "Perda real: X MT · Em risco: Y MT"
- [x] Botões: "Ver produtos" (fecha e vai ao separador Produtos) e "Dispensar hoje"

### `Views/MainView.swift`
- [x] Badge vermelho com a contagem no item Produtos da sidebar (macOS) e do `TabView` (iOS) — permanente enquanto houver lotes fora de `.safe/.none`

## 2.4 — Painel de perdas em Produtos

### `Views/Products/ProductListView.swift`
- [x] Duas cards no topo:
  - **Perda real** (vermelho) — soma dos lotes expirados × preço base
  - **Em risco** (laranja) — soma dos lotes a expirar × preço base
- [x] Tocar em "Em risco" expande o breakdown por faixa (dias / 1m / 2m / 3m)
- [x] Deixar explícito no rodapé da card: "Calculado com o preço base de cada lote."

## 2.5 — Wizard de produto (2 passos)

### `Views/Products/ProductFormView.swift` — reescrever o layout
- [x] Janela larga: `.frame(minWidth: 720, idealWidth: 820, minHeight: 560)` na sheet (macOS). Objetivo: zero scroll.
- [x] Indicador de progresso no topo: `① Identificação —— ② Preços & Stock`, passo concluído clicável para voltar
- [x] **Passo 1 — Identificação**: nome, código de barras (+ scanner, já existe), seletor de categoria (chips com ícone). "Seguinte" desativado enquanto o nome estiver vazio.
- [x] **Passo 2 — Preços, stock e lote**: preço base, IVA, margem, resumo do preço final (já existe a lógica), quantidade, data de validade (`DatePicker`, nativo) e opção "Não expira"
- [x] Rodapé fixo: "Voltar" · "Cancelar" · "Guardar" (só ativo no passo 2 com `canSave`)
- [x] Em modo `.edit`: mostrar a lista de lotes existentes no passo 2, editáveis, com botão "Adicionar lote"
- [x] Em modo `.create`: guardar cria o produto **e** o primeiro lote

## 2.6 — Relatórios: popout de exportação

### `Views/Reports/DailyReportView.swift` e `MonthlyReportView.swift`
- [x] Botão "Exportar" na toolbar abre `Menu`/popover com duas opções: **CSV** e **PDF**
- [x] Exporta direto pelo `ReportService`, mostra um toast de sucesso com o caminho e revela no Finder (macOS) / abre `ShareSheet` (iOS)
- [x] Estado de progresso enquanto o PDF renderiza (é `async`)

## 2.7 — Liquid Glass nos Relatórios

⚠️ Confirmar o deployment target no `.xcodeproj` **antes** de escrever código: `.glassEffect()` exige macOS 26 / iOS 26. Se o target for inferior, o build parte — decidir aí entre subir o target ou usar `#available`.

### `Views/Reports/ReportComponents.swift`
- [x] Substituir os fundos de card por `.glassEffect(.regular, in: .rect(cornerRadius: 16))`
- [x] Agrupar cards relacionados em `GlassEffectContainer` (necessário para o efeito de fusão entre elementos próximos)
- [x] Botões de exportação e chips de período: `.buttonStyle(.glass)`
- [x] Cabeçalho de totais: glass sobre um gradiente de marca (`AppTheme.accent`)
- [x] Não aplicar glass sobre glass — um único plano de vidro por secção, senão fica lamacento
- [x] Verificar contraste do texto sobre vidro em modo claro **e** escuro

---

## Correções pós-teste (Parte 2)

Registadas ao compilar e correr os testes depois de fechar a Parte 2. Ciclo compilar → testar → corrigir repetido até `xcodebuild build` e `xcodebuild test` passarem nos dois alvos.

- [x] **IDs de objeto duplicados no `project.pbxproj`** — `Sales_Project.xcodeproj/project.pbxproj`: os cinco ficheiros novos da Parte 2 foram registados com IDs `BB2222220000000000000020`–`0029`, que já pertenciam aos ficheiros de teste da Parte 1 (`FIFOTests`, `PasswordHashTests`, `SQLInjectionTests`, `TransactionTests`, …). O Xcode passou a resolver os testes contra o grupo errado e o build falhava com `Build input files cannot be found: .../Views/Sales/SQLInjectionTests.swift`. Renumerados para `BB2222220000000000000050`–`0059`.
- [x] **`ReportComponents.swift` sem `import Combine`** — `Views/Reports/ReportComponents.swift`: o `ReportExportState` novo é `ObservableObject` com `@Published`, e o ficheiro só importava SwiftUI: `type 'ReportExportState' does not conform to protocol 'ObservableObject'` + 30 erros de `missing import of defining module 'Combine'`. Acrescentado `internal import Combine`, o mesmo padrão dos ViewModels.
- [x] **Três chips de categoria diferentes** — os dois agentes criaram, em paralelo, `CategoryChipView` (`CategoryManagerView.swift`), `SaleCategoryChip` (`SaleView.swift`) e `FormCategoryChip` (`ProductFormView.swift`), com aspetos divergentes para o mesmo elemento. Contra a regra de reutilização do `CLAUDE.md` §7. Consolidados num único `CategoryChipView` em `Utils/AppTheme.swift` (com `showsCheckmark` para as grelhas de seleção); os dois privados foram apagados e as chamadas passaram a envolvê-lo num `Button`. Efeito secundário: desaparecem os literais `.white` que as versões com preenchimento saturado obrigavam.
- [x] **Código morto em `ReportComponents.swift`** — `ExportButton` e `SummaryCardView` ficaram sem utilizadores depois de a exportação passar para o `Menu` da toolbar. Apagados.
- [x] **Registo dos ficheiros novos nos alvos** — `Sales_Project.xcodeproj/project.pbxproj`: o alvo usa lista explícita de ficheiros. Acrescentados `Utils/CategoryIcons.swift`, `Views/Products/CategoryManagerView.swift`, `Views/Products/CategoryFormView.swift`, `Views/Products/ExpiryAlertView.swift` e `Views/Sales/ProductCardView.swift`.

**Resultado final:** `xcodebuild build` OK no alvo `Sales_Project` (macOS) e no alvo `List_Storage` (iOS); `xcodebuild test` — 64 testes em 15 suites, todos a passar.

### Dívida deixada em aberto (não bloqueia)

- `Sales_Project/Sales_ProjectApp.swift` (ponto de entrada legado, `@main` comentado) chama `MainView()` sem injectar `CategoryViewModel`/`BatchViewModel` — compila, mas rebentava em runtime se alguém reativasse o `@main`. Já consta da secção "Dívida arquitetural conhecida" do `Docs/architecture/ARCHITECTURE.md`, ponto 1.
- Liquid Glass ainda não chegou a Fecho de Caixa, Definições, Login e Pagamento.

---

## Ordem de trabalho sugerida

0. 1.0 Fundações — segurança (1.0.1) e diagrama do sistema (1.0.2). Bloqueia tudo o resto.
1. 1.1 Categorias (backend) → 2.1 UI de categorias — entrega fechada, testável sozinha
2. 1.2 + 1.3 Lotes e FIFO — a parte de risco; commit isolado, testes a passar antes de seguir
3. 1.4 + 2.3 + 2.4 Alertas e perdas
4. 2.2 Cards de venda + filtro
5. 2.5 Wizard de produto
6. 1.5 + 2.6 Exportação de relatórios
7. 2.7 Liquid Glass (só depois de confirmar o target de OS)

## Fora de âmbito (não fazer sem pedido)

- Fotos de produto nos cards
- Alertas por notificação do sistema
- Histórico de lotes descartados / registo de quebras
- Sincronização na nuvem

---

## 2026-08-15 — Relatório anual, cards de factura e correcção do texto invertido nos PDF
	
# PARTE 1 — BACKEND

## 1.1 Relatório anual + correcção do PDF

- [x] 1.1.1 Acrescentar `case annual = "annual"` (e `label`) ao `ReportType` — `Models/Report.swift`
- [x] 1.1.2 `fetchSalesByYear(year:)` com `LIKE 'AAAA-%'` (prefixo, não `%…%`) — `Database/DatabaseManager.swift`
- [x] 1.1.3 `annualSales`, `loadAnnualSales(date:)` e `salesByMonth(for:)` — `Views/Reports/ReportViewModel.swift`
- [x] 1.1.4 `exportAnnualCSV(sales:date:)` e `exportAnnualPDF(sales:date:)` — `Views/Reports/ReportService.swift`
- [x] 1.1.5 **Corrigir texto invertido no PDF**: `drawText` aplicava `scaleBy(y: -1)` mas criava `NSGraphicsContext(flipped: false)` — o glifo saía espelhado na vertical. Removido o flip manual; `NSGraphicsContext.current` passa a ser guardado e reposto — `Views/Reports/ReportService.swift`

# PARTE 2 — FRONTEND

## 2.1 Um só botão de partilha por secção

- [x] 2.1.1 Em macOS o `TabView` instanciava as três vistas em simultâneo dentro do mesmo `NavigationStack`, e os `.toolbar` de Diário e Mensal fundiam-se na mesma barra. macOS e iOS unificados no `ReportsHomeView` (picker segmentado, só a secção activa existe) — `Views/MainView.swift`

## 2.2 Separador Anual

- [x] 2.2.1 Nova vista com selector de ano, cards de resumo, top produto, barras por mês e grelha de vendas — `Views/Reports/AnnualReportView.swift`
- [x] 2.2.2 Acrescentar "Anual" ao selector de secções — `Views/MainView.swift`
- [x] 2.2.3 Selector de ano reutilizável `YearSelectorHeader` — `Views/Reports/ReportComponents.swift`
- [x] 2.2.4 Filtro "Anuais" e etiqueta do tipo a partir de `ReportType.label` — `Views/Reports/ReportHistoryView.swift`

## 2.3 Facturas anteriores em cards quadrados

- [x] 2.3.1 Linha expansível convertida em card quadrado (`aspectRatio(1)`, vidro, detalhe em sheet `SaleGroupDetailView` com CSV/PDF) — `Views/Reports/SaleReportRowView.swift`
- [x] 2.3.2 Cards em `LazyVGrid` adaptativa (`SaleCardsGrid`) com animação de inserção e respeito por Reduce Motion; `groupSales` duplicado nas Views passou a `groupSalesByClient` partilhado — `Views/Reports/ReportComponents.swift`, `DailyReportView.swift`, `MonthlyReportView.swift`, `AnnualReportView.swift`

# PARTE 3 — DOCUMENTAÇÃO

- [x] 3.1 Funcionalidade "Relatório Anual", cards quadrados e árvore com `AnnualReportView.swift` — `README.md`
- [x] 3.2 `fetchSalesByYear` e o valor `annual` da coluna `Reports.type` — `Docs/database/DATABASE.md`
- [x] 3.3 `ReportsHomeView` como ponto único de navegação dos relatórios; `loadAnnualSales`; regra do `drawText` sem flip — `Docs/architecture/ARCHITECTURE.md`
- [x] 3.4 `stateDiagram-v2` das secções + `flowchart` de exportação com a via anual e o `drawText` — `Docs/architecture/SYSTEM_DESIGN.md`
- [x] 3.5 Sem `.md` novo criado — índice sem alteração — `Docs/DOCUMENTATION.md`

## Correções pós-teste

- [x] P1 `subscript(safe:)` só existe no alvo `List_Storage`, não no `Sales_Project` — `salesByMonth` deixou de indexar `shortMonthSymbols` e passa a derivar o nome do mês da própria data da venda — `Views/Reports/ReportViewModel.swift`
- [x] P2 `Views/` não é um grupo sincronizado do Xcode — `AnnualReportView.swift` teve de ser registado à mão (`PBXFileReference`, `PBXBuildFile`, grupo `Reports`, fase `Sources`) — `Sales_Project.xcodeproj/project.pbxproj`
- [x] P3 Teste do PDF: `page.thumbnail` devolve `NSCGImageSnapshotRep`, não `NSBitmapImageRep` — bitmap passou a ser construído a partir de `tiffRepresentation` — `POSAppTests/FilenameSanitizationTests.swift`
- [x] P4 Teste do PDF: a primeira versão comparava a posição da linha e passava na mesma com o bug (o flip mantinha a linha na mesma banda, só virava cada glifo). Passou a desenhar "TTTT" e a comparar o peso da tinta na metade superior vs inferior da mancha — verificado por mutação: falha com o `scaleBy(y: -1)` reposto, passa sem ele — `POSAppTests/FilenameSanitizationTests.swift`


---

## 2026-08-15 — Histórico de relatórios pesquisável, Fecho do Ano, Definições redesenhadas (+ wizard) e Guia actualizado

Ciclo: Histórico de relatórios pesquisável, Fecho do Ano, redesenho de Definições
(+ wizard de utilizador) e redesenho/actualização do Guia.

---

# PARTE 1 — BACKEND

- [x] **1.1 — `Database/DatabaseManager.swift`**: `deleteReport(id: Int) -> Bool`
      (`DELETE FROM Reports WHERE id = ?`, com `sqlite3_bind_int`). Hoje o
      histórico só apaga o ficheiro e deixa a linha órfã na base de dados.
- [x] **1.2 — `Views/Reports/ReportViewModel.swift`**: filtro do histórico —
      `enum ReportSearchScope { all, day, month, year }` e
      `static func filterReports(_:scope:date:type:) -> [Report]` (função pura,
      compara o prefixo de `Report.period`).
- [x] **1.3 — `Views/DayClose/DayCloseView.swift` (`DayCloseViewModel`)**:
      `yearSummary`, `loadYear(year:)`, `exportYearExcel(date:)`,
      `exportYearPDF(date:)` — reutiliza `fetchSalesByYear` +
      `fetchPaymentsByDate` e `CloseExportService`.
- [x] **1.4 — `POSAppTests/`**: teste do filtro do histórico (1.2) —
      `ReportFilterTests.swift`.

---

# PARTE 2 — FRONTEND

- [x] **2.1 — `Views/Reports/ReportHistoryView.swift`**: pesquisa por Dia / Mês /
      Ano (segmented + selector de data) sobre o filtro de tipo existente;
      resultados listados abaixo, com animação e estado vazio; apagar usa
      `deleteReport` (1.1).
- [x] **2.2 — `Views/DayClose/DayCloseView.swift`**: separador **Fecho do Ano**
      (macOS `TabView` + picker iOS) com `YearCloseTabView` — resumo por método,
      gráfico de distribuição e exportação Excel/PDF (só Admin).
- [x] **2.3 — `Views/Settings/SettingsView.swift`**: redesenho UI/UX — cartões
      com `glassEffect`, cabeçalhos de secção, linha de utilizador com acções
      claras (editar/apagar), animações de estado e mensagens de sucesso.
- [x] **2.4 — `Views/Settings/UserFormView.swift`**: formulário em **wizard**
      (Dados → Segurança → Função → Revisão) com barra de progresso, validação
      por passo e navegação Anterior/Seguinte.
- [x] **2.5 — `Views/Posguideview.swift`**: redesenho de todo o painel do Guia
      (sidebar com secções agrupadas, cabeçalho, pesquisa) e **actualização do
      conteúdo** dos capítulos Relatórios (Diário/Mensal/Anual/Histórico
      pesquisável), Fecho (Dia/Mês/Ano, nova sessão, exportação) e Produtos
      (categorias, lotes/FIFO, validades, stock baixo, código de barras).

---

# PARTE 3 — DOCUMENTAÇÃO

- [x] **3.1 — `README.md`**: funcionalidades + árvore da estrutura.
- [x] **3.2 — `Docs/architecture/ARCHITECTURE.md`**: `DayCloseViewModel`
      (fecho anual) e filtro do histórico no `ReportViewModel`.
- [x] **3.3 — `Docs/architecture/SYSTEM_DESIGN.md`**: diagramas Mermaid dos
      fluxos alterados (fecho anual, histórico pesquisável, wizard de utilizador).
- [x] **3.4 — `Docs/database/DATABASE.md`**: query `deleteReport` na tabela
      `Reports`.

---

## Correções pós-teste

- [x] `Views/Reports/ReportHistoryView.swift` + `Database/DatabaseManager.swift` —
      apagar um relatório do histórico só removia o ficheiro e deixava a linha
      órfã em `Reports` (reaparecia como "Ficheiro não encontrado"). Passa a
      chamar `deleteReport(id:)`.
- [x] `Utils/Constants.swift` + `Views/Settings/SettingsView.swift` — a versão
      da app estava escrita à mão ("1.1.0"); passa a `Constants.appVersion`
      lido do bundle.
- [x] `Sales_Project.xcodeproj/project.pbxproj` — o alvo `POSAppTests` usa
      referências explícitas, por isso `ReportFilterTests.swift` não corria.
      Adicionado ao grupo e à fase Sources (72 testes, 17 suites, tudo a passar).

## Nota de fecho

Verificado: `xcodebuild` compila o alvo macOS sem erros e a suite passa
(72 testes, 17 suites). A app arranca até ao ecrã de login sem crash.
A passagem pelos ecrãs autenticados (histórico pesquisável, Fecho do Ano,
Definições, wizard de utilizador, Guia) fica do lado do utilizador — precisa
das credenciais de Admin.

---

## 2026-08-16 — Impressão de facturas (80 mm/A4), redesenho de painéis e novos gráficos

Ciclo: impressão de facturas (80 mm / A4), redesenho de painéis (Pagamento,
Factura, Produtos, Histórico, Fecho de Caixa) e novos gráficos/top de produtos
nos Relatórios.

---

# PARTE 1 — BACKEND

## 1.1 — Serviço de impressão (`Views/Sales/ReceiptPrintService.swift`) — novo ficheiro
- [x] Criar `enum ReceiptFormat: String, CaseIterable` com `.thermal80` (80 mm) e `.a4`, com `label`, `icon` e `pageWidth` em pontos (80 mm = 226.77 pt; A4 = 595 pt).
- [x] Criar `final class ReceiptPrintService` com `func makeReceiptPDF(sales:[Sale], payments:[Payment], format:ReceiptFormat) -> URL?` — desenha o talão em CoreGraphics/CoreText, largura conforme o formato, altura de página A4 fixa e talão contínuo no formato 80 mm.
- [x] Conteúdo do talão: nome da app, nº de factura, data/hora, cliente + NIF (se existirem), tabela de artigos (qtd × preço = subtotal), total, métodos de pagamento e rodapé.
- [x] `func printPDF(at url: URL) -> Bool` — macOS: `PDFDocument.printOperation(for:scalingMode:autoRotate:)` + `NSPrintPanel` (escolha de impressora nativa); iOS: `UIPrintInteractionController`. Sem caminhos escritos à mão — ficheiros só na directoria de relatórios da app.
- [x] Validar entradas: lista de vendas vazia devolve `nil`, nunca escreve ficheiro.

## 1.2 — Testes do serviço de impressão (`POSAppTests/ReceiptPrintTests.swift`) — novo ficheiro
- [x] Testar `ReceiptFormat.pageWidth` (80 mm ≈ 226.77 pt, A4 = 595 pt).
- [x] Testar que `makeReceiptPDF` devolve `nil` com vendas vazias.
- [x] Testar que `makeReceiptPDF` gera ficheiro não vazio para uma venda com itens, nos dois formatos.

## 1.3 — Top de produtos vendidos (`Views/Reports/ReportViewModel.swift`)
- [x] Criar `struct TopProductEntry: Identifiable` (nome, quantidade, total).
- [x] Criar `func topProducts(for sales: [Sale], limit: Int = 50) -> [TopProductEntry]` — agrega por nome, soma quantidade e subtotal, ordena por quantidade desc.
- [x] Manter `topProduct(for:)` como derivado do novo método (uma só fonte de verdade).

## 1.4 — Séries para gráficos (`Views/Reports/ReportViewModel.swift`)
- [x] `func salesCountByMonth(for:) -> [(month: String, count: Int)]`.
- [x] `func itemsByMonth(for:) -> [(month: String, items: Int)]`.
- [x] `func salesCountByDay(for:) -> [(day: String, count: Int)]` e `func itemsByDay(for:) -> [(day: String, items: Int)]` para a secção mensal.

## 1.5 — Detalhe de risco por produto (`ViewModels/BatchViewModel.swift`)
- [x] `struct ProductRiskEntry: Identifiable` (productId, nome, lotes em risco, quantidade total, valor total).
- [x] `func riskEntries(products: [Product]) -> [ProductRiskEntry]` — só lotes `isAlerting`, ordenado por valor desc.
- [x] `func worstStatus(productId: Int) -> ExpiryStatus?` — faixa mais grave dos lotes de um produto (badge de estado na lista de Produtos).

## 1.6 — Testes de agregação (`POSAppTests/ReportFilterTests.swift`)
- [x] Testar `topProducts` (ordem, soma de quantidades, limite).
- [x] Testar `riskEntries` (só lotes em alerta, totais correctos).

---

# PARTE 2 — FRONTEND

## 2.1 — Selector de formato + impressão (`Views/Sales/PrintFormatSheet.swift`) — novo ficheiro
- [x] `struct PrintFormatSheet` reutilizável: escolha 80 mm / A4 em cartões de vidro, botão "Imprimir" que gera o PDF e abre o painel de impressão do sistema (escolha de impressora).
- [x] Estados de carregamento e erro; animação de selecção; respeita `Reduce Motion`.

## 2.2 — Factura da venda (`Views/Sales/InvoiceView.swift`)
- [x] Acrescentar botão "Imprimir" ao lado de "Partilhar PDF".
- [x] "Imprimir" abre a `PrintFormatSheet` (80 mm / A4 → impressora).

## 2.3 — Painel de Pagamento (`Views/Sales/PaymentView.swift`)
- [x] Redesenhar UI/UX: cabeçalho de total em vidro, grelha de métodos com `GlassEffectContainer`, campo de valor com teclado rápido de atalhos, lista de pagamentos animada, resumo fixo no fundo.
- [x] Animar todas as mudanças de estado; respeitar `Reduce Motion`; contraste em claro/escuro.

## 2.4 — Detalhe de factura nos Relatórios (`Views/Reports/SaleReportRowView.swift`)
- [x] Redesenhar o painel de detalhe (cabeçalho, artigos, total em destaque).
- [x] Acrescentar botão "Reimprimir" com escolha 80 mm / A4 e painel de impressora (`PrintFormatSheet`).

## 2.5 — Painel de risco de validade (`Views/Products/ProductListView.swift`)
- [x] Clicar em "Em risco" abre painel lateral direito com produtos em risco: nome, lotes, quantidades, valor por produto e total geral.
- [x] Clicar num produto do painel abre o formulário de edição do produto.
- [x] Transição animada de entrada/saída do painel.

## 2.6 — Stock baixo ao lado dos painéis (`Views/Products/ProductListView.swift`)
- [x] Mover o aviso de stock baixo para a mesma linha de "Perda real" e "Em risco" (terceiro cartão, clicável).

## 2.7 — Lista de produtos (`Views/Products/ProductListView.swift`)
- [x] Redesenhar a linha de produto (`ProductRowView`) e acrescentar badge de estado do lote mais grave (validade) quando existir problema.

## 2.8 — Top 50 e layout do Diário (`Views/Reports/DailyReportView.swift`, `Views/Reports/ReportComponents.swift`)
- [x] Novo `TopProductsPanel` (lista dos 50 mais vendidos com quantidade e total, scroll interno).
- [x] Layout: coluna esquerda com Total do Dia + Vendas/Itens; coluna direita com o `TopProductsPanel` a ocupar a altura das duas linhas.

## 2.9 — Mesmo layout no Mensal e Anual (`Views/Reports/MonthlyReportView.swift`, `Views/Reports/AnnualReportView.swift`)
- [x] Aplicar o mesmo layout de duas colunas com o `TopProductsPanel`.

## 2.10 — Novos gráficos (`Views/Reports/ReportComponents.swift`, Mensal e Anual)
- [x] Componente de barras verticais reutilizável (`VerticalBarsCard`) com Swift Charts.
- [x] Mensal: gráficos de nº de vendas e de itens vendidos por dia.
- [x] Anual: gráficos de nº de vendas e de itens vendidos por mês.

## 2.11 — Gráfico anual na vertical (`Views/Reports/AnnualReportView.swift`)
- [x] Converter `MonthlyBreakdownCard` de barras horizontais para barras verticais.

## 2.12 — Histórico de relatórios (`Views/Reports/ReportHistoryView.swift`)
- [x] Remover o filtro "Tipo".
- [x] Redesenhar em duas colunas: painel de pesquisa/filtros à esquerda, lista de relatórios à direita.

## 2.13 — Fecho de Caixa (`Views/DayClose/DayCloseView.swift`)
- [x] Redesenhar o Fecho do Dia: cartões à esquerda, gráfico à direita.
- [x] `AnimatedBreakdownChart` de barras horizontais para verticais.
- [x] Mesmo layout no Fecho do Mês e Fecho do Ano (incluindo gráfico no Fecho do Dia).

## 2.14 — Documentação
- [x] `README.md` — funcionalidades novas (impressão 80 mm/A4, painel de risco, top 50) e árvore de ficheiros.
- [x] `Docs/architecture/ARCHITECTURE.md` — `ReceiptPrintService` e novos métodos de ViewModel.
- [x] `Docs/architecture/SYSTEM_DESIGN.md` — fluxo de impressão em Mermaid.
- [x] `Docs/DOCUMENTATION.md` — índice (sem ficheiros `.md` novos, confirmar).
- [x] `Docs/database/DATABASE.md` — sem alterações de esquema (confirmar e registar).

---

## Correções pós-teste

- [x] `Views/Sales/ReceiptPrintService.swift` — `NSPrintInfo(dictionary:)` não aceita o `NSMutableDictionary` de `NSPrintInfo.shared.dictionary()`; passou a fazer-se `as? [NSPrintInfo.AttributeKey: Any]` com `[:]` por omissão.
- [x] `Views/Sales/ReceiptPrintService.swift` — os pagamentos eram filtrados por `saleId == sale.id || saleId == 0`, o que repetia as linhas de pagamento em cada factura ao imprimir um grupo; filtra-se só pela venda.
- [x] `Views/Sales/PrintFormatSheet.swift` — o método chamava-se `print()` e sombreava o `print` da stdlib; renomeado para `startPrinting()`.
- [x] `Views/Products/ProductListView.swift` — `\(valor, specifier:)` só funciona em interpolação de `Text`, não num parâmetro `String`; IVA e margem passaram a usar `formatted(.number.precision(.fractionLength(0)))`.
- [x] `Views/Reports/AnnualReportView.swift` — `MonthlyBreakdownCard` (barras horizontais) ficou sem uso depois da conversão para vertical; removido em vez de ficar código morto.
- [x] Verificação prática do talão: PDFs gerados nos dois formatos e inspeccionados — texto direito (sem espelhamento), colunas alinhadas, talão 80 mm contínuo e A4 paginado. Ficheiros de teste apagados no fim.

---

## 2026-08-16 — Gráficos do fecho a toda a altura e partilha na fatura

# PARTE 1 — BACKEND

Nada nesta ronda (só layout de UI).

# PARTE 2 — FRONTEND

- [x] 2.1 `Views/Reports/ReportComponents.swift` — `VerticalBarsCard.height` passa a `CGFloat?`; quando `nil`, o gráfico estica (`maxHeight: .infinity`) em vez de altura fixa. Restantes chamadas ficam iguais.
- [x] 2.2 `Views/DayClose/DayCloseView.swift` — `CloseSummarySection` passa de `HStack` para `Grid`/`GridRow` para o cartão do gráfico ocupar toda a altura da coluna dos cartões (Fecho do Dia / Mês / Ano). `AnimatedBreakdownChart` deixa de fixar 250.
- [x] 2.3 `Views/Sales/InvoiceView.swift` — botão de partilha da fatura não aparecia no macOS (dois `ToolbarItem` com `.confirmationAction`). Juntos Partilhar + Imprimir num só `ToolbarItem`, mantendo Fechar e Imprimir.

## Correções pós-teste

- [x] `Views/DayClose/DayCloseView.swift` — com `HStack` o filho flexível não estica (dentro de `ScrollView` a proposta de altura é `nil`); confirmado por teste de render offscreen que só o `Grid` propõe a altura da linha à célula. Layout mudado para `Grid`.
- [x] Compilação (`xcodebuild ... build`) e testes (`** TEST SUCCEEDED **`) a passar.

---

## 2026-08-16 — Nome do programa configurável, cards de venda maiores, stepper no carrinho, documentos e layout do fecho

# PARTE 1 — BACKEND

- [x] 1.1 `Utils/Constants.swift` — `appName` deixa de ser constante: lê/escreve `UserDefaults` (chave `Constants.appNameKey`), com `sanitizedAppName` (trim, sem quebras de linha, máx. 40 caracteres) e fallback para `"POS App"`.
- [x] 1.2 `ViewModels/SaleViewModel.swift` — `updateQuantity(productId:newQuantity:)`: valida contra `availableStock` (lotes), remove a linha a zero, recalcula o subtotal. `Models/SaleItem.swift` passa a `Equatable` para a lista do carrinho animar.
- [x] 1.3 `Utils/CSVField.swift` — `csvNumber(_:)` (número cru, ponto decimal, 2 casas) e `csvBOM` (BOM UTF-8).
- [x] 1.4 `Views/Reports/CloseExportService.swift` — CSV: BOM, todos os campos de texto por `csvField` (um cliente "Silva, Lda" partia a linha), valores monetários numéricos, nova coluna "Nº Itens"; PDF: cabeçalho da tabela repetido em cada página nova e rodapé com origem + "Página N".
- [x] 1.5 `Views/Reports/ReportService.swift` — CSV: BOM e valores monetários numéricos (Excel passa a somar as colunas), linha TOTAL com total de itens; PDF: rodapé com numeração em todas as páginas, coluna "Total Venda" (saía sempre vazia) removida, moeda no cabeçalho das colunas, `drawTableHeader()` morto apagado.
- [x] 1.6 `POSAppTests/CSVEscapingTests.swift` — testes de `csvNumber`, do `csvBOM` e da validação do nome do programa.

# PARTE 2 — FRONTEND

- [x] 2.1 `Views/Settings/SettingsView.swift` — `AppNameRow` na secção Aplicação: campo de texto, botão de gravar que só aparece quando o valor muda, toast de confirmação.
- [x] 2.2 `Views/LoginView.swift` e `Views/MainView.swift` — `@AppStorage(Constants.appNameKey)`; o nome muda no login e no título sem reiniciar a app.
- [x] 2.3 `Views/Sales/ProductCardView.swift` — cards maiores: fora o `aspectRatio(1)` (era ele que os esmagava), `minHeight: 250`, ícone 46, nome 16, preço 19, badges e stepper com área de toque maior.
- [x] 2.4 `Views/Sales/SaleView.swift` — grelha com coluna mínima 200 (era 150); `CartItemRowView` com stepper −/+ ligado a `updateQuantity`, com `contentTransition(.numericText())` e animação da lista.
- [x] 2.5 `Views/DayClose/DayCloseView.swift` — `CloseSummarySection` ganha `chartHeight` e um slot `below` na coluna direita: o Fecho do Dia mete as Notas por baixo do gráfico (o espaço que estava vazio), Mês e Ano deixam o gráfico esticar até ao fundo dos cartões.

# PARTE 3 — DOCUMENTAÇÃO

- [x] 3.1 `README.md` — nome do programa configurável, stepper do carrinho, cards maiores, layout do fecho e melhorias de CSV/PDF; árvore actualizada.
- [x] 3.2 `Docs/architecture/ARCHITECTURE.md` — `SaleViewModel.updateQuantity`, `Constants.appName`/`sanitizedAppName` e os helpers de CSV na tabela de regras.
- [x] 3.3 `Docs/architecture/SYSTEM_DESIGN.md` — fluxo de venda com o stepper do carrinho, diagrama do fecho com o slot da coluna direita e nova secção "Nome do Programa" (Mermaid).
- [x] 3.4 `Docs/architecture/TECHNICAL_DESIGN.md` — colunas reais do CSV, BOM, `csvNumber` e rodapé paginado do PDF. `Docs/DOCUMENTATION.md` sem alterações: nenhum `.md` criado, movido ou apagado.

## Correções pós-teste

- [x] `Views/Sales/SaleView.swift` — `.animation(value: cartItems)` obrigava `SaleItem: Equatable`; conformidade acrescentada em `Models/SaleItem.swift`.
- [x] `Views/Sales/SaleView.swift` — parâmetro `enabled` do `quantityButton` era sempre `true`; removido.
- [x] Compilação (`xcodebuild ... build` → `** BUILD SUCCEEDED **`) e testes (`** TEST SUCCEEDED **`, 87 testes em 20 suites, incluindo os 3 novos) a passar.
- [x] `Views/Reports/ReportService.swift` — **overlap no PDF**: o novo `startPage()` repunha `y` no topo depois de o cabeçalho (título, subtítulo, cards) já ter sido posicionado, e a tabela voltava a escrever por cima ("V POS" sobre "Venda #35 · Cliente anónimo", cards de resumo por baixo da tabela). `startPage()` deixa de mexer no `y` (só `newPage()` volta ao topo) e o cabeçalho passa a ser desenhado directamente depois de abrir a página — o buffer `lines`/`PDFLine`, que só existia para adiar esse desenho, foi apagado.
- [x] `POSAppTests/ReportFilterTests.swift` — suite "Layout do PDF de relatórios": gera o PDF por `exportGroupPDF` e falha se dois caracteres partilharem mais de 50% da área (PDFKit `characterBounds`). Confirmado por mutação: com o defeito reposto o teste acusa `[("V","V"), ("P","V"), ("P","n"), …]`.
- [x] `Docs/database/DATABASE.md` — o diagrama "Ciclo de uma Venda" não renderizava: fence ```` ```mermaid ```` a mais antes do texto de introdução, que engolia o bloco seguinte. Varridos todos os `.md` do projeto à procura do mesmo defeito — nenhum outro.
- [x] App lançada e verificada no arranque (ecrã de login com o nome do programa). Os ecrãs de Vendas e Fecho ficam por conferir com sessão iniciada — exigem credenciais do utilizador.

---

## 2026-08-16 — Validade a bloquear a venda, promoções, gráficos e painéis animados

# PARTE 1 — BACKEND

## 1.1 — Bloquear venda de produto expirado
- [x] `Database/DatabaseManager.swift`: novo `sellableStock(productId:)` — soma só dos lotes com `expiry_date IS NULL OR expiry_date >= hoje`.
- [x] `Database/DatabaseManager.swift`: `consumeStockFIFO(excludeExpired:)` deixa de consumir lotes expirados na venda (o ajuste manual de stock continua a poder escoá-los).
- [x] `Database/DatabaseManager.swift`: `createSaleAtomic` revalida com `sellableStock` e consome com `excludeExpired: true`.
- [x] `ViewModels/SaleViewModel.swift`: `addToCart` e `updateQuantity` usam `sellableStock`; mensagem "Produto expirado. Não pode ser vendido." quando só há lotes fora do prazo.
- [x] `POSAppTests/FIFOTests.swift`: lote expirado não conta para stock vendável, não é consumido, e o produto não entra no carrinho.

## 1.2 — Promoção/desconto por produto a expirar
- [x] `Database/DatabaseManager.swift`: migração `discount_percent REAL NOT NULL DEFAULT 0` em `Products` (`migrateAddDiscountToProducts`) + coluna nas queries de produto.
- [x] `Database/DatabaseManager.swift`: `setProductDiscount(productId:percent:)` — só Admin (S3), 0…90, com `logAudit("discount_changed")`.
- [x] `Models/Product.swift`: `discountPercent`, `priceWithDiscount` e `hasDiscount`.
- [x] `ViewModels/ProductViewModel.swift`: `applyDiscount(productId:percent:)` com validação 0…90.
- [x] `ViewModels/SaleViewModel.swift`: carrinho usa `priceWithDiscount`.
- [x] `POSAppTests/FIFOTests.swift`: desconto aplicado ao preço do carrinho e percentagem fora de gama rejeitada.

# PARTE 2 — FRONTEND

## 2.1 — Animação de crescimento dos gráficos (Relatórios + Fecho)
- [x] `Views/Reports/ReportComponents.swift`: `VerticalBarsCard` cresce de 0 até ao valor ao entrar na aba, com escala Y fixa; respeita Reduce Motion.

## 2.2 — Animação dos valores dos painéis (Relatórios + Fecho)
- [x] `Views/Reports/ReportComponents.swift`: `AnimatedValueText` (contagem interpolada via `Animatable`) + `formatCount`.
- [x] `Views/Reports/ReportComponents.swift`: `PrimaryMetricCard` e `SecondaryMetricCard` recebem `Double` e animam.
- [x] `Views/Reports/DailyReportView.swift`, `MonthlyReportView.swift`, `AnnualReportView.swift`: passam o total numérico ao `ReportSummaryHeader`.
- [x] `Views/DayClose/DayCloseView.swift`: total geral e cartões por método com valores animados.

## 2.3 — Liquid Glass nos painéis do Fecho de Caixa
- [x] `Views/DayClose/DayCloseView.swift`: total e grelha de métodos em `glassEffect` dentro de `GlassEffectContainer`, com a cor do método em gradiente **por baixo** do vidro.

## 2.4 — Definições: Utilizadores e Aplicação lado a lado
- [x] `Views/Settings/SettingsView.swift`: `ViewThatFits` — lado a lado com largura, empilhados em ecrã estreito; largura máxima 1080.

## 2.5 — Vendas: filtros maiores, "Todos" / "Filtrar"
- [x] `Views/Sales/SaleView.swift`: dois botões grandes de vidro; "Filtrar" revela as categorias lado a lado com transição de vidro animada.

## 2.6 — Vendas: produto expirado não entra no carrinho
- [x] `Views/Sales/ProductCardView.swift`: recebe `sellableStock`, badge "Expirado", botão desactivado e preço com promoção.
- [x] `Views/Sales/SaleView.swift`: calcula o stock vendável de cada produto a partir dos lotes.

## 2.7 — Produtos: perguntar promoção e painel de desconto
- [x] `Views/Products/ProductListView.swift`: acção "Promoção" na linha do produto a expirar → confirmação → `PromotionPanel` que desce de cima, com slider 0…90%, pré-visualização de preço/poupança e remoção da promoção.

## 2.8 — Documentação
- [x] `README.md`, `Docs/database/DATABASE.md`, `Docs/architecture/ARCHITECTURE.md`, `Docs/architecture/SYSTEM_DESIGN.md` (nova secção "Promoção de Produto a Expirar", em Mermaid). `Docs/DOCUMENTATION.md` sem alterações: nenhum `.md` criado, movido ou apagado.

## Correções pós-teste

- [x] `Views/DayClose/DayCloseView.swift` — o ternário entre `formatCount` e `{ formatMT($0) }` rebentava o type-checker (`failed to produce diagnostic for expression`); passou a uma única closure `{ isCount ? formatCount($0) : formatMT($0) }`.
- [x] `Views/Reports/ReportComponents.swift` — repor `growth = 0` e animar para 1 no mesmo update não produzia animação nenhuma (o SwiftUI não via mudança); o arranque da animação passou para o ciclo seguinte via `DispatchQueue.main.async`.
- [x] Compilação (`xcodebuild ... build` → `** BUILD SUCCEEDED **`) e testes (91 testes em 21 suites, incluindo os 3 novos) a passar.
- [x] App lançada e verificada no arranque, sem crash. Os ecrãs com sessão iniciada (Vendas, Fecho, Produtos) ficam por conferir à vista — exigem credenciais do utilizador.

## 2026-08-16 — UX de vendas: filtro com scroll, pagamento em duas colunas, botão Imprimir com cor

# PARTE 1 — BACKEND

Sem alterações de backend nesta ronda (só UI/UX).

# PARTE 2 — FRONTEND

- [x] 2.1 `Views/Sales/SaleView.swift` — barra de filtro passou a um único `ScrollView(.horizontal)` (Todos + Filtrar + categorias) com `.scrollBounceBehavior(.basedOnSize, axes: .horizontal)` e `.frame(maxWidth: .infinity)`. Antes, o scroll interno das categorias ficava dentro do `GlassEffectContainer` e os chips transbordavam por cima da coluna do carrinho; agora limitam-se à largura da coluna e deslizam lado a lado. Transição por chip mantida.
- [x] 2.2 `Views/Sales/PaymentView.swift` — "Pagamentos adicionados" passou para o lado de "Método de pagamento" (`HStack(alignment: .top)`, cada coluna `maxWidth: .infinity`), com o "Valor" a ocupar a largura toda por baixo. Folha alargada para `minWidth: 720 / idealWidth: 820`. A coluna direita só existe quando há entradas, com transição de opacidade + `move(edge: .trailing)`.
- [x] 2.3 `Views/Sales/InvoiceView.swift` — botão "Imprimir" deixou de ser `.buttonStyle(.glass)` incolor: fundo `AppTheme.accent`, texto branco, cantos 8, no mesmo registo do "Partilhar" laranja.
- [x] 2.4 `Docs/architecture/SYSTEM_DESIGN.md` — nova secção "Layout do ecrã de venda e de pagamento" (flowchart Mermaid) com a barra de filtro, as duas colunas do pagamento e os botões da fatura. `README.md`, `DATABASE.md` e `ARCHITECTURE.md` sem alteração: nenhum ficheiro, tabela, ViewModel ou serviço novo.

## Correções pós-teste

- [x] Compilação (`xcodebuild -scheme Sales_Project -destination 'platform=macOS' build` → `** BUILD SUCCEEDED **`) e testes (`test` → `** TEST SUCCEEDED **`) a passar sem correções necessárias.
- [x] Verificação à vista dos três ecrãs fica por conferir — exigem sessão iniciada com credenciais do utilizador.

## 2026-08-16 — Painel de perda real, filtro unificado, cor nos cartões e fim do fundo cinzento do Fecho

# PARTE 1 — BACKEND

- [x] 1.1 `ViewModels/BatchViewModel.swift` — agrupamento por produto extraído para `entries(products:where:)` (filtro de lotes por closure). `riskEntries(products:)` passa a chamá-lo e junta-se `lossEntries(products:)` (só lotes `.expired`), que alimenta o painel de "Perda real" sem duplicar código.

# PARTE 2 — FRONTEND

- [x] 2.1 `Views/Sales/InvoiceView.swift` — botão "Imprimir" já não aparece truncado ("Impri…"): `.fixedSize()` no grupo da toolbar, `.lineLimit(1)` no label e `minWidth: 580 / minHeight: 620` na folha (macOS).
- [x] 2.2 `Utils/AppTheme.swift` — nova `CategoryFilterBar`: barra "Todos / Filtrar" com os chips grandes de categoria a abrirem ao lado, num só `ScrollView(.horizontal)`, com `GlassEffectContainer`, tinta por baixo do vidro e `Reduce Motion` respeitado. Fonte única da barra de filtro por categoria.
- [x] 2.3 `Views/Sales/SaleView.swift` — `filterBar`/`filterButton` privados (≈75 linhas) substituídos por `CategoryFilterBar`; estado `showFilters` deixou de ser preciso na View. Sem mudança visual.
- [x] 2.4 `Views/Products/ProductListView.swift` — a lista de produtos passou a usar a mesma `CategoryFilterBar` das Vendas, em vez dos chips pequenos.
- [x] 2.5 `Views/Products/ProductListView.swift` — cartão "Perda real" ficou clicável e abre no painel lateral direito a lista dos produtos com lotes já expirados; clicar num produto abre `ProductFormView(.edit)`. `RiskSidePanel` generalizado (título, ícone, cor, rótulo do total, estado vazio, entradas, breakdown) e serve os dois painéis; `showRiskPanel: Bool` passou a `sidePanel: ProductSidePanel?` — os dois painéis excluem-se e o chevron reflecte o estado.
- [x] 2.6 `Views/Reports/ReportComponents.swift` — `SecondaryMetricCard` ("Vendas" e "Itens Vendidos") ganhou gradiente da própria cor por baixo do vidro, como os cartões do fecho de caixa. Um único plano de vidro por cartão.
- [x] 2.7 `Views/DayClose/DayCloseView.swift` — fundo cinzento do Fecho de Caixa eliminado: o `TabView` de macOS deu lugar ao mesmo picker segmentado dos Relatórios (uma só via para as duas plataformas, `#if os(iOS)` removido) e o campo de Notas trocou `Color(.controlBackgroundColor)` por `.glassEffect(.regular, in: .rect(cornerRadius: 10))`.

# PARTE 3 — DOCUMENTAÇÃO

- [x] 3.1 `Docs/architecture/SYSTEM_DESIGN.md` — actualizados o diagrama de componentes (`CategoryFilterBar` em `AppTheme.swift`), o painel lateral de Produtos (risco + perda real, `ProductSidePanel`), a Gestão de Categorias (as duas barras apontam à `CategoryFilterBar`) e o Fecho de Caixa (picker segmentado nas duas plataformas). `README.md`, `DATABASE.md` e `ARCHITECTURE.md` sem alteração: nenhum ficheiro, tabela, ViewModel ou serviço novo.

## Correções pós-teste

- [x] Compilação (`xcodebuild -scheme Sales_Project -destination 'platform=macOS' build` → `** BUILD SUCCEEDED **`) e testes (`test` → `** TEST SUCCEEDED **`, 91 testes em 21 suites) a passar sem correções necessárias.
- [x] Verificação à vista dos ecrãs fica por conferir — exigem sessão iniciada com credenciais do utilizador.

## 2026-08-16 — Reordenar categorias por drag + redesenho do gestor de categorias

# PARTE 1 — BACKEND

- [x] 1.1 `Database/DatabaseManager.swift` — `reorderCategories(_ orderedIDs: [Int]) -> Bool`:
      UPDATE `sort_order` por id, dentro de `transaction` com `sqlite3_prepare_v2` + `bind` (nada de interpolação).
- [x] 1.2 `ViewModels/CategoryViewModel.swift` — `move(from:to:)` + `reordering(_:from:to:)` (sem SwiftUI no ViewModel):
      aplica o movimento, renumera `sortOrder`, persiste via 1.1, mantém a lista antiga e escreve `errorMessage` se falhar.
- [x] 1.3 `POSAppTests/CategoryReorderTests.swift` — 3 testes da renumeração (topo, fim, no-op);
      ficheiro registado no target `POSAppTests` em `Sales_Project.xcodeproj/project.pbxproj`.

# PARTE 2 — FRONTEND

- [x] 2.1 `Views/Products/CategoryManagerView.swift` — redesenho: cabeçalho próprio (ícone em vidro,
      título, contagem + "arrasta para reordenar"), linhas em cartão de vidro dentro de `GlassEffectContainer`,
      pega `line.3.horizontal`, `.onMove` ligado a 1.2, `EditButton` no iOS, rodapé com Fechar + Nova categoria (⌘N).
- [x] 2.2 `Views/Products/CategoryManagerView.swift` — animação de abertura (escala + opacidade + desfoque),
      animação de reordenação/inserção/remoção e do erro; tudo anulado com `Reduce Motion`.

# PARTE 3 — DOCUMENTAÇÃO

- [x] 3.1 `Docs/database/DATABASE.md` — `reorderCategories` nas operações de `Categories` e nota em `sort_order`.
- [x] 3.2 `Docs/architecture/ARCHITECTURE.md` (`CategoryViewModel.move`) e `Docs/architecture/SYSTEM_DESIGN.md`
      (fluxo "Arrastar linha" no diagrama de Gestão de Categorias).
- [x] 3.3 `README.md` — funcionalidade de reordenar categorias + árvore do projeto.

## Correções pós-teste

- [x] `CategoryViewModel.swift` — `move(fromOffsets:toOffset:)` é da SwiftUI e não estava disponível no ViewModel
      (`error: instance method 'move(fromOffsets:toOffset:)' is not available due to missing import`);
      substituído por `reordering(_:from:to:)` em Foundation puro.
- [x] `CategoryManagerView.swift` — `error: conflicting arguments to generic parameter 'Result'` no closure do
      `.onMove`; resolvido com `_ = categoryViewModel.move(...)`.
- [x] `POSAppTests/CategoryReorderTests.swift` — `'Category' is ambiguous for type lookup`; tipo qualificado como `POSApp.Category`.
- [x] Compilação (`** BUILD SUCCEEDED **`) e testes (`** TEST SUCCEEDED **`, 94 testes em 22 suites) a passar.
- [x] Verificação à vista do ecrã de Categorias fica por conferir pelo utilizador — exige sessão iniciada com credenciais.

## 2026-08-16 — Produtos: chips de categoria maiores, painéis Perda/Risco separados, stock dos lotes

# PARTE 1 — BACKEND

- [x] 1.1 `Database/DatabaseManager.swift` — `updateProduct` deixou de escrever `stock`.
      Guardar o produto repunha o `stock` do retrato tirado ao abrir a sheet (2 un.),
      apagando os lotes criados/editados entretanto (17 un.). O `stock` vem só de `syncProductStock`.
- [x] 1.2 `ViewModels/BatchViewModel.swift` — `riskEntries` exclui lotes `.expired`
      (fica alinhado com `riskValue`): expirado só no painel de Perda real, por expirar só no de Em risco.
- [x] 1.3 `POSAppTests/ReportFilterTests.swift` — teste de `riskEntries` actualizado à separação
      (totais 200/240, `worstStatus == .days`) + novo teste "Lote expirado só aparece na perda real".

# PARTE 2 — FRONTEND

- [x] 2.1 `Utils/AppTheme.swift` — `CategoryChipView` ganhou `isLarge`: texto/ícone a 15 pt,
      padding 16/12 e `.glassEffect(.regular, in: .capsule)` só nesta variante (nunca vidro sobre vidro).
- [x] 2.2 `Views/Products/ProductFormView.swift` — grelha de categorias do passo 1 em `GlassEffectContainer`,
      colunas de 175 pt, espaçamento 12 e selecção animada em spring (anulada com `Reduce Motion`).
- [x] 2.3 `Views/Products/ProductFormView.swift` — editar/apagar lote chama `productViewModel.loadProducts()`,
      para a linha de Produtos acompanhar o stock dos lotes sem fechar a sheet.

# PARTE 3 — DOCUMENTAÇÃO

- [x] 3.1 `Docs/database/DATABASE.md` — nota de stock reescrita: `updateProduct` ignora `stock`.
- [x] 3.2 `Docs/architecture/SYSTEM_DESIGN.md` — painéis Perda real / Em risco descritos como conjuntos disjuntos.

## Correções pós-teste

- [x] Compilação (`** BUILD SUCCEEDED **`) e testes (`** TEST SUCCEEDED **`, 95 testes em 22 suites) a passar.
- [x] Verificação à vista dos ecrãs de Produtos fica por conferir pelo utilizador — exige sessão iniciada com credenciais.


---

## 2026-08-16 — Área de Administração (dashboard, validade, produtos parados, fecho por caixa) e correcções nas categorias

Ciclo: **Área de Administração** (dashboard, produtos parados, validade, fechos por caixa)
+ correcções na gestão de categorias e promoção por menu de contexto.

---

# PARTE 1 — BACKEND

## 1.1 — Base de dados: última venda por produto
- [x] `Database/DatabaseManager.swift` — `lastSaleDates() -> [Int: Date]`
      (`SaleItems` ⨝ `Sales`, `MAX(date)` por `product_id`, só vendas `completed`).
      SQL preparado, sem interpolação.

## 1.2 — Base de dados: fecho por caixa
- [x] `Models/CashierClose.swift` — modelo novo (`date`, `userId`, totais por método,
      `numSales`, `notes`, `closedBy`, `closedAt`).
- [x] `Database/DatabaseManager.swift` — `createCashierClosesTable()`
      (`UNIQUE(date, user_id)`, índice por data) + chamada em `createTables()`.
- [x] `Database/DatabaseManager.swift` — `saveCashierClose(...)`,
      `fetchCashierCloses(date:)`, `reopenCashierClose(date:userId:)` (só Admin).
      Escrita em transacção, `logAudit` em cada fecho/reabertura.

## 1.3 — ViewModel de administração
- [x] `ViewModels/AdminViewModel.swift` — novo:
      - estatísticas do dashboard (hoje/mês/ano: receita, nº vendas, ticket médio,
        série diária dos últimos 30 dias, mix de métodos de pagamento,
        top de produtos, receita por categoria);
      - `staleProducts(months:)` — produtos sem venda há mais de 6 meses
        (inclui nunca vendidos, com base na data do lote mais antigo);
      - `staleBatches(months:)` — lotes parados há mais de 6 meses;
      - estado de fecho por caixa numa data (vendas por utilizador + fecho feito ou não).

## 1.4 — Autorização por perfil
- [x] `ViewModels/AuthViewModel.swift` / `Database/DatabaseManager.swift` — confirmar que
      Produtos e Relatórios continuam bloqueados na camada de dados para perfil Caixa
      (esconder na UI não chega).

## 1.5 — Testes
- [x] `POSAppTests/StaleProductTests.swift` — regra dos 6 meses (limite exacto,
      nunca vendido, vendido ontem).
- [x] `POSAppTests/CashierCloseTests.swift` — agregação de vendas por caixa e
      estado "fechado / por fechar".

---

# PARTE 2 — FRONTEND

## 2.1 — Navegação e perfis
- [x] `Views/MainView.swift` — separador **Administração** entre "Fecho de Caixa" e
      "Definições", só para Admin.
- [x] `Views/MainView.swift` — perfil Caixa: esconder **Produtos** e **Relatórios**.

## 2.2 — Área de administração
- [x] `Views/Admin/AdminView.swift` — contentor com secções:
      Dashboard · Validade · Parados · Fechos · Relatórios.
- [x] `Views/Admin/AdminDashboardView.swift` — dashboard de estatísticas da loja
      (KPIs, gráfico de receita, mix de pagamento, top de produtos, receita por categoria).
      Referência visual: `../Ideas/Swift UI idea/src/dashboard`.
- [x] `Views/Admin/AdminExpiryView.swift` — cartões "Perda real / Em risco / Stock baixo"
      + lista de produtos e lotes a expirar e já expirados (redesenho do painel lateral).
- [x] `Views/Admin/StaleProductsView.swift` — produtos e lotes sem venda há mais de
      6 meses, com acção de promoção.
- [x] `Views/Admin/CashierCloseAdminView.swift` — lista de caixas do dia, com fecho
      feito ou por fazer; o Admin pode fechar a caixa de cada utilizador.

## 2.3 — Mover histórico para Administração
- [x] `Views/DayClose/DayCloseView.swift` — tirar a secção "Histórico" do Fecho de Caixa.
- [x] `Views/MainView.swift` (`ReportsHomeView`) — tirar a secção "Histórico" dos Relatórios.
- [x] `Views/Admin/AdminView.swift` — as duas passam a viver aqui, redesenhadas.

## 2.4 — Fecho de Caixa por perfil
- [x] `Views/DayClose/DayCloseView.swift` — perfil Caixa: só o fecho da sua própria caixa.

## 2.5 — Produtos
- [x] `Views/Products/ProductListView.swift` — menu de contexto (botão direito) nas
      linhas de produto com "Fazer promoção" / "Remover promoção".
- [x] `Views/Products/ProductListView.swift` — remover os cartões de estado e o painel
      lateral (passam para Administração).

## 2.6 — Correcções na gestão de categorias
- [x] `Views/Products/CategoryManagerView.swift` — cabeçalho e rodapé deixam de ser
      atravessados pelas linhas no scroll (fundo opaco + `safeAreaInset`).
- [x] `Views/Products/CategoryManagerView.swift` — arrastar para reordenar volta a
      funcionar em macOS (o `onTapGesture` da linha estava a comer o gesto de arrasto).

## 2.7 — Documentação
- [x] `README.md` — funcionalidades + árvore do projecto.
- [x] `Docs/database/DATABASE.md` — tabela `CashierCloses` no `erDiagram` e no `graph LR`.
- [x] `Docs/architecture/ARCHITECTURE.md` — `AdminViewModel` e camada de administração.
- [x] `Docs/architecture/SYSTEM_DESIGN.md` — fluxos novos em Mermaid.
- [x] `Docs/DOCUMENTATION.md` — índice.

## Correções pós-teste

- [x] `ViewModels/AdminViewModel.swift` — `revenueByCategory` reescrito em ciclos explícitos; a versão com `Dictionary(grouping:)` encadeado fazia o compilador falhar com *"unable to type-check this expression in reasonable time"*.
- [x] `ViewModels/AdminViewModel.swift` — `StaleProduct` e `CashierDayStatus` deixaram de declarar `Hashable`: `Product`, `Sale`, `User` e `Payment` não são `Equatable`.
- [x] `POSAppTests/AdminStatsTests.swift` — o teste do limite exacto lia `Self.limit` duas vezes (dois `Date()` diferentes, o segundo mais tarde) e falhava; passa a guardar o limite numa variável.
- [x] `Sales_Project.xcodeproj/project.pbxproj` — ficheiros novos registados nos grupos `Models`, `ViewModels` e no grupo novo `Views/Admin`, e nas fases `Sources` da app e dos testes.
- [x] Compilação (`** BUILD SUCCEEDED **`) e testes (`** TEST SUCCEEDED **`, 24 suites incluindo as duas novas) a passar; app arrancada em macOS sem crash.

---

## 2026-08-16 — Fecho da própria caixa, Guia por perfil e edição de lotes/stock na Administração

# TODO — POS Sales_Project

# PARTE 1 — BACKEND

- [x] 1.1 — Bug: perfil Caixa sem botão de fecho da sua caixa.
  Reproduzido ao nível do ViewModel/DB em `POSAppTests/CashierCloseFlowTests.swift`
  (o caminho de dados estava correcto — o Caixa vê e fecha a sua caixa).
  **Causa real, na UI**: em `Views/Admin/CashierCloseAdminView.swift`, quando a
  caixa já estava **fechada** (por exemplo, fechada pelo Admin), a única acção
  desenhada era "Reabrir caixa", visível só para Admin — o Caixa ficava com o
  cartão sem botão nenhum.
  **Correcção**: a caixa própria tem sempre acção — "Fechar a minha caixa" quando
  está por fechar e "Actualizar o meu fecho" quando já está fechada (regrava o
  fecho com os valores actuais, incluindo vendas feitas depois).

- [x] 1.2 — `ViewModels/AdminViewModel.swift`: edição a partir da Administração.
  - `updateBatch(_ batch: Batch) -> Bool` — quantidade e validade de um lote
    (reaproveita `DatabaseManager.updateBatch`), com validação no ViewModel.
  - `updateStock(productId:newStock:) -> Bool` — repor stock de um produto
    (reaproveita `DatabaseManager.updateStock`), com validação no ViewModel.
  - Ambos recarregam (`load()`) e escrevem `errorMessage` em caso de falha.

- [x] 1.3 — `POSAppTests/AdminEditingTests.swift`: testes das validações de 1.2
  (quantidade negativa, stock negativo, escrita válida + stock sincronizado).

# PARTE 2 — FRONTEND

- [x] 2.1 — `Views/Posguideview.swift` + `Views/MainView.swift`: Guia por perfil.
  `POSGuideView(isAdmin:)` e `POSGuideWindowController.open(isAdmin:)` (refaz a
  janela se o perfil mudar). O Caixa vê Visão Geral, Vendas, Pagamentos, Fecho de
  Caixa e Atalhos; Produtos, Lotes, Relatórios, Definições e Partilha iOS são só
  do Admin. Visão Geral, Fecho de Caixa e Atalhos mudam de conteúdo por perfil.

- [x] 2.2 — `Views/Admin/AdminExpiryView.swift`: separador "Em risco" redesenhado.
  Ordenação pelo prazo mais curto, chip com os dias que faltam por produto, e uma
  barra única repartida pelas faixas com legenda (lotes, % e valor) em vez das
  barras soltas que davam sempre 100% com uma faixa só.

- [x] 2.3 — `Views/Admin/AdminExpiryView.swift`: em "Expirados" (e também em
  "Em risco"), tocar num lote abre o `BatchEditSheet` — quantidade e data de
  validade, gravadas por 1.2.

- [x] 2.4 — `Views/Admin/AdminExpiryView.swift`: em "Stock baixo", tocar num
  produto abre o `StockEditSheet` — reposição de stock (+5/+10/+20/+50 ou valor
  directo), gravada por 1.2.

- [x] 2.5 — Documentação actualizada: `README.md`,
  `Docs/architecture/ARCHITECTURE.md`, `Docs/architecture/SYSTEM_DESIGN.md`
  (diagramas do Guia por perfil, estados da caixa própria e sheets de edição),
  `Docs/architecture/TECHNICAL_DESIGN.md`. `Docs/database/DATABASE.md` e
  `Docs/DOCUMENTATION.md` não mudaram — não houve alteração de esquema nem `.md`
  novo.

## Correções pós-teste

- [x] `Views/Admin/AdminExpiryView.swift` — o texto de ajuda do `StockEditSheet`
  dizia "entra no lote mais recente"; `adjustStockToBatches` põe a subida no lote
  **sem validade** (cria um se não existir) e a descida sai por FIFO. Texto corrigido.
- [x] `Views/Posguideview.swift` — a janela do Guia em macOS era reutilizada entre
  sessões; se mudasse o perfil, o Caixa herdava o guia do Admin. Passa a refazer-se
  quando `isAdmin` muda.
- [x] `Views/Admin/AdminExpiryView.swift` — `vm.errorMessage` não era mostrado
  neste ecrã; uma gravação falhada ficava silenciosa. Passou a ter linha de erro.

- [x] `Docs/architecture/SYSTEM_DESIGN.md` — o `sequenceDiagram` de "Fecho por Caixa"
  não renderizava: o `;` dentro da mensagem `DB->>DB: S3 — Caixa só fecha a sua; ...`
  termina a instrução em Mermaid. Trocado por `·` (e tirados os parênteses/aspas do
  `logAudit`). Os 55 blocos Mermaid de `Docs/` foram validados com `mermaid-cli` — todos renderizam.

Estado: `xcodebuild build` e `xcodebuild test` (macOS) passam — 107 testes, 26 suites.

---

## 2026-08-16 — Folhas de lote e stock em Liquid Glass, selector de meses e cartões tingidos em Parados

# TODO — POS Sales_Project

# PARTE 1 — BACKEND

Sem trabalho de backend: as tarefas deste ciclo são só de apresentação (Views).

# PARTE 2 — FRONTEND

- [x] 2.1 `Views/Admin/AdminExpiryView.swift` — redesenhar `BatchEditSheet` (aberta em "Em risco" e "Expirados"): cabeçalho com ícone tingido pelo estado de validade, dias em falta em texto exacto, campo de quantidade e validade num único plano de vidro, botões em vidro, animação de estado.
- [x] 2.2 `Views/Admin/AdminExpiryView.swift` — redesenhar `StockEditSheet` (aberta em "Stock baixo"): mesmo cabeçalho, delta face ao stock actual, atalhos +5/+10/+20/+50 em `GlassEffectContainer`, botões em vidro.
- [x] 2.3 `Views/Admin/StaleProductsView.swift` — corrigir o selector de meses: o rótulo "Meses" aparecia colado e partido ao lado do `Picker`; esconder o rótulo e alinhar a linha.
- [x] 2.4 `Views/Admin/AdminView.swift` + `Views/Admin/StaleProductsView.swift` — `AdminKPICard` com vidro tingido pela cor do ícone (opção `tinted`), usada nos três cartões de "Parados".
- [x] 2.5 Documentação: `README.md`, `Docs/architecture/ARCHITECTURE.md`, `Docs/architecture/SYSTEM_DESIGN.md`, `Docs/architecture/TECHNICAL_DESIGN.md`.

## Correções pós-teste

Estado: `xcodebuild build` e `xcodebuild test` (macOS) passam.

---

## 2026-08-16 — Regra UX antes de UI com PLAN.md, animação/transição e Liquid Glass obrigatórios

# TODO — POS Sales_Project

# PARTE 1 — BACKEND

Sem trabalho de backend: ciclo só de regras e documentação.

# PARTE 2 — FRONTEND

- [x] 2.1 `Docs/development/STYLE_GUIDE.md` — nova secção obrigatória "UX antes de UI": antes de implementar qualquer UI, escrever o plano de UX em `Docs/planning/PLAN.md`; o `PLAN.md` funciona como cache e é esvaziado assim que a UI fica executada.
- [x] 2.2 `Docs/development/STYLE_GUIDE.md` — tornar explícita a obrigação de animação, transição e Liquid Glass em toda a UI onde for possível (§4 e §5) e acrescentar os itens à checklist §15.
- [x] 2.3 `Docs/planning/PLAN.md` — criar o ficheiro (vazio, pronto para o primeiro plano).
- [x] 2.4 `CLAUDE.md` — obrigação de pensar UX antes de UI (com `PLAN.md`) e de seguir rigorosamente o `Docs/development/STYLE_GUIDE.md` em toda a UI.
- [x] 2.5 `Docs/DOCUMENTATION.md` — indexar `PLAN.md` em `Docs/planning/`.

## Correções pós-teste

Estado: ciclo só de regras e documentação; `xcodebuild build` (macOS) passa.

---

## 2026-08-16 — Filtro de data no Dashboard da Administração

# TODO — POS Sales_Project

Ciclo: filtro de data do Dashboard da Administração.

Contexto: no Dashboard, "Mês" e "Ano" têm de ser sempre do ano actual (e dizê-lo no ecrã);
"Total" tem de deixar filtrar por ano, mês e dia; todos os gráficos e painéis abaixo dos
indicadores passam a seguir o período/filtro escolhido (hoje a série é sempre "últimos 30 dias",
ignora o período).

# PARTE 1 — BACKEND

- [x] 1.1 `ViewModels/AdminViewModel.swift` — `struct DateFilter { year, month, day }` (todos opcionais) + `@Published var filter` usado só no período `.all`.
- [x] 1.2 `ViewModels/AdminViewModel.swift` — `sales(in:)` aplica o `filter` quando o período é `.all`; `.month`/`.year` continuam presos ao ano actual (`isDate(equalTo:toGranularity:)` compara também o ano).
- [x] 1.3 `ViewModels/AdminViewModel.swift` — `availableYears` (anos com vendas, do mais recente para o mais antigo) e `daysInSelectedMonth` para o picker de dia.
- [x] 1.4 `ViewModels/AdminViewModel.swift` — substituir `dailyRevenue(days:)` por `revenueSeries(in:)`: pontos + granularidade (`.hour` para um dia, `.day` para um mês, `.month` para um ano ou para o total), com buckets vazios incluídos.
- [x] 1.5 `ViewModels/AdminViewModel.swift` — `periodLabel(_:)`: texto do período para subtítulos ("Agosto de 2026", "2026", "Total", "16/08/2026").
- [x] 1.6 `POSAppTests/AdminDateFilterTests.swift` — testes: filtro ano/mês/dia, série com buckets vazios, granularidade por período.

# PARTE 2 — FRONTEND

- [x] 2.1 `Docs/planning/PLAN.md` — plano de UX da barra de período/filtro (§0.1).
- [x] 2.2 `Views/Admin/AdminDashboardView.swift` — barra de filtro (Ano · Mês · Dia) visível só em "Total", com dia desactivado enquanto não houver ano+mês (prevenir em vez de corrigir).
- [x] 2.3 `Views/Admin/AdminDashboardView.swift` — gráfico de receita passa a usar `revenueSeries(in:)`, título e eixo X seguem a granularidade; subtítulos dos três painéis usam `periodLabel`.
- [x] 2.4 Animar mudança de período/filtro e esvaziar o `PLAN.md`.

# PARTE 3 — DOCUMENTAÇÃO

- [x] 3.1 `README.md` — dashboard com filtro de data.
- [x] 3.2 `Docs/architecture/ARCHITECTURE.md`, `SYSTEM_DESIGN.md`, `TECHNICAL_DESIGN.md` — `DateFilter`/`revenueSeries` no AdminViewModel.
- [x] 3.3 `Docs/DOCUMENTATION.md` — indexar `AdminDateFilterTests` se aplicável.

## Correções pós-teste

- [x] `Views/Admin/AdminDashboardView.swift` — `Chart` com `x: .value(..., unit:)` exige `Calendar.Component` constante no `ForEach`; resolvido passando a unidade da série ao mark.


---

## 2026-08-16 — Cartões de "Parados" com o vidro neutro da Administração

# TODO — POS Sales_Project

Ciclo: uniformizar o aspecto dos indicadores de Administração › Parados com o resto da Administração (Relatórios, Dashboard, Validade, Fechos).

# PARTE 1 — BACKEND

- [x] 1.1 Sem alterações de backend.

# PARTE 2 — FRONTEND

- [x] 2.1 `Views/Admin/AdminView.swift` — remover a opção `tinted` do `AdminKPICard`: um único plano de vidro `.regular` em toda a Administração.
- [x] 2.2 `Views/Admin/StaleProductsView.swift` — os três indicadores ("Produtos parados", "Capital imobilizado", "Unidades paradas") passam ao cartão neutro; a cor do indicador fica só no ícone e no valor.

# PARTE 3 — DOCUMENTAÇÃO

- [x] 3.1 `Docs/architecture/ARCHITECTURE.md` — fim da variante tingida em Parados.
- [x] 3.2 `Docs/architecture/TECHNICAL_DESIGN.md` — secção Administração › Parados actualizada.

Estado: `xcodebuild build` (macOS) passa.

---

## 2026-08-17 — Segurança em três rondas, SECURITY_POLICY, TESTING.md e ERRORS.md

# TODO — POS Sales_Project

Ciclo de regras: segurança validada em três rondas, teste de implementação antes da UX/UI e registo de erros.
Trabalho de processo e documentação — não toca em Swift, por isso a Parte 2 (Frontend) fica sem itens.

Baseline antes de começar: `xcodebuild -scheme Sales_Project -destination 'platform=macOS' test` → `** TEST SUCCEEDED **`, 118 testes em 27 suites.

# PARTE 1 — BACKEND (regras, segurança, testes e documentação)

## 1.1 `Docs/security/SECURITY.md` — obstáculos antes de implementar

- [x] Cabeçalho: tabela que divide o trabalho entre `SECURITY.md` (o que tem de estar no código) e `SECURITY_POLICY.md` (como se garante e o que fazer quando falha) — `Docs/security/SECURITY.md`
- [x] §2.2.1 novo: **análise de obstáculos obrigatória antes de escrever a função** — listar cada entrada, que lixo hostil o campo aceita hoje e o que acontece se passar, com quadro dos 12 obstáculos típicos — `Docs/security/SECURITY.md`
- [x] §2.2.2: catálogo de validação por tipo de campo, com colunas **Aceita** / **Recusa sempre** (campo numérico com letras/símbolos, nome de pessoa com dígitos, nome só de símbolos, `NaN`/`infinity`, negativos, datas fora de gama, comprimento, caracteres de controlo) — `Docs/security/SECURITY.md`
- [x] §2.2.3: a UI (teclado, formatter, stepper) **não é validação** — a barreira real vive no ViewModel e repete-se na camada de dados — `Docs/security/SECURITY.md`

## 1.2 `Docs/security/SECURITY.md` — três rondas de validação

- [x] §2.5 novo: **V1** (plano, antes de codificar), **V2** (código relido), **V3** (compilado e testado com entradas hostis), com prova por mutação e a regra de repetir V2+V3 depois de qualquer correção — `Docs/security/SECURITY.md`
- [x] §6: os testes de segurança passam a apontar para a bateria hostil do `Docs/development/TESTING.md` — `Docs/security/SECURITY.md`

## 1.3 `Docs/security/SECURITY.md` — registo de validações aplicadas

- [x] §11 novo: tabela `#`, data, função/ecrã, campo, regra aplicada, onde vive, teste — semeada com 17 validações que já existem no código (`ProductViewModel`, `AdminViewModel`, `AuthViewModel`, `CategoryViewModel`, `CSVField`, `ReportService`, `ProximityManager`) — `Docs/security/SECURITY.md`
- [x] §11.1 novo: lacunas conhecidas G1–G6 entre o catálogo e o que o código valida hoje, com severidade — sem fingir cobertura que não existe — `Docs/security/SECURITY.md`
- [x] §10 checklist: acrescentadas as três rondas, o registo §11, a bateria do `TESTING.md`, o `ERRORS.md` e a obrigação de corrigir o próprio documento — `Docs/security/SECURITY.md`
- [x] §8: passa a apontar para o `SECURITY_POLICY.md` em vez de repetir a resposta a incidente — `Docs/security/SECURITY.md`

## 1.4 `Docs/security/SECURITY_POLICY.md` (novo)

- [x] Responde a "**Como este projeto garante a sua segurança e o que fazer quando existe uma falha?**": âmbito, seis portões obrigatórios P1–P6 (com `flowchart` Mermaid e retorno da correção ao P3), papéis, severidade A/M/B com prazos, cadência de revisão, resposta a incidente em 7 passos, suspeita de acesso indevido, comunicação de vulnerabilidade (prefixo `SEC:`), dados pessoais e checklist de resposta — `Docs/security/SECURITY_POLICY.md`

## 1.5 `Docs/development/TESTING.md` (novo)

- [x] Regra do teste de implementação **antes** da UX e da UI (é a V3); como correr a suite e porque é que o plano tem `parallelizable: false`; tabela de índice T1–T16 com o que cada suite resolve; bateria de entradas hostis por tipo de campo; regras para acrescentar teste novo (nome em PT, prova por mutação, limpeza com `defer`, registo no alvo `POSAppTests`); verificação manual — `Docs/development/TESTING.md`

## 1.6 `Docs/development/ERRORS.md` (novo)

- [x] Tabela de índice E1–E22 (data, sintoma, onde, categoria, estado) + uma entrada por erro com **sintoma, causa, solução e prova**, semeada com os erros reais já resolvidos e registados no `Docs/CHANGELOG.md` — `Docs/development/ERRORS.md`

## 1.7 `CLAUDE.md` — regras novas

- [x] Leitura obrigatória passa a incluir `SECURITY_POLICY.md`, `TESTING.md` e `ERRORS.md` — `CLAUDE.md`
- [x] §2: quatro linhas novas na tabela de documentação (validação nova → `SECURITY.md` §11; regra de segurança em falta → `SECURITY.md`/`SECURITY_POLICY.md`; teste novo → `TESTING.md`; erro resolvido → `ERRORS.md`) e subpastas atualizadas — `CLAUDE.md`
- [x] §3 reescrita, com 3.1 análise de obstáculos antes de implementar, 3.2 validação tripla, 3.3 reforço das validações em toda a função nova, 3.4 registo no `SECURITY.md` §11, 3.5 obrigação de **enriquecer** o `SECURITY.md`/`SECURITY_POLICY.md`, 3.6 teste da função/janela nova contra `SECURITY.md` §10 **e** `STYLE_GUIDE.md` §15 — `CLAUDE.md`
- [x] §8 ordem de trabalho reescrita em 11 passos: V1 → backend → V2 → **teste de implementação (V3, documentado no `TESTING.md`)** → UX → UI → checklists → documentação → teste final — `CLAUDE.md`
- [x] §10 e §11 novas: `TESTING.md` e `ERRORS.md` como documentos de leitura e escrita obrigatórias — `CLAUDE.md`

## 1.8 Índices e estrutura

- [x] `Docs/DOCUMENTATION.md` — indexados `SECURITY_POLICY.md` (4.2), `TESTING.md` (5.2) e `ERRORS.md` (5.3)
- [x] `README.md` — árvore do `Docs/` com os três ficheiros novos e o `PLAN.md`, `AdminDateFilterTests.swift` na lista de testes e linha de leitura obrigatória atualizada
- [x] `Docs/architecture/` — percorridos os três `.md`: `ARCHITECTURE.md` (alvo de testes, registo no `project.pbxproj`, validação como camada, tabela "onde acrescentar"), `TECHNICAL_DESIGN.md` (hash do `AuthViewModel`), `SYSTEM_DESIGN.md` (sem alteração — só cobre fluxos da app, nenhum mudou)

## 1.9 Testes

- [x] Compilação e suite completa antes e depois: `** TEST SUCCEEDED **`, 118 testes em 27 suites
- [x] Nenhum `.md` novo entrou no alvo do Xcode (documentação não é recurso — lição E5)

## Correções pós-teste

- [x] `Docs/architecture/ARCHITECTURE.md` — o alvo `POSAppTests` listava 7 suites de um estado antigo do projeto (são 16 ficheiros, 118 testes em 27 suites); passou a apontar para o índice do `TESTING.md` e ganhou a nota do registo no `project.pbxproj` (E3/E4).
- [x] `Docs/architecture/TECHNICAL_DESIGN.md` — `AuthViewModel` descrito como "hash SHA256"; está em PBKDF2-HMAC-SHA256 desde a correção S2. Corrigido.
- [x] `README.md` — árvore do `Docs/` sem `PLAN.md` e sem os ficheiros novos; `AdminDateFilterTests.swift` em falta na lista de testes. Corrigido.
- [x] Fences ` ```mermaid ` verificadas em todos os ficheiros novos e alterados (lição E10): todos os blocos abertos e fechados, `SECURITY.md` com 1 diagrama e `SECURITY_POLICY.md` com 1.
- [x] Âncoras do índice do `ERRORS.md` conferidas contra os cabeçalhos `### E<n> — …` (backticks, parênteses e dois-pontos caem na geração da âncora).
- [x] Ciclo sem alterações a Swift, logo sem erros de compilação novos para o `ERRORS.md` — as 22 entradas são o histórico já resolvido, recuperado do `CHANGELOG.md`.

# PARTE 2 — FRONTEND

Sem trabalho de UI neste ciclo — nenhuma View tocada, logo não há plano de UX em `Docs/planning/PLAN.md`.

---

## 2026-08-17 — Validação em cinco rondas (V1–V5) e portões P1–P8

# TODO — POS Sales_Project

Ciclo: as rondas de validação passam de **três para cinco** (V1–V5). Documentação e processo — não toca em Swift, por isso a Parte 2 (Frontend) fica sem itens.

# PARTE 1 — BACKEND (regras e documentação)

## 1.1 `Docs/security/SECURITY.md` — §2.5 com cinco rondas

- [x] Título e texto: "três rondas" → **cinco rondas**, com o que distingue cada meio (papel, código lido, código a correr isolado, app a correr a sério, conjunto todo depois da última correção) — `Docs/security/SECURITY.md`
- [x] Tabela das rondas: **V1** plano · **V2** código · **V3** testes automáticos · **V4** fluxo real na app (Caixa e Admin, recusa visível em PT, nada gravado a meio, ficheiro exportado conferido) · **V5** regressão e varrimento do `git diff` — `Docs/security/SECURITY.md`
- [x] Regras de fecho: correção obriga a repetir **a partir da V2**; V5 é sempre a última antes de `[x]`; a V4 não se dispensa por ser manual e o que não puder ser provado fica escrito no `TODO.md`; nenhuma ronda se salta nem troca de ordem — `Docs/security/SECURITY.md`

## 1.2 `Docs/security/SECURITY.md` — propagar a mudança

- [x] Cabeçalho (tabela de divisão), §6 (ligação ao `TESTING.md`, agora com V4 e V5), §10 (checklist com as cinco rondas) e §11 (intro: o registo é parte da V5) — `Docs/security/SECURITY.md`
- [x] IDs do registo §11 renomeados de `V1…V17` para `R1…R17` — colidiam com os nomes das rondas V1–V5 — `Docs/security/SECURITY.md`

## 1.3 `Docs/security/SECURITY_POLICY.md` — portões alinhados com as rondas

- [x] Portões de P1–P6 para **P1–P8**: tarefa, V1, V2, V3, V4 (fluxo real), V5 (regressão e diff), documentação, fecho do ciclo — `Docs/security/SECURITY_POLICY.md`
- [x] Mermaid atualizado: P1→…→P8, falha em P4, P5 ou P6 volta ao P3 pelo nó de correção; texto do retorno e do "UX/UI só depois do P4" reescrito — `Docs/security/SECURITY_POLICY.md`
- [x] §3 (papéis, "oito portões"), §5 (cadência, P1–P8) e §6 passo 5 (repetir **V2 a V5**) — `Docs/security/SECURITY_POLICY.md`

## 1.4 `Docs/development/TESTING.md`

- [x] Ordem obrigatória com as cinco rondas (V4 e V5 depois da UI); §5 passou a ser a **V4 — fluxo real** (perfil Caixa e Admin, nada gravado a meio, ficheiro exportado aberto e conferido) — `Docs/development/TESTING.md`
- [x] §6 nova: **V5 — regressão e varrimento do diff** (suite completa, `git diff` sem SQL interpolado/`print` sensível/credenciais, ficheiros registados no alvo, contagem de testes conferida, registos escritos) — `Docs/development/TESTING.md`

## 1.5 `CLAUDE.md`

- [x] §3 tabela dos dois documentos (cinco rondas) e §3.2 reescrita com a tabela V1–V5 e as regras de repetição — `CLAUDE.md`
- [x] §3.4 (registo é parte da V5, IDs `R…`), §3.6 (checklist com cinco rondas) — `CLAUDE.md`
- [x] §8 ordem de trabalho em 12 passos, com **V4 — fluxo real** depois da UI e **V5 — regressão e fecho** antes de marcar `[x]` — `CLAUDE.md`
- [x] §10 (regras 1, 6 e 7 com V3/V4/V5) e §11 (regra 4: repetir a partir da V2, acabar na V5) — `CLAUDE.md`

## 1.6 Índices e ficheiros que citam as rondas

- [x] `README.md` (árvore do `Docs/`), `Docs/DOCUMENTATION.md` (descrição 4.1) e `Docs/development/ERRORS.md` (regra 4) — cinco rondas

## 1.7 Testes

- [x] Suite completa: `xcodebuild -scheme Sales_Project -destination 'platform=macOS' test` → `** TEST SUCCEEDED **`
- [x] Varrimento final: nenhuma menção a "três rondas", "validação tripla" ou `V1/V2/V3` ficou em `CLAUDE.md`, `README.md` ou `Docs/`; fences ` ``` ` todas fechadas nos ficheiros tocados

## Correções pós-teste

- [x] `Docs/security/SECURITY.md` — os IDs do registo §11 (`V1`–`V17`) passaram a colidir com os nomes das rondas assim que estas chegaram a V5; renomeados para `R1`–`R17`, com a nota na introdução da secção e em `CLAUDE.md` §3.4.
- [x] `Docs/security/SECURITY_POLICY.md` — os seis portões deixavam duas rondas novas sem prova exigida; passaram a oito, com o diagrama a mostrar que a falha em P4, P5 **ou** P6 volta sempre ao P3.
- [x] `Docs/development/TESTING.md` — a "verificação manual" era uma lista solta; passou a ser a ronda V4 com critérios verificáveis (perfil Caixa e Admin, estado da BD depois de uma recusa, ficheiro exportado aberto), e a regressão ganhou secção própria como V5.

# PARTE 2 — FRONTEND

Sem trabalho de UI neste ciclo.

---

## 2026-08-19 — Seletor de gráfico no Dashboard (Receita · Vendas por caixa) e indicadores em grelha de colunas iguais

Redesenho de UX do Dashboard da Administração (mesmos componentes, nova hierarquia e layout),
com o painel de referência enviado pelo utilizador como amostra: um indicador herói em destaque,
coluna principal + coluna lateral, e ar entre grupos em vez de uma grelha uniforme.
Ronda 2 (pedido do utilizador): métodos de pagamento passam para a coluna lateral e o Dashboard
ganha estatística por caixa (nº de vendas e valor total).

# PARTE 1 — BACKEND

O redesenho em si não acrescenta dados — usa o `AdminViewModel` como está (`revenue`,
`averageTicket`, `itemsSold`, `stockValue`, `riskValue`, `realLoss`, `revenueSeries`,
`paymentMix`, `topProducts`, `revenueByCategory`). A estatística por caixa é a única
adição, e não abre entrada nova do utilizador (ecrã só de leitura), logo não há validação
nova a registar em `SECURITY.md` §11.

- [x] 1.1 `ViewModels/AdminViewModel.swift` — `CashierPerformance` (utilizador, nº de vendas, total) + `static func cashierPerformance(sales:users:)` puro (testável sem base de dados) e `cashierPerformance(in:)` que o aplica ao período. Venda de um utilizador apagado fica com o nome de recurso `Utilizador #<id>` em vez de sair do total.
- [x] 1.2 `ViewModels/AdminViewModel.swift` — `@Published var users` carregado no `load()`; o painel novo lê a lista em memória em vez de chamar `fetchUsers()` a cada redesenho.
- [x] 1.3 V3 — `POSAppTests/AdminStatsTests.swift`: suite "Vendas por caixa" (agrega nº e total por utilizador, ordena por total, nome de recurso para utilizador desconhecido, sem vendas dá lista vazia) + prova por mutação.
- [x] 1.4 `Docs/development/TESTING.md` — linha na tabela de índice §2 para a suite nova.

# PARTE 2 — FRONTEND

- [x] 2.1 `Docs/planning/PLAN.md` — plano de UX do Dashboard, antes de tocar na View.
- [x] 2.2 `Views/Admin/AdminView.swift` — `AdminKPICard` ganha `prominent: Bool = false`: mesmo cartão e mesmo vidro `.regular`, tipografia e espaçamento maiores para o indicador herói. O destaque é por tamanho, não por tinta (decisão do ciclo anterior mantida).
- [x] 2.3 `Views/Admin/AdminDashboardView.swift` — cabeçalho com período e filtro de data; o rótulo do período passa a ser dito uma só vez e sai do subtítulo de cada painel.
- [x] 2.4 `Views/Admin/AdminDashboardView.swift` — bloco de indicadores: Receita como cartão herói ao lado da grelha dos restantes cinco; empilha em ecrã estreito (`ViewThatFits`).
- [x] 2.5 `Views/Admin/AdminDashboardView.swift` — layout em duas colunas (`ViewThatFits`), que empilham em iOS/janela estreita.
- [x] 2.6 `Views/Admin/AdminDashboardView.swift` — escala de espaçamento do `STYLE_GUIDE` §1 (8/12/16/24) e largura máxima de leitura (1280), igual ao padrão do `SettingsView`.
- [x] 2.7 `Views/Admin/AdminDashboardView.swift` — "Métodos de pagamento" passa para a coluna lateral, por baixo de "Receita por categoria".
- [x] 2.8 `Views/Admin/AdminDashboardView.swift` — painel "Vendas por caixa" na coluna principal, com `AdminPanel` + `AdminProportionRow` (nome · nº de vendas, valor total, barra proporcional ao maior).
- [x] 2.9 `Views/Admin/AdminView.swift` — corrigir o cartão herói: sem `Spacer`/`maxHeight: .infinity`, que deixavam um vazio grande entre o rótulo e o valor quando a grelha ao lado é mais alta.
- [x] 2.10 V4 — fluxo real, **por conferir no ecrã** (precisa de sessão iniciada, perfis Admin e Caixa): os quatro períodos, filtro Ano·Mês·Dia, janela larga e janela estreita (colunas empilhadas), claro e escuro, contraste do valor herói sobre vidro, painel de caixas com mais do que um utilizador.
- [x] 2.11 V5 — regressão: `xcodebuild -scheme Sales_Project -destination 'platform=macOS' test` completo e `git diff` varrido (sem SQL interpolado, sem `print` sensível, sem credenciais, sem ficheiros novos por registar no alvo).
- [x] 2.12 Documentação: `Docs/architecture/TECHNICAL_DESIGN.md`, `Docs/architecture/ARCHITECTURE.md`, `Docs/architecture/SYSTEM_DESIGN.md`, `README.md`, `Docs/development/TESTING.md` e `Docs/planning/PLAN.md` esvaziado.

## Correções pós-teste

- [x] `Views/Admin/AdminView.swift` — cartão herói deixava um vazio grande entre o rótulo e o valor (o `Spacer` + `maxHeight: .infinity` esticavam-no à altura da grelha ao lado). Removidos: o cartão passa a ter a altura do seu conteúdo. Prova: `xcodebuild ... build` + ecrã.
- [x] `POSAppTests/AdminStatsTests.swift` — os helpers `user`/`sale` do `@Suite` novo eram `static` e estavam a ser chamados sem `Self.` ("static member 'user' cannot be used on instance"), e a soma inline das duas listas rebentava o type-checker. Prefixadas com `Self.` e as somas passadas para variáveis `Double`. Prova: `123 tests in 28 suites passed`.
- [x] Prova por mutação (V3): inverter a ordenação de `cashierPerformance` deixa vermelho o teste "Ordena do maior total para o menor" (`["Ana", "Bruno"] == ["Bruno", "Ana"]` falha); guarda reposta e suite outra vez verde.

---

# Ronda 3 — seletor de gráfico no Dashboard (pedido do utilizador)

O painel do gráfico passa a ter um seletor: "Receita" (evolução no tempo, como está)
ou "Vendas por caixa" (barras, quem vendeu mais no período). O painel de linhas
"Vendas por caixa" desaparece — a mesma informação passa a ser gráfico dentro do
seletor, em vez de existir duas vezes.

## PARTE 1 — BACKEND

- [x] 1.1 Nada a fazer: `AdminViewModel.cashierPerformance(in:)` e `revenueSeries(in:)` já existem e já estão testados (`POSAppTests/AdminStatsTests.swift`). Ecrã só de leitura, sem entrada nova do utilizador — sem validação nova para `SECURITY.md` §11.

## PARTE 2 — FRONTEND

- [x] 2.1 `Docs/planning/PLAN.md` — plano de UX do seletor, antes de tocar na View.
- [x] 2.2 `Views/Admin/AdminDashboardView.swift` — `enum ChartKind { receita, caixas }` em `@State`, seletor segmentado no topo do painel do gráfico, com `.animation` e respeito por `Reduce Motion`.
- [x] 2.3 `Views/Admin/AdminDashboardView.swift` — gráfico de barras horizontais das caixas (`BarMark`, valor por caixa, rótulo com nome), estado de vazio em PT e `accessibilityLabel`.
- [x] 2.4 `Views/Admin/AdminDashboardView.swift` — remover o painel de linhas "Vendas por caixa" da coluna principal (passou a ser o segundo gráfico do seletor).
- [x] 2.5 V4 — fluxo real, **por conferir no ecrã**: alternar os dois gráficos nos quatro períodos, com e sem vendas, janela larga e estreita, claro e escuro, perfis Admin e Caixa.
- [x] 2.6 V5 — regressão: `xcodebuild -scheme Sales_Project -destination 'platform=macOS' test` e `git diff` varrido.
- [x] 2.7 Documentação: `Docs/architecture/SYSTEM_DESIGN.md`, `Docs/architecture/TECHNICAL_DESIGN.md`, `Docs/architecture/ARCHITECTURE.md`, `README.md` e `Docs/planning/PLAN.md` esvaziado.

---

# Ronda 4 — os seis indicadores a ocupar a largura (pedido do utilizador)

Os seis cartões de indicador (Receita + ticket médio, artigos, stock, risco, perda)
deixavam buraco na última linha: a grelha `.adaptive(minimum: 170)` ao lado do cartão
herói de largura fixa dava 3+2 e sobrava espaço. Passam a ser uma grelha única de
colunas iguais, com contagem que divide 6 sem resto (3 · 2 · 1).

## PARTE 1 — BACKEND

- [x] 1.1 Nada a fazer — mudança só de layout, sem dados novos e sem entrada do utilizador.

## PARTE 2 — FRONTEND

- [x] 2.1 `Docs/planning/PLAN.md` — plano de UX da grelha, antes de tocar na View.
- [x] 2.2 `Views/Admin/AdminDashboardView.swift` — `kpiBlock` passa a `ViewThatFits` de três grelhas de colunas iguais (3 · 2 · 1 colunas, `GridItem(.flexible(minimum: 170))`), com a Receita como primeiro cartão. Sem buracos na última linha em nenhuma largura.
- [x] 2.3 `Views/Admin/AdminView.swift` — `AdminKPICard` estica à altura da linha (`maxHeight: .infinity`) para os cartões da mesma linha ficarem com o mesmo plano de vidro, sem o vazio que o `Spacer` dava na ronda anterior.
- [x] 2.4 V4 — fluxo real, **por conferir no ecrã**: janela larga (3 colunas), média (2) e estreita/iPhone (1), claro e escuro.
- [x] 2.5 V5 — regressão: `xcodebuild ... test` e `git diff` varrido.
- [x] 2.6 Documentação: `Docs/architecture/TECHNICAL_DESIGN.md`, `Docs/architecture/ARCHITECTURE.md`, `README.md` e `Docs/planning/PLAN.md` esvaziado.

## 2026-08-19 — Ecrã de login redesenhado — painel dividido, Liquid Glass, animação de entrada, de recusa e de transição

## Ciclo — UX do ecrã de login (Liquid Glass + animação de entrada, rejeição e transição)

Referências visuais consultadas: `../Ideas/Swift UI idea/src/login/` (painel dividido: marca à esquerda, formulário à direita, plano único de vidro, fundo com profundidade).

# PARTE 1 — BACKEND

- [x] 1.1 `Utils/Constants.swift` — limites de entrada de credenciais: `usernameMaxLength = 64`, `passwordMaxLength = 128`.
- [x] 1.2 `ViewModels/AuthViewModel.swift` — V1/V2: recusar entrada hostil em `login()` **antes** de tocar na base de dados: username vazio/só espaços, acima de 64 caracteres, com caracteres de controlo (`\n`, `\r`, `\t`, `\0`); password vazia ou acima de 128 caracteres. Mensagem única `"Credenciais inválidas."` (não revela qual falhou). Username passa a ser lido com `trimmingCharacters`.
- [x] 1.3 `ViewModels/AuthViewModel.swift` — `@Published var loginFailureCount: Int`, incrementado em **toda** a rejeição (entrada hostil, credenciais erradas, bloqueio). É o gatilho da animação de rejeição na UI; não guarda nada sensível.
- [x] 1.4 V3 — testes em `POSAppTests/PasswordHashTests.swift`: bateria hostil de login (username 100 caracteres recusado, password 200 caracteres recusada, caracteres de controlo recusados, espaços à volta do username aceites, `loginFailureCount` incrementa). Prova por mutação: retirar o guarda de comprimento e ver vermelho.
- [x] 1.5 V3 — `Docs/development/TESTING.md`: atualizar a linha de índice §2 de `PasswordHashTests`.

# PARTE 2 — FRONTEND

- [x] 2.1 `Docs/planning/PLAN.md` — plano de UX escrito antes de tocar na View (STYLE_GUIDE §0.1).
- [x] 2.2 `Views/LoginView.swift` — redesenho: painel dividido em ecrã largo (marca à esquerda, formulário à direita), coluna única em ecrã estreito/iOS; fundo `MeshGradient` com deriva lenta; **um só plano de vidro** (o cartão do formulário) dentro de `GlassEffectContainer`; tipografia semântica (Dynamic Type); campos com 44 pt de alvo; `onSubmit` encadeia utilizador → password → entrar.
- [x] 2.3 `Views/LoginView.swift` — animação de entrada quando a app abre: marca e cartão entram escalonados (opacidade + deslocamento + escala).
- [x] 2.4 `Views/LoginView.swift` — animação de rejeição no ecrã inteiro: `keyframeAnimator` com abanão horizontal + clarão vermelho, disparado por `loginFailureCount`. Com `Reduce Motion` fica só o clarão, sem abanão.
- [x] 2.5 `Views/POSAppApp.swift` — `RootView` novo com a troca animada Paywall ↔ Login ↔ MainView: saída do login com escala para dentro + desfoque, entrada do painel com escala para fora. Respeita `Reduce Motion`.
- [x] 2.6 V4 — fluxo real: abrir a app, falhar o login (ver abanão + banner), entrar com Admin e com Caixa (ver transição), primeiro arranque sem utilizadores (criação de Admin), claro e escuro, janela estreita e larga.
- [x] 2.7 Checklists: `Docs/security/SECURITY.md` §10 e `Docs/development/STYLE_GUIDE.md` §15.
- [x] 2.8 Documentação: `Docs/security/SECURITY.md` §11 (R18), `Docs/architecture/ARCHITECTURE.md`, `Docs/architecture/SYSTEM_DESIGN.md`, `Docs/architecture/TECHNICAL_DESIGN.md`, `README.md`.
- [x] 2.9 V5 — regressão: suite completa outra vez + `git diff` varrido (SQL interpolado, `print` sensível, credenciais em claro).
- [x] 2.10 Esvaziar o `Docs/planning/PLAN.md` depois da UI implementada.

## V4 — o que ficou provado no ecrã e o que falta conferir

Provado com a app a correr (macOS, tema escuro, janela larga):

- arranque com entrada escalonada e layout dividido;
- `Tab` encadeia utilizador → password, anel de foco visível;
- credenciais erradas: banner `Credenciais inválidas.` e foco devolvido à password.

Por conferir à vista (não dá para provar por captura — são fotogramas de meio segundo
ou dependem de credenciais/ambiente):

- fotogramas do abanão e do clarão vermelho;
- transição login → painel com utilizador válido, com perfil Admin e com perfil Caixa;
- tema claro, janela estreita (coluna única) e iOS;
- `Reduce Motion` ligado.

## 2026-08-19 — Login a recusar credenciais certas — sqlite3_bind_text com SQLITE_STATIC (E23)

## Ciclo — login recusa credenciais certas de vez em quando

Sintoma relatado: com utilizador e password corretos, o login falha **às vezes**.

# PARTE 1 — BACKEND

- [x] 1.1 `Database/DatabaseManager.swift` — causa raiz: as 54 chamadas `sqlite3_bind_text(..., (x as NSString).utf8String, -1, nil)` passam `SQLITE_STATIC`, prometendo que o ponteiro vive até ao `sqlite3_step`. O ponteiro é de uma `NSString` temporária (autoreleased) e pode ser libertado antes disso — o valor ligado passa a lixo. No login, o `SELECT ... WHERE username = ?` deixa de encontrar a linha e a resposta é `Credenciais inválidas.` com a password certa. Correção numa só camada: constante `SQLITE_TRANSIENT` (SQLite copia o texto durante a chamada) aplicada a **todas** as ligações de texto do ficheiro.
- [x] 1.2 V3 — teste em `POSAppTests/PasswordHashTests.swift`: `fetchUserByUsername` repetido 60 vezes, com pressão de autorelease pelo meio, tem de devolver sempre o mesmo utilizador; e `login()` com credenciais certas repetido tem de entrar sempre.
- [x] 1.3 V3 — `Docs/development/TESTING.md`: atualizar a linha de índice §2.
- [x] 1.4 `Docs/development/ERRORS.md` — entrada com sintoma, causa, solução e prova + linha na tabela de índice §1.

# PARTE 2 — FRONTEND

- [x] 2.1 `Views/LoginView.swift` — no iOS, com "mostrar password" ligado o campo passa a `TextField` e apanha maiúscula automática e correção do teclado: a password escrita deixa de ser a que o utilizador quer. Desligar `textInputAutocapitalization` e `autocorrectionDisabled` nos campos de password.
- [x] 2.2 V4 — entrar com credenciais certas várias vezes seguidas; confirmar que o bloqueio de 5 tentativas continua a dizer os segundos que faltam.
- [x] 2.3 V5 — suite completa + `git diff` varrido.
- [x] 2.4 Documentação: `Docs/architecture/ARCHITECTURE.md` (dívida/regra de ligação de valores) e `Docs/security/SECURITY.md` (regra: ligar texto sempre com `SQLITE_TRANSIENT`).

## Nota de prova (V3)

O teste de repetição (60 consultas com churn de autorelease) **não** apanha o defeito: fica
verde com o `nil` reposto, porque o erro depende de quando o autorelease pool esvazia. Ficou
na suite como teste de comportamento, mas a guarda que prova a correção é determinista — o
teste que lê `Database/DatabaseManager.swift` e falha se alguma ligação de texto voltar a
passar `SQLITE_STATIC`. Mutação feita: `nil` reposto → vermelho na linha 337 → `SQLITE_TRANSIENT`
reposto → verde.

## Por conferir

- Confirmar no uso diário que a recusa intermitente desapareceu — o defeito não se reproduz à ordem.
