# Tribunal de Justiça de Minas Gerais — jurisprudência

> Jurisprudência do TJMG.

| | |
|---|---|
| **Órgão** | TJMG |
| **Tipo de acesso** | 📘 Oficial documentada |
| **Autenticação** | Nenhuma |
| **Site oficial** | <https://jurisprudencia-api.tjmg.jus.br/v3/api-docs> |
| **Documentação oficial** | <https://jurisprudencia-api.tjmg.jus.br/v3/api-docs> |
| **Domínios usados** | `jurisprudencia-api.tjmg.jus.br` |
| **Aceita busca por palavra** | sim |
| **Aceita filtro por data** | sim |
| **Verificado em** | outubro de 2026 |

## Resumo

Período por data de publicação (campo_data=julgamento troca o critério). Filtros opcionais: orgaos, classes, comarcas, magistrados, tipos, assuntos, processos (listas separadas por vírgula). Inteiro teor só com inteiro_teor=sim e só para itens com documentoHash (endpoint /document não validado). Sem link permanente.

## Como a API funciona (notas verificadas ao vivo)

```text
TJMG — API de jurisprudência v3 (jurisprudencia-api.tjmg.jus.br).

Fonte: API com OpenAPI pública em https://jurisprudencia-api.tjmg.jus.br/v3/api-docs. Fatos verificados
ao vivo em 12/10/2026:
- POST /jurisprudencias/filter?page&size (page começa em 0) com corpo JurisprudenciaFilter: texto,
  datasPublicacao/datasJulgamento [{inicio, fim}] em AAAA-MM-DD, listas assuntos, classes, tiposDocumento,
  comarcas, magistrados, numerosProcessos, orgaosJulgadores, ids e o booleano total;
- a OpenAPI declara oauth2, mas a consulta respondeu 200 sem token (consulta pública);
- resposta {retrieveTime, totalRecords, jurisprudencias[]}; totalRecords para de contar em 1.000 (um único
  dia de publicação, 01/10/2026, já marcou 1.000), mas a paginação continua: page=60&size=20 (posição 1.200)
  devolveu 20 itens; por isso, saturado o total, o cliente pagina até a página vir incompleta;
- itens: id (estável), tipoDocumento ("Acórdão", com ementa; "Decisão Turma Recursal", sem ementa e com
  documentoHash), assuntos, ementa, orgaoJulgador, julgamentoData e publicacaoData (dd/mm/aaaa),
  numeroProcessoTj, numeroProcessoCnj, magistrado, classe, comarca, documentoId;
- POST /jurisprudencias/document devolve o inteiro teor, mas com {ids, documentoId} respondeu 500 ("Dados de
  documento inválidos ou incompletos"); a chamada só é feita com o parâmetro inteiro_teor=sim e apenas para
  itens com documentoHash (não validada ao vivo);
- POST /dominio/orgaoJulgador respondeu 500; não há partição automática por órgão.
Sem link permanente por documento: o link aponta para a pesquisa clássica de jurisprudência do TJMG
(www5.tjmg.jus.br, não consultada nesta sessão; jurisprudencia.tjmg.jus.br/ respondeu 404).
```

## Uso responsável

- Faça no máximo 1 requisição por segundo (ou menos, se a nota acima pedir).
- Guarde o resultado em vez de consultar de novo a mesma coisa.
- Não tente contornar CAPTCHA, login ou bloqueio: se aparecer, pare.
- Decisões trazem nomes de pessoas: respeite a LGPD ao guardar e publicar.

[⬅ Voltar para a lista](../README.md)
