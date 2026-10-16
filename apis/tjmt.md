# Tribunal de Justiça de Mato Grosso — jurisprudência

> Jurisprudência do TJMT.

| | |
|---|---|
| **Órgão** | TJMT |
| **Tipo de acesso** | 🔧 JSON do site oficial |
| **Autenticação** | Token público do site |
| **Site oficial** | <https://jurisprudencia.tjmt.jus.br/consulta/judicial> |
| **Domínios usados** | `hellsgate.tjmt.jus.br`, `jurisprudencia.tjmt.jus.br` |
| **Aceita busca por palavra** | sim (obrigatória) |
| **Aceita filtro por data** | sim |
| **Verificado em** | outubro de 2026 |

> [!WARNING]
> Em 12–14/10/2026 a API estava em manutenção (504). Leia o token no JavaScript público do site, ele muda.

## Resumo

NÃO validado ao vivo (504/manutenção em 12/10/2026). Exige termo, como o front. Período por data de julgamento. Token público lido do bundle da SPA (ou parâmetro `token`). Parâmetro `tipos` (acordao, decisao; padrão ambos). Nomes de campo dos itens ainda não verificados.

## Como a API funciona (notas verificadas ao vivo)

```text
TJMT — consulta de jurisprudência (jurisprudencia.tjmt.jus.br).

Fonte: API "hellsgate" consumida pela SPA Angular oficial. NÃO VALIDADO AO VIVO: em 12/10/2026 a única chamada
à API devolveu 504 (Gateway Time-out) e, antes, os sistemas do TJMT exibiam "Site em manutenção — TJMT".
Fatos lidos no bundle oficial em 12/10/2026 (index, main e chunks do próprio domínio):
- ambiente da SPA: api_url "https://hellsgate.tjmt.jus.br/jurisprudencia" e api_hellsgate_token (token público
  enviado no cabeçalho `token` por um interceptor HTTP; em 12/10/2026 o valor era o mesmo já conhecido); o
  levantamento anterior citava o host hellsgate-preview.tjmt.jus.br;
- a consulta judicial é GET {api_url}/consulta com indicePagina, quantidadePagina, tipoConsulta (1 = acórdão,
  2 = decisão monocrática, 3 = recursal eletrônico), termoDeBusca, tipoBusca (1), OrdenarPor ("Julgamento"),
  Decrescente ("true"), thesaurus, exibirArquivados e, quando há período, periodoDataDe/periodoDataAte
  (AAAA-MM-DD); filtros opcionais relator, orgaoJulgador, colegiado, tipoProcesso, fq*;
- o front lê `value.countAcordaoDocumento` e `value.countDecisaoMonocratica`; o levantamento anterior descreve
  AcordaoCollection, DecisaoMonocraticaCollection e CountAcordaoDocumento — o cliente aceita os dois formatos
  (com ou sem `value`, chaves sem diferenciar maiúsculas);
- o front exige termo ("não pode ser vazio, informe termo válido"); o levantamento anterior cita no máximo
  100 itens por página;
- o ambiente da SPA também declara um verificador reCAPTCHA, sem uso encontrado no fluxo da consulta lido; se a
  API passar a exigir token de CAPTCHA, o cliente deve ser excluído (não contornar).
Os nomes de campo dos itens das coleções NÃO foram verificados: o mapeamento procura nomes prováveis sem
diferenciar maiúsculas (Id, NumeroUnico/NumeroProcesso, Ementa, DataJulgamento, Relator...).
```

## Uso responsável

- Faça no máximo 1 requisição por segundo (ou menos, se a nota acima pedir).
- Guarde o resultado em vez de consultar de novo a mesma coisa.
- Não tente contornar CAPTCHA, login ou bloqueio: se aparecer, pare.
- Decisões trazem nomes de pessoas: respeite a LGPD ao guardar e publicar.

[⬅ Voltar para a lista](../README.md)
