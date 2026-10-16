# Tribunal de Contas do Estado do Rio de Janeiro — pesquisa textual

> Processos e decisões do TCE-RJ.

| | |
|---|---|
| **Órgão** | TCE-RJ |
| **Tipo de acesso** | 🔧 JSON do site oficial |
| **Autenticação** | Nenhuma |
| **Site oficial** | <https://www.tcerj.tc.br/consulta-processo/PesquisaTextual> |
| **Domínios usados** | `www.tcerj.tc.br` |
| **Aceita busca por palavra** | sim |
| **Aceita filtro por data** | sim |
| **Verificado em** | outubro de 2026 |

## Resumo

Período pela data da SESSÃO PLENÁRIA (opção `campo_data`='cadastro' usa a data de cadastro do processo). Cada documento encontrado (voto, acórdão, ofício...) vira um Documento; os "dados cadastrais" do processo viram tipo PROCESSO. O texto devolvido pela busca é um trecho em volta do termo (metadados['texto_parcial']); o inteiro teor é o PDF público em url_inteiro_teor. parametros: bases (lista entre dadosCadastrais, infobase, votos, eTCERJ, oficios, registros, acordaos, anexos, certidoes, diariosOficiais, digitalizacoes, termos, transformados, condenacoes, atas), interessado. Consulta sem termo não verificada.

## Como a API funciona (notas verificadas ao vivo)

```text
TCE-RJ — pesquisa textual (www.tcerj.tc.br/consulta-processo/PesquisaTextual).

Fonte: JSON da API "liana" consumida pela aplicação Angular oficial da pesquisa textual.
Fatos verificados ao vivo em 15/10/2026:
- a página /consulta-processo/PesquisaTextual carrega a aplicação /pesquisa-textual/app (rota "app" ->
  IframeModule, chunks 10 e 855); o serviço do main-es2015 faz POST
  https://www.tcerj.tc.br/liana-pesquisa-externo/api/pesquisatextual/pagina/{p}/tamanhoPagina/{n} (o front usa
  n = 20) e o componente de pesquisa (chunk 10) monta o corpo: comTodasAsPalavras (em maiúsculas), interessado,
  dataCadIni/dataCadFim ("Processo cadastrado entre"), dataSessaoIni/dataSessaoFim ("Sessão Plenária realizada
  entre"; o datepicker envia um Date serializado em ISO UTC), naturezas, naturezasExcluidas (null numa pesquisa
  nova), bases (dadosCadastrais, infobase, votos, eTCERJ, oficios, registros, acordaos, anexos, certidoes,
  diariosOficiais, digitalizacoes, termos, transformados, condenacoes — marcadas — e atas, desmarcada),
  baseComplementar=1, retornaTextoDocumento, pagina e quantidadePorPagina;
- nenhum desses arquivos nem a API usam CAPTCHA; a tela /consulta-processo/Processo/Details (reCAPTCHA) não é usada;
- "licitação" com sessão entre 01 e 30/09/2026: quantidadeTotal 255, 20 grupos (processos) por página, cada um com
  numero/dv/ano, titulo (com <mark> no termo), interessado, orgao, observacao e a lista "resultados" de documentos:
  idDocumento, tipoDocumentoPesquisado (0 = dados cadastrais do processo; 2 = categoria "VOTO"...), categoria,
  texto (com retornaTextoDocumento=true, um trecho de até ~1.300 caracteres em volta do termo, que termina em
  "... " e usa  isolado como quebra de linha), guidDocumento, idArquivo,
  sigiloso, dataDocumento ("2026-09-24T00:00:00-03:00", dentro do período pedido) e observacaoDocumento;
- o PDF público sai de https://www.tcerj.tc.br/documento-webapi-externo/api/documento/processo/{numero}/{dv}/{ano}/
  arquivo/{idArquivo} ou .../indentificador/{guid} (grafia da própria API) — é o url_inteiro_teor;
- LGPD: "interessado" (pode ser pessoa física) não vai para os metadados.
```

## Uso responsável

- Faça no máximo 1 requisição por segundo (ou menos, se a nota acima pedir).
- Guarde o resultado em vez de consultar de novo a mesma coisa.
- Não tente contornar CAPTCHA, login ou bloqueio: se aparecer, pare.
- Decisões trazem nomes de pessoas: respeite a LGPD ao guardar e publicar.

[⬅ Voltar para a lista](../README.md)
