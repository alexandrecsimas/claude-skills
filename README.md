# claude-skills

Skills pessoais para Claude Code, distribuidas como marketplace de plugin.

## Instalacao

No Claude Code:

```
/plugin marketplace add alexandrecsimas/claude-skills
/plugin install web-research@xandy-skills
```

## Skills

- **web-research** — politica de roteamento de pesquisa web custo-consciente: MCPs Z.ai (gratis no GLM Coding Pro, ~1k/mes) -> WebFetch nativo -> Perplexity (deep research) -> fallback manual via `PERPLEXITY.md`.

## Contexto

Pensado para quem usa Claude Code via Z.ai (GLM Coding Pro), onde pesquisa web via MCPs Z.ai (`web-search-prime`, `web-reader`, `zread`) ja esta inclusa no plano. Perplexity fica como camada opcional para deep research / modo academico, com fallback manual quando sem credito.

## Round-trip manual (quando Perplexity MCP esta sem credito)

1. Abra o app/browser do Perplexity.
2. Cole o contexto de `~/.claude/PERPLEXITY.md` + a tarefa.
3. Rode em **Pro Search** (rapido), **Deep Research** (investigacao) ou **Academic** (papers).
4. Copie a saida (markdown) e cole de volta no arquivo local pertinente do projeto (`CLAUDE.md`, `NOTES.md`, doc de referencia).
