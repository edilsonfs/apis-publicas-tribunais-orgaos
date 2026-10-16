# Tribunal de Contas do Estado de Goiás — Consulta de Decisões (acórdãos e resoluções)

> Decisões do TCE-GO.

| | |
|---|---|
| **Órgão** | TCE-GO |
| **Tipo de acesso** | 🔧 JSON do site oficial |
| **Autenticação** | Nenhuma |
| **Site oficial** | <https://decisoes.tce.go.gov.br> |
| **Domínios usados** | `iago-search-api.tce.go.gov.br` |
| **Aceita busca por palavra** | não |
| **Aceita filtro por data** | sim |
| **Verificado em** | outubro de 2026 |

## Resumo

Sem termo de busca (a ferramenta mistura busca semântica por IA): coleta por período (data da sessão) e filtros oficiais `tipo`, `ano`, `numero`, `processo`, `sessao`, `colegiado`, `relator`, `relator_processo`. Descarta summary (ementa gerada por IA), highlights, score, model e a lista de interessados. `inteiro_teor` (padrão sim) busca o texto integral em /decisions/<id> (uma requisição por decisão).

## Como a API funciona (notas verificadas ao vivo)

```text
TCE-GO — Consulta de Decisões (decisoes.tce.go.gov.br), acórdãos e resoluções.

Fonte: JSON da API oficial (iago-search-api.tce.go.gov.br) consumida pelo front-end Next.js da consulta.
Fatos verificados ao vivo em 12/10/2026:
- o front chama POST /decisions/search com corpo {term} e, na query string, page (desde 0), order
  (RELEVANCE | RECENT | OLD), cookie (identificador aleatório do navegador, dispensável), year, number, process,
  type, session, collegiate, reporter (relator da decisão), rapporteur (relator do processo), interested, start
  e end (AAAA-MM-DD, vindos do seletor de datas); GET /decisions/<id> devolve {id, text} (texto integral);
  a página de cada decisão é https://decisoes.tce.go.gov.br/view/<id>;
- sem termo (corpo {}), order=RECENT, start=2026-09-01, end=2026-09-30: página Spring com 382 itens
  (totalElements), 25 por página (size fixo), totalPages 16, `last`;
- itens: id, title, type (Acórdão, Resolução Administrativa...), indicator (AC, SA...), number, year, date
  ("28/09/2026 10:00"), collegiate, subject, process, rapporteur, decision_rapporteur, procurator, auditor,
  ementa (oficial), confidential, interested (lista de partes — não armazenada, LGPD) e campos da camada de
  IA: summary ("Ementa Artificial", gerada por IA — NÃO armazenada), highlights, score, model e track;
- a ferramenta também oferece pesquisa por termo com recursos de IA (busca semântica, avaliação "ajuda a IA a
  melhorar os resultados"); como não há garantia de busca puramente textual, o cliente NÃO envia termo:
  coleta só por período e filtros oficiais, com score/model nulos — se a resposta indicar um modelo
  (campo `model`), o cliente interrompe com erro em vez de gravar resultado semântico;
- precaução: acima de 10.000 itens o cliente pede janela menor.
```

## Uso responsável

- Faça no máximo 1 requisição por segundo (ou menos, se a nota acima pedir).
- Guarde o resultado em vez de consultar de novo a mesma coisa.
- Não tente contornar CAPTCHA, login ou bloqueio: se aparecer, pare.
- Decisões trazem nomes de pessoas: respeite a LGPD ao guardar e publicar.

[⬅ Voltar para a lista](../README.md)
