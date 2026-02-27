# PRD: Documentação da Integração do Google Stitch UI e Agente @ui-builder no Antigravity

## Contexto e Objetivos

Recentemente, o ecossistema Antigravity (AIOS) foi estendido para suportar a geração autônoma de interfaces de usuário utilizando o **Google Stitch (via MCP)**.
Em conjunto, foi introduzido o agente especializado **`@ui-builder`** e as parametrizações de estilo (`ui-guidelines.yaml`).
O objetivo deste projeto de documentação é garantir que todos os artefatos em `docs/pt/antigravity` e `docs/en/antigravity` reflitam as novas capacidades, atualizando o índice, guias de início, seções de agentes e workflows, garantindo a paridade entre os idiomas e o correto entendimento da arquitetura.

## Escopo da Atualização

### 1. Documentação de Fluxos (Workflows & Templates)

- **`spec-pipeline.md` (Workflow Mestre):** Deve ser documentado como o `@pm` insere as perguntas sobre _Stitch UI_ no PRD, e como o `@architect` obrigatoriamente gera o arquivo `docs/architecture/ui-guidelines.yaml`.
- **`story-development-cycle.md`:** A documentação deve ser alterada para explicar a segregação de tarefas: sprints genéricas e de backend invocam o `@dev`, enquanto sprints de front-end ou UI (que posuem _ui-guidelines_) invocam o `@ui-builder`.
- **`stitch-ui-workflow.md`:** (Novo) Criar a versão de documentação legível e detalhada deste pipeline dentro das pastas `/workflows` do projeto público (`docs/pt` e `docs/en`).

### 2. Documentação de Agentes

- **`ui-builder.md`:** (Novo) Criar a documentação explicativa deste agente nas pastas `/agents`. Explicar as quatro heurísticas principais: leitura do `ui-guidelines.yaml`, acionamento exclusivo via MCP Google Stitch para layout, implementação do Business Binding e a proibição de "alucinar" CSS manual.
- **`dev.md`:** Atualizar a documentação do `@dev` esclarecendo que ele não lida mais com geração de casca visual (UI), redirecionando os usuários para ler a documentação do `@ui-builder` quando se tratar de frontend pesado.

### 3. Guias Básicos

- **`getting-started.md`:** Inserir breve menção de que o ecossistema suporta integração visual nativa.
- **`index.md`:** Atualizar os índices para mapear as novas documentações dos workflows e do agente `@ui-builder`.

## Referências Existentes

O agente encarregado dessa atualização herda todo o conhecimento armazenado na pasta `.synapse/antigravity/detalhamentos/`:

- `comparativo-desenvolvimento-aios.md` (Seção 7 - Integração Google Stitch)
- `stitch-ui-workflow.md` (Passo a passo da orquestração)
- `ui-builder-strategy.md` (A decisão estratégica de separação de domínios)
- O template central de PRDs em `.antigravity/templates/prd-tmpl.yaml`
- O Agent Profile em `.antigravity/agents/ui-builder.md`

## Critérios de Aceite (Acceptance Criteria)

- [ ] A pasta `docs/pt/antigravity` possui os novos conteúdos e os arquivos existentes foram inteligentemente refatorados para mencionar as regras do Stitch.
- [ ] A pasta `docs/en/antigravity` possui a exata mesma estrutura introduzida no diretório em Português.
- [ ] O arquivo `AGENTS.md` da raiz do repositório foi referenciado para demonstrar como o atalho `/ui-builder` se encaixa no desenvolvimento.
- [ ] Nenhum documento do Antigravity transmite a ideia de que o AIOS tenta gerar páginas inteiras escrevendo CSS puro sem uso de ferramentas MCP.
