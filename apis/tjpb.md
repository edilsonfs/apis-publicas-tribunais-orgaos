# Tribunal de Justiça da Paraíba — jurisprudência do PJe

> Ementas do TJPB (base de 2015–2018).

| | |
|---|---|
| **Órgão** | TJPB |
| **Tipo de acesso** | 🔧 JSON do site oficial |
| **Autenticação** | Nenhuma |
| **Site oficial** | <https://pje-jurisprudencia.tjpb.jus.br/> |
| **Domínios usados** | `pje-jurisprudencia.tjpb.jus.br` |
| **Aceita busca por palavra** | sim |
| **Aceita filtro por data** | sim |
| **Verificado em** | outubro de 2026 |

> [!WARNING]
> A base acessível sem desafio tem decisões de 2015 a 2018; a base atual fica atrás do Cloudflare.

## Resumo

Base de jurisprudência do PJe do TJPB, aparentemente legada (decisões de 2015–2018; nada em 10/2026). Período pela data da ementa (dt_ementa). Termo pesquisado na ementa; parâmetro `escopo`=inteiro_teor pesquisa no teor. Parâmetro `decisoes`=true marca a caixa 'Decisões Monocráticas'. A busca devolve só ementa, número e data; o teor fica na página /jurisprudencia/view/<id>.

## Como a API funciona (notas verificadas ao vivo)

```text
TJPB — jurisprudência do PJe (pje-jurisprudencia.tjpb.jus.br).

Fonte: JSON servido pela aplicação Laravel/Vue oficial. Fatos verificados ao vivo em 12/10/2026:
- GET https://pje-jurisprudencia.tjpb.jus.br/ devolve a página pública com <meta name="_token"> (token CSRF do
  Laravel, ligado ao cookie de sessão) — sem CAPTCHA nem desafio de WAF;
- POST /api/jurisprudencia/pesquisar com JSON {_token, jurisprudencia:{ementa, inteiro_teor, nr_processo,
  id_classe_judicial, id_orgao_julgador, id_relator, dt_inicio, dt_fim (dd/mm/aaaa), id_origem, decisoes}, page}
  (page começa em 1; o front pagina de 10 em 10) e X-Requested-With: XMLHttpRequest; `decisoes` é a caixa
  "Decisões Monocráticas" do formulário;
- resposta {total, hits[]}; cada hit traz _id, _score, ementa, numero_processo (CNJ formatado) e dt_ementa
  (dd/mm/aaaa); o front liga cada resultado a /jurisprudencia/view/<_id>;
- ementa "dano moral" sem período: total=49.220, com dt_ementa entre 2015 e 2018 nos 10 primeiros; período de
  01 a 07/10/2026: total=0 — o índice do PJe parece legado (sem decisões recentes);
- a outra base (app.tjpb.jus.br/juris-pb-backend) fica atrás de Cloudflare e respondia 503: não é usada.
```

## Uso responsável

- Faça no máximo 1 requisição por segundo (ou menos, se a nota acima pedir).
- Guarde o resultado em vez de consultar de novo a mesma coisa.
- Não tente contornar CAPTCHA, login ou bloqueio: se aparecer, pare.
- Decisões trazem nomes de pessoas: respeite a LGPD ao guardar e publicar.

[⬅ Voltar para a lista](../README.md)
