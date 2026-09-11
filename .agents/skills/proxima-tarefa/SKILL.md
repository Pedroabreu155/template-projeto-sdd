---
name: proxima-tarefa
description: "Use quando o usuário perguntar qual a próxima tarefa prioritária, o que fazer agora, prioridades do dia/semana, ou ao iniciar sessão de planejamento. Consulta o kanban do projeto no Notion e aplica regra de prioridade (P0, dependências, bloqueios, teto de 3 em andamento). Triggers: proxima tarefa, próxima tarefa, o que fazer, prioridade, prioridades, kanban, backlog. PREENCHER: data_source com a URL collection:// do seu kanban."
metadata:
  version: "1.0.0"
---

# Próxima tarefa (kanban no Notion)

Responde "qual a próxima tarefa prioritária?" consultando o kanban em vez de
adivinhar. Nunca recomende de memória: rode a consulta toda vez.

> **Preencher ao adotar este template:** substitua `[DATA-SOURCE-URL]` pela URL
> `collection://...` do seu kanban (aparece no `fetch` do database, tag
> `<data-source url="...">`) e `[PROJETO-PADRÃO]` pelo projeto deste repo.
> Apague este aviso depois de preencher.

## Fonte

- Data source (nome de tabela no SQL, entre aspas): `[DATA-SOURCE-URL]`
- Escopo padrão: `[PROJETO-PADRÃO]`

Antes da primeira consulta, faça `fetch` no data source para confirmar os nomes
exatos das propriedades. Convenção esperada: `Tarefa` (título), `Projeto`,
`Prioridade` (P0–P3), `Status`, `Esforço`, `Responsável`, `Depende de` (array
JSON de URLs), `Notas`. Se o schema divergir, adapte os nomes e mantenha o algoritmo.

## Consulta (via `query_data_sources`, modo SQL)

```sql
SELECT url, "Tarefa", "Status", "Prioridade", "Esforço", "Responsável", "Depende de"
FROM "[DATA-SOURCE-URL]"
WHERE "Projeto" = ?
  AND "Status" NOT IN ('Feito', 'Bloqueado')
ORDER BY
  CASE "Prioridade" WHEN 'P0' THEN 0 WHEN 'P1' THEN 1 WHEN 'P2' THEN 2 ELSE 3 END,
  "Tarefa"
```

Params: `["[PROJETO-PADRÃO]"]`. Não assuma a lista de opções de `Status` —
ela muda; a única garantia é excluir `Feito` e separar `Bloqueado`.

## Regra de prioridade (nesta ordem)

1. **Excluir `Feito`.** Separar `Bloqueado` numa lista à parte.
2. **Blocos estacionados** (projeto em backlog por decisão): não recomendar
   salvo pedido explícito.
3. **Elegibilidade por dependência:** card com `Depende de` só é elegível se TODAS
   as dependências estiverem `Feito` (checar cada URL via fetch ou
   `SELECT "Status" ... WHERE url = ?`). Dependência não-feita = "travada por X".
4. **Ordem:** P0 elegível primeiro (comprometido da semana); depois P1, P2, P3.
   Empate: menor esforço primeiro.
5. **Responsável externo/terceiro:** a ação é **cobrar/disparar**, não executar —
   recomendar o follow-up com o texto pronto.
6. **Teto operacional:** no máximo 3 cards em execução simultânea. Se já houver 3,
   a recomendação é terminar um antes de puxar outro.
7. **Espelhos de execução:** cards que espelham um tracker do repo (ex: `TASKS.md`)
   — a execução e os commits seguem pelo repo; o card só reflete o status.

## Formato da resposta

- **Recomendação única** (1 card): título + por que agora (prioridade, dependências ok).
- **Se responsável externo:** o texto exato do follow-up.
- **Em 1–2 linhas:** o que está travado e por quê + próximos da fila (máx 3).
- Nunca despejar a lista inteira do kanban.
