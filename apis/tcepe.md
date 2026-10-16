# Tribunal de Contas do Estado de Pernambuco — jurisprudência (deliberações)

> Deliberações do TCE-PE.

| | |
|---|---|
| **Órgão** | TCE-PE |
| **Tipo de acesso** | 🔧 JSON do site oficial |
| **Autenticação** | Nenhuma |
| **Site oficial** | <https://portal.tcepe.tc.br/jurisprudencia/consulta/deliberacoes> |
| **Domínios usados** | `portal.tcepe.tc.br` |
| **Aceita busca por palavra** | sim |
| **Aceita filtro por data** | sim |
| **Verificado em** | outubro de 2026 |

## Resumo

Período pela data de julgamento (filtro da própria fonte). Parâmetros opcionais: `exata` (expressão exata), `modalidade`, `tipo_processo`, `relator`, `unidade_gestora`, `orgao_julgador`, `processo`. Inteiro teor vem na busca; links do e-TCE (http) guardados como fornecidos. Intermediário TLS Thawte em repositório de certificados confiáveis.

## Como a API funciona (notas verificadas ao vivo)

```text
TCE-PE — portal de jurisprudência, base de deliberações (portal.tcepe.tc.br/jurisprudencia).

Fonte: JSON da API pública do portal (aplicação JHipster) consumida pelo front-end Angular oficial.
Fatos verificados ao vivo em 12/10/2026:
- GET https://portal.tcepe.tc.br/jurisprudencia/services/jurisprudencia/api/publico/deliberacoes devolve a lista
  de deliberações e o total no cabeçalho X-Total-Count;
- o 400 {"message": null} com só page/size/termo/sort vinha da ordenação errada e da falta dos parâmetros que o
  front sempre envia: o componente de resultados monta page, size, todasBaseDescricao.equals, todasBaseExprExata.equals,
  modalidade.in, tipoProcesso.in, relator.contains, unidadeGestora.equals, orgaoJulgador.equals,
  numeroProcesso.equals, acordao.equals, decisao.equals, parecerPrevio.equals, inteiroTeor.equals (booleanos,
  false por padrão), dataJulgamentoInicio.equals, dataJulgamentoFim.equals (AAAA-MM-DD), numeroDeliberacao.equals,
  anoDeliberacao.in e sort=dataJulgamentoProcesso,desc — vazios inclusive;
- 01–30/09/2026 sem termo: X-Total-Count 275, com julgamentos de 30/09 na primeira página (fim inclusivo);
- cada item traz nomeTipoDocumento (ACORDAO/PARECER/DECISAO), numeroProcessoProcesso, anoProcessoProcesso,
  numeroDeliberacaoProcesso, anoDeliberacaoProcesso, codigoDeliberacaoProcesso, codigoInteiroteorProcesso,
  origemProcessoProcesso (ETCE), dataJulgamentoProcesso, descricaoTipoProcessoProcesso, modalidadeProcesso,
  descricaoParecerProcesso (inteiro teor da deliberação em HTML simples), descricaoItdProcesso,
  detalheProcessoNomeUnidadeJurisdicionada, detalheProcessoNomeOrgaoJulgador, detalheProcessoNomeServidor
  (relator), links oficiais do e-TCE (linkConsultaProcesso, linkDocumentoDeliberacao, linkDocumentoITD, em http)
  e códigos de validação;
- o texto já vem na busca, então o cliente não chama conteudo-documento; a tela "baixar documento" do portal usa
  reCAPTCHA e não é usada;
- precaução: acima de 10.000 resultados o cliente pede janela menor;
- o intermediário TLS Thawte (cadeia incompleta) deve ser acrescentado ao repositório de certificados confiáveis do seu cliente.
```

## Uso responsável

- Faça no máximo 1 requisição por segundo (ou menos, se a nota acima pedir).
- Guarde o resultado em vez de consultar de novo a mesma coisa.
- Não tente contornar CAPTCHA, login ou bloqueio: se aparecer, pare.
- Decisões trazem nomes de pessoas: respeite a LGPD ao guardar e publicar.

[⬅ Voltar para a lista](../README.md)
