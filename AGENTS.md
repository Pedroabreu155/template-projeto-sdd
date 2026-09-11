# [NOME DO PROJETO] — AGENTS.md (específico do projeto)

Workflow base: `~/.config/opencode/AGENTS.md` (genérico, vale para todos os projetos).
Aqui só o que é específico deste projeto. Quando ambos existirem, ambos valem.

## Tracker e docs

- **Retomada:** `[HANDOFF.md ou equivalente]` (estado verificado), depois `[TASKS.md ou equivalente]`.
- `[TASKS.md]` é a fonte única da execução. Portfólio/produto: `[link do Notion ou "não há — o TASKS.md é o único nível"]`.
- Detalhe do fluxo de specs: `docs/WORKFLOW-SPECS.md`. Regras de código e testes: `[CLAUDE.md ou seção abaixo]`.

## Gates de verificação

- `[ex: npx tsc --noEmit + npx vitest run]`.
- Integração externa `[se houver, ex: Stripe, API de clima]`: smoke real antes de marcar como concluído.

## Restrições do projeto

- Não alterar `[preço, limites de plano, schema do banco, provedor de API, textos legais — ajuste à realidade]` sem confirmar.
- Não refatorar fora do escopo da task.
- Fora do escopo do agente: `[ex: contato com terceiros, credenciais, publicação, divulgação]`.
