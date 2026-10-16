# Assembleia Legislativa de Minas Gerais — legislação mineira

> Leis e normas de Minas Gerais.

| | |
|---|---|
| **Órgão** | ALMG |
| **Tipo de acesso** | 📘 Oficial documentada |
| **Autenticação** | Nenhuma |
| **Site oficial** | <https://www.almg.gov.br/legislacao-mineira/> |
| **Documentação oficial** | <https://dadosabertos.almg.gov.br/api/ajuda/swagger/view/lastest> |
| **Domínios usados** | `dadosabertos.almg.gov.br` |
| **Aceita busca por palavra** | sim |
| **Aceita filtro por data** | sim |
| **Verificado em** | outubro de 2026 |

## Resumo

Período = data da norma (dataLegislacao). Termo vai no parâmetro oficial 'ass' (assunto). parametros: tipo (sigla ALMG: LEI, DEC, DNE, LCP...), ano, num, grupo e detalhar=true (busca também o registro individual). inteiro_teor = texto consolidado quando existe, senão o original.

## Como a API funciona (notas verificadas ao vivo)

```text
Assembleia Legislativa de Minas Gerais — legislação mineira (API de dados abertos v2).

Fonte oficial documentada: OpenAPI em https://dadosabertos.almg.gov.br/api/ajuda/swagger/endpoints/lastest
(interface em /api/ajuda/swagger/view/lastest); "a atual API não requer autenticação"; licença da API
CC BY-SA 4.0; o serviço limita a duas requisições simultâneas. Fatos verificados ao vivo em 12/10/2026:
- o host é dadosabertos.almg.gov.br (o mesmo caminho em www.almg.gov.br responde 404);
- GET /api/v2/legislacao/mineira/pesquisa/direcionada: tp (tamanho da página), p (página), grupo, tipo,
  num, comp, ano, ini/fim (AAAAMMDD, filtram dataLegislacao), ass (assunto), th (thesaurus), ord
  (0 = data decrescente), resumido; resposta {"resultado": {noOcorrencias, tamanhoPagina, numPagina,
  listaItem[]}} (a consulta interna é do tipo Elasticsearch: o teto de 10.000 é tratado como saturação);
  setembro/2026 teve 105 normas;
- GET /api/v2/legislacao/mineira/{tipo}/{num}/{ano} (ou /{tipo}/{num}/{comp}/{ano}): registro completo
  com texto (original) e textoConsolidado em HTML, tema, indexacao, resumo, assuntoGeral, vigencia,
  listaVide, linkProposicao, tags, midias e fonte (HTML com link para o Jornal Minas Gerais), ex.:
  LEI 23631/2020 -> "Minas Gerais Diário do Executivo Edição Extra - 02/04/2020 Pág. 2 Col. 1";
- a pesquisa direcionada já devolve esses mesmos campos em cada item (inclusive textoConsolidado quando
  existe), então o registro individual só é consultado com opção `detalhar`=true;
- /documento?tipoDoc=142|572 devolve os documentos ODT gerados (não usado: o registro já traz os textos);
- página pública verificada: https://www.almg.gov.br/legislacao-mineira/texto/LEI/23631/2020/.
```

## Uso responsável

- Faça no máximo 1 requisição por segundo (ou menos, se a nota acima pedir).
- Guarde o resultado em vez de consultar de novo a mesma coisa.
- Não tente contornar CAPTCHA, login ou bloqueio: se aparecer, pare.
- Decisões trazem nomes de pessoas: respeite a LGPD ao guardar e publicar.

[⬅ Voltar para a lista](../README.md)
