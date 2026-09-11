# Handoff — [NOME DO PROJETO]

**Escrito em:** [DATA] · **Branch:** `[branch]` · **HEAD:** `[hash]` · **Working tree:** [limpo/sujo]

Diário de sessão para o próximo agente (ou para você depois de um tempo longe).
Lê-se **uma vez por sessão** — não carrega por prompt como o `AGENTS.md`.

> **O que entra aqui:** estado volátil (branch, trabalho não commitado),
> evidências medidas (smokes, números), divergências entre docs, armadilhas recentes.
> **O que NÃO entra:** regra estável. Armadilha que virou lei sai daqui e é promovida
> para `AGENTS.md`/`CLAUDE.md`/mapping — senão este arquivo vira um segundo AGENTS
> que apodrece.

---

## 1. Leia nesta ordem

| Arquivo | O que responde |
|---|---|
| `AGENTS.md` | Como trabalhar (gate, restrições) |
| `TASKS.md` | O que falta — **fonte única de tarefas** |
| `HANDOFF.md` (este) | Estado verificado, evidências, armadilhas |

---

## 2. Estado do repositório (confirme antes de codar)

```
[branch base]   [hash]  [onde produção aponta, se houver]
[branch atual]  [hash]  [+ arquivos NÃO COMMITADOS, se houver]
```

---

## 3. O que foi medido (não é suposição)

[Smokes contra APIs reais, com comando para reproduzir. Sem mock que confirma premissa.]

---

## 4. Próximo passo recomendado

[Ordem que respeita as prioridades do projeto + o que depende de terceiros, em paralelo.]

---

## 5. Armadilhas (já custaram tempo uma vez)

- [Cada item: o erro + por que acontece + como evitar. Quando estabilizar, promover para o AGENTS.md e remover daqui.]
