# Modernização do POSApp para o mercado moçambicano de mercearias e farmácias

**A tua app POS personalizada já tem duas vantagens que nenhum grande concorrente iguala: integração nativa com M-Pesa/e-Mola e zero mensalidades SaaS.** Mas uma análise comparativa com 9 plataformas POS principais revela **47 funcionalidades em falta** que os retalhistas modernos esperam. A conformidade fiscal (SAFT-MZ), sincronização offline-first, rastreio de validade, e fidelização de clientes são as adições de maior impacto. O mercado moçambicano — onde mais de 400.000 agentes de carteiras móveis superam os 33.191 terminais POS tradicionais e menos de 35% dos adultos têm conta bancária — exige uma arquitetura POS fundamentalmente diferente das soluções SaaS ocidentais. Este relatório mapeia todas as lacunas, prioriza por impacto no mercado e fornece caminhos técnicos específicos dentro do ecossistema Apple.

---

## Como a tua app se compara com 9 grandes plataformas POS

Uma comparação sistemática do Square, Shopify POS, Lightspeed, Toast, Clover, Vend, Loyverse, KORONA POS e sistemas focados em África (Yoco, DPO Group) revela que **todos os grandes concorrentes oferecem sincronização cloud, fidelização de clientes, alertas de stock baixo e motor de descontos/promoções** — quatro capacidades que a tua app não tem atualmente.

**O Loyverse é o teu concorrente mais próximo** e a ameaça mais perigosa. Oferece POS base gratuito, suporte em português, compatibilidade Android (dominante em África), modo offline, gestão multi-loja e programa de fidelização integrado. O ponto fraco: sem suporte nativo a dinheiro móvel e funcionalidades de farmácia limitadas. **O KORONA POS** lidera em inteligência específica de retalho com classificação ABC de inventário, ajustes automáticos de preço para manter margens, e analítica sofisticada de prevenção de furtos. **O Lightspeed** define o padrão de excelência para gestão de inventário multi-loja mas custa $89–$239/mês — proibitivo para pequenos negócios moçambicanos.

Nenhum sistema POS internacional suporta nativamente M-Pesa ou e-Mola. Este é o teu maior fosso competitivo. Combina-o com um **modelo de preço de compra única** (a preferência no mercado africano, onde o Smart POS Software em Moçambique já usa licenciamento vitalício) em vez de subscrições SaaS, e tens uma proposta de valor convincente.

As funcionalidades que faltam na tua app e que aparecem em 6+ dos 9 sistemas analisados:

- **Sincronização cloud com resiliência offline** (todos os 9 sistemas)
- **Perfis de clientes com histórico de compras** (todos os 9)
- **Programa de fidelização/recompensas** (7 de 9)
- **Alertas de stock baixo e pontos de reabastecimento automático** (todos os 9)
- **Motor de descontos e promoções** (todos os 9)
- **Suporte multi-loja** com painel centralizado (todos os 9)
- **Recibos eletrónicos** via SMS/email (todos os 9)
- **Ordens de compra e gestão de fornecedores** (6 de 9)
- **Controlo de horas de trabalho** dos funcionários (6 de 9)
- **Relatórios de margem de lucro e COGS** (6 de 9)

---

## A conformidade fiscal moçambicana é inegociável

**Esta é a área mais crítica a resolver.** A Autoridade Tributária de Moçambique (MTA) exige que todo o software de faturação seja certificado antes da implementação, e o incumprimento acarreta penalidades incluindo bloqueio de conta durante 5 dias impedindo a emissão de novas faturas.

**Taxas de IVA atuais a partir de janeiro de 2026:** A taxa normal é de **16%** (reduzida de 17% em 2023). Uma **taxa reduzida de 5%** aplica-se a serviços privados de saúde e educação. Exportações são isentas com taxa zero. Açúcar, óleos alimentares e sabões estiveram isentos até dezembro de 2025 (verificar prorrogação).

Cada fatura deve incluir estes campos obrigatórios segundo o Artigo 27 do Código do IVA:

- Numeração sequencial ininterrupta dentro de cada série
- Nome/NUIT/morada do fornecedor
- Nome/NUIT do cliente (quando disponível)
- Quantidades discriminadas com preços unitários sem imposto
- Taxa(s) de IVA aplicáveis mostradas separadamente
- Montantes de IVA discriminados por taxa
- Base legal citada para itens isentos
- Total com IVA
- Língua portuguesa
- Moeda Metical Moçambicano (MZN)

**A comunicação mensal de dados de faturas tornou-se obrigatória em maio de 2025.** Todos os contribuintes registados no IVA devem carregar um ficheiro contendo todas as faturas emitidas no mês anterior em **edeclaracao.at.gov.mz**. Os dados obrigatórios incluem datas de transação, identificação das partes, descrição de bens/serviços, valores unitários e totais, e montantes de IVA.

**O SAF-T Moçambique (SAFT-MZ)** visa implementação completa em 2026. Este ficheiro XML de auditoria padrão OCDE deve incluir dados de faturação, dados de compras, dados de auto-faturação e tags de despesas salariais. A tag salarial deve corresponder ao salário bruto no registo de vencimentos — uma variação superior a 3% desencadeia uma auditoria. Os developers devem contactar diretamente a MTA em **saft-mz.com** para especificações técnicas e certificação completa.

**Notas de crédito** requerem a sua própria série de numeração sequencial (ex: NC 2026/0001), devem referenciar o número e data da fatura original, conter todos os campos obrigatórios do Artigo 27, e reverter o IVA original. Faturas originais nunca podem ser eliminadas ou modificadas — correções apenas via notas de crédito. Ambos os documentos devem ser retidos durante **10 anos**.

Alterações legislativas recentes aceleram a conformidade digital. A Lei 10/2025 (em vigor desde janeiro de 2026) traz explicitamente bens/serviços digitais e transações de carteiras móveis para a base do IVA, revoga os regimes simplificado e de isenção do IVA, estende o processamento de reembolsos de IVA para 150 dias, e introduz um limite de 10 anos para créditos de IVA a montante.

**Ações imediatas:**

1. Contactar a MTA para iniciar a certificação do software
2. Construir capacidade de exportação XML SAF-T
3. Implementar numeração sequencial inviolável com cadeias de hash (seguindo o modelo fiscal de origem portuguesa)
4. Desenhar arquitetura de retenção de dados de 10 anos

---

## Fidelização de clientes e CRM colmatam a maior lacuna percetível

Todos os concorrentes exceto os mais básicos incluem gestão de clientes. Para o mercado moçambicano de mercearias e farmácias, onde a **cultura da "caderneta" (fiado)** está profundamente enraizada no pequeno comércio, digitalizar relações com clientes é transformador.

**Os perfis de clientes devem ser indexados por número de telefone** — não por email. A penetração móvel de 77% de Moçambique versus baixa adoção de email torna o telefone o identificador natural. Armazenar: nome, telefone, NIF, histórico de compras, gasto total, frequência de visitas, valor médio de transação, produtos preferidos, notas personalizadas e saldo de crédito pendente.

### Motor de pontos configurável

- Taxa de acumulação por MZN gasto (ajustável por produto/categoria)
- 3–5 níveis auto-atribuídos com base no gasto acumulado
- Pontos utilizáveis como método de pagamento no checkout
- Eventos promocionais de pontos duplos e bónus de boas-vindas
- Cartões de fidelização com código de barras imprimível (importante onde a adoção de smartphones é menor)
- Pesquisa por número de telefone no checkout

### Motor de promoções

- Percentagem de desconto e valor fixo de desconto
- BOGO (quantidades X e Y configuráveis)
- Preços escalonados por quantidade
- Ativação/desativação automática programada
- Targeting por categoria ou produto
- Regras anti-acumulação

### Gestão de crédito/fiado do cliente

- Contas correntes com limites de crédito configuráveis por cliente
- Condições de pagamento (semanal/mensal)
- Geração periódica de extratos
- Relatórios de antiguidade de dívidas
- Alertas automáticos quando clientes se aproximam dos limites de crédito
- Crédito de loja emitido a partir de devoluções rastreado separadamente com data de expiração opcional

### Comunicação

**SMS (não email) é o canal para Moçambique.** Enviar recibos de transação, saldos de pontos de fidelização, mensagens promocionais para segmentos de clientes, saudações de aniversário, lembretes de reabastecimento (farmácia), e ofertas de recuperação de clientes inativos. A integração com WhatsApp adiciona um segundo canal para entrega de recibos e alertas de stock.

---

## Gestão de inventário precisa de upgrade de nível farmacêutico

O teu CRUD básico atual com código de barras e níveis de stock cobre talvez 30% do que a gestão de inventário moderna exige. A lacuna é mais aguda para operações de farmácia, onde o **rastreio de validade é a funcionalidade de maior impacto** — estudos mostram que a gestão automatizada de validades reduz a dispensa de medicamentos expirados em até 99%.

### Rastreio de validade com FEFO (First Expired, First Out)

Obrigatório em cada receção de stock. Alertas multi-nível:

- **6 meses** antes da expiração → sinalizar para preço promocional
- **3 meses** → considerar devolução ao fornecedor
- **1 mês** → crítico — remover da venda ativa ou desconto agressivo
- **Expirado** → bloqueio automático de venda, solicitar abate

Cada listagem de produto deve mostrar estado de validade codificado por cores: verde, amarelo, vermelho.

### Rastreio por lote

Atribui um identificador único a cada lote de entrega, armazenando número de lote, data de fabrico, data de validade, fornecedor, quantidade e custo. Cada venda liga-se ao lote específico dispensado. Permite rastreabilidade de recolha de produtos — quando um fabricante emite uma recolha por número de lote, o sistema identifica instantaneamente o stock afetado e quais clientes o receberam. Embalagens farmacêuticas modernas usam códigos de barras GS1 2D DataMatrix que codificam código de produto, número de lote, data de validade e número de série — digitalizar estes deve preencher automaticamente os dados do lote.

### Gestão de ordens de compra

Ciclo completo: Rascunho → Enviada → Parcialmente Recebida → Totalmente Recebida → Fechada. O workflow de receção deve suportar leitura de código de barras para verificar itens contra a OC, registando discrepâncias. A receção parcial é essencial — os desafios logísticos de Moçambique fazem com que entregas cheguem frequentemente incompletas. Gerar OCs como PDF para partilha via WhatsApp/SMS com fornecedores. Auto-gerar OCs em rascunho agrupadas por fornecedor quando produtos atingem pontos de reabastecimento.

### Sistema de reabastecimento

Começar com Min/Max (quando o stock desce abaixo do mínimo, encomendar até ao máximo) e depois adicionar reabastecimento baseado em consumo que considere stock atual, quantidades comprometidas, stock em trânsito, OCs abertas, mínimos do fornecedor e prazos de entrega. Para as cadeias de fornecimento voláteis de Moçambique, o rastreio de prazos de entrega por fornecedor é crítico.

### Contagens de inventário

Tanto contagem física completa (anual) como contagem cíclica (subconjuntos rotativos, com itens de alto valor contados mais frequentemente segundo classificação ABC). Workflow: iniciar contagem → gerar folhas de contagem → digitalizar/introduzir contagens → rever relatório de variância → aprovar ajustes com códigos de motivo (dano, furto/quebra, erro de registo, deterioração, expiração). Rastreio de desperdício/dano regista cada ajuste com código de motivo, quantidade, foto opcional e membro da equipa.

### Rastreio de custos

Custo Médio Ponderado (recalcular custo médio cada vez que novo stock é recebido). Rastrear COGS por produto, gerar relatórios de valorização de inventário, e calcular taxas de rotação. O ajuste automático de preço de retalho do KORONA — que atualiza automaticamente preços com base em alterações de custo para manter margens mínimas de lucro — é uma funcionalidade que vale replicar para a economia moçambicana propensa a inflação.

---

## Módulos verticais: Farmácia e Mercearia

### Prioridades do módulo de farmácia

- **Gestão simplificada de prescrições** — ligar vendas a números de referência de prescrição com nome e número de registo do prescritor
- **Perfis de pacientes** — nome, contacto, idade, alergias como texto livre, ligados ao histórico completo de compras
- **Rastreio de reabastecimento** para medicação crónica com lembretes SMS
- **Substâncias controladas** — registo reforçado: identidade do comprador, quantidade, data/hora e membro da equipa para cada venda, com limites de quantidade configuráveis por transação/cliente/período
- **Sugestões de substituição genérica** — mapear produtos de marca para alternativas genéricas com comparação de preços no ecrã do POS

### Prioridades do módulo de mercearia

- **Preço por peso** — introdução manual de peso (caixa digita peso, sistema calcula preço = peso × preço unitário por kg), depois integração com balança Bluetooth/USB (protocolos CAS, Mettler Toledo, DIGI)
- **Gestão de tara** — subtrai peso do contentor com valores de tara comuns armazenados mais introdução manual
- **Códigos PLU (Price Look-Up)** — códigos numéricos curtos para itens sem código de barras, com pesquisa visual por imagens de produtos
- **Botões de venda rápida** — grelha touchscreen configurável com botões grandes, coloridos e baseados em imagem organizados por separadores de departamento (Padaria, Talho, Frutas & Legumes, Bebidas, Limpeza), predefinidos com os 20–30 itens mais vendidos
- **Promoções programadas** com ativação/desativação automática para promoções semanais e descontos de fim de dia em perecíveis
- **Verificação de idade** para álcool e tabaco com flag e override do gerente

---

## Analítica orientada à decisão

### Painel de KPIs em tempo real (ecrã inicial)

- Total de vendas de hoje
- Contagem de transações
- Valor médio do cesto
- Top 5 produtos
- Repartição por método de pagamento (dinheiro vs. dinheiro móvel vs. cartão)
- Alertas de inventário
- Usar WidgetKit para mostrar métricas-chave fora da app

### Análise ABC

Classifica automaticamente produtos em classe A (top 80% da receita, menos itens), classe B (próximos 15%) e classe C (últimos 5%, mais itens). Orienta prioridade de reabastecimento, alocação de espaço de prateleira e identificação de stock morto. Rastrear produtos à medida que mudam entre classes.

### Análise de horas de pico

Heatmap de vendas por hora e dia da semana para otimização de pessoal. Sobrepor horários de funcionários contra volume de vendas para identificar períodos com excesso ou défice de pessoal. Estudos mostram **22% de melhoria nas vendas por hora de trabalho** através de otimização da força de trabalho.

### Métricas de desempenho de funcionários

- Vendas por funcionário
- Valor médio de transação
- Itens por transação
- Devoluções/anulações por funcionário (deteção de fraude)
- Frequência de descontos
- Rácio de produtividade vendas-por-hora
- Indicadores semáforo (verde/amarelo/vermelho)

### Análise de margem de lucro

Por produto e categoria, com cálculo de GMROI (Retorno de Margem Bruta sobre Investimento). Taxas de rotação de inventário e projeções de dias-de-stock-restante. Retalhistas que usam dados POS para estratégias de preço veem **14,5% de melhoria média na margem de lucro**.

---

## Devoluções, reembolsos e trocas

### Workflow de devolução

1. Pesquisar a transação original (por número de recibo, código de barras, data ou cliente)
2. Selecionar itens e quantidades específicas a devolver
3. Seleção obrigatória de motivo de devolução
4. Escolher método de reembolso (método de pagamento original ou crédito de loja)
5. Opcionalmente repor itens em stock (com estado de inspeção para bens danificados)
6. Gerar nota de crédito com numeração sequencial

### Transações de troca

Combinam devolução e nova venda: itens devolvidos como linhas negativas, novos itens como positivos, sistema calcula total líquido. Um único recibo documenta toda a troca.

### Prevenção de fraude em devoluções

- Verificação de recibo cruzando devoluções com vendas originais
- Devoluções sem recibo → crédito de loja ao preço mais baixo recente com aprovação do gerente
- Alertas de frequência de devoluções por cliente (ex: >3 devoluções em 30 dias)
- Monitorização de taxa de devolução por produto
- Rastreio de atividade de reembolso por funcionário
- Montantes máximos de reembolso com PIN de autorização do gerente

### Permissões granulares

Expandir para além de admin/caixa para pelo menos 18 permissões toggleáveis em 4–5 níveis (Proprietário > Gerente > Caixa Sénior > Caixa > Auxiliar de Stock). Gates críticos: processar reembolsos, aplicar descontos (com percentagem máxima configurável), anular transações, abrir gaveta de dinheiro, gerir preços e exportar dados.

---

## Reconciliação de pagamentos e dinheiro móvel

### Reconciliação de fim de dia

Verificação tripla: totais POS registados por método de pagamento ↔ contagem física de dinheiro ↔ registos de liquidação bancária/dinheiro móvel. Cada método de pagamento precisa da sua própria linha:

- Dinheiro esperado (vendas menos troco dado)
- Total de lote de cartão versus liquidação do processador
- Confirmações de transação M-Pesa versus registos POS
- Confirmações e-Mola versus registos POS
- Taxas do processador rastreadas separadamente

### Sistema de Pagamento Instantâneo de Moçambique

Lançado a 10 de março de 2026 via SIMO, conecta bancos e carteiras digitais para transferências instantâneas 24/7 com limites de **200.000 MZN/dia para particulares e 500.000 MZN/dia para empresas**. Integrar cedo dá vantagem competitiva que nenhum POS existente suporta.

### Pagamentos por código QR

Dois padrões: apresentado pelo comerciante (POS gera QR dinâmico, cliente digitaliza com app de carteira) e apresentado pelo cliente (cliente mostra QR, POS digitaliza via câmara). O e-Mola já suporta pagamentos QR incluindo digitalização de QR a partir da galeria de fotos.

### Compra a prestações (Layaway)

Serve consumidores moçambicanos sensíveis ao preço: cliente seleciona itens, faz depósito (10–50%), itens reservados, plano de pagamento rastreia prestações, bens libertados após pagamento completo. Cada depósito gera recibo; fatura final emitida quando todos os pagamentos concluídos.

---

## Arquitetura de sincronização offline-first usando CKSyncEngine

O caminho técnico ótimo é **GRDB.swift (ou SQLite.swift) + CKSyncEngine** — preservando o investimento existente em SQLite enquanto ganhas a infraestrutura de sincronização mais recente da Apple. SwiftData até 2025 continua a ser mais lento que Core Data, com demasiado acoplamento entre persistência e UI, e instável. O CKSyncEngine, introduzido na WWDC 2023, alimenta a própria app Freeform da Apple.

### Resolução de conflitos POS

O cenário crítico — dois dispositivos a vender o último item em simultâneo — exige resolução baseada em operações. Armazenar **deltas de inventário** (ex: "−1 item vendido") em vez de contagens absolutas de stock. Na sincronização, somar todos os deltas para computar stock atual. Esta abordagem inspirada em CRDT previne vendas duplas. Transações de venda usam deduplicação baseada em UUID append-only.

### Padrão de arquitetura

```
SwiftUI Views → ViewModels (@Observable/@MainActor)
        ↓
   Repositories (CRUD em SQLite via GRDB)
        ↓
   SyncEngine (ponte SQLite ↔ CloudKit via CKSyncEngine)
```

- Usar `NWPathMonitor` para detetar mudanças de conectividade e disparar sincronização
- Persistir `CKSyncEngine.State.Serialization` localmente para rastrear progresso
- CKRecordZones dedicadas por domínio de dados (Produtos, Vendas, Clientes)
- Migração faseada: manter SQLite existente → adicionar GRDB.swift → adicionar CKSyncEngine

---

## Segurança: correções imediatas

### Substituir SHA256 (URGENTE)

SHA256 é um hash rápido para integridade de dados, não para passwords — atacantes fazem força bruta a biliões de tentativas por segundo. Substituir por **PBKDF2 via CommonCrypto** (integrado nas plataformas Apple) com 600.000 iterações (OWASP). Migração: no primeiro login bem-sucedido com hash antigo, re-fazer hash com PBKDF2 e adicionar coluna `hashVersion`.

### Keychain em vez de SQLite para credenciais

O Keychain fornece encriptação AES-256-GCM, armazenamento via Secure Enclave, persistência entre reinstalações, e acesso biométrico. Combinar com `LocalAuthentication` para Touch ID/Face ID.

### Encriptação da base de dados

SQLCipher (encriptação AES-256 transparente como substituto do SQLite) com chave no Keychain. Nunca codificar chaves no código.

### Logging de auditoria

Tabela append-only: login/logout, cada transação com ID do funcionário, anulações/reembolsos com motivo, aberturas de gaveta, descontos, overrides de preço, ajustes de inventário. Sincronizar via CloudKit. Suporta o requisito de 10 anos de retenção.

### PCI DSS

Nunca armazenar, processar ou transmitir números de cartão. Encaminhar pagamentos por cartão através de PSP compatível PCI (Stripe Terminal, Square). Apple Pay elimina completamente o âmbito PCI.

---

## Padrões UX modernos para POS

### Atalhos de teclado (SwiftUI `.keyboardShortcut()`)

- ⌘N → Nova venda
- Enter → Adicionar ao carrinho
- ⌘P → Processar pagamento
- ⌘⌫ → Anular último item
- ⌘F → Pesquisar produtos
- ⌘⇧D → Abrir gaveta

No iPad com teclado externo, ⌘ pressionado mostra todos os atalhos.

### Layout

NavigationSplitView de 3 colunas: sidebar de categorias | grelha de produtos | carrinho/checkout. `@Environment(\.horizontalSizeClass)` para adaptar iPad/Mac. Stage Manager via `UISupportsMultipleWindows` no Info.plist. Alvos de toque mínimo **44pt**.

### Apple ecosystem

- **WidgetKit** — receita de hoje, transações, alertas de stock no Home Screen
- **Live Activities** (iPadOS 17+) — sessão de venda ativa no Lock Screen
- **VisionKit DataScannerViewController** — leitura de código de barras via câmara sem hardware externo
- **Apple Wallet** (PKPassLibrary) — cartões de fidelização e recibos digitais com push updates
- **AirPrint** — impressão de recibos nativa; impressoras térmicas via SDKs (Star Micronics, Epson iOS SDK)

---

## O que o mercado africano realmente exige

Sintetizando feedback do Reddit, Capterra, G2, e investigação do mercado africano, as funcionalidades mais pedidas são:

1. **Modo offline robusto com sincronização automática** (#1 para mercados em desenvolvimento; cloud híbrido a 18,3% CAGR até 2033)
2. **Gestão de inventário avançada** com alertas de validade e reabastecimento automatizado
3. **Suporte multi-pagamento** incluindo dinheiro móvel, pagamentos divididos e QR
4. **UI intuitiva exigindo formação mínima** ("Treinámos o pessoal em 30 minutos" é o benchmark)
5. **Relatórios abrangentes** acessíveis remotamente

**Requisitos específicos de Moçambique:**

- Banco de Moçambique exige que POS usem o sistema financeiro nacional (plataformas estrangeiras proibidas)
- Língua portuguesa essencial
- Modelo de compra única fortemente preferido sobre subscrições
- Cortes de energia → bateria do iPad como vantagem natural
- Internet instável fora das grandes cidades → offline-first é obrigatório

---

## Roteiro priorizado

### Fase 1 — Conformidade fiscal e lacunas críticas (BLOQUEADORES)

- Certificação do software MTA
- Exportação SAFT-MZ
- Formatação correta de faturas (Artigo 27)
- Migração SHA256 → PBKDF2
- Credenciais no Keychain
- Numeração sequencial com hash chain

### Fase 2 — Paridade competitiva

- Rastreio de validade/lotes
- Perfis de clientes com pontos de fidelização
- Motor de promoções
- Ordens de compra com gestão de fornecedores
- Sincronização multi-dispositivo (CKSyncEngine)

### Fase 3 — Diferenciação de mercado

- Preço por peso
- Rastreio de prescrições farmacêuticas
- Análise ABC
- Métricas de desempenho de funcionários
- Workflow completo de devoluções/notas de crédito

### Fase 4 — Funcionalidades de crescimento

- Suporte multi-loja
- Previsão de procura com IA
- Integração com Sistema de Pagamento Instantâneo de Moçambique
- Passes de fidelização Apple Wallet

---

## Posicionamento competitivo

A tua app como **POS offline-first, nativo em dinheiro móvel, de compra única, construído especificamente para mercearias e farmácias moçambicanas** endereça todos os pontos de dor em que as plataformas POS internacionais falham neste mercado. A combinação de integração M-Pesa/e-Mola, língua portuguesa, conformidade fiscal MTA, e resiliência da bateria do iPad durante cortes de energia cria uma posição competitiva defensável que nem o Loyverse nem qualquer plataforma SaaS internacional consegue replicar facilmente.