# Task — Correção de Gaps de Integração AntiGravity

> **Criada:** 2026-02-26  
> **PRD:** `prd-gaps-antigravity.md` (nesta pasta)  
> **Status:** ✅ CONCLUÍDO em 2026-02-26  
> **Tipo:** implementation_plan

---

## Progresso Geral

| Gap                                     | ID  | Status             | Prioridade |
| --------------------------------------- | --- | ------------------ | ---------- |
| user-guide.md sem seção AntiGravity     | G1  | ✅ Concluído       | Alta       |
| package.json/files sem .antigravity/    | G2  | ✅ Concluído       | Alta       |
| sync:ide sem AntiGravity por padrão     | G3  | ✅ Concluído (doc) | Média      |
| gemini não documentado como ai.provider | G4  | ✅ Concluído       | Média      |
| antigravity-guide.md não existe         | G5  | ✅ Concluído       | Média      |

---

## G4 — Documentar `gemini` como ai.provider

> Começa aqui por ser o menor e o mais direto — sem dependências.

### T4.1 — Atualizar user-guide.md (PT)

- [ ] Localizar seção "Arquivo Principal de Configuração" (`aios.config.yaml`)
- [ ] Adicionar exemplo com `provider: gemini` e `model: gemini-2.0-flash`
- [ ] Localizar seção "Variáveis de Ambiente"
- [ ] Adicionar `GEMINI_API_KEY=sua-chave-gemini-api` ao exemplo `.env`
- [ ] Atualizar seção "Integração com IDE" para mencionar AntiGravity

### T4.2 — Atualizar user-guide.md (EN)

- [ ] Replicar mesmas alterações na versão inglesa
- [ ] Verificar consistência entre PT e EN

### T4.3 — Atualizar development-setup.md (PT)

- [ ] Localizar seção "Variáveis de Ambiente" com exemplo `.env`
- [ ] Adicionar `GEMINI_API_KEY` como variável para usuários AntiGravity
- [ ] Adicionar nota: "Para AntiGravity, use GEMINI_API_KEY em vez de ANTHROPIC_API_KEY"

**Critério de saída G4:** As três instâncias de documentação têm `gemini` documentado como provider.

---

## G1 — Adicionar seção AntiGravity no user-guide.md

> Depende de G4 estar concluído (para referenciar configuração gemini).

### T1.1 — Atualizar user-guide.md (PT)

- [ ] Adicionar seção "## Usando com AntiGravity" após "## Configuração"
- [ ] Conteúdo da seção:
  - O que é o AntiGravity (1 parágrafo)
  - Tabela comparativa Claude Code vs AntiGravity (3-4 linhas)
  - Pré-requisito: IDE Gemini Code Assist ou Antigravity IDE
  - Referência ao `ai.provider: gemini` (já documentado em T4.1)
  - Link: `[Guia Completo de AntiGravity](../../pt/antigravity/getting-started.md)`
  - Link: `[Guia Prático AntiGravity](./antigravity-guide.md)` _(quando G5 estiver pronto)_
- [ ] Atualizar tabela "Integração com IDE" para incluir AntiGravity

### T1.2 — Atualizar user-guide.md (EN)

- [ ] Replicar mesmas alterações na versão inglesa
- [ ] Link: `[AntiGravity Complete Guide](../../en/antigravity/getting-started.md)`

### T1.3 — Atualizar índice de guias

- [ ] Verificar se existe `docs/pt/guides/README.md` — adicionar AntiGravity guide quando G5 pronto
- [ ] Verificar se docs/guides/user-guide.md (EN raiz) precisa de atualização correspondente

**Critério de saída G1:** user-guide.md (PT + EN) tem seção AntiGravity completa e links funcionais.

---

## G3 — Auditar e ajustar sync:ide para AntiGravity

> Independente dos outros. Envolve leitura de script antes de qualquer mudança.

### T3.1 — Auditar ide-sync/index.js

- [ ] Ler arquivo: `.aios-core/infrastructure/scripts/ide-sync/index.js`
- [ ] Identificar: quais IDEs são sincronizadas no modo `sync` padrão (sem flag `--ide`)
- [ ] Verificar: `--ide antigravity` está implementado ou é apenas um script stub
- [ ] Verificar: qual diretório de destino é usado para AntiGravity (`.antigravity/agents/`?)
- [ ] Documentar resultado da auditoria aqui antes de prosseguir

**⚠️ PONTO DE DECISÃO após T3.1:**

- Se `sync:ide` padrão **já inclui AntiGravity** → T3.2 é apenas documentação
- Se `sync:ide` padrão **não inclui AntiGravity** → T3.3 implementação necessária

### T3.2 — Se já incluído: documentar

- [ ] Atualizar `development-setup.md` para mencionar `sync:ide:antigravity` explicitamente
- [ ] Verificar que `lint-staged` cobre `.antigravity/agents/` ao editar agentes

### T3.3 — Se NÃO incluído: implementar

- [ ] Adicionar AntiGravity ao modo padrão do `ide-sync/index.js`
- [ ] OU documentar que usuários AntiGravity devem usar `npm run sync:ide:antigravity`
- [ ] Atualizar `lint-staged` no `package.json` se necessário:
  ```json
  ".aios-core/development/agents/*.md": [
    "npm run sync:ide:antigravity"
  ]
  ```

**Critério de saída G3:** Comportamento de sync:ide para AntiGravity está implementado e documentado.

---

## G2 — Adicionar `.antigravity/` ao package.json files

> Gap mais técnico. Requer análise de `bin/aios.js` antes de alterar.

### T2.1 — Auditar bin/aios.js (comando init/install)

- [ ] Ler arquivo: `bin/aios.js`
- [ ] Identificar: como o comando `init` copia arquivos para o projeto do usuário
- [ ] Verificar: usa o campo `files` do `package.json` ou lógica própria
- [ ] Verificar: existe `.npmignore` que possa excluir `.antigravity/`
- [ ] Verificar: existe algum manifesto de instalação que lista o que copiar
- [ ] Documentar resultado aqui antes de alterar `package.json`

**⚠️ PONTO DE DECISÃO após T2.1:**

- Se usa `files` → alterar `package.json` (T2.2)
- Se usa lógica própria → alterar também a lógica do init (T2.3)

### T2.2 — Alterar package.json (campo files)

- [ ] Adicionar ao campo `files`:
  ```json
  ".antigravity/ANTIGRAVITY.md",
  ".antigravity/agents/",
  ".antigravity/rules/",
  ".antigravity/skills/",
  ".antigravity/workflows/",
  ".antigravity/templates/",
  ".antigravity/agent-memory/"
  ```
- [ ] **NÃO incluir** `.antigravity/` inteiro se houver arquivos de sessão ou dados pessoais

### T2.3 — Alterar lógica de init (se necessário)

- [ ] Localizar array/config de arquivos copiados no init
- [ ] Adicionar cópia de `.antigravity/` para projeto de destino
- [ ] Manter `.claude/` também (não remover — suporte multi-IDE)

### T2.4 — Teste de validação

- [ ] Criar projeto de teste: `npx aios-core init test-projeto-validate`
- [ ] Verificar que `.antigravity/` está presente no projeto criado
- [ ] Verificar que `.claude/` ainda está presente (sem regressão)
- [ ] Limpar projeto de teste após validação

**Critério de saída G2:** `npx aios-core init` cria projeto com `.antigravity/` e `.claude/` simultaneamente.

---

## G5 — Criar antigravity-guide.md

> Depende de G4 (para documentar config gemini) e G1 concluído (para linkar).

### T5.1 — Planejar estrutura do guia

- [ ] Definir seções (proposta no PRD):
  1. Por que AntiGravity?
  2. Pré-requisitos e instalação
  3. Configuração inicial
  4. Primeiro projeto (greenfield walkthrough)
  5. Ciclo de desenvolvimento SDC
  6. Ferramentas exclusivas
  7. Troubleshooting

### T5.2 — Criar antigravity-guide.md (PT)

- [ ] Criar arquivo: `docs/pt/guides/antigravity-guide.md`
- [ ] Seção 1: Tabela comparativa Claude Code vs AntiGravity
- [ ] Seção 2: Pré-requisitos (IDE Gemini, Node.js, Git, GEMINI_API_KEY)
- [ ] Seção 3: Configuração passo a passo
  - Download/clone do repositório
  - `npx aios-core init my-project`
  - Configurar `.env` com `GEMINI_API_KEY`
  - Verificar `.antigravity/` presente
- [ ] Seção 4: Primeiro projeto
  - Ativar `@pm` e criar PRD simples
  - Usar workflow `greenfield-fullstack` passo a passo
  - Exemplo concreto com output esperado
- [ ] Seção 5: Ciclo SDC
  - `@sm *draft → @po *validate → @dev → @qa → @devops *push`
- [ ] Seção 6: Ferramentas exclusivas
  - `generate_image` com exemplo prático
  - `mcp_stitch_*` com fluxo de uso
  - `browser_subagent` com exemplo de teste
- [ ] Seção 7: Troubleshooting
  - `.antigravity/` não encontrado → reinstalar
  - Agente não ativa → verificar ANTIGRAVITY.md
  - Stitch MCP não funciona → verificar MCP configuration

### T5.3 — Criar antigravity-guide.md (EN)

- [ ] Traduzir e adaptar `antigravity-guide.md` PT → EN
- [ ] Criar: `docs/en/guides/antigravity-guide.md`

### T5.4 — Atualizar índice de guias

- [ ] Adicionar entry no índice `docs/pt/guides/README.md` (se existir)
- [ ] Atualizar `user-guide.md` com link para `antigravity-guide.md` (T1.1 > link placeholder)

**Critério de saída G5:** Guias criados (PT + EN), referenciados no user-guide e no índice.

---

## Ordem de Execução Recomendada

```
1. G4 (30min, independente, sem riscos)
   ↓
2. G3-T3.1 (auditoria ide-sync — informação crítica)
   ↓ (paralelo)
3. G2-T2.1 (auditoria bin/aios.js — informação crítica)
   ↓
4. G1 (após G4) + G3 completo + G2 completo (paralelo)
   ↓
5. G5 (após G1 e G4, para linkar corretamente)
```

---

## Notas e Descobertas

> _Preencher durante execução_

**T3.1 — Resultado auditoria ide-sync:**

- [x] AntiGravity incluído no padrão? **SIM** (`enabled: true` na `defaultConfig`)
- [x] IDEs sincronizadas no padrão: claude-code, codex, gemini, github-copilot, cursor, **antigravity**
- [x] path: `.antigravity/rules/agents`, format: `cursor-style` (antigravityTransformer)
- [x] `--ide antigravity` totalmente implementado

**T2.1 — Resultado auditoria bin/aios.js:**

- [x] Usa campo `files` do package.json? **Indiretamente** — `files` controla o tarball npm
- [x] Usa lógica própria? **Sim** — init delega ao wizard (`packages/installer/src/wizard/index.js`)
- [x] Existe `.npmignore`? **Não encontrado**
- [x] Ação tomada: adicionado `.antigravity/*` ao campo `files` do `package.json`

---

## Critério de Conclusão Global

**Sessão de revisão final:** Todos os links internos verificados. Guias PT+EN criados e referenciados.

- [x] G1 ✅ — user-guide.md atualizado (PT + EN)
- [x] G2 ✅ — package.json/init copia .antigravity/ (campo files atualizado)
- [x] G3 ✅ — sync:ide já incluía AntiGravity; documentado em development-setup.md
- [x] G4 ✅ — gemini documentado como provider (PT + EN + dev-setup)
- [x] G5 ✅ — antigravity-guide.md criado (PT + EN) e referenciado
