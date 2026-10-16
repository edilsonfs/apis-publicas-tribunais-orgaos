# Tribunal Regional Federal da 5ª Região — jurisprudência (Julia)

> Jurisprudência do TRF da 5ª Região e turmas recursais.

| | |
|---|---|
| **Órgão** | TRF5 |
| **Tipo de acesso** | 🔧 JSON do site oficial |
| **Autenticação** | Nenhuma |
| **Site oficial** | <https://juliapesquisa.trf5.jus.br/julia-pesquisa/> |
| **Domínios usados** | `juliapesquisa.trf5.jus.br` |
| **Aceita busca por palavra** | sim |
| **Aceita filtro por data** | sim |
| **Verificado em** | outubro de 2026 |

## Resumo

Período = data de julgamento ou de publicação (critério da própria fonte). Parâmetro `origens` (padrão: G2,TR_AL,TR_CE,TR_PB,TR_PE,TR_RN,TR_SE,TRU); filtros opcionais numeroProcesso, orgaoJulgador e relator. Sem 1º grau (G1 recusa a consulta). Sem link permanente por documento.

## Como a API funciona (notas verificadas ao vivo)

```text
TRF5 — Julia Pesquisa (jurisprudência do TRF da 5ª Região e das Turmas Recursais).

Fonte: JSON servido pelo próprio portal juliapesquisa.trf5.jus.br ao front-end (DataTables no modo
servidor). Fatos verificados ao vivo em 12/10/2026:
- GET /julia-pesquisa/api/v1/documento:dt/{origem} com os parâmetros do DataTables (draw, start, length e
  columns[0][data]=codigoDocumento, com os colchetes codificados) e os filtros pesquisaLivre,
  numeroProcesso, orgaoJulgador, relator, dataIni e dataFim (vazios quando não usados);
- datas em dd/mm/aaaa (o js/pesquisa.js só repassa o campo do formulário); o campo `criteria` da resposta
  confirma "julgamento/publicação entre 01/09/2026 e 30/09/2026" e G2 devolveu 8.080 documentos no mês;
- origens: G2 e TR_<seção> (AL, CE, PB, PE, RN, SE), montadas pelo js como 'TR' + '_' + seção, e TRU
  (G2 e TR_PE consultadas ao vivo; nas TRs o campo `orgao` do item é a seção, ex.: JFPE);
  G1 responde 400 ("parâmetro com formato inválido") com estes parâmetros e fica fora do padrão;
- resposta {draw, recordsTotal, recordsFiltered, data[], error, criteria}; recordsTotal satura em 10.000;
- o índice tem atraso: em 12/10/2026 o G2 não tinha nenhum documento de 01–02/10/2026;
- cada item traz codigoDocumento (estável), tipoDocumento ("EMENTA" nos itens vistos), numeroProcesso,
  classeJudicial, relator, orgaoJulgador, dataJulgamento, dataAssinatura (aaaa-mm-dd), texto (documento
  completo, com cabeçalho e partes), decisao, indexacao, referenciasLegislativas, votantes, publicacoes,
  doutrinas e url (nula nos itens vistos). Não há link permanente: o link aponta para a pesquisa.
```

## Uso responsável

- Faça no máximo 1 requisição por segundo (ou menos, se a nota acima pedir).
- Guarde o resultado em vez de consultar de novo a mesma coisa.
- Não tente contornar CAPTCHA, login ou bloqueio: se aparecer, pare.
- Decisões trazem nomes de pessoas: respeite a LGPD ao guardar e publicar.

[⬅ Voltar para a lista](../README.md)
