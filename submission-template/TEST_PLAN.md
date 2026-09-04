# Plano de Testes

> Página única descrevendo sua estratégia para este desafio.
> Sugestão de seções abaixo — sinta-se à vontade para ajustar.

## Escopo

- Ambiente restrito: http://localhost:3000 "Loja Cadastra"
- Homepage (`/`): Home, seções de produtos, coleções em destaque, cadastro na newsletter, footer.
- PLP (`/collections`): grade de produtos, filtros, resultados de pesquisa, paginação.
- PDP & carrinho (`/products/`): imagem, descrições do produto, CTA "Adicionar à sacola", produtos relacionados(vitrine). Carrinho: contador, gaveta lateral deslizante, controles de quantidade, subtotal, esvaziar sacola.
- News: validação de entrada, mensagens de sucesso/duplicidade/erro. E funcionalidade da News: visualização em lista/análise, persistência(back).
- Não funcional (front): persistência dados (carrinho + produtos/valores), layout responsivo, acessibilidade/navegação.


## Riscos & priorização

| Área | Risco | Prioridade | Justificativa |
|------|-------|------------|---------------|
| Carrinho | Perda/divergências | **Alta** | Fluxo crítico de compra; bugs de quantidade podem gerar perda financeira |
| Newsletter/Subscribers | Duplicatas, e-mails inválidos sendo cadastrados | **Alta** | Impacta integridade de dados e futuros "CRM" de emails duplicados|
| Busca | Resultados com erros/sem resultados relevantes | Média | perda de receita/interesse na loja comportamento de pesquisa IA-Synerise, mas não bloqueia funcionalidade |
| Paginação | Perda de filtros ao navegar | Alta | Usuário perde contexto de filtragem ao navegar ou filtros ocultam produtos pois não foram cadastrados corretamente |
| Filtros | Dropdown não fechar ao clicar fora | Média | Comportamento comum de UX, mas Esc ainda funciona |
| Navegação | Links quebrados/fakes | Média | Dependendo da loja, seguir regulamentação do local e/ou legislação ex. LGPD-GDPR-ECA digital |


## Tipos de teste aplicados

1. **Funcional** — Verificação de fluxo positivo e navegação/compra.
2. **Validação de campo email/news** — Testes para email (sem @ / ."ponto", espaços, maiúsculas/minúsculas, duplicadas, limite de campo, script/html).
3. **Persistência** — Verificação de que carrinho e newsletters são adicionados.
4. **Acessibilidade (A11y)** — Verificação de atributos, teclado (Esc para fechar modais), tag's alternativos.
5. **Regressão** — Filtros combinados funcionam/mantém após mudanças na paginação.
6. **UX/UI** — Mensagens informativas em estados, labels corretas.
7. **Navegação** — Links de navegação, breadcrumb implícito via URL.


## Técnicas formais utilizadas

1. **Particionamento Equivalência** — Para validação de e-mail: partições válidas (formato correto), inválidas (sem @, com espaços) e duplicadas.
2. **Valor "Limite"** — carrinho: limite inferior (qty=1, clicar em "−" deve remover); paginação: página 1 e última página (Previous/Next OFF).
3. **Tabelas de Decisão** — Newsletter: combinação de {email válido/inválido} × {novo/duplicado} × {maiúsculas/minúsculas}.
4. **Estados de Transição** — Carrinho: entrada, mensagens de sucesso/duplicidade/erro, normalização de e-mail.
5. **Exploratório** — Navegação explorada core da loja, verificação imagens/produtos, teste de URLs externas.

## Cobertura por funcionalidade

| Funcionalidade | Funcional | Validação | Persistência | A11y | UX | Navegação |
|---------|-----------|-----------|--------------|------|-----|-----------|
| Home | ✓ |   |   | ✓ |   | ✓ |
| Coleções | ✓ |   |   |   |   | ✓ |
| Filtros | ✓ |   |   | ✓ | ✓ | ✓ |
| Paginação | ✓ |   |   | ✓ |   | ✓ |
| Busca | ✓ | ✓ |   | ✓ | ✓ | ✓ |
| PDP | ✓ |   |   | ✓ |   | ✓ |
| Carrinho | ✓ | ✓ | ✓ | ✓ | ✓ |   |
| Newsletter/News | ✓ | ✓ | ✓ | ✓ | ✓ |   |


## Limitações & premissas

- Somente testes front, limitado até carrinho.
- Testes manuais de interação (cliques, teclado, dropdown) foram validados.
- Responsividade (mobile/desktop) não foi testada em todos navegadores/resoluções.
- Imagens/links externos podem não estar disponíveis em ambiente real.
- Payment/checkout: geralmente mais crítico/importante num ecommerce.
- Performance test: local/homologação x produção.
- Visual: sem Figma/XD, para pixel-perfect.


## Perguntas em aberto

1. Mobile: acesso de menus/categorias/PLPs só na Home sem hamburguer pode prejudicar UIxUX?
2. A página "Ready to Wear" deveria mapear para uma Section (ex: "trending") ou para uma Category específica, ou simplesmente filtrado direto 'collections?category=dresses'?
3. O botão "Checkout(E2E)" no carrinho e/ou "Reserve in store" no PDP deveriam ter funcionalidade?
4. Os links do footer, deveriam navegar para conteúdo/link fake para teste? ou CS/KS preencheria num SiteEditor/Admin Vtex depois?

