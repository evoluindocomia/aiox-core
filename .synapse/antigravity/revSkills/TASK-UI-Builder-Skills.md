# Task: Implementação de Skills para o `@ui-builder`

## Descrição

Execução prática das definições do `PRD-UI-Builder-Skills.md` para integrar 3 Skills ao ecossistema do Antigravity, promovendo auto-roteamento no agente de interface de acordo com a stack (Web ou Mobile).

## Checklist de Execução

### Fase 1: Criação das Skills Base (Bunkers de Conhecimento)

- [ ] Criar a Skill `web-ui-reviewer.md` em `.antigravity/skills/web-ui-reviewer/SKILL.md`.
  - Garantir Persona de Revisor HTML5/SEO/TailwindCSS.
  - Garantir lógica de parada (interrupção e aprovação do usuário).
- [ ] Criar a Skill `flutter-architect.md` em `.antigravity/skills/flutter-architect/SKILL.md`.
  - Garantir Persona de Engenheiro Sênior 15+ XP em Flutter.
  - Impor heurísticas estruturais de injeção de dependência (`GetIt`, `Injectable`).
- [ ] Criar a Skill `stitch-to-flutter.md` em `.antigravity/skills/stitch-to-flutter/SKILL.md`.
  - Garantir Persona Elite de conversão visual de UI (vinda do Stitch) para Flutter Widgets.
  - Impor aderência obrigatória ao `ui-guidelines.yaml`.

### Fase 2: Roteamento Dinâmico (Evolução do Agente)

- [ ] Editar `.antigravity/agents/ui-builder.md`
  - Adicionar seção de auto-verificação do ecossistema/plataforma (`ui-guidelines.yaml`).
  - Modificar as "Heurísticas Rígidas" para introduzir a regra "SE projeto Web ENTÃO ative web-ui-reviewer".
  - Modificar as "Heurísticas Rígidas" para introduzir a regra "SE projeto Mobile ENTÃO ative flutter-architect E stitch-to-flutter".
  - Garantir a permanência e invocação intactas do Google Stitch MCP (isso nunca deve ser sobrescrito).

### Fase 3: Revisão

- [ ] Verificar logs e qualidade das instruções.
- [ ] Confirmar compatibilidade e não-sobreposição entre Web e Mobile.
