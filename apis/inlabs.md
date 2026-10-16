# INLABS (Imprensa Nacional) — XML diário do DOU

> Diário Oficial da União do dia (XML/PDF).

| | |
|---|---|
| **Órgão** | IN |
| **Tipo de acesso** | 📘 Oficial documentada |
| **Autenticação** | Cadastro gratuito |
| **Site oficial** | <https://inlabs.in.gov.br/> |
| **Documentação oficial** | <https://github.com/Imprensa-Nacional/inlabs> |
| **Domínios usados** | `inlabs.in.gov.br` |
| **Aceita busca por palavra** | sim |
| **Aceita filtro por data** | sim |
| **Verificado em** | outubro de 2026 |

## Resumo

Exige cadastro gratuito em https://inlabs.in.gov.br/acessar.php e as variáveis JURIS_INLABS_EMAIL e JURIS_INLABS_SENHA. Só os últimos 4 meses (antes disso use dou). parametros: secoes (DO1 padrão; DO2, DO3, DO1E, DO2E, DO3E) e tipos (artType ou subtipo). Termo filtrado localmente. Não validado ao vivo.

## Como a API funciona (notas verificadas ao vivo)

```text
INLABS (Imprensa Nacional) — XML diário do Diário Oficial da União, com cadastro gratuito.

Fonte oficial documentada no repositório da Imprensa Nacional (https://github.com/Imprensa-Nacional/inlabs).
Fatos (fornecidos e conferidos em 12/10/2026 até onde é possível sem credenciais):
- a página https://inlabs.in.gov.br/ redireciona para acessar.php, que traz o formulário de login
  (POST logar.php com os campos email e password) e o de cadastro (registrar.php); sem CAPTCHA;
- o login devolve o cookie inlabs_session_cookie; o download é
  GET https://inlabs.in.gov.br/index.php?p=AAAA-MM-DD&dl=AAAA-MM-DD-<SEÇÃO>.zip com o cookie e o
  cabeçalho origem: 736372697074; seções em XML: DO1, DO2, DO3, DO1E, DO2E, DO3E;
- só os últimos quatro meses ficam disponíveis (datas anteriores: use o cliente dou);
- o XML segue o mesmo esquema da base de dados abertos (ver _dou_xml.py).
Não validado ao vivo (sem credenciais): o comportamento para dia sem edição foi inferido do script oficial
(resposta diferente de 200 = arquivo inexistente) e o teste usa XMLs reais da base de dados abertos.
```

## Uso responsável

- Faça no máximo 1 requisição por segundo (ou menos, se a nota acima pedir).
- Guarde o resultado em vez de consultar de novo a mesma coisa.
- Não tente contornar CAPTCHA, login ou bloqueio: se aparecer, pare.
- Decisões trazem nomes de pessoas: respeite a LGPD ao guardar e publicar.

[⬅ Voltar para a lista](../README.md)
