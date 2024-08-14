# Configurar Jest no Angular

**Desinstalando o Karma**

```bash
npm uninstall karma karma-chrome-launcher karma-coverage-istanbul-reporter karma-jasmine karma-jasmine-html-reporter karma-coverage jasmine-core
```

---

**Apagar os arquivos `karma.conf.js` `test.ts`**

**Remover bloco `test` do arquivo `angular.config`**

---

**Instalando as libs**

```bash
npm install jest jest-preset-angular @types/jest ts-node --save-dev
```

---

**Criar arquivo `setup-jest.ts`**

```jsx
import 'jest-preset-angular/setup-jest';
```

---

**Atualizar `tsconfig.spec.json`**

```json
{
  "extends": "./tsconfig.json",
  "compilerOptions": {
    "outDir": "./out-tsc/spec",
    "types": [
      "jest",
      "node"
    ]
  },
  "files": [
    "src/setup-jest.ts",
  ],
  "include": [
    "src/**/*.spec.ts",
    "src/**/*.d.ts"
  ]
}
```

---

Criar arquivo de configuração do jest **`*jest.config.ts*`**

```jsx
import type {Config} from 'jest';

const config: Config = {
  collectCoverageFrom: [
    '**/*.{js,jsx}',
    '!**/node_modules/**',
    '!**/vendor/**',
  ],
  preset: "jest-preset-angular",
  setupFilesAfterEnv: ["<rootDir>/setup-jest.ts"],
  globalSetup: 'jest-preset-angular/global-setup',
  testPathIgnorePatterns: [
    "<rootDir>/node_modules/",
    "<rootDir>/dist/"
  ],
  transform: {
    '^.+\\.(ts|js|html)$': ['jest-preset-angular', {
      tsConfig: "<rootDir>/tsconfig.spec.json",
      stringifyContentPathRegex: "\\.html$"
    }]
  },
};

export default config;
```

---

Trocar o script de teste pelo `jest`

```json
"scripts": {
    "ng": "ng",
    "start": "ng serve",
    "build": "ng build",
    "watch": "ng build --watch --configuration development",
    "test": "jest"
  },
```
