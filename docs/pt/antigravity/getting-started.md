# Getting Started — Ambiente Antigravity

> **Versão:** 2.0 | **Atualizado:** 2026-02-26

Guia completo para começar a usar o AIOS no Antigravity (Gemini IDE) — do zero ao primeiro ciclo de desenvolvimento.

---

## Pré-requisitos

- **Node.js** 18+ e **npm** 8+
- **Git** instalado
- IDE **Antigravity** (Google Gemini Code Assist ou Gemini IDE)
- AIOS instalado no projeto (ver instalação abaixo)

---

## 1. Instalação do AIOS

### Projeto Novo

```bash
# Cria estrutura completa do projeto com AIOS
npx aios-core init my-project
cd my-project
```

O comando `init` cria automaticamente:

- `.antigravity/` — configuração do Antigravity (agentes, rules, skills, workflows)
- `.aios-core/` — framework central (tasks, templates, checklists)
- `docs/` — estrutura de documentação
- `squads/` — packs de agentes especializados

### Projeto Existente

```bash
# Adiciona AIOS a projeto já existente
cd existing-project
npx aios-core install
```

### Verificar instalação

```bash
npx aios-core doctor    # Diagnóstico completo
npx aios-core info      # Versão e status
```

---

## 2. Entendendo o documento master

Toda sessão no Antigravity começa com o `ANTIGRAVITY.md` sendo lido automaticamente. Ele define:

- **Constitution** — 6 princípios fundamentais (CLI First, Agent Authority, etc.)
- **Idioma** — PT-BR por padrão
- **Sistema de agentes** — quem faz o quê
- **Guia de seleção de workflows** — qual workflow usar em cada situação
- **Governança** — verificações obrigatórias antes de operações críticas

> Arquivo: [`.antigravity/ANTIGRAVITY.md`](../../../../.antigravity/ANTIGRAVITY.md)

---

## 3. Escolhendo o Workflow Certo

Antes de invocar um agente, identifique o workflow para sua situação:

### Projeto novo

```
"Quero criar uma aplicação fullstack do zero"
  → Antigravity usa: greenfield-fullstack.md
  → Inicia: @analyst → @pm → @ux → @architect → @po → @dev → @qa → @devops
```

```
"Quero criar só um backend/API"
  → greenfield-service.md

"Quero criar só um frontend/landing page"
  → greenfield-ui.md  (+ design com Stitch MCP)
```

### Projeto existente

```
"Nunca trabalhei neste projeto — preciso entender"
  → brownfield-discovery.md
  → @architect mapeia → @data-engineer audita DB → @ux audita frontend

"Já conheço — quero adicionar feature fullstack"
  → brownfield-fullstack.md

"Quero adicionar endpoint ao backend existente"
  → brownfield-service.md

"Quero adicionar página/componente ao frontend"
  → brownfield-ui.md
```

### Durante o desenvolvimento

```
"Tenho uma ideia → quero criar backlog completo"
  → spec-pipeline.md

"Tenho épico pronto → quero executar todas as stories"
  → epic-orchestration.md

"Tenho uma story → quero implementar"
  → story-development-cycle.md (SDC)

"QA reprovou → preciso corrigir e re-validar"
  → qa-loop.md  (máximo 5 iterações, escalação automática)
```

> **Índice completo:** [`.antigravity/workflows/README.md`](../../../../.antigravity/workflows/README.md)

---

## 4. Ativando Agentes

Use o prefixo `@` para invocar qualquer agente:

```
@dev           → Dex, desenvolvedor principal
@qa            → Quinn, testes e qualidade
@architect     → Aria, arquitetura de sistema
@pm            → Kai, product management
@po            → Nova, product owner e stories
@sm            → River, scrum master
@analyst       → Zara, pesquisa e análise
@data-engineer → Dara, banco de dados e schema
@ux            → Uma, UX/UI design
@devops        → Gage, CI/CD e git push
@brad-frost    → Brad Frost, Design System (Atomic Design)
@squad-chief   → Squad Architect 🎨
```

**Exemplo:**

```
@architect crie a arquitetura para o serviço de pagamentos
```

```
@dev implemente o endpoint de autenticação conforme a story 3.2
```

---

## 5. Comandos de Agente (`*`)

Dentro de um contexto de agente, use `*` para executar ações específicas:

| Comando              | O que faz                              |
| -------------------- | -------------------------------------- |
| `*help`              | Lista todos os comandos disponíveis    |
| `*create-story`      | Cria nova story de desenvolvimento     |
| `*task {nome}`       | Executa task específica                |
| `*qa-loop {storyId}` | Inicia ciclo iterativo de correção QA  |
| `*push`              | (exclusivo @devops) — push para remote |
| `*status`            | Mostra progresso do épico ou workflow  |
| `*exit`              | Sai do modo agente                     |

---

## 6. Ciclo de Desenvolvimento Completo (SDC)

O **Story Development Cycle** é o fluxo padrão para implementar qualquer feature:

```
1. @sm *draft         → Rascunha a story com contexto do épico
2. @po *validate      → Valida acceptance criteria (GO / NO-GO)
3. @dev *develop      → Implementa (modo Interactive ou YOLO)
4. @qa *qa-gate       → Quality gate — PASS / CONCERNS / FAIL
5. @devops *push      → Push para remote (autoridade exclusiva)
```

**Se o QA reprovar** → `qa-loop.md` assume automaticamente (máximo 5 iterações).

> ⚠️ **Regra inviolável:** Apenas `@devops` pode executar `git push`. Todos os outros agentes devem delegar.

---

## 7. Governança Automática

O Antigravity verifica proativamente antes de cada operação crítica:

| Operação                          | Verificação obrigatória               |
| --------------------------------- | ------------------------------------- |
| Escrever em `supabase/functions/` | Documentação de arquitetura aprovada? |
| Criar `squads/*/agents/*.md`      | DNA extraído para mind-clones?        |
| Executar SQL DDL                  | Usar `supabase migration` CLI?        |
| `git push`                        | Agente ativo é `@devops`?             |
| `git worktree add/remove`         | Agente ativo é `@devops`?             |
| Usar `mcp_stitch_*`               | Contexto de UI/Design System?         |
| Slugs/IDs                         | Formato `snake_case` válido?          |

Detalhes: [`.antigravity/rules/governance.md`](../../../../.antigravity/rules/governance.md)

---

## 8. Ferramentas Exclusivas do Antigravity

Capacidades que o Claude Code **não possui**:

### Geração de Imagens

```
@ux crie um mockup da tela de login do produto
→ Usa: generate_image() — retorna imagem real
```

### Design de UI com Stitch MCP

```
@ux gere as telas principais do dashboard baseadas na front-end-spec
→ Usa: mcp_stitch_generate_screen_from_text()
→ Cria wireframes de alta fidelidade sem ferramentas externas
```

### Automação de Browser

```
@qa valide visualmente o componente de login em browser
→ Usa: browser_subagent()
→ Grava vídeo WebP automático do fluxo testado
```

---

## 9. Criando um Squad Especializado

```
@squad-chief quero um squad de marketing digital
```

O `@squad-chief` vai:

1. Pesquisar as mentes de elite do domínio
2. Extrair DNA de comportamento e pensamento de cada especialista
3. Criar agentes baseados nas mentes reais
4. Gerar toda a estrutura do squad em `squads/`

> Workflow: [`.antigravity/workflows/create-squad.md`](../../../../.antigravity/workflows/create-squad.md)

---

## 10. Worktrees — Desenvolvimento Paralelo

Para trabalhar em múltiplas features simultaneamente:

```
@devops, cria um worktree para a feature de pagamentos
→ Workflow: auto-worktree.md
→ Cria branch isolado: feat/pagamentos
→ Desenvolvimento ocorre sem afetar o main
```

---

## Próximos Passos

- [Sistema de Agentes](./agents/overview.md) — Hierarquia completa dos 28+ agentes
- [Rules e Governance](./rules/overview.md) — Regras de comportamento e segurança
- [Workflows](./workflows/overview.md) — Os 14 workflows e quando usar cada um
- [Mapeamento de Ferramentas](./tools/tool-mapping.md) — Todas as ferramentas disponíveis
- [Templates](./templates/overview.md) — 16 templates prontos para usar
- [Migração do Claude](./migration/from-claude.md) — Diferenças e adaptações

---

_Synkra AIOS — Antigravity Getting Started v2.0_
_Atualizado em 2026-02-26_
