---
name: session-pull
description: Puxa o contexto de outra sessão do ZCode para esta (handoff). Argumento id da sessão de origem (sess_...). Use quando o usuário citar um id de sessão ou pedir para trazer o contexto de outra conversa.
---

# Session Pull

Argumento `$ARGUMENTS`: id da sessão de origem (`sess_...`). Se vier vazio,
peça o id ao usuário — ele pega com `/session-id` na sessão de origem.

1. Normalize: remova `#`, aspas e espaços em volta; valide o formato `sess_`
   seguido de `[A-Za-z0-9._-]`. Se não casar, mostre o que recebeu e peça de
   novo — não adivinhe o id.

2. Chame a ferramenta `ReadSessionContext` com:
   - `sessionId`: o id normalizado
   - `strategy`: `"handoff"`
   - `maxTokens`: 12000
   - `query`: "Handoff desta sessão: decisões tomadas, estado final do
     trabalho, pendências, caminhos de arquivos relevantes e próximos passos
     combinados."

3. Entregue um resumo enxuto ao usuário (decisões → estado → pendências) e
   deixe claro que dali em diante isso vale como background da conversa — não
   como instrução a re-executar automaticamente.

4. Se o `ReadSessionContext` falhar (id inexistente, sessão não persistida),
   mostre o erro, e sugira confirmar o id com `/session-id` na sessão de
   origem antes de tentar de novo.
