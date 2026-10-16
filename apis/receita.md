# Receita Federal — atos normativos (SIJUT2)

> Instruções normativas, soluções de consulta e atos da Receita.

| | |
|---|---|
| **Órgão** | RFB |
| **Tipo de acesso** | 🔧 JSON do site oficial |
| **Autenticação** | Nenhuma |
| **Site oficial** | <https://normasinternet2.receita.fazenda.gov.br/> |
| **Domínios usados** | `normas.receita.fazenda.gov.br`, `normasinternet2.receita.fazenda.gov.br` |
| **Aceita busca por palavra** | sim |
| **Aceita filtro por data** | sim |
| **Verificado em** | outubro de 2026 |

## Resumo

Período = data de publicação. Uma requisição extra por ato para o texto (visão multivigente; trechos tachados, já revogados, ficam fora do inteiro_teor). parametros: tipos e orgaos (siglas, nomes ou ids: IN,SC,ADI / Cosit,PGFN), ano, numero, vigentes=true. Portaria de Pessoal, Edital de Intimação e Termo de Exclusão do Simples ficam fora salvo tipos explícito ou tipos=todos.

## Como a API funciona (notas verificadas ao vivo)

```text
Receita Federal — SIJUT2 (Normas): atos infralegais (IN, Portaria, Solução de Consulta, ADI, Parecer Normativo...).

Fonte: JSON servido pelo próprio portal oficial (normas.receita.fazenda.gov.br e normasinternet2), sem
autenticação e sem CAPTCHA. Fatos verificados ao vivo em 12/10/2026:
- POST https://normas.receita.fazenda.gov.br/api/indexacao/ato/pesquisar (JSON): tipoPesquisa
  ("formulario" sem termo, "relevancia" com termo), termo, tipoData "dataPublicacao", dataInicio/dataFim
  em dd/MM/aaaa, anoAto, numeroAto, apenasAtosVigentes, internet true, orgaosSelecionados e
  tiposAtosSelecionados (ids separados por ";"), paginacaoPaginaAtual, paginacaoQuantidadePorPagina,
  ordenacaoColuna/ordenacaoDirecao, skipAggregations; resposta: atos[] (idAto, numeroAto, anoAto,
  dataAto, dataPublicacao, tipoAto{idTipoAto, siglaTipoAto, nomeTipoAto}, orgaos[], ementa em HTML,
  vigente, resumoRevogado, revigorado, tipoSolucao, urlVisualizacao), quantidadeTotal, quantidadePaginas;
  ex.: 08 a 09/10/2026 -> 44 atos; "Selo Sintonia" + tipos 9;42 -> 2 atos;
- GET /api/tipoAto/ativo: 44 tipos (IN = 42, SC = 72, Parecer Normativo = 59, Portaria = 57, ADI = 10...);
  GET /api/orgao/ativo: órgãos (Cosit = 111, PGFN = 222);
- GET https://normasinternet2.receita.fazenda.gov.br/api/consulta-externa/ato/{idAto}/visao/multivigente:
  epigrafeCompleta, dadosPublicacao ("Publicado(a) no DOU de 09/10/2026, seção 1, página 35"),
  dataPublicacao, dataVigenciaInicio, vigente, ementas[] e outrosSegmentos[] (textoIntegra, omitir, tachado);
- caminhos /api/ato/... e /api/auth/... respondem 403 (uso interno autenticado): não são usados.
A busca é Elasticsearch ("indexacao"): recortes com 10.000+ atos são recusados como saturação.
```

## Uso responsável

- Faça no máximo 1 requisição por segundo (ou menos, se a nota acima pedir).
- Guarde o resultado em vez de consultar de novo a mesma coisa.
- Não tente contornar CAPTCHA, login ou bloqueio: se aparecer, pare.
- Decisões trazem nomes de pessoas: respeite a LGPD ao guardar e publicar.

[⬅ Voltar para a lista](../README.md)
