# Test Execution

Preencha a coluna **Resultado** com `PASS`, `FAIL` ou `BLOCKED`.
Use a coluna **Observação** para registrar evidência ou contexto quando `FAIL`.

> Limpe o `localStorage` entre seções quando necessário para isolar os cenários.

---

## Home (`/`)

| ID | Caso | Resultado | Observação |
|----|------|-----------|------------|
| TC-HOME-01 | A home carrega sem erros visíveis e sem erros no console |PASS| |
| TC-HOME-02 | O header fica fixo no topo ao rolar a página |PASS| Identificado erro grave de responsividade onde os links do menu somem sem menu alternativo no mobile (registrado no bugs.yaml).| navigation
| TC-HOME-03 | Logo do header não ultrapassa 80px de altura em qualquer breakpoint |PASS|Validado em diferentes resoluções, durante o scroll e com zoom. Altura mantida corretamente.|
| TC-HOME-04 | Clicar na logo navega para `/` |PASS| |

## Coleções e filtros (`/collections`)

| ID | Caso | Resultado | Observação |
|----|------|-----------|------------|
| TC-COL-01 | A listagem mostra produtos em grid de 3 colunas no desktop |PASS|Exibe 3 colunas em resolução normal de desktop. O comportamento responsivo (1 ou 2 colunas em telas menores/zoom) funciona conforme o esperado para boa usabilidade.|
| TC-COL-02 | Dropdown "Section" mostra as 3 seções com contagem por seção |PASS|O dropdown exibe as opções 'Essentials' (4), 'New Arrivals' (6) e 'Trending' (4) corretamente em desktop e mobile. |
| TC-COL-03 | Dropdown "Category" mostra as categorias existentes com contagem|PASS|Apresentado corretamente em mobile e desktop.|
| TC-COL-04 | Selecionar uma Section filtra a listagem corretamente |PASS|Apresentado corretamente em mobile e desktop os produtos pertencentes ao filtro|
| TC-COL-05 | Selecionar uma Category filtra a listagem corretamente |PASS|Apresentado corretamente em mobile e desktop os produtos pertencentes ao filtro |
| TC-COL-06 | Combinar Section + Category aplica os dois filtros simultaneamente |PASS|Apresentado corretamente em mobile e desktop os produtos pertencentes a ambos os filtros |
| TC-COL-07 | "Clear All" remove todos os filtros e volta para a listagem completa |PASS|Idependente da seleção de 1 ou mais filtros, realiza a limpeza corretamente |
| TC-COL-08 | Clicar fora de um dropdown aberto fecha o dropdown |FAIL|O menu do dropdown permanece aberto mesmo após clicar em áreas vazias da tela ou em outros elementos.|
| TC-COL-09 | Pressionar `Esc` com um dropdown aberto fecha o dropdown |PASS|O menu fecha corretamente usando a tecla Esc do teclado.|
| TC-COL-10 | URL reflete os filtros (`?section=...&category=...`) e link compartilhável aplica o filtro |FAIL|O link só funciona se digitado manualmente. Ao usar os dropdowns na interface, a URL não é atualizada com os parâmetros correspondentes.|

## Paginação (`/collections`)

| ID | Caso | Resultado | Observação |
|----|------|-----------|------------|
| TC-PAG-01 | A paginação aparece quando há mais de 6 produtos no resultado |PASS|O limite de 6 produtos por página é respeitado e a paginação é exibida quando o resultado possui mais de 6 itens (ex: categoria Tops com 8 itens). |
| TC-PAG-02 | "Previous" fica desabilitado na primeira página |PASS|O botão exibe estado desabilitado corretamente na primeira página de qualquer listagem. |
| TC-PAG-03 | "Next" fica desabilitado na última página |PASS|O botão "Next" exibe o estado desabilitado (inativo) corretamente ao atingir a última página de resultados.|
| TC-PAG-04 | Avançar para a página 2 preserva o filtro de Category ativo na URL |FAIL|Ao estar na página 1 com o filtro "Tops" (8 itens), clicar na página 2 remove o filtro e exibe a listagem total de produtos (14 itens). 
 GET /collections?category=tops 200 in 28ms
 GET /collections?page=2 200 in 32ms
 GET /collections?page=3 200 in 29ms|
| TC-PAG-05 | Avançar para a página 2 preserva o filtro de Section ativo na URL |BLOCKED|Impossível testar. O banco de dados atual não possui nenhuma "Section" com mais de 6 itens para acionar o componente de paginação e permitir o avanço para a página 2.|

## Busca (header)

| ID | Caso | Resultado | Observação |
|----|------|-----------|------------|
| TC-SRC-01 | O ícone da lupa abre o campo de busca |PASS✅|A barra de pesquisa é exibida corretamente ao clicar no ícone da lupa, sobrepondo o header conforme esperado.|
| TC-SRC-02 | Pressionar Enter com um termo válido navega para `/collections?q=...` |PASS|A navegação ocorre corretamente e a URL é atualizada com o parâmetro de busca (ex: ?q=as).|
| TC-SRC-03 | A busca por "coat" retorna o Sculpted Wool Coat |PASS|Produto retornado corretamente com o termo em letras minúsculas.|
| TC-SRC-04 | A busca por "Coat" (com maiúscula) retorna o mesmo resultado de "coat" |FAIL|A busca é case-sensitive. Termos com letras maiúsculas não encontram produtos que estão cadastrados com minúsculas (retorna 0 itens).|
| TC-SRC-05 | A busca sem resultados mostra mensagem amigável |PASS|A interface exibe corretamente uma mensagem amigável (ex: "No items match... Try a different keyword.") quando não há resultados.|

## Carrinho (PDP + drawer)

| ID | Caso | Resultado | Observação |
|----|------|-----------|------------|
| TC-CART-01 | Clicar "Add to bag" no PDP incrementa o badge no header e abre o drawer |PASS|O carrinho lateral abre automaticamente e o badge superior é atualizado para 1.|
| TC-CART-02 | Adicionar o mesmo produto duas vezes soma na quantidade, não duplica linha |PASS|O carrinho agrupa itens iguais, incrementando a quantidade e calculando o subtotal corretamente.|
| TC-CART-03 | Botão "−" no drawer não permite quantidade abaixo de 1 (clicar em qty=1 remove o item) |FAIL|O botão permite reduzir a quantidade até 0, e o item não é removido do carrinho como deveria.|
| TC-CART-04 | Botão "+" no drawer aumenta a quantidade do item |PASS|O botão "+" funciona perfeitamente, atualizando quantidade e valores.|
| TC-CART-05 | Remover um item via "×" atualiza o badge do header |PASS|O item é removido da lista e o contador no badge do header reflete a exclusão instantaneamente.|
| TC-CART-06 | "Clear bag" esvazia o drawer |PASS|o botão segue o comportamento esperado de remoção dos itens do carrinho |
| TC-CART-07 | Pressionar `Esc` com o drawer aberto fecha o drawer |FAIL|O painel lateral do carrinho não responde à tecla Esc do teclado, permanecendo aberto na tela.|
| TC-CART-08 | Fechar e abrir o navegador mantém os itens do carrinho (localStorage) |PASS|Os produtos e quantidades são preservados com sucesso no carrinho após recarregar a página ou reabrir o navegador.|
| TC-CART-09 | Subtotal exibido no drawer corresponde à soma de (preço × quantidade) dos itens |PASS|O cálculo matemático do subtotal está correto e reflete fielmente a soma de todos os itens e suas respectivas quantidades.|

## Newsletter (`/` footer)

| ID | Caso | Resultado | Observação |
|----|------|-----------|------------|
| TC-NEWS-01 | E-mail válido (`teste@exemplo.com`) mostra mensagem de sucesso e limpa o input |PASS|O cadastro é realizado com sucesso, exibe o feedback visual correto e o campo de input é redefinido.|
| TC-NEWS-02 | E-mail sem domínio TLD (`teste@exemplo`) é rejeitado com mensagem de erro |FAIL|O formulário aceitou o e-mail incompleto e exibiu a mensagem de sucesso em vez de barrar a inscrição.|
| TC-NEWS-03 | E-mail sem `@` (`teste.com`) é rejeitado com mensagem de erro |PASS|O sistema validou corretamente e impediu a inscrição, exibindo o erro esperado.|
| TC-NEWS-04 | E-mail com espaços (`a @b.com`) é rejeitado com mensagem de erro |PASS|O sistema identificou o espaço e impediu a inscrição corretamente.|
| TC-NEWS-05 | Submeter o mesmo e-mail duas vezes mostra mensagem de "já cadastrado" |FAIL|O sistema aceita inscrições duplicadas infinitamente, retornando sucesso sempre.|
| TC-NEWS-06 | E-mail com MAIÚSCULAS é normalizado para minúsculas em `/subscribers` |PASS|O sistema normaliza corretamente o endereço de e-mail, convertendo todos os caracteres para letras minúsculas ao salvar na base de inscritos.|

## `/subscribers`

| ID | Caso | Resultado | Observação |
|----|------|-----------|------------|
| TC-SUB-01 | E-mail recém-cadastrado aparece em `/subscribers` com data/hora |PASS|Os e-mails são listados corretamente, exibindo a data e hora exatas do cadastro.|
| TC-SUB-02 | Mesmo e-mail submetido 2x aparece apenas 1 vez na lista |FAIL|A aplicação exibe as duplicatas na tabela em vez de agrupá-las ou bloqueá-las, o que causa um erro de "same key" no console do React.|
| TC-SUB-03 | Botão "×" individual remove apenas aquele e-mail |PASS|A remoção funciona de forma independente, excluindo apenas a linha clicada sem afetar duplicatas.|
| TC-SUB-04 | "Clear all" exibe confirmação e, ao confirmar, esvazia a lista |PASS|O modal nativo de confirmação é exibido. A limpeza da lista só ocorre ao clicar em "OK", e é cancelada corretamente no "Cancelar". |
| TC-SUB-05 | Reload da página mantém os e-mails cadastrados (localStorage) |PASS|Os e-mails listados permanecem salvos e são renderizados perfeitamente após o F5 ou ao retornar à página, comprovando o uso correto do localStorage.|

---

**Total: 40 casos**
