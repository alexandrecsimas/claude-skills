---
name: web-research
description: Roteia pesquisa web de forma custo-consciente. Use quando precisar de informacao atual/externa da web — precos, planos, CVEs/security advisories, changelogs, release notes, breaking changes, comparacoes (X vs Y), docs/API de versao especifica, status de servico, ou qualquer mencao a "latest/atual/recente/2026". NAO use para o que esta no repositorio local, raciocinio, refatoracao ou escrita de codigo.
---

# Web Research — politica de roteamento

## Quando buscar na web
- Fatos atuais: "latest", "atual", "recente", ano corrente ou futuro
- Mercado: pricing, planos, "compare X vs Y", benchmark
- Seguranca: CVE, security advisory, vulnerabilidade
- Upstream: changelog, release notes, breaking changes, docs/API nova
- Operacao: status/incidente/downtime de servico

## Quando NAO buscar (resolva local)
- Resposta esta nos arquivos do projeto/repositorio
- Raciocinio arquitetural, design, brainstorming, opiniao tecnica
- Refatoracao, escrita/revisao de codigo, troubleshooting de logs locais
- Explicacao conceitual atemporal

## Camadas de busca (nesta ordem — mais barato primeiro)
1. **MCPs Z.ai** — `webSearchPrime` (busca), `webReader` (fetch de 1 URL), `zread` (repo open-source). Gratis no GLM Coding Pro, ~1.000 calls/mes. Padrao para quase tudo.
2. **WebFetch / WebSearch nativos** — quando MCPs Z.ai indisponiveis ou for fetch de URL ja conhecida.
3. **Perplexity MCP** (`perplexity_ask` / `perplexity_research` / `perplexity_reason`) — **so se** (a) tiver credito (nao retornar 401 quota) **e** (b) for deep research multi-fonte ou modo academico. Custo alto.
4. **Fallback manual** — se Perplexity MCP falhar e a tarefa precisar de profundidade: oriente o usuario a abrir o app/browser do Perplexity, colar a tarefa junto com o conteudo de `~/.claude/PERPLEXITY.md` (contexto + template de round-trip), rodar em Deep Research/Academic, e trazer o markdown de volta ao projeto.

## Economia de quota
- Uma consulta por subproblema; reutilize o resultado no mesmo contexto.
- Se ja tem a URL, use `webReader` em vez de `webSearchPrime`.
- Nao pesquise para "confirmar" o que voce ja sabe com confianca.
- Logs/changelogs locais vem antes de qualquer busca.
