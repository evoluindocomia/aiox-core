# Task: Documentação Completa do .antigravity/

## Planejamento

- [x] Ler walkthrough-migracao-claude.md
- [x] Explorar estrutura .antigravity/ (agentes, rules, skills, workflows, templates)
- [x] Explorar estrutura docs/ existente
- [x] Criar implementation_plan.md
- [x] Criar task.md

## Arquivos de Documentação — docs/pt

### Seção Principal

- [ ] [docs/pt/antigravity/index.md](file:///f:/Projetos%20C%C3%B3digos/AIOS%20Agentes/modulo-antigravity-001/docs/pt/antigravity/index.md) — Visão geral do ambiente Antigravit
- [ ] [docs/pt/antigravity/getting-started.md](file:///f:/Projetos%20C%C3%B3digos/AIOS%20Agentes/modulo-antigravity-001/docs/pt/antigravity/getting-started.md) — Como começar com o Antigravit

### Agentes

- [ ] [docs/pt/antigravity/agents/overview.md](file:///f:/Projetos%20C%C3%B3digos/AIOS%20Agentes/modulo-antigravity-001/docs/pt/antigravity/agents/overview.md) — Visão geral do sistema de agentes
- [ ] [docs/pt/antigravity/agents/core-agents.md](file:///f:/Projetos%20C%C3%B3digos/AIOS%20Agentes/modulo-antigravity-001/docs/pt/antigravity/agents/core-agents.md) — 11 agentes core AIOS
- [ ] [docs/pt/antigravity/agents/chiefs.md](file:///f:/Projetos%20C%C3%B3digos/AIOS%20Agentes/modulo-antigravity-001/docs/pt/antigravity/agents/chiefs.md) — 8 Chiefs e suas especialidades
- [ ] [docs/pt/antigravity/agents/mind-clones.md](file:///f:/Projetos%20C%C3%B3digos/AIOS%20Agentes/modulo-antigravity-001/docs/pt/antigravity/agents/mind-clones.md) — 5 Mind Clones / Design Squad
- [ ] [docs/pt/antigravity/agents/special-agents.md](file:///f:/Projetos%20C%C3%B3digos/AIOS%20Agentes/modulo-antigravity-001/docs/pt/antigravity/agents/special-agents.md) — 4 Agentes especiais

### Rules

- [ ] [docs/pt/antigravity/rules/overview.md](file:///f:/Projetos%20C%C3%B3digos/AIOS%20Agentes/modulo-antigravity-001/docs/pt/antigravity/rules/overview.md) — Sistema de rules e como funciona
- [ ] [docs/pt/antigravity/rules/governance.md](file:///f:/Projetos%20C%C3%B3digos/AIOS%20Agentes/modulo-antigravity-001/docs/pt/antigravity/rules/governance.md) — Governança automática (substituto de hooks)

### Skills

- [ ] [docs/pt/antigravity/skills/overview.md](file:///f:/Projetos%20C%C3%B3digos/AIOS%20Agentes/modulo-antigravity-001/docs/pt/antigravity/skills/overview.md) — Sistema de skills

### Workflows

- [ ] [docs/pt/antigravity/workflows/overview.md](file:///f:/Projetos%20C%C3%B3digos/AIOS%20Agentes/modulo-antigravity-001/docs/pt/antigravity/workflows/overview.md) — 4 workflows nativos

### Templates

- [ ] [docs/pt/antigravity/templates/overview.md](file:///f:/Projetos%20C%C3%B3digos/AIOS%20Agentes/modulo-antigravity-001/docs/pt/antigravity/templates/overview.md) — Catálogo de templates

### Ferramentas

- [ ] [docs/pt/antigravity/tools/tool-mapping.md](file:///f:/Projetos%20C%C3%B3digos/AIOS%20Agentes/modulo-antigravity-001/docs/pt/antigravity/tools/tool-mapping.md) — Mapeamento Claude → Antigravit + ferramentas exclusivas

### Migração

- [ ] [docs/pt/antigravity/migration/from-claude.md](file:///f:/Projetos%20C%C3%B3digos/AIOS%20Agentes/modulo-antigravity-001/docs/pt/antigravity/migration/from-claude.md) — Guia de migração Claude → Antigravit

## Arquivos de Documentação — docs/en (paridade)

- [x] [docs/en/antigravity/index.md](file:///f:/Projetos%20C%C3%B3digos/AIOS%20Agentes/modulo-antigravity-001/docs/en/antigravity/index.md)
- [x] [docs/en/antigravity/agents/overview.md](file:///f:/Projetos%20C%C3%B3digos/AIOS%20Agentes/modulo-antigravity-001/docs/en/antigravity/agents/overview.md)
- [x] [docs/en/antigravity/tools/tool-mapping.md](file:///f:/Projetos%20C%C3%B3digos/AIOS%20Agentes/modulo-antigravity-001/docs/en/antigravity/tools/tool-mapping.md)
- [x] [docs/en/antigravity/migration/from-claude.md](file:///f:/Projetos%20C%C3%B3digos/AIOS%20Agentes/modulo-antigravity-001/docs/en/antigravity/migration/from-claude.md)
- [x] [docs/en/antigravity/agents/core-agents.md](file:///f:/Projetos%20C%C3%B3digos/AIOS%20Agentes/modulo-antigravity-001/docs/en/antigravity/agents/core-agents.md) (adicionado)
- [x] [docs/en/antigravity/getting-started.md](file:///f:/Projetos%20C%C3%B3digos/AIOS%20Agentes/modulo-antigravity-001/docs/en/antigravity/getting-started.md) (adicionado)

## Adaptação do Sistema de Squads (Squad Management)

- [x] Criar [docs/architecture/squad-management-adaptation-prd.md](file:///f:/Projetos%20C%C3%B3digos/AIOS%20Agentes/modulo-antigravity-001/docs/architecture/squad-management-adaptation-prd.md)
- [x] Criar estrutura `squads/squad-creator/`
  - [x] `squad.yaml`
  - [x] `agents/oalanicolas.md` (adaptado)
  - [x] `agents/pedro-valerio.md` (adaptado)
  - [x] `tasks/create-squad.md` (adaptado do framework)
  - [x] `tasks/sync-squads.md` (novo)
- [x] Atualizar `.antigravity/agents/squad-chief.md`
- [x] Atualizar `.antigravity/skills/squad/SKILL.md` e `clone-mind/SKILL.md`

## Verificação

- [ ] Verificar links internos entre arquivos
- [ ] Checar consistência de nomenclatura
