# Workflows AntiGravity — Índice e Guia de Seleção

> Ponto de entrada único para todos os workflows do AIOS no ambiente AntiGravity.

**Total de Workflows:** 14 | **Última Atualização:** 2026-02-26

---

## Guia de Seleção Rápida

### Novo Projeto?

| Tipo de Projeto           | Workflow                                             |
| ------------------------- | ---------------------------------------------------- |
| Full-Stack (front + back) | [greenfield-fullstack.md](./greenfield-fullstack.md) |
| Backend / API apenas      | [greenfield-service.md](./greenfield-service.md)     |
| Frontend / UI apenas      | [greenfield-ui.md](./greenfield-ui.md)               |

### Projeto Existente?

| Situação                  | Primeiro passo                                       |
| ------------------------- | ---------------------------------------------------- |
| Não conheço o projeto     | [brownfield-discovery.md](./brownfield-discovery.md) |
| Conheço — Full-Stack      | [brownfield-fullstack.md](./brownfield-fullstack.md) |
| Conheço — Backend apenas  | [brownfield-service.md](./brownfield-service.md)     |
| Conheço — Frontend apenas | [brownfield-ui.md](./brownfield-ui.md)               |

### Processo de Desenvolvimento?

| Situação                              | Workflow                                                   |
| ------------------------------------- | ---------------------------------------------------------- |
| Tenho ideia → quero backlog pronto    | [spec-pipeline.md](./spec-pipeline.md)                     |
| Tenho épico → quero executar stories  | [epic-orchestration.md](./epic-orchestration.md)           |
| Story pronta → implementar e entregar | [story-development-cycle.md](./story-development-cycle.md) |
| QA reprovou → ciclo de correção       | [qa-loop.md](./qa-loop.md)                                 |
| Criar design system                   | [design-system-build.md](./design-system-build.md)         |
| Criar novo squad de agentes IA        | [create-squad.md](./create-squad.md)                       |
| Trabalho paralelo em features         | [auto-worktree.md](./auto-worktree.md)                     |

---

## Índice Completo

### Greenfield (Projetos Novos)

| Workflow              | Arquivo                   | Quando Usar                   |
| --------------------- | ------------------------- | ----------------------------- |
| Greenfield Full-Stack | `greenfield-fullstack.md` | App full-stack do zero        |
| Greenfield Service    | `greenfield-service.md`   | Backend/API do zero           |
| Greenfield UI         | `greenfield-ui.md`        | Frontend do zero + Stitch MCP |

### Brownfield (Projetos Existentes)

| Workflow              | Arquivo                   | Quando Usar                           |
| --------------------- | ------------------------- | ------------------------------------- |
| Brownfield Discovery  | `brownfield-discovery.md` | Primeiro mapeamento de projeto legado |
| Brownfield Full-Stack | `brownfield-fullstack.md` | Evolução full-stack existente         |
| Brownfield Service    | `brownfield-service.md`   | Evolução backend existente            |
| Brownfield UI         | `brownfield-ui.md`        | Evolução frontend existente           |

### Processos de Desenvolvimento

| Workflow                | Arquivo                      | Quando Usar                           |
| ----------------------- | ---------------------------- | ------------------------------------- |
| Spec Pipeline           | `spec-pipeline.md`           | Ideia → PRD → Épicos → Stories        |
| Epic Orchestration      | `epic-orchestration.md`      | Execução coordenada de épico completo |
| Story Development Cycle | `story-development-cycle.md` | Uma story — análise, dev, QA, commit  |
| QA Loop                 | `qa-loop.md`                 | Ciclo iterativo de correção QA        |

### Especiais

| Workflow            | Arquivo                  | Quando Usar                          |
| ------------------- | ------------------------ | ------------------------------------ |
| Design System Build | `design-system-build.md` | Criar/refatorar design system        |
| Create Squad        | `create-squad.md`        | Criar squad de mind clones           |
| Auto Worktree       | `auto-worktree.md`       | Desenvolvimento paralelo de features |

---

## Fluxo entre Workflows

```
Novo Projeto:
  greenfield-* → spec-pipeline → epic-orchestration → story-development-cycle → qa-loop

Projeto Existente:
  brownfield-discovery → brownfield-* → epic-orchestration → story-development-cycle → qa-loop

Processos Transversais:
  spec-pipeline   → Qualquer fluxo de desenvolvimento
  qa-loop         → Qualquer story com NEEDS_WORK
  design-system   → Greenfield UI ou Brownfield UI
  auto-worktree   → Qualquer workflow (paralelismo)
  create-squad    → Independente, qualquer momento
```

---

## Vantagens Exclusivas AntiGravity

Os seguintes workflows têm capacidades que **não existem no Claude Code**:

| Workflow              | Capacidade Exclusiva                                |
| --------------------- | --------------------------------------------------- |
| `greenfield-ui`       | `mcp_stitch_*` para gerar screens de design         |
| `brownfield-ui`       | `browser_subagent` para validação visual em browser |
| `design-system-build` | `mcp_stitch_*` + `generate_image` para design       |
| `auto-worktree`       | Adaptado sem limitações de hooks Python             |

---

_Documentação gerada durante a revisão de integração AntiGravity — 2026-02-26_
