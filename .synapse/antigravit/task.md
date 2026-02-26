# Task: Análise e Migração Claude → Antigravit

## Parte 1: Análise do .claude ✅

- [x] Mapear estrutura de diretórios do .claude
- [x] Ler CLAUDE.md (constitution, agentes, CLI First)
- [x] Analisar .claude/rules/ (10 arquivos)
- [x] Analisar .claude/hooks/ (12 arquivos, 6 scripts Python de governança)
- [x] Analisar .claude/agents/ (29 agentes, foco em squad-chief)
- [x] Analisar .claude/skills/ (squad.md, oalanicolas, pedro-valerio, etc.)
- [x] Analisar .claude/commands/ (greet, AIOS, synapse, cohort-squad, design-system)
- [x] Analisar .claude/templates/ (18 templates YAML/MD)
- [x] Analisar .claude/settings e settings.local.json

## Parte 2: Análise do .antigravity ✅

- [x] Mapear estrutura atual do .antigravity (apenas rules/ vazia)
- [x] Verificar regras existentes em .antigravity/rules/

## Parte 3: PRD Completo ✅

- [x] Criar PRD completo (prd-migracao-claude-antigravit.md)
  - [x] Resumo executivo e objetivos
  - [x] Inventário completo de funcionalidades do .claude
  - [x] Análise de replicabilidade por funcionalidade
  - [x] Guia passo-a-passo por funcionalidade
  - [x] Funcionalidades impossíveis de replicar
  - [x] Roadmap de implementação dividido em partes

## Parte 4 — Implementação Parte 1: Fundação ✅

- [x] Criar ANTIGRAVITY.md (equivalente ao CLAUDE.md) — 17KB
- [x] Criar .antigravity/rules/agent-authority.md
- [x] Criar .antigravity/rules/agent-handoff.md
- [x] Criar .antigravity/rules/workflow-execution.md
- [x] Criar .antigravity/rules/story-lifecycle.md
- [x] Criar .antigravity/rules/governance.md (NOVO — substitui 6 hooks Python)
- [x] Criar .antigravity/rules/tool-usage.md (NOVO — Antigravit + MCP)
- [x] Criar .antigravity/rules/ids-principles.md
- [x] Criar .antigravity/rules/agent-memory-imports.md
- [x] Criar .antigravity/agent-memory/aios-dev/MEMORY.md
- [x] Criar .antigravity/agent-memory/aios-qa/MEMORY.md
- [x] Criar .antigravity/agent-memory/aios-architect/MEMORY.md
- [x] Criar .antigravity/agent-memory/aios-pm/MEMORY.md
- [x] Criar .antigravity/agent-memory/aios-po/MEMORY.md
- [x] Criar .antigravity/agent-memory/aios-devops/MEMORY.md
- [x] Criar .antigravity/agent-memory/squad/MEMORY.md
- [x] Salvar walkthrough em .synapse/antigravit/walkthrough-migracao-claude.md

## Parte 4 — Implementação Parte 2: Agentes Core ✅

- [x] Criar .antigravity/agents/
- [x] Migrar aios-dev.md → .antigravity/agents/ (ferramentas nativas + governança inline)
- [x] Migrar aios-qa.md → .antigravity/agents/ (adaptado)
- [x] Migrar aios-architect.md → .antigravity/agents/ (search_web/read_url_content)
- [x] Migrar aios-pm.md → .antigravity/agents/ (adaptado)
- [x] Migrar aios-po.md → .antigravity/agents/ (adaptado)
- [x] Migrar aios-sm.md → .antigravity/agents/ (model: flash)
- [x] Migrar aios-analyst.md → .antigravity/agents/ (search_web/read_url_content)
- [x] Migrar aios-data-engineer.md → .antigravity/agents/ (SQL governance inline)
- [x] Migrar aios-ux.md → .antigravity/agents/ (+ generate*image + mcp_stitch*\*)
- [x] Migrar aios-devops.md → .antigravity/agents/ (autoridade exclusiva de push)
- [x] Migrar squad-chief.md → .antigravity/agents/ (greeting inline, PT-BR, MINDS FIRST preservado)

## Parte 4 — Implementação Parte 3: Skills, Workflows e Templates ✅

- [x] Criar .antigravity/skills/ (6 skills: clone-mind, architect-first, enhance-workflow, checklist-runner, squad, synapse)
- [x] Criar .antigravity/workflows/ (4 workflows: story-development-cycle, create-squad, brownfield-discovery, spec-pipeline)
- [x] Criar .antigravity/templates/ (16 templates + README: todos os 18 originais migrados e adaptados para PT-BR)

## Parte 4 — Implementação Parte 4: Chiefs e Mind Clones ✅

- [x] Migrar 8 Chiefs → .antigravity/agents/ (copy-chief, cyber-chief, data-chief, design-chief, legal-chief, story-chief, traffic-masters-chief, db-sage)
- [x] Migrar 5 Mind Clones/Design Squad → .antigravity/agents/ (brad-frost, dan-mall, dave-malouf, oalanicolas, pedro-valerio)
- [x] Migrar agentes especiais → .antigravity/agents/ (design-system, tools-orchestrator, nano-banana-generator, sop-extractor)
- [x] Total: 28 agentes em .antigravity/agents/ (11 AIOS core + 17 Chiefs/Mind Clones/Especiais)

