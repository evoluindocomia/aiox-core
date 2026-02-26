# Checklist de Cobertura — AIOS Governance Pipeline

> **Validação de Paridade vs Hooks Python do Claude Code**

| Hook Python Original            | Task AGP Equivalente          | Status            | Detalhes da Cobertura e Casos Atendidos                                                                                                                                                                        |
| ------------------------------- | ----------------------------- | ----------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `enforce-architecture-first.py` | `check-architecture-first.md` | ✅ Paridade total | O AGP valida o PROTECTED_PATH e a ALLOWED_LIST extamente iguais. Bloqueia (com aprovação) write operations que não possuam doc e libera para caminhos white-listed ou edições puras.                           |
| `mind-clone-governance.py`      | `check-mind-clone-dna.md`     | ✅ Paridade total | O AGP faz matching com sufixos/prefixos funcionais validando a permissão prévia, além de testar obrigatoriedade técnica da existência dos 4 paths vitais de DNA em criações de mentes humanas.                 |
| `sql-governance.py`             | `check-sql-governance.md`     | ✅ Paridade total | Todos os termos destrutivos e de designação de banco (ex. CREATE, ALTER, DROP, POLICY) foram rastreados e bloqueados para exigir o Supabase CLI. DML puro e backups via scripts `pg_dump` estão liberados.     |
| `enforce-git-push-authority.sh` | `check-git-push-authority.md` | ✅ Paridade total | Restrição ativa para `git push` ou `git worktree` restrita exclusivamente à autoridade de cargos englobados pelo profile `@devops`. Não autorizados repassam a task através de workflow delegado.              |
| `write-path-validation.py`      | `check-write-path.md`         | ✅ Paridade total | Verificação rigorosa de rotas `docs/` operando de forma interativa através do mecanismo `notify_user(Blocked)`. Age exigindo aceitação à regra de nomenclatura de diretório como esperado pela fail-open.      |
| `slug-validation.py`            | `check-slug-format.md`        | ✅ Paridade total | Validação atrelada nativamente ao regex base de snake*case puro `^[a-z0-9]+(*[a-z0-9]+)\*$`. Aplica substituições on-the-fly das chaves erradas (como camelCase e dots), servindo feedback sintático do termo. |

## Resumo H6 - Validação Final

- **Lógica e Conflitos**: Todas as _tasks_ roteiam estritamente pelo `SKILL.md` (único _entry point_), se interligam ao config centralizado e funcionam independentes no ambiente Antigravity eliminando a dependência do interceptor nativo.
- **Documentação Master**: O antigo arquivo mandatório `governance.md` foi adaptado com as flags ativas e reflete fielmente o mecanismo do pipeline e das regras Python legadas.
