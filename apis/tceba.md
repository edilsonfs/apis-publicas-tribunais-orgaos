# Tribunal de Contas do Estado da Bahia — jurisprudência

> Decisões do TCE-BA.

| | |
|---|---|
| **Órgão** | TCE-BA |
| **Tipo de acesso** | 🔧 JSON do site oficial |
| **Autenticação** | Nenhuma |
| **Site oficial** | <https://www.tce.ba.gov.br/jurisprudencia/consulta> |
| **Domínios usados** | `proinfo.tce.ba.gov.br` |
| **Aceita busca por palavra** | sim (obrigatória) |
| **Aceita filtro por data** | sim |
| **Verificado em** | outubro de 2026 |

## Resumo

Exige termo; a fonte devolve no máximo 200 decisões por consulta, sem paginação (acima disso responde 400 e o cliente pede refinamento). Período aplicado no cliente pela data da sessão. Filtros opcionais repassados como na página oficial: idRelator, numeroProtocolo, anoProtocolo, anoDecisao, anoExercicio, numeroDecisao, idColegiado, idNatureza, listaIdTipoDecisao. Intermediário TLS Sectigo OV R36 em repositório de certificados confiáveis.

## Como a API funciona (notas verificadas ao vivo)

```text
TCE-BA — consulta de jurisprudência (www.tce.ba.gov.br/jurisprudencia/consulta).

Fonte: JSON da API ProInfo (proinfo.tce.ba.gov.br/rest3) chamada pelo script oficial da página de consulta.
Fatos verificados ao vivo em 12/10/2026:
- a página define o servidor em <input id="servidorRest" value="https://proinfo.tce.ba.gov.br/rest3"> e o script
  ProInfoJulgamento.js monta GET .../api/portaltce/julgamento/obterDecisoes com, nesta ordem, termo, qtRegistros,
  idRelator, numeroProtocolo, anoProtocolo, anoDecisao, anoExercicio, numeroDecisao, idColegiado, idNatureza,
  listaIdTipoDecisao, resumoDocumento e nomeOrgaoUnidade (só os preenchidos); o front fixa qtRegistros=200;
- não há paginação nem filtro por data: quando há mais ocorrências que qtRegistros a API responde HTTP 400
  {"message": "A sua pesquisa retornou mais de N ocorrências. Por favor, refine..."} (visto com qtRegistros=3);
  o cliente converte isso em erro pedindo refinamento;
- termo "fracionamento" + anoDecisao=2026: 1 item (Resolução nº 000097/2025, sessão de 18/12/2025) — o filtro
  anoDecisao não corresponde ao ano do documento, por isso o cliente não o deriva do período;
- cada item traz nomeColegiado, tituloDocumentoDecisao, dataSessaoJulgamento ("2025-12-18 14:30:00.0"),
  anoDocumento, idProtocolo, idColegiado, dataConferenciaDecisao, idTipoDecisao, idDocumentoDecisao,
  resumoExibicao (texto integral do documento), resumoDocumento (ementa), numeroProtocolo ("TCE/014914/2025"),
  nomeTipoDecisao, nomeRelator e numeroDocumento; a deduplicação usa idDocumentoDecisao; resumoDocumento
  pode vir como "..." (sem ementa), tratado como vazio;
- o front liga o processo a https://www.tce.ba.gov.br/servicos/processo/<numeroProtocolo com "/" trocada por "-">;
- a cadeia TLS do host é incompleta: o intermediário Sectigo OV R36 deve ser acrescentado ao repositório de certificados confiáveis do seu cliente.
```

## Uso responsável

- Faça no máximo 1 requisição por segundo (ou menos, se a nota acima pedir).
- Guarde o resultado em vez de consultar de novo a mesma coisa.
- Não tente contornar CAPTCHA, login ou bloqueio: se aparecer, pare.
- Decisões trazem nomes de pessoas: respeite a LGPD ao guardar e publicar.

[⬅ Voltar para a lista](../README.md)
