# PRD — Correção de Gaps de Integração AntiGravity

> **Versão:** 1.0  
> **Data:** 2026-02-26  
> **Prioridade:** Alta (G1, G2) / Média (G3, G4, G5)  
> **Status:** 🔴 EM ABERTO  
> **Responsável:** @pm, @dev, @devops  
> **Task de Execução:** `task-gaps-antigravity.md` (nesta pasta)

---

## 1. Contexto e Origem

Durante a revisão de workflows da sessão `revWorkFlows` (2026-02-25/26), foi identificado que o ambiente AntiGravity atingiu **paridade funcional** com o Claude Code para workflows e agentes. No entanto, a **camada de instalação e documentação de onboarding** ainda referencia Claude Code como default e não contempla plenamente o fluxo de uso via AntiGravity.

**Impacto atual:** Um usuário que clona o repositório e segue o `user-guide.md` é direcionado para Claude Code — não descobre o AntiGravity.

---

## 2. Gaps Identificados

### GAP-01 — `user-guide.md` sem seção AntiGravity

**Prioridade:** 🔴 Alta  
**Arquivo afetado:** `docs/pt/guides/user-guide.md` + `docs/en/guides/user-guide.md`

**Situação atual:**

- O guia menciona apenas Claude Code e Cursor como IDEs
- Seção de Configuração lista `ai.provider: anthropic` como único exemplo
- `Integração com IDE` referencia `.claude/` exclusivamente
- Seção "Por que AIOS" não menciona AntiGravity como opção

**Situação desejada:**

- Nova seção "Usando com AntiGravity" após seção de Instalação
- Tabela comparativa atualizada com AntiGravity como opção
- `ai.provider: gemini` documentado
- Link para `docs/pt/antigravity/getting-started.md`

---

### GAP-02 — `npx aios-core init` não copia `.antigravity/`

**Prioridade:** 🔴 Alta  
**Arquivo afetado:** `package.json` → campo `files` + scripts de `init` em `bin/`

**Situação atual:**

```json
"files": [
  "bin/",
  "scripts/",
  "packages/",
  ".aios-core/",
  ".claude/CLAUDE.md",
  ".claude/rules/",
  ".claude/hooks/",
  ...
]
```

O campo `files` do `package.json` **não inclui** `.antigravity/`. Isso significa que ao publicar o pacote npm e instalar via `npx aios-core init`, a pasta `.antigravity/` não é distribuída.

**Análise do `bin/aios.js`:** O comando `init` provavelmente copia arquivos do pacote instalado para o projeto alvo. Sem `.antigravity/` no `files`, ela não chega ao projeto do usuário.

**Situação desejada:**

```json
"files": [
  "bin/",
  "scripts/",
  "packages/",
  ".aios-core/",
  ".claude/CLAUDE.md",
  ".claude/rules/",
  ".claude/hooks/",
  ".antigravity/ANTIGRAVITY.md",
  ".antigravity/agents/",
  ".antigravity/rules/",
  ".antigravity/skills/",
  ".antigravity/workflows/",
  ".antigravity/templates/",
  ...
]
```

---

### GAP-03 — `npm run sync:ide` não inclui AntiGravity por padrão

**Prioridade:** 🟡 Média  
**Arquivo afetado:** `package.json` → script `sync:ide` + `lint-staged`

**Situação atual:**

```json
"sync:ide": "node .aios-core/infrastructure/scripts/ide-sync/index.js sync",
"sync:ide:antigravity": "node .aios-core/infrastructure/scripts/ide-sync/index.js sync --ide antigravity"
```

- O comando `sync:ide:antigravity` **já existe** (linha 48 do `package.json`) — isso é positivo!
- Porém, `sync:ide` (sem flag) sincroniza para todas as IDEs configuradas por padrão, que pode ou não incluir AntiGravity dependendo do script de sincronização
- O `lint-staged` usa `npm run sync:ide` ao editar agentes — precisa verificar se AntiGravity está incluso

**Análise necessária:** Verificar o script `ide-sync/index.js` para entender quais IDEs são sincronizadas no modo padrão.

**Situação desejada:**

- `sync:ide` padrão inclui AntiGravity entre as IDEs sincronizadas
- `lint-staged` ao editar `.aios-core/development/agents/*.md` também sincroniza para `.antigravity/agents/`
- Documentação em `development-setup.md` menciona `sync:ide:antigravity` como opção

---

### GAP-04 — `gemini` não documentado como `ai.provider`

**Prioridade:** 🟡 Média  
**Arquivos afetados:** `docs/pt/guides/user-guide.md`, `docs/en/guides/user-guide.md`, `docs/pt/guides/development-setup.md`

**Situação atual:**

```yaml
# aios.config.yaml — exemplo atual
ai:
  provider: anthropic
  model: claude-3-opus
```

- Apenas Anthropic e OpenAI são documentados como provedores de IA
- O AntiGravity usa Gemini, mas a configuração não instrui o usuário sobre isso
- `.env` de exemplo não menciona `GEMINI_API_KEY` ou `GOOGLE_API_KEY`

**Situação desejada:**

```yaml
# Exemplo para Claude Code
ai:
  provider: anthropic
  model: claude-3-opus

# Exemplo para AntiGravity (Gemini)
ai:
  provider: gemini
  model: gemini-2.0-flash
```

- Documentar `GEMINI_API_KEY` no `.env` de exemplo
- Adicionar seção de variáveis de ambiente por IDE

---

### GAP-05 — Guia específico `antigravity-guide.md` não existe

**Prioridade:** 🟡 Média  
**Arquivo a criar:** `docs/pt/guides/antigravity-guide.md` + `docs/en/guides/antigravity-guide.md`

**Situação atual:**

- O `user-guide.md` é orientado para Claude Code
- O `docs/pt/antigravity/` contém documentation técnica de referência (agentes, rules, etc.)
- **Não existe** um guia prático e sequencial do ponto de vista do usuário que escolheu AntiGravity

**Diferença de propósito:**
| Documento | Propósito |
|---|---|
| `user-guide.md` | Guia geral AIOS (Claude Code como default) |
| `docs/pt/antigravity/*.md` | Referência técnica do ambiente .antigravity/ |
| `antigravity-guide.md` _(a criar)_ | Guia prático step-by-step para usuário AntiGravity |

**Situação desejada:** Guia com:

1. Por que AntiGravity? (vantagens vs Claude Code)
2. Instalação/ativação (extensão Gemini Code Assist)
3. Configuração inicial (ANTIGRAVITY.md, GEMINI_API_KEY)
4. Primeiro projeto (greenfield-fullstack passo a passo)
5. Primeiro agente (@dev exemplo real)
6. Ferramentas exclusivas (Stitch MCP, generate_image, browser_subagent)
7. Troubleshooting específico

---

## 3. Dependências entre Gaps

```
GAP-02 (package.json/files)
  └── Depende de: validar ide-sync/index.js (pré-análise de GAP-03)
  └── Bloqueia: qualquer usuário que instala via npx

GAP-01 (user-guide.md)
  └── Referencia: GAP-04 (gemini config) e GAP-05 (antigravity-guide.md)
  └── Link para: docs/pt/antigravity/getting-started.md (já existe ✅)

GAP-05 (antigravity-guide.md)
  └── Consome: GAP-04 (config gemini)
  └── Complementa: GAP-01 (user-guide)

GAP-03 (sync:ide)
  └── Requer: leitura de ide-sync/index.js antes de alterar
  └── Independente dos outros gaps
```

---

## 4. Critérios de Aceitação (DoD)

### GAP-01

- [ ] `user-guide.md` (PT + EN) tem seção "Usando com AntiGravity"
- [ ] Tabela de IDEs inclui AntiGravity com link para guia
- [ ] `ai.provider: gemini` está documentado
- [ ] Links para `antigravity-guide.md` funcionam

### GAP-02

- [ ] Campo `files` em `package.json` inclui `.antigravity/` (pastas essenciais)
- [ ] `npx aios-core install` copia `.antigravity/` para projeto do usuário
- [ ] Testar: criar projeto teste com `npx aios-core init teste-projeto` e verificar `.antigravity/` presente

### GAP-03

- [ ] `npm run sync:ide` padrão sincroniza para AntiGravity
- [ ] OU documentação indica explicitamente: "Use `sync:ide:antigravity` para o AntiGravity"
- [ ] `lint-staged` ao editar agentes cobre `.antigravity/agents/`

### GAP-04

- [ ] `user-guide.md` (PT + EN) documenta `gemini` como provider
- [ ] `development-setup.md` lista `GEMINI_API_KEY` no `.env` de exemplo
- [ ] Seção de variáveis de ambiente é separada por IDE/provider

### GAP-05

- [ ] `docs/pt/guides/antigravity-guide.md` criado (PT)
- [ ] `docs/en/guides/antigravity-guide.md` criado (EN)
- [ ] Guia é referenciado no `user-guide.md` e no índice de guias (`README.md`)
- [ ] Guia cobre: instalação → configuração → primeiro ciclo SDC → ferramentas exclusivas

---

## 5. Estimativa de Esforço

| Gap    | Complexidade | Esforço Estimado    | Agente                       |
| ------ | ------------ | ------------------- | ---------------------------- |
| GAP-01 | Média        | 1-2h                | `@dev`                       |
| GAP-02 | Alta         | 2-4h                | `@dev` + validação `@devops` |
| GAP-03 | Média        | 1-2h (após análise) | `@dev`                       |
| GAP-04 | Baixa        | 30min               | `@dev`                       |
| GAP-05 | Alta         | 3-5h                | `@pm` + `@dev`               |

**Total estimado:** 8-14h de trabalho focado

---

## 6. Riscos

| Risco                                                                                  | Probabilidade | Impacto | Mitigação                                   |
| -------------------------------------------------------------------------------------- | ------------- | ------- | ------------------------------------------- |
| `ide-sync/index.js` não suporta `.antigravity/` corretamente                           | Média         | Alto    | Investigar script antes de GAP-02           |
| `npx aios-core init` usa lógica customizada além de `files` que ignora `.antigravity/` | Média         | Alto    | Auditar `bin/aios.js` (init command)        |
| Adição de `.antigravity/` ao `files` aumenta tamanho do pacote npm                     | Baixa         | Médio   | Verificar `.npmignore` ou filtros seletivos |
| `user-guide.md` (EN) pode ter estrutura diferente da versão PT                         | Baixa         | Baixo   | Revisar ambas as versões                    |

---

## 7. Referências

| Arquivo                                               | Relevância                                                 |
| ----------------------------------------------------- | ---------------------------------------------------------- |
| `package.json`                                        | GAP-02/03 — campo `files` e scripts `sync:ide:antigravity` |
| `docs/pt/guides/user-guide.md`                        | GAP-01/04 — seções a atualizar                             |
| `docs/pt/antigravity/getting-started.md`              | Já atualizado ✅ — usar como referência para GAP-05        |
| `.aios-core/infrastructure/scripts/ide-sync/index.js` | GAP-03 — auditar antes de alterar                          |
| `bin/aios.js`                                         | GAP-02 — auditar comando `init`                            |
| `.antigravity/ANTIGRAVITY.md`                         | GAP-05 — fonte de verdade do ambiente                      |
