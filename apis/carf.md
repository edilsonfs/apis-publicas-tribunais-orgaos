# CARF — acórdãos do Conselho Administrativo de Recursos Fiscais

> Acórdãos do CARF (tributário).

| | |
|---|---|
| **Órgão** | CARF |
| **Tipo de acesso** | 🔧 JSON do site oficial |
| **Autenticação** | Nenhuma |
| **Site oficial** | <https://acordaos.economia.gov.br/> |
| **Domínios usados** | `acordaos.economia.gov.br` |
| **Aceita busca por palavra** | sim |
| **Aceita filtro por data** | sim |
| **Verificado em** | outubro de 2026 |

## Resumo

Período = data de publicação (dt_publicacao_tdt). Termo com a mesma configuração do buscador oficial (edismax sobre _texto, todas as palavras). Inteiro teor = texto extraído do PDF pelo próprio CARF.

## Como a API funciona (notas verificadas ao vivo)

```text
CARF — Conselho Administrativo de Recursos Fiscais (Ministério da Fazenda): acórdãos e resoluções.

Fonte: índice Solr público do próprio domínio oficial acordaos.economia.gov.br (base do sistema de pesquisa).
Fatos verificados ao vivo em 12/10/2026:
- GET /solr/acordaos2/select?wt=json (também /browse); 3.695 documentos publicados em 09/2026;
- o handler oficial /browse usa defType=edismax, qf=_texto (campo agregado) e mm=100% — reproduzido aqui
  no /select para buscas com termo;
- recorte por período com fq=dt_publicacao_tdt:[AAAA-MM-DDT00:00:00Z TO AAAA-MM-DDT23:59:59Z];
- paginação profunda com cursorMark (sort "dt_publicacao_tdt asc,id asc"), sem teto; rows até 100;
- campos: id, numero_decisao_s, numero_processo_s (processo administrativo), ementa_s, decisao_txt (lista),
  conteudo_txt ("Metadados => ...; Conteúdo => <texto extraído do PDF>"), nome_relator_s, turma_s, secao_s,
  dt_sessao_tdt, dt_publicacao_tdt, dt_registro_atualizacao_tdt, ano_publicacao_s, anomes_publicacao_s,
  nome_arquivo_pdf_s → PDF em /acordaos2/pdfs/processados/<nome> (HEAD respondeu 200 application/pdf).
```

## Uso responsável

- Faça no máximo 1 requisição por segundo (ou menos, se a nota acima pedir).
- Guarde o resultado em vez de consultar de novo a mesma coisa.
- Não tente contornar CAPTCHA, login ou bloqueio: se aparecer, pare.
- Decisões trazem nomes de pessoas: respeite a LGPD ao guardar e publicar.

[⬅ Voltar para a lista](../README.md)
