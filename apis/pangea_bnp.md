# CNJ — Banco Nacional de Precedentes (Pangea)

> Precedentes qualificados de todo o país (teses e temas).

| | |
|---|---|
| **Órgão** | CNJ |
| **Tipo de acesso** | 🔧 JSON do site oficial |
| **Autenticação** | Nenhuma |
| **Site oficial** | <https://pangeabnp.pdpj.jus.br/> |
| **Documentação oficial** | <https://docs.pdpj.jus.br/servicos-negociais/BNP-Pangea/BNP%20-%20Manual%20de%20Utiliza%C3%A7%C3%A3o> |
| **Domínios usados** | `pangeabnp.pdpj.jus.br` |
| **Aceita busca por palavra** | sim |
| **Aceita filtro por data** | sim |
| **Verificado em** | outubro de 2026 |

## Resumo

Período = data da última atualização do precedente. parametros: orgaos (siglas do BNP, ex.: STJ,STF,TJSC,TRF04,TRT02; padrão: todos com precedentes), tipos (espécies, ex.: RR,RG,SUM,IRDR; padrão: todas as válidas para os órgãos), cancelados (true/false), ordenacao. Documentação é o manual do usuário, não da API.

## Como a API funciona (notas verificadas ao vivo)

```text
CNJ — Banco Nacional de Precedentes (BNP/Pangea): teses de precedentes qualificados de todos os tribunais.

Fonte: API JSON do próprio portal pangeabnp.pdpj.jus.br (front-end Angular oficial, sem login nem CAPTCHA).
Fatos verificados ao vivo em 12/10/2026 (código do front-end + chamadas à API):
- GET /api/v1/parametros: espécies (sigla/descrição), órgãos (93, com grupoEspecies e semPrecedentes),
  grupos de espécies por órgão e o manual do sistema;
- POST /api/v1/precedentes {"filtro": {...}} com as chaves que o front-end sempre envia: buscaGeral,
  todasPalavras, quaisquerPalavras, semPalavras, trechoExato, atualizacaoDesde/atualizacaoAte (DD/MM/AAAA,
  data da última atualização), cancelados, ordenacao (Text | Crono-Asc | Crono-Desc | Nume-Asc | Nume-Desc),
  nr, pagina (1-based), tamanhoPagina (10, 20, 50 ou 100), orgaos[], tipos[] (espécies válidas para os órgãos);
- um corpo incompleto (só buscaGeral vazio, orgaos e tipos) devolveu HTTP 500;
- resposta: {total, posicao_inicial, posicao_final, resultados[], aggsEspecies[], aggsOrgaos[]}; cada resultado:
  id ("stj-rr-65"), orgao, tipo, nr, situacao, questao, tese (HTML), historico[], suspensoes[],
  processosParadigma[{classe, numero (CNJ), link}], ultimaAtualizacao (DD/MM/AAAA), highlight (não armazenado);
- link oficial: /pesquisa?orgao=<órgão>&tipo=<espécie>&nr=<número> (rota que o front-end lê).
Período = data da última atualização do precedente no BNP.
```

## Uso responsável

- Faça no máximo 1 requisição por segundo (ou menos, se a nota acima pedir).
- Guarde o resultado em vez de consultar de novo a mesma coisa.
- Não tente contornar CAPTCHA, login ou bloqueio: se aparecer, pare.
- Decisões trazem nomes de pessoas: respeite a LGPD ao guardar e publicar.

[⬅ Voltar para a lista](../README.md)
