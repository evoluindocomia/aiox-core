# PRD: Interceptação YOLO Mode vs. Squad Padrão

## 1. Contexto e Problema Central

O AIOS, sob a égide do ambiente Antigravity (IDE), possui duas vertentes operacionais diametralmente opostas:

1. **YOLO Mode (You Only Live Once):** Execução assíncrona, acelerada e generalista onde a IA absorve a tarefa num único prompt e cospe a solução direta (sem orquestração de pares).
2. **SDC (Story Development Cycle) com Squads:** Linha de montagem industrial. Envolve `@pm`, `@architect`, `@ui-builder`, `@dev` e `@qa`. Exige passagens de bastão burocráticas e paradas para validação humana (ex: criar e validar `ui-guidelines.yaml` antes de tocar no código).

**O Problema:** Usuários disparam gatilhos globais (como "Crie um projeto Greenfield") sem acionar uma Squad explicitamente. O sistema silenciosamente assume o YOLO Mode, ignorando a esteira SDC, ferramentas como o Google Stitch MCP, e pulando fases de arquitetura.

## 2. Objetivo da Solução

Criar uma "Trava de Consciência" (Interception Hook) **exclusiva para quando o Antigravity for a IDE em uso**.
Se o desenvolvedor der uma ordem de peso arquitetural sem designar uma Squad, a interface deverá suspender a execução, alertar o usuário sobre o modo padrão (YOLO) e fornecer a opção de transição dinâmica para uma **Squad Padrão** (Default Squad) que carregue todo o pipeline do SDC.

## 3. Pessoas Atendidas

- **Devs & Arquitets** que esperam qualidade rigorosa (SDC) mas falham em invocar o comando da Squad corretamente.
- **Prototipadores Ágeis** que querem apenas o YOLO Mode e podem confirmá-lo ativamente, assumindo os riscos estéticos e lógicos.

## 4. Especificação Funcional (Features)

- **F1: Consolidação da "Default Squad":**
  - Existência obrigatória de uma Squad de escopo geral (ex: `squads/default-squad/squad.yaml` ou metadado global), configurada por default para atuar com o SDC completo (incorporando Architect, UI-Builder com Stitch, Dev e QA).

- **F2: Gatilho de Interceptação Conversacional (The Hook):**
  - Sempre que comandos indicando criação de projetos, "workflows" ou implementações fullstack pesadas forem recebidos em `.antigravity`, uma regra de sistema avaliará a presença da orquestração.
  - Critério: O prompt do usuário cita explicitamente `squad`, `@squad-chief`, ou delega agentes em etapas? Se NÃO, ativa F3.

- **F3: A Mensagem de Bloqueio (Prompting):**
  - O AIOS pausa e emite o alerta interativo.
  - _Mensagem de exemplo:_ "Nenhuma Squad foi definida para este comando. O comportamento padrão enviará a execução para o **YOLO Mode** (Execução direta em tiro-único pelo agente generalista). Você deseja: **1)** Continuar em YOLO Mode, ou **2)** Escalar para a **Squad Padrão** (iniciando a orquestração do SDC passo a passo: Arquitetura -> UI Builder -> Dev -> QA)?"

- **F4: Rutas de Escolha (The Pathways):**
  - **Se 1:** AIOS consome a thread como generalista e coda agressivamente.
  - **Se 2:** AIOS muda seu estado. Invoca o roteamento da Squad Padrão, encarna a primeira persona da cadeia (ex: o `@architect`) e começa o output da Fase 1 do SDC.

## 5. Requisitos Não Funcionais (NFRs)

- **NFR1:** Restrição de Ambiente: Este comportamento de _Interception_ existe **apenas** nas diretrizes de base do `.antigravity` (não deve vazar para as regras cruas do Node.js puro ou `claude-code` legado).
- **NFR2:** Zero atrito de CLI; a pergunta deve ser orgânica no modelo conversacional de LLM, atuando nas `rules` ou no _System Prompt_ de entrada.
