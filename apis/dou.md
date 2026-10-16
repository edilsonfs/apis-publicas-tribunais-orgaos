# Diário Oficial da União — base de dados abertos (XML mensal)

> Atos publicados no Diário Oficial da União (arquivos mensais).

| | |
|---|---|
| **Órgão** | IN |
| **Tipo de acesso** | 📦 Arquivo de dados abertos |
| **Autenticação** | Nenhuma |
| **Site oficial** | <https://www.in.gov.br/acesso-a-informacao/dados-abertos/base-de-dados> |
| **Domínios usados** | `www.in.gov.br` |
| **Aceita busca por palavra** | sim |
| **Aceita filtro por data** | sim |
| **Verificado em** | outubro de 2026 |

## Resumo

Arquivos mensais liberados na 1ª terça-feira do mês seguinte: mês não liberado gera erro (o cursor não avança). O S01 passa de 50 MiB (teto próprio de 1 GiB por arquivo). parametros: secoes (S01 padrão, S02, S03) e tipos (artType ou subtipo, ex.: lei,decreto,portaria). Termo filtrado localmente. User-Agent padrão funcionou em 12/10/2026; robots.txt do domínio diz Disallow: /, mas é a página oficial de dados abertos.

## Como a API funciona (notas verificadas ao vivo)

```text
Diário Oficial da União — base de dados abertos da Imprensa Nacional (XML mensal em ZIP).

Fonte oficial em lote: https://www.in.gov.br/acesso-a-informacao/dados-abertos/base-de-dados
(licença do portal: Creative Commons Atribuição-SemDerivações 3.0). Fatos verificados ao vivo em 12/10/2026:
- a página aceita ?ano=AAAA&mes=<NomeDoMês> e lista S01MMAAAA.zip, S02MMAAAA.zip e S03MMAAAA.zip em URLs
  do Liferay com UUID (/documents/49035712/<pasta>/S01082026.zip/<uuid>?version=1.0&t=...&download=true),
  por isso os links são lidos da página; cobertura 01/2002 a 08/2026; mês ainda não liberado não tem links;
- liberação "na primeira terça-feira de cada mês, contendo as edições publicadas no mês anterior";
  "o conteúdo dos arquivos em formato aberto não substitui a publicação da versão certificada (pdf)";
- S01082026.zip tem 52.565.336 bytes (8.590 XML + imagens), acima do limite padrão do cliente
  (50 MiB): o download usa teto próprio por requisição (_TETO_ZIP);
- a página, o HEAD e o download responderam 200 com o User-Agent padrão do projeto (o bloqueio de UA
  não navegador relatado antes não se repetiu); o robots.txt do domínio diz Disallow: /, mas esta é a
  página oficial de dados abertos indicada pela Imprensa Nacional;
- o portal dados.gov.br (organização imprensa-nacional-in) responde 401 na API (exige chave): não usado.
O esquema do XML está em _dou_xml.py. Seção 1 traz os atos normativos; S02 (pessoal) e S03 (contratos)
só entram com opção `secoes`.
```

## Uso responsável

- Faça no máximo 1 requisição por segundo (ou menos, se a nota acima pedir).
- Guarde o resultado em vez de consultar de novo a mesma coisa.
- Não tente contornar CAPTCHA, login ou bloqueio: se aparecer, pare.
- Decisões trazem nomes de pessoas: respeite a LGPD ao guardar e publicar.

[⬅ Voltar para a lista](../README.md)
