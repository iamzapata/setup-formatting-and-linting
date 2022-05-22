# Install lint-staged

```bash
yarn add lint-staged -D
```

## Install Prettier

```bash
yarn add prettier -D
```

## Prettier Ignore

1) create ignore file:

```bash
touch .prettierignore
```


2) Add contents to .prettierignore:

```bash
# Ignore artifacts:
build
coverage
.vscode
.vercel
.next
.husky
public
node_modules

# Ignore all HTML files:
*.html

*-lock.json
```

## Prettier Config

```bash
{
  "printWidth": 80,
  "tabWidth": 2,
  "semi": false,
  "trailingComma": "es5",
  "singleQuote": true,
  "useTabs": false,
  "importOrderSeparation": true,
  "importOrderSortSpecifiers": true
}

```

## Install ESLint

```bash
yarn add @typescript-eslint/parser @typescript-eslint/eslint-plugin eslint eslint-config-prettier eslint-plugin-jsx-a11y -D
```

## ESLint Config

1) create config file:

```bash
touch .eslintrc.js
```

2) Add eslint config:

```bash
module.exports = {
  plugins: ['@typescript-eslint', 'jsx-a11y'],
  extends: [
    'plugin:@typescript-eslint/recommended',
    'prettier',
    'plugin:jsx-a11y/recommended',
  ],
  rules: {
    '@typescript-eslint/no-unused-vars': 'error',
    '@typescript-eslint/no-explicit-any': 'error',
  },
}

```

## Install Husky

```bash
npx husky-init && yarn
```

## Create lint-staged config

1) create config file:

```bash
touch lint-staged.config.js
```

2) Add lint-staged config:

```javascript
// lint-staged.config.js
module.exports = {
  // Type check TypeScript files
  '**/*.(ts|tsx)': () => 'yarn tsc --noEmit',

  // Lint then format TypeScript and JavaScript files
  '**/*.(ts|tsx|js)': (filenames) => [
    `yarn eslint --fix ${filenames.join(' ')}`,
    `yarn prettier --write ${filenames.join(' ')}`,
  ],

  // Format MarkDown and JSON
  '**/*.(md|json)': (filenames) =>
    `yarn prettier --write ${filenames.join(' ')} --ignore-unknown`,
}
```

