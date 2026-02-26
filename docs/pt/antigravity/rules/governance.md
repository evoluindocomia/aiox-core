# Governance — Governança Automática

> **Origem:** Este arquivo substitui os **6 hooks Python** (PreToolUse) do Claude Code.  
> Como o Antigravit não possui sistema de interceptação automática de ferramentas, estas verificações são aplicadas **proativamente** pelo agente antes de cada operação crítica.

---

## Como Funciona

No Claude Code, haviam scripts Python que **bloqueavam automaticamente** operações indesejadas antes de executarem:

```
enforce-architecture-first.py  → bloqueava writes sem doc aprovada
mind-clone-governance.py       → bloqueava criação sem DNA
sql-governance.py              → bloqueava SQL DDL direto
enforce-git-push-authority.sh  → bloqueava push de não-devops
write-path-validation.py       → validava paths de documentos
slug-validation.py             → validava formato de slugs
```

No Antigravit, **essas regras vivem em `governance.md`** e são verificadas instrucionalmente pelo agente (sem automação, mas com cobertura de ~95% dos casos).

---

## Verificações Obrigatórias

### 🔴 Antes de ESCREVER em paths protegidos

**Gatilho:** `write_to_file` ou `replace_file_content` em:

- `supabase/functions/**`
- `supabase/migrations/**`

**Checklist:**

- [ ] Existe `docs/architecture/{nome}.md` aprovado?
- [ ] Ou existe `docs/approved-plans/{nome}.md` aprovado?
- [ ] Se o arquivo já existir → operação de edição é **permitida**

**Se documentação NÃO existe:**

1. Criar documentação arquitetural primeiro
2. Obter aprovação via `notify_user`
3. Então retornar à operação de código

**Paths ALWAYS ALLOWED** (não requerem doc):

```
.antigravity/  |  docs/  |  outputs/  |  squads/
.aios-core/    |  .aios-custom/  |  node_modules/  |  .git/
package.json   |  tsconfig.json  |  .env  |  README.md
```

---

### 🔴 Antes de CRIAR agente em `squads/*/agents/*.md`

**Gatilho:** `write_to_file` criando novo `.md` em diretório `squads/*/agents/`

**Checklist — verificar se é agente funcional:**

- [ ] O agent-id tem sufixo funcional?  
       (`-chief`, `-orchestrator`, `-chair`, `-validator`, `-calculator`, `-generator`, `-extractor`, `-analyzer`, `-architect`, `-mapper`, `-designer`, `-engineer`)
- [ ] Ou começa com `tools-`, `process-`, `workflow-`?

**Se SIM** → ✅ Agente funcional. Criar normalmente.

**Se NÃO** (provavelmente pessoa real) → Verificar DNA:

- [ ] Existe `squads/{pack}/data/minds/{agent_id}_dna.yaml`?
- [ ] Ou `squads/{pack}/data/{agent_id}-dna.yaml`?
- [ ] Ou `outputs/minds/{agent_id}/`?

**Se DNA NÃO existe** → **BLOQUEAR.** Executar pipeline:

```
*collect-sources → *extract-voice-dna → *extract-thinking-dna → *create-agent
```

---

### 🔴 Antes de EXECUTAR SQL DDL via `run_command`

**Gatilho:** `run_command` contendo qualquer SQL DDL

**Comandos BLOQUEADOS** (nunca executar diretamente):

```sql
CREATE TABLE ...
CREATE VIEW ...
CREATE FUNCTION ...
CREATE TRIGGER ...
ALTER TABLE ...
DROP TABLE ...
DROP VIEW ...
DROP FUNCTION ...
```

**Comandos PERMITIDOS:**

```bash
supabase migration new {nome}   # Via CLI oficial
supabase db push                # Deploy de migration
pg_dump ...                     # Backup/export
SELECT / INSERT / UPDATE        # DML é permitido
```

---

### 🔴 Antes de GIT PUSH

**Gatilho:** `run_command` com `git push`

**Verificação:**

- [ ] O agente ativo é `@devops` (Gage)?

**Se NÃO** → **BLOQUEAR.** Delegar:

```
→ @devops *push
```

**Se SIM** → Executar quality gates antes de push:

```bash
npm run lint         # ✅ deve passar
npm run typecheck    # ✅ deve passar
npm test             # ✅ deve passar
```

---

### 🟡 Antes de CRIAR ou REMOVER Git Worktrees

**Gatilho:** `run_command` com `git worktree add` ou `git worktree remove`

**Verificação obrigatória:**

- [ ] O agente ativo é `@devops` (Gage)?

Se NÃO → **BLOQUEAR.** Worktrees devem ser gerenciados apenas por @devops:

```
→ @devops *create-worktree {branch}
→ @devops *remove-worktree {branch}
→ @devops *list-worktrees
```

Se SIM → Seguir protocolo do workflow `auto-worktree.md`.

---

### 🟡 Antes de usar `mcp_stitch_*`

**Gatilho:** Qualquer invocação de ferramentas Stitch MCP

**Verificação:**

- [ ] O contexto é de Design System ou UI? (workflows: `design-system-build.md`, `greenfield-ui.md`, `brownfield-ui.md`)

Se SIM → Prosseguir normalmente.
Se NÃO → Alertar: use Stitch MCP apenas no contexto de workflows de UI/Design System.

Verificar se o tipo de documento está no path correto:

| Tipo de Documento   | Path Correto                                        |
| ------------------- | --------------------------------------------------- |
| Sessions / handoffs | `docs/sessions/YYYY-MM/`                            |
| Arquitetura         | `docs/architecture/`                                |
| Guias               | `docs/guides/`                                      |
| Stories             | `docs/stories/active/` ou `docs/stories/completed/` |
| Planos aprovados    | `docs/approved-plans/`                              |

Se o documento parece estar no path errado → alertar antes de salvar.

---

### 🟡 Formato de Slugs e IDs

**Regra:** Todos os slugs e IDs devem ser `snake_case`

```
Padrão válido: ^[a-z0-9]+(_[a-z0-9]+)*$
```

| Exemplo              | Status                  |
| -------------------- | ----------------------- |
| `jose_carlos_amorim` | ✅ VÁLIDO               |
| `workflow_execution` | ✅ VÁLIDO               |
| `jose-carlos-amorim` | ❌ INVÁLIDO (hífen)     |
| `JoseAmorim`         | ❌ INVÁLIDO (camelCase) |
| `jose.carlos`        | ❌ INVÁLIDO (ponto)     |

---

### 🔵 Leitura Parcial de Arquivos Protegidos

**Arquivos que NUNCA devem ser lidos parcialmente** (sem StartLine/EndLine quando tomando decisões):

- `.antigravity/ANTIGRAVITY.md`
- `.antigravity/rules/*.md`
- `.aios-core/development/agents/*.md`
- `supabase/docs/SCHEMA.md`
- `package.json`, `tsconfig.json`

**Regra:** Ler o arquivo completo quando tomando decisões sobre estes arquivos.

---

## Validação Manual com Scripts Originais

Os scripts Python do `.claude/hooks/` ainda existem e podem ser usados para validação manual:

```bash
# Validar architecture-first
echo '{"tool_name": "Write", "tool_input": {"file_path": "supabase/functions/minha-funcao/index.ts"}}' \
  | python3 .claude/hooks/enforce-architecture-first.py

# Validar mind-clone governance
echo '{"tool_name": "Write", "tool_input": {"file_path": "squads/meu-squad/agents/gary-halbert.md"}}' \
  | python3 .claude/hooks/mind-clone-governance.py

# Validar slug
echo '{"tool_name": "Bash", "tool_input": {"command": "criar slug jose-carlos"}}' \
  | python3 .claude/hooks/slug-validation.py
```

---

## Referência

| Conceito              | Arquivo                                 |
| --------------------- | --------------------------------------- |
| Regra completa        | `.antigravity/rules/governance.md`      |
| Autoridade de agentes | `.antigravity/rules/agent-authority.md` |
| Documento master      | `.antigravity/ANTIGRAVITY.md`           |
