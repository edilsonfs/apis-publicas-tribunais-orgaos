# Tribunal de Contas do Estado de Santa Catarina — jurisprudência (deliberações e decisões singulares)

> Jurisprudência do TCE-SC.

| | |
|---|---|
| **Órgão** | TCE-SC |
| **Tipo de acesso** | 🔧 JSON do site oficial |
| **Autenticação** | Nenhuma |
| **Site oficial** | <https://virtual.tce.sc.gov.br/jurisprudencia/jurisprudencia> |
| **Domínios usados** | `api.virtual.tce.sc.gov.br` |
| **Aceita busca por palavra** | sim (obrigatória) |
| **Aceita filtro por data** | sim |
| **Verificado em** | outubro de 2026 |

## Resumo

Exige termo (como o formulário oficial). Período aplicado no cliente pela data da sessão (filtros de data da fonte não funcionam porque dataSessao vem nula). Parâmetros: `bases` (deliberacoes,singulares; padrão as duas) e `abrangencia` (INTEIRO_TEOR ou EMENTA). Inteiro teor = relatório e voto; PDF oficial no storage.

## Como a API funciona (notas verificadas ao vivo)

```text
TCE-SC — Portal da Jurisprudência, pesquisa integrada (virtual.tce.sc.gov.br/jurisprudencia).

Fonte: GraphQL oficial (api-gateway/ms-jurisprudencia) usado pelo micro front-end "@tce/jurisprudencia".
Fatos verificados ao vivo em 12/10/2026:
- POST https://api.virtual.tce.sc.gov.br/api-gateway/ms-jurisprudencia/graphql; a introspecção está aberta e
  expõe pesquisarJurisprudencia(filtro: JurisprudenciaFiltroInput!) -> {totalResultados, pagina, tamanhoPagina,
  resultados[], facets}; o filtro aceita textoBusca, abrangencia (INTEIRO_TEOR | EMENTA), ordenacao
  (RELEVANCIA | MAIS_RECENTES | MAIS_ANTIGOS), pagina (desde 0), tamanhoPagina, decisaoSingular, numeroProcesso,
  numeroDecisao, identificadores de relator/unidade/tipo e datas de autuação, sessão e publicação (dd/mm/aaaa);
- o formulário oficial exige textoBusca (mínimo de 3 caracteres) e separa deliberações (decisaoSingular=false)
  de decisões singulares (true); o cliente também exige termo e consulta as duas bases;
- "licitação", INTEIRO_TEOR, deliberações, MAIS_RECENTES: 5.965 resultados; os itens vêm com dataSessao e
  dataPublicacao nulos e, por isso, os filtros dataSessaoInicio/Fim devolvem 0 (testado com e sem termo):
  o período é aplicado no cliente pela data da sessão lida na referência oficial (textoCopiarEmenta, ex.:
  "TCE/SC, Sessão Sessão Ordinária em Ambiente Virtual, Decisão: n. 199/2026, ..., Sessão: 11/09/2026.") ou,
  na falta dela, por dataDecisao; como a ordem "mais recentes" acompanha a sessão e não a dataDecisao, a parada
  antecipada só ocorre quando uma página inteira é anterior ao início do período com 30 dias de folga;
- cada resultado traz numeroProcesso, processoNumeroFormatado, linkProcesso (virtual.tce.sc.gov.br),
  relator, unidadeGestora[], tipoProcesso, dataDecisao, ementa, votoTexto (relatório e voto, com marcações
  <mark> do realce, removidas), textoCopiarEmenta e documentos[] com linkPublico em storage.tce.sc.gov.br;
  linkDocumento aponta para um ambiente de homologação (virtual.qa.tce.sc.gov.br) e não é usado;
- precaução: o cliente não pagina além de 10.000 resultados e pede refinamento (de imediato quando não há
  início de período que permita parar antes).
```

## Uso responsável

- Faça no máximo 1 requisição por segundo (ou menos, se a nota acima pedir).
- Guarde o resultado em vez de consultar de novo a mesma coisa.
- Não tente contornar CAPTCHA, login ou bloqueio: se aparecer, pare.
- Decisões trazem nomes de pessoas: respeite a LGPD ao guardar e publicar.

[⬅ Voltar para a lista](../README.md)
