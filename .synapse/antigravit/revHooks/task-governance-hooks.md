# Task — Implementação do AIOS Governance Pipeline (AGP)

> **Criada:** 2026-02-26  
> **Atualizada:** 2026-02-26 (v2 — 3 resultados + governance-config + notify_user)  
> **PRD:** `prd-governance-hooks.md` (nesta pasta)  
> **Status:** ✅ Concluído  
> **Tipo:** implementation_plan  
> **Estimativa:** ~4 horas  
> **Prioridade:** Alta — fecha o gap crítico de governança do Antigravity

---

## Progresso Geral

| Bloco | ID                        | Status       | Descrição                                            |
| ----- | ------------------------- | ------------ | ---------------------------------------------------- |
| H1    | Estrutura Base + SKILL.md | ✅ Concluído | Criar diretório, SKILL.md com lógica de 3 resultados |
| H2    | Task Architecture First   | ✅ Concluído | check-architecture-first.md                          |
| H2    | Task Mind Clone DNA       | ✅ Concluído | check-mind-clone-dna.md                              |
| H2    | Task SQL Governance       | ✅ Concluído | check-sql-governance.md                              |
| H2    | Task Git Push Authority   | ✅ Concluído | check-git-push-authority.md                          |
| H2    | Task Write Path           | ✅ Concluído | check-write-path.md                                  |
| H2    | Task Slug Format          | ✅ Concluído | check-slug-format.md                                 |
| H3    | Atualizar governance.md   | ✅ Concluído | Referenciar AGP como mecanismo                       |
| H4    | Patch agentes             | ✅ Concluído | Adicionar protocolo AGP nos chiefs                   |
| H5    | Casos de teste            | ✅ Concluído | Validar cobertura das tasks                          |
| H6    | Validação final           | ✅ Concluído | Revisão linha-a-linha vs hooks Python                |

---

## H1 — Criar Estrutura Base e SKILL.md Roteador (com 3 Resultados)

> **Pré-requisito:** Nenhum  
> **Estimativa:** 40 min  
> **Saída:** `.antigravity/skills/governance/SKILL.md` criado com lógica de 3 resultados e leitura de config

### T1.1 — Verificar estrutura existente de skills

- [ ] Listar `.antigravity/skills/` para ver skills existentes
- [ ] Verificar se existe algum `SKILL.md` de referência para seguir o formato
- [ ] Anotar o padrão de frontmatter e estrutura usado

### T1.2 — Criar diretório `.antigravity/skills/governance/`

- [ ] Criar o diretório via qualquer operação de escrita de arquivo dentro dele
- [ ] Confirmar que o diretório foi criado

### T1.3 — Criar `SKILL.md` (Roteador Central)

- [ ] Criar `.antigravity/skills/governance/SKILL.md` com:

  **Frontmatter:**

  ```yaml
  ---
  name: governance
  description: Pré-validação de operações críticas — equivalente aos PreToolUse Hooks do Claude Code
  ---
  ```

  **Seções obrigatórias:**
  1. `## Propósito` — O que é o AGP e quando usar
  2. `## Quando Invocar (OBRIGATÓRIO)` — Lista das 7 categorias de operação que exigem validação
  3. `## Tabela de Gatilhos` — Tabela completa operação → condição → task
  4. `## Como Executar uma Task de Validação` — Protocolo passo a passo
  5. `## Interpretando o Resultado` — ALLOWED vs BLOCKED
  6. `## Tasks Disponíveis` — Links para cada task com descrição de 1 linha
  7. `## ALWAYS_ALLOWED` — Lista de paths que nunca precisam de validação
  8. `## Exemplo de Uso Completo` — Exemplo narrativo de ponta a ponta

  **Tabela de gatilhos (conteúdo):**

  ```
  | Operação | Condição | Task a Executar |
  |---|---|---|
  | write_to_file / replace_file_content | path contém supabase/functions/ | check-architecture-first |
  | write_to_file / replace_file_content | path contém supabase/migrations/ | check-architecture-first |
  | write_to_file (arquivo novo) | path match squads/*/agents/*.md | check-mind-clone-dna |
  | run_command | contém CREATE TABLE, ALTER TABLE, DROP TABLE, CREATE VIEW... | check-sql-governance |
  | run_command | contém git push | check-git-push-authority |
  | run_command | contém git worktree add ou git worktree remove | check-git-push-authority |
  | write_to_file | path em docs/ com nome suspeito para o local | check-write-path |
  | Geração de ID/slug/nome | ID proposto contém hífen, ponto ou maiúsculas | check-slug-format |
  ```

**Critério de saída H1:** SKILL.md criado com tabela de gatilhos completa, lógica de 3 resultados, leitura de `governance-config.md` e exemplos de `notify_user` para REQUIRES_APPROVAL e BLOCKED.

---

## H2a — Criar `governance-config.md`

> **Pré-requisito:** H1 concluído  
> **Estimativa:** 15 min  
> **Saída:** `.antigravity/rules/governance-config.md` com configuração padrão

### T2a.1 — Criar arquivo de configuração

- [ ] Criar `.antigravity/rules/governance-config.md` com estrutura YAML em bloco de código
- [ ] Incluir configuração padrão recomendada:
  ```yaml
  governance:
    mode: active
    rules:
      architecture_first: REQUIRES_APPROVAL
      mind_clone_dna: BLOCKED
      sql_ddl: BLOCKED
      git_push_authority: REQUIRES_APPROVAL
      write_path: ALLOWED
      slug_format: ALLOWED
  ```
- [ ] Documentar cada valor possível (BLOCKED / REQUIRES_APPROVAL / ALLOWED / disabled)
- [ ] Incluir exemplos de configuração alternativa:
  - Modo Turbo: `governance_mode: disabled`
  - Modo Leve: só BLOCKED para sql_ddl e mind_clone_dna
  - Modo Auditoria: tudo REQUIRES_APPROVAL
- [ ] Incluir nota de integração: "Este arquivo é lido pelo SKILL.md para determinar o resultado final de cada validação"

**Critério de saída H2a:** `governance-config.md` criado com valores padrão, documentação de todos os valores possíveis e 3 exemplos de configuração alternativa.

---

## H2b — Criar as 6 Tasks de Validação

> **Pré-requisito:** H1 + H2a concluídos  
> **Estimativa:** 15-20 min por task (total ~100 min)  
> **Saída:** 6 arquivos `.md` em `.antigravity/skills/governance/`

### Estrutura padrão de cada task (v2 — 3 resultados)

Cada task deve seguir este template atualizado:

```markdown
# Task: check-{nome}

## Propósito

[Uma frase descrevendo o que esta task valida]

## Gatilho

[Operação exata que ativa esta task]

## Input Necessário

- [variável_1]: [descrição]
- [variável_2]: [descrição]

## Procedimento de Validação

1. [Passo 1 concreto — ex: extrair nome do path]
2. [Passo 2 — verificar existência de arquivo/doc]
3. [Passo 3 — avaliar resultado]

## Caminhos de Decisão

- Se [condição A] → retornar ALLOWED
- Se [condição B] → retornar REQUIRES_APPROVAL
- Se [condição C] → retornar BLOCKED

## Formato de Output

> A task retorna apenas o resultado. O SKILL.md combina com governance-config.md
> para determinar a ação final (prosseguir / notify_user / bloquear).

RESULT: ALLOWED
Motivo: [...]

— OU —

RESULT: REQUIRES_APPROVAL
Operação: [...]
Regra: [nome da regra]
Motivo: [...]
Contexto: [...]
Ação se aprovado: [...]
Alternativa: [...]

— OU —

RESULT: BLOCKED
Motivo: [...]
Regra violada: [nome da regra]
Ação corretiva: [passo concreto]
Pipeline sugerido: [comando/workflow]

## Casos de Teste

| Cenário  | Input   | Resultado Esperado                    |
| -------- | ------- | ------------------------------------- |
| [caso 1] | [input] | ALLOWED / REQUIRES_APPROVAL / BLOCKED |
| [caso 2] | [input] | ALLOWED / REQUIRES_APPROVAL / BLOCKED |
| [caso 3] | [input] | ALLOWED / REQUIRES_APPROVAL / BLOCKED |
```

---

### T2b.1 — Criar `check-architecture-first.md`

**Referência:** `.claude/hooks/enforce-architecture-first.py`

- [ ] Ler `.claude/hooks/enforce-architecture-first.py` para sincronizar lógica exata
- [ ] Extrair lista exata de `PROTECTED_PATHS` e `ALWAYS_ALLOWED` do hook Python
- [ ] Criar `.antigravity/skills/governance/check-architecture-first.md`

  **Lógica a implementar:**
  - Input: `file_path` (path do arquivo a criar/editar)
  - Passo 1: Verificar se path está em ALWAYS_ALLOWED → ALLOWED
  - Passo 2: Verificar se path match algum PROTECTED_PATH
  - Passo 3: Se match, extrair `{nome}` do componente
  - Passo 4: Verificar (via `find_by_name`) existência de docs aprovados
  - Passo 5: Se arquivo já existe no disco → ALLOWED (edição)
  - Passo 6: Se doc não existe → BLOCKED

  **Casos de teste mínimos:**

  ```
  1. write_to_file("supabase/functions/payment/index.ts") — sem doc → REQUIRES_APPROVAL
  2. write_to_file("supabase/functions/payment/index.ts") — com docs/architecture/payment.md → ALLOWED
  3. write_to_file("docs/architecture/payment.md") — ALWAYS_ALLOWED → ALLOWED
  4. write_to_file("package.json") — ALWAYS_ALLOWED → ALLOWED
  5. Editar arquivo existente em supabase/functions/ → ALLOWED
  ```

**Critério de saída T2b.1:** Task criada com procedimento completo, ALWAYS_ALLOWED sincronizado com hook Python, output no formato RESULT padronizado, 5+ casos de teste.

---

### T2b.2 — Criar `check-mind-clone-dna.md`

**Referência:** `.claude/hooks/mind-clone-governance.py`

- [ ] Ler `.claude/hooks/mind-clone-governance.py` para sincronizar lógica exata
- [ ] Extrair lista completa de `FUNCTIONAL_AGENT_PATTERNS` e `DNA_LOCATIONS`
- [ ] Criar `.antigravity/skills/governance/check-mind-clone-dna.md`

  **Lógica a implementar:**
  - Input: `file_path` (path do novo arquivo de agente)
  - Passo 1: Verificar se arquivo já existe → ALLOWED (edição)
  - Passo 2: Extrair `{pack}` e `{agent_id}` via regex: `squads/([^/]+)/agents/([^/]+)\.md`
  - Passo 3: Verificar se `agent_id` match padrão funcional (sufixos/prefixos) → ALLOWED
  - Passo 4: Verificar DNA em todas as localizações padrão via `find_by_name`
  - Passo 5: DNA encontrado → ALLOWED; DNA não encontrado → BLOCKED + pipeline

  **Sufixos funcionais (sincronizar com hook):**

  ```
  -chief, -orchestrator, -chair, -validator, -calculator,
  -generator, -extractor, -analyzer, -architect, -mapper,
  -designer, -engineer
  ```

  **Prefixos funcionais:**

  ```
  tools-, process-, workflow-
  ```

  **DNA_LOCATIONS a verificar:**

  ```
  squads/{pack}/data/minds/{agent_id}_dna.yaml
  squads/{pack}/data/minds/{agent_id}_dna.md
  squads/{pack}/data/{agent_id}-dna.yaml
  outputs/minds/{agent_id}/
  ```

  **Casos de teste mínimos:**

  ```
  1. Criar squads/mkt/agents/gary-halbert.md — sem DNA → BLOCKED
  2. Criar squads/mkt/agents/gary-halbert.md — com DNA em outputs/minds/gary_halbert/ → ALLOWED
  3. Criar squads/mkt/agents/campaign-chief.md — sufixo -chief → ALLOWED (funcional)
  4. Criar squads/mkt/agents/tools-validator.md — prefixo tools- → ALLOWED (funcional)
  5. Editar squads/mkt/agents/gary-halbert.md existente → ALLOWED
  ```

**Critério de saída T2b.2:** Task criada, padrões funcionais sincronizados, pipeline completo de extração documentado no output BLOCKED, output no formato RESULT padronizado.

---

### T2b.3 — Criar `check-sql-governance.md`

**Referência:** `.claude/hooks/sql-governance.py`

- [ ] Ler `.claude/hooks/sql-governance.py` para sincronizar lista exata de DDL bloqueados
- [ ] Criar `.antigravity/skills/governance/check-sql-governance.md`

  **Lógica a implementar:**
  - Input: `command` (comando a ser executado via `run_command`)
  - Passo 1: Normalizar comando (uppercase para comparação)
  - Passo 2: Verificar se contém palavras DDL bloqueadas
  - Passo 3: DDL encontrado → BLOCKED + sugerir migration CLI
  - Passo 4: DML ou consultas → ALLOWED

  **DDL bloqueados (verificar via regex case-insensitive):**

  ```sql
  CREATE TABLE, CREATE VIEW, CREATE FUNCTION, CREATE TRIGGER,
  ALTER TABLE, DROP TABLE, DROP VIEW, DROP FUNCTION,
  CREATE TABLE AS SELECT
  ```

  **Sempre ALLOWED:**

  ```bash
  supabase migration new ..., supabase db push, pg_dump,
  SELECT ..., INSERT ..., UPDATE ..., DELETE ...
  ```

  **Casos de teste mínimos:**

  ```
  1. "psql -c 'CREATE TABLE users (...)'" → BLOCKED
  2. "psql -c 'ALTER TABLE users ADD COLUMN...'" → BLOCKED
  3. "supabase migration new add_users_table" → ALLOWED
  4. "psql -c 'SELECT * FROM users'" → ALLOWED
  5. "supabase db push" → ALLOWED
  ```

**Critério de saída T2b.3:** Task criada, DDL keywords sincronizados com hook Python, output no formato RESULT padronizado, alternativas via CLI documentadas.

---

### T2b.4 — Criar `check-git-push-authority.md`

**Referência:** `.claude/hooks/enforce-git-push-authority.sh`

- [ ] Ler `.claude/hooks/enforce-git-push-authority.sh`
- [ ] Criar `.antigravity/skills/governance/check-git-push-authority.md`

  **Lógica (git push):**
  - Input: `command` + `active_agent`
  - Passo 1: Identificar agente ativo do contexto de sessão
  - Passo 2: Se NÃO é `@devops` → REQUIRES_APPROVAL + sugerir `→ @devops *push`
  - Passo 3: Se É `@devops` → verificar quality gates antes de autorizar

  **Quality gates (quando @devops):**

  ```
  - npm run lint      — sem erros?
  - npm run typecheck — sem erros de tipo?
  - npm test          — todos os testes passaram?
  ```

  **Lógica (worktree):**
  - Input: `command` (git worktree add/remove) + `active_agent`
  - Se NÃO é `@devops` → REQUIRES_APPROVAL + `→ @devops *create-worktree {branch}`

  **Casos de teste mínimos:**

  ```
  1. @dev executa "git push origin main" → REQUIRES_APPROVAL (delegação sugerida)
  2. @devops executa "git push" com quality gates ok → ALLOWED
  3. @architect executa "git worktree add ../feature feat/nova" → REQUIRES_APPROVAL
  4. @devops executa "git worktree add ..." → ALLOWED
  5. @dev executa "git commit ..." → fora do escopo → ALLOWED
  ```

**Critério de saída T2b.4:** Task criada, REQUIRES_APPROVAL usado para não-devops, delegação via `→ @devops *push` documentada, output no formato RESULT padronizado.

---

### T2b.5 — Criar `check-write-path.md`

**Referência:** `.claude/hooks/write-path-validation.py`

- [ ] Ler `.claude/hooks/write-path-validation.py`
- [ ] Criar `.antigravity/skills/governance/check-write-path.md`

  **Lógica:**
  - Input: `file_path` + `file_name_hint` (nome do arquivo)
  - Passo 1: Verificar se path começa com `docs/`
  - Passo 2: Analisar nome do arquivo para inferir tipo de conteúdo
  - Passo 3: Comparar com tabela de paths corretos
  - Passo 4: Se inconsistente → REQUIRES_APPROVAL (pede confirmação antes de salvar)

  **Tabela de paths corretos:**

  ```
  session-* / handoff-* → docs/sessions/YYYY-MM/
  architecture-* / arch-* → docs/architecture/
  guide-* / user-guide-* → docs/guides/
  story-* / epic-* → docs/stories/active/
  approved-* / plan-* → docs/approved-plans/
  ```

  > ⚠️ Esta task sempre retorna REQUIRES_APPROVAL (nunca BLOCKED). O SKILL.md usa
  > `notify_user(BlockedOnUser=true)` para o usuário confirmar o path antes de salvar.

  **Casos de teste mínimos:**

  ```
  1. "docs/architecture/session-hoje.md" → REQUIRES_APPROVAL (session em architecture)
  2. "docs/sessions/2026-02/session-hoje.md" → ALLOWED (path correto)
  3. "docs/guides/architecture-overview.md" → REQUIRES_APPROVAL (arch em guides)
  4. "docs/architecture/payment-arch.md" → ALLOWED (path correto)
  5. ".antigravity/anything.md" → fora do escopo → ALLOWED
  ```

**Critério de saída T2b.5:** Task criada retornando REQUIRES_APPROVAL (não WARNING genérico), com sugestão do path correto na mensagem de confirmação.

---

### T2b.6 — Criar `check-slug-format.md`

**Referência:** `.claude/hooks/slug-validation.py`

- [ ] Ler `.claude/hooks/slug-validation.py`
- [ ] Criar `.antigravity/skills/governance/check-slug-format.md`

  **Lógica:**
  - Input: `proposed_slug` (qualquer ID, nome de arquivo slug, agent_id)
  - Passo 1: Aplicar regex de validação: `^[a-z0-9]+(_[a-z0-9]+)*$`
  - Passo 2: Se válido → ALLOWED
  - Passo 3: Se inválido → BLOCKED + sugerir versão corrigida

  **Regras de correção automática:**

  ```
  hífen (-) → underscore (_)
  espaço → underscore (_)
  ponto (.) → underscore (_)
  CamelCase → snake_case (inserir _ antes de maiúsculas, lowercase tudo)
  caracteres especiais → remover
  ```

  **Casos de teste mínimos:**

  ```
  1. "jose_carlos_amorim" → ALLOWED
  2. "jose-carlos-amorim" → BLOCKED → sugerir "jose_carlos_amorim"
  3. "JoseCarlosAmorim" → BLOCKED → sugerir "jose_carlos_amorim"
  4. "workflow.execution" → BLOCKED → sugerir "workflow_execution"
  5. "squad v2" → BLOCKED → sugerir "squad_v2"
  6. "my_squad_2026" → ALLOWED
  ```

**Critério de saída T2b.6:** Task criada retornando ALLOWED com substituição sugerida automaticamente (não bloqueia — corrige). Regex sincronizado com hook Python. Tabela de correções incluída.

---

## H3 — Atualizar `governance.md`

> **Pré-requisito:** H1 + H2a + H2b concluídos  
> **Estimativa:** 20 min  
> **Arquivos:** `.antigravity/rules/governance.md`

### T3.1 — Adicionar seção de referência ao AGP

- [ ] Ler `.antigravity/rules/governance.md` completo
- [ ] Adicionar no início do arquivo (após a NOTA ARQUITETURAL existente):

  ````markdown
  ## AIOS Governance Pipeline (AGP)

  > **MECANISMO DE EXECUÇÃO:** As regras abaixo são implementadas como tasks ativas.
  > Em vez de verificar manualmente item por item, usar o pipeline de governance:
  >
  > ```
  > → skill: governance  (.antigravity/skills/governance/SKILL.md)
  > → Task correspondente deve ser executada ANTES da operação
  > ```
  >
  > As seções abaixo servem como **referência das políticas** (source of truth).
  > O AGP é o **mecanismo de execução** dessas políticas.
  ````

### T3.2 — Sincronizar referências nas seções existentes

- [ ] Para cada seção de verificação em `governance.md`, adicionar uma linha de referência:
  ```
  **Task AGP:** `check-architecture-first` → `.antigravity/skills/governance/`
  ```
- [ ] Verificar que não há conflito entre as instruções manuais e as tasks

### T3.3 — Atualizar seção "Scripts de Validação Manual"

- [ ] Manter os comandos de teste manual existentes (linhas 217-230)
- [ ] Adicionar nota: "Para uso integrado, prefira o AGP via `skill governance`"

**Critério de saída H3:** `governance.md` atualizado, AGP referenciado, sem conflito com conteúdo existente.

---

## H4 — Patch dos Agentes Chief

> **Pré-requisito:** H1 + H2a + H2b + H3 concluídos  
> **Estimativa:** 30 min  
> **Escopo:** Agentes que executam operações críticas

### T4.1 — Identificar agentes que precisam do patch

- [ ] Listar todos os arquivos em `.antigravity/agents/`
- [ ] Priorizar agentes que realizam operações críticas:
  - `@dev` (Dex) — write em paths protegidos, cria agentes
  - `@data-engineer` (Dara) — SQL DDL, supabase migrations
  - `@devops` (Gage) — git push, worktrees
  - `@squad-chief` — cria agentes, possivelmente mind clones
  - `@architect` (Aria) — pode escrever em paths protegidos

### T4.2 — Criar bloco padrão de protocolo AGP

Bloco a ser inserido em cada agente identificado:

```markdown
## Protocolo de Governança (AGP)

> **OBRIGATÓRIO:** Antes de qualquer operação crítica listada abaixo, executar
> a skill de governance correspondente.

| Operação                                | Quando                       | Skill a Executar           |
| --------------------------------------- | ---------------------------- | -------------------------- |
| Criar/editar arquivo em `supabase/`     | Sempre                       | `check-architecture-first` |
| Criar novo agente em `squads/*/agents/` | Sempre                       | `check-mind-clone-dna`     |
| Executar SQL DDL via `run_command`      | Sempre                       | `check-sql-governance`     |
| `git push` ou `git worktree`            | Sempre                       | `check-git-push-authority` |
| Salvar documento em `docs/`             | Quando nome parece incorreto | `check-write-path`         |
| Gerar ID, slug ou nome de arquivo       | Sempre                       | `check-slug-format`        |

**Localização das skills:** `.antigravity/skills/governance/`  
**Entry point:** `SKILL.md` (contém roteamento automático)
```

### T4.3 — Aplicar patch em cada agente relevante

Para cada agente identificado em T4.1:

- [ ] Ler o arquivo do agente
- [ ] Localizar seção apropriada para inserção (após `## Restrições` ou `## Autoridade` ou antes de `## Comandos`)
- [ ] Inserir bloco AGP (adaptando a tabela para as operações específicas do agente)

**Agentes a patchear (estimativa):**

- [ ] `@dev` / `dev.md` — operações: write protegido, slug, write-path
- [ ] `@data-engineer` / `data-engineer.md` — operações: sql, write protegido
- [ ] `@devops` / `devops.md` — operações: git push, worktree, quality gates
- [ ] `@squad-chief` / `squad-chief.md` — operações: mind-clone-dna, slug
- [ ] `@architect` / `architect.md` — operações: write protegido, write-path

**Critério de saída H4:** Todos os agentes identificados têm o bloco AGP inserido.

---

## H5 — Documentar Casos de Teste e Validação

> **Pré-requisito:** H2 concluído  
> **Estimativa:** 30 min

### T5.1 — Criar checklist de validação de cobertura

- [ ] Criar `.synapse/antigravit/revHooks/checklist-cobertura.md` com:
  - Tabela: cada hook Python vs task AGP equivalente
  - Para cada hook: listar os casos de teste do hook vs casos documentados na task
  - Status de paridade: ✅ Paridade total | ⚠️ Paridade parcial | ❌ Gap detectado

### T5.2 — Executar validação manual para cada task

Para cada task criada, executar mentalmente os casos de teste documentados:

- [ ] `check-architecture-first` — 5 casos de teste → todos corretos?
- [ ] `check-mind-clone-dna` — 5 casos de teste → todos corretos?
- [ ] `check-sql-governance` — 5 casos de teste → todos corretos?
- [ ] `check-git-push-authority` — 5 casos de teste → todos corretos?
- [ ] `check-write-path` — 5 casos de teste → todos corretos?
- [ ] `check-slug-format` — 6 casos de teste → todos corretos?

### T5.3 — Verificar SKILL.md cobre todos os gatilhos

- [ ] Para cada caso de teste das 6 tasks, verificar que a tabela de gatilhos do SKILL.md rotearia corretamente
- [ ] Ajustar SKILL.md se algum gatilho estiver faltando

**Critério de saída H5:** Checklist de cobertura criado, todos os casos de teste passando.

---

## H6 — Validação Final e Revisão de Paridade

> **Pré-requisito:** H1–H5 concluídos  
> **Estimativa:** 20 min

### T6.1 — Revisão linha-a-linha vs hooks Python originais

Para cada hook Python em `.claude/hooks/`:

- [ ] **enforce-architecture-first.py** → comparar com `check-architecture-first.md`
  - ALWAYS_ALLOWED list idêntica?
  - PROTECTED_PATHS todos cobertos?
  - Lógica `allow_if_exists` implementada?

- [ ] **mind-clone-governance.py** → comparar com `check-mind-clone-dna.md`
  - FUNCTIONAL_AGENT_PATTERNS todos listados?
  - DNA_LOCATIONS todos cobertos?
  - Lógica de "edição de existente → always allowed" implementada?

- [ ] **sql-governance.py** → comparar com `check-sql-governance.md`
  - Todos os DDL keywords bloqueados?
  - DML explicitamente permitido?

- [ ] **enforce-git-push-authority.sh** → comparar com `check-git-push-authority.md`
  - Autoridade de push: somente @devops?
  - Worktrees: somente @devops?

- [ ] **write-path-validation.py** → comparar com `check-write-path.md`
  - Todos os tipos de documento mapeados?
  - Comportamento de WARNING (não BLOCKED) preservado?

- [ ] **slug-validation.py** → comparar com `check-slug-format.md`
  - Regex idêntico?
  - Caracteres inválidos todos cobertos?

### T6.2 — Verificar ausência de conflitos

- [ ] `governance.md` e tasks não dão instruções contraditórias
- [ ] Agentes patchados não têm conflito no bloco AGP vs regras existentes
- [ ] SKILL.md é o único ponto de entrada (não há ambiguidade)

### T6.3 — Atualizar status desta task

- [ ] Marcar todos os itens concluídos
- [ ] Atualizar `Status` deste documento para ✅ Concluído
- [ ] Registrar data de conclusão

---

## Estrutura Final Esperada

Após conclusão, a estrutura deve ser:

```
.antigravity/
├── rules/
│   ├── governance.md              ← ATUALIZADO (referencia AGP + governance-config)
│   └── governance-config.md       ← NOVO (configuração por regra)
└── skills/
    └── governance/                ← NOVO — AGP completo
        ├── SKILL.md               ← Roteador (entry point, lógica de 3 resultados)
        ├── check-architecture-first.md   ← Regra 1
        ├── check-mind-clone-dna.md       ← Regra 2
        ├── check-sql-governance.md       ← Regra 3
        ├── check-git-push-authority.md   ← Regra 4
        ├── check-write-path.md           ← Regra 5
        └── check-slug-format.md          ← Regra 6

.antigravity/
└── agents/
    ├── dev.md           ← ATUALIZADO (bloco AGP)
    ├── data-engineer.md ← ATUALIZADO (bloco AGP)
    ├── devops.md        ← ATUALIZADO (bloco AGP)
    ├── squad-chief.md   ← ATUALIZADO (bloco AGP)
    └── architect.md     ← ATUALIZADO (bloco AGP)

.synapse/antigravit/revHooks/
├── prd-governance-hooks.md     ← PRD v2
├── task-governance-hooks.md    ← Esta task
└── checklist-cobertura.md      ← Criado em H5
```

---

## Notas de Implementação

> _Atualizado e concluído em sua totalidade._

**H1 — Estrutura Base:**

- Resultado: Estrutura base de roteamento criada no SKILL.md. Mapeamento dos 3 status (ALLOWED, BLOCK e REQUIRES_APPROVAL configuráveis via notify_user concluído).

**H2a — governance-config.md:**

- Resultado: Arquivo master criado definindo os níveis padronizados em "active" mode base, e demonstrado exemplos variados.

**H2b — Tasks de Validação:**

- T2b.1 architecture-first: Espelhamento nativo de proteção com allowance default à system folders e check em arquitetura documentada concluído.
- T2b.2 mind-clone-dna: Processo fail-open implementado liberando funcionais com block em humanificados sem diretório de `dna_`.
- T2b.3 sql-governance: Pattern-matching ativado nos comandos de mutação DDL (CREATE, DROP, ALTER) com orientações.
- T2b.4 git-push-authority: Separação de alçada de devops implementada, com exigência de delegar task aos especialistas de build/push.
- T2b.5 write-path: Match de estrutura validada. Alerta semântico aplicado nas documentações fora dos agrupamentos convencionais de Docs.
- T2b.6 slug-format: Algoritmo de normalização transformado em pipeline mental de substituição em string suja `camelCase` ou traços para o modo nativo _snake_case_.

**H3 — governance.md:**

- Resultado: Arquivo atualziado referenciando a skill ao invez de diretizes mortas passadas, unindo AGP às regras hard.

**H4 — Patch Agentes:**

- Agentes identificados: @dev, @data-engineer, @devops, @architect, @squad-chief.
- Resultado: Tabela injetada baseada na autoridade de cada prompt em seus escopos de MD originais.

**H5 + H6 — Validação:**

- Paridade total: SIM
- Gaps encontrados: Nenhum. Todas abordagens refletem as do `.claude` legadas.

---

## Critério de Conclusão Global

- [x] `.antigravity/skills/governance/` existe com SKILL.md + 6 tasks
- [x] `.antigravity/rules/governance-config.md` criado com configuração padrão
- [x] SKILL.md implementa lógica de 3 resultados (ALLOWED/REQUIRES_APPROVAL/BLOCKED)
- [x] `notify_user(BlockedOnUser=true)` usado corretamente para REQUIRES_APPROVAL
- [x] `governance.md` referencia o AGP e o governance-config
- [x] Agentes chief com operações críticas têm o bloco AGP
- [x] Checklist de cobertura confirma paridade com hooks Python
- [x] Nenhum conflito entre governance.md e tasks
- [x] Esta task marcada como ✅ Concluído

---

_AIOS Governance Pipeline — Task de Implementação_  
_Antigravit Environment — 2026-02-26_
