# STJ — precedentes qualificados (dados abertos)

> Temas repetitivos e precedentes do STJ.

| | |
|---|---|
| **Órgão** | STJ |
| **Tipo de acesso** | 📦 Arquivo de dados abertos |
| **Autenticação** | Nenhuma |
| **Site oficial** | <https://dadosabertos.web.stj.jus.br/dataset/precedentes-qualificados> |
| **Documentação oficial** | <https://dadosabertos.web.stj.jus.br/dataset/precedentes-qualificados> |
| **Domínios usados** | `dadosabertos.web.stj.jus.br` |
| **Aceita busca por palavra** | não |
| **Aceita filtro por data** | não |
| **Verificado em** | outubro de 2026 |

## Resumo

Carga completa (dois CSV, ~4 MB) a cada coleta; o índice descarta o que não mudou.

## Como a API funciona (notas verificadas ao vivo)

```text
STJ — Precedentes qualificados (temas repetitivos, controvérsias, IAC, PUIL, SIRDR) — dados abertos, CC-BY.

Fonte: conjunto "precedentes-qualificados" no CKAN oficial (dadosabertos.web.stj.jus.br), extraído do Sistema
de Gestão de Precedentes do STJ. Fatos verificados ao vivo em 12/10/2026:
- quatro recursos: Temas.csv (2,6 MB), Processos.csv (1,1 MB) e os dicionários de cada um; CSV em UTF-8,
  separador vírgula, campos com quebras de linha entre aspas;
- 2.403 linhas em Temas.csv; `sequencialPrecedente` liga os dois arquivos e se repete em Temas.csv quando o
  precedente se vincula a mais de um tema de repercussão geral do STF (só mudam numeroRepercussaoGeralSTF e
  descricaoRepercussaoGeral) — as linhas são agregadas;
- tipoPrecedente: Tema, Controvérsia, PUIL, IAC, SIRDR; orgaoJulgador: S1, S2, S3, CE (ou vazio);
- Processos.csv (5.554 linhas): Processo, numeroRegistro, ministroRelator, leadingCase (S/N), datas de
  afetação/julgamento, tribunal de origem, processos suspensos na origem etc.; também repete linhas
  idênticas nos precedentes com vários temas de RG (deduplicadas);
- link oficial do tema: processo.stj.jus.br/repetitivos/temas_repetitivos/pesquisa.jsp (respondeu 200).
Carga completa a cada coleta (suporta_periodo=False).
```

## Uso responsável

- Faça no máximo 1 requisição por segundo (ou menos, se a nota acima pedir).
- Guarde o resultado em vez de consultar de novo a mesma coisa.
- Não tente contornar CAPTCHA, login ou bloqueio: se aparecer, pare.
- Decisões trazem nomes de pessoas: respeite a LGPD ao guardar e publicar.

[⬅ Voltar para a lista](../README.md)
