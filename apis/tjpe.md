# Tribunal de Justiça de Pernambuco — jurisprudência

> Acórdãos e decisões do TJPE com inteiro teor.

| | |
|---|---|
| **Órgão** | TJPE |
| **Tipo de acesso** | 🔧 JSON do site oficial |
| **Autenticação** | Nenhuma |
| **Site oficial** | <https://consultajurisprudencia.app.tjpe.jus.br/> |
| **Domínios usados** | `consultajurisprudencia.app.tjpe.jus.br` |
| **Aceita busca por palavra** | sim |
| **Aceita filtro por data** | sim |
| **Verificado em** | outubro de 2026 |

## Resumo

Sem 1º grau. Sem link permanente por documento: o link aponta para o portal de pesquisa.

## Como a API funciona (notas verificadas ao vivo)

```text
TJPE — consulta de jurisprudência (2º grau e Turmas Recursais).

Fonte: API REST JSON servida pelo próprio portal oficial (consultajurisprudencia.app.tjpe.jus.br),
linkada em portal.tjpe.jus.br/web/jurisprudencia. Fatos verificados ao vivo em 12/10/2026:
- GET /api/v1/jurisprudencias com filtros no padrão `campo.operador` (pesquisaLivre.contains,
  dataPublicacao.greaterThanOrEqual / lessThanOrEqual, tipoSentenca.in);
- `tipoSentenca.in` é obrigatório (sem ele a API responde 500); A = acórdão, D = decisão monocrática;
- total no cabeçalho x-total-count, que satura em 10.000; size máximo 100; page começa em 0;
- não há link permanente por documento (chave.equals é ignorado).
O servidor envia cadeia TLS incompleta; o intermediário Amazon RSA 2048 M01 deve ser acrescentado ao repositório de certificados confiáveis do seu cliente.
```

## Uso responsável

- Faça no máximo 1 requisição por segundo (ou menos, se a nota acima pedir).
- Guarde o resultado em vez de consultar de novo a mesma coisa.
- Não tente contornar CAPTCHA, login ou bloqueio: se aparecer, pare.
- Decisões trazem nomes de pessoas: respeite a LGPD ao guardar e publicar.

[⬅ Voltar para a lista](../README.md)
