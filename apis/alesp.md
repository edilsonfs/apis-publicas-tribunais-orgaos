# Assembleia Legislativa de São Paulo — normas estaduais (dados abertos)

> Normas do Estado de São Paulo (metadados).

| | |
|---|---|
| **Órgão** | ALESP |
| **Tipo de acesso** | 📦 Arquivo de dados abertos |
| **Autenticação** | Nenhuma |
| **Site oficial** | <https://www.al.sp.gov.br/dados-abertos/recurso/49> |
| **Documentação oficial** | <https://www.al.sp.gov.br/repositorioDados/docs/legislacao/legislacao_normas.pdf> |
| **Domínios usados** | `www.al.sp.gov.br` |
| **Aceita busca por palavra** | sim |
| **Aceita filtro por data** | não |
| **Verificado em** | outubro de 2026 |

## Resumo

Só metadados (ementa, número, caderno e página do DOE, ficha oficial): sem texto integral. Cada coleta baixa o arquivo completo (~10 MB); o período filtra localmente pela data de PROMULGAÇÃO (normas cadastradas com atraso exigem recarga completa sem período). DataDO do arquivo é carimbo de carga, não data do Diário. parametros: tipos (Lei, Decreto... ou subtipo). Termo filtrado localmente na ementa.

## Como a API funciona (notas verificadas ao vivo)

```text
Assembleia Legislativa de São Paulo — normas estaduais (dados abertos, carga completa em XML).

Fonte oficial em lote: recurso "Normas" do portal de dados abertos (https://www.al.sp.gov.br/dados-abertos/recurso/49),
arquivo https://www.al.sp.gov.br/repositorioDados/legislacao/legislacao_normas.zip, atualização diária,
dicionário em https://www.al.sp.gov.br/repositorioDados/docs/legislacao/legislacao_normas.pdf.
Fatos verificados ao vivo em 12/10/2026:
- ZIP de 10.225.975 bytes com um único legislacao_normas.xml de 118.777.732 bytes (UTF-8):
  <Normas><LegislacaoNorma> com Data (promulgação), Ementa, IdNorma, IdTema, CadDO, DataDO, Numero,
  PagDO, IdTipo, Promulg (E/L), Situacao, URLFicha e, em parte dos registros, Autores;
- 254.060 registros para 183.142 IdNorma: a mesma norma se repete por tema (IdTema) e por caderno/página
  do Diário Oficial; os registros são agregados por IdNorma;
- DataDO não é a data do Diário: é um carimbo de carga (ex.: "2023-05-05 16:38:29" em lei de 1836) e
  está ausente desde 2024 — por isso data_publicacao fica vazia e a promulgação vai em metadados;
- Situacao vem numérica (1 a 6), diferente das letras do dicionário de 2014, e não há tabela oficial
  dos códigos: o código é guardado sem interpretação; os campos URLDO, URLIntegra, URLCompilado, Ambito,
  Index, IdSubTema e NumCompl do dicionário não aparecem no arquivo atual;
- tipos (IdTipo -> DsTipo) do recurso oficial legislacao_tipo_normas.xml (14 tipos, conferido no mesmo dia);
- a ficha (URLFicha, publicada com http://) responde em https://www.al.sp.gov.br/norma/{IdNorma}.
```

## Uso responsável

- Faça no máximo 1 requisição por segundo (ou menos, se a nota acima pedir).
- Guarde o resultado em vez de consultar de novo a mesma coisa.
- Não tente contornar CAPTCHA, login ou bloqueio: se aparecer, pare.
- Decisões trazem nomes de pessoas: respeite a LGPD ao guardar e publicar.

[⬅ Voltar para a lista](../README.md)
