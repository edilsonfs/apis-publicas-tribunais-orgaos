# Tribunal de Contas do Estado do Rio Grande do Sul — jurisprudência (decisões)

> Decisões do TCE-RS.

| | |
|---|---|
| **Órgão** | TCE-RS |
| **Tipo de acesso** | 🔧 JSON do site oficial |
| **Autenticação** | Nenhuma |
| **Site oficial** | <https://portal.tce.rs.gov.br/app/pesquisa/jurisprudencia/> |
| **Domínios usados** | `portal.tce.rs.gov.br` |
| **Aceita busca por palavra** | sim |
| **Aceita filtro por data** | sim |
| **Verificado em** | outubro de 2026 |

## Resumo

Base Decisões (índice jurisprudencia-decisoes). Período pela data da sessão (filtro da própria fonte); termo opcional com operadores E, OU, NÃO. Inteiro teor = relatório e voto; links do visualizador oficial.

## Como a API funciona (notas verificadas ao vivo)

```text
TCE-RS — Plataforma de Pesquisa de Jurisprudência, base Decisões (portal.tce.rs.gov.br/app/pesquisa/jurisprudencia).

Fonte: JSON do middleware oficial de pesquisa (Elasticsearch) usado pelo front-end Angular da plataforma.
Fatos verificados ao vivo em 12/10/2026:
- a configuração pública assets/config/app.config.json lista as bases e, para "decisoes", tipoServicoIndexacao
  "elasticsearch", urlMiddleware "/api/pesquisa/v2", indice "jurisprudencia-decisoes", 10 resultados por página,
  ordenação padrão por dt_sessao desc, operadores E/OU/NÃO/~/$ e os campos pesquisáveis (nr_processo, ementa,
  relatório, decisão...); há também as bases sumulas, pareceres e informacoes_ct (não coletadas aqui);
- o serviço do front faz POST <urlMiddleware>/<indice>/<página, desde 1> com o objeto de parâmetros {termos,
  filtros, opcoes, camposPesquisaveis, totalizadoresCampos}; o filtro de data da sessão é
  {campo:"dt_sessao", tipo:"data", valores:[], inicio, fim} com datas serializadas em ISO (meia-noite de
  Brasília = 03:00Z); as opções incluem quantidadeResultadosPorPagina, ordenacaoCampo e ordenacaoDirecao;
- 01–30/09/2026 sem termo, ordenado por dt_sessao desc: {resultados:{total:{valor:31, relacao:"EQUAL_TO"},
  paginaAtual, resultados:[{id, score, campos}]}}; o termo vazio é aceito (o front mostra "(sem termos)");
- `campos` traz nr_processo_fmt, ds_tp_processo, orgao (órgão fiscalizado), nm_orgao_julgador, nm_magistrado
  (relator), nm_gabinete, dt_sessao, nr_sessao, ano_sessao, publicacao_dt_publicacao, texto_ementa (às vezes
  nula), relatorio (relatório e voto em texto), texto (decisão resumida, ex.: "Multa"), dec_descricao,
  link_visualizador_decisao e link_visualizador_relatorio_voto (visualizador anônimo oficial);
- relação diferente de EQUAL_TO (GREATER_THAN_OR_EQUAL_TO) indica total saturado: o cliente pede janela menor;
- o termo segue as regras do front: "-" e "/" escapados, operadores E/OU/NÃO convertidos para &, |, !.
```

## Uso responsável

- Faça no máximo 1 requisição por segundo (ou menos, se a nota acima pedir).
- Guarde o resultado em vez de consultar de novo a mesma coisa.
- Não tente contornar CAPTCHA, login ou bloqueio: se aparecer, pare.
- Decisões trazem nomes de pessoas: respeite a LGPD ao guardar e publicar.

[⬅ Voltar para a lista](../README.md)
