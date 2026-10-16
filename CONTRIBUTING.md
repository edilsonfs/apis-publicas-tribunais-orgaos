# Como contribuir

Obrigado por ajudar a manter esta lista atualizada.

## O que aceitamos

- **API nova** de tribunal ou órgão público brasileiro.
- **Correção** de endereço, parâmetro, limite ou link.
- **Aviso** de que uma API mudou ou parou de funcionar.

## Regras

1. **Domínio oficial.** O endereço precisa ser do próprio órgão (`.jus.br`, `.gov.br`, `.leg.br`, `.mp.br`, `tc.br`...). Agregadores e espelhos privados não entram.
2. **Testado por você.** Informe a data do teste e um exemplo de chamada que funcionou.
3. **Sem contornar proteção.** Se a fonte exige CAPTCHA, login ou desafio que só humano resolve, ela vai para a lista de “Fontes sem API”, não para as tabelas.
4. **Diga o tipo de acesso:** 📘 documentada, 📦 arquivo de dados abertos, 🔧 JSON do site oficial ou 🛡️ precisa de navegador.
5. **Sem dados pessoais** nos exemplos (CPF, nomes de partes, e-mails).

## Como enviar

1. Faça um fork e crie um branch.
2. Para API nova: crie `apis/<id>.md` seguindo o modelo das fichas existentes e acrescente uma linha na tabela da seção certa do `README.md`.
3. Abra o pull request explicando o que testou.

Não sabe mexer com Git? Tudo bem: [abra uma issue](../../issues/new/choose) com as informações e alguém transforma em ficha.
