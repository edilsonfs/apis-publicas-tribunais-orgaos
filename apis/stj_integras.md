# STJ — íntegras de decisões terminativas e acórdãos (dados abertos)

> Texto completo das decisões do STJ (desde 2021).

| | |
|---|---|
| **Órgão** | STJ |
| **Tipo de acesso** | 📦 Arquivo de dados abertos |
| **Autenticação** | Nenhuma |
| **Site oficial** | <https://dadosabertos.web.stj.jus.br/dataset/integras-de-decisoes-terminativas-e-acordaos-do-diario-da-justica> |
| **Documentação oficial** | <https://dadosabertos.web.stj.jus.br/dataset/integras-de-decisoes-terminativas-e-acordaos-do-diario-da-justica> |
| **Domínios usados** | `dadosabertos.web.stj.jus.br` |
| **Aceita busca por palavra** | não |
| **Aceita filtro por data** | sim |
| **Verificado em** | outubro de 2026 |

## Resumo

Arquivos diários publicados no dia útil seguinte: a coleta incremental revisita os últimos 5 dias. Período = data de publicação no DJe (nome do arquivo). Sem processos em segredo de justiça. Teto próprio de 512 MiB por arquivo (ZIPs mensais de 2022 passam de 170 MB).

## Como a API funciona (notas verificadas ao vivo)

```text
STJ — Íntegras de decisões terminativas e acórdãos do Diário da Justiça (dados abertos, CC-BY).

Fonte: conjunto "integras-de-decisoes-terminativas-e-acordaos-do-diario-da-justica" no CKAN oficial
(dadosabertos.web.stj.jus.br). Fatos verificados ao vivo em 12/10/2026:
- 2.643 recursos: dicionário CSV + pares diários "metadadosAAAAMMDD" (JSON) e "AAAAMMDD.zip" (TXT), de
  20210104 a 20261008, publicados no dia útil seguinte (~17h); carga inicial mensal "metadadosAAAAMM.json" /
  "AAAAMM.zip" (2022-02 a 2022-04 e 2022-07; os ZIPs mensais de 2022-02 a 2022-04 têm 170–246 MB);
- há dias com JSON e sem ZIP (ex.: 20260611, 20260615) e JSON republicado no dia seguinte (fica o mais novo);
- metadados: SeqDocumento (= nome do .txt no ZIP), dataPublicacao (AAAA-MM-DD; o dicionário prevê epoch ms),
  tipoDocumento (DECISAO/DECISÃO/ACÓRDÃO), numeroRegistro, processo ("HC 637258"), dataRecebimento,
  dataDistribuicao (ou "dataDistribuição"), NM_MINISTRO (o dicionário chama de "ministro"), recurso
  (AgInt, EDcl…; nulo = processo principal), teor, descricaoMonocratica, assuntos (códigos CNJ);
- textos em UTF-8 com <br>; acórdãos trazem os blocos ACÓRDÃO / EMENTA / RELATÓRIO / VOTO;
- processos em segredo de justiça não são publicados.
O período seleciona os arquivos pela data de publicação no nome; arquivos mensais são filtrados item a item.
```

## Uso responsável

- Faça no máximo 1 requisição por segundo (ou menos, se a nota acima pedir).
- Guarde o resultado em vez de consultar de novo a mesma coisa.
- Não tente contornar CAPTCHA, login ou bloqueio: se aparecer, pare.
- Decisões trazem nomes de pessoas: respeite a LGPD ao guardar e publicar.

[⬅ Voltar para a lista](../README.md)
