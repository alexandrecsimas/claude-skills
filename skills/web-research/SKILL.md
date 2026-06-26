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
4. **Fallback manual** — se Perplexity MCP falhar e a tarefa precisar de profundidade: oriente o usuario a abrir o app/browser do Perplexity, colar a tarefa junto com o conteudo de `~/.claude/PERPLEXITY.md` (contexto + template de round-trip), rodar em Deep Research/Academic, e trazer o markdown de volta ao projeto. **Antes de colar no Perplexity (servico externo), generalize ou remova detalhes sensiveis** — nomes internos de sistemas/projetos, topologia de infra, credenciais, dados pessoais ou de producao (ver secao Privacidade).

## Privacidade e nao-exposicao
- Tudo que voce envia a servicos externos (Perplexity; `webSearchPrime`/`webReader` via Z.ai) pode ser processado e armazenado por eles. **Nunca inclua** credenciais, segredos, dados pessoais (LGPD) ou detalhes sensiveis de projetos e instituicoes (nomes internos de sistemas, topologia de infra, clientes, dados de producao).
- No round-trip pro Perplexity, generalize o contexto privado antes de colar (ex: troque nomes de sistemas internos por descricoes genericas como "sistema X em Laravel"; resuma em vez de copiar trechos de codigo proprietario).
- Skills, configuracoes e docs destinadas a **repos publicos** (ex: o proprio repo desta skill) nunca devem mencionar projetos, clientes ou instituicoes especificas — mantenham-se genéricas.

## Economia de quota
- Uma consulta por subproblema; reutilize o resultado no mesmo contexto.
- Se ja tem a URL, use `webReader` em vez de `webSearchPrime`.
- Nao pesquise para "confirmar" o que voce ja sabe com confianca.
- Logs/changelogs locais vem antes de qualquer busca.
