# Docs/development/STYLE_GUIDE.md — Regras de interface do Sales POS

Obrigatório em toda a UI. Alvo: **macOS 26 / iOS 26**, SwiftUI (+ AppKit/UIKit só onde a plataforma exigir).

Cada regra aqui tem um número ou um critério verificável — "parece bem" não é critério de aceitação. As bases vêm da Apple HIG, WCAG 2.2 AA, das heurísticas de Nielsen e de *Refactoring UI*; o que interessa nesta app está traduzido em regras concretas abaixo.

---

## 0. Os cinco princípios que decidem discussões

1. **Sistema antes de gosto.** Escalas fixas de espaçamento, tipo e cor. Um valor fora da escala precisa de justificação escrita no PR.
2. **Prevenir em vez de corrigir** (Norman). Desativar o que não é válido é melhor do que deixar clicar e mostrar erro.
3. **Reconhecer em vez de recordar.** Mostrar as opções (chips de categoria, métodos de pagamento) em vez de exigir memória.
4. **Feedback sempre, em ≤400 ms.** Toda a ação tem resposta visível. Sem resposta, o utilizador clica outra vez — e numa venda isso duplica linhas.
5. **Menos palavras.** Cortar metade do texto, depois metade do que sobra (Krug). Português direto, sem "happy talk".

---

## 0.1 UX antes de UI — `Docs/planning/PLAN.md` (obrigatório)

**Nenhuma UI se implementa sem plano de UX escrito.** Antes de tocar numa View — ecrã novo, redesenho, folha, painel ou componente — escrever primeiro o plano em `Docs/planning/PLAN.md`:

| Ponto | O que responde |
|---|---|
| Tarefa do utilizador | O que a pessoa vem cá fazer, em uma frase. |
| Decisão | Que informação é precisa para decidir, e qual é ruído a cortar. |
| Fluxo | Passos, do primeiro toque à confirmação. Menos passos ganha. |
| Hierarquia | O que é primário, secundário e terciário no ecrã. |
| Estados | Vazio · carregamento · erro · parcial · conteúdo. Todos escritos, nenhum descoberto depois. |
| Erros e prevenção | O que é desativado em vez de deixar falhar; o que se pode desfazer. |
| Movimento e vidro | Que mudanças de estado animam e onde entra o plano de vidro (secções 4 e 5). |
| Acessibilidade | Alvos, foco, Dynamic Type, contraste sobre vidro, `Reduce Motion`. |

Regras:

1. **UX primeiro, UI depois.** Só se escolhe layout, cor ou componente depois de o fluxo e a hierarquia estarem fechados no `PLAN.md`.
2. **O `PLAN.md` é cache, não é histórico.** Só tem o plano da UI que está a ser feita agora.
3. **Terminada a implementação da UI, esvaziar o `PLAN.md`** — o ficheiro fica, sem texto, pronto para o plano seguinte. O que fica registado é o `TODO.md`/`CHANGELOG.md` e a documentação de arquitetura, nunca o `PLAN.md`.
4. Se o plano mudar a meio (o fluxo não aguenta o ecrã real), **reescrever o `PLAN.md` antes** de continuar a codificar.

## 1. Tokens, espaçamento e escalas

- **Todas as cores saem de `Utils/AppTheme.swift`.** Nunca `Color(red:...)` nem hex à mão dentro de uma View.
- Tokens de marca: `AppTheme.accent` (`5856D6`), `brandPurple`, `brandOrange`, `brandGreen`.
- **Nomear pela intenção, não pela aparência**: `AppTheme.stockCritical`, não `AppTheme.vermelho`. O nome tem de sobreviver a uma mudança de valor.
- Cor de método de pagamento vem sempre de `AppTheme.methodColor(_:)`.
- **Grelha de 8 pt** (4 pt para acertos finos). Escala única de espaçamento: **4 · 8 · 12 · 16 · 24 · 32 · 48**. Nada de `padding(13)`.
- Raio de canto: **8** (controlos), **12** (cards pequenos), **16** (painéis e superfícies de vidro). Um raio por nível, sempre o mesmo.
- Espaçamento comunica agrupamento (Gestalt): elementos do mesmo grupo a 8 pt, grupos diferentes a 24 pt. Agrupar por proximidade antes de agrupar por caixa ou linha divisória.

## 2. Cor e contraste

- Semântica fixa: **verde** = sucesso/stock OK · **laranja** = aviso/em risco · **vermelho** = erro/perda real · **accent** = ação primária.
- **Contraste mínimo (WCAG 2.2 AA, obrigatório)**: 4.5:1 para texto normal, 3:1 para texto ≥ 18 pt ou a negrito ≥ 14 pt, 3:1 para ícones, bordas de campo e indicadores de estado.
- **Nunca comunicar informação só por cor.** Sempre cor + ícone ou cor + texto (badge de stock, faixa de validade, estado de pagamento). Cerca de 1 em 12 homens tem daltonismo — e um POS decide-se por cores de stock.
- **Modo escuro não é a paleta invertida**: fundo nunca preto puro (vibra e "sangra" sobre vidro); texto de corpo nunca branco puro. Reduzir a saturação dos acentos. Elevação por luminosidade, não por sombra pesada.
- Uma cor de acento por ecrã. Se tudo se destaca, nada se destaca (Von Restorff).

## 3. Tipografia

- Estilos dinâmicos do sistema (`.largeTitle`, `.title`, `.headline`, `.body`, `.caption`). **Nunca tamanhos fixos em pontos** para texto de conteúdo.
- Hierarquia por **tamanho + peso + cor**, não por posição. Secundário desenfatizado (`.secondary`), não encolhido até ficar ilegível.
- **Comprimento de linha 45–75 caracteres** em texto corrido (guias, descrições, faturas). Acima disso o olho perde a linha — limitar com `.frame(maxWidth: 600)`.
- Números em tabelas e totais alinhados à **direita**, com casas decimais consistentes; texto alinhado à esquerda. Nada de texto longo centrado.
- Texto sempre em **Português (PT)**. Moeda formatada por `formatCurrency(_:)` (`Utils/Constants.swift`), nunca concatenada à mão.
- PT é ~20% mais longo que EN: testar os botões com as frases reais ("Finalizar venda", "Fechar caixa") sem truncar.

## 4. Liquid Glass

- **Obrigatório em toda a UI onde for possível.** Superfície que se lê como card, painel, folha, barra ou botão de ação leva vidro nativo — não é opção de gosto. Só fica sem vidro o que não pode: texto corrido dentro de um card já em vidro, conteúdo de tabela densa, e superfícies onde o vidro faria vidro sobre vidro ou baixaria o contraste abaixo de 4.5:1 (nesse caso, camada opaca por baixo do texto).
- Vidro tingido pela cor semântica quando a superfície tem estado (validade, stock, indicador): `.glassEffect(.regular.tint(cor.opacity(0.10–0.16)), in: .rect(cornerRadius: 16))`. A cor do ícone e a do vidro são a mesma.
- Superfícies de card/painel: `.glassEffect(.regular, in: .rect(cornerRadius: 16))`.
- Botões de ação: `.buttonStyle(.glass)`.
- Elementos próximos que devem fundir-se: envolver num `GlassEffectContainer`.
- **Um só plano de vidro por secção.** Vidro sobre vidro fica lamacento — proibido.
- Verificar contraste do texto sobre vidro em modo **claro e escuro** antes de dar a tarefa por feita. Se falhar 4.5:1, pôr uma camada opaca por baixo do texto — não baixar o requisito.
- Vidro sobre gradiente de marca só em cabeçalhos de destaque (totais, paywall).

## 5. Animação e transição

- **Animação e transição são obrigatórias, não decorativas.** Toda a mudança de estado visível anima (`.animation(_:value:)`, `withAnimation`) e tudo o que entra ou sai do ecrã tem `.transition(...)`. UI entregue com mudanças secas está por acabar — a única excepção é a lista das ações de alta frequência mais abaixo e o `Reduce Motion`.
- Toda a mudança de estado visível anima. Nada aparece nem desaparece de forma seca.
- **Durações**: microinteração 100–200 ms · transição de vista 200–300 ms · sheet/painel 300–350 ms. **Acima de 500 ms parece lento; abaixo de ~80 ms parece um bug.**
- Curvas: `.easeOut` para entrar, `.easeIn` para sair, `.easeInOut` para mudanças de layout, `.spring` só em interação direta (arrastar, stepper, adicionar ao carrinho).
- Animar **opacidade, escala e posição**. Não animar largura, altura ou padding em listas grandes — obriga a recalcular layout e perde-se fluidez.
- Entradas começam em `scale(0.95)`, nunca em `scale(0)`.
- Filtros e pesquisa: `.animation(.easeInOut, value: <coleção filtrada>.count)`.
- Listas e grelhas animam inserção, remoção e reordenação.
- Sheets e navegação de detalhe: `.transition(...)` e, quando há continuidade visual, `matchedGeometryEffect`.
- **Ações de alta frequência não animam**: adicionar ao carrinho com o scanner, teclas rápidas, stepper repetido. Animação em fluxo repetitivo é atrito.
- Respeitar `@Environment(\.accessibilityReduceMotion)` — reduzir a fade simples, nunca partir a UI.

## 6. Feedback e performance percebida

| Tempo de resposta | Regra |
|---|---|
| ≤ 100 ms | Sente-se instantâneo. Alvo para toque, stepper, filtro, pesquisa local. |
| ≤ 400 ms | Limite para manter o utilizador em fluxo. Alvo para gravar uma venda. |
| > 1 s | Obrigatório indicador de progresso. |
| > 10 s | Obrigatório progresso com percentagem e forma de cancelar (render de PDF, transferência por proximidade). |

- **Não mostrar indicador para operações abaixo de ~300 ms** — o pisca-pisca parece avaria.
- Ação irreversível ou lenta: desativar o botão durante a execução, para não haver duplo envio de venda.
- Uma venda finalizada mostra confirmação explícita (recibo ou toast), nunca um ecrã que simplesmente volta atrás.

## 7. Estados obrigatórios

Cada ecrã que carrega ou mostra dados trata todos os estados:

| Estado | Regra |
|---|---|
| Carregamento | Indicador de progresso; nunca ecrã em branco parado. |
| Vazio | `AppEmptyStateView` (em `Utils/AppTheme.swift`) com ícone, frase em PT e ação sugerida — nunca um vazio mudo. |
| Erro | Mensagem legível em PT, com ação de recuperação. Nunca mostrar erro SQL cru nem dados sensíveis. |
| Parcial | Se só parte dos dados carregou, dizê-lo — não apresentar dados incompletos como completos. |
| Sem ligação | Estado explícito nos ecrãs de proximidade e subscrição (é a única parte da app que depende de rede). |
| Conteúdo | Contador de resultados quando há pesquisa ou filtro ativo. |

## 8. Formulários

O padrão onde mais se ganha: validação inline mede +22% de sucesso, −22% de erros e −42% de tempo face a validar só no fim.

- **Label visível por cima do campo, sempre.** Placeholder nunca substitui label — desaparece ao escrever e não é lido de forma fiável por leitores de ecrã.
- **Validar ao sair do campo** (perda de foco), não a cada tecla. Erro por baixo do campo, alinhado com a label, um por campo.
- Mensagem de erro diz **o que está errado e como corrigir**: "O preço base tem de ser maior que zero.", não "Valor inválido.".
- Botão de guardar desativado enquanto a validação não passa (`canSave`), **com a razão visível** — botão morto e sem explicação é dos piores atritos.
- Nunca apagar o que o utilizador escreveu por causa de um erro noutro campo.
- Formulários longos partem-se em passos (wizard) com indicador de progresso e passo concluído clicável.
- Rodapé de ações fixo: "Voltar" · "Cancelar" · "Guardar".
- Campos numéricos com teclado adequado em iOS (`.keyboardType(.decimalPad)`) e `onSubmit` a saltar para o campo seguinte em macOS.
- Estado válido/inválido com **cor + ícone** (check / exclamação), nunca só a cor da borda.

## 9. Listas, grelhas e tabelas densas

- Altura de linha: **44–48 pt** normal, **36–40 pt** em modo compacto. Se houver modo compacto, é uma preferência, não o valor por omissão.
- Cabeçalhos fixos ao rolar; totais visíveis sem chegar ao fim da lista.
- Ordenação por coluna e pesquisa com realce da correspondência.
- macOS: ações secundárias reveladas em `hover` e disponíveis também em `.contextMenu` — hover sozinho não é acessível por teclado.
- Linhas horizontais simples por omissão; grelha completa só onde a densidade a exige.
- Listas longas usam `LazyVStack`/`LazyVGrid`. Uma grelha de vendas com centenas de produtos não pode construir tudo de uma vez.

## 10. Adaptação macOS ↔ iOS

- macOS: navegação por sidebar (`NavigationSplitView`), sheets com `.frame(minWidth:idealWidth:minHeight:)` para não haver scroll desnecessário, exportação revelada no Finder (`NSWorkspace.shared.activateFileViewerSelecting`).
- iOS: `TabView`, sheets em altura natural, exportação via `ShareSheet` (`List_Storage/ShareSheet.swift` — reutilizar, não duplicar).
- Diferenças de plataforma isoladas com `#if os(macOS)`, nunca ficheiros de View duplicados.
- **Alvos**: iOS mínimo **44×44 pt**; macOS controlos compactos (~22–28 pt) mas nunca abaixo de 24×24 pt de área clicável.
- **macOS é dirigido por teclado**: `.keyboardShortcut` nas ações frequentes (⌘N novo produto, ⌘F pesquisar, ⏎ confirmar, Esc fechar sheet), estados de `hover` nos elementos interativos, `Tab` percorre tudo por ordem lógica.
- Não replicar o padrão iOS no Mac: nada de menu "hambúrguer" no desktop, nada de sheet a ocupar o ecrã inteiro quando um painel chega.

## 11. Acessibilidade (WCAG 2.2 AA + Apple)

- Todo o ícone-só-ícone leva `.accessibilityLabel(...)` em PT.
- Nunca comunicar informação apenas por cor (ver secção 2).
- **Foco sempre visível** e nunca tapado por cabeçalho fixo ou toolbar; ordem de tabulação lógica.
- Suportar Dynamic Type: layouts com `ViewThatFits` ou quebra de linha em vez de truncar informação crítica. Testar no tamanho acessível maior — o preço final e o total nunca podem ficar cortados.
- Navegação por teclado funcional em macOS (Tab, Enter para confirmar, Esc para fechar sheet).
- `accessibilityReduceMotion` e `accessibilityReduceTransparency` respeitados — com transparência reduzida, o vidro passa a superfície opaca legível.
- Agrupar com `.accessibilityElement(children: .combine)` o que é lido como uma unidade (linha de produto, card de venda).

## 12. Texto e microcopy

- Verbos imperativos nos botões: "Guardar", "Finalizar venda", "Fechar caixa". Nunca "OK" sozinho num diálogo de decisão.
- Confirmações destrutivas dizem o que vai acontecer e a quantos itens: "Apagar 12 produtos desta categoria?".
- Preferir **desfazer** a pedir confirmação, sempre que a operação for reversível.
- Sem jargão técnico visível ao utilizador. "Não foi possível guardar a venda." em vez do erro do SQLite.
- Números com unidade e moeda coerentes em todo o ecrã.

## 13. Padrões proibidos (paywall e subscrição)

A app tem período de teste e paywall — é onde os padrões enganosos aparecem, e são risco legal além de risco de confiança.

- Preço, periodicidade e renovação automática visíveis **antes** do botão de compra, no mesmo ecrã.
- Cancelar tem de ser tão fácil quanto subscrever, e o caminho é indicado na app.
- **Proibido** o "confirmshaming" ("Não, prefiro perder dinheiro"), opções pré-selecionadas escondidas, contagens decrescentes falsas e botão de recusa escondido em texto cinzento minúsculo.
- Fim do período de teste é avisado com antecedência, sem bloquear o acesso aos dados já introduzidos.
- Dados do utilizador continuam exportáveis mesmo com a subscrição expirada.

## 14. Componentes partilhados

Antes de criar um componente novo, procurar em `Utils/AppTheme.swift` e `Views/Reports/ReportComponents.swift`. Duplicar componente é falha de revisão.

## 15. Revisão de UI — checklist antes de fechar a tarefa

- [ ] Plano de UX escrito em `Docs/planning/PLAN.md` **antes** de implementar — e o ficheiro esvaziado depois de a UI ficar feita.
- [ ] Vidro em todas as superfícies onde é possível, um só plano por secção, tingido pela cor do estado quando o há.
- [ ] Todas as mudanças de estado animadas e tudo o que entra/sai com `.transition(...)`.
- [ ] Espaçamentos na escala (4/8/12/16/24/32/48); raios de canto na escala (8/12/16).
- [ ] Zero cores fora de `AppTheme`; contraste 4.5:1 verificado em claro **e** escuro, sobre vidro incluído.
- [ ] Nenhuma informação transmitida só por cor.
- [ ] Todos os estados tratados: carregamento, vazio, erro, parcial, sem ligação, conteúdo.
- [ ] Animações entre 100–350 ms, com `Reduce Motion` respeitado.
- [ ] Toda a ação tem feedback; nada acima de 1 s sem indicador.
- [ ] Formulário: labels visíveis, validação ao sair do campo, erro acionável junto ao campo, razão do botão desativado visível.
- [ ] Alvos ≥ 44 pt em iOS; atalhos de teclado e `hover` em macOS; foco visível e ordem de Tab correta.
- [ ] Dynamic Type no tamanho maior sem truncar preços, totais nem nomes de produto.
- [ ] Texto em PT, imperativo, sem jargão; confirmação destrutiva diz o que apaga.
- [ ] Nenhum componente duplicado que já exista em `AppTheme` ou `ReportComponents`.

Revisão heurística: 3 a 5 passagens independentes por esta checklist apanham ~75% dos problemas — vale mais do que uma leitura demorada de uma pessoa só.
