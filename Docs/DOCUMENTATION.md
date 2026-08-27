# Índice de Documentação — Sales POS

Todos os ficheiros `.md` do projeto vivem em `Docs/`, exceto `README.md` e `CLAUDE.md` (raiz).
Os nomes seguem a convenção de `NAME_MD.md` e estão organizados por área (`architecture/`, `database/`, `security/`, `development/`, `features/`, `guides/`, `planning/`).
Sempre que um `.md` for criado, renomeado, movido ou apagado, esta tabela tem de ser atualizada (ver `CLAUDE.md`, secção 2).

## Raiz

| **Number** | **Ficheiro** | **Descrição**                          |
| ---------- | ------------ | -------------------------------------- |
| 0.1        | `README.md`  | Visão geral e estrutura do projeto     |
| 0.2        | `CLAUDE.md`  | Regras obrigatórias de desenvolvimento |

## Docs/ (raiz)

| **Number** | **Link**             | **Caminho**              | **Descrição**                                       |
| ---------- | -------------------- | ------------------------ | --------------------------------------------------- |
| 1.1        | [[DOCUMENTATION]]    | `Docs/DOCUMENTATION.md`  | Este índice de todos os `.md` do projeto            |
| 1.2        | [[TODO]]             | `Docs/TODO.md`           | Tarefas do ciclo atual (Backend → Frontend)         |
| 1.3        | [[CHANGELOG]]        | `Docs/CHANGELOG.md`      | Histórico dos ciclos de `TODO.md` já fechados       |
| 1.4        | [[PROJECT_OVERVIEW]] | `Docs/PROJECT_OVERVIEW.md` | Documentação completa da app (visão geral funcional) |

## Docs/architecture/

| **Number** | **Link**            | **Caminho**                             | **Descrição**                                                                 |
| ---------- | ------------------- | --------------------------------------- | ----------------------------------------------------------------------------- |
| 2.1        | [[ARCHITECTURE]]    | `Docs/architecture/ARCHITECTURE.md`     | Camadas, regras de dependência, fluxos, serviços, dívida arquitetural         |
| 2.2        | [[SYSTEM_DESIGN]]   | `Docs/architecture/SYSTEM_DESIGN.md`    | Diagramas Mermaid do sistema inteiro (venda, impressão de facturas, lotes, validade, administração, produtos parados, fecho por caixa, relatórios, subscrição, proximidade) |
| 2.3        | [[TECHNICAL_DESIGN]] | `Docs/architecture/TECHNICAL_DESIGN.md` | Design técnico: modelos, enums, constantes, fluxos internos                   |

## Docs/database/

| **Number** | **Link**     | **Caminho**                  | **Descrição**                                          |
| ---------- | ------------ | ---------------------------- | ------------------------------------------------------ |
| 3.1        | [[DATABASE]] | `Docs/database/DATABASE.md`  | Esquema SQLite, `erDiagram`, relações, migrações, índices |

## Docs/security/

| **Number** | **Link**     | **Caminho**                  | **Descrição**                                                |
| ---------- | ------------ | ---------------------------- | ------------------------------------------------------------ |
| 4.1        | [[SECURITY]] | `Docs/security/SECURITY.md`  | Modelo de ameaça, regras técnicas, catálogo de validações, cinco rondas (V1–V5), testes, auditoria e registo de validações |
| 4.2        | [[SECURITY_POLICY]] | `Docs/security/SECURITY_POLICY.md` | Como o projeto garante a segurança e o que fazer quando existe uma falha: portões, papéis, severidade, resposta a incidente |

## Docs/development/

| **Number** | **Link**        | **Caminho**                        | **Descrição**                                          |
| ---------- | --------------- | ---------------------------------- | ------------------------------------------------------ |
| 5.1        | [[STYLE_GUIDE]] | `Docs/development/STYLE_GUIDE.md`  | Regras de UI/UX, acessibilidade, Liquid Glass, animação |
| 5.2        | [[TESTING]]     | `Docs/development/TESTING.md`      | Teste de implementação antes da UX/UI, índice das suites, bateria de entradas hostis |
| 5.3        | [[ERRORS]]      | `Docs/development/ERRORS.md`       | Erros encontrados e resolvidos: sintoma, causa, solução e prova, com índice |

## Docs/features/

| **Number** | **Link**                      | **Caminho**                                     | **Descrição**                                      |
| ---------- | ----------------------------- | ----------------------------------------------- | -------------------------------------------------- |
| 6.1        | [[FEATURE_PROXIMITY]]         | `Docs/features/FEATURE_PROXIMITY.md`            | Partilha por proximidade — visão geral (Bonjour + Network.framework) |
| 6.2        | [[INSTALL_PROXIMITY]]         | `Docs/features/INSTALL_PROXIMITY.md`            | Partilha por proximidade — configuração e setup    |
| 6.3        | [[PROXIMITY_WAITING_LIST]]    | `Docs/features/PROXIMITY_WAITING_LIST.md`       | Partilha por proximidade — sinalização "aguardar lista" |
| 6.4        | [[FEATURE_LOW_STOCK_SHARING]] | `Docs/features/FEATURE_LOW_STOCK_SHARING.md`    | Exportação/partilha de stock baixo (`.posstock`)   |

## Docs/guides/

| **Number** | **Link**         | **Caminho**                      | **Descrição**                                     |
| ---------- | ---------------- | -------------------------------- | ------------------------------------------------- |
| 7.1        | [[USER_GUIDE]]   | `Docs/guides/USER_GUIDE.md`      | Guia do utilizador final                          |
| 7.2        | [[UI_WIREFRAMES]] | `Docs/guides/UI_WIREFRAMES.md`  | Wireframes dos ecrãs (transferência por proximidade) |

## Docs/planning/

| **Number** | **Link**    | **Caminho**                 | **Descrição**                                                     |
| ---------- | ----------- | --------------------------- | ----------------------------------------------------------------- |
| 8.1        | [[ROADMAP]] | `Docs/planning/ROADMAP.md`  | Análise de mercado e funcionalidades em falta face à concorrência |
| 8.2        | [[PLAN]]    | `Docs/planning/PLAN.md`     | Cache do plano de UX da UI em curso — esvaziado quando a UI fica feita (`STYLE_GUIDE` §0.1) |
