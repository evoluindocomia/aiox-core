# PRD — AIOS Governance Pipeline (AGP)

## Equivalente aos PreToolUse Hooks do Claude Code no Antigravity

> **Criado:** 2026-02-26  
> **Atualizado:** 2026-02-26 (v2 — Arquitetura REQUIRES_APPROVAL + Configurabilidade)  
> **Status:** 📋 Planejamento  
> **Task de implementação:** `task-governance-hooks.md` (nesta pasta)

---

## 1. Contexto e Problema

### 1.1 Situação Atual

O AIOS possui um sistema de governança no **Claude Code** baseado em 6 hooks Python que executam como `PreToolUse hooks` — interceptando operações **antes** de executarem, com bloqueio via `exit 2`:

| Hook                            | Operação Interceptada                       | Impacto se Ausente                  |
| ------------------------------- | ------------------------------------------- | ----------------------------------- |
| `enforce-architecture-first.py` | Escrita em `supabase/` sem doc arquitetural | Código sem documentação prévia      |
| `mind-clone-governance.py`      | Criação de agente sem DNA extraído          | Mind clones com personagem genérico |
| `sql-governance.py`             | SQL DDL direto (sem migration)              | Schema drift, sem histórico         |
| `enforce-git-push-authority.sh` | `git push` por agente não-devops            | Push não autorizado                 |
| `write-path-validation.py`      | Documentos em paths incorretos              | Organização comprometida            |
| `slug-validation.py`            | IDs/slugs fora de snake_case                | Inconsistência de naming            |

### 1.2 Gap no Antigravity

O Antigravity não possui sistema de interceptação automática de ferramentas. A solução atual (`governance.md`) é instrucional: o LLM lê as regras e decide aplicá-las proativamente.

**Cobertura estimada: ~95%**  
Os ~5% de gap ocorrem quando:

- O contexto de sessão é longo e a regra "some" da atenção ativa do LLM
- Agente está em modo auto-proceed (`ShouldAutoProceed: true`) e pula checkpoints
- Operações em cadeia rápida fazem o LLM priorizar velocidade
- Sub-agentes ativados não herdam o checklist completo

### 1.3 Causa Raiz do Gap

O problema combina dois fatores:

```
Fator 1: ShouldAutoProceed = true
    → Agente executa sem parar para confirmar
    → Operações críticas passam sem checkpoint

Fator 2: Instrucional vs Mecanismo
    → Regras dependem da memória ativa do LLM
    → Em contexto longo, regras perdem saliência
```

---

## 2. Solução Proposta: AIOS Governance Pipeline (AGP) v2

### 2.1 Insight Central

O Antigravity possui um mecanismo nativo que é o **equivalente funcional exato** do `exit 2` dos hooks do Claude Code:

```
Claude Code hooks:  exit 2 → runtime para a execução
Antigravity:        notify_user (BlockedOnUser=true) → plataforma para a execução
```

A diferença: `notify_user` com `BlockedOnUser=true` **não depende do bom comportamento do LLM** — o mecanismo da plataforma garante a pausa, independentemente do contexto ou modo de execução.

### 2.2 Três Resultados Possíveis

O AGP v2 introduz um terceiro resultado além de ALLOWED/BLOCKED:

| Resultado              | Mecanismo                        | Comportamento                                         |
| ---------------------- | -------------------------------- | ----------------------------------------------------- |
| ✅ `ALLOWED`           | Continua normalmente             | Operação prossegue sem interrupção                    |
| ⏸️ `REQUIRES_APPROVAL` | `notify_user` BlockedOnUser=true | **Plataforma para.** Usuário confirma ou rejeita      |
| 🛑 `BLOCKED`           | `notify_user` informativo        | Operação não prossegue, usuário é informado do motivo |

### 2.3 Fluxo Completo

```
Operação crítica pretendida
        ↓
[SKILL: governance-router]  ← Detecta tipo de operação
        ↓
[TASK: check-{regra}]       ← Executa validação + consulta config
        ↓
┌─────────────────────────────────────────────────────────────┐
│ ALLOWED          → prosseguir                               │
│ REQUIRES_APPROVAL → notify_user(BlockedOnUser=true)         │
│                    "Operação crítica detectada. Confirmar?" │
│                    Usuário: Sim → prossegue                 │
│                    Usuário: Não → cancela                   │
│ BLOCKED          → notify_user (informativo)                │
│                    "Bloqueado por governance. Motivo: ..."  │
└─────────────────────────────────────────────────────────────┘
```

### 2.4 Superioridade sobre Claude Code Hooks

| Critério                   | Claude Code Hooks           | AGP v2                                          |
| -------------------------- | --------------------------- | ----------------------------------------------- |
| **Mecanismo de bloqueio**  | `exit 2` (runtime)          | `notify_user` (plataforma)                      |
| **Interação com usuário**  | ❌ Bloqueia silenciosamente | ✅ Explica + pede confirmação                   |
| **Configurável por regra** | ❌ Todo-ou-nada             | ✅ Por regra: BLOCKED/REQUIRES_APPROVAL/ALLOWED |
| **Desabilitável**          | ❌ Requer editar hook       | ✅ `governance_mode: disabled`                  |
| **Rastreabilidade**        | Log no terminal             | Conversa documentada                            |
| **Ação corretiva**         | Texto em stderr             | Passo concreto + pipeline sugerido              |

---

## 3. Sistema de Configuração

### 3.1 Arquivo de Configuração

**Novo arquivo:** `.antigravity/rules/governance-config.md`

Este arquivo controla o comportamento de cada regra de governança:

```yaml
# AIOS Governance Pipeline — Configuração
# Valores possíveis por regra: BLOCKED | REQUIRES_APPROVAL | ALLOWED | disabled
# governance_mode: active (padrão) | disabled (desativa tudo)

governance:
  mode: active # Mude para 'disabled' para desativar completamente

  rules:
    architecture_first: REQUIRES_APPROVAL # Pede confirmação antes de criar em supabase/
    mind_clone_dna: BLOCKED # Nunca cria agente sem DNA
    sql_ddl: BLOCKED # Nunca executa DDL direto
    git_push_authority: REQUIRES_APPROVAL # Pede confirmação de push
    write_path: ALLOWED # Só avisa, não bloqueia
    slug_format: ALLOWED # Só corrige, não bloqueia
```

### 3.2 Valores de Configuração

| Valor                       | Comportamento                                         |
| --------------------------- | ----------------------------------------------------- |
| `BLOCKED`                   | Sempre bloqueia. Equivalente ao `exit 2` dos hooks.   |
| `REQUIRES_APPROVAL`         | Para e pede confirmação do usuário via `notify_user`. |
| `ALLOWED`                   | Notifica/orienta mas prossegue sem parar.             |
| `disabled`                  | Desativa completamente aquela regra.                  |
| `governance_mode: disabled` | Desativa o AGP inteiro (modo turbo sem governance).   |

### 3.3 Configuração Padrão Recomendada

```yaml
# Nível de segurança máximo (default)
architecture_first: REQUIRES_APPROVAL # Crítico mas reversível via doc
mind_clone_dna: BLOCKED # Irreversível sem pipeline completo
sql_ddl: BLOCKED # Schema drift é catastrófico
git_push_authority: REQUIRES_APPROVAL # Crítico — @devops deve confirmar
write_path: ALLOWED # Baixo impacto, só orientação
slug_format: ALLOWED # Baixo impacto, correção automática sugerida
```

### 3.4 Exemplos de Configuração Alternativa

**Modo Turbo (sem interrupções):**

```yaml
governance:
  mode: disabled
```

**Modo Leve (só BLOCKED para DDL e DNA):**

```yaml
rules:
  architecture_first: ALLOWED
  mind_clone_dna: BLOCKED
  sql_ddl: BLOCKED
  git_push_authority: ALLOWED
  write_path: disabled
  slug_format: disabled
```

**Modo Auditoria (tudo REQUIRES_APPROVAL):**

```yaml
rules:
  architecture_first: REQUIRES_APPROVAL
  mind_clone_dna: REQUIRES_APPROVAL
  sql_ddl: REQUIRES_APPROVAL
  git_push_authority: REQUIRES_APPROVAL
  write_path: REQUIRES_APPROVAL
  slug_format: REQUIRES_APPROVAL
```

---

## 4. Arquitetura Detalhada

### 4.1 Estrutura de Arquivos

```
.antigravity/
├── rules/
│   ├── governance.md              ← Existente (source of truth das políticas)
│   └── governance-config.md      ← NOVO (configuração dos resultados por regra)
└── skills/
    └── governance/                ← NOVO — AGP
        ├── SKILL.md               ← Roteador central (dispatcher)
        ├── check-architecture-first.md
        ├── check-mind-clone-dna.md
        ├── check-sql-governance.md
        ├── check-git-push-authority.md
        ├── check-write-path.md
        └── check-slug-format.md
```

### 4.2 SKILL.md — Roteador de Governança

O `SKILL.md` é o ponto de entrada único. Responsabilidades:

1. Receber a operação pretendida
2. Verificar se `governance_mode: disabled` → se sim, prosseguir sem validação
3. Mapear operação para a regra via tabela de gatilhos
4. Executar a task especializada
5. Ler o resultado da task + configuração da regra em `governance-config.md`
6. Executar a ação correspondente (prosseguir / notify_user REQUIRES_APPROVAL / notify_user BLOCKED)

**Tabela de Gatilhos:**

| Operação                                 | Condição de Gatilho                                         | Regra                | Task                       |
| ---------------------------------------- | ----------------------------------------------------------- | -------------------- | -------------------------- |
| `write_to_file` / `replace_file_content` | path contém `supabase/functions/` ou `supabase/migrations/` | `architecture_first` | `check-architecture-first` |
| `write_to_file` (arquivo novo)           | path match `squads/*/agents/*.md`                           | `mind_clone_dna`     | `check-mind-clone-dna`     |
| `run_command`                            | contém `CREATE TABLE`, `ALTER TABLE`, `DROP`...             | `sql_ddl`            | `check-sql-governance`     |
| `run_command`                            | contém `git push`                                           | `git_push_authority` | `check-git-push-authority` |
| `run_command`                            | contém `git worktree add/remove`                            | `git_push_authority` | `check-git-push-authority` |
| `write_to_file`                          | path em `docs/` com nome inconsistente                      | `write_path`         | `check-write-path`         |
| Geração de ID/slug                       | ID contém hífen, ponto ou maiúsculas                        | `slug_format`        | `check-slug-format`        |

### 4.3 Formato de Output das Tasks

Cada task retorna um resultado padronizado que o SKILL.md interpreta:

```
RESULT: ALLOWED
Motivo: [razão pela qual a operação é permitida]
Prosseguir com: [operação original]

— OU —

RESULT: REQUIRES_APPROVAL
Operação: [descrição da operação pretendida]
Regra: [nome da regra]
Motivo: [por que esta operação requer aprovação]
Contexto: [detalhes relevantes — ex: arquivo não existe ainda, agente ativo]
Ação sugerida se aprovado: [o que acontece se o usuário confirmar]
Alternativa: [o que fazer se rejeitar]

— OU —

RESULT: BLOCKED
Motivo: [razão exata do bloqueio]
Regra violada: [nome da regra]
Ação corretiva: [passo concreto a executar primeiro]
Pipeline sugerido: [comando/workflow a usar]
```

### 4.4 Comportamento do SKILL.md por Resultado

Após receber o output da task, o SKILL.md age assim:

```python
# Pseudocódigo do SKILL.md

config = ler("governance-config.md")[regra]

if config == "disabled":
    → prosseguir (sem validação)

resultado = executar(task)

if resultado == ALLOWED:
    → prosseguir normalmente

elif resultado == REQUIRES_APPROVAL or (resultado == BLOCKED and config == "REQUIRES_APPROVAL"):
    → notify_user(
        BlockedOnUser=True,
        Message=formatar_mensagem_approval(resultado),
        PathsToReview=[]
    )
    # Aguarda resposta do usuário
    # Se aprovado: prosseguir
    # Se rejeitado: cancelar + orientar alternativa

elif resultado == BLOCKED and config == "BLOCKED":
    → notify_user(
        BlockedOnUser=False,  # informativo, execução já parou
        Message=formatar_mensagem_blocked(resultado)
    )
    # Não prossegue
```

---

## 5. Especificação das 6 Tasks

### 5.1 `check-architecture-first`

**Gatilho:** `write_to_file`/`replace_file_content` em paths protegidos

**Lógica:**

1. Verificar ALWAYS_ALLOWED → ALLOWED (sem validação)
2. Verificar match de PROTECTED_PATH
3. Extrair `{nome}` do componente
4. Verificar existência de docs aprovados (`find_by_name`)
5. Verificar se arquivo alvo já existe (edição → ALLOWED)
6. Doc encontrado → ALLOWED
7. Doc não encontrado → REQUIRES_APPROVAL (config padrão)

**ALWAYS_ALLOWED:** `.antigravity/`, `docs/`, `outputs/`, `squads/`, `.aios-core/`, `node_modules/`, `.git/`, `package.json`, `tsconfig.json`, `.env`, `README.md`

---

### 5.2 `check-mind-clone-dna`

**Gatilho:** `write_to_file` criando novo arquivo em `squads/*/agents/*.md`

**Lógica:**

1. Arquivo já existe → ALLOWED (edição)
2. Extrair `{pack}` e `{agent_id}` do path
3. Match padrão funcional (sufixo/prefixo) → ALLOWED
4. Verificar DNA em localizações padrão (`find_by_name`)
5. DNA encontrado → ALLOWED
6. DNA não encontrado → BLOCKED (config padrão — não há alternativa sem DNA)

**Output BLOCKED inclui** o pipeline completo:

```
→ @squad-chief *collect-sources {agent_id}
→ @squad-chief *extract-voice-dna {agent_id}
→ @squad-chief *extract-thinking-dna {agent_id}
→ @squad-chief *create-agent {agent_id}
```

---

### 5.3 `check-sql-governance`

**Gatilho:** `run_command` com SQL DDL

**DDL Bloqueados:** `CREATE TABLE`, `CREATE VIEW`, `CREATE FUNCTION`, `CREATE TRIGGER`, `ALTER TABLE`, `DROP TABLE`, `DROP VIEW`, `DROP FUNCTION`, `CREATE TABLE AS SELECT`

**Output BLOCKED inclui:**

```
→ supabase migration new {nome-descritivo}
  (criar migration, depois: supabase db push)
```

---

### 5.4 `check-git-push-authority`

**Gatilho:** `run_command` com `git push` ou `git worktree`

**Lógica:**

- Agente ativo NÃO é `@devops` → REQUIRES_APPROVAL com delegação sugerida
- Agente ativo É `@devops` → verificar quality gates → ALLOWED ou REQUIRES_APPROVAL

**Output REQUIRES_APPROVAL (não-devops) inclui:**

```
Delegação: → @devops *push
```

---

### 5.5 `check-write-path`

**Gatilho:** `write_to_file` em `docs/` com path inconsistente

**Comportamento:** Sempre retorna REQUIRES_APPROVAL (não BLOCKED) — é um warning interativo.

**Tabela de paths corretos:**

| Tipo                | Path Correto             |
| ------------------- | ------------------------ |
| Sessions / handoffs | `docs/sessions/YYYY-MM/` |
| Arquitetura         | `docs/architecture/`     |
| Guias               | `docs/guides/`           |
| Stories             | `docs/stories/active/`   |
| Planos aprovados    | `docs/approved-plans/`   |

---

### 5.6 `check-slug-format`

**Gatilho:** Geração de qualquer ID, slug ou nome de arquivo

**Regex válido:** `^[a-z0-9]+(_[a-z0-9]+)*$`

**Comportamento ALLOWED:** Task corrige automaticamente e informa a versão snake_case correta, mas não bloqueia — apenas substitui o valor proposto.

---

## 6. Experiência do Usuário

### 6.1 Exemplo: REQUIRES_APPROVAL para git push

```
⏸️  GOVERNANCE — Aprovação Necessária

Operação: git push origin main
Agente: @dev (não é @devops)
Regra: git_push_authority

Esta operação requer confirmação pois apenas @devops (Gage) tem
autoridade de push. Deseja prosseguir mesmo assim?

Alternativa recomendada: → @devops *push

[ Confirmar ] [ Cancelar — usar @devops ]
```

### 6.2 Exemplo: BLOCKED para mind clone sem DNA

```
🛑  GOVERNANCE — Operação Bloqueada

Operação: Criar squads/mkt/agents/gary-halbert.md
Regra: mind_clone_dna

Este agente parece ser um mind clone (pessoa real), mas não foi
encontrado DNA extraído. Mind clones requerem DNA para garantir
autenticidade da persona.

Pipeline obrigatório:
→ @squad-chief *collect-sources gary_halbert
→ @squad-chief *extract-voice-dna gary_halbert
→ @squad-chief *extract-thinking-dna gary_halbert
→ @squad-chief *create-agent gary_halbert

Se for um agente funcional (não mind clone), renomeie com sufixo:
-chief, -orchestrator, -validator, -architect, etc.
```

### 6.3 Exemplo: governance_mode disabled

```yaml
# governance-config.md
governance:
  mode: disabled # ← turbo total, sem verificações
```

Resultado: SKILL.md retorna ALLOWED imediatamente para qualquer operação, sem executar tasks.

---

## 7. Integração com Agentes

### 7.1 Bloco Padrão em Cada Agente Chief

```markdown
## Protocolo de Governança (AGP)

> **OBRIGATÓRIO:** Antes de operações críticas, executar a skill de governance.
> Configuração em: `.antigravity/rules/governance-config.md`

| Operação                                | Regra AGP                  |
| --------------------------------------- | -------------------------- |
| Criar/editar em `supabase/`             | `check-architecture-first` |
| Criar novo agente em `squads/*/agents/` | `check-mind-clone-dna`     |
| Executar SQL DDL via `run_command`      | `check-sql-governance`     |
| `git push` ou `git worktree`            | `check-git-push-authority` |
| Salvar doc em `docs/` (path suspeito)   | `check-write-path`         |
| Gerar ID/slug                           | `check-slug-format`        |

**Entry point:** `.antigravity/skills/governance/SKILL.md`
```

---

## 8. Critérios de Aceitação

### 8.1 Funcionais

- [ ] SKILL.md lê `governance-config.md` para determinar o resultado final
- [ ] `REQUIRES_APPROVAL` usa `notify_user` com `BlockedOnUser=true`
- [ ] `BLOCKED` usa `notify_user` informativo (BlockedOnUser=false, pois não há escolha)
- [ ] `governance_mode: disabled` faz SKILL.md prosseguir sem executar tasks
- [ ] Cada regra pode ser configurada independentemente
- [ ] Cada task retorna output padronizado (RESULT: ALLOWED/REQUIRES_APPROVAL/BLOCKED)

### 8.2 Cobertura

- [ ] 100% das 6 regras dos hooks Python têm task equivalente
- [ ] ALWAYS_ALLOWED sincronizado com `enforce-architecture-first.py`
- [ ] Padrões funcionais sincronizados com `mind-clone-governance.py`
- [ ] DDL keywords sincronizados com `sql-governance.py`

### 8.3 Configuração

- [ ] `governance-config.md` existe com valores padrão documentados
- [ ] Cada valor (BLOCKED/REQUIRES_APPROVAL/ALLOWED/disabled) está documentado
- [ ] Exemplos de configuração alternativa estão documentados (Turbo, Leve, Auditoria)

### 8.4 UX

- [ ] Mensagens de REQUIRES_APPROVAL são claras e incluem alternativa
- [ ] Mensagens de BLOCKED incluem pipeline completo de resolução
- [ ] Usuário nunca fica sem saber o que fazer a seguir

---

## 9. Fora do Escopo (Fase 2)

- Dashboard de auditoria de aprovações/bloqueios
- Integração com CI/CD pipeline
- Histórico de decisões de governance por sessão
- Rate limiting por operação (ex: máximo N approvals por hora)
- Modificação dos hooks Python originais em `.claude/hooks/`

---

## 10. Roadmap de Implementação

Ver `task-governance-hooks.md` para breakdown completo.

**Estimativa total:** ~4 horas  
**Novos artefatos vs PRD v1:** `governance-config.md` (novo), lógica de 3 resultados em SKILL.md, UX de confirmação por resultado

```
H1. Criar estrutura base + SKILL.md com lógica de 3 resultados
H2. Criar governance-config.md com valores padrão
H3. Implementar 6 tasks (referenciando config)
H4. Atualizar governance.md
H5. Patch dos agentes chief
H6. Validação final de cobertura e UX
```

---

_AIOS Governance Pipeline v2.0 — PRD_  
_Antigravit Environment — 2026-02-26_  
_Arquitetura: Tasks + notify_user + Configuração por Regra_
