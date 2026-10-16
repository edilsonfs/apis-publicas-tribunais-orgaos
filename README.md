<div align="center">

# 🇧🇷 APIs Públicas de Tribunais e Órgãos Públicos

**Um mapa das portas abertas da Justiça e do governo brasileiro na internet.**<br>
Onde pedir leis, decisões e processos por API — testado de verdade, explicado de forma simples.

[![APIs verificadas](https://img.shields.io/badge/APIs%20verificadas-39-2ea44f)](#índice)
[![Verificado em](https://img.shields.io/badge/verificado%20em-out%2F2026-blue)](#como-sabemos-que-funciona)
[![Licença MIT](https://img.shields.io/badge/licen%C3%A7a-MIT-yellow)](LICENSE)
[![PRs bem-vindos](https://img.shields.io/badge/PRs-bem--vindos-brightgreen)](CONTRIBUTING.md)

</div>

---

## 🧒 Explicando como se fosse para uma criança

Imagine que cada tribunal e cada órgão do governo é uma **biblioteca gigante** cheia de leis e decisões.

Algumas bibliotecas têm uma **janelinha** onde um computador pode pedir um papel e receber a resposta na hora, sem ninguém precisar abrir a porta. Essa janelinha se chama **API**.

O problema: ninguém conta onde ficam as janelinhas, nem como falar com elas. Cada biblioteca fala de um jeito diferente.

**Este repositório é o mapa.** Ele mostra onde fica cada janelinha, o que dá para pedir, como pedir e quais regras de educação seguir para não incomodar a biblioteca.

## 🎯 Para que serve

- **Quem programa** encontra a API certa sem passar dias investigando o site de cada tribunal.
- **Quem pesquisa** (Direito, jornalismo de dados, ciência política) sabe de onde vêm os dados e o que cada fonte cobre.
- **Quem fiscaliza** acha as fontes oficiais, sem depender de sites intermediários pagos.

Tudo aqui aponta para **domínios oficiais** (`.jus.br`, `.gov.br`, `.leg.br`, `tc.br`). Nada de espelhos ou agregadores privados.

## Índice

- [Como ler as tabelas](#como-ler-as-tabelas)
- [Supremo, Tribunais Superiores e CNJ](#supremo-tribunais-superiores-e-cnj)
- [Justiça do Trabalho](#justiça-do-trabalho)
- [Justiça Federal](#justiça-federal)
- [Justiça Estadual (Tribunais de Justiça)](#justiça-estadual-tribunais-de-justiça)
- [Tribunais de Contas](#tribunais-de-contas)
- [Legislação federal](#legislação-federal)
- [Legislação estadual e municipal](#legislação-estadual-e-municipal)
- [Receita, Banco Central e órgãos administrativos](#receita-banco-central-e-órgãos-administrativos)
- [Exemplos rápidos (copiar e colar)](#exemplos-rápidos-copiar-e-colar)
- [Uso responsável](#uso-responsável)
- [Fontes sem API (e por quê)](#fontes-sem-api-e-por-quê)
- [Como sabemos que funciona](#como-sabemos-que-funciona)
- [Como contribuir](#como-contribuir)

## Como ler as tabelas

| Símbolo | Significa |
|---|---|
| 📘 **Oficial documentada** | O órgão publicou documentação da API. É a opção mais estável. |
| 📦 **Arquivo de dados abertos** | O órgão publica arquivos (ZIP, JSON, CSV) para baixar. Ótimo para ter tudo no seu computador. |
| 🔧 **JSON do site oficial** | É a API que o próprio site de pesquisa do órgão usa. Funciona, mas **não tem contrato público**: pode mudar sem aviso. |
| 🛡️ **Precisa de navegador** | O site pede um teste anti-robô automático (não é CAPTCHA). É preciso abrir um navegador uma vez para receber um cookie. |
| ⚠️ | Tem uma pegadinha importante. Leia a ficha antes de usar. |

Cada linha tem uma **ficha** com endereço, parâmetros, limites e observações verificadas.

## Supremo, Tribunais Superiores e CNJ

| API | O que você encontra | Acesso | Autenticação | Detalhes |
|---|---|---|---|---|
| [STF](https://jurisprudencia.stf.jus.br/pages/search) | Acórdãos e decisões do STF com ementa ⚠️ | 🛡️ Precisa de navegador | Cookie de desafio (navegador) | [ficha](apis/stf.md) |
| [STJ](https://dadosabertos.web.stj.jus.br/dataset/integras-de-decisoes-terminativas-e-acordaos-do-diario-da-justica) | Texto completo das decisões do STJ (desde 2021) | 📦 Arquivo de dados abertos | Nenhuma | [ficha](apis/stj_integras.md) |
| [STJ](https://dadosabertos.web.stj.jus.br/dataset/?q=espelhos-de-acordaos) | Espelhos de acórdãos do STJ (ementa, tese, legislação citada) | 📦 Arquivo de dados abertos | Nenhuma | [ficha](apis/stj_espelhos.md) |
| [STJ](https://dadosabertos.web.stj.jus.br/dataset/precedentes-qualificados) | Temas repetitivos e precedentes do STJ | 📦 Arquivo de dados abertos | Nenhuma | [ficha](apis/stj_precedentes.md) |
| [CNJ](https://comunica.pje.jus.br/) | Tudo o que os tribunais publicam no Diário de Justiça Nacional | 📘 Oficial documentada | Nenhuma | [ficha](apis/djen.md) |
| [CNJ](https://datajud-wiki.cnj.jus.br/api-publica/) | Dados dos processos de todos os tribunais (sem o texto) ⚠️ | 📘 Oficial documentada | Chave pública do CNJ | [ficha](apis/datajud.md) |
| [CNJ](https://pangeabnp.pdpj.jus.br/) | Precedentes qualificados de todo o país (teses e temas) | 🔧 JSON do site oficial | Nenhuma | [ficha](apis/pangea_bnp.md) |

**[⬆ Voltar ao índice](#índice)**

## Justiça do Trabalho

| API | O que você encontra | Acesso | Autenticação | Detalhes |
|---|---|---|---|---|
| [JT](https://jurisprudencia.jt.jus.br/jurisprudencia-nacional/) | Acórdãos do TST e dos 24 TRTs ⚠️ | 🔧 JSON do site oficial | sessionId livre + navegador | [ficha](apis/falcao.md) |

**[⬆ Voltar ao índice](#índice)**

## Justiça Federal

| API | O que você encontra | Acesso | Autenticação | Detalhes |
|---|---|---|---|---|
| [TRF5](https://juliapesquisa.trf5.jus.br/julia-pesquisa/) | Jurisprudência do TRF da 5ª Região e turmas recursais | 🔧 JSON do site oficial | Nenhuma | [ficha](apis/trf5.md) |

**[⬆ Voltar ao índice](#índice)**

## Justiça Estadual (Tribunais de Justiça)

| API | O que você encontra | Acesso | Autenticação | Detalhes |
|---|---|---|---|---|
| [TJBA](https://jurisprudencia.tjba.jus.br/) | Jurisprudência do TJBA | 🔧 JSON do site oficial | Nenhuma | [ficha](apis/tjba.md) |
| [TJCE](https://sjuris.tjce.jus.br/tela-consulta) | Jurisprudência do TJCE (SJURIS) | 🔧 JSON do site oficial | Nenhuma | [ficha](apis/tjce.md) |
| [TJDFT](https://jurisdf.tjdft.jus.br/) | Jurisprudência do TJDFT | 📘 Oficial documentada | Nenhuma | [ficha](apis/tjdft.md) |
| [TJES](https://sistemas.tjes.jus.br/consulta-jurisprudencia/) | Jurisprudência do TJES, inclusive 1º grau | 🔧 JSON do site oficial | Nenhuma | [ficha](apis/tjes.md) |
| [TJMG](https://jurisprudencia-api.tjmg.jus.br/v3/api-docs) | Jurisprudência do TJMG | 📘 Oficial documentada | Nenhuma | [ficha](apis/tjmg.md) |
| [TJMT](https://jurisprudencia.tjmt.jus.br/consulta/judicial) | Jurisprudência do TJMT ⚠️ | 🔧 JSON do site oficial | Token público do site | [ficha](apis/tjmt.md) |
| [TJPA](https://jurisprudencia.tjpa.jus.br/) | Jurisprudência do TJPA | 🔧 JSON do site oficial | Nenhuma | [ficha](apis/tjpa.md) |
| [TJPB](https://pje-jurisprudencia.tjpb.jus.br/) | Ementas do TJPB (base de 2015–2018) ⚠️ | 🔧 JSON do site oficial | Nenhuma | [ficha](apis/tjpb.md) |
| [TJPE](https://consultajurisprudencia.app.tjpe.jus.br/) | Acórdãos e decisões do TJPE com inteiro teor | 🔧 JSON do site oficial | Nenhuma | [ficha](apis/tjpe.md) |
| [TJRO](https://juris.tjro.jus.br/) | Jurisprudência do TJRO, inclusive sentenças ⚠️ | 🔧 JSON do site oficial | Nenhuma | [ficha](apis/tjro.md) |
| [TJRS](https://www.tjrs.jus.br/buscas/jurisprudencia/?aba=jurisprudencia) | Jurisprudência do TJRS com íntegra | 🔧 JSON do site oficial | Nenhuma | [ficha](apis/tjrs.md) |

**[⬆ Voltar ao índice](#índice)**

## Tribunais de Contas

| API | O que você encontra | Acesso | Autenticação | Detalhes |
|---|---|---|---|---|
| [TCU](https://pesquisa.apps.tcu.gov.br/) | Acórdãos do TCU | 🔧 JSON do site oficial | Nenhuma | [ficha](apis/tcu.md) |
| [TCDF](https://busca.tc.df.gov.br/#/jurisprudencia/inteiro-teor) | Decisões do TCDF | 🔧 JSON do site oficial | Nenhuma | [ficha](apis/tcdf.md) |
| [TCE-BA](https://www.tce.ba.gov.br/jurisprudencia/consulta) | Decisões do TCE-BA | 🔧 JSON do site oficial | Nenhuma | [ficha](apis/tceba.md) |
| [TCE-CE](https://www.tce.ce.gov.br/contexto/) | Documentos do TCE-CE | 🔧 JSON do site oficial | Nenhuma | [ficha](apis/tcece.md) |
| [TCE-GO](https://decisoes.tce.go.gov.br) | Decisões do TCE-GO | 🔧 JSON do site oficial | Nenhuma | [ficha](apis/tcego.md) |
| [TCE-PE](https://portal.tcepe.tc.br/jurisprudencia/consulta/deliberacoes) | Deliberações do TCE-PE | 🔧 JSON do site oficial | Nenhuma | [ficha](apis/tcepe.md) |
| [TCE-RJ](https://www.tcerj.tc.br/consulta-processo/PesquisaTextual) | Processos e decisões do TCE-RJ | 🔧 JSON do site oficial | Nenhuma | [ficha](apis/tcerj.md) |
| [TCE-RS](https://portal.tce.rs.gov.br/app/pesquisa/jurisprudencia/) | Decisões do TCE-RS | 🔧 JSON do site oficial | Nenhuma | [ficha](apis/tcers.md) |
| [TCE-SC](https://virtual.tce.sc.gov.br/jurisprudencia/jurisprudencia) | Jurisprudência do TCE-SC | 🔧 JSON do site oficial | Nenhuma | [ficha](apis/tcesc.md) |

**[⬆ Voltar ao índice](#índice)**

## Legislação federal

| API | O que você encontra | Acesso | Autenticação | Detalhes |
|---|---|---|---|---|
| [Senado](https://legis.senado.leg.br/dadosabertos/legislacao/lista) | Todas as normas federais: dados, alterações e publicação | 📘 Oficial documentada | Nenhuma | [ficha](apis/senado.md) |
| [CN](https://normas.leg.br/) | Texto das leis federais (original e atualizado) ⚠️ | 🔧 JSON do site oficial | Nenhuma | [ficha](apis/normas_leg.md) |
| [IN](https://www.in.gov.br/acesso-a-informacao/dados-abertos/base-de-dados) | Atos publicados no Diário Oficial da União (arquivos mensais) | 📦 Arquivo de dados abertos | Nenhuma | [ficha](apis/dou.md) |
| [IN](https://inlabs.in.gov.br/) | Diário Oficial da União do dia (XML/PDF) | 📘 Oficial documentada | Cadastro gratuito | [ficha](apis/inlabs.md) |

**[⬆ Voltar ao índice](#índice)**

## Legislação estadual e municipal

| API | O que você encontra | Acesso | Autenticação | Detalhes |
|---|---|---|---|---|
| [ALMG](https://www.almg.gov.br/legislacao-mineira/) | Leis e normas de Minas Gerais | 📘 Oficial documentada | Nenhuma | [ficha](apis/almg.md) |
| [ALESP](https://www.al.sp.gov.br/dados-abertos/recurso/49) | Normas do Estado de São Paulo (metadados) | 📦 Arquivo de dados abertos | Nenhuma | [ficha](apis/alesp.md) |
| [SAPL](https://www.interlegis.leg.br/) | Leis de Assembleias e Câmaras que usam o SAPL | 📘 Oficial documentada | Nenhuma | [ficha](apis/sapl.md) |

**[⬆ Voltar ao índice](#índice)**

## Receita, Banco Central e órgãos administrativos

| API | O que você encontra | Acesso | Autenticação | Detalhes |
|---|---|---|---|---|
| [RFB](https://normasinternet2.receita.fazenda.gov.br/) | Instruções normativas, soluções de consulta e atos da Receita | 🔧 JSON do site oficial | Nenhuma | [ficha](apis/receita.md) |
| [BCB](https://www.bcb.gov.br/estabilidadefinanceira/buscanormas) | Resoluções, circulares e normas do Banco Central | 🔧 JSON do site oficial | Nenhuma | [ficha](apis/bcb.md) |
| [CARF](https://acordaos.economia.gov.br/) | Acórdãos do CARF (tributário) | 🔧 JSON do site oficial | Nenhuma | [ficha](apis/carf.md) |

**[⬆ Voltar ao índice](#índice)**

## Exemplos rápidos (copiar e colar)

Funcionam no terminal (`curl`). Troque as datas e os termos à vontade.

**Diário de Justiça Eletrônico Nacional (DJEN/CNJ)**: o que um tribunal publicou num dia.
```bash
curl "https://comunicaapi.pje.jus.br/api/v1/comunicacao?siglaTribunal=TJPE&dataDisponibilizacaoInicio=2026-10-08&dataDisponibilizacaoFim=2026-10-08&pagina=1&itensPorPagina=5"
```

**TJPE**: decisões publicadas num dia (o total vem no cabeçalho `x-total-count`).
```bash
curl -i "https://consultajurisprudencia.app.tjpe.jus.br/api/v1/jurisprudencias?tipoSentenca.in=A,D&dataPublicacao.greaterThanOrEqual=2026-10-06&dataPublicacao.lessThanOrEqual=2026-10-06&page=0&size=5"
```

**TJDFT**: busca por palavra (API documentada pelo tribunal).
```bash
curl -X POST "https://jurisdf.tjdft.jus.br/api/v1/pesquisa" -H "Content-Type: application/json" \
  -d '{"query": "dano moral", "pagina": 0, "tamanho": 5}'
```

**CARF**: acórdãos do contencioso tributário federal.
```bash
curl "https://acordaos.economia.gov.br/solr/acordaos2/browse?wt=json&q=imposto&rows=5"
```

**Senado**: dados de uma lei federal (publicação, alterações, link do texto).
```bash
curl -H "Accept: application/json" "https://legis.senado.leg.br/dadosabertos/legislacao/lei/8078/1990"
```

**STJ (dados abertos)**: lista dos arquivos com o texto integral das decisões.
```bash
curl "https://dadosabertos.web.stj.jus.br/api/3/action/package_show?id=integras-de-decisoes-terminativas-e-acordaos-do-diario-da-justica"
```

**DataJud (CNJ)**: dados de processos. A chave é pública e fica na [wiki do CNJ](https://datajud-wiki.cnj.jus.br/api-publica/acesso).
```bash
curl -X POST "https://api-publica.datajud.cnj.jus.br/api_publica_tjpe/_search" \
  -H "Authorization: APIKey $DATAJUD_CHAVE" -H "Content-Type: application/json" -d '{"size": 1}'
```

## Uso responsável

Essas janelinhas atendem o país inteiro. Seja gentil:

1. **Devagar:** no máximo 1 requisição por segundo. Algumas fontes bloqueiam por horas quem corre (veja os ⚠️).
2. **Guarde o que baixou:** não peça a mesma coisa duas vezes. Para muitos dados, prefira os 📦 arquivos.
3. **CAPTCHA, login ou bloqueio = pare.** Contornar proteção não é uso de API pública.
4. **Pessoas de verdade:** decisões trazem nomes. Respeite a LGPD (Lei 13.709/2018) ao guardar e publicar.
5. **Valor legal:** o texto que vale é o publicado no Diário Oficial. Cópias e compilações ajudam, mas não substituem.
6. **Termos de uso:** o DataJud, por exemplo, só permite uso não comercial. Leia a ficha.

## Fontes sem API (e por quê)

Algumas fontes importantes **não entram** porque exigem CAPTCHA, login ou desafio anti-robô que só um humano resolve:

| Fonte | Motivo | Alternativa |
|---|---|---|
| TSE e os 27 TREs | Busca exige hCaptcha | DJEN |
| TJSP | e-SAJ com reCAPTCHA | DJEN, DataJud |
| TJMA, TJSE, TJAP (acórdãos) | CAPTCHA validado no servidor | DJEN, DataJud |
| TJRN | Bloqueio do Akamai para acesso automatizado | DJEN, DataJud |
| STJ (SCON) | Desafio interativo do Cloudflare | STJ dados abertos, DJEN |
| TJSC, TCE-PA | Desafio F5 que exige navegador | DJEN, DataJud |
| TCE-ES, TCE-SP | Página de busca com reCAPTCHA | Diário Oficial do tribunal |
| LexML (busca) | Desafio de prova de trabalho e robots.txt proibindo | Senado, normas.leg.br |
| Planalto (busca) | Sem API; só páginas HTML | Senado, normas.leg.br |

Também ficaram de fora fontes que só existem como **formulário HTML** (eproc dos TRFs, e-SAJ, entre outras): funcionam por raspagem de página, não por API.

## Como sabemos que funciona

Cada API desta lista foi **chamada de verdade** em outubro de 2026, a partir do Brasil, com o resultado conferido (campos, paginação, limites). As fichas registram o que foi visto e quando.

APIs mudam. Se alguma parou de funcionar, [abra uma issue](../../issues/new?template=api-quebrada.md) — é a contribuição mais valiosa que existe aqui.

## Como contribuir

Achou uma API nova, uma pegadinha ou um link quebrado? Veja o [guia de contribuição](CONTRIBUTING.md). Regras de ouro:

- Só **domínios oficiais**.
- Só o que **você testou** (diga a data).
- Nada que exija contornar CAPTCHA ou login.

## Licença

[MIT](LICENSE). Use, copie e melhore. Os dados de cada API pertencem aos respectivos órgãos e seguem as regras deles.

<div align="center">

Feito para quem já perdeu horas procurando “onde fica a API do tribunal”. ⭐ Se ajudou, deixe uma estrela.

</div>
