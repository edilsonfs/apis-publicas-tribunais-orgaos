# Portal normas.leg.br (Congresso Nacional) — texto vigente de normas federais

> Texto das leis federais (original e atualizado).

| | |
|---|---|
| **Órgão** | CN |
| **Tipo de acesso** | 🔧 JSON do site oficial |
| **Autenticação** | Nenhuma |
| **Site oficial** | <https://normas.leg.br/> |
| **Documentação oficial** | <https://normas.leg.br/v3/api-docs> |
| **Domínios usados** | `normas.leg.br`, `legis.senado.leg.br` |
| **Aceita busca por palavra** | sim |
| **Aceita filtro por data** | sim |
| **Verificado em** | outubro de 2026 |

> [!WARNING]
> O próprio portal marca os textos como sem valor legal oficial: o valor legal é o do Diário Oficial.

## Resumo

Texto compilado SEM valor legal (UnofficialLegalValue no JSON-LD): o texto oficial é o publicado no DOU, registrado em metadados['versoes']. Período = data de assinatura (URNs listadas na API do Senado); aceita parametros urns (lista) e tipos (siglas do Senado: LEI,DEC,MPV...). Termo filtrado localmente.

## Como a API funciona (notas verificadas ao vivo)

```text
Portal normas.leg.br (Congresso Nacional) — texto compilado vigente das normas federais.

Fonte oficial: API pública do portal, descrita em OpenAPI (https://normas.leg.br/v3/api-docs), sem
página de documentação nem termos de uso; licença declarada no JSON-LD: CC BY 4.0. Fatos verificados
ao vivo em 12/10/2026:
- GET /api/public/normas?urn=<urn>&tipo_documento=maior-detalhe devolve JSON-LD schema.org
  "Legislation": headline, name, alternateName, abstract (ementa), legislationDate (assinatura),
  datePublished, legislationType, keywords, about (temas), legislationAmends / Repeals / Commences,
  legislationSourceProcess, sameAs (LexML e Senado), license e encoding;
- encoding é objeto (norma recente, só "Original") ou lista com até três versões: Original
  (PublicacaoOriginal), Intermediate (Retificacao) e Current (CompilacaoMonoVigenteNaCD); todas com
  legislationLegalValue = UnofficialLegalValue — o texto com valor legal é o publicado no DOU
  (isBasedOn.legislationLegalVersion = OfficialLegalValue);
- encoding.contentUrl aponta para /api/binario/{id}/texto, que responde 404: o HTML real está em
  /api/public/binario/{id}/texto (o <head> traz nomes de servidores em comentário; descartado);
- normas recentes trazem hasPart (articulação estruturada), não usado: o texto vem do binário;
- não há listagem por período: as URNs são obtidas na API do Senado (data de assinatura, dia a dia).
Algumas normas (decretos e MPs antigos) vêm sem encoding: o documento sai com inteiro_teor None.
```

## Uso responsável

- Faça no máximo 1 requisição por segundo (ou menos, se a nota acima pedir).
- Guarde o resultado em vez de consultar de novo a mesma coisa.
- Não tente contornar CAPTCHA, login ou bloqueio: se aparecer, pare.
- Decisões trazem nomes de pessoas: respeite a LGPD ao guardar e publicar.

[⬅ Voltar para a lista](../README.md)
