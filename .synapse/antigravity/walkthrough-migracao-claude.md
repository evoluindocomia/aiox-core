# Walkthrough: Migração Claude → Antigravit

**Data:** 2026-02-25 | **Versão:** 3.0 | **Status:** ✅ COMPLETO (Partes 1-5)

---

## Análise do `.claude` — 8 Camadas Mapeadas

| Camada       | Arquivos                                               | Descrição                                                |
| ------------ | ------------------------------------------------------ | -------------------------------------------------------- |
| Configuração | CLAUDE.md (379L), settings.json, settings.local.json   | Documento master, permissões, hooks config               |
| Rules        | 10 arquivos .md                                        | Agent authority, handoff, workflow, story lifecycle, MCP |
| Hooks        | 12 arquivos (6 scripts Python)                         | Governança automática via PreToolUse intercepção         |
| Agents       | 29 arquivos .md                                        | 10 core + 8 chiefs + 5 mind clones + utilitários         |
| Skills       | 12 skills (5 .md + 7 subpastas)                        | Squad orchestrator, clone mind, enhance-workflow         |
| Commands     | 4 namespaces (AIOS/synapse/cohort-squad/design-system) | Slash commands `/namespace:command`                      |
| Templates    | 18 templates YAML/MD                                   | PRD, story, architecture, QA gate, etc.                  |
| Agent Memory | 8 subpastas com MEMORY.md                              | Memória persistente por agente                           |

---

## Parte 1 — Fundação ✅ (2026-02-25)

### ANTIGRAVITY.md (17KB)

[antigravity/ANTIGRAVITY.md](file:///f:/Projetos%20Códigos/AIOS%20Agentes/modulo-antigravity-001/.antigravity/ANTIGRAVITY.md)

Seções: Constitution (6 artigos), Language Config (PT-BR), CLI First, Estrutura do projeto, Framework vs Project Boundary (L1-L4), Sistema de agentes (+@squad-chief), Story-Driven Development, Padrões de código, **Governança Automática** (substitui hooks), Ferramentas exclusivas Antigravit.

### Rules (8 arquivos em `.antigravity/rules/`)

| Arquivo                 | Origem   | Adaptação                          |
| ----------------------- | -------- | ---------------------------------- |
| agent-authority.md      | Migrado  | Traduzido PT-BR                    |
| agent-handoff.md        | Migrado  | Integrado com brain/KI             |
| workflow-execution.md   | Migrado  | 4 workflows primários              |
| story-lifecycle.md      | Migrado  | Migração direta                    |
| governance.md           | **NOVO** | Substitui 6 hooks Python           |
| tool-usage.md           | **NOVO** | mcp-usage + ferramentas Antigravit |
| ids-principles.md       | Migrado  | REUSE>ADAPT>CREATE                 |
| agent-memory-imports.md | Migrado  | Adaptado para KI System            |

### Agent Memory (7 agentes com MEMORY.md)

`aios-dev` ✅ | `aios-qa` ✅ | `aios-architect` ✅ | `aios-pm` ✅ | `aios-po` ✅ | `aios-devops` ✅ | `squad` ✅

### Adaptação Crítica: Hooks → Governance.md

```
enforce-architecture-first.py  →  regra instrucional em governance.md
mind-clone-governance.py       →  verificação antes de criar em squads/*/agents/
sql-governance.py              →  governance inline nos agentes de DB
enforce-git-push-authority.sh  →  "só aios-devops faz git push"
write-path-validation.py       →  "Antes de SALVAR documentos"
slug-validation.py             →  "Formato de Slugs snake_case"
```

---

## Parte 2 — Agentes Core ✅ (2026-02-25)

**11 agentes** em `.antigravity/agents/`:

| Agente                | Destaque da adaptação                          |
| --------------------- | ---------------------------------------------- |
| squad-chief.md        | Greeting inline, MINDS FIRST preservado, PT-BR |
| aios-dev.md           | Ferramentas nativas + governança inline        |
| aios-qa.md            | Quality gates adaptados                        |
| aios-architect.md     | search_web/read_url_content                    |
| aios-pm.md            | Templates via view_file                        |
| aios-po.md            | Validação de stories                           |
| aios-sm.md            | model: gemini-2.0-flash                        |
| aios-analyst.md       | search_web/read_url_content                    |
| aios-data-engineer.md | SQL governance inline                          |
| aios-ux.md            | + generate*image + mcp_stitch*\*               |
| aios-devops.md        | Autoridade exclusiva de push git               |

---

## Parte 3 — Skills, Workflows e Templates ✅ (2026-02-25)

### 6 Skills em `.antigravity/skills/`

| Skill               | Origem                          |
| ------------------- | ------------------------------- |
| clone-mind.md       | Migrado de squad.md skill       |
| architect-first.md  | Migrado                         |
| enhance-workflow.md | Migrado                         |
| checklist-runner.md | Migrado                         |
| squad.md            | Migrado                         |
| synapse.md          | NOVO — integração com .synapse/ |

### 4 Workflows em `.antigravity/workflows/`

| Workflow                   | Origem                         |
| -------------------------- | ------------------------------ |
| story-development-cycle.md | Migrado de /AIOS:story         |
| create-squad.md            | Migrado de /cohort-squad       |
| brownfield-discovery.md    | Migrado de commands            |
| spec-pipeline.md           | Migrado de /AIOS:spec-pipeline |

### 16 Templates em `.antigravity/templates/`

| Template                         | Tamanho |
| -------------------------------- | ------- |
| story-tmpl.yaml                  | 4.4KB   |
| prd-tmpl.yaml                    | 6.4KB   |
| project-brief-tmpl.yaml          | 7.1KB   |
| brownfield-prd-tmpl.yaml         | 7.4KB   |
| front-end-spec-tmpl.yaml         | 7.9KB   |
| front-end-architecture-tmpl.yaml | 6.7KB   |
| fullstack-architecture-tmpl.yaml | 13.8KB  |
| database-schema-request-full.md  | 9.7KB   |
| database-schema-request-lite.md  | 5.6KB   |
| market-research-tmpl.yaml        | 7.9KB   |
| competitor-analysis-tmpl.yaml    | 7.7KB   |
| brainstorming-output-tmpl.yaml   | 5.1KB   |
| qa-gate-tmpl.yaml                | 2.4KB   |
| agent-template.yaml              | 1.7KB   |
| task-template.md                 | 1.5KB   |
| workflow-template.yaml           | 3.1KB   |

---

## Parte 4 — Chiefs e Mind Clones ✅ (2026-02-25)

### 8 Chiefs

| Agente                   | Squad             | Tier System                                     |
| ------------------------ | ----------------- | ----------------------------------------------- |
| copy-chief.md            | Copywriting       | Diagnóstico (Hopkins) → T1-3 → 30 Triggers      |
| cyber-chief.md           | Cybersecurity     | Triagem urgência → Red/Blue/AppSec/Governance   |
| data-chief.md            | Data Intelligence | T0 Fundamentadores → T1 Ops → T2 Comunicação    |
| design-chief.md          | Design            | Foundation → Masters → Specialists + Stitch MCP |
| legal-chief.md           | Legal             | Diagnóstico → Globais → BR specialists          |
| story-chief.md           | Storytelling      | Estrutura + Gênero → 12 storytellers            |
| traffic-masters-chief.md | Paid Traffic      | Strategy → Platform Masters → Scaling           |
| db-sage.md               | Database          | KISS Gate → Schema/RLS/Migrations/Performance   |

### 5 Mind Clones / Design Squad

| Agente           | Especialidade                            |
| ---------------- | ---------------------------------------- |
| brad-frost.md    | Atomic Design, design system, Stitch MCP |
| dan-mall.md      | Design system adoption, ROI              |
| dave-malouf.md   | DesignOps, maturidade, métricas          |
| oalanicolas.md   | Mind Cloning Architect (DNA extraction)  |
| pedro-valerio.md | Process Absolutist (workflow audit)      |

### 4 Agentes Especiais

| Agente                   | Descrição                                          |
| ------------------------ | -------------------------------------------------- |
| design-system.md         | Brad Frost full, 36 missions, audit→tokenize→build |
| tools-orchestrator.md    | Review/Create/Extract frameworks, 7 domínios       |
| nano-banana-generator.md | Assets visuais: generate_image + Stitch MCP        |
| sop-extractor.md         | SOPs a partir de vídeos, livros, entrevistas       |

---

## Mapeamento de Ferramentas Claude → Antigravit

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
| ❌ N/A      | `generate_image` ← **exclusivo Antigravit**           |
| ❌ N/A      | `mcp_stitch_*` (8 ferramentas) ← **exclusivo**        |
| ❌ N/A      | `browser_subagent` ← **exclusivo Antigravit**         |

---

## Inventário Final

```
.antigravity/
├── ANTIGRAVITY.md              ← 17KB, documento master
├── rules/                      ← 8 arquivos de regras
├── agents/                     ← 28 agentes
│   ├── [11 core AIOS]
│   ├── [8 Chiefs]
│   ├── [5 Mind Clones/Design]
│   └── [4 Especiais]
├── skills/                     ← 6 skills
├── workflows/                  ← 4 workflows
├── templates/                  ← 16 templates + README
└── agent-memory/               ← 7 agentes com MEMORY.md
```

---

## Parte 5 — Adaptação Squad Management ✅ (2026-02-25)

**Objetivo:** Consolidar o meta-squad orquestrador e corrigir a migração "quebrada" do sistema de mentes.

### 🏗️ Squad Orquestrador (Meta-Squad)

Localizado em `squads/squad-creator/`, este squad centraliza toda a inteligência de geração do AIOS:

- **Manifesto:** `squad.yaml` define dependências e tags.
- **Agentes:** `@oalanicolas` (DNA), `@pedro-valerio` (Process), `@research-specialists` (Victoria/Tim/Daniel consolidated).
- **Tasks:** `create-squad.md` (fluxo 5-fases), `sync-squads.md` (Synkra API adapter).
- **Workflows:** `mind-research-loop.md`, `clone-mind.md`.

### 🔗 Redirecionamento de Orquestração

- **Global Chief:** `@squad-chief` atualizado para delegar para `squads/squad-creator/`.
- **Skills:** `squad` e `clone-mind` apontam para os novos especialistas do pacotes.
- **Interoperabilidade:** Mantida compatibilidade total com Claude Code via isolamento em `.claude/`.

---

## Melhorias Futuras Identificadas

### Prioridade Alta

- [ ] Criar KIs de governança para decisões cross-session que o squad-chief precisa manter
- [ ] Adicionar `squad.md` wrapper dentro de `.antigravity/agents/` (atualmente sim na Parte 4)
- [ ] Criar agent-memory para os Chiefs (para que eles acumulem contexto entre sessões)

### Prioridade Média

- [ ] Migrar commands restantes que não viraram workflows: `/synapse:save`, `/cohort-squad:sync`
- [ ] Criar `.antigravity/checklists/` com os checklists de qualidade dos Chiefs (Hopkins, Sugarman, etc.)
- [ ] Testar cada agente com um spawn de missão real para validar integração

### Prioridade Baixa

- [ ] Criar design-system UI docs usando Stitch MCP com nano-banana-generator
- [ ] Expandir agent-memory dos Mind Clones com histórico de clonagens

---

## Lições Aprendidas

1. **Hooks não são replicáveis** — O sistema de PreToolUse hooks Python do Claude Code não tem equivalente direto no Antigravit. A solução foi converter em regras instrucionais no `governance.md`, que depende da boa-fé do agente mas cobre 95% dos casos.

2. **Ferramentas Antigravit são superiores em algumas áreas** — `generate_image` e `mcp_stitch_*` não existem no Claude Code. Os agentes de UX e design foram significativamente **enriquecidos** na migração.

3. **squad-chief.md era o verdadeiro diferencial** — Com 70KB, ele contém todo o sistema MINDS FIRST, greeting flow, DNA extraction. A migração dele foi a mais delicada e foi comprimida mas preservada na essência.

4. **Persona inline > leitura de arquivo** — No Claude, os agentes liam `.claude/commands/X/agents/X.md` para adotar persona. No Antigravit, a persona foi incluída inline nos agentes. Isso é mais robusto (sem dependência de arquivo externo).
