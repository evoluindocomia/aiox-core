# Task: Atualização de Documentos (Integração Google Stitch UI)

## Objetivo

Você está assumindo a repescagem e implementação de documentação legível (Markdown) baseando-se no **PRD `prd-docs-stitch.md`**.
O cenário introduz o agente `@ui-builder` e o processo de geração visual delegada via Google Stitch (MCP).

## Tarefas a Executar

### Fase 1: Análise e Absorção (Read-only)

- [ ] Ler o PRD: `.synapse/antigravity/detalhamentos/prd-docs-stitch.md`
- [ ] Ler as referências técnicas principais:
  - `.synapse/antigravity/detalhamentos/ui-builder-strategy.md`
  - `.synapse/antigravity/detalhamentos/stitch-ui-workflow.md`
- [ ] Visualizar a árvore existente de `docs/pt/antigravity` e `docs/en/antigravity`.

### Fase 2: Atualização de Guias e Workflows (Português e Inglês)

- [ ] Refatorar os passos do Workflow referenciando a cisão entre `@dev` e `@ui-builder`. Se o arquivo existir na pasta `/docs`, atualizá-lo.
- [ ] Criar a página de documentação `docs/pt/antigravity/workflows/stitch-ui-workflow.md`.
- [ ] Criar a página equivalente `docs/en/antigravity/workflows/stitch-ui-workflow.md` em inglês.
- [ ] Atualizar os índices (`index.md` e `getting-started.md`) adicionando os links de UX/UI.

### Fase 3: Documentação de Agentes (Português e Inglês)

- [ ] Criar página explicativa detalhada do perfil em `docs/pt/antigravity/agents/ui-builder.md` e suas heurísticas (Conselho: Não copie o .yaml do prompt e cole na documentação; explique-o de forma legível para o desenvolvedor final).
- [ ] Criar página idêntica em `docs/en/antigravity/agents/ui-builder.md`.
- [ ] Fazer uma sutil modificação nos arquivos documentais do `@dev` limitando explicitamente seu escopo para backend e lógicas (onde front-ends ricos passarem pela esteira).

### Fase Final: Verificação Geral

- [ ] Rodar o comando de lint de documentação, se disponível na base do repositório.
- [ ] Checar se não sobrou nenhuma menção antiga no projeto informando que o AIOS precisa "adivinhar" o código base de tela.
