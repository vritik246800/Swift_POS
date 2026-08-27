# Docs/development/ERRORS.md — Erros e soluções do Sales POS

Documento obrigatório (`CLAUDE.md` §11). **Todo o erro encontrado a compilar, a testar ou a usar a app entra aqui**, com a solução — nunca se corrige em silêncio.

Para que serve: os erros deste projeto repetem-se. Ficheiro novo esquecido no alvo, expressão que o type-checker não aguenta, teste que passa com e sem o bug. Quem consulta esta lista antes de debugar poupa a ronda inteira.

Regras:

1. Uma entrada por erro, com **sintoma, causa, solução e prova**. Sem prova, o erro não está fechado.
2. A tabela de índice §1 é atualizada na mesma tarefa — erro novo, linha nova.
3. Erro de segurança entra também no `Docs/security/SECURITY.md` §9 e segue o procedimento do `Docs/security/SECURITY_POLICY.md` §6.
4. Erro encontrado em qualquer ronda obriga a repetir **a partir da V2** e a acabar na **V5** (`SECURITY.md` §2.5).
5. Correção sem teste que a proteja só se aceita quando o erro é de configuração do projeto (`.pbxproj`, plano de testes) — e fica escrito que é esse o caso.

---

## 1. Índice

| #                                                                  | Data       | Erro (sintoma)                                                                     | Onde                                          | Categoria        | Estado    |
| ------------------------------------------------------------------ | ---------- | ---------------------------------------------------------------------------------- | --------------------------------------------- | ---------------- | --------- |
| [E1](#e1--illegal-multi-threaded-access-to-database-connection)    | 2026-08-14 | `illegal multi-threaded access to database connection`                             | `Database/DatabaseManager.swift`              | Concorrência     | Resolvido |
| [E2](#e2--12-testes-a-falhar-em-paralelo-sobre-o-mesmo-singleton)  | 2026-08-14 | 12 testes a falhar sem razão aparente                                              | `Sales_Project.xctestplan`                    | Testes           | Resolvido |
| [E3](#e3--build-input-files-cannot-be-found)                       | 2026-08-14 | `Build input files cannot be found: …/Views/Sales/SQLInjectionTests.swift`         | `project.pbxproj`                             | Projeto/alvo     | Resolvido |
| [E4](#e4--ficheiro-novo-não-compila-nem-aparece-no-alvo)           | 2026-08-14 | Ficheiro novo ignorado pelo build                                                  | `project.pbxproj`                             | Projeto/alvo     | Resolvido |
| [E5](#e5--no-such-file-or-directory-em-md-na-fase-resources)       | 2026-08-14 | `No such file or directory` num `.md`                                              | `project.pbxproj`                             | Projeto/alvo     | Resolvido |
| [E6](#e6--does-not-conform-to-protocol-observableobject)           | 2026-08-14 | `type '…' does not conform to protocol 'ObservableObject'` + 30 erros de `Combine` | `Views/Reports/ReportComponents.swift`        | Compilador       | Resolvido |
| [E7](#e7--unable-to-type-check-this-expression-in-reasonable-time) | 2026-08-16 | `unable to type-check this expression in reasonable time`                          | `ViewModels/AdminViewModel.swift`             | Compilador       | Resolvido |
| [E8](#e8--failed-to-produce-diagnostic-for-expression)             | 2026-08-16 | `failed to produce diagnostic for expression`                                      | `Views/DayClose/DayCloseView.swift`           | Compilador       | Resolvido |
| [E9](#e9--pdf-com-texto-por-cima-do-cabeçalho-e-glifos-espelhados) | 2026-08-16 | Texto do PDF sobreposto e espelhado                                                | `Views/Reports/ReportService.swift`           | PDF              | Resolvido |
| [E10](#e10--diagrama-mermaid-não-renderiza)                        | 2026-08-16 | Bloco Mermaid mostrado como texto                                                  | `Docs/database/DATABASE.md`                   | Documentação     | Resolvido |
| [E11](#e11--category-is-ambiguous-for-type-lookup)                 | 2026-08-16 | `'Category' is ambiguous for type lookup`                                          | `POSAppTests/CategoryReorderTests.swift`      | Compilador       | Resolvido |
| [E12](#e12--helper-só-existe-num-dos-alvos)                        | 2026-08-15 | `subscript(safe:)` não encontrado no alvo da app                                   | `Views/Reports/ReportViewModel.swift`         | Projeto/alvo     | Resolvido |
| [E13](#e13--animação-que-não-arranca)                              | 2026-08-16 | Barra anima na primeira vez e nunca mais                                           | `Views/Reports/ReportComponents.swift`        | SwiftUI          | Resolvido |
| [E14](#e14--nsprintinfodictionary-recusa-o-dicionário-partilhado)  | 2026-08-16 | Impressão falha ao construir `NSPrintInfo`                                         | `Views/Sales/ReceiptPrintService.swift`       | AppKit           | Resolvido |
| [E15](#e15--método-print-a-sombrear-a-stdlib)                      | 2026-08-16 | Chamadas a `print` deixam de funcionar                                             | `Views/Sales/PrintFormatSheet.swift`          | Swift            | Resolvido |
| [E16](#e16--specifier-fora-de-um-text)                             | 2026-08-16 | `specifier:` não compila num parâmetro `String`                                    | `Views/Products/ProductListView.swift`        | SwiftUI          | Resolvido |
| [E17](#e17--linhas-de-pagamento-repetidas-em-cada-factura)         | 2026-08-16 | Pagamentos duplicados ao imprimir um grupo                                         | `Views/Sales/ReceiptPrintService.swift`       | Regra de negócio | Resolvido |
| [E18](#e18--filho-flexível-não-estica-dentro-de-um-scrollview)     | 2026-08-16 | Gráfico com altura errada no fecho                                                 | `Views/DayClose/DayCloseView.swift`           | SwiftUI          | Resolvido |
| [E19](#e19--animationvalue-exige-equatable)                        | 2026-08-16 | `.animation(value:)` não compila com o carrinho                                    | `Views/Sales/SaleView.swift`                  | SwiftUI          | Resolvido |
| [E20](#e20--três-componentes-diferentes-para-o-mesmo-elemento)     | 2026-08-14 | Três chips de categoria com aspetos distintos                                      | `Utils/AppTheme.swift`                        | Arquitetura      | Resolvido |
| [E21](#e21--teste-que-lê-a-hora-duas-vezes)                        | 2026-08-16 | Teste da fronteira exata falha de forma intermitente                               | `POSAppTests/AdminStatsTests.swift`           | Testes           | Resolvido |
| [E22](#e22--teste-de-pdf-que-passava-com-o-bug-reposto)            | 2026-08-15 | Teste verde com o defeito ainda no código                                          | `POSAppTests/FilenameSanitizationTests.swift` | Testes           | Resolvido |
| [E23](#e23--login-recusa-credenciais-certas-de-vez-em-quando)      | 2026-08-19 | Login falha com a password certa, mas só às vezes                                  | `Database/DatabaseManager.swift`              | Base de dados    | Resolvido |

---

## 2. Entradas

### E1 — `illegal multi-threaded access to database connection`

- **Sintoma**: a app rebenta durante os testes e no acesso à BD a partir das filas de rede da proximidade.
- **Causa**: `sqlite3_open` abre a ligação sem mutex; o `DatabaseManager` é singleton e é tocado por várias filas.
- **Solução**: `sqlite3_open_v2` com `SQLITE_OPEN_FULLMUTEX` (modo serializado) — `Database/DatabaseManager.swift`.
- **Prova**: suite completa a passar com as suites de proximidade e de transação ativas.

### E2 — 12 testes a falhar em paralelo sobre o mesmo singleton

- **Sintoma**: 12 falhas sem padrão, diferentes a cada execução.
- **Causa**: suites em paralelo a partilhar `DatabaseManager.shared`: transações `BEGIN IMMEDIATE` concorrentes na mesma ligação e `currentUser` pisado entre suites.
- **Solução**: `Sales_Project.xctestplan` com `parallelizable: false` — e cada teste a fixar o seu `db.currentUser`.
- **Prova**: execuções repetidas com o mesmo resultado (`** TEST SUCCEEDED **`). Erro de configuração: sem teste próprio.

### E3 — `Build input files cannot be found`

- **Sintoma**: `Build input files cannot be found: …/Views/Sales/SQLInjectionTests.swift` — ficheiro que nunca esteve nesse caminho.
- **Causa**: IDs de objeto duplicados no `project.pbxproj` (ficheiros novos registados com IDs já usados pelos testes); o Xcode resolveu contra o grupo errado.
- **Solução**: renumerar os IDs para uma gama livre. **Ao acrescentar ficheiros à mão, confirmar sempre que o ID não existe** (`grep` do ID antes de escrever).
- **Prova**: `** BUILD SUCCEEDED **` e os testes a correr do caminho certo.

### E4 — Ficheiro novo não compila nem aparece no alvo

- **Sintoma**: símbolos "não encontrados" de um ficheiro que existe em disco.
- **Causa**: o alvo usa **lista explícita de ficheiros**, não pasta sincronizada — criar o `.swift` não o põe no build.
- **Solução**: registar `PBXFileReference` + `PBXBuildFile` + grupo + fase `Sources`, no alvo certo (app, `List_Storage` ou `POSAppTests`).
- **Prova**: build e testes a passar. Erro de configuração: sem teste próprio.

### E5 — `No such file or directory` em `.md` na fase Resources

- **Sintoma**: build completo falha a copiar `SYSTEM_DESIGN.md` e outros.
- **Causa**: `.md` movidos para `Docs/` continuavam listados na fase *Resources* com caminho antigo em `Views/`.
- **Solução**: remover as referências — **documentação não é recurso da app**. Regra que fica: `.md` novo nunca entra no alvo.
- **Prova**: build limpo.

### E6 — `does not conform to protocol 'ObservableObject'`

- **Sintoma**: `type 'ReportExportState' does not conform to protocol 'ObservableObject'` mais ~30 erros de `missing import of defining module 'Combine'`.
- **Causa**: ficheiro com `@Published` a importar só SwiftUI.
- **Solução**: `internal import Combine`, o mesmo padrão dos ViewModels.
- **Prova**: compilação limpa.

### E7 — `unable to type-check this expression in reasonable time`

- **Sintoma**: compilação encalha e falha nessa função.
- **Causa**: `Dictionary(grouping:)` encadeado com `map`/`reduce` numa só expressão (`revenueByCategory`).
- **Solução**: reescrever em ciclos explícitos. **Regra**: expressão de agregação com mais de dois encadeamentos parte-se em passos com tipo declarado.
- **Prova**: compilação em tempo normal; `AdminStatsTests` a passar.

### E8 — `failed to produce diagnostic for expression`

- **Sintoma**: erro sem localização útil, o compilador desiste.
- **Causa**: ternário entre duas funções de formatação (`formatCount` vs `{ formatMT($0) }`) — tipos de closure diferentes no mesmo ternário.
- **Solução**: uma única closure com o ternário dentro: `{ isCount ? formatCount($0) : formatMT($0) }`.
- **Prova**: `** BUILD SUCCEEDED **`.

### E9 — PDF com texto por cima do cabeçalho e glifos espelhados

- **Sintoma**: "V POS" escrito por cima de "Venda #35 · Cliente anónimo"; noutra versão, cada glifo espelhado na vertical.
- **Causa**: `startPage()` repunha `y` no topo **depois** de o cabeçalho já estar posicionado; e um `scaleBy(y: -1)` no contexto do PDF virava os glifos.
- **Solução**: `startPage()` deixa de mexer no `y` (só `newPage()` volta ao topo), cabeçalho desenhado logo após abrir a página; buffer `lines`/`PDFLine` apagado; transformação de escala removida.
- **Prova**: `ReportFilterTests` → suite "Layout do PDF de relatórios": falha se dois caracteres partilharem mais de 50% da área (`characterBounds`); teste da orientação compara peso da tinta na metade superior vs inferior. Ambos confirmados por mutação.

### E10 — Diagrama Mermaid não renderiza

- **Sintoma**: bloco aparece como texto no Obsidian/GitHub.
- **Causa**: fence ` ```mermaid ` a mais antes do texto de introdução — engolia o bloco seguinte.
- **Solução**: remover a fence solta. Varrer os restantes `.md` à procura do mesmo defeito.
- **Prova**: pré-visualização a renderizar; `grep -c '```mermaid'` par com o número de blocos fechados.

### E11 — `'Category' is ambiguous for type lookup`

- **Sintoma**: teste não compila ao usar `Category`.
- **Causa**: colisão com o `Category` de outro módulo visível no alvo de testes.
- **Solução**: qualificar o tipo — `POSApp.Category`.
- **Prova**: `CategoryReorderTests` a compilar e passar.

### E12 — Helper só existe num dos alvos

- **Sintoma**: `subscript(safe:)` não encontrado no alvo `Sales_Project`.
- **Causa**: extensão registada só no alvo `List_Storage`.
- **Solução**: deixar de depender do helper nesse sítio (o nome do mês passou a derivar da própria data da venda). Alternativa válida: registar o ficheiro nos dois alvos.
- **Prova**: build dos dois alvos.

### E13 — Animação que não arranca

- **Sintoma**: a barra cresce à primeira e depois fica parada.
- **Causa**: repor `growth = 0` e animar para `1` no **mesmo** update — o SwiftUI não vê mudança.
- **Solução**: arrancar a animação no ciclo seguinte (`DispatchQueue.main.async`).
- **Prova**: verificação à vista, nos dois modos.

### E14 — `NSPrintInfo(dictionary:)` recusa o dicionário partilhado

- **Sintoma**: impressão falha a construir o `NSPrintInfo`.
- **Causa**: `NSPrintInfo.shared.dictionary()` devolve `NSMutableDictionary`, que o inicializador não aceita.
- **Solução**: `as? [NSPrintInfo.AttributeKey: Any]` com `[:]` por omissão.
- **Prova**: impressão nos dois formatos (80 mm e A4).

### E15 — Método `print()` a sombrear a stdlib

- **Sintoma**: chamadas a `print` dentro do tipo deixam de escrever na consola.
- **Causa**: método de instância com o nome `print()`.
- **Solução**: renomear para `startPrinting()`.
- **Prova**: compilação e diagnósticos de volta.

### E16 — `specifier:` fora de um `Text`

- **Sintoma**: `\(valor, specifier: "%.0f")` não compila.
- **Causa**: a interpolação com `specifier:` só existe em `Text`, não em `String`.
- **Solução**: `valor.formatted(.number.precision(.fractionLength(0)))`.
- **Prova**: compilação; IVA e margem na lista de produtos com as casas certas.

### E17 — Linhas de pagamento repetidas em cada factura

- **Sintoma**: ao imprimir um grupo de facturas, os pagamentos aparecem repetidos em todas.
- **Causa**: filtro `saleId == sale.id || saleId == 0` — o `|| saleId == 0` apanhava pagamentos de outras vendas.
- **Solução**: filtrar só pela venda.
- **Prova**: impressão de grupo verificada; suite de facturas a passar.

### E18 — Filho flexível não estica dentro de um `ScrollView`

- **Sintoma**: gráfico do fecho de caixa com altura errada.
- **Causa**: dentro de `ScrollView` a proposta de altura é `nil`; num `HStack` o filho flexível não recebe altura.
- **Solução**: layout em `Grid` — só o `Grid` propõe a altura da linha à célula.
- **Prova**: teste de render offscreen a confirmar a proposta de altura.

### E19 — `.animation(value:)` exige `Equatable`

- **Sintoma**: `.animation(value: cartItems)` não compila.
- **Causa**: `SaleItem` não era `Equatable`.
- **Solução**: conformidade `Equatable` em `Models/SaleItem.swift`.
- **Prova**: compilação; animação do carrinho à vista.

### E20 — Três componentes diferentes para o mesmo elemento

- **Sintoma**: chips de categoria com aspetos distintos em três ecrãs (`CategoryChipView`, `SaleCategoryChip`, `FormCategoryChip`).
- **Causa**: trabalho em paralelo sem procurar o que já existia — contra `CLAUDE.md` §7.
- **Solução**: um único `CategoryChipView` em `Utils/AppTheme.swift` (com `showsCheckmark`); os privados apagados. Efeito secundário bom: desaparecem os literais `.white`.
- **Prova**: verificação à vista dos três ecrãs; `grep` sem os nomes antigos.

### E21 — Teste que lê a hora duas vezes

- **Sintoma**: teste da fronteira exata dos 6 meses falha de forma intermitente.
- **Causa**: `Self.limit` lido duas vezes → dois `Date()` diferentes, o segundo mais tarde.
- **Solução**: guardar o limite numa variável local e usar sempre a mesma.
- **Prova**: `AdminStatsTests` estável em execuções repetidas.

### E22 — Teste de PDF que passava com o bug reposto

- **Sintoma**: teste verde com o defeito ainda no código (glifos espelhados).
- **Causa**: o teste comparava a **posição da linha**, que o flip mantinha na mesma banda — só virava cada glifo. E `page.thumbnail` devolve `NSCGImageSnapshotRep`, não `NSBitmapImageRep`.
- **Solução**: desenhar "TTTT" e comparar o peso da tinta na metade superior vs inferior; bitmap construído a partir de `tiffRepresentation`.
- **Prova**: mutação — falha com o `scaleBy(y: -1)` reposto, passa sem ele. **É o exemplo de porque a V3 exige prova por mutação** (`TESTING.md` §4, regra 3).

### E23 — Login recusa credenciais certas de vez em quando

- **Sintoma**: com utilizador e password corretos, o login responde `Credenciais inválidas.` — não sempre, só de vez em quando. Repetir a mesma tentativa costuma entrar.
- **Causa**: as 54 chamadas `sqlite3_bind_text(statement, n, (x as NSString).utf8String, -1, nil)` passavam `nil` como destrutor, que é **`SQLITE_STATIC`**: promete ao SQLite que o ponteiro continua válido até ao `sqlite3_step`. O ponteiro é o buffer de uma `NSString` temporária (autoreleased) — na maioria das vezes sobrevive até ao fim do ciclo do run loop, mas não é garantido. Quando morre antes, o valor ligado é lixo, o `SELECT … WHERE username = ?` não encontra linha e o login trata isso como credenciais erradas. Qualquer outra query com texto corria o mesmo risco.
- **Solução**: constante `SQLITE_TRANSIENT` (`unsafeBitCast(-1, to: sqlite3_destructor_type.self)`) no topo de `Database/DatabaseManager.swift`, aplicada a **todas** as ligações de texto — o SQLite copia o valor durante a chamada e deixa de depender do tempo de vida do ponteiro. Correção numa só camada: todos os chamadores passam por ela.
- **Prova**: repetir a consulta 60 vezes com churn de autorelease **não** apanha o defeito (fica verde com o bug reposto) — é um erro dependente de tempo e de memória. A guarda que serve é determinista: o teste `Nenhum sqlite3_bind_text volta a usar SQLITE_STATIC` (`POSAppTests/PasswordHashTests.swift`) lê o código-fonte e falha se alguma ligação de texto voltar a passar `nil`. Mutação: repor `nil` numa ligação → vermelho a apontar a linha 337; repor `SQLITE_TRANSIENT` → verde.
- **Regra que fica**: ligação de texto ao SQLite é sempre `SQLITE_TRANSIENT`. `nil`/`SQLITE_STATIC` só com um buffer cujo tempo de vida esteja garantido até ao `finalize` — o que aqui nunca acontece.
