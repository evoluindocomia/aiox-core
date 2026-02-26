# Rules — Sistema de Regras de Comportamento

As **8 rules** em `.antigravity/rules/` definem como os agentes se comportam. São carregadas automaticamente ou por contexto (via `paths:` frontmatter).

> **Atualizado:** 2026-02-26 — `workflow-execution.md` cobre agora todos os **14 workflows**.

---

## O que são Rules no Antigravit?

Rules são arquivos `.md` que o Antigravit injeta no contexto dos agentes. Diferente do Claude Code (onde eram todas sempre carregadas), no Antigravit as rules podem ser **condicionais por path** — elas só se tornam ativas quando o agente está trabalhando em arquivos relacionados.

---

## Tabela de Rules

| Arquivo                   | Tipo     | Descrição                                                   |
| ------------------------- | -------- | ----------------------------------------------------------- |
| `agent-authority.md`      | Migrado  | Hierarquia de autoridade, Framework/Project Boundary L1-L4  |
| `agent-handoff.md`        | Migrado  | Protocolo de handoff entre agentes, integrado com KI System |
| `agent-memory-imports.md` | Migrado  | Quando e como carregar MEMORY.md, KI summaries              |
| `governance.md`           | **NOVO** | Substitui 6 hooks Python do Claude — checklist pré-operação |
| `ids-principles.md`       | Migrado  | IDS: REUSE > ADAPT > CREATE                                 |
| `story-lifecycle.md`      | Migrado  | Ciclo de vida das stories                                   |
| `tool-usage.md`           | **NOVO** | Regras de uso de ferramentas + MCP                          |
| `workflow-execution.md`   | Migrado  | 14 workflows completos + guia de seleção                    |

---

## Regras Críticas por Categoria

### 🏛️ Agent Authority (`agent-authority.md`)

Define **quem pode fazer o quê** e a hierarquia de autoridade entre agentes.

**Framework vs Project Boundary:**

| Camada       | Path                                    | Regra                 |
| ------------ | --------------------------------------- | --------------------- |
| L1 Core      | `.aios-core/core/`, `bin/aios.js`       | NUNCA modificar       |
| L2 Templates | `.aios-core/development/`               | NUNCA modificar       |
| L3 Config    | `.aios-core/data/`, `MEMORY.md`         | Modificar com cuidado |
| L4 Runtime   | `docs/stories/`, `packages/`, `squads/` | Sempre pode modificar |

**Autoridade exclusiva:** Apenas `@devops` executa `git push`.

---

### 🔄 Agent Handoff (`agent-handoff.md`)

Protocolo formal de passagem de contexto entre agentes.

**Formato de handoff:**

```
→ @{agent-id} — {razão}
Contexto: {resumo do estado atual}
Próximo passo: {o que deve ser feito}
Artifacts: {links para KIs ou artefatos relevantes}
```

**Integração com KI System:** Ao fazer handoff, o agente criador documenta decisões críticas em Knowledge Items para recuperação em sessões futuras.

---

### 🧠 Agent Memory Imports (`agent-memory-imports.md`)

Define quando e como carregar a memória persistente.

**Prioridade de carregamento:**

1. KI Summaries (resumos do Knowledge System)
2. Conversation logs relevantes
3. `MEMORY.md` do agente específico

**Regra:** Sempre verificar KI summaries **antes** de qualquer pesquisa. Evita trabalho duplicado entre sessões.

---

### 🛡️ Governance (`governance.md`)

> Este é o arquivo mais crítico de operação. Ver documentação completa: [Governance](./governance.md)

Substitui os **6 hooks Python** do Claude Code por um sistema instrucional de verificações obrigatórias.

---

### ♻️ IDS Principles (`ids-principles.md`)

**Incremental Development Strategy:** REUSE > ADAPT > CREATE

```
1. REUSE   → Existe algo que resolve isso no codebase?
2. ADAPT   → Posso adaptar algo existente?
3. CREATE  → Só então criar do zero
```

Esta regra força os agentes a consultarem o codebase antes de criar qualquer nova estrutura.

---

### 📖 Story Lifecycle (`story-lifecycle.md`)

Define o ciclo de vida completo de uma story:

```
draft → validated → in_progress → review → done → archived
```

**Estados e responsáveis:**

- `draft` — `@sm` ou `@po`
- `validated` — `@po` (critérios de aceitação definidos)
- `in_progress` — `@dev`
- `review` — `@qa`
- `done` — `@devops` (após push)
- `archived` — mover para `docs/stories/completed/`

---

### 🔧 Tool Usage (`tool-usage.md`)

Prioridade de uso de ferramentas:

| Tarefa          | Ferramenta Preferida                                  | Evitar            |
| --------------- | ----------------------------------------------------- | ----------------- |
| Ler arquivo     | `view_file`                                           | MCP equivalentes  |
| Editar arquivo  | `replace_file_content` / `multi_replace_file_content` | Bash alternatives |
| Criar arquivo   | `write_to_file`                                       | —                 |
| Buscar conteúdo | `grep_search`                                         | —                 |
| Buscar arquivos | `find_by_name`                                        | —                 |
| Comandos shell  | `run_command`                                         | —                 |
| Browser         | `browser_subagent`                                    | —                 |
| Gerar imagens   | `generate_image`                                      | —                 |

**MCP disponíveis:**

- `stitch` — 8 ferramentas de design de UI

---

### 🔄 Workflow Execution (`workflow-execution.md`)

Os 14 workflows e quando acioná-los — agora com guia de seleção completo:

| Categoria              | Workflows                                                                             |
| ---------------------- | ------------------------------------------------------------------------------------- |
| Greenfield (Novo)      | `greenfield-fullstack`, `greenfield-service`, `greenfield-ui`                         |
| Brownfield (Existente) | `brownfield-discovery`, `brownfield-fullstack`, `brownfield-service`, `brownfield-ui` |
| Desenvolvimento        | `story-development-cycle`, `spec-pipeline`, `epic-orchestration`, `qa-loop`           |
| Especiais              | `design-system-build`, `create-squad`, `auto-worktree`                                |

> Índice de seleção: [`.antigravity/workflows/README.md`](../../../../.antigravity/workflows/README.md)

---

## Como as Rules São Carregadas

No Antigravit, o sistema de rules funciona assim:

1. **Rules globais** — Sempre carregadas (sem `paths:` no frontmatter)
2. **Rules condicionais** — Carregadas apenas quando trabalhando em paths específicos
3. **ANTIGRAVITY.md** — Sempre carregado como documento master

```yaml
# Exemplo de rule com paths (carregamento condicional)
---
paths:
  - 'supabase/**'
  - 'packages/db/**'
---
```

> **Nota:** Regras condicionais por path otimizam o uso de contexto — o agente só carrega regras relevantes para o que está fazendo.

---

## Documentação Relacionada

- [Governance (detalhado)](./governance.md)
- [Mapeamento de Ferramentas](../tools/tool-mapping.md)
- [Workflows](../workflows/overview.md)
