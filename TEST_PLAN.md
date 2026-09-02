# Test Plan

> Estratégia de Qualidade para o E-commerce "The Silent Narrative" (Cadastra)

## Escopo

**O que está incluído (In-Scope):**
* **Navegação e Estrutura:** Header responsivo, links de categoria, barra de busca e Footer.
* **Página Inicial (Home):** Layout, responsividade do Hero Banner e call-to-actions.
* **Listagem de Produtos (Collections):** Aplicação de filtros combinados, comportamento de estado (fechamento de dropdowns) e paginação.
* **Carrinho de Compras (Cart):** Adição/remoção de itens, cálculo de subtotal, controle de quantidade, persistência via `localStorage` e usabilidade/acessibilidade (Cart Drawer).
* **Newsletter & Área de Inscritos (/subscribers):** Validação de formulário (front-end), regras de negócio sobre duplicidade, sanitização de dados e persistência.

**O que está fora de escopo (Out-of-Scope):**
* **Integração de Pagamento (Checkout):** Gateways de pagamento externos (ex: Stripe, PayPal).
* **Testes de Carga/Performance:** Stresstest de servidor ou tempos de carregamento (LCP, FCP).
* **Testes Automatizados (E2E/Unitários):** Apenas testes manuais/exploratórios foram aplicados.
* **Cross-browser Exaustivo:** Testes focados no comportamento padrão em navegadores modernos (Chromium), sem abranger legado.
* **Banco de Dados/Backend Real:** Assumiu-se o uso de `localStorage` como mock temporário de persistência para o escopo do desafio.

---

## Riscos & priorização

A estratégia de testes foi guiada pelo **risco ao negócio (impacto na conversão e receita)**:

1.  **Navegação Mobile (Risco Crítico):** Prioridade Máxima. Um erro aqui bloqueia todo o fluxo de compras de mais de 50% dos usuários (encontrado o BUG-03 que esconde o menu).
2.  **Carrinho de Compras (Risco Alto):** A lógica matemática, limites numéricos (não permitir quantidades <= 0) e a persistência do carrinho garantem a venda. Falhas aqui causam perdas financeiras diretas.
3.  **Busca e Filtros (Risco Médio/Alto):** Diretamente ligados à descoberta do produto. Se a paginação quebra os filtros ou a busca difere maiúsculas, o usuário não encontra o que quer e abandona a loja.
4.  **Newsletter (Risco Médio):** Essencial para marketing. Regras de negócio falhas aqui geram bases de dados "sujas" (duplicatas e e-mails falsos).
5.  **UX e Polimento Visual (Risco Baixo):** Imagens quebradas ou falhas de *click-outside* incomodam, mas raramente impedem a compra.

---

## Tipos de teste aplicados

* **Teste Funcional:** Validação de fluxos centrais (adicionar ao carrinho, navegar, buscar produtos).
* **Teste de Usabilidade (UX / UI):** Comportamento de interface, responsividade de imagens (Hero) e interações (fechamento de modais).
* **Teste de Validação (Front-end & Regras de Negócio):** Expressões regulares (Regex) de e-mail, *case sensitivity* em buscas.
* **Teste de Acessibilidade:** Uso de navegação por teclado (tecla Esc no drawer) e armadilhas de foco (DOM/ARIA).
* **Teste de Persistência de Dados:** Avaliação do estado da aplicação através de Reloads e reabertura de abas (LocalStorage).
* **Teste Exploratório:** Busca intencional por comportamentos não mapeados, vasculhando o Console do navegador em busca de Dívidas Técnicas e erros de renderização (React keys).

---

## Técnicas formais utilizadas

* **Análise de Valor Limite:** Aplicada no contador do carrinho de compras para testar limites de quantidade (transição de 1 para 0) validando se o item é excluído ou se permite valores ilógicos.
* **Particionamento de Equivalência:** Aplicado no campo da Newsletter dividindo os inputs em partições válidas (`teste@exemplo.com`) e inválidas (`teste@exemplo`, `teste.com`, `a @b.com`) para validar o comportamento da Regex.
* **Transição de Estado:** Utilizada na paginação (Página 1 -> Página 2 -> Página 1) para verificar se o estado global dos filtros se mantinha durante as transições de rota.
* **Error Guessing:** Técnica empírica aplicada para encontrar o bug de *case sensitivity* na busca (testando "Coat" vs "coat") e na submissão de duplicatas na Newsletter.

---

## Cobertura por feature

| Feature | Tipos de Teste Aplicados | Status/Qualidade Atual |
| :--- | :--- | :--- |
| **Navegação (Header/Footer)** | Funcional, UX, Responsivo | Comprometido no Mobile (Bug crítico no menu). |
| **Página Inicial (Home)** | UX, Funcional, Error Guessing | Estável, com pequenos bugs de polimento. |
| **Busca e Filtros** | Funcional, State Transition | Bugs de estado na paginação e case-sensitivity. |
| **Carrinho de Compras** | Funcional, Persistência, A11y, Valor Limite | Persistência boa, mas com falhas matemáticas e A11y. |
| **Newsletter e /subscribers** | Validação, Lógica, Particionamento de Equivalência | Crítico para integridade de dados (validação fraca e duplicatas). |

---

## Limitações & premissas

* **Premissa:** Assumiu-se que o uso do `localStorage` para manter a Newsletter e o Carrinho é o comportamento intencional e aceitável para o escopo deste teste, agindo como substituto de um banco de dados real.
* **Premissa:** Assumiu-se que o limite máximo de estoque por produto não estava implementado nesta etapa; portanto, só validei o limite mínimo inferior (zero).
* **Limitação (Dispositivos):** A responsividade foi testada através da emulação de viewport no Google Chrome DevTools. Não foram realizados testes em dispositivos físicos (iOS/Android reais).
* **Limitação (Integração):** O botão "Checkout" não pôde ser testado fim-a-fim, pois não havia integração de gateway configurada para o desafio.

---

## Perguntas em aberto

* **Regra de Negócio (Newsletter):** Ao cadastrar um e-mail já existente, o sistema deveria apenas atualizar a data da última submissão de forma silenciosa ou deveria exibir um erro explícito de "E-mail já cadastrado" para o usuário?
* **Fluxo de UX (Home):** Qual é o comportamento esperado para o botão "Explore Film" no Hero Banner? Ele deveria abrir um modal de vídeo nativo ou navegar para uma página externa?
* **Gestão de Estoque:** O que deve acontecer com os itens persistidos no `localStorage` do carrinho se um deles ficar sem estoque ou sofrer alteração de preço enquanto o usuário estiver fora da loja?
