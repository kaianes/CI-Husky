# 🛠️ Qualidade de Código com ESLint, Prettier, Husky, Testes e Commitizen

Este projeto utiliza uma configuração automatizada para garantir a qualidade e estabilidade do código antes de qualquer commit ou push.

---

## ⚙️ Ferramentas Utilizadas

- **ESLint**: análise estática para encontrar erros e más práticas.
- **Commitizen**: ferramenta que guia a escrita de mensagens de commit no padrão Conventional Commits.
- **Prettier**: formatação automática do código.
- **Husky**: execução de scripts em hooks do Git.
- **lint-staged**: aplica lint apenas nos arquivos modificados.
- **Jest**: testes automatizados.
- **TypeScript** + **Airbnb Base** para padronização de estilo.

---

## 🔐 Validações Automáticas

| Hook Git       | Ação Executada              |
|----------------|-----------------------------|
| `pre-commit`   | Lint + Compilação (`build`) |
| `pre-push`     | Testes automatizados        |
| `commit-msg`   | Verificação de Conventional Commits |

---

## 📁 Estrutura dos Hooks

### `.husky/pre-commit`

````bash
#!/usr/bin/env sh
. "$(dirname -- "$0")/_/husky.sh"

yarn lint-staged
yarn build
````

### `.husky/pre-push`

````bash
#!/usr/bin/env sh
. "$(dirname -- "$0")/_/husky.sh"

yarn test
````

### `.husky/commit-msg`

````bash
#!/bin/sh

if ! head -1 "$1" | grep -qE "^(feat|fix|docs|style|refactor|perf|test|chore|build|ci|revert|wip|improvement|update)(\(.+?\))?: .{1,}$"; then
  echo "ERROR: Commit message does not follow the conventional commit format." >&2
  echo "Please use one of the following types: feat, fix, docs, style, refactor, perf, test, chore, build, ci, revert, wip, improvement, update." >&2
  exit 1
fi

if ! head -1 "$1" | grep -qE "^.{1,88}$"; then
  echo "ERROR: Aborting commit. Commit message is too long." >&2
  exit 1
fi
````

---

## 🚀 Scripts disponíveis

````json
"scripts": {
  "lint": "eslint .",
  "lint:fix": "eslint  --fix",
  "test": "jest",
  "build": "tsc -p tsconfig.prod.json",
  "prepare": "husky install",
}
````

---

## 🧩 Configuração Padrão do ESLint

O projeto segue os padrões:

- `eslint:recommended`
- `@typescript-eslint/recommended`
- `airbnb-base`
- `plugin:prettier/recommended`

---

## ✔️ Benefícios

- Previne commits com código quebrado.
- Evita pushes com testes falhando.
- Garante histórico de commits padronizado.
- Mantém o código limpo, organizado e funcional.

---

## ▶️ Como utilizar

````bash
yarn install
yarn prepare
````

Para realizar commits com Commitizen:

````bash
yarn commit
````
