# Tribunal de Justiça do Pará — jurisprudência

> Jurisprudência do TJPA.

| | |
|---|---|
| **Órgão** | TJPA |
| **Tipo de acesso** | 🔧 JSON do site oficial |
| **Autenticação** | Nenhuma |
| **Site oficial** | <https://jurisprudencia.tjpa.jus.br/> |
| **Domínios usados** | `jurisprudencia.tjpa.jus.br` |
| **Aceita busca por palavra** | sim (obrigatória) |
| **Aceita filtro por data** | sim |
| **Verificado em** | outubro de 2026 |

## Resumo

Exige termo (o próprio front recusa pesquisa vazia). Período por data de julgamento. Parâmetros `escopo` (ementa | inteiro_teor; padrão ementa), `tipos` e `origens` (descrições do portal, ex.: 'Acórdão', 'Tribunal de Justiça do Estado do Pará'; padrão sem filtro). Ordenação só por relevância. Campos temas/indexacao não são armazenados.

## Como a API funciona (notas verificadas ao vivo)

```text
TJPA — Jurisprudência do TJPA (jurisprudencia.tjpa.jus.br).

Fonte: JSON servido pelo BFF oficial ao front-end Angular do portal. Fatos verificados ao vivo em 12/10/2026:
- POST https://jurisprudencia.tjpa.jus.br/bff/api/decisoes/buscar com Origin/Referer do próprio portal e corpo
  JSON {query, queryType "free", queryScope "ementa" | "inteiroTeor", origem[], tipo[], dataJulgamentoInicio,
  dataJulgamentoFim (AAAA-MM-DD), page (começa em 0), size (o front usa 25), sortBy "relevancia" (único aceito),
  sortOrder "desc"}; o front também monta dataPublicacaoInicio/Fim, classe, assunto, relatores e
  orgaoJulgadorColegiado;
- o front recusa pesquisa sem termo ("Não é possível pesquisar sem o termo de busca"): o cliente exige termo;
- `origem` e `tipo` levam as descrições servidas por /bff/api/decisoes/filtros (ex.: tipo "Acórdão"), não os
  códigos internos 74/64 — com tipo ["74", "64"] a busca devolveu 0; sem `origem` e `tipo` não há filtro;
- termo "direito", julgamento de 28/09 a 02/10/2026: totalElements=398 (os 3 primeiros julgados em 29/09); já o
  período 29–30/09/2026 devolveu itens julgados em 01/10/2026 — o cliente descarta itens fora do período pedido;
- resposta {message, data:{content[], totalElements, totalAcordaos, totalDecisoesMonocraticas, totalPages,
  currentPage, size, facets, consultaUtilizada, excedeuLimiteTecnico, limiteMaximo, mensagemLimiteTecnico}};
- cada item traz id, numeroprocesso (CNJ já formatado), tipo ("Acórdão"), area, origem, sistemaorigem, classe
  {nome, codigo}, assuntos[], orgaojulgador (gabinete), orgaojulgadorcolegiado, competencia, especie, pessoas
  (relator), datajulgamento, datadocumento, datapublicacao (nula nos itens vistos), sentidodecisao,
  ementatextopuro (ementa em texto), textoementa (HTML), textopuro (inteiro teor em texto), textooriginal (HTML),
  trechos destacados e hashstorage;
- link permanente montado pelo front: https://jurisprudencia.tjpa.jus.br/documento/<id>.
Os campos temas e indexacao (vazios nos itens vistos; o portal tem módulo de IA) não são armazenados.
```

## Uso responsável

- Faça no máximo 1 requisição por segundo (ou menos, se a nota acima pedir).
- Guarde o resultado em vez de consultar de novo a mesma coisa.
- Não tente contornar CAPTCHA, login ou bloqueio: se aparecer, pare.
- Decisões trazem nomes de pessoas: respeite a LGPD ao guardar e publicar.

[⬅ Voltar para a lista](../README.md)
