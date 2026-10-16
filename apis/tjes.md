# Tribunal de Justiça do Espírito Santo — jurisprudência

> Jurisprudência do TJES, inclusive 1º grau.

| | |
|---|---|
| **Órgão** | TJES |
| **Tipo de acesso** | 🔧 JSON do site oficial |
| **Autenticação** | Nenhuma |
| **Site oficial** | <https://sistemas.tjes.jus.br/consulta-jurisprudencia/> |
| **Domínios usados** | `sistemas.tjes.jus.br` |
| **Aceita busca por palavra** | sim |
| **Aceita filtro por data** | sim |
| **Verificado em** | outubro de 2026 |

## Resumo

Período = data de juntada nos autos (filtro dataIni/dataFim da fonte); sem data de publicação no índice, a juntada é usada como data de publicação. Parâmetro `cores` (padrão pje2g,pje2g_mono; também pje1g, legado, turma_recursal_legado). Campo `resumo` descartado. Sem link permanente por documento.

## Como a API funciona (notas verificadas ao vivo)

```text
TJES — consulta de jurisprudência (sistemas.tjes.jus.br/consulta-jurisprudencia).

Fonte: JSON servido pelo próprio domínio oficial ao front-end (Vue). Fatos verificados ao vivo em 12/10/2026:
- GET /consulta-jurisprudencia/api/search com core, q ("*:*" quando sem termo), page (começa em 1),
  per_page, sort e os filtros do formulário dataIni/dataFim (campos type="date", AAAA-MM-DD);
- cores conhecidos pelo front: pje1g, pje2g, pje2g_mono, legado, turma_recursal_legado (/api/cores lista);
- resposta {core_used, docs[], facets, page, per_page, total, total_pages}; pje2g com dataIni=2026-10-01 e
  dataFim=2026-10-02 devolveu total=1.343 (Tribunal de Justiça e Turmas Recursais), todos com dt_juntada no
  período: os filtros de data recaem sobre a juntada nos autos;
- docs do pje2g: id, nr_processo, classe_judicial(+sigla, códigos), magistrado, orgao_julgador, jurisdicao,
  competencia, localizacao, assunto_principal, lista_assunto, dt_juntada (ISO UTC), ementa/ementa_html e o
  inteiro teor em acordao/acordao_html; não trazem data_julgamento nem data_publicacao;
- pje2g_mono (decisões monocráticas) validado ao vivo: mesmos metadados, inteiro teor em inteiro_teor;
- o front lê o inteiro teor em: pje2g → acordao(_html); pje2g_mono e pje1g → inteiro_teor(_html);
  legado → conteudo_decisao(_completa)_html; turma_recursal_legado → cont_ementa;
- o campo `resumo` exibido pelo front não é armazenado (pode ser gerado automaticamente; regra "sem IA").
Sem link permanente por documento: o link aponta para a página de consulta.
```

## Uso responsável

- Faça no máximo 1 requisição por segundo (ou menos, se a nota acima pedir).
- Guarde o resultado em vez de consultar de novo a mesma coisa.
- Não tente contornar CAPTCHA, login ou bloqueio: se aparecer, pare.
- Decisões trazem nomes de pessoas: respeite a LGPD ao guardar e publicar.

[⬅ Voltar para a lista](../README.md)
