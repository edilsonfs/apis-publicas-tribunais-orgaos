# Diário de Justiça Eletrônico Nacional (CNJ) — teor publicado

> Tudo o que os tribunais publicam no Diário de Justiça Nacional.

| | |
|---|---|
| **Órgão** | CNJ |
| **Tipo de acesso** | 📘 Oficial documentada |
| **Autenticação** | Nenhuma |
| **Site oficial** | <https://comunica.pje.jus.br/> |
| **Documentação oficial** | <https://comunicaapi.pje.jus.br/swagger/djen.yml> |
| **Domínios usados** | `comunicaapi.pje.jus.br`, `s3.cnj.jus.br` |
| **Aceita busca por palavra** | sim |
| **Aceita filtro por data** | sim |
| **Verificado em** | outubro de 2026 |

## Resumo

Exige opção `tribunais` (siglas, ex.: TJPE,STJ,TRT6). Sem termo usa o caderno diário (dia completo); com termo usa a busca textual (até 10.000 itens).

## Como a API funciona (notas verificadas ao vivo)

```text
DJEN — Diário de Justiça Eletrônico Nacional (CNJ), API de Comunicações Processuais.

Fonte oficial documentada: OpenAPI em comunicaapi.pje.jus.br/swagger/djen.yml (Res. CNJ 455/2022).
Fatos verificados ao vivo em 12/10/2026:
- GET /api/v1/comunicacao (sem autenticação): siglaTribunal, texto, dataDisponibilizacaoInicio/Fim
  (AAAA-MM-DD), pagina, itensPorPagina (5 ou 100); `count` satura em 10.000 por consulta;
- limite por IP informado em X-RateLimit-Limit (20) — 429 pede espera de 1 minuto;
- GET /api/v1/caderno/{sigla}/{AAAA-MM-DD}/{D|E}: metadados do caderno do dia com `hash` SHA-256 e
  `url` pré-assinada (5 min) em djen-prd.prd.s3.cnj.jus.br; o ZIP contém JSON {count, items} com os
  mesmos campos da consulta — é a única forma de obter o dia inteiro de tribunais com >10.000 itens.
O campo `texto` traz o teor publicado (inclusive acórdãos com ementa).
Por minimização (LGPD), destinatários e advogados não são armazenados, só a contagem.
```

## Uso responsável

- Faça no máximo 1 requisição por segundo (ou menos, se a nota acima pedir).
- Guarde o resultado em vez de consultar de novo a mesma coisa.
- Não tente contornar CAPTCHA, login ou bloqueio: se aparecer, pare.
- Decisões trazem nomes de pessoas: respeite a LGPD ao guardar e publicar.

[⬅ Voltar para a lista](../README.md)
