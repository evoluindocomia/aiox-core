# Guia Prático AntiGravity

> **PT-BR** | [EN](../../../guides/antigravity-guide.md)

---

Guia step-by-step completo para usar o AIOS com o ambiente **AntiGravity** + Gemini Code Assist.

**Versão:** 1.0.0  
**Criado em:** 2026-02-26  
**Referência técnica:** [Getting Started AntiGravity](../../pt/antigravity/getting-started.md)

---

## 1. Por que AntiGravity?

O **AntiGravity** é o ambiente nativo do AIOS para uso com **Gemini Code Assist** da Google. Ele oferece paridade funcional completa com o Claude Code e adiciona ferramentas exclusivas do ecossistema Gemini.

| Característica       | Claude Code         | AntiGravity           |
| -------------------- | ------------------- | --------------------- |
| IDE                  | Claude Code         | Gemini Code Assist    |
| Provider de IA       | `anthropic`         | `gemini`              |
| Chave de API         | `ANTHROPIC_API_KEY` | `GEMINI_API_KEY`      |
| Diretório de config  | `.claude/`          | `.antigravity/`       |
| Geração de imagem    | ✗                   | ✅ `generate_image`   |
| Design de UI         | ✗                   | ✅ Stitch MCP         |
| Automação de browser | ✗                   | ✅ `browser_subagent` |
| Agentes AIOS         | 11 agentes          | 11 agentes (mesmos)   |
| Workflows            | Completo            | Completo (paridade)   |
| Squads               | Completo            | Completo (paridade)   |

> **Resumo:** Se você usa Gemini / Google AI Studio ou prefere o ecossistema Google, AntiGravity é a escolha certa.

---

## 2. Pré-requisitos e Instalação

### O que você precisa

| Item               | Versão           | Obter em                                                                                                     |
| ------------------ | ---------------- | ------------------------------------------------------------------------------------------------------------ |
| Node.js            | 18.0.0+          | [nodejs.org](https://nodejs.org)                                                                             |
| npm                | 9.0.0+           | (incluso no Node.js)                                                                                         |
| Git                | 2.30+            | [git-scm.com](https://git-scm.com)                                                                           |
| Gemini Code Assist | Extensão VS Code | [marketplace.visualstudio.com](https://marketplace.visualstudio.com/items?itemName=Google.google-cloud-code) |
| Conta Google       | —                | Lógin via extensão                                                                                           |

> **Sem chave de API!** O Gemini Code Assist autentica pela sua conta Google — você não precisa de `GEMINI_API_KEY` para o uso padrão via IDE.

### Instalando a extensão

1. No VS Code, abra a aba Extensões (`Ctrl+Shift+X`)
2. Pesquise por `Gemini Code Assist`
3. Clique em **Instalar**
4. Faça login com sua conta Google quando solicitado
5. Pronto — o chat já está disponível!

### Instalando o AIOS

```bash
# Novo projeto (Greenfield)
npx aios-core init my-project

# Projeto existente (Brownfield)
cd existing-project
npx aios-core install
```

---

## 3. Configuração Inicial

### Passo 1: Configurar variáveis de ambiente (opcional)

Para o uso padrão via **Gemini Code Assist**, não é necessário configurar chaves de API — a autenticação é feita pela sua conta Google através da extensão.

Se você precisar de acesso programático direto à API do Gemini (ex: scripts, automações):

```bash
# Opcional — apenas para chamadas programáticas à API
GEMINI_API_KEY=sua-chave-gemini
```

### Passo 2: Verificar `.antigravity/` presente

```bash
ls .antigravity/
# Esperado: ANTIGRAVITY.md  agents/  rules/  skills/  workflows/  templates/
```

> Se `.antigravity/` não existir, execute `npx aios-core install` novamente.

### Passo 3: Configurar `aios.config.yaml`

```yaml
# .aios-core/core/config/aios.config.yaml
ai:
  provider: gemini
  model: gemini-2.0-flash
```

### Passo 4: Sincronizar agentes para AntiGravity

```bash
# Sincronizar agentes para todas as IDEs (inclui AntiGravity por padrão)
npm run sync:ide

# Ou apenas para AntiGravity
npm run sync:ide:antigravity

# Validar
npm run validate:antigravity-sync
```

### Passo 5: Verificar instalação

```bash
npx aios-core doctor
```

---

## 4. Primeiro Projeto

Veja como criar um projeto do zero usando o workflow `greenfield-fullstack`.

### Passo 1: Ativar o PM e criar o PRD

No chat do Gemini Code Assist, digite:

```
@pm
*create-prd
```

O agente **Kai** (`@pm`) guiará você pelo processo de criação do PRD.

### Passo 2: Executar o workflow Greenfield

```
@sm
*draft
```

O agente **River** (`@sm`) inicia o workflow `greenfield-fullstack`:

```
@sm *draft → @po *validate → @dev *develop → @qa *review → @devops *push
```

### Passo 3: Ciclo de desenvolvimento

1. **`@sm *draft`** — Cria a story com requisitos
2. **`@po *validate`** — Valida os critérios de aceitação
3. **`@dev`** — Implementa o código
4. **`@qa *review`** — Revisa e testa
5. **`@devops *push`** — Deploy e operações

---

## 5. Ciclo de Desenvolvimento SDC

O SDC (Story-Driven Cycle) é o fluxo padrão do AIOS:

```
@sm *draft
  └─► cria docs/stories/story-X.X.md
      └─► @po *validate
              └─► @dev (implementação)
                      └─► @qa *review
                                └─► @devops *push (deploy)
```

### Comandos essenciais por agente

| Agente       | Comando           | O que faz                     |
| ------------ | ----------------- | ----------------------------- |
| `@pm`        | `*create-prd`     | Cria PRD do produto           |
| `@sm`        | `*draft`          | Cria story a partir do PRD    |
| `@po`        | `*validate`       | Valida critérios de aceitação |
| `@dev`       | `*develop`        | Implementa código da story    |
| `@qa`        | `*review`         | Revisa qualidade do código    |
| `@devops`    | `*push`           | Deploy para produção          |
| `@architect` | `*analyze-impact` | Analisa impacto arquitetural  |

---

## 6. Ferramentas Exclusivas do AntiGravity

### 6.1 `generate_image` — Geração de imagens

Gere assets visuais diretamente no chat:

```
@dev
Crie um logo para o projeto MyApp — fundo escuro, estilo minimalista, cores #6366f1 e branco.
```

O assistente usará `generate_image` para criar e salvar o arquivo no projeto.

### 6.2 Stitch MCP — Design de UI

Crie interfaces visuais com o Stitch MCP integrado ao AntiGravity:

```
@ux-expert
*design-screen "Dashboard de métricas com gráficos de linha e cards de KPI"
```

O Stitch MCP gera protótipos de tela exportáveis diretamente para o projeto.

### 6.3 `browser_subagent` — Automação de browser

Teste e explore páginas web automaticamente:

```
@qa
*browser-test "https://meu-projeto.vercel.app" — Verificar fluxo de login
```

O `browser_subagent` abre, navega e reporta o resultado com screenshot.

---

## 7. Troubleshooting

### `.antigravity/` não foi criado

```bash
# Reinstalar
npx aios-core install --force

# Verificar
ls .antigravity/
```

### Agente não ativa no Gemini Code Assist

1. Verifique se `ANTIGRAVITY.md` está presente:
   ```bash
   cat .antigravity/ANTIGRAVITY.md
   ```
2. Confirme que a extensão Gemini Code Assist está ativa no VS Code
3. Recarregue a janela: `Ctrl+Shift+P` → `Developer: Reload Window`

### `GEMINI_API_KEY` não reconhecida

```bash
# Verificar se o arquivo .env está correto
cat .env | grep GEMINI

# Testar a chave
node -e "console.log(process.env.GEMINI_API_KEY)" # deve retornar a chave
```

### Stitch MCP não funciona

1. Verifique se o servidor MCP está configurado em `.antigravity/`
2. Consulte [Configuração MCP](./mcp-global-setup.md)
3. Execute `npx aios-core doctor` para diagnóstico

### Agentes não sincronizados

```bash
npm run sync:ide:antigravity
npm run validate:antigravity-sync
```

---

## Referências

- [Referência Técnica AntiGravity](../../pt/antigravity/getting-started.md)
- [Guia do Usuário AIOS](./user-guide.md)
- [Configuração de Desenvolvimento](./development-setup.md)
- [Guia de Squads](./squads-guide.md)
- [Integração MCP](./mcp-global-setup.md)

---

_Guia Prático AntiGravity v1.0 — 2026-02-26_
