# Supremo Tribunal Federal — jurisprudência (acórdãos e decisões)

> Acórdãos e decisões do STF com ementa.

| | |
|---|---|
| **Órgão** | STF |
| **Tipo de acesso** | 🛡️ Precisa de navegador |
| **Autenticação** | Cookie de desafio (navegador) |
| **Site oficial** | <https://jurisprudencia.stf.jus.br/pages/search> |
| **Domínios usados** | `jurisprudencia.stf.jus.br` |
| **Aceita busca por palavra** | sim |
| **Aceita filtro por data** | sim |
| **Verificado em** | outubro de 2026 |

> [!WARNING]
> O desafio AWS WAF (não é CAPTCHA) bloqueia navegador headless; o cookie obtido vale cerca de 4 dias.

## Resumo

Requer Playwright (uv sync --extra navegador; uv run playwright install chromium) para o cookie do desafio AWS WAF (JavaScript, não CAPTCHA); o headless recebe 403, então o Chromium abre com janela (em servidor, use um display virtual). O cookie vale ~4 dias, fica em <dados_dir>/stf-waf.json e é usado com o User-Agent do navegador que o obteve. Período = data de julgamento. opção `base` = acordaos | decisoes (padrão: ambas); opção `headless`='true' para testar.

## Como a API funciona (notas verificadas ao vivo)

```text
STF — pesquisa de jurisprudência (acórdãos e decisões monocráticas).

Fonte: API JSON da SPA oficial jurisprudencia.stf.jus.br, atrás de desafio JavaScript do AWS WAF (não é
CAPTCHA; ver _stf_waf.py). Fatos verificados ao vivo em 12/10/2026, interceptando a própria SPA:
- POST /api/search/search com corpo Elasticsearch; resposta {"result": {hits, aggregations}, "search_id"};
- os corpos enviados pela SPA estão em stf_corpos.json, reproduzidos fielmente (mesmas chaves, _source, aggs,
  highlight, post_filter por base); só mudam termo, datas, size e from;
- com termo, a SPA põe o termo em 10 query_string (consulta e highlight) e o período como
  {"range": {"julgamento_data": {"format": "ddMMyyyy", "from": ..., "lte": ...}}};
- sem termo, a SPA só pesquisa pela data de julgamento da busca avançada:
  {"range": {"julgamento_data": {"gte": "AAAA-MM-DD", "lte": "AAAA-MM-DD"}}};
- ordenação por data = [{"julgamento_data": "desc"}]; size até 250 (aceito pela SPA); from = página × size;
  from + size ≤ 10.000;
- bases: acordaos (ementa_texto, acordao_ata, documental_*) e decisoes (decisao_texto = texto da decisão);
- link do documento: /pages/search/<id>/false (rota de detalhe da SPA); inteiro teor em PDF
  (inteiro_teor_url, portal.stf.jus.br).
Período = data de julgamento (único filtro de data aceito pela SPA sem termo).
```

## Uso responsável

- Faça no máximo 1 requisição por segundo (ou menos, se a nota acima pedir).
- Guarde o resultado em vez de consultar de novo a mesma coisa.
- Não tente contornar CAPTCHA, login ou bloqueio: se aparecer, pare.
- Decisões trazem nomes de pessoas: respeite a LGPD ao guardar e publicar.

[⬅ Voltar para a lista](../README.md)
