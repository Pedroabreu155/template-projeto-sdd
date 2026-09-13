# [NOME DO PROJETO] — AGENTS.md (específico do projeto)

Workflow base: `~/.config/opencode/AGENTS.md` (genérico, vale para todos os projetos).
Aqui só o que é específico deste projeto. Quando ambos existirem, ambos valem.

## Tracker e docs

- **Retomada:** `[HANDOFF.md ou equivalente]` (estado verificado), depois `[TASKS.md ou equivalente]`.
- `[TASKS.md]` é a fonte única da execução. Portfólio/produto: `[link do Notion ou "não há — o TASKS.md é o único nível"]`.
- Detalhe do fluxo de specs: `docs/WORKFLOW-SPECS.md`. Regras de código e testes: `[CLAUDE.md ou seção abaixo]`.

## Docs de produto e negócio (vault)

- Contexto de produto e negócio vive **fora deste repo**, num vault de documentação: `[caminho do vault, ex: ~/Projetos/me/vault/<projeto> — ou "não há"]`.
- **Se o caminho não estiver definido, pergunte ao usuário** onde ficam (ou se haverá) os docs de produto, antes de criar qualquer um no repo. Não invente um segundo lugar para a verdade.
- Separação: engenharia (este arquivo, `CLAUDE.md`, `TASKS.md`, `HANDOFF.md`, `docs/`) fica no repo; produto/negócio fica no vault. Leia o vault antes de decidir prioridade de produto.
- Tarefas e gestão (backlog, kanban, status) ficam no tracker — não no vault nem duplicadas no repo. O vault guarda contexto, não fila.
- Se não houver vault nem intenção de ter, apague esta seção.

## Gates de verificação

- `[ex: npx tsc --noEmit + npx vitest run]`.
- Integração externa `[se houver, ex: Stripe, API de clima]`: smoke real antes de marcar como concluído.

## Restrições do projeto

- Não alterar `[preço, limites de plano, schema do banco, provedor de API, textos legais — ajuste à realidade]` sem confirmar.
- Não refatorar fora do escopo da task.
- Fora do escopo do agente: `[ex: contato com terceiros, credenciais, publicação, divulgação]`.
