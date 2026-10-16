# CNJ DataJud — metadados processuais (API Pública)

> Dados dos processos de todos os tribunais (sem o texto).

| | |
|---|---|
| **Órgão** | CNJ |
| **Tipo de acesso** | 📘 Oficial documentada |
| **Autenticação** | Chave pública do CNJ |
| **Site oficial** | <https://datajud-wiki.cnj.jus.br/api-publica/> |
| **Documentação oficial** | <https://datajud-wiki.cnj.jus.br/api-publica/> |
| **Domínios usados** | `api-publica.datajud.cnj.jus.br` |
| **Aceita busca por palavra** | sim |
| **Aceita filtro por data** | sim |
| **Verificado em** | outubro de 2026 |

> [!WARNING]
> Só metadados de processos (sem ementa nem inteiro teor). O termo de uso do CNJ restringe a fins não comerciais.

## Resumo

Exige opção `tribunais` (aliases: stj, tst, trf1, tjpe, tjdft, trt6, tre-pe, tre-dft...). Período = dataHoraUltimaAtualizacao (UTC). Só metadados e movimentos, sem ementa nem teor. Termo de uso do CNJ: fins legais e não comerciais; proíbe redistribuição. Não há índice do STF. Filtros opcionais: classes, assuntos, orgaos_julgadores (códigos), graus. Termo: número CNJ ou texto sobre nomes de classe/assunto/órgão. Consultas lentas (até 60 s).

## Como a API funciona (notas verificadas ao vivo)

```text
CNJ DataJud — API Pública de metadados processuais (Res. CNJ 331/2020).

Fonte oficial documentada: datajud-wiki.cnj.jus.br/api-publica/. Fatos verificados ao vivo em 12/10/2026:
- POST https://api-publica.datajud.cnj.jus.br/api_publica_<alias>/_search, cabeçalho
  "Authorization: APIKey <chave pública do CNJ>", corpo em Elasticsearch Query DSL;
- aliases: stj, tst, tse, stm, trf1..trf6, tj<uf> (tjdft), trt1..trt24, tre-<uf> (tre-dft), tjmmg, tjmrs,
  tjmsp; não há índice do STF;
- cada hit traz só metadados: id ("STJ_SUP_<número>"), tribunal, grau, numeroProcesso (20 dígitos),
  classe{codigo,nome}, assuntos[], orgaoJulgador{codigo,nome,codigoMunicipioIBGE}, formato, sistema,
  nivelSigilo, dataAjuizamento ("AAAAMMDDhhmmss"), dataHoraUltimaAtualizacao (UTC), @timestamp, movimentos[];
  sem ementa nem inteiro teor;
- varredura com sort [@timestamp, id.keyword] + search_after (sem teto de 10.000); consultas levam 40–60 s;
- com o cluster sobrecarregado a API responde 200 com `_shards.failed` > 0 (resultado parcial, ex.: 147 de
  215) ou 429/504 — resultado parcial vira erro, nunca é gravado como completo.
Termo de uso do CNJ: dados para fins legais e não comerciais; vedada a redistribuição.
```

## Uso responsável

- Faça no máximo 1 requisição por segundo (ou menos, se a nota acima pedir).
- Guarde o resultado em vez de consultar de novo a mesma coisa.
- Não tente contornar CAPTCHA, login ou bloqueio: se aparecer, pare.
- Decisões trazem nomes de pessoas: respeite a LGPD ao guardar e publicar.

[⬅ Voltar para a lista](../README.md)
