# Justiça do Trabalho — Jurisprudência Nacional (TST e TRTs)

> Acórdãos do TST e dos 24 TRTs.

| | |
|---|---|
| **Órgão** | JT |
| **Tipo de acesso** | 🔧 JSON do site oficial |
| **Autenticação** | sessionId livre + navegador |
| **Site oficial** | <https://jurisprudencia.jt.jus.br/jurisprudencia-nacional/> |
| **Domínios usados** | `jurisprudencia.jt.jus.br` |
| **Aceita busca por palavra** | sim |
| **Aceita filtro por data** | sim |
| **Verificado em** | outubro de 2026 |

> [!WARNING]
> Responde 403 para IPs de datacenter (testado numa VPS); funciona a partir de conexões residenciais. Limite anônimo: 200 resultados por consulta.

## Resumo

User-Agent de navegador porque o CloudFront do portal recusa UA de robô. Acesso anônimo limitado a 200 itens por consulta (20 páginas de 10): recorte maior gera erro; use parametros tribunais, orgao_julgador, relator, classe ou um termo. Período = data de juntada. Limite de requisições com bloqueio de horas: intervalo de 10 s e parada quando x-rate-limit-remaining < 10. parametros: tribunais (TST,TRT1..TRT24), colecao (acordaos|sentencas|decisoesmonocraticas|precedentes|recursorevista; só acordaos verificada), ordenacao, tem_ementa, somente_ementas.

## Como a API funciona (notas verificadas ao vivo)

```text
Jurisprudência Nacional da Justiça do Trabalho ("Falcão") — TST e TRT1 a TRT24.

Fonte: API JSON do próprio portal jurisprudencia.jt.jus.br (front-end Angular oficial, sem login nem CAPTCHA).
Fatos verificados ao vivo em 12/10/2026 (código do front-end + 3 chamadas à API):
- GET /jurisprudencia-nacional-backend/api/no-auth/pesquisa; o front-end envia sessionId, latitude=0,
  longitude=0 (sem geolocalização), texto já codificado com encodeURIComponent (codificação dupla na URL),
  tribunais (CSV), ordenacao, dataInicio/dataFim (AAAA-MM-DD), colecao, page (0-based) e size;
- sem sessionId a API responde 403; qualquer "_" + 7 caracteres base36 gerado localmente serve;
- o CloudFront recusa User-Agent de robô: o cliente usa um UA de navegador (motivo registrado);
- o período filtra pela data de juntada (dataJuntada), não pela de julgamento; texto é opcional;
- anônimo: size 5 ou 10 e no máximo 20 páginas — page=20 devolve 403 "não tem autorização para ir além da
  página 20" — logo, teto de 200 itens por consulta; quantidadeTotal satura em 10.000;
- envelope {documentos, temasTopFive, quantidadeTotal}; campos: numeroProcesso, siglaClasseProcesso,
  classeProcesso, relator, tribunal, gabinete, turma, textoAcordao (HTML com imagens base64), ementa (HTML),
  possuiEmenta (S/N), idDocumentoAcordao, referenciaLegislativa (lista), dataJulgamento e dataJuntada
  (DD/MM/AAAA), prioridades; highlight* (não armazenados);
- cabeçalho x-rate-limit-remaining (39 com chamadas espaçadas); relatos de 429 com bloqueio de horas após
  ~25 chamadas seguidas — o cliente para antes de esgotar o limite.
```

## Uso responsável

- Faça no máximo 1 requisição por segundo (ou menos, se a nota acima pedir).
- Guarde o resultado em vez de consultar de novo a mesma coisa.
- Não tente contornar CAPTCHA, login ou bloqueio: se aparecer, pare.
- Decisões trazem nomes de pessoas: respeite a LGPD ao guardar e publicar.

[⬅ Voltar para a lista](../README.md)
