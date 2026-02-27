---
description: Estratégia de integração do Google Stitch UI com o ecossistema Antigravity AIOS, detalhando o papel do agente especializado @ui-builder.
---

# Estratégia de Integração: Stitch UI & Agente Especializado

## 📋 Análise do Problema (Integração de UI)

Com a introdução da parametrização do Google Stitch UI (`ui-guidelines.yaml`), surgiu a necessidade de definir **quando** e **como** a ferramenta MCP do Google Stitch seria acionada durante a fase de desenvolvimento.
A principal questão arquitetural era: devemos inflar o agente de desenvolvimento genérico (`@dev`) com esse novo conhecimento ou criar um agente especializado?

## 🧠 Decisão Estratégica: O Agente @ui-builder

A melhor estratégia no ecossistema Antigravity é a **criação e adoção de um agente especializado**, nomeado `@ui-builder`, ao invés de sobrecarregar o `@dev` genérico.

**Por que a separação é necessária? (Princípio de Context Boundaries no Antigravity)**

1. **Separação de Preocupações (Separation of Concerns):** O agente genérico `@dev` funciona perfeitamente para lógica de backend, construção de APIs, scripts, integrações contínuas, etc. Injetar instruções pesadas específicas de UI (como checar diretrizes visuais e invocar o servidor MCP do Stitch) no prompt do `@dev` o tornaria inchado e altamente propenso a alucinações durante sprints focados estritamente em back-end.

2. **Herança Limpa por Squad:** A arquitetura do Antigravity permite que _Squads_ sejam modulares e criadas sob demanda. Quando o `@squad-chief` iniciar uma nova Squad para um Épico de Frontend (ex: `squad-ui-dashboard`), ele deverá inserir o agente especializado `@ui-builder`. Este agente possui o conhecimento de Stitch UI embutido nativamente no seu "DNA" ou prompt de sistema. Como consequência, toda nova squad focada em front-end herda esse comportamento impecável e padronizado e a esteira UI flui naturalmente.

## 🚀 O Papel do @ui-builder no Fluxo

Para que essa estratégia funcione plenamente, **três componentes** mantêm o ecossistema orquestrado:

1. **A Mente do Agente (`.antigravity/agents/ui-builder.md`):** O `@ui-builder` possui três heurísticas fundamentais incorporadas em seu DNA:
   - _Heurística 1:_ Antes de iniciar qualquer código de front-end, DEVE procurar pelo arquivo `docs/architecture/ui-guidelines.yaml`.
   - _Heurística 2:_ Se as Diretrizes de UI existirem, DEVE chamar obrigatoriamente a ferramenta MCP do Google Stitch para gerar os componentes visuais baseados nessas diretrizes, nunca os "desenhando" do zero "da própria cabeça".
   - _Heurística 3:_ O agente assume a codificação de fato apenas no Pós-Stitch, implementando as integrações com regras de negócios, hooks, state management e eventos na tela crua retornada.

2. **Registro de Agentes (`AGENTS.md`):** O agente `@ui-builder` (e seus atalhos correspondentes) encontram-se registrados globalmente como o especialista mandatário dentro do domínio de Design/Front-End.

3. **Ciclo de Desenvolvimento (`story-development-cycle.md`):** O SDC foi desenhado para identificar a natureza da Story em status "Ready". Se o foco for genérico/back-end, o sistema aciona o `@dev`. Para stories puramente em contexto de Frontend/UI a invocação passa a ser para o `@ui-builder`, preservando o isolamento de escopo.
