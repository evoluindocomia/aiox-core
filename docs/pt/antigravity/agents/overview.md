# Sistema de Agentes — Visão Geral

O Antigravit possui **28 agentes** organizados em 4 categorias, todos residentes em `.antigravity/agents/`.

---

## Categorias de Agentes

| Categoria                        | Quantidade | Descrição                                            |
| -------------------------------- | ---------- | ---------------------------------------------------- |
| [Core AIOS](./core-agents.md)    | 11         | Agentes fundamentais do ciclo de desenvolvimento     |
| [Chiefs](./chiefs.md)            | 8          | Orquestradores especializados por domínio de negócio |
| [Mind Clones](./mind-clones.md)  | 5          | Clones de mentes reais (Design Squad)                |
| [Especiais](./special-agents.md) | 4          | Agentes com capacidades únicas                       |

---

## Ativação de Agentes

```
@{agent-id}  → ativa o agente
```

O agente lê seu próprio arquivo `.antigravity/agents/{id}.md`, adota a persona definida e exibe um greeting inline.

**Importante:** A persona fica **inline no arquivo do agente** — não há dependências externas. Isso torna a ativação mais robusta que no Claude Code.

---

## Hierarquia e Autoridade

O AIOS define uma hierarquia clara de autoridade via `.antigravity/rules/agent-authority.md`:

```
Constitution (L1)
  └── Framework Rules (L2)
        └── Agent Authority (L3)
              └── Task Scope (L4)
```

Cada agente tem escopo definido. Respeitar os limites de escopo é **obrigatório**.

### Regra de Ouro

> **Apenas `@devops` (Gage) pode executar `git push` para remote.**  
> Todos os outros agentes devem delegar via `→ @devops *push`.

---

## Mapeamento Agente → Codebase

| Agente           | Diretórios Principais                   |
| ---------------- | --------------------------------------- |
| `@dev`           | `packages/`, `.aios-core/core/`, `bin/` |
| `@architect`     | `docs/architecture/`, design de sistema |
| `@data-engineer` | `packages/db/`, migrations, schema      |
| `@qa`            | `tests/`, `*.test.js`, quality gates    |
| `@po`            | Stories, epics, requirements            |
| `@devops`        | `.github/`, CI/CD, git operations       |
| `@ux`            | UI/UX, mockups, design system           |
| `@brad-frost`    | Design System, Atomic Design            |
| `@squad-chief`   | `squads/`, criação de agentes           |

---

## Sistema de Comandos (`*`)

Dentro de qualquer agente ativo, use o prefixo `*`:

| Comando Universal | Descrição                     |
| ----------------- | ----------------------------- |
| `*help`           | Lista comandos do agente      |
| `*create-story`   | Cria story de desenvolvimento |
| `*task {nome}`    | Executa task específica       |
| `*exit`           | Sai do modo agente            |

Cada agente pode ter comandos específicos adicionais listados em seu arquivo de definição.

---

## Agent Memory

Cada agente possui memória persistente em `.antigravity/agent-memory/{id}/MEMORY.md`.

**Agentes com memória:**

| Agente           | Arquivo de Memória                                   |
| ---------------- | ---------------------------------------------------- |
| `aios-dev`       | `.antigravity/agent-memory/aios-dev/MEMORY.md`       |
| `aios-qa`        | `.antigravity/agent-memory/aios-qa/MEMORY.md`        |
| `aios-architect` | `.antigravity/agent-memory/aios-architect/MEMORY.md` |
| `aios-pm`        | `.antigravity/agent-memory/aios-pm/MEMORY.md`        |
| `aios-po`        | `.antigravity/agent-memory/aios-po/MEMORY.md`        |
| `aios-devops`    | `.antigravity/agent-memory/aios-devops/MEMORY.md`    |
| `squad`          | `.antigravity/agent-memory/squad/MEMORY.md`          |

A memória é lida pelo agente no início de cada sessão, conforme as regras em `.antigravity/rules/agent-memory-imports.md`.

---

## Handoffs entre Agentes

Quando um agente precisa delegar para outro, usa o formato de handoff definido em `.antigravity/rules/agent-handoff.md`:

```
→ @{agent-id} — {razão do handoff}
Contexto: {resumo do que foi feito}
Próximo passo: {o que precisa ser feito}
```

**Exemplo:**

```
→ @devops — implementação concluída, quality gates passando
Contexto: Feature X implementada na branch feat/feature-x
Próximo passo: Push para remote e criar PR
```

---

## Knowledge Items (KI System)

O Antigravit usa o **KI System** para memória cross-session estruturada:

- KIs ficam em `C:\Users\Administrador\.gemini\antigravity\knowledge\`
- Cada KI contém `metadata.json` e `artifacts/`
- **Sempre verificar KI summaries** antes de pesquisar — evita trabalho duplicado
- Criar KIs após cada squad criado ou decisão arquitetural importante

> Regra: `.antigravity/rules/agent-memory-imports.md`

---

## Framework vs Project Boundary (L1-L4)

Os agentes operam dentro de um modelo de 4 camadas que define o que pode ser modificado:

| Camada                     | Mutabilidade            | Exemplos                                |
| -------------------------- | ----------------------- | --------------------------------------- |
| **L1** Framework Core      | NUNCA modificar         | `.aios-core/core/`, `bin/aios.js`       |
| **L2** Framework Templates | NUNCA modificar         | `.aios-core/development/`               |
| **L3** Project Config      | Permitido (com cuidado) | `.aios-core/data/`, `MEMORY.md`         |
| **L4** Project Runtime     | SEMPRE pode modificar   | `docs/stories/`, `packages/`, `squads/` |

> Regra formal: `.antigravity/rules/agent-authority.md`

---

## Subagentes do Squad-Chief

O `@squad-chief` orquestra dois subagentes especializados:

| Subagente       | Trigger de ativação                            | Localização                                           |
| --------------- | ---------------------------------------------- | ----------------------------------------------------- |
| `oalanicolas`   | Clonagem de mente, extração de DNA, fidelidade | `squads/squad-creator/agents/oalanicolas.md`          |
| `pedro-valerio` | Design de workflow, validação de processo      | `squads/squad-creator/agents/pedro-valerio.md`        |
| `research-...`  | Deep research e frameworks                     | `squads/squad-creator/agents/research-specialists.md` |

---

## Handoffs entre Workflows

Além do handoff entre agentes, os workflows se encadeiam naturalmente. Ao concluir um workflow, o agente notifica qual workflow pode ser o próximo:

| Workflow Concluído        | Próximo Sugerido                  |
| ------------------------- | --------------------------------- |
| `brownfield-discovery`    | `brownfield-fullstack/service/ui` |
| `spec-pipeline`           | `epic-orchestration`              |
| `epic-orchestration`      | `story-development-cycle`         |
| `story-development-cycle` | `qa-loop` (se QA reprovar)        |
| `greenfield-ui`           | `design-system-build`             |

> Ver detalhes: [`.antigravity/rules/agent-handoff.md`](../../../../.antigravity/rules/agent-handoff.md)

---

## Documentação Relacionada

- [Agentes Core](./core-agents.md)
- [Chiefs](./chiefs.md)
- [Mind Clones](./mind-clones.md)
- [Agentes Especiais](./special-agents.md)
- [Rules: Agent Authority](../rules/overview.md)
- [Rules: Agent Handoff](../rules/overview.md)
- [Rules: Agent Memory](../rules/overview.md)
