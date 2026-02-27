# Migração do Claude para o Antigravit

Guia técnico sobre o que foi migrado, o que mudou e o que é exclusivo do Antigravit.

> **Migração realizada em:** 2026-02-25  
> **Status:** ✅ COMPLETO (Partes 1-5)  
> **Walkthrough completo:** `.synapse/antigravity/walkthrough-migracao-claude.md`

---

## O que foi Migrado

O `.claude/` possuía **8 camadas** que foram mapeadas e migradas para o `.antigravity/`:

| Camada Claude | Arquivos                            | Destino Antigravit                       |
| ------------- | ----------------------------------- | ---------------------------------------- |
| Configuração  | `CLAUDE.md` (379L), `settings.json` | `ANTIGRAVITY.md` (17KB)                  |
| Rules         | 10 arquivos `.md`                   | `.antigravity/rules/` (8 arquivos)       |
| Hooks         | 12 arquivos (6 scripts Python)      | `governance.md` (instrucional)           |
| Agents        | 29 arquivos `.md`                   | `.antigravity/agents/` (28 arquivos)     |
| Skills        | 12 skills + subpastas               | `.antigravity/skills/` (6 skills)        |
| Commands      | 4 namespaces de slash commands      | `.antigravity/workflows/` (14 workflows) |
| Templates     | 18 templates YAML/MD                | `.antigravity/templates/` (16 templates) |
| Agent Memory  | 8 subpastas com `MEMORY.md`         | `.antigravity/agent-memory/` (7 agentes) |

---

## Mudanças Críticas

### 1. Hooks → Governance.md (maior diferença)

**No Claude Code:**

```
PreToolUse hooks bloqueavam automaticamente operações via exit codes:
  exit 0 = permitido
  exit 2 = bloqueado (ferramenta não executava)
```

**No Antigravit:**

```
Não existe sistema de interceptação automática de ferramentas.
Governance.md define as mesmas regras como checklist instrucional
que o agente deve verificar proativamente antes de cada operação.
```

**Cobertura:** ~95% dos casos cobertos. Depende da "boa-fé" do agente (sem automação de bloqueio).

| Hook Python Original            | Equivalente em governance.md                          |
| ------------------------------- | ----------------------------------------------------- |
| `enforce-architecture-first.py` | Seção 🔴 "Antes de ESCREVER em paths protegidos"      |
| `mind-clone-governance.py`      | Seção 🔴 "Antes de CRIAR agente em squads/\*/agents/" |
| `sql-governance.py`             | Seção 🔴 "Antes de EXECUTAR SQL DDL"                  |
| `enforce-git-push-authority.sh` | Seção 🔴 "Antes de GIT PUSH"                          |
| `write-path-validation.py`      | Seção 🟡 "Antes de SALVAR documentos"                 |
| `slug-validation.py`            | Seção 🟡 "Formato de Slugs"                           |

---

### 2. Persona Inline > Leitura de Arquivo Externo

**No Claude Code:**

```
Ao ativar @dev, o agente lia .claude/commands/AIOS/agents/dev.md
para adotar a persona (dependência externa)
```

**No Antigravit:**

```
A persona está INLINE no próprio arquivo .antigravity/agents/aios-dev.md
Sem dependência de arquivo externo → mais robusto e portátil
```

---

### 3. Slash Commands → Workflows

O Antigravity agora possui **paridade total** com os slash commands do Claude Code, além de workflows adicionais com capacidades exclusivas:

| Slash Command Claude   | Workflow Antigravity          | Status         |
| ---------------------- | ----------------------------- | -------------- |
| `/AIOS:story`          | `story-development-cycle.md`  | ✅ Migrado     |
| `/AIOS:spec-pipeline`  | `spec-pipeline.md`            | ✅ Migrado     |
| `/cohort-squad:create` | `create-squad.md` (via packs) | ✅ Migrado     |
| `/cohort-squad:sync`   | `sync-squads.md` (via packs)  | ✅ Migrado     |
| Analysis commands      | `brownfield-discovery.md`     | ✅ Migrado     |
| _(não existia)_        | `greenfield-fullstack.md`     | ✅ **NOVO**    |
| _(não existia)_        | `greenfield-service.md`       | ✅ **NOVO**    |
| _(não existia)_        | `greenfield-ui.md`            | ✅ **NOVO** ⭐ |
| _(não existia)_        | `brownfield-fullstack.md`     | ✅ **NOVO**    |
| _(não existia)_        | `brownfield-service.md`       | ✅ **NOVO**    |
| _(não existia)_        | `brownfield-ui.md`            | ✅ **NOVO**    |
| _(não existia)_        | `epic-orchestration.md`       | ✅ **NOVO**    |
| _(não existia)_        | `qa-loop.md`                  | ✅ **NOVO**    |
| _(não existia)_        | `design-system-build.md`      | ✅ **NOVO** ⭐ |
| _(não existia)_        | `auto-worktree.md`            | ✅ **NOVO**    |

> ⭐ Workflows com capacidades exclusivas Antigravity (Stitch MCP, browser_subagent, generate_image)

---

### 4. Skills: de 12 para 6 (consolidação)

O `.claude/` tinha 12 skills. O Antigravit consolidou para 6, mais a adição da skill `synapse` (nova):

| Claude Skill       | Status Antigravit                    |
| ------------------ | ------------------------------------ |
| `clone-mind`       | ✅ Migrado                           |
| `architect-first`  | ✅ Migrado                           |
| `enhance-workflow` | ✅ Migrado                           |
| `checklist-runner` | ✅ Migrado                           |
| `squad`            | ✅ Migrado                           |
| `synapse`          | ✅ **NOVO** — integração `.synapse/` |
| Outras 6 skills    | Consolidadas nas 5 acima             |

---

## O que NÃO Existe no Antigravit (Limitações)

| Recurso Claude                       | Status Antigravit | Workaround                                 |
| ------------------------------------ | ----------------- | ------------------------------------------ |
| PreToolUse Hooks automáticos         | ❌ N/A            | `governance.md` instrucional               |
| `/synapse:save` command              | ❌ N/A            | Salvar manualmente em `.synapse/sessions/` |
| `/cohort-squad:sync` command         | ❌ N/A            | Sync manual via `@devops`                  |
| Checklists de Chiefs (Hopkins, etc.) | ⚠️ Não criados    | Prioridade média (ver melhorias futuras)   |
| Agent Memory para Chiefs             | ⚠️ Não criados    | Prioridade alta (ver melhorias futuras)    |

---

## O que Melhorou no Antigravit (Vantagens)

| Capacidade                        | Claude Code       | Antigravit                           |
| --------------------------------- | ----------------- | ------------------------------------ |
| Geração de imagens                | ❌                | ✅ `generate_image`                  |
| Design de UI interativo           | ❌                | ✅ `mcp_stitch_*` (8 ferramentas)    |
| Gravação de sessão de browser     | ❌                | ✅ `browser_subagent` com vídeo WebP |
| Memória cross-session estruturada | MEMORY.md simples | ✅ KI System completo                |
| Comunicação de progresso          | ❌                | ✅ `task_boundary` + `notify_user`   |
| Agentes de UX/Design              | Básico            | Significativamente enriquecidos      |

---

## Mapeamento de Ferramentas

| Claude Tool | Antigravit Tool                                       |
| ----------- | ----------------------------------------------------- |
| `Read`      | `view_file`                                           |
| `Write`     | `write_to_file`                                       |
| `Edit`      | `replace_file_content` / `multi_replace_file_content` |
| `Grep`      | `grep_search`                                         |
| `Glob`      | `find_by_name`                                        |
| `WebSearch` | `search_web`                                          |
| `WebFetch`  | `read_url_content`                                    |
| `Bash`      | `run_command`                                         |
| `Task`      | `browser_subagent` (casos compatíveis)                |

---

## Melhorias Futuras Planejadas

### Prioridade Alta

- [x] Integração completa de 14 workflows em `.antigravity/workflows/` ✅ (2026-02-26)
- [x] Atualização de `ANTIGRAVITY.md` com guia de seleção ✅
- [ ] Criar `agent-memory/` para os Chiefs

### Prioridade Média

- [x] Workflows `greenfield-*` e `brownfield-*` com capacidades Stitch MCP ✅
- [ ] Atualizar `npx aios-core init` para copiar `.antigravity/` junto com `.claude/`
- [ ] Adicionar `gemini` como `ai.provider` na configuração

### Prioridade Baixa

- [ ] Design system UI docs usando Stitch MCP com `@nano-banana-generator`
- [ ] Expandir agent-memory dos Mind Clones com histórico de clonagens
- [ ] KI de Governança de Workflows (adiado — ver decisão em `.synapse/antigravity/revWorkFlows/task.md`)

---

## Lições Aprendidas

1. **Hooks não são replicáveis** — A solução instrucional cobre 95% dos casos mas depende do comportamento do agente.

2. **Ferramentas Antigravit são superiores em algumas áreas** — `generate_image` e `mcp_stitch_*` não existem no Claude Code. Os agentes de UX e design foram _significativamente enriquecidos_ na migração.

3. **`squad-chief.md` era o verdadeiro diferencial** — Com 70KB no Claude e 16KB na versão comprimida do Antigravit, o sistema MINDS FIRST foi preservado na essência.

4. **Persona inline > leitura de arquivo** — A desacoplação das personas de arquivos externos tornou o sistema mais robusto.

---

## Referências

| Documento                        | Path                                                  |
| -------------------------------- | ----------------------------------------------------- |
| Walkthrough completo da migração | `.synapse/antigravity/walkthrough-migracao-claude.md` |
| Documento master Antigravit      | `.antigravity/ANTIGRAVITY.md`                         |
| Governance (substitui hooks)     | `.antigravity/rules/governance.md`                    |
| Tool mapping (esta doc)          | `docs/pt/antigravity/tools/tool-mapping.md`           |
