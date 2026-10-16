# Tribunal de Justiça do Ceará — jurisprudência (SJURIS)

> Jurisprudência do TJCE (SJURIS).

| | |
|---|---|
| **Órgão** | TJCE |
| **Tipo de acesso** | 🔧 JSON do site oficial |
| **Autenticação** | Nenhuma |
| **Site oficial** | <https://sjuris.tjce.jus.br/tela-consulta> |
| **Domínios usados** | `gateway.tjce.jus.br` |
| **Aceita busca por palavra** | sim |
| **Aceita filtro por data** | sim |
| **Verificado em** | outubro de 2026 |

## Resumo

Período por data de julgamento. Parâmetros `documentos` (padrão ACÓRDÃO,DECISÃO MONOCRÁTICA), `bases` (padrão 2º GRAU) e `origens` (padrão PJE,SAJ). Sem termo, envia busca='a' como o próprio front. Partes e PDF embutido são descartados. Sem link permanente por documento.

## Como a API funciona (notas verificadas ao vivo)

```text
TJCE — SJURIS, consulta de jurisprudência (sjuris.tjce.jus.br).

Fonte: JSON servido pelo gateway oficial do TJCE ao front-end Angular do SJURIS. Fatos verificados ao vivo
em 12/10/2026:
- POST https://gateway.tjce.jus.br/sjuris/api/v1/jurisprudencia/?page=N&size=M (page começa em 0; o front
  oferece 5, 10 ou 20 por página) com Origin/Referer https://sjuris.tjce.jus.br e corpo JSON em UTF-8;
- corpo montado pelo front: busca, dataJulgamento ([]), dataJulgamentoInicial/dataJulgamentoFinal (objetos
  Date serializados, ex.: 2026-10-01T03:00:00.000Z), ordenacao "order1", nomeDocumento (um tipo por vez:
  ACÓRDÃO, DECISÃO MONOCRÁTICA ou SÚMULA), baseDocumento (ex.: "2º GRAU") e origem (PJE, SAJ);
- sem palavra-chave o front envia busca="a" (termo presente em praticamente todo texto); o cliente repete;
- 01–02/10/2026, ACÓRDÃO, 2º GRAU: totalElements=668 com origem [PJE] e também com [PJE, SAJ]; a faceta
  dataJulgamento trouxe 01/10 (564) e 02/10 (104), ou seja, o último dia entra no período;
- resposta {pagina:{content[], totalElements, totalPages, ...}, filtros[]}; cada item traz id
  (processo_idDocumento), idDocumento, nomeDocumento, numeroProcesso, classe, orgaoJulgador, magistrado,
  dataJulgamento ([aaaa, m, d]), dataPublicacao ("n/d" nos vistos), ementa, conteudo (inteiro teor em texto),
  assuntos, assuntoCompleto, classeJudicial/assuntoPrincipal/orgaoJulgadorScpu (códigos), origem,
  siglaSistema, idScpu, situacaoScpu, partes (nomes e OAB — não armazenados, LGPD) e pdfAutenticadoBase64
  (PDF embutido, ~200 KB por item — não armazenado);
- não há link permanente por documento: o link aponta para a tela de consulta.
```

## Uso responsável

- Faça no máximo 1 requisição por segundo (ou menos, se a nota acima pedir).
- Guarde o resultado em vez de consultar de novo a mesma coisa.
- Não tente contornar CAPTCHA, login ou bloqueio: se aparecer, pare.
- Decisões trazem nomes de pessoas: respeite a LGPD ao guardar e publicar.

[⬅ Voltar para a lista](../README.md)
