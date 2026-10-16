# Tribunal de Contas da União — acórdãos

> Acórdãos do TCU.

| | |
|---|---|
| **Órgão** | TCU |
| **Tipo de acesso** | 🔧 JSON do site oficial |
| **Autenticação** | Nenhuma |
| **Site oficial** | <https://pesquisa.apps.tcu.gov.br/> |
| **Documentação oficial** | <https://sites.tcu.gov.br/dados-abertos/webservices-tcu/> |
| **Domínios usados** | `dados-abertos.apps.tcu.gov.br`, `pesquisa.apps.tcu.gov.br` |
| **Aceita busca por palavra** | não |
| **Aceita filtro por data** | sim |
| **Verificado em** | outubro de 2026 |

## Resumo

Lista e datas pelo webservice documentado de dados abertos; texto (acórdão, relatório e voto) pela API da pesquisa integrada, uma chamada por acórdão. opção `texto`='false' usa só o webservice documentado. Período = data da sessão. Serviços do TCU podem ficar fora do ar entre 20h e 21h.

## Como a API funciona (notas verificadas ao vivo)

```text
TCU — acórdãos do Tribunal de Contas da União (lista oficial + texto da pesquisa integrada).

Fontes oficiais, verificadas ao vivo em 12/10/2026:
(a) Webservice documentado em sites.tcu.gov.br/dados-abertos/webservices-tcu/:
    GET https://dados-abertos.apps.tcu.gov.br/api/acordao/recupera-acordaos?inicio=N&quantidade=M → lista JSON
    (key, tipo, anoAcordao, titulo, numeroAcordao, numeroAta, colegiado, dataSessao DD/MM/AAAA, relator,
    situacao, sumario, urlArquivo, urlArquivoPdf, urlAcordao). Sem filtro de data; a lista vem em ordem
    decrescente de dataSessao (0 inversões em 300 itens; ~150 acórdãos por dia de sessão); quantidade=300 aceita.
(b) API JSON da pesquisa integrada (pesquisa.apps.tcu.gov.br, sem documentação pública):
    GET /rest/publico/base/acordao-completo/documento?termo=KEY:"<key>"&ordenacao=...&quantidade=1&inicio=0
    — o mesmo pedido que o front-end faz ao abrir um acórdão — devolve ACORDAO, RELATORIO e VOTO (HTML),
    ASSUNTO, ENTIDADE, TIPOPROCESSO, UNIDADETECNICA, PROC, DTATUALIZACAO etc. O WAF desse host recusa UA de
    navegador e aceita o UA descritivo do projeto.
O recorte por período localiza o início da janela na lista (a) por busca binária e lê até passar da data inicial.
Não são armazenados INTERESSADOS, ADVOGADO nem REPRESENTANTEMP (LGPD).
```

## Uso responsável

- Faça no máximo 1 requisição por segundo (ou menos, se a nota acima pedir).
- Guarde o resultado em vez de consultar de novo a mesma coisa.
- Não tente contornar CAPTCHA, login ou bloqueio: se aparecer, pare.
- Decisões trazem nomes de pessoas: respeite a LGPD ao guardar e publicar.

[⬅ Voltar para a lista](../README.md)
