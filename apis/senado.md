# Senado Federal — legislação federal (dados abertos legislativos)

> Todas as normas federais: dados, alterações e publicação.

| | |
|---|---|
| **Órgão** | Senado |
| **Tipo de acesso** | 📘 Oficial documentada |
| **Autenticação** | Nenhuma |
| **Site oficial** | <https://legis.senado.leg.br/dadosabertos/legislacao/lista> |
| **Documentação oficial** | <https://legis.senado.leg.br/dadosabertos/v3/api-docs> |
| **Domínios usados** | `legis.senado.leg.br` |
| **Aceita busca por palavra** | sim |
| **Aceita filtro por data** | sim |
| **Verificado em** | outubro de 2026 |

## Resumo

Período = data de ASSINATURA (a API não filtra publicação); uma requisição por dia mais uma por norma. Também aceita parametros tipo/numero/ano (ex.: tipo=LEI, ano=2026), tipos (siglas para filtrar: LEI,DEC,MPV,LCP...) e urns. O termo é filtrado localmente na ementa e no apelido. Só metadados: o texto vigente vem do cliente normas_leg.

## Como a API funciona (notas verificadas ao vivo)

```text
Senado Federal — API de Dados Abertos Legislativos: normas jurídicas federais (metadados).

Fonte oficial documentada: OpenAPI em https://legis.senado.leg.br/dadosabertos/v3/api-docs
("API de acesso público, sem necessidade de autenticação"). Fatos verificados ao vivo em 12/10/2026:
- GET /dadosabertos/legislacao/lista.json com tipo, numero, ano, data (assinatura, AAAAMMDD), seq,
  reedicao, ident, complemento; NÃO há intervalo de datas: a coleta por período consulta dia a dia
  pela data de assinatura (ex.: data=20260928 trouxe o Decreto 13.128 e as Leis 15.522 a 15.525);
- itens da lista: id (código), tipo (sigla: LEI-n, DEC-n, MPV, LCP...), descricao, numero, norma,
  normaNome, ementa, dataassinatura, anoassinatura, apelido — sem URN;
- GET /legislacao/{codigo}.json e /legislacao/urn.json?urn=: identificacao.urlDocumento
  (https://normas.leg.br/?urn=...), publicacoes (fonte no DOU, data, página, coluna; tipo PUB ou RET),
  vides (normas posteriores que alteram, regulamentam ou vetam), edivs (normas anteriores alteradas),
  ementa, observacao, catalogo, indexacao e classes. Não há texto integral (ver cliente normas_leg);
- tipos de norma: /dadosabertos/dados/ListaTiposDocumento.json (destino do 301 de /legislacao/tiposNorma);
- mais de 10 requisições por segundo recebem HTTP 429.
Página oficial da norma: https://legis.senado.leg.br/norma/{codigo} (verificada).
```

## Uso responsável

- Faça no máximo 1 requisição por segundo (ou menos, se a nota acima pedir).
- Guarde o resultado em vez de consultar de novo a mesma coisa.
- Não tente contornar CAPTCHA, login ou bloqueio: se aparecer, pare.
- Decisões trazem nomes de pessoas: respeite a LGPD ao guardar e publicar.

[⬅ Voltar para a lista](../README.md)
