# Tribunal de Contas do Estado do Ceará — Contexto (acórdãos, decisões e pareceres prévios)

> Documentos do TCE-CE.

| | |
|---|---|
| **Órgão** | TCE-CE |
| **Tipo de acesso** | 🔧 JSON do site oficial |
| **Autenticação** | Nenhuma |
| **Site oficial** | <https://www.tce.ce.gov.br/contexto/> |
| **Domínios usados** | `contexto-api.tce.ce.gov.br` |
| **Aceita busca por palavra** | sim (obrigatória) |
| **Aceita filtro por data** | sim |
| **Verificado em** | outubro de 2026 |

## Resumo

Exige termo. Período pela data de finalização do documento (dtfinalizado), aplicado no cliente sobre a lista em ordem decrescente. Parâmetro `tipos` (códigos idtipodocumento; padrão 4,687,25,633 = acórdão, acórdão retificador, parecer prévio, decisão) e `exata` (busca pela expressão exata). A fonte só devolve o começo do texto: guarda-se a ementa a partir desse trecho e o link do PDF oficial; interessados descartados.

## Como a API funciona (notas verificadas ao vivo)

```text
TCE-CE — Contexto, consulta textual de documentos (www.tce.ce.gov.br/contexto).

Fonte: JSON da API oficial do Contexto (contexto-api.tce.ce.gov.br) consumida pelo front-end da ferramenta.
Fatos verificados ao vivo em 12/10/2026:
- POST https://contexto-api.tce.ce.gov.br/documentos/buscar com corpo {texto, filtros, searchAfterSort,
  buscaPalavraExata, buscaPesquisaExata, sort}; resposta {erros:[], data:{tempo, tamanho, lista[], agregacao}};
  `tamanho` satura em 10.000 e cada página traz 10 itens; a página seguinte repete o corpo com
  searchAfterSort = campo `sort` do último item ([instante de dtfinalizado em ms, iddocumento]);
- `filtros` são cláusulas do Elasticsearch montadas pelo front; {"terms":{"idtipodocumento":[...]}} funciona
  ("licitação" + tipos 4, 687, 25, 633: 8.722 documentos — 8.690 acórdãos, 20 decisões, 12 pareceres prévios);
  a tabela GET /tabelas-auxiliares/tipo-documento dá os códigos (4 ACÓRDÃO, 687 ACÓRDÃO RETIFICADOR,
  25 PARECER PRÉVIO, 633 DECISÃO, 3 RESOLUÇÃO, 160 SÚMULA...);
- o intervalo por data da sessão ({"range":{"dtsessao":{...}}}) devolveu 0 itens porque dtsessao vem nulo nos
  documentos; com sort "desc" a lista vem por dtfinalizado decrescente, então o período (data de finalização
  do documento) é aplicado no cliente, parando ao passar do início;
- texto vazio não foi validado ao vivo; por segurança o cliente exige termo;
- o front escapa o texto antes de enviar ("/" vira espaço; ":" e aspas são escapados) porque aspas cruas
  quebram a busca (HTTP 200 com erro); o cliente escapa da mesma forma e trata `erros` não vazios como erro;
- cada item traz iddocumento, dtfinalizado, nmtipodocumento, nrdocumento, nranodocumento, idprocesso,
  nrprocesso, dtentradaprocesso, dtsessao, tpsessao, esferajulgamento, dsentidade, dslocalidade, dsespecie,
  nmsetor, nmmembrorelator, dsdocumento (caminho do PDF), conteudo (só os ~1.000 primeiros caracteres do
  documento, com cabeçalho e nomes das partes), highlight e nminteressado (não armazenado, LGPD);
- o PDF oficial é baixado em https://api-add.tce.ce.gov.br/arquivos/documento?documento_id=<iddocumento>;
- como `conteudo` é só o começo do documento, o cliente guarda como ementa o trecho a partir de "EMENTA"
  (marcando quando pode estar truncado) e não preenche inteiro teor (o texto integral está no PDF).
```

## Uso responsável

- Faça no máximo 1 requisição por segundo (ou menos, se a nota acima pedir).
- Guarde o resultado em vez de consultar de novo a mesma coisa.
- Não tente contornar CAPTCHA, login ou bloqueio: se aparecer, pare.
- Decisões trazem nomes de pessoas: respeite a LGPD ao guardar e publicar.

[⬅ Voltar para a lista](../README.md)
