# Tribunal de Justiça do Distrito Federal e dos Territórios — jurisprudência

> Jurisprudência do TJDFT.

| | |
|---|---|
| **Órgão** | TJDFT |
| **Tipo de acesso** | 📘 Oficial documentada |
| **Autenticação** | Nenhuma |
| **Site oficial** | <https://jurisdf.tjdft.jus.br/> |
| **Documentação oficial** | <https://www.tjdft.jus.br/transparencia/tecnologia-da-informacao-e-comunicacao/dados-abertos/webservice-ou-api> |
| **Domínios usados** | `jurisdf.tjdft.jus.br` |
| **Aceita busca por palavra** | sim |
| **Aceita filtro por data** | sim |
| **Verificado em** | outubro de 2026 |

## Resumo

Período por data de publicação (parâmetro campo_data=julgamento troca o critério), consultado dia a dia. Parâmetro opcional `bases` (ex.: acordaos,decisoes); por padrão a API devolve a base de acórdãos (2º grau e Turmas Recursais). Sem link permanente por documento: o link aponta para o portal jurisdf.

## Como a API funciona (notas verificadas ao vivo)

```text
TJDFT — API pública de consulta à jurisprudência (jurisdf).

Fonte: API documentada pelo próprio TJDFT (página "Webservice ou API" do portal de transparência e o PDF
documentacao_api_seti_transparencia.pdf). Fatos verificados ao vivo em 12/10/2026:
- POST https://jurisdf.tjdft.jus.br/api/v1/pesquisa com JSON {query, termosAcessorios:[{campo, valor}],
  pagina (começa em 0), tamanho (máximo 30), sinonimos, espelho, inteiroTeor, retornaInteiroTeor,
  retornaTotalizacao}; `query` vazia é aceita quando há filtro;
- a documentação lista os campos de termosAcessorios (base, subbase, origem, uuid, identificador,
  processo, nomeRelator, nomeRevisor, nomeRelatorDesignado, descricaoOrgaoJulgador, dataJulgamento,
  dataPublicacao, descricaoClasseCnj); as datas recebem um único dia (AAAA-MM-DD), sem intervalo, por
  isso o cliente consulta dia a dia;
- dataPublicacao=2026-10-01 devolveu hits.value=692, todos na base "acordaos" (subbases acordaos e
  acordaos-tr); com base=decisoes o mesmo dia devolveu 0;
- resposta {hits:{value}, agregacoes, paginacao:{pagina, tamanho}, registros[]}; cada registro traz uuid,
  identificador (número do acórdão), base, subbase, processo, nomeRelator, descricaoOrgaoJulgador,
  dataJulgamento e dataPublicacao (ISO em UTC), ementa, decisao, inteiroTeor (texto), codigoClasseCnj,
  segredoJustica, turmaRecursal e possuiInteiroTeor; não há link permanente por documento;
- o balanceador alterna índices: o cookie de sessão (guardado pelo cliente HTTP) mantém a paginação
  no mesmo índice.
```

## Uso responsável

- Faça no máximo 1 requisição por segundo (ou menos, se a nota acima pedir).
- Guarde o resultado em vez de consultar de novo a mesma coisa.
- Não tente contornar CAPTCHA, login ou bloqueio: se aparecer, pare.
- Decisões trazem nomes de pessoas: respeite a LGPD ao guardar e publicar.

[⬅ Voltar para a lista](../README.md)
