# Template de projeto com workflow de agentes

Estrutura mínima para um projeto pessoal novo já nascer com o workflow
tasks → specs → implementação. Copie esta pasta, preencha os `[COLCHETES]`
e apague o que não usar.

## Como usar

1. Crie o repo no GitHub (ex: `projeto-novo`) e clone.
2. Copie o conteúdo desta pasta para a raiz do repo.
3. Preencha os `[COLCHETES]` em `AGENTS.md`, `TASKS.md` e `HANDOFF.md`.
4. Instale a skill spec-driven em cada máquina
   (o workflow referencia `tlc-spec-driven` ou equivalente):
   o `AGENTS.md` global (`~/.config/opencode/AGENTS.md`) degrada para as
   regras estáticas quando a skill não existir — nada quebra.
5. (Opcional) No `opencode.json` do projeto, adicione `instructions` remotas
   apontando para a versão publicada deste template, para herdar atualizações:
   `"instructions": ["https://raw.githubusercontent.com/[USER]/[TEMPLATE-REPO]/main/docs/WORKFLOW-SPECS.md"]`.
6. No primeiro uso, o agente lê `HANDOFF.md` → `TASKS.md` e segue o gate.

## O que vai em cada arquivo (e por quê separados)

- `AGENTS.md` — **lei estável do projeto** (tracker, gates, restrições).
  Muda raramente. É o que o agente carrega sempre.
- `TASKS.md` — **fila viva** (próximas, histórico, decisões). Muda a cada task.
- `HANDOFF.md` — **diário de sessão** (estado do repo, evidências medidas,
  armadilhas recentes). Lê-se uma vez por sessão, não por prompt.
  Regra de ciclo de vida: armadilha que virou regra estável sai daqui e é
  promovida para `AGENTS.md`/`CLAUDE.md`/mapping.
- `docs/WORKFLOW-SPECS.md` — o método (mapping → product-spec → tech-spec).
- `.specs/features/` — onde nascem `spec.md`, `design.md`, `tasks.md` por feature.
- `.agents/skills/proxima-tarefa/` — skill que lê seu kanban e responde "qual a
  próxima tarefa?". **Preencha `[DATA-SOURCE-URL]` e `[PROJETO-PADRÃO]` no SKILL.md.**
  O opencode descobre skills do repo automaticamente.
