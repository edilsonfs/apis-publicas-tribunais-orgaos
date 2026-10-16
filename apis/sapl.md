# SAPL (Interlegis) — normas de Assembleias Legislativas e Câmaras Municipais

> Leis de Assembleias e Câmaras que usam o SAPL.

| | |
|---|---|
| **Órgão** | SAPL |
| **Tipo de acesso** | 📘 Oficial documentada |
| **Autenticação** | Nenhuma |
| **Site oficial** | <https://www.interlegis.leg.br/> |
| **Documentação oficial** | <https://sapl.al.pb.leg.br/api/schema/> |
| **Domínios usados** | `leg.br` |
| **Aceita busca por palavra** | sim |
| **Aceita filtro por data** | sim |
| **Verificado em** | outubro de 2026 |

## Resumo

Exige opção `casas` (hosts .leg.br, ex.: sapl.al.pb.leg.br,sapl.olinda.pe.leg.br). Período = data da última atualização do cadastro (incremental); opção `campo_data` = publicacao ou data muda o critério. Termo vai em ementa__icontains. Texto só em PDF (url_inteiro_teor); inteiro_teor vazio. Campos ip e user da API não são gravados. Esfera e órgão de cada documento vêm da casa (AL-PB, CM-Olinda/PE...).

## Como a API funciona (notas verificadas ao vivo)

```text
SAPL (Interlegis/Senado) — normas jurídicas de Assembleias Legislativas e Câmaras Municipais.

Fonte oficial documentada: cada instância do SAPL publica OpenAPI 3 em https://<casa>/api/schema/
(ex.: https://sapl.al.pb.leg.br/api/schema/, 445 filtros em /api/norma/normajuridica/). Fatos verificados
ao vivo em 12/10/2026 (sapl.al.pb.leg.br e sapl.olinda.pe.leg.br):
- GET /api/norma/normajuridica/?page_size=100&page=N sem autenticação; resposta
  {pagination: {links: {next, previous}, total_entries, total_pages, page...}, results: [...]};
  os links "next" vêm com http:// — a URL da página seguinte é montada aqui, nunca seguida;
- filtros automáticos por campo: data_ultima_atualizacao__gte / __lt, data__gte / __lte,
  data_publicacao__gte / __lte, ementa__icontains...; ordenação o=id (estável) e o=-data_ultima_atualizacao;
- campos: id, __str__, texto_integral (URL do PDF, em http://), numero, ano, esfera_federacao (E/M),
  data, data_publicacao, veiculo_publicacao, pagina_inicio_publicacao, pagina_fim_publicacao, ementa,
  indexacao, observacao, complemento, data_vigencia, timestamp, data_ultima_atualizacao, ip, ultima_edicao,
  tipo (id), materia, orgao, user, assuntos (ids), selos_ods, autores (ids);
- ip e user identificam quem editou o cadastro: NÃO são gravados (LGPD);
- /api/norma/tiponormajuridica/ traz descricao, sigla e equivalente_lexml de cada tipo;
- página pública da norma: https://<casa>/norma/<id>.
O SAPL só oferece o texto em PDF: url_inteiro_teor guarda o link e inteiro_teor fica vazio.
```

## Uso responsável

- Faça no máximo 1 requisição por segundo (ou menos, se a nota acima pedir).
- Guarde o resultado em vez de consultar de novo a mesma coisa.
- Não tente contornar CAPTCHA, login ou bloqueio: se aparecer, pare.
- Decisões trazem nomes de pessoas: respeite a LGPD ao guardar e publicar.

[⬅ Voltar para a lista](../README.md)
