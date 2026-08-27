# CLAUDE.md — Regras obrigatórias do projeto Sales POS

Estas regras são **obrigatórias** e sobrepõem-se a qualquer comportamento por omissão.
Antes de escrever uma única linha de código, ler: `Docs/TODO.md`, `Docs/architecture/ARCHITECTURE.md`, `Docs/security/SECURITY.md`, `Docs/security/SECURITY_POLICY.md`, `Docs/development/STYLE_GUIDE.md`, `Docs/development/TESTING.md`, `Docs/development/ERRORS.md`, `Docs/database/DATABASE.md`.

---

## 1. TODO.md manda em tudo

`Docs/TODO.md` é a fonte única do trabalho. Regras:

1. **Antes de qualquer alteração ao projeto, escrever primeiro a tarefa no `Docs/TODO.md`.** Vale para tudo, sem exceção de tamanho: funcionalidade nova, bug, refactor, mudança de uma linha, ajuste de texto, cor, espaçamento, renomear variável ou mexer num `.md`. **Não existe alteração "pequena de mais" para o TODO** — se toca no projeto, escreve-se primeiro no `Docs/TODO.md` e só depois se codifica. Nunca começar a codificar sem a tarefa estar escrita.
2. **É obrigatório terminar as tarefas pendentes do `Docs/TODO.md` antes de começar seja o que for de novo.** Nada novo enquanto houver `[ ]` por fechar.
3. Se aparecer trabalho novo a meio (ideia, bug, pedido), **não o fazer agora** — acrescentar ao `Docs/TODO.md` para ser feito depois, pela ordem.
4. Marcar `[x]` cada item assim que fica realmente feito (compila e funciona), não antes.
5. **Quando tudo o que está no `Docs/TODO.md` estiver implementado, é obrigatório testar antes de fechar o ciclo:**
   - compilar o projeto (`xcodebuild`) e correr os testes;
   - testar na prática os fluxos que as tarefas tocaram;
   - se algo falhar, **corrigir**;
   - **cada correção feita é escrita no `Docs/TODO.md`** — nova linha em secção `## Correções pós-teste`, com o ficheiro tocado, marcada `[x]` quando corrigida e re-testada;
   - repetir compilar → testar → corrigir até tudo passar. Só depois se aplica a regra 6.
6. **O ciclo fecha-se sozinho: assim que todas as tarefas do `Docs/TODO.md` estiverem `[x]` (incluindo as correções pós-teste), transferir o texto para o `Docs/CHANGELOG.md` — sem esperar por pedido do utilizador e sem perguntar.** Enquanto sobrar um `[ ]`, não se escreve nada no `CHANGELOG.md`.
7. **Fecho do ciclo (automático, pela regra 6, ou quando o utilizador pedir):**
   - criar/abrir `Docs/CHANGELOG.md`;
   - mover **todo** o texto do `Docs/TODO.md` para o fim do `Docs/CHANGELOG.md`, sob um cabeçalho com a data (`## AAAA-MM-DD — <resumo>`);
   - **atualizar a tabela de índice no início do `Docs/CHANGELOG.md`** — ver secção 1.6.1;
   - apagar **apenas o texto** do `Docs/TODO.md` (o ficheiro fica, vazio, pronto para o ciclo seguinte).
   - Se sobrar sequer uma tarefa por fechar, **não** transferir nada.

### 1.6.1 — Índice do CHANGELOG.md

O `Docs/CHANGELOG.md` começa sempre com uma secção `## Índice`: tabela com uma linha por ciclo.

| Coluna | Conteúdo |
|---|---|
| `Data` | data do ciclo (`AAAA-MM-DD`) |
| `Título` | resumo do cabeçalho, sem a data |
| `Linha` | número da linha onde está o cabeçalho `## AAAA-MM-DD — ...` |
| `Ligação` | link Obsidian para o cabeçalho: `[[CHANGELOG#<cabeçalho completo>\|ir]]` (o `\|` do alias vai escapado, senão parte a tabela) |

Regras:

- **A tabela é recalculada por inteiro a cada escrita, nunca só acrescentada no fim.** Acrescentar um ciclo empurra o texto para baixo e muda o número de linha de **todos** os ciclos seguintes; todas as linhas da coluna `Linha` são reescritas.
- Verificar sempre depois de escrever: `grep -nE "^## [0-9]{4}-[0-9]{2}-[0-9]{2}" Docs/CHANGELOG.md` tem de dar exatamente os números que estão na tabela.
- Só entram na tabela os cabeçalhos de ciclo (`## AAAA-MM-DD — ...`), não os `##` internos que vieram do `TODO.md`.

### Estrutura obrigatória do TODO.md

Todo o `TODO.md` separa **backend** de **frontend**, e **backend vem sempre primeiro**:

```markdown
# PARTE 1 — BACKEND
(base de dados, modelos, ViewModels, serviços. Nada de UI aqui.)

# PARTE 2 — FRONTEND
(Views SwiftUI. Só arrancar depois da Parte 1 compilar e os testes passarem.)
```

Cada item indica o ficheiro que toca. Ordem de execução explícita (1.1 → 1.2 → ...).

---

## 2. Documentação — obrigações de atualização

| Aconteceu | Tem de atualizar |
|---|---|
| Funcionalidade nova, alterada ou removida | `README.md` (funcionalidades + estrutura do projeto) |
| Ficheiro novo, movido ou apagado | `README.md` (árvore da estrutura) |
| Tabela, coluna, índice, migração ou query estrutural nova/alterada | `Docs/database/DATABASE.md` |
| Camada, ViewModel, serviço, dependência, fluxo, ponto de entrada ou alvo novo/alterado | `Docs/architecture/ARCHITECTURE.md` |
| Qualquer fluxo, ecrã, componente, ViewModel, serviço ou protocolo **novo, alterado ou removido** | `Docs/architecture/SYSTEM_DESIGN.md` (**em Mermaid** — ver secção 9) |
| Qualquer ficheiro `.md` criado, renomeado ou apagado | `Docs/DOCUMENTATION.md` (índice) |
| **Validação nova aplicada a um campo ou função** | `Docs/security/SECURITY.md` §11 (registo de validações) |
| **Regra de segurança em falta, errada ou por afinar** | `Docs/security/SECURITY.md` (regra técnica) ou `Docs/security/SECURITY_POLICY.md` (processo/resposta) |
| **Teste novo ou alterado** | `Docs/development/TESTING.md` (tabela de índice §2) |
| **Erro encontrado a compilar, testar ou usar — e resolvido** | `Docs/development/ERRORS.md` (índice §1 + entrada com sintoma, causa, solução, prova) |

Regras adicionais:

- **Todos os `.md` vivem em `Docs/`** — as únicas exceções são `README.md` e `CLAUDE.md`, que ficam na raiz.
- **`Docs/` está organizado por área**, e um `.md` novo entra na subpasta certa (nome em maiúsculas, convenção de `NAME_MD.md`):

| Subpasta | Conteúdo |
|---|---|
| `Docs/` (raiz) | `DOCUMENTATION.md`, `TODO.md`, `CHANGELOG.md`, `PROJECT_OVERVIEW.md` |
| `Docs/architecture/` | `ARCHITECTURE.md`, `SYSTEM_DESIGN.md`, `TECHNICAL_DESIGN.md` |
| `Docs/database/` | `DATABASE.md` |
| `Docs/security/` | `SECURITY.md`, `SECURITY_POLICY.md` |
| `Docs/development/` | `STYLE_GUIDE.md`, `TESTING.md`, `ERRORS.md` |
| `Docs/features/` | documentação por funcionalidade (`FEATURE_*.md`, `INSTALL_*.md`) |
| `Docs/guides/` | `USER_GUIDE.md`, `UI_WIREFRAMES.md` |
| `Docs/planning/` | `ROADMAP.md`, `PLAN.md` (cache do plano de UX da UI em curso — ver secção 6.1) |

- **`Docs/DOCUMENTATION.md` é o índice de todos os `.md`.** É obrigatório indexar lá cada `.md`, no formato de tabela com link Obsidian `[[nome]]`.
- **`Docs/architecture/SYSTEM_DESIGN.md` cobre o sistema inteiro**, não só a partilha por proximidade: arquitetura geral, fluxo de venda, lotes/FIFO, alertas de validade, relatórios, subscrição e proximidade. Se uma tarefa acrescenta ou apaga um fluxo, esse diagrama é atualizado na mesma tarefa.
- **`Docs/architecture/` atualiza-se sempre e por inteiro.** Qualquer alteração ao programa obriga a percorrer **todos** os `.md` dessa pasta (`ARCHITECTURE.md`, `SYSTEM_DESIGN.md`, `TECHNICAL_DESIGN.md` e qualquer outro que lá esteja) e a atualizar os que ficaram desatualizados — não só os dois da tabela acima. Listar a pasta antes de fechar a tarefa; não presumir que se sabe o que lá está.
- Estas atualizações fazem parte da tarefa, não são um passo opcional a seguir: uma funcionalidade só está feita quando a documentação a reflete.

---

## 3. Segurança — `Docs/security/SECURITY.md` + `Docs/security/SECURITY_POLICY.md`

Dois documentos, um par obrigatório:

| Documento                          | Responde a                                                                                                                                    |
| ---------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| `Docs/security/SECURITY.md`        | **O que tem de estar no código** — ameaças, regras técnicas, catálogo de validações, cinco rondas, testes, auditoria, registo de validações   |
| `Docs/security/SECURITY_POLICY.md` | **Como o projeto garante a segurança e o que fazer quando existe uma falha** — portões, papéis, severidade, resposta a incidente, comunicação |

É obrigatório seguir as etapas de `Docs/security/SECURITY.md`: planeamento → desenvolvimento seguro → autenticação → autorização → proteção de dados → testes → monitorização → manutenção.

**As regras do `SECURITY.md` reforçam-se sempre, em toda a resposta e em todo o código** — não se assume que já estão sabidas nem se dá uma por dispensada porque "o valor é seguro" ou "é só um ecrã interno".

Na prática, em todo o código deste projeto:

- **SQL sempre com `sqlite3_prepare_v2` + `sqlite3_bind_*`.** Nunca interpolar strings em SQL — zero exceções, mesmo para valores "seguros".
- **Validar todas as entradas do utilizador** no ViewModel antes de chegar à base de dados (nome vazio, quantidade negativa, preço inválido, datas fora de gama).
- **Passwords só em hash.** Nunca guardar, registar (`print`/log) nem mostrar password em claro.
- **Autorização por perfil** (Admin / Caixa) verificada na camada de dados/ViewModel, não só escondendo botões na UI.
- **Nunca escrever dados sensíveis em logs**, mensagens de erro visíveis ou ficheiros exportados.
- Escritas com várias etapas (venda, fecho de caixa, migração) correm em **transação SQL** com `ROLLBACK` em caso de falha.
- Ficheiros exportados vão para diretorias da app; nada de caminhos escritos à mão fora da sandbox.

### 3.1 — Antes de implementar: testar a segurança da função

**Nenhuma função, ecrã ou janela nova começa a ser escrita sem a análise de obstáculos** (`SECURITY.md` §2.2.1). Antes do primeiro `func`, escrever, entrada a entrada: o que o campo aceita se ninguém o defender, o que **tem de ser recusado** e o que acontece se passar.

Os obstáculos essenciais, que nunca podem ser aceites (catálogo completo em `SECURITY.md` §2.2.2):

- **campo de número não aceita letras nem símbolos** (`abc`, `12a`, `€10`, `1e999`), nem `NaN`/`infinity`, nem negativo onde não faz sentido, nem `0` em preço ou quantidade de venda;
- **nome de pessoa não aceita dígitos nem símbolos**; nome de produto não aceita vazio, só espaços, só dígitos (`"2024"`) nem só símbolos;
- **texto tem sempre limite de comprimento** e nunca leva caracteres de controlo (`\n`, `\r`, `\t`, `\0`);
- **nada de metacaracteres a decidir comportamento**: `'; DROP TABLE …--`, `%`, `=SOMA(1;1)`, `../../` são texto literal, escapados ou recusados;
- **datas fora de gama são recusadas**; validade nova não fica no passado.

A UI (teclado, `formatter`, `Stepper`) **não conta como validação** — a barreira vive no ViewModel e repete-se na camada de dados quando decide dinheiro, stock ou perfil.

### 3.2 — Validação em cinco rondas obrigatórias (V1 → V5)

Toda a implementação nova é validada **cinco vezes** (`SECURITY.md` §2.5), com meios diferentes:

| Ronda | O que é |
|---|---|
| **V1 — plano** | análise de obstáculos e lista do que tem de ser recusado, antes de codificar |
| **V2 — código** | código relido contra o catálogo §2.2.2 e a checklist §10, antes de compilar |
| **V3 — testes** | bateria hostil em `POSAppTests/` a passar, com prova por mutação |
| **V4 — fluxo real** | app a correr: fluxo no ecrã com perfil Caixa **e** Admin, recusa visível em PT, nada gravado a meio, ficheiro exportado conferido |
| **V5 — regressão** | depois da última correção: suite completa outra vez + `git diff` sem SQL interpolado, sem `print` sensível, sem credenciais, com os ficheiros novos no alvo |

Regras que não se negoceiam:

- a V3 exige **prova por mutação**: retirar a guarda, ver o teste ficar vermelho, repor a guarda;
- a V4 **não se dispensa por ser manual** — o que não puder ser provado (credenciais, impressora, segundo dispositivo) fica escrito no `TODO.md` como por conferir;
- **qualquer correção obriga a repetir a partir da V2**, e a V5 é sempre a última a correr antes de marcar `[x]`;
- ronda por fechar **bloqueia** a tarefa — não se passa à UX/UI com a V3 por provar.

### 3.3 — Reforçar as validações em cada função nova

Função nova nunca sai mais fraca do que a anterior: repetir as validações que o projeto já tem para o mesmo tipo de campo (procurar no registo `SECURITY.md` §11 antes de inventar), e acrescentar as que faltarem. Se um ecrã antigo é tocado, **as lacunas §11.1 desse ecrã fecham-se nessa tarefa**.

### 3.4 — Registar a validação nova no `SECURITY.md`

Toda a validação que passa as cinco rondas entra na tabela `SECURITY.md` §11 (data, função/ecrã, campo, o que é recusado, ficheiro, teste) — é parte da V5, na mesma tarefa. Sem essa linha, a tarefa não está feita. Os IDs do registo são `R…`, para não colidirem com as rondas `V1–V5`.

### 3.5 — Enriquecer o `SECURITY.md` e o `SECURITY_POLICY.md`

**Obrigação, não sugestão**: sempre que uma regra destes documentos estiver em falta, errada, ambígua ou já não fizer sentido face ao código, **corrigi-la ou acrescentá-la na mesma tarefa** — regra técnica no `SECURITY.md`, processo e resposta a falha no `SECURITY_POLICY.md`. Ameaça nova, campo novo, formato de ficheiro novo ou canal novo obrigam a rever o modelo de ameaça (§1) e o catálogo (§2.2.2). Nada fica "para escrever depois".

### 3.6 — Testar a função/janela nova contra `SECURITY.md` **e** `STYLE_GUIDE.md`

Antes de dar por feita qualquer função ou janela nova, correr as duas checklists, por inteiro:

- `Docs/security/SECURITY.md` §10 — SQL parametrizado, entradas validadas, transação, autorização na camada de dados, nada sensível em log, CSV/ficheiro sanitizados, cinco rondas fechadas, registo §11 escrito;
- `Docs/development/STYLE_GUIDE.md` §15 — tokens do `AppTheme`, Liquid Glass, animação e transição, estados de vazio/carregamento/erro, texto em PT, acessibilidade, claro e escuro, macOS e iOS.

Falha num ponto de qualquer das duas = tarefa por fechar.

---

## 4. Tecnologia — só SwiftUI e AppKit

- **Apenas SwiftUI e AppKit** (e UIKit apenas onde o iOS o exigir, ex.: `ShareSheet`, scanner).
- **Zero dependências externas.** Nada de SPM/CocoaPods/Carthage. SQLite é o `libsqlite3` do sistema.
- Se algo parecer precisar de uma biblioteca, resolve-se com a stdlib ou com um framework da Apple.

---

## 5. Liquid Glass, animação e transição

É obrigatório dar o **máximo de suporte a Liquid Glass**, animação e transição. Alvo: macOS 26 / iOS 26 (as APIs nativas estão disponíveis).

- Superfícies: `.glassEffect(.regular, in: .rect(cornerRadius: 16))`; botões: `.buttonStyle(.glass)`.
- Agrupar elementos próximos em `GlassEffectContainer` para o efeito de fusão.
- **Nunca vidro sobre vidro** — um único plano de vidro por secção.
- Verificar sempre o contraste do texto sobre vidro em modo **claro e escuro**.
- Toda a mudança de estado visível anima: `.animation(_:value:)`, `.transition(...)`, `withAnimation`, `matchedGeometryEffect` em navegações de detalhe.
- Listas e grelhas animam inserção/remoção/reordenação; nada aparece ou desaparece de forma seca.
- Respeitar `Reduce Motion` (`@Environment(\.accessibilityReduceMotion)`) — animação reduzida, nunca UI partida.

Detalhe completo em `Docs/development/STYLE_GUIDE.md`.

---

## 6. UI/UX — `Docs/development/STYLE_GUIDE.md`

**É obrigatório seguir `Docs/development/STYLE_GUIDE.md` rigorosamente, regra a regra, em toda a UI** — não é referência opcional: tokens de `Utils/AppTheme.swift` (nunca cores à mão nas Views), escalas de espaçamento e raio, Liquid Glass onde for possível, animação e transição em toda a mudança de estado, texto em Português (PT), acessibilidade, estados de vazio/carregamento/erro, e adaptação macOS ↔ iOS. Uma tarefa de UI só está feita depois de a checklist §15 do `STYLE_GUIDE.md` passar toda.

### 6.1 — UX antes de UI (obrigatório)

**Primeiro pensa-se UX, só depois se faz UI.** Antes de escrever uma linha de View — ecrã novo, redesenho, folha, painel ou componente:

1. Escrever o plano de UX em `Docs/planning/PLAN.md` (tarefa do utilizador, decisão, fluxo, hierarquia, estados, prevenção de erro, movimento e vidro, acessibilidade) — formato em `Docs/development/STYLE_GUIDE.md` §0.1.
2. Só com o fluxo e a hierarquia fechados se escolhe layout, componente e cor.
3. **O `PLAN.md` é cache**: assim que a UI fica implementada, esvaziar o texto (o ficheiro fica, vazio, para o plano seguinte). O registo do trabalho vive no `TODO.md`/`CHANGELOG.md` e na documentação de arquitetura.
4. Se o plano deixar de servir a meio, reescrevê-lo antes de continuar a codificar.

---

## 7. Arquitetura — `Docs/architecture/ARCHITECTURE.md`

`Docs/architecture/ARCHITECTURE.md` descreve as camadas, regras de dependência, arranque, navegação, fluxos, serviços, alvos, concorrência e dívida arquitetural. **É obrigatório lê-lo antes de mexer na estrutura e mantê-lo atualizado.**

Atualizar `Docs/architecture/ARCHITECTURE.md` sempre que:

- se criar/alterar/remover um **ViewModel, serviço ou manager**;
- se mudar um **fluxo principal** (venda, login, fecho de caixa, subscrição, proximidade);
- se mudar o **ponto de entrada** (`@main`), a navegação ou um alvo do projeto;
- se mudar uma **regra de dependência** entre camadas, ou o modelo de concorrência;
- se resolver ou acrescentar um item da secção **Dívida arquitetural conhecida**.

Se uma tarefa toca em estrutura, a atualização do `Docs/architecture/ARCHITECTURE.md` é um item explícito dessa tarefa no `TODO.md`.

Resumo das regras que o documento fixa:

- **MVVM**: `Views → ViewModels → DatabaseManager → Models`.
- **Models** não importam SwiftUI. Cores/ícones derivados vivem em extensões dentro de `Utils/AppTheme.swift`.
- **Views** não fazem SQL nem contêm regras de negócio.
- Todo o acesso a SQL passa pelo `Database/DatabaseManager.swift`.
- Antes de criar um helper/serviço novo, procurar no projeto — reutilizar o que já existe (ex.: `ReportService`, `ShareSheet`, `AppTheme`).

---

## 8. Ordem de trabalho de cada tarefa

1. Ler `Docs/TODO.md` — há pendências? Fechar essas primeiro.
2. Escrever a tarefa nova no `Docs/TODO.md` (Backend antes de Frontend).
3. **V1 — plano de validação** (secção 3.1): análise de obstáculos escrita, lista do que tem de ser recusado, bateria hostil no `Docs/development/TESTING.md`.
4. Implementar **backend** → **V2** (código relido contra `SECURITY.md` §2.2.2 e §10) → compilar.
5. **V3 — teste de implementação, antes da UX e da UI** (secção 10): escrever/atualizar os testes em `POSAppTests/`, correr a suite, provar por mutação e **documentar no `Docs/development/TESTING.md`**. Cada erro encontrado vai para o `Docs/development/ERRORS.md` (secção 11) e obriga a repetir a partir da V2.
6. **Só com a V3 verde: pensar UX** — escrever o plano em `Docs/planning/PLAN.md` (secção 6.1).
7. Implementar **frontend** seguindo o `Docs/development/STYLE_GUIDE.md` à risca (Liquid Glass onde for possível + animação e transição), e **esvaziar o `PLAN.md`** quando a UI ficar feita.
8. **V4 — fluxo real** (`TESTING.md` §5): app a correr, fluxo no ecrã com perfil Caixa **e** Admin, lixo da bateria hostil metido à mão, ficheiro exportado aberto e conferido. O que não puder ser provado fica escrito no `TODO.md`.
9. Correr as duas checklists (secção 3.6): `SECURITY.md` §10 e `STYLE_GUIDE.md` §15.
10. Atualizar `README.md`, `Docs/database/DATABASE.md`, **todos os `.md` de `Docs/architecture/`** e `Docs/DOCUMENTATION.md` conforme a secção 2.
11. **V5 — regressão e fecho** (`TESTING.md` §6): suite completa outra vez depois da última correção, `git diff` varrido (SQL interpolado, `print` sensível, credenciais, ficheiros por registar no alvo), correções escritas no `Docs/TODO.md` (secção 1.5) e no `ERRORS.md`, validação nova registada em `SECURITY.md` §11.
12. Marcar `[x]`. Com o `Docs/TODO.md` todo `[x]`, **fechar o ciclo já**: mover o texto para o `Docs/CHANGELOG.md`, recalcular o índice e esvaziar o `TODO.md` (secções 1.6 e 1.6.1) — sem esperar por pedido.

---

## 9. Diagramas — Mermaid obrigatório

**`Docs/architecture/SYSTEM_DESIGN.md` e `Docs/database/DATABASE.md` são documentos Mermaid.** Se o diagrama for representável em Mermaid, tem de ser Mermaid — **é proibido deixar ASCII art** nesses dois ficheiros.

Regras:

1. Todo o diagrama novo ou alterado nestes dois ficheiros entra em bloco ` ```mermaid `.
2. Ao mexer numa secção com ASCII art antigo, **converter para Mermaid nessa mesma tarefa** — não deixar para depois.
3. Escolher o tipo certo de diagrama — ver a tabela **Que tipo usar** no fim desta secção.
4. **Dados tabulares não são diagramas** — métricas, campos de protocolo, migrações e listas de propriedades vão em **tabela Markdown**, nunca em caixas ASCII.
5. **Única exceção permitida a ASCII**: wireframes/mockups de ecrãs, porque o Mermaid não tem diagrama equivalente. Nesse caso, marcar a secção como wireframe e acrescentar ao lado o `stateDiagram-v2` dos estados que a produzem.
6. `Docs/database/DATABASE.md`: qualquer tabela, coluna ou relação nova obriga a atualizar o `erDiagram` e o `graph LR` das relações — não basta escrever o SQL.
7. Verificar que o bloco renderiza (Obsidian/GitHub) antes de dar a tarefa por feita. Evitar sintaxe recente e frágil (ex.: setas bidirecionais `<<->>`); usar duas setas simples.

### Que tipo usar

| Conteúdo | Tipo Mermaid |
|---|---|
| Esquema de base de dados, entidades e relações | `erDiagram` |
| Arquitetura, componentes, camadas, árvores de Views | `flowchart` (+ `subgraph`) |
| Troca de mensagens entre dispositivos/camadas no tempo | `sequenceDiagram` |
| Estados de ligação, ciclo de vida, máquinas de estado | `stateDiagram-v2` |
| Cronologia de um processo | `timeline` |
| Relações simples entre tabelas | `graph LR` |

---

## 10. Testes — `Docs/development/TESTING.md`

**É obrigatório conhecer e manter o `Docs/development/TESTING.md`.** É lá que vive o que é testado, o que cada teste resolve e como se escreve um teste novo.

Regras:

1. **O teste de implementação vem antes da UX e antes da UI.** Backend feito → testes escritos e a passar (**V3**) → só depois `PLAN.md` e View. Nunca o contrário.
2. **Todo o teste novo ou alterado é documentado no `TESTING.md`**: linha na tabela de índice §2, com o ficheiro, o número de testes, a suite e — a coluna que interessa — **o que resolve** (o problema que impede de voltar).
3. **Bateria hostil obrigatória** (`TESTING.md` §3): o teste tem de provar que a entrada má é recusada, não só que a boa é aceite.
4. **Prova por mutação** em pelo menos um teste por tarefa: retirar a guarda, ver vermelho, repor.
5. Ficheiro de teste novo é registado no alvo `POSAppTests` (lista explícita no `project.pbxproj`, IDs únicos).
6. Suite completa a passar antes de dar qualquer tarefa por feita, e outra vez depois da última correção (**V5**, `TESTING.md` §6): `xcodebuild -scheme Sales_Project -destination 'platform=macOS' test`.
7. O que não dá para testar automaticamente (fluxo no ecrã, perfil Caixa vs Admin, contraste, impressão) é a **V4** — lista em `TESTING.md` §5 — e o que ficar por conferir escreve-se no `TODO.md`, em vez de se dar por verificado.

---

## 11. Erros — `Docs/development/ERRORS.md`

**É obrigatório conhecer e manter o `Docs/development/ERRORS.md`.** Erro que aparece a compilar, a testar ou a usar a app é **resolvido e escrito**, nunca corrigido em silêncio.

Regras:

1. **Consultar primeiro**: antes de debugar, procurar no `ERRORS.md` — os erros deste projeto repetem-se (ficheiro por registar no alvo, expressão que o type-checker não aguenta, teste que passa com o bug reposto).
2. **Uma entrada por erro**, com **sintoma, causa, solução e prova**. Sem prova, o erro não está fechado.
3. **Tabela de índice §1 atualizada na mesma tarefa** — erro novo, linha nova (data, sintoma, onde, categoria, estado).
4. Erro encontrado em qualquer ronda obriga a repetir **a partir da V2** (secção 3.2), acabando sempre na V5.
5. Erro de segurança entra também no `Docs/security/SECURITY.md` §9 e segue a resposta do `Docs/security/SECURITY_POLICY.md` §6.
6. As correções continuam a ser registadas no `Docs/TODO.md` (`## Correções pós-teste`, secção 1.5) — o `ERRORS.md` guarda o **conhecimento**, o `TODO.md` guarda o **trabalho**.
