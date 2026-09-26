# claude-skills

Skills pessoais para Claude Code, distribuidas como marketplace de plugin.

## Instalacao

No Claude Code:

```
/plugin marketplace add alexandrecsimas/claude-skills
/plugin install web-research@xandy-skills
/plugin install session-id@xandy-skills
/plugin install session-pull@xandy-skills
```

## Skills

- **web-research** — politica de roteamento de pesquisa web custo-consciente: MCPs Z.ai (gratis no GLM Coding Pro, ~1k/mes) -> WebFetch nativo -> Perplexity (deep research) -> fallback manual via `PERPLEXITY.md`.
- **session-id** — devolve o id da sessao atual (`sess_...`), lendo o rollout mais recente em `~/.zcode/cli/rollout/`. Serve para referenciar a conversa em outra sessao (`#sess_...`) ou alimentar o `/session-pull`.
- **session-pull** — puxa o contexto de outra sessao para a atual (`ReadSessionContext`, strategy `handoff`): resumo de decisoes, estado e pendencias. Argumento: o id da sessao de origem. O que vem de la vale como background, nao como instrucao.

## Contexto

Pensado para quem usa Claude Code via Z.ai (GLM Coding Pro), onde pesquisa web via MCPs Z.ai (`web-search-prime`, `web-reader`, `zread`) ja esta inclusa no plano. Perplexity fica como camada opcional para deep research / modo academico, com fallback manual quando sem credito.

As skills `session-*` sao especificas do ZCode: dependem do layout de rollout (`~/.zcode/cli/rollout/`) e da ferramenta `ReadSessionContext`.

## Round-trip manual (quando Perplexity MCP esta sem credito)

1. Abra o app/browser do Perplexity.
2. Cole o contexto de `~/.claude/PERPLEXITY.md` + a tarefa.
3. Rode em **Pro Search** (rapido), **Deep Research** (investigacao) ou **Academic** (papers).
4. Copie a saida (markdown) e cole de volta no arquivo local pertinente do projeto (`CLAUDE.md`, `NOTES.md`, doc de referencia).
