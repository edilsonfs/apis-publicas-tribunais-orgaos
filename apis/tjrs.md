# Tribunal de Justiça do Rio Grande do Sul — jurisprudência

> Jurisprudência do TJRS com íntegra.

| | |
|---|---|
| **Órgão** | TJRS |
| **Tipo de acesso** | 🔧 JSON do site oficial |
| **Autenticação** | Nenhuma |
| **Site oficial** | <https://www.tjrs.jus.br/buscas/jurisprudencia/?aba=jurisprudencia> |
| **Domínios usados** | `www.tjrs.jus.br` |
| **Aceita busca por palavra** | sim |
| **Aceita filtro por data** | sim |
| **Verificado em** | outubro de 2026 |

## Resumo

Período por data de julgamento (parâmetro `campo_data`=publicacao usa a data de publicação). Parâmetros `conteudo` (ementa | inteiro_teor; padrão ementa) e `tipos` (acordao, monocratica, admissibilidade, duvida; padrão todos). Íntegra decodificada do base64 da própria resposta; sem link permanente. Documentos com ind_segredo_justica='S' recebem metadados.segredo_justica=True.

## Como a API funciona (notas verificadas ao vivo)

```text
TJRS — consulta de jurisprudência (www.tjrs.jus.br/buscas/jurisprudencia).

Fonte: JSON do Solr devolvido pelo ajax.php oficial ao front-end AngularJS/jQuery da pesquisa. Fatos verificados
ao vivo em 12/10/2026:
- POST https://www.tjrs.jus.br/buscas/jurisprudencia/ajax.php (formulário) com action=consultas_solr_ajax,
  metodo=buscar_resultados e parametros=<form#form_busca serializado>; a resposta vem como text/html, mas o corpo
  é JSON ({responseHeader, response:{numFound, start, docs[]}, facet_counts, url, query, filtro, ...}; erro de
  sintaxe vem em `error`);
- campos do formulário (página ?aba=jurisprudencia): aba, realizando_pesquisa, pagina_atual (1, 2, ...),
  q_palavra_chave, conteudo_busca (ementa_completa | documento_text), filtroTribunal/filtroRelator/... (-1 =
  todos), data_julgamento_de/_ate e data_publicacao_de/_ate (dd/mm/aaaa), caixas filtroacordao=acordao,
  filtroMonocratica=monocratica, filtroAdmissibilidade=admissibilidade, filtroDuvida=duvida, facet*, wt=json,
  ordem=desc; o front valida as datas no formato d/m/aaaa;
- 10 documentos por página (rows=10, ordenação data_julgamento desc); sem termo o Solr recebe ementa_completa:*;
- julgamento em 01/10/2026, sem termo: numFound=773, todos com data_julgamento 2026-10-01; ~1 MB por página
  porque cada documento traz a íntegra;
- cada doc traz cod_ementa (chave usada pelo front), numero_processo (20 dígitos), tipo_documento ("Monocratica",
  "Acordao"...), tipo_processo, nome_classe_cnj, nome_assunto_cnj, nome_relator, orgao_julgador, origem
  (comarca), secao, nome_tribunal, data_julgamento/data_publicacao (ISO, 03:00Z), ind_segredo_justica,
  ementa_completa (lista; o campo `ementa` traz "Sem ementa." nos vistos) e documento_text (íntegra em HTML
  ISO-8859-1 codificado em base64);
- não há link permanente: o front exibe a íntegra embutida na própria resposta.
```

## Uso responsável

- Faça no máximo 1 requisição por segundo (ou menos, se a nota acima pedir).
- Guarde o resultado em vez de consultar de novo a mesma coisa.
- Não tente contornar CAPTCHA, login ou bloqueio: se aparecer, pare.
- Decisões trazem nomes de pessoas: respeite a LGPD ao guardar e publicar.

[⬅ Voltar para a lista](../README.md)
