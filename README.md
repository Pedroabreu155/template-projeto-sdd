# Template de projeto com workflow de agentes

Estrutura mínima para um projeto pessoal novo já nascer com o workflow
tasks → specs → implementação. Copie esta pasta, preencha os `[COLCHETES]`
e apague o que não usar.

## Como usar

1. Crie o repo no GitHub (ex: `projeto-novo`) e clone.
2. Copie o conteúdo desta pasta para a raiz do repo.
3. Preencha os `[COLCHETES]` em `AGENTS.md`, `TASKS.md` e `HANDOFF.md`.
4. **Defina onde ficam os docs de produto.** Se você mantém um vault de
   documentação, aponte o caminho em `AGENTS.md` (seção "Docs de produto e
   negócio"). Se não houver, deixe o colchete e o agente **pergunta** no primeiro
   uso — não crie docs de negócio no repo por reflexo.
5. Instale a skill spec-driven em cada máquina
   (o workflow referencia `tlc-spec-driven` ou equivalente):
   o `AGENTS.md` global (`~/.config/opencode/AGENTS.md`) degrada para as
   regras estáticas quando a skill não existir — nada quebra.
6. (Opcional) No `opencode.json` do projeto, adicione `instructions` remotas
   apontando para a versão publicada deste template, para herdar atualizações:
   `"instructions": ["https://raw.githubusercontent.com/[USER]/[TEMPLATE-REPO]/main/docs/WORKFLOW-SPECS.md"]`.
7. No primeiro uso, o agente lê `HANDOFF.md` → `TASKS.md` e segue o gate. Sem
   vault definido, ele pergunta onde ficam os docs de produto.

## O que vai em cada arquivo (e por quê separados)

- `AGENTS.md` — **lei estável do projeto** (tracker, gates, restrições, vault).
  Muda raramente. É o que o agente carrega sempre. A seção *Docs de produto e
  negócio* aponta o vault; sem vault definido, o agente pergunta em vez de
  inventar um lugar para a verdade.
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
