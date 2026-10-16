# Tribunal de Justiça da Bahia — jurisprudência

> Jurisprudência do TJBA.

| | |
|---|---|
| **Órgão** | TJBA |
| **Tipo de acesso** | 🔧 JSON do site oficial |
| **Autenticação** | Nenhuma |
| **Site oficial** | <https://jurisprudencia.tjba.jus.br/> |
| **Domínios usados** | `jurisprudenciaws.tjba.jus.br` |
| **Aceita busca por palavra** | sim |
| **Aceita filtro por data** | sim |
| **Verificado em** | outubro de 2026 |

## Resumo

Período por data de publicação. Parâmetros opcionais (sim/não): segundo_grau, turmas_recursais, acordaos, monocraticas (todos ligados por padrão). Monocráticas não têm hash: id derivado do conteúdo e link para a pesquisa.

## Como a API funciona (notas verificadas ao vivo)

```text
TJBA — jurisprudência (GraphQL do portal jurisprudencia.tjba.jus.br).

Fonte: GraphQL servido pelo próprio domínio oficial ao front-end (o bundle JS do portal aponta para
https://jurisprudenciaws.tjba.jus.br/graphql). Fatos verificados ao vivo em 12/10/2026:
- POST /graphql, operationName "filter", variáveis decisaoFilter (DecisaoFilter!: assunto, orgaos, relatores,
  classes, dataInicial, dataFinal, segundoGrau, turmasRecursais, tipoAcordaos, tipoDecisoesMonocraticas,
  ordenadoPor), pageNumber (começa em 0) e itemsPerPage; a consulta abaixo foi escrita a partir desses fatos;
- datas em AAAA-MM-DD (período de publicação); o front usa ordenadoPor="dataPublicacao" e converte
  E/OU/NÃO do termo em AND/OR/NOT;
- resposta data.filter {decisoes[], pageCount, itemCount}; pageCount acompanha itemsPerPage
  (111 itens em 01–02/10/2026 → 56 páginas de 2); erros vêm em `errors`;
- decisão: dataPublicacao (ISO, 03:00Z = meia-noite de Brasília), relator{id,nome}, orgaoJulgador{id,nome},
  classe{id,descricao}, tipoDecisao (ACORDAO | DECISAO_MONOCRATICA), ementa, conteudo (HTML do inteiro teor,
  nulo nas monocráticas vistas, cuja íntegra vem em `ementa`), hash (só nos acórdãos) e numeroProcesso (CNJ);
- não há id por decisão: usa-se o hash; sem ele, um resumo SHA-256 de processo, data, tipo e texto;
- link do inteiro teor no front: https://jurisprudenciaws.tjba.jus.br/inteiroTeor/{hash}.
```

## Uso responsável

- Faça no máximo 1 requisição por segundo (ou menos, se a nota acima pedir).
- Guarde o resultado em vez de consultar de novo a mesma coisa.
- Não tente contornar CAPTCHA, login ou bloqueio: se aparecer, pare.
- Decisões trazem nomes de pessoas: respeite a LGPD ao guardar e publicar.

[⬅ Voltar para a lista](../README.md)
