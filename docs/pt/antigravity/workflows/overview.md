# Workflows — Os 14 Workflows Nativos

> **Atualizado:** 2026-02-26 | **Total:** 14 workflows + README de seleção

Os **14 workflows** em `.antigravity/workflows/` são equivalentes a slash commands e sequências do Claude Code, traduzidos e enriquecidos para o formato nativo do Antigravity.

---

## O que são Workflows no Antigravity?

No Claude Code, os workflows eram slash commands como `/AIOS:story`, `/cohort-squad:create`. No Antigravity, eles são arquivos `.md` em `.antigravity/workflows/` que os agentes executam como sequências de passos estruturados.

**Formato:**

```yaml
---
description: breve descrição do workflow
---
## Passos
1. ...
2. ...
```

> **Índice completo com guia de seleção:** [`.antigravity/workflows/README.md`](../../../../.antigravity/workflows/README.md)

---

## Tabela Completa de Workflows

### Greenfield — Projetos Novos

| Workflow               | Quando Usar                        | Responsável                                                      |
| ---------------------- | ---------------------------------- | ---------------------------------------------------------------- |
| `greenfield-fullstack` | Nova aplicação full-stack do zero  | `@analyst → @pm → @ux → @architect → @po → @dev → @qa → @devops` |
| `greenfield-service`   | Novo backend/API do zero           | `@architect → @data-engineer → @dev → @qa`                       |
| `greenfield-ui`        | Novo frontend/landing page do zero | `@ux → @dev → @qa` (+ Stitch MCP)                                |

### Brownfield — Projetos Existentes

| Workflow               | Quando Usar                        | Responsável                                    |
| ---------------------- | ---------------------------------- | ---------------------------------------------- |
| `brownfield-discovery` | Novo no projeto — precisa entender | `@architect → @analyst → @data-engineer → @ux` |
| `brownfield-fullstack` | Adicionar feature full-stack       | `@architect → @dev → @qa → @devops`            |
| `brownfield-service`   | Adicionar endpoint/serviço         | `@data-engineer → @dev → @qa`                  |
| `brownfield-ui`        | Adicionar página/componente        | `@ux → @dev → @qa` (+ browser_subagent)        |

### Desenvolvimento e Qualidade

| Workflow                  | Quando Usar                         | Responsável                                |
| ------------------------- | ----------------------------------- | ------------------------------------------ |
| `story-development-cycle` | Implementar uma story               | `@sm → @po → @dev → @qa → @devops`         |
| `spec-pipeline`           | Ideia → backlog completo            | `@pm → @analyst → @architect → @po → @dev` |
| `epic-orchestration`      | Executar épico completo             | `@po → @sm → @dev → @qa → @devops`         |
| `qa-loop`                 | QA reprovou → corrigir e re-validar | `@qa → @dev → @qa` (máx. 5 iterações)      |

### Especiais

| Workflow              | Quando Usar                          | Responsável                      |
| --------------------- | ------------------------------------ | -------------------------------- |
| `design-system-build` | Criar ou refatorar design system     | `@ux → @brad-frost → @dev → @qa` |
| `create-squad`        | Criar squad de especialistas         | `@squad-chief → @oalanicolas`    |
| `auto-worktree`       | Desenvolvimento paralelo de features | `@devops`                        |

### Correspondência com Claude Code

| Slash Command Claude   | Workflow Antigravity                            |
| ---------------------- | ----------------------------------------------- |
| `/AIOS:story`          | `story-development-cycle.md`                    |
| `/AIOS:spec-pipeline`  | `spec-pipeline.md`                              |
| `/cohort-squad:create` | `create-squad.md`                               |
| `/cohort-squad:sync`   | `auto-worktree.md` (parcial)                    |
| Analysis commands      | `brownfield-discovery.md`                       |
| _(não existia)_        | `greenfield-fullstack.md` (novo)                |
| _(não existia)_        | `greenfield-ui.md` + Stitch MCP **(exclusivo)** |
| _(não existia)_        | `design-system-build.md` **(exclusivo)**        |
| _(não existia)_        | `epic-orchestration.md` (novo)                  |
| _(não existia)_        | `qa-loop.md` (novo)                             |

---

## Detalhes dos Workflows Principais

### `story-development-cycle` — Ciclo Completo de Story

**Arquivo:** `.antigravity/workflows/story-development-cycle.md`

O workflow mais usado — governa o ciclo completo de desenvolvimento de uma feature.

**Sequência:**

```
@sm *draft
  ↓
@po *validate
  ↓
@dev *develop
  ↓
@qa *qa-gate
  ↓
@devops *push
```

| Etapa    | Agente    | Artefato                      | Critério de Saída                 |
| -------- | --------- | ----------------------------- | --------------------------------- |
| Draft    | `@sm`     | Story em `docs/stories/`      | Story com critérios iniciais      |
| Validate | `@po`     | Story com acceptance criteria | ACs mensuráveis e completos       |
| Develop  | `@dev`    | Código implementado           | Todos os ACs cobertos             |
| QA Gate  | `@qa`     | Relatório de qualidade        | lint ✅ + typecheck ✅ + tests ✅ |
| Push     | `@devops` | PR criado / branch pushed     | Remote atualizado                 |

---

### `greenfield-fullstack` — Projeto Full-Stack do Zero

**Arquivo:** `.antigravity/workflows/greenfield-fullstack.md`

Workflow completo para construir aplicações full-stack do zero. Inclui 4 fases:

```
Fase 0: Bootstrap de ambiente
Fase 1: Discovery & Planning (@analyst → @pm → @ux → @architect → @po)
Fase 2: Fragmentação de documentos
Fase 3: Ciclo de desenvolvimento (SDC repetido para cada story)
```

---

### `qa-loop` — Ciclo Iterativo de Correção QA

**Arquivo:** `.antigravity/workflows/qa-loop.md`

Ativado quando `@qa` emite veredicto `REJECT`. Opera com máximo de **5 iterações**:

```
@qa review → veredicto REJECT
  ↓
@qa create-fix-request
  ↓
@dev apply-fixes
  ↓
Incrementa iteração — volta para review
  ↓ (se iteração ≥ 5 ou BLOCKED)
ESCALAÇÃO para humano
```

**Veredictos:** `APPROVE` / `REJECT` / `BLOCKED`

---

### `design-system-build` — Design System com Stitch MCP

**Arquivo:** `.antigravity/workflows/design-system-build.md`

> ⭐ Workflow exclusivo do Antigravity — utiliza ferramentas que o Claude Code não possui.

```
@ux audit → @brad-frost atomic design review
→ mcp_stitch_* (wireframes e telas)
→ generate_image (assets visuais)
→ @dev implementa tokens e componentes
→ @qa valida visual com browser_subagent
```

---

### `create-squad` — Criação de Squad

**Arquivo:** `.antigravity/workflows/create-squad.md`

```
@squad-chief recebe request
→ Pesquisa mentes de elite (search_web)
→ Curada de especialistas reais com frameworks
→ DNA extraction por @oalanicolas
→ Geração de agentes
→ Estrutura do squad em squads/
```

---

## Encadeamento Natural entre Workflows

Alguns workflows se encadeiam naturalmente após a conclusão de outro:

| Workflow Concluído        | Próximo Sugerido                  | Condição                            |
| ------------------------- | --------------------------------- | ----------------------------------- |
| `brownfield-discovery`    | `brownfield-fullstack/service/ui` | Baseado no tipo de evolução         |
| `spec-pipeline`           | `epic-orchestration`              | Após épicos gerados                 |
| `epic-orchestration`      | `story-development-cycle`         | Para cada story                     |
| `story-development-cycle` | `qa-loop`                         | Se QA emitir REJECT                 |
| `greenfield-ui`           | `design-system-build`             | Quando design system for necessário |

---

## Documentação Relacionada

- [Índice de Workflows](../../../../.antigravity/workflows/README.md) — Seleção rápida completa
- [Agentes Core](../agents/core-agents.md) — Agentes que executam os workflows
- [Templates](../templates/overview.md) — Templates usados nos workflows
- [Skills](../skills/overview.md) — Skills chamadas durante os workflows
