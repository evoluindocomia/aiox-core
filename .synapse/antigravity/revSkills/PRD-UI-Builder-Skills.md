# PRD: UI Builder Skills Integration

## 1. Introdução e Contexto

O agente `@ui-builder` é o orquestrador especialista em Front-end, responsável por gerar interfaces visuais a partir de Acceptance Criteria utilizando o Google Stitch MCP. Contudo, devido à complexidade distinta entre aplicações Web (HTML5/CSS3/React) e Mobile (Flutter/Dart), o agente necessita delegar conhecimentos técnicos profundos e validações específicas a "Skills" dedicadas.

A finalidade deste PRD é definir a integração de 3 novas Skills injetáveis para o `@ui-builder` garantir robustez estrutural, sem comprometer a estabilidade já adquirida no processo atual do Stitch MCP.

## 2. Objetivos

- Reduzir a carga cognitiva do agente `@ui-builder`, modularizando a atenção e regras de negócio.
- Prover validações avançadas (Revisor) de HTML5/CSS3/TailwindCSS e SEO em aplicações Web pós-Stitch.
- Permitir uma delegação estrutural perfeita para Flutter (Mobile), incluindo injeção de dependência e conversão correta da estrutura do Stitch.
- Transformar o `@ui-builder` em um Roteador Inteligente dependente do contexto.

## 3. Escopo Funcional (As 3 Novas Skills)

### 3.1 Skill 1: `web-ui-reviewer`

- **Persona:** Revisor especialista e obsessivo por qualidade em HTML5, CSS3, SCSS, TailwindCSS e SEO.
- **Responsabilidade:** Analisar a tela Web gerada pelo Stitch.
- **Comportamento:** Apenas ativada em projetos Web. Se houver inconsistências estruturais, de tags semânticas de SEO, ou classes Tailwind ausentes, a Skill interrompe o fluxo (Quality Gate) e solicita aprovação/ação do usuário antes de prosseguir.

### 3.2 Skill 2: `flutter-architect`

- **Persona:** Engenheiro de Software Sênior Mobile (+15 anos de XP em Flutter).
- **Responsabilidade:** Definir o esqueleto arquitetural, o roteamento e o gerenciamento de dependências.
- **Ferramentas Mandatórias:** `GetIt` e `Injectable`.
- **Comportamento:** Ativada em projetos Mobile antes (ou durande) o bind das regras de negócio. Ele audita os princípios Clean Code, separação por features, DI (Dependency Injection), além de sugerir os setups iniciais ou validar a estrutura.

### 3.3 Skill 3: `stitch-to-flutter`

- **Persona:** Engenheiro de Conversão Elite.
- **Responsabilidade:** Converter cirurgicamente o design/estrutura devolvido pelo Google Stitch MCP para código nativo ou Widgets do Flutter consistentes.
- **Comentários:** Altamente intuitivo, assertivo, e ciente das restrições do `ui-guidelines.yaml`. Age em tandem com o `flutter-architect` em projetos Mobile para garantir um casamento perfeito arquitetura/UI.

## 4. Atualização no Agente Base (`ui-builder.md`)

O arquivo do agente deverá receber uma heurística robusta de auto-roteamento (Auto-Routing). Dependendo do tipo de projeto detalhado pelos `ui-guidelines.yaml` (Mobile ou Web), o agente ativará ou a pipeline Web (`web-ui-reviewer`) ou a pipeline Mobile (`flutter-architect` + `stitch-to-flutter`), sem desativar sua lógica de invocar o MCP do Stitch primeiro.

## 5. Critérios de Aceite

- Os três arquivos `.antigravity/skills/*/SKILL.md` existem e possuem personas super bem detalhadas.
- As orientações e descrições deixam claro que os processos de Web e Mobile são excludentes (ou roda Web, ou roda Mobile).
- O arquivo `.antigravity/agents/ui-builder.md` foi atualizado com a inteligência de auto-roteamento.
- Os pipelines respeitam o retorno inicial pelo Google Stitch MCP e servem como complementos modulares.
