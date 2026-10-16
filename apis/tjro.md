# Tribunal de Justiça de Rondônia — jurisprudência

> Jurisprudência do TJRO, inclusive sentenças.

| | |
|---|---|
| **Órgão** | TJRO |
| **Tipo de acesso** | 🔧 JSON do site oficial |
| **Autenticação** | Nenhuma |
| **Site oficial** | <https://juris.tjro.jus.br/> |
| **Domínios usados** | `juris-back.tjro.jus.br` |
| **Aceita busca por palavra** | sim |
| **Aceita filtro por data** | sim |
| **Verificado em** | outubro de 2026 |

> [!WARNING]
> Bloqueia o IP por dezenas de minutos após rajadas. Use 1 requisição a cada 2 segundos ou mais.

## Resumo

Período por data de julgamento, aplicado na própria consulta (dtjulgamento:[de TO até]). Inclui sentenças de 1º grau e peças do 2º grau (acórdão, voto, ementa, relatório, decisão). Parâmetro `processo` filtra por número. Bloqueia o IP por dezenas de minutos após rajadas (resposta malformada ou 'Página Bloqueada'): intervalo de 2 s. Sem link permanente por documento.

## Como a API funciona (notas verificadas ao vivo)

```text
TJRO — pesquisa de jurisprudência (juris.tjro.jus.br).

Fonte: JSON (Elasticsearch) servido por juris-back.tjro.jus.br ao front-end oficial. Fatos verificados ao vivo
em 12/10/2026:
- POST https://juris-back.tjro.jus.br/search/varios_parametros/ com Origin/Referer https://juris.tjro.jus.br e
  corpo JSON {from, size, fields:{nr_processo, query, ...}, sort:[...]}; o front ordena por
  [{_score: desc}, {dtjulgamento: desc}] e a API aceitou [{dtjulgamento: desc}] sozinho;
- `fields.query` aceita a sintaxe de consulta do Elasticsearch: "dtjulgamento:[2026-10-01 TO 2026-10-02]"
  devolveu 1.879 documentos e a agregação datas_julgamento só trouxe 01/10 (1.286) e 02/10 (593). o cliente
  monta o período assim, combinado ao termo com AND (os nomes dos filtros de data do front não foram lidos: o
  front bloqueou este IP com "Página Bloqueada — suspeita de robotização" e não houve nova tentativa);
- query "dano moral": hits.total.value=1.123.875; resposta {took, hits:{total:{value, relation}, hits[]},
  aggregations, suggest}; cada hit traz _id (ex.: "143937283-PJEPG"), _source e sort;
- _source: tipo (SENTENÇA, ACÓRDÃO, VOTO, EMENTA, RELATÓRIO, DECISÃO, VOTO VENCEDOR), grau_jurisdicao,
  nr_processo (20 dígitos), ds_classe_judicial, cd_classe_judicial, ds_assunto_trf, cd_assunto_trf,
  ds_orgao_julgador, ds_orgao_julgador_colegiado, nome_relator_acordao, nome_relator_processo, ds_nome
  (magistrado signatário: aparece no fecho do texto antes de "Juiz de Direito"), dtjulgamento (AAAA-MM-DD),
  dtpublicacao (nula nos vistos), ds_modelo_documento (íntegra em HTML), nivel_sigilo_processo, sistema_origem,
  id_processo_documento, ds_md5_documento e data_indexacao;
- limite por IP com bloqueio de dezenas de minutos e resposta HTTP malformada: intervalo conservador. Em
  12/10/2026, após duas consultas diretas bem-sucedidas, a validação pelo cliente recebeu o cabeçalho ilegal
  "Connection: close\x00" (bloqueio); o cliente converte isso em bloqueio temporário;
- teto do Elasticsearch: from + size <= 10.000.
```

## Uso responsável

- Faça no máximo 1 requisição por segundo (ou menos, se a nota acima pedir).
- Guarde o resultado em vez de consultar de novo a mesma coisa.
- Não tente contornar CAPTCHA, login ou bloqueio: se aparecer, pare.
- Decisões trazem nomes de pessoas: respeite a LGPD ao guardar e publicar.

[⬅ Voltar para a lista](../README.md)
