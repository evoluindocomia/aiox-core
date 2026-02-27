# Guia de Onboarding Definitivo — Antigravity

Bem-vindo ao guia passo-a-passo definitivo para iniciar no ambiente **Antigravity** do AIOS. Este guia foi desenhado para ajudar você a contornar limitações da CLI atual e começar a desenvolver aplicações incríveis imediatamente usando o provedor Gemini.

---

## 1. Setup Inicial e Resolução de Gaps

Atualmente, o comando `aios-core init` pode não copiar todos os arquivos do ambiente `.antigravity/` para o seu workspace por limitações técnicas no empacotamento (`package.json`). Siga os passos abaixo para garantir uma instalação perfeita.

### PASSO A PASSO DA INSTALAÇÃO SEGURA

1. **Instale o AIOS normalmente no seu diretório:**

   ```bash
   npx aios-core init meu-projeto
   cd meu-projeto
   ```

2. **Copie o ambiente Antigravity (WORKAROUND GAP-02):**
   Caso a pasta `.antigravity/` não tenha sido copiada completamente, você deve copiar o diretório fonte `.antigravity/` inteiro (que inclui `agents/`, `rules/`, `skills/`, `workflows/`, `templates/` e o arquivo `ANTIGRAVITY.md`) da origem do `aios-core` para a raiz do seu `meu-projeto`.

3. **Sincronização com a IDE (WORKAROUND GAP-03):**
   Se o comando de sincronização (`npm run sync:ide`) ou as rotinas de _lint-staged_ não incluírem automaticamente as pastas do Antigravity, certifique-se de adicioná-las manualmente nas configurações do projeto caso perceba alguma dessincronização entre o `MEMORY.md` e a sua IDE.

---

## 2. Configurando as Chaves da API (GAP-04)

Para que o Antigravity utilize as engines de IA e as integrações mais avançadas do ecossistema AIOS (como geradores de interface e pesquisa na web), você precisa garantir que o provider principal seja o Gemini e que a chave de API esteja presente no seu ambiente.

1. Escolha o provider `gemini` sempre que o prompt da IDE ou da CLI perguntar qual modelo será utilizado.
2. Configure sua chave mestra antes de inicializar agentes. No Windows (PowerShell/CMD) ou Unix (bash/zsh):

   ```bash
   # Unix / MacOS
   export GEMINI_API_KEY="sua_chave_gemini_aqui"

   # Windows PowerShell
   $env:GEMINI_API_KEY="sua_chave_gemini_aqui"
   ```

3. Configure as permissões necessárias para a sua extensão ou IDE caso esteja utilizando um ambiente migrado ou modificado do Claude Code.

---

## 3. O Primeiro Uso: Executando um Greenfield Fullstack

Agora que as pastas estão copiadas e as chaves de API estão definidas, vamos construir sua primeira aplicação orientada por agentes!

Para acionar a magia do AIOS, seu ponto de partida sempre deve ser acionar o workflow correto na sua IDE.

1. **Abra o painel do seu assistente de IA** na IDE (como o Gemini Code Assist ou terminal interno).
2. **Peça explicitamente pelo workflow Greenfield Fullstack:**
   ```text
   Quero iniciar um projeto novo usando o workflow greenfield-fullstack.
   Vamos construir uma aplicação de lista de tarefas em React e Supabase.
   ```
3. O Antigravity injetará o arquivo `.antigravity/workflows/greenfield-fullstack.md` no contexto de execução.
4. **Observe a cadeia de agentes em ação:**
   - A agente `@analyst` fará um diagnóstico detalhado das suas necessidades.
   - O agente `@pm` criará um Product Requirements Document (PRD).
   - O `@architect` definirá a estrutura Front-end e Back-end.
   - A `@po` vai segmentar a especificação em Stories executáveis usando o arquivo `story-tmpl.yaml`.
   - O `@dev` implementará o código das Stories e a `@qa` testará.

---

## 4. Troubleshooting Comum

**O agente não está respeitando as regras governacionais e de Hook**

- **Causa:** O arquivo `ANTIGRAVITY.md` ou a pasta `rules/` não estão devidamente presentes.
- **Solução:** Volte ao Passo 1 e certifique-se de que a estrutura `.antigravity/` foi copiada completamente para a raiz e não está bloqueada pelo seu arquivo `.gitignore`.

**"Provider não suportado ou erro de autenticação"**

- **Causa:** Ausência da `GEMINI_API_KEY` rodando num ambiente restrito ou reiniciado.
- **Solução:** O terminal atual pode não ter carregado suas variáveis de ambiente. Exporte a variável novamente (Passo 2).

**O assistente diz que a skill/agente não existe**

- **Causa:** A limitação de contexto do assistente da IDE não carregou o conteúdo da pasta em tempo hábil.
- **Solução:** Invoque explicitamente a leitura do arquivo base. Exemplo: _"Leia as instruções em `.antigravity/skills/synapse/SKILL.md`"_.

---

## 5. Testes e Validação Local do Instalador

Caso você esteja contribuindo para o desenvolvimento do AIOS ou precise validar o instalador localmente sem publicá-lo no NPM, você pode utilizar duas estratégias principais:

### Opção 1: Simulação de Empacotamento via NPM Pack (Recomendado)

Esta opção simula exatamente o comportamento do usuário final descompactando o pacote via `npx`.

1. Na raiz do projeto original (onde está o `package.json` principal do `aios-core`), execute:
   ```bash
   npm pack
   ```
2. Um arquivo `.tgz` será gerado (ex: `aios-core-4.4.6.tgz`).
3. Em uma pasta de ambiente de testes separada, execute o comando apontando para o arquivo local:
   ```bash
   npx "/caminho/absoluto/para/aios-core-4.4.6.tgz" init meu-projeto-teste
   ```

### Opção 2: Execução Direta Node (Para Debugging)

Esta opção é ideal para inspecionar o código linha a linha usando _breakpoints_ na sua IDE (ex: VSCode).

1. Crie uma pasta de testes isolada.
2. A partir do terminal dessa pasta (ou via `launch.json` da sua IDE), execute o arquivo Javascript principal diretamente via Node:
   ```bash
   node "/caminho/absoluto/para/aios-core/bin/aios.js" init meu-projeto-teste
   ```

---

## 6. Mergulhando Mais Fundo

Após finalizar sua primeira aplicação, você está pronto para explorar:

- [A orquestração do Design System usando Stitch MCP e geração autônoma de telas](./workflows/overview.md#design-system-build--design-system-with-stitch-mcp)
- [Criação de novos Mind Clones baseados em perfis de pessoas reais](./agents/mind-clones.md)
