# Test Execution

Preencha a coluna **Resultado** com `PASS`, `FAIL` ou `BLOCKED`.
Use a coluna **Observação** para registrar evidência ou contexto quando `FAIL`.

> Limpe o `localStorage` entre seções quando necessário para isolar os cenários.

---

## Home (`/`)

| ID | Caso | Resultado | Observação |
|----|------|-----------|------------|
| TC-HOME-01 | A home carrega sem erros e sem erros no console | PASS |  |
| TC-HOME-02 | O header fica fixo no topo ao rolar a página | PASS ||
| TC-HOME-03 | Clicar na logo navega para `/` | PASS | Logo wraps Image in `<Link href="/">` |
| TC-HOME-04 | Menus alinhamento visual | FAIL | Pelo contexto: "Accessories" no desktop/web está alinhado no bloco de busca/minicart, seria alinhamento à Coleções/Menus |
| TC-HOME-05 | Menu hamburguer - mobile | FAIL | Mudar as categoria/menus como se fossem "filtros/ordenar por" sem ter um menu mobile hamburguer comum nas lojas, pode difucultar UIxUX |



## PLP / Coleções e filtros (`/collections`)

| ID | Caso | Resultado | Observação |
|----|------|-----------|------------|
| TC-COL-01 | A listagem mostra produtos em grid  | PASS ||
| TC-COL-02 | Dropdown "Section" mostra as 3 seções com contagem por seção | PASS | |
| TC-COL-03 | Dropdown "Category" mostra as categorias existentes com contagem | PASS | |
| TC-COL-04 | Selecionar uma Section filtra a listagem corretamente | PASS |  |
| TC-COL-05 | Selecionar uma Category filtra a listagem corretamente | PASS ||
| TC-COL-06 | Combinar Section + Category aplica os dois filtros simultaneamente | FAIL | a combinação com indicativo de quantidade, fica sem produtos, mesmo indicando ex. "1" |
| TC-COL-07 | "Clear All" remove todos os filtros e volta para a listagem completa | PASS | |
| TC-COL-08 | Clicar fora de um dropdown aberto fecha o dropdown | FAIL | ideal fechar |
| TC-COL-09 | Pressionar `Esc` com um dropdown aberto fecha o dropdown | PASS |  |
| TC-COL-10 | URL reflete os filtros (`?section=...&category=...`) e link aplica o filtro | PASS |  |


## Paginação (`/collections`)

| ID | Caso | Resultado | Observação |
|----|------|-----------|------------|
| TC-PAG-01 | A paginação aparece quando há mais de 6 produtos no resultado | PASS |  |
| TC-PAG-02 | "Previous" fica desabilitado na primeira página | PASS |  |
| TC-PAG-03 | "Next" fica desabilitado na última página | PASS | |
| TC-PAG-04 | Avançar para a página 2 preserva o filtro de Category ativo na URL | FAIL |  na category=tops, diz 8 mas na paginação surge a "3ª" + repete na "2ª" e adiciona mais 2 produtos |
| TC-PAG-05 | Avançar para a página 2 preserva o filtro de Section ativo na URL | PASS | |


## Busca (header)

| ID | Caso | Resultado | Observação |
|----|------|-----------|------------|
| TC-SRC-01 | O ícone abre o cmapo | PASS | |
| TC-SRC-02 | Pressionar Enter com um termo válido navega para pesquisa | PASS |  |
| TC-SRC-03 | A busca por "coat" retorna o Sculpted Wool Coat | PASS |  |
| TC-SRC-04 | A busca por "Coat" (com maiúscula) retorna o mesmo resultado de "coat" | FAIL | No items match “COAT”. Try a different keyword. |
| TC-SRC-05 | A busca sem resultados mostra mensagem amigável | PASS |  |



## PDP / Carrinho (PDP + drawer)

| ID | Caso | Resultado | Observação |
|----|------|-----------|------------|
| TC-CART-01 | Clicar "Add to bag" no PDP incrementa o badge no header e abre o drawer | PASS | |
| TC-CART-02 | Adicionar o mesmo produto duas vezes soma na quantidade, não duplica linha | PASS | |
| TC-CART-03 | Botão "−" permite quantidade abaixo de "1 " | FAIL | mesmo que seja "0" evita problemas de estoque| 
| TC-CART-04 | Botão "+" no drawer aumenta a quantidade do item | PASS |  |
| TC-CART-05 | Remover um item via "×" atualiza | PASS | |
| TC-CART-06 | Fechar e abrir o navegador mantém os itens do carrinho (localStorage) | PASS |  |
| TC-CART-07 | Subtotal exibido no drawer corresponde à soma de (preço × quantidade) dos itens | |
| TC-CART-08 | label/campo qtde | FAIL | me parece que existe em: "font-body text-label-caps min-w-[1.5rem] text-center", mas os seletores - e + sobrepõe|
| TC-CART-09 | Resere in store - mobile | FAIL |  diferente do desktop, mesmo que não funcione muda a cor no mouse click/press |


## Newsletter (`/` footer)

| ID | Caso | Resultado | Observação |
|----|------|-----------|------------|
| TC-NEWS-01 | E-mail válido (`qa@teste.com`) mensagem de sucesso e limpa o input | PASS | |
| TC-NEWS-02 | E-mail sem domínio  (`qa@test`) é rejeitado com mensagem de erro | FAIL |  |
| TC-NEWS-01 | E-mail sem `@` (`teste.com`) é rejeitado com mensagem de erro | PASS | |
| TC-NEWS-04 | E-mail com espaços (`a @b.com`) é rejeitado com mensagem de erro | PASS | |
| TC-NEWS-05 | Submeter o mesmo e-mail duas vezes mostra mensagem de "já cadastrado" | FAIL | permite o mesmo email|
| TC-NEWS-06 | E-mail com MAIÚSCULAS é entende como minúsculas em `/subscribers` | PASS | |



## `/subscribers` (Back)

| ID | Caso | Resultado | Observação |
|----|------|-----------|------------|
| TC-SUB-01 | E-mail recém-cadastrado aparece em `/subscribers` com data/hora | PASS |  |
| TC-SUB-02 | Mesmo e-mail submetido 2x aparece apenas 1 vez na lista | FAIL |permite mesmo email gerando duplicaidade |
| TC-SUB-03 | Botão "×" individual remove apenas aquele e-mail | PASS | |
| TC-SUB-04 | "Clear all" exibe confirmação e, ao confirmar, esvazia a lista | PASS |  |
| TC-SUB-05 | Reload da página mantém os e-mails cadastrados (localStorage) | PASS |  |

---

**Total: 45 casos**

