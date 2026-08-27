# Docs/development/TESTING.md — Testes do Sales POS

Documento obrigatório (`CLAUDE.md` §10). Aqui vive **o que é testado, o que cada teste resolve e como se escreve um teste novo**.

Regra que manda em tudo: **o teste de implementação vem antes da UX e antes da UI.** Uma função só chega ao ecrã depois de existir prova de que faz o que diz e recusa o que não deve aceitar. É a ronda **V3** das cinco de `Docs/security/SECURITY.md` §2.5 — e este documento fecha também a **V4** (fluxo real, §5) e a **V5** (regressão, §6).

Ordem obrigatória de uma funcionalidade nova:

```
Tarefa no TODO.md → V1 (plano de validação) → backend → V2 (código relido)
    → TESTE DE IMPLEMENTAÇÃO (este documento) → V3 verde
        → UX (PLAN.md) → UI
            → V4 fluxo real na app (§5) → V5 regressão + diff limpo (§6) → documentação
```

Erro encontrado em qualquer destes passos vai para o `Docs/development/ERRORS.md` — sintoma, causa, solução, prova.

---

## 1. Como correr

```bash
# Suite completa (macOS)
xcodebuild -scheme Sales_Project -destination 'platform=macOS' test

# Só compilar
xcodebuild -scheme Sales_Project -destination 'platform=macOS' build
```

- Framework: **Swift Testing** (`import Testing`, `@Suite`, `@Test`, `#expect`, `#require`) — nada de XCTest em testes novos.
- Plano: `Sales_Project.xctestplan`, com `parallelizable: false`. **Não ligar paralelismo**: as suites partilham o singleton `DatabaseManager` e as transações `BEGIN IMMEDIATE` concorrentes na mesma ligação partem os testes (ver `ERRORS.md` E2).
- Estado atual: **118 testes em 27 suites**, `** TEST SUCCEEDED **` (2026-08-17).

---

## 2. Índice das suites

Uma linha por ficheiro de teste. **Teste novo obriga a linha nova aqui** — a coluna que interessa é *O que resolve*: o problema real que o teste impede de voltar.

| #   | Ficheiro                                      | Testes | Suites                                                                                            | O que resolve                                                                                                                                                                                                                         |
| --- | --------------------------------------------- | ------ | ------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| T1  | `POSAppTests/SQLInjectionTests.swift`         | 2      | Injeção de SQL                                                                                    | Prefixo de mês e pesquisa de produtos com `'; DROP TABLE …--` e `%` gravam e leem como texto literal — prova que o SQL é ligado, não interpolado (`SECURITY.md` §2.1)                                                                 |
| T2  | `POSAppTests/PasswordHashTests.swift`         | 11     | Hash de password (PBKDF2) · Login — entrada hostil                                              | Formato `pbkdf2$sha256$…`, sal aleatório por utilizador, verificação certa/errada, hash antigo `sha256` ainda válido, hash malformado recusado sem rebentar; **e (R18)** username acima de 64 caracteres, password acima de 128, caracteres de controlo e campos vazios recusados antes da base de dados, espaços à volta do username tolerados, `loginFailureCount` a incrementar em cada recusa |
| T2b | `POSAppTests/PasswordHashTests.swift`         | 3      | Login — leitura estável do utilizador                                                             | `fetchUserByUsername` devolve sempre o mesmo utilizador consulta após consulta, login com credenciais certas entra em todas as tentativas seguidas, e nenhuma ligação de texto ao SQLite volta a passar `SQLITE_STATIC` (guarda determinista do erro E23) |
| T3  | `POSAppTests/AuthorizationTests.swift`        | 5      | Autorização na camada de dados                                                                    | Caixa não apaga produtos, não altera preços, não apaga utilizadores nem reabre fechos; ninguém se promove a si próprio; o último Admin não é apagado — sem passar pela UI                                                             |
| T4  | `POSAppTests/TransactionTests.swift`          | 4      | Transação da venda                                                                                | Venda válida grava tudo e desconta stock; stock insuficiente ou item inválido a meio não deixam nada gravado (`ROLLBACK`)                                                                                                             |
| T5  | `POSAppTests/CSVEscapingTests.swift`          | 11     | CSV Escaping                                                                                      | Vírgula, ponto e vírgula, aspas e nova linha não partem o ficheiro; fórmula (`=SOMA(1;1)`) é neutralizada; números saem com ponto decimal; BOM correto                                                                                |
| T6  | `POSAppTests/FilenameSanitizationTests.swift` | 7      | Filename Sanitization · PDF orientação do texto                                                   | `../../evil` não sobrevive, o ficheiro fica dentro da diretoria de relatórios, nome vazio vira `anonimo`, máximo 40 caracteres; e os glifos do PDF não saem espelhados                                                                |
| T7  | `POSAppTests/ProximityPayloadTests.swift`     | 11     | Proximity Payload                                                                                 | Tamanho `0` ou acima de 10 MB recusado **antes de alocar**; JSON malformado, envelope sem `products`, campos hostis e listas acima do máximo rejeitados; código de emparelhamento com 6 dígitos e parâmetros TLS distintos por código |
| T8  | `POSAppTests/ProximityTests.swift`            | 15     | Low Stock Export · Proximity Service · Transfer Protocol · Receiver · File Document · Integration | Exportação CSV/JSON de stock baixo, cabeçalho de tamanho, parsing de produtos e fluxo completo de transferência                                                                                                                       |
| T9  | `POSAppTests/FIFOTests.swift`                 | 7      | Consumo de stock por FIFO                                                                         | Venda atravessa lotes pelo mais antigo, lote sem validade fica para o fim, stock insuficiente não consome nada, lote expirado não é vendável, promoção aplica desconto                                                                |
| T10 | `POSAppTests/ExpiryStatusTests.swift`         | 5      | Faixas de validade                                                                                | Faixas e fronteiras exatas (0/30/31/60/61/90/91/120/121 dias), ausência de validade, ordenação por gravidade, valor perdido pelo preço do lote                                                                                        |
| T11 | `POSAppTests/ReportFilterTests.swift`         | 20     | Filtro do histórico · Top de produtos · Risco de validade · Impressão de facturas · Layout do PDF | Âmbitos dia/mês/ano do histórico, ranking de produtos, separação entre perda real e risco, larguras de página e **cabeçalho a não sobrepor a tabela no PDF**                                                                          |
| T12 | `POSAppTests/AdminStatsTests.swift`           | 13     | Produtos parados (6 meses) · Fecho por caixa · Vendas por caixa                                   | Regra dos 6 meses com fronteira exata, totais por caixa e por método de pagamento, estado de caixa fechada/por fechar; e no Dashboard: nº de vendas e total agregados por utilizador, ordenados pelo maior, venda de utilizador apagado ainda a contar (`Utilizador #<id>`) para a soma dos caixas bater certo com a receita do período |
| T13 | `POSAppTests/AdminDateFilterTests.swift`      | 11     | Filtro de data do Dashboard                                                                       | Combinações ano/mês/dia, granularidade da série, dias sem vendas a zero, calendário real (Fevereiro de 2024 com 29 dias), anos do mais recente para o mais antigo                                                                     |
| T14 | `POSAppTests/AdminEditingTests.swift`         | 3      | Edição na Administração (lote e stock)                                                            | Quantidade de lote negativa e stock negativo recusados; valores válidos gravados com o stock a acompanhar                                                                                                                             |
| T15 | `POSAppTests/CashierCloseFlowTests.swift`     | 1      | Fecho da própria caixa (perfil Caixa)                                                             | Caixa vê a sua caixa com vendas e consegue fechá-la — sem tocar nas dos outros                                                                                                                                                        |
| T16 | `POSAppTests/CategoryReorderTests.swift`      | 3      | Reordenação de categorias                                                                         | Mover para o topo, para o fim (destino é o índice antes da remoção) e para a própria posição                                                                                                                                          |

---

## 3. Bateria de entradas hostis — obrigatória por tipo de campo

Sai da análise de obstáculos do `SECURITY.md` §2.2.1 e é o mínimo que um teste de campo novo tem de tentar. **Testar que o valor bom é aceite não prova nada** — o teste tem de provar que o mau é recusado.

| Tipo de campo | Entradas a atirar | Resultado esperado |
|---|---|---|
| Numérico (preço, quantidade, stock, %) | `"abc"`, `"12a"`, `"€10"`, `"1,,5"`, `"--3"`, `"1e999"`, `-1`, `0`, `NaN`, `infinity`, `999999999` | recusado com mensagem em PT; nada gravado |
| Nome de pessoa | `""`, `"   "`, `"Ana123"`, `"@@@"`, 200 caracteres, `"\n\t"` | recusado |
| Nome de produto | `""`, `"   "`, `"2024"`, `"---"`, 200 caracteres, `"Azeite 1L"` (este passa) | só o último é aceite |
| Texto exportado para CSV | `a,b`, `a;b`, `a"b`, `a\nb`, `=SOMA(1;1)`, `+1`, `@cmd` | escapado e fórmula neutralizada |
| Texto usado em nome de ficheiro | `../../evil`, `/etc/passwd`, `"   "`, 100 caracteres | ficheiro dentro da diretoria de relatórios, nome ≤ 40 |
| Texto que chega ao SQL | `'; DROP TABLE Products;--`, `%`, `_`, `"` | gravado e lido **literal**; tabelas intactas |
| Data | ano `0001`, ano `9999`, validade de ontem | recusada |
| Payload de rede | `0` bytes, 10 MB + 1, JSON malformado, campo a mais, tipo trocado | recusado antes de alocar/gravar |
| Autorização | a mesma operação com perfil `Caixa` | recusada na camada de dados, não só na View |

---

## 4. Como escrever um teste novo

1. **Nome em Português**, a descrever o comportamento, não o método: `@Test("Stock negativo é recusado")`, não `@Test("testUpdateStock")`.
2. **Uma suite por assunto**, com `@Suite("…")` em PT.
3. **Prova por mutação, obrigatória em pelo menos um teste da tarefa**: retirar a guarda que se acabou de escrever, ver o teste ficar vermelho, repor a guarda. Um teste que passa com e sem a validação não é um teste — é decoração.
4. **Limpar o que se cria**: `defer` a apagar utilizadores, produtos e fechos criados (a BD é a real, partilhada pelo `DatabaseManager.shared`).
5. **Perfil explícito**: pôr `db.currentUser` no perfil que o teste precisa; não herdar o da suite anterior.
6. **Registar o ficheiro no alvo `POSAppTests`** em `Sales_Project.xcodeproj/project.pbxproj` — o alvo usa lista explícita de ficheiros, não pasta sincronizada. IDs de objeto novos e **únicos** (ver `ERRORS.md` E3 e E4).
7. **Acrescentar a linha na tabela §2** deste documento, com o que o teste resolve.
8. Se o teste nasceu de uma validação de segurança, acrescentar também a linha no registo `SECURITY.md` §11 e, se for de segurança pura, no quadro `SECURITY.md` §6.

### O que não se testa

Layout de SwiftUI pixel a pixel, cor e animação — isso é a checklist §15 do `Docs/development/STYLE_GUIDE.md`, verificada à vista nos dois modos (claro/escuro). Testa-se o que é **regra**: cálculo, validação, autorização, persistência, formato de ficheiro.

---

## 5. V4 — fluxo real: o que os testes não apanham

Com a UI feita e a suite verde. Os testes provam a regra isolada; a V4 prova que a regra chega ao utilizador.

- [ ] App lançada, sem crash no arranque.
- [ ] Fluxo tocado percorrido no ecrã real (venda, fecho, produto, administração, transferência).
- [ ] Campos novos testados à mão com o lixo da §3 — o utilizador vê **mensagem em PT**, não um valor a `0` nem um erro técnico.
- [ ] O mesmo fluxo com perfil **Caixa** e com **Admin**: o que é restrito é mesmo recusado, e a recusa vem da camada de dados.
- [ ] Nada gravado a meio: depois de uma recusa, a lista, o stock e o total ficam como estavam.
- [ ] Ficheiro exportado durante a prova **aberto e conferido** (colunas, escape, nome dentro da diretoria da app).
- [ ] Modo claro e escuro, contraste sobre vidro (`STYLE_GUIDE.md` §15).
- [ ] Ficheiros de teste exportados durante a verificação **apagados no fim**.

O que ficar por conferir por exigir credenciais, impressora ou segundo dispositivo escreve-se no `Docs/TODO.md`, em vez de se dar por verificado.

---

## 6. V5 — regressão e varrimento do diff

A última coisa a correr, depois da **última** correção — não antes.

- [ ] Suite completa outra vez, do princípio: `xcodebuild -scheme Sales_Project -destination 'platform=macOS' test` → `** TEST SUCCEEDED **`.
- [ ] `git diff` lido de ponta a ponta à procura de: interpolação de strings em SQL, `print` fora de `#if DEBUG` ou com dados sensíveis, credenciais em código, `try?` a engolir erro em venda/pagamento/fecho.
- [ ] Ficheiros novos registados no alvo certo do `project.pbxproj` (e nenhum `.md` como recurso — E5).
- [ ] Contagem de testes conferida contra a §1 deste documento; se mudou, a §1 e a §2 são atualizadas.
- [ ] Registos escritos: `SECURITY.md` §11, índice §2 deste documento, `ERRORS.md` por cada erro das rondas.

Só com a V5 fechada se marca `[x]` no `Docs/TODO.md`.
