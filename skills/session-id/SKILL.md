---
name: session-id
description: Devolve o id da sessão atual (sess_...) para referenciar em outra conversa com #sess_... ou para usar com /session-pull. Use quando o usuário pedir o id desta sessão.
---

# Session ID

Objetivo: devolver ao usuário o id da sessão atual, no formato `sess_...`.

1. Rode no shell:

   ```
   ls -t ~/.zcode/cli/rollout/model-io-sess_*.jsonl | head -1 | sed 's/.*model-io-\(sess_.*\)\.jsonl/\1/'
   ```

   O arquivo mais recentemente modificado é o desta sessão — invocar este
   comando acabou de escrever nele.

2. Desempate (só se houver suspeita de outra sessão ativa escrevendo em
   paralelo): confira se o arquivo contém um trecho marcante das últimas
   mensagens desta conversa (grep por uma frase recente e característica do
   usuário). Se não contiver, teste o próximo arquivo mais novo.

3. Responda curto: o id num bloco de código + uma linha de uso — mencionar
   `#<id>` em outra conversa (ou chamar `/session-pull <id>` lá) permite puxar
   este contexto. Não imprima caminhos de disco nem trechos da conversa.
