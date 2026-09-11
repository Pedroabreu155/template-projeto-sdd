# Workflow de specs — mapping → product-spec → tech-spec

Ordem de uso: **mapping** (o que existe) → **product-spec** (o quê/porquê)
→ **tech-spec** (como) → implementação em slices.

Toda implementação de agente entra por `TASKS.md` — nunca direto pelo código.
Para calibrar Specify → Design → Tasks → Execute, usar skill spec-driven
(`tlc-spec-driven` ou equivalente; auto-sizing: small pula etapas, medium
enxuga, large/complex full).

---

## 1. Mapping

Retrato fiel do código como está hoje. Fonte que os specs consultam para não
perguntar o óbvio nem contradizer o existente.

```
.mapping/               # opcional no início; criar lazy por módulo
├── glossary.md         # termos do domínio
├── architecture.md     # decisões transversais (stack, convenções, o que é lei)
├── OPEN-QUESTIONS.md   # dúvidas sem resposta — nunca inferir em silêncio
└── modules/
    └── <modulo>/
        ├── business.md   # regras de negócio que o código aplica hoje
        └── technical.md  # decisões técnicas, contratos, dívidas
```

Regras: nunca inferir (dúvida vira linha em `OPEN-QUESTIONS.md`); criar arquivos
só com conteúdo real; spec que muda regra/decisão atualiza o mapping como
critério de aceite.

---

## 2. Product-spec — `.specs/features/<slug>/spec.md`

O quê e porquê, sem stack. **Quando:** feature nova ou mudança de comportamento
com regra de negócio. **Não usar** para bugfix, copy ou refactor (vai direto).

Estrutura: Resumo (o que é e o que **não** é) · Atores · Premissas e Restrições ·
Fluxo Principal · Regras de Negócio (**RN-01…**) · Exceções · Entidades e Campos ·
Integrações · Métricas de Sucesso · Fora de Escopo · Glossário Local.

---

## 3. Tech-spec — `.specs/features/<slug>/design.md`

Plano executável: arquivos a tocar, contratos, decisões (**D-XX** rastreando
RN-XX, com alternativa descartada e preço aceito), riscos (**R-XX**), testes,
migração/rollout, critérios de aceite (**CA-XX**, um por RN) + aceite operacional
final: **mapping atualizado**. **Quando:** product-spec médio/grande, tradeoff
real, migração de schema ou fronteira de módulo — mesmo sem product-spec
(derivar as RNs no doc). Nunca codifica, nunca edita o mapping (sinaliza o conflito).

---

## 4. Fluxo ponta a ponta

```
TASKS.md (task + dependências + aceite — leitura obrigatória)
  → classificar: direto | product-spec | tech-spec
  → mapping do(s) módulo(s) (criar lazy se não existe)
  → product-spec → tech-spec → tasks atômicas (.specs/features/<slug>/)
  → implementação por slices (commits atômicos)
  → TASKS.md (✅ + Histórico) + mapping atualizado
```

Exemplo de calibragem: copy com regra = product-spec rápido ou direto;
feature média = product + tech + slices; bugfix = direto.
