# POSApp — Guia do Utilizador

**Versão:** 1.1.0  
**Sistema:** macOS e iPadOS

---

## Índice

1. [[#Primeiro Acesso]]
2. [[#Ecrã Principal]]
3. [[#Gestão de Produtos]]
4. [[#Realizar uma Venda]]
5. [[#Métodos de Pagamento]]
6. [[#Faturas]]
7. [[#Fecho de Caixa]]
8. [[#Relatórios]]
9. [[#Definições e Utilizadores]]
10. [[#Relatórios Automáticos]]
11. [[#Dados e Ficheiros]]
12. [[#Perguntas Frequentes]]

---

## Primeiro Acesso

Ao abrir o POSApp pela primeira vez, é apresentado o ecrã de login.

**Credenciais iniciais:**

- Utilizador: `admin`
- Password: `admin123`

> ⚠️ **Importante:** Após o primeiro login, vá às **Definições** e altere a password do administrador.

```mermaid
flowchart TD
    A([Abrir POSApp]) --> B[Ecrã de Login]
    B --> C{Credenciais válidas?}
    C -- Não --> D[Mensagem de erro]
    D --> B
    C -- Sim --> E[Ecrã Principal]
    E --> F{Primeiro acesso?}
    F -- Sim --> G[⚠️ Alterar password do admin\nem Definições]
    F -- Não --> H[Usar a aplicação]
    G --> H
```

---

## Ecrã Principal

Após o login, o ecrã principal divide-se em 4 secções:

|Secção|Ícone|Descrição|
|---|---|---|
|Vendas|🛒|Realizar vendas e gerir o carrinho|
|Produtos|📦|Gerir catálogo de produtos e stock|
|Relatórios|📊|Consultar e exportar relatórios|
|Definições|⚙️|Gerir utilizadores e configurações (só admins)|

**No macOS** a navegação está na barra lateral esquerda.  
**No iPad** a navegação está na barra inferior.

```mermaid
graph LR
    App([POSApp]) --> V(🛒 Vendas)
    App --> P(📦 Produtos)
    App --> R(📊 Relatórios)
    App --> D(⚙️ Definições\nSó Admin)

    V --> V1[Pesquisar produto]
    V --> V2[Carrinho]
    V --> V3[Finalizar Venda]

    P --> P1[Lista de produtos]
    P --> P2[Criar / Editar]
    P --> P3[Apagar]

    R --> R1[Diário]
    R --> R2[Mensal]
    R --> R3[Histórico]
    R --> R4[Fecho de Caixa]

    D --> D1[Utilizadores]
    D --> D2[Terminar Sessão]
    D --> D3[Pasta Relatórios]
```

---

## Gestão de Produtos

### Ver produtos

Na secção **Produtos** encontra a lista completa do catálogo.

Cada produto mostra:

- Nome e código de barras (se definido)
- Preço base, IVA e margem de lucro
- Preço final (calculado automaticamente)
- Stock disponível (laranja se abaixo de 5 unidades)

### Pesquisar produto

Use a barra de pesquisa no topo da lista para filtrar produtos por **nome ou código de barras**. A pesquisa é em tempo real.

### Código de Barras

Cada produto pode ter um código de barras associado. O código de barras:

- É único no sistema — não é possível ter dois produtos com o mesmo código
- Permite pesquisa direta por scanner ou por digitação
- É opcional — produtos sem código de barras funcionam normalmente

Para usar um **scanner de código de barras** na secção de Vendas, aponte o scanner para o código do produto. O produto é adicionado automaticamente ao carrinho.

### Criar produto

```mermaid
flowchart TD
    A([Botão +]) --> B[Formulário Novo Produto]
    B --> C[Nome do produto]
    B --> D[Código de barras\nopcional]
    B --> E[Preço Base]
    B --> F[IVA — slider 0% a 30%\ndefault 16%]
    B --> G[Margem de Lucro\nslider 0% a 200%]
    B --> H[Stock]
    E & F & G --> I[Preço Final\ncalculado em tempo real]
    I --> J{Clicar Criar}
    J -- Barcode duplicado --> K[❌ Erro — código já existe]
    J -- OK --> L[✅ Produto guardado]
```

**Fórmula do preço final:**

> Preço Base × (1 + Margem%) × (1 + IVA%)

_Exemplo: 10€ base + 20% margem + 16% IVA = **13,92€**_

### Editar produto

Clique em qualquer produto da lista para abrir o formulário de edição. Altere os campos e clique **Guardar**.

### Apagar produto

Na lista de produtos, deslize o item para a esquerda (iPad) ou use o botão de lixo para apagar.

> ⚠️ A eliminação é permanente. Vendas anteriores com este produto não são afetadas — o nome e preço ficam gravados no histórico.

---

## Realizar uma Venda

```mermaid
flowchart TD
    A([Secção Vendas]) --> B[Pesquisar produto\npor nome ou barcode]
    B --> B2{Produto encontrado?}
    B2 -- Não --> B
    B2 -- Sim --> C{Stock disponível?}
    C -- Não --> D[❌ Produto acinzentado\nnão pode ser adicionado]
    C -- Sim --> E[Ajustar quantidade]
    E --> F[Adicionar ao carrinho ➕]
    F --> G{Mais produtos?}
    G -- Sim --> B
    G -- Não --> H[Dados do cliente\nopcional: Nome + NIF]
    H --> I[Selecionar método de pagamento]
    I --> J[Finalizar Venda]
    J --> K[Stock atualizado automaticamente]
    K --> L[Fatura apresentada]
    L --> M([Nova venda])
```

### Carrinho

O carrinho aparece à direita do ecrã (macOS) ou em baixo (iPad).

Para **remover um item** do carrinho, clique no ícone de lixo ao lado do item.

Para **limpar o carrinho** completamente, clique no botão **Limpar** (vermelho). Será pedida confirmação.

---

## Métodos de Pagamento

O POSApp suporta **pagamento misto** — uma venda pode ser paga com múltiplos métodos simultaneamente.

### Métodos disponíveis

|Método|Descrição|
|---|---|
|💵 Dinheiro|Pagamento em numerário|
|💳 Cartão|Cartão de débito ou crédito|
|🏦 Transferência Bancária|Transferência directa entre contas|
|📱 M-Pesa|Pagamento via M-Pesa|
|📱 e-Mola|Pagamento via e-Mola|

### Fluxo de pagamento misto

```mermaid
flowchart TD
    A([Total da venda calculado]) --> B[Selecionar métodos de pagamento]
    B --> C{Quantos métodos?}

    C -- Um --> D[Introduzir valor total\nnesse método]
    C -- Vários --> E[Distribuir valor\npor cada método]

    D --> F{Referência necessária?\nM-Pesa / e-Mola / Transf.}
    E --> F

    F -- Sim --> G[Preencher referência\nda transação]
    F -- Não --> H{Soma cobre o total?}
    G --> H

    H -- Não --> I[❌ Corrigir valores]
    I --> E
    H -- Sim --> J[✅ Confirmar pagamento]
    J --> K([Venda registada])
```

> 💡 **Exemplo:** Uma venda de 1.500 MT pode ser paga com 500 MT em dinheiro + 1.000 MT via M-Pesa.

### Referências de pagamento

Para pagamentos digitais (M-Pesa, e-Mola, Transferência), é recomendável preencher o campo **referência** com o número de confirmação da transação. Esta referência fica gravada no histórico da venda.

---

## Faturas

Após finalizar uma venda, a fatura é apresentada automaticamente com:

- Número da fatura (ID da venda)
- Data e hora
- Nome e NIF do cliente (se preenchido)
- Lista de artigos com quantidade, preço unitário e subtotal
- Métodos de pagamento utilizados
- Total da venda

Feche a fatura clicando **Fechar** para realizar uma nova venda.

---

## Fecho de Caixa

O fecho de caixa regista o resumo financeiro do dia e fecha o período para efeitos contabilísticos.

> ⚠️ Só é possível fazer **um fecho por dia**. Se necessário refazer, o registo anterior é substituído.

```mermaid
flowchart TD
    A([Relatórios → Fecho de Caixa]) --> B[Resumo automático do dia]
    B --> C[Total vendas\nTotal por método de pagamento\nNº de vendas]
    C --> D[Adicionar notas\nopcional]
    D --> E{Dia já fechado?}
    E -- Não --> F[Clicar Fechar Caixa]
    E -- Sim --> G[⚠️ Confirmação:\nsubstituir registo anterior?]
    G -- Cancelar --> H([Sair sem fechar])
    G -- Confirmar --> F
    F --> I[✅ Registo guardado em DayCloses]
    I --> J([Fecho concluído])
```

### O que fica registado

|Campo|Descrição|
|---|---|
|Data|Dia do fecho (`AAAA-MM-DD`)|
|Total vendas|Soma de todas as vendas do dia|
|Total dinheiro|Soma de todos os pagamentos em numerário|
|Total cartão|Soma de todos os pagamentos por cartão|
|Total transf. bancária|Soma de todas as transferências|
|Total M-Pesa|Soma de todos os pagamentos M-Pesa|
|Total e-Mola|Soma de todos os pagamentos e-Mola|
|Nº de vendas|Contagem de vendas do dia|
|Notas|Observações do operador|
|Fechado por|Utilizador que efetuou o fecho|
|Fechado às|Timestamp exacto do fecho|

### Consultar fechos anteriores

No histórico de fechos de caixa pode filtrar por mês. Para cada registo pode ver o detalhe completo por método de pagamento.

---

## Relatórios

```mermaid
flowchart LR
    A([Secção Relatórios]) --> B[Diário]
    A --> C[Mensal]
    A --> D[Histórico]

    B --> B1[Selecionar data]
    B1 --> B2[Resumo: total, nº vendas,\nproduto mais vendido]
    B2 --> B3[Exportar CSV]
    B2 --> B4[Exportar PDF]

    C --> C1[Selecionar mês]
    C1 --> C2[Agregado mensal]
    C2 --> C3[Exportar CSV]
    C2 --> C4[Exportar PDF]

    D --> D1[Lista de relatórios\nexportados]
    D1 --> D2[Abrir ficheiro ↗]
    D1 --> D3[Remover registo 🗑]
```

### Diário

1. Selecione a **data** com o seletor
2. Veja o resumo: total de vendas, número de vendas, itens vendidos e produto mais vendido
3. Consulte a lista detalhada de todas as vendas do dia, incluindo os métodos de pagamento utilizados

**Exportar:** CSV (folha de cálculo) ou PDF.

### Mensal

Agrega as vendas de um mês completo. Selecione o mês com o seletor de data.

### Histórico

Lista todos os relatórios já exportados com tipo, período, data de criação e indicação se o ficheiro existe no disco.

---

## Definições e Utilizadores

> Esta secção é acessível apenas a utilizadores com perfil **Administrador**.

```mermaid
flowchart TD
    A([Definições — só Admin]) --> B[Lista de utilizadores]
    B --> C[Criar utilizador]
    B --> D[Editar utilizador]
    B --> E[Apagar utilizador]

    C --> C1[Nome + Username\nPassword + Função]
    C1 --> C2{Password maior ou igual 6 chars?}
    C2 -- Não --> C1
    C2 -- Sim --> C3[✅ Utilizador criado]

    D --> D1[Alterar dados]
    D1 --> D2{Password preenchida?}
    D2 -- Sim --> D3[Atualiza password]
    D2 -- Não --> D4[Mantém password atual]

    E --> E1{É o próprio utilizador?}
    E1 -- Sim --> E2[❌ Não permitido]
    E1 -- Não --> E3[Confirmação]
    E3 --> E4[✅ Utilizador apagado]
```

### Funções disponíveis

|Função|Vendas|Produtos|Relatórios|Fecho de Caixa|Definições|
|---|---|---|---|---|---|
|Caixa|✅|✅|✅|✅|❌|
|Administrador|✅|✅|✅|✅|✅|

### Terminar sessão

Clique em **Terminar Sessão** na secção "Sessão Atual" para sair.

---

## Relatórios Automáticos

```mermaid
flowchart TD
    A([App fechada ou\nem segundo plano]) --> B{Há vendas hoje?}
    B -- Não --> C([Nenhum ficheiro gerado])
    B -- Sim --> D[Exportar CSV do dia]
    D --> E[Exportar PDF do dia]
    E --> F{É o último dia\ndo mês?}
    F -- Não --> G([Concluído])
    F -- Sim --> H[Exportar CSV mensal]
    H --> I[Exportar PDF mensal]
    I --> G
```

### Onde ficam os ficheiros

**macOS:**

```
~/Documents/POSApp_Relatorios/
```

**iPad:**  
Pasta Documents da app, acessível via **Ficheiros** do iOS.

Para abrir a pasta diretamente no macOS, vá a **Definições → Abrir pasta de relatórios**.

---

## Dados e Ficheiros

```mermaid
graph TD
    A([POSApp]) --> B[(Base de dados SQLite)]
    A --> C[Relatórios exportados]

    B --> B1["macOS\n~/Library/Application Support/posapp.sqlite"]
    B --> B2["iPad\nInterno — não acessível\npelo sistema de ficheiros"]

    C --> C1["macOS\n~/Documents/POSApp_Relatorios/"]
    C --> C2["iPad\nDocuments da app\nvia Ficheiros do iOS"]
```

### Estrutura dos dados

|Tabela|Conteúdo|
|---|---|
|`Users`|Utilizadores e credenciais|
|`Products`|Catálogo de produtos com preços e stock|
|`Sales`|Cabeçalho de cada venda|
|`SaleItems`|Linhas de detalhe de cada venda|
|`Payments`|Pagamentos por método de cada venda|
|`DayCloses`|Resumos de fecho de caixa diário|
|`Reports`|Metadados dos relatórios exportados|

> ℹ️ Para documentação técnica completa da base de dados, consulte `Docs/database/DATABASE.md`.

### Sincronização entre dispositivos

Na versão atual os dados são **locais em cada dispositivo**. A sincronização entre macOS e iPad está prevista para uma versão futura.

---

## Perguntas Frequentes

**O stock não está a baixar após uma venda. O que fazer?**  
Verifique se a venda foi finalizada com sucesso (fatura apresentada). Se sim, o stock foi atualizado. Refresque a lista de produtos saindo e voltando ao separador.

---

**Esqueci-me da password. Como recuperar?**  
Não é possível recuperar a password diretamente. Um administrador pode editar o utilizador e definir uma nova password em **Definições → (utilizador) → Editar**.

---

**O relatório PDF está em branco.**  
Certifique-se de que existem vendas no período selecionado antes de exportar. Se não houver vendas, o ficheiro será exportado vazio.

---

**Posso registar uma venda com pagamento parcial em dinheiro e o restante por M-Pesa?**  
Sim. Na finalização da venda, selecione ambos os métodos (Dinheiro e M-Pesa) e distribua o valor total pelos dois. Adicione a referência da transação M-Pesa no campo correspondente.

---

**O fecho de caixa já foi feito mas preciso de corrigir. Posso refazer?**  
Sim. Ao fazer um novo fecho para o mesmo dia, o registo anterior é substituído automaticamente. O histórico guarda sempre o último fecho do dia.

---

**Como alterar a taxa de IVA padrão?**  
No formulário de cada produto, ajuste o slider de IVA individualmente. O valor padrão (16%) é definido em `Constants.swift` e pode ser alterado pelo programador.

---

**O scanner de código de barras não está a reconhecer o produto.**  
Verifique que o produto tem o código de barras correctamente registado em **Produtos → (produto) → Editar**. O código deve corresponder exactamente ao que está no produto físico.

---

**Posso ter dois produtos com o mesmo código de barras?**  
Não. O sistema rejeita duplicados. Produtos sem código de barras não têm esta restrição.

---

_POSApp v1.1.0 — Sistema de Vendas para macOS e iPadOS_
