# STJ — espelhos de acórdãos (dados abertos)

> Espelhos de acórdãos do STJ (ementa, tese, legislação citada).

| | |
|---|---|
| **Órgão** | STJ |
| **Tipo de acesso** | 📦 Arquivo de dados abertos |
| **Autenticação** | Nenhuma |
| **Site oficial** | <https://dadosabertos.web.stj.jus.br/dataset/?q=espelhos-de-acordaos> |
| **Documentação oficial** | <https://scon.stj.jus.br/docs_internet/jurisprudencia/ajuda/Espelho_do_Acordao_atualizado.pdf> |
| **Domínios usados** | `dadosabertos.web.stj.jus.br` |
| **Aceita busca por palavra** | não |
| **Aceita filtro por data** | sim |
| **Verificado em** | outubro de 2026 |

## Resumo

Arquivos mensais (data de extração no nome, publicados no início do mês seguinte): a coleta incremental revisita os últimos 45 dias. opção `orgaos` restringe os conjuntos (ex.: primeira-turma,corte-especial). O campo 'decisao' é o resultado do julgamento, não o inteiro teor. Teto próprio de 512 MiB por arquivo.

## Como a API funciona (notas verificadas ao vivo)

```text
STJ — Espelhos de acórdãos (dados abertos, CC-BY), um conjunto por órgão julgador.

Fonte: conjuntos "espelhos-de-acordaos-<órgão>" no CKAN oficial (dadosabertos.web.stj.jus.br).
Fatos verificados ao vivo em 12/10/2026:
- 10 conjuntos (Corte Especial, 1ª a 3ª Seção, 1ª a 6ª Turma), cada um com: ZIP inicial com todo o histórico
  até 07–08/05/2022 (5 a 115 MB), dicionário CSV e um JSON mensal "AAAAMMDD.json" de 20220531 a 20260831;
- segundo a descrição oficial, o nome é a data de extração e cada arquivo traz só o que entrou na base desde o
  anterior; o mesmo acórdão pode constar de dois arquivos (o `id` resolve a duplicidade);
- há recurso sem nome (o nome do arquivo na URL tem a data) e recurso vazio (ignorado);
- campos (dicionário oficial dicionario-espelhodoacordao.csv): id, numeroDocumento, numeroProcesso,
  numeroRegistro, siglaClasse, descricaoClasse, classePadronizada, nomeOrgaoJulgador, ministroRelator,
  dataPublicacao ("DJEN       DATA:29/06/2026"), ementa, tipoDeDecisao, dataDecisao (AAAAMMDD),
  decisao (resultado do julgamento — NÃO é o inteiro teor), jurisprudenciaCitada, notas,
  informacoesComplementares, termosAuxiliares, teseJuridica, tema, referenciasLegislativas (lista),
  acordaosSimilares (lista).
O período seleciona os arquivos pela data de extração do nome; não há filtro item a item.
```

## Uso responsável

- Faça no máximo 1 requisição por segundo (ou menos, se a nota acima pedir).
- Guarde o resultado em vez de consultar de novo a mesma coisa.
- Não tente contornar CAPTCHA, login ou bloqueio: se aparecer, pare.
- Decisões trazem nomes de pessoas: respeite a LGPD ao guardar e publicar.

[⬅ Voltar para a lista](../README.md)
