# AULA 12 - N8N RESPONDENDO COMENTÁRIOS E MENSAGENS

## Detalhes

**Disciplina:** TÓPICOS ESPECIAIS EM PROGRAMAÇÃO

**Docente:** BENEVID FELIX DA SILVA

**Discente:**
- WILLEN SILVA DE SOUZA - willen.silva@unemat.br

**LINK DO GIT:** https://github.com/WillenSouza/aula-n8n/tree/main/aula12

**LINK DO POST:** https://www.instagram.com/reel/DfTRNS6NQnJ/

## O que foi feito

- Túnel ngrok com domínio fixo para o n8n isolado da aula (porta 5679).
- Webhook da Meta verificado e assinado em `comments` e `messages`.
- Três workflows (pasta `workflows/`):
  - `verificacao-webhook.json`: responde ao desafio GET da Meta (token confere ou 403).
  - `comentarios-e-direct.json`: recebe o POST, separa comentário e mensagem, filtra o post escolhido e a própria conta (trava anti-loop), responde por tabela de palavras-chave e chama o agente no Direct.
  - `direct-com-agente.json`: agente com DeepSeek (`deepseek-chat`) e memória por remetente.
- Auxiliares: `posts-da-conta.json` (lista as mídias para obter o `media.id`) e `politica-de-privacidade.json` (página exigida pela Meta para publicar o app).

## Teste verificado

- Comentário "Onde encontro o material?" de outra conta no reel: o workflow respondeu com a regra `material` e o sufixo "(resposta automática)".
- A réplica gerou um novo evento, descartado no Filter (`de_id` igual ao id da conta).
- Agente: respondeu apresentando-se como assistente automático; teste com remetente fictício falhou só no envio, porque o destinatário não existe.

## Observações

- O token de verificação foi trocado por `<TOKEN_DE_VERIFICACAO>` nos JSONs exportados.
- O PDF afirma que "material" casa com "materiais", mas não casa; a palavra `materiais` foi acrescentada à regra.
- O modelo do PDF (Groq) foi substituído por DeepSeek.
