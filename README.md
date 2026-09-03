# QA Challenge — Cadastra Editorial

Instruções para execução do teste de QA manual sobre a storefront editorial em Next.js.

## Preview no GitHub

Abra a aplicação direto no navegador via **GitHub Codespaces** (sem instalar nada localmente):

[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/viniciusdelfino/cadastra-qa-challenge?quickstart=1)

> Ao subir o Codespace, o `npm install` e `npm run dev` rodam automaticamente. Quando a porta `3000` ficar disponível, o VS Code abrirá o preview da aplicação. Use o botão **"Open in Browser"** para testar em uma aba dedicada.

---

## Sumário

- [Preview no GitHub](#preview-no-github)
- [Pré-requisitos](#pré-requisitos)
- [Como rodar a aplicação](#como-rodar-a-aplicação)
- [Escopo do teste](#escopo-do-teste)
- [O que entregar](#o-que-entregar)
- [Como preencher os entregáveis](#como-preencher-os-entregáveis)
- [Critérios de severidade](#critérios-de-severidade)
- [Regras](#regras)
- [Submissão](#submissão)

---

## Pré-requisitos

- Node.js **20.x** ou superior
- npm **10.x** ou superior
- Navegador atualizado (Chrome/Edge/Firefox)

---

## Como rodar a aplicação

```bash
git clone <repo>
cd cadastra-qa-challenge
git checkout qa-challenge
npm install
npm run dev   # http://localhost:3000
```

Alternativamente, use a URL de preview já deployada (link enviado por e-mail).

### Limpando estado entre cenários

Limpe o `localStorage` quando necessário:

> DevTools → Application → Local Storage → clique direito → **Clear**.

Chaves usadas pela aplicação:

- `cadastra-cart:v1`
- `cadastra-subscribers:v1`

---

## Escopo do teste

A aplicação contém **defeitos plantados**. Sua missão é encontrá-los executando QA manual nas seguintes rotas e fluxos:

| Rota | O que cobrir |
| --- | --- |
| `/` | Hero, coleções em destaque, newsletter |
| `/collections` | Listagem com filtros (Section, Category), busca via header, paginação |
| `/products/[slug]` | Detalhe do produto e "Add to bag" |
| Carrinho | Drawer lateral, badge no header, persistência local |
| Newsletter | Cadastro, validações, persistência |
| `/subscribers` | Visualização dos cadastros |

Recomenda-se cobrir **todas** as features listadas.

---

## O que entregar

Na raiz do seu fork, com um Pull Request de volta para `main`:

1. **`TEST_PLAN.md`** — sua estratégia em 1 página (obrigatório).
2. **`TEST_EXECUTION.md`** — checklist preenchido (obrigatório).
3. **`bugs.yaml`** — bugs descobertos (obrigatório).
4. **`tests/candidate/*.spec.ts`** — automação Playwright (opcional, bônus).

Templates prontos em [`submission-template/`](submission-template/). Copie a pasta e preencha:

```bash
cp -r submission-template/* .
```

---

## Como preencher os entregáveis

### `TEST_PLAN.md`

Sua estratégia em 1 página: cobertura, riscos, priorização, premissas e perguntas sobre o produto.

### `TEST_EXECUTION.md`

Checklist com IDs de casos de teste (`TC-HOME-*`, `TC-COL-*`, `TC-PAG-*`, `TC-SRC-*`, `TC-CART-*`, `TC-NEWS-*`, `TC-SUB-*`). Para cada caso, marque **PASS** ou **FAIL** com observação quando houver bug.

### `bugs.yaml`

Liste cada bug encontrado com:

- `id`, `title`, `severity` (High / Medium / Low)
- Passos de reprodução
- Resultado esperado vs. obtido

---

## Critérios de severidade

Use no `bugs.yaml`:

- **High** — bloqueia funcionalidade central, gera perda/duplicação de dados ou quebra fluxo crítico (carrinho, cadastro).
- **Medium** — degrada a experiência sem bloquear (validação fraca, mensagem incorreta).
- **Low** — incômodo ou polimento (UX, microinteração, copy).

---

## Regras

- **Não altere** o código da aplicação. Só pode escrever testes/relatórios.
- Em caso de dúvida sobre o produto, registre como pergunta no `TEST_PLAN.md` em vez de contatar o time — entender o que está dado é parte da avaliação.

---

## Submissão

1. **Fork** este repositório para sua conta pessoal.
2. Clone o seu fork:

   ```bash
   git clone https://github.com/<seu-usuario>/cadastra-qa-challenge.git
   cd cadastra-qa-challenge
   ```

3. Copie os templates para a raiz e preencha:

   ```bash
   cp -r submission-template/* .
   # edite TEST_PLAN.md, TEST_EXECUTION.md, bugs.yaml
   ```

4. Crie uma branch, commit e push para o **seu fork**:

   ```bash
   git checkout -b submission
   git add TEST_PLAN.md TEST_EXECUTION.md bugs.yaml
   git commit -m "QA submission - <seu-nome>"
   git push origin submission
   ```

5. **Abra um Pull Request** do seu fork (`submission`) de volta para este repositório (`main` de `Cadastra-Next-Gen-Company/cadastra-qa-challenge`). Use o título `QA submission - <seu-nome>`.

Em poucos segundos, um comentário automático no PR confirma se a submissão é válida. A nota detalhada não aparece no PR — é enviada internamente para o time. Você é avaliado(a) na primeira PR; push de correções na mesma branch dispara nova rodada.

Boa caça.
