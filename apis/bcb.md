# Banco Central do Brasil — normas (CMN e BCB)

> Resoluções, circulares e normas do Banco Central.

| | |
|---|---|
| **Órgão** | BCB |
| **Tipo de acesso** | 🔧 JSON do site oficial |
| **Autenticação** | Nenhuma |
| **Site oficial** | <https://www.bcb.gov.br/estabilidadefinanceira/buscanormas> |
| **Domínios usados** | `www.bcb.gov.br` |
| **Aceita busca por palavra** | sim |
| **Aceita filtro por data** | sim |
| **Verificado em** | outubro de 2026 |

## Resumo

Período = data de divulgação no portal (convertida para o horário de Brasília); data_publicacao = data do DOU quando informada. opção `tipos` filtra no servidor pelo nome exato (Resolução CMN, Resolução BCB, Circular, Carta Circular, Comunicado, Instrução Normativa BCB...). Uma requisição extra por norma para o texto.

## Como a API funciona (notas verificadas ao vivo)

```text
Banco Central do Brasil — busca de normas (Resoluções CMN e BCB, Circulares, Comunicados, INs...).

Fonte: JSON servido pelo próprio portal oficial (www.bcb.gov.br) à página "Busca de normas", sem CAPTCHA.
Fatos verificados ao vivo em 12/10/2026:
- GET /api/search/app/normativos/buscanormativos?querytext=ContentType:normativo AND contentSource:normativos
  [AND <termo>]&rowlimit=N&startrow=M&sortlist=Data1OWSDATE:descending&refinementfilters=Data:range(
  datetime(AAAA-MM-DD),datetime(AAAA-MM-DD)) -> {TotalRows, RowCount, Rows[]}; cada linha: title,
  TipodoNormativoOWSCHCS, NumeroOWSNMBR ("5343.00000000000"), data (UTC), RefinableString01 (data local),
  ResponsavelOWSText, RevogadoOWSBOOL, CanceladoOWSBOOL, AssuntoNormativoOWSMTXT, listItemId;
  01/09 a 10/10/2026 -> 290 normas (259 Comunicados, 14 Resoluções BCB, 8 INs BCB, 4 Resoluções CMN...);
- o filtro por tipo funciona como refinamento FQL:
  and(Data:range(...),TipodoNormativoOWSCHCS:equals("Resolução CMN")) -> 4 resoluções no mesmo período;
- texto: GET /api/conteudo/app/normativos/exibenormativo?p1=<tipo>&p2=<número> (ex.: Resolução CMN 5.343) e
  /exibeoutrasnormas?p1=&p2= (ex.: Comunicado 46.105) -> conteudo[]: Titulo, Tipo, DOU ("Publicada no DOU
  de 28/9/2026, Seção 1, p. 50."), Id, Data, DataTexto, Numero, VersaoNormativo, Assunto, NormasVinculadas,
  Referencias, Atualizacoes, Revogado, Cancelado, Texto (HTML), Voto; o endpoint "errado" responde 200 com
  conteudo vazio, então o outro é tentado em seguida;
- listItemId pertence a listas diferentes (pode repetir entre elas): o id estável é tipo + número;
- página pública: https://www.bcb.gov.br/estabilidadefinanceira/<exibenormativo|exibeoutrasnormas>?tipo=&numero=.
O limite de paginação da busca não é documentado: recortes com 10.000+ itens são recusados e uma página
vazia antes do total é tratada como truncamento.
```

## Uso responsável

- Faça no máximo 1 requisição por segundo (ou menos, se a nota acima pedir).
- Guarde o resultado em vez de consultar de novo a mesma coisa.
- Não tente contornar CAPTCHA, login ou bloqueio: se aparecer, pare.
- Decisões trazem nomes de pessoas: respeite a LGPD ao guardar e publicar.

[⬅ Voltar para a lista](../README.md)
