# Tribunal de Contas do Distrito Federal — jurisprudência (Busca TCDF)

> Decisões do TCDF.

| | |
|---|---|
| **Órgão** | TCDF |
| **Tipo de acesso** | 🔧 JSON do site oficial |
| **Autenticação** | Nenhuma |
| **Site oficial** | <https://busca.tc.df.gov.br/#/jurisprudencia/inteiro-teor> |
| **Domínios usados** | `api-busca-publica.tc.df.gov.br` |
| **Aceita busca por palavra** | sim |
| **Aceita filtro por data** | sim |
| **Verificado em** | outubro de 2026 |

## Resumo

Período pela data da sessão (filtro por ano na fonte + recorte no cliente). Parâmetros opcionais: `situacao` (ex.: Publicada = jurisprudência selecionada; padrão: todas), `relator` e `sessao_tipo`. Inteiro teor = textos da DECISÃO e do RELATÓRIO / VOTO servidos pela busca. Campo `analista` descartado. Cadeia TLS incompleta na fonte: intermediários Let's Encrypt YR1/Root YR em repositório de certificados confiáveis.

## Como a API funciona (notas verificadas ao vivo)

```text
TCDF — pesquisa pública de jurisprudência (busca.tc.df.gov.br).

Fonte: JSON (Elasticsearch, índice "forseti") servido pela API oficial ao front-end da Busca do TCDF.
Fatos verificados ao vivo em 12/10/2026:
- GET https://api-busca-publica.tc.df.gov.br/jurisprudencia/?q=<termo>&from=<deslocamento>&maxPerPage=<n>
  responde 200 {data:{took, hits:{total:{value}, hits:[{_id, _source}]}}} com o User-Agent padrão do projeto
  (não foi preciso UA de navegador);
- o front (busca.tc.df.gov.br, que redireciona para busca2.tc.df.gov.br) usa maxPerPage=25, `from` como
  deslocamento (página × tamanho), ordenação sort=sessao_data&order=desc ("mais recentes") e os filtros
  filter[ano]=AAAA, filter[relator]='...', filter[sessao_tipo]='...' e, na aba de jurisprudência selecionada,
  filter[jurisprudencia_situacao]='Publicada'; sem palavra-chave o parâmetro q é omitido;
- filter[ano]=2026 sem termo: 1.929 documentos, devolvidos em ordem decrescente de sessao_data;
- não há filtro por intervalo de datas: o cliente filtra por ano e recorta no cliente pela data da sessão,
  parando quando a lista ordenada passa do início do período;
- cada _source traz documento_edoc e hash (o link de compartilhamento do front é
  https://busca.tc.df.gov.br#/jurisprudencia/inteiro-teor?q=<edoc>&filter[hash]=<hash>), documento_numero_ano,
  jurisprudencia_tipo_descricao ("Decisão"), processo_numero_completo, processo_relator, sessao_data/numero/tipo,
  jurisprudencia_data_publicacao, ementa, ementa do voto, decisão (dispositivo), resumo de boletim, verbetação,
  assuntos, legislação, decisões relacionadas e jurisprudencia_relacionados (texto integral da DECISÃO e do
  RELATÓRIO / VOTO); jurisprudencia_situacao vale "Publicada" (selecionada) ou "Descartada";
- o campo `analista` (servidor que fez a análise) não é armazenado;
- a cadeia TLS do host vem incompleta (só a folha "*.tc.df.gov.br", emitida por Let's Encrypt YR1): os
  intermediários YR1 e "Root YR" assinado pela ISRG Root X1, obtidos das URLs AIA do próprio certificado,
  deve ser acrescentado ao repositório de certificados confiáveis do seu cliente;
- maxPerPage grande provoca HTTP 200 com erro fatal do PHP ("Allowed memory size..."): vira erro;
- o Elasticsearch não pagina além de 10.000 (from + tamanho): acima disso o cliente pede recorte menor.
```

## Uso responsável

- Faça no máximo 1 requisição por segundo (ou menos, se a nota acima pedir).
- Guarde o resultado em vez de consultar de novo a mesma coisa.
- Não tente contornar CAPTCHA, login ou bloqueio: se aparecer, pare.
- Decisões trazem nomes de pessoas: respeite a LGPD ao guardar e publicar.

[⬅ Voltar para a lista](../README.md)
