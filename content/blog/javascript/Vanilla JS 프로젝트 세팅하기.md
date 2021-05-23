---
title: 'Vanilla JS 프로젝트 세팅하기'
date: 2021-05-10 09:03:18
category: 'javascript'
draft: false
---

## 📝 description

Vanilla JS로 프로젝트를 진행할 때 제가 자주 사용하는 세팅을 정리한 글입니다. 전체 코드 및 Boilerplate는 아래 링크의 레포지토리에서 확인하실 수 있습니다.

- [vanilla-javascript-boilerplate](https://github.com/yujo11/vanilla-javascript-boilerplate)

## ⚙️ setting

### 1. yarn init

```
yarn init
```

### 2. install eslint, prettier

```
yarn add -D eslint prettier eslint-config-prettier eslint-config-airbnb-base eslint-plugin-import
```

### 3. install webpack, webpack-dev-server

```
yarn add -D webpack webpack-cli webpack-dev-server
```

### 4. install webpack plugins, loaders

```
yarn add -D babel-loader css-loader mini-css-extract-plugin html-webpack-plugin
```

### 5. install babel

```
yarn add -D @babel/core @babel/eslint-parser @babel/preset-env
```

### 6. setting lint-staged & husky

- [Husky 사용할 때 주의! / 김태곤님 블로그](https://taegon.kim/archives/10276)

> 라이선스의 변화
> Husky v4까지는 MIT 라이선스였기 때문에 사용하는 데 있어 아무런 제약이 없었다. 하지만 Husky v5에서는 약간의 변화가 생겼다. 현재 v5는 한시적인 기간, 조금 더 자세히 말하면 Early Access 기간에는 Parity License를 적용한다. 간단히 말해 "우리 저작물을 사용하려면 당신 저작물도 오픈하라"라는 것이다. GPL처럼 오픈하는 라이선스에 대해서는 제약을 두지 않고 있으나 결국 상업용 프로젝트에는 사용할 수 없다는 의미다.
> 단, Husky 프로젝트에 후원한 단체/개인에 한해서는 코드를 공개하지 않고도 사용할 수 있다. 다시 말해, Husky v5는 현재 오픈소스 혹은 프로젝트 후원자의 상업용 프로젝트에만 사용할 수 있다. 그 외의 경우에는 라이선스 위반이 된다.

프라이빗 레포에서 사용하실 경우 최신 버전이 아닌 4.X 버전을 사용하셔야 합니다!

#### 6-1. install package

```
yarn add -D lint-staged husky
```

#### 6-2. add config

- `package.json`

```
"lint-staged": {
  "*.js": "eslint --cache",
  "*.{js,css,md,html,json}": "prettier --write"
},
```

#### 6-3. set husky

- prepare husky

```
yarn husky install
```

- add pre-commit

```
npx husky add .husky/pre-commit "npx lint-staged"
```

### (optional) install cypress

- install cypress

```
yarn add -D cypress
```

- install eslint-plugin-cypress

```
yarn add -D eslint-plugin-cypress
```

- `.eslintrc.js` add config

```
extends: [plugin:cypress/recommended'],
```

## 📜 config files

### .gitignore

```
node_modules
.DS_Store
.eslintcache
```

### .prettierrc.js

```
module.exports = {
  printWidth: 120,
  singleQuote: true,
};
```

### .eslintrc.js

```
module.exports = {
  env: {
    browser: true,
    es2021: true,
  },
  parser: "@babel/eslint-parser",
  extends: ["airbnb-base", "prettier"],
  parserOptions: {
    ecmaVersion: 2021,
    sourceType: "module",
  },
  plugins: [],
  rules: {},
};
```

### webpack.config.js

```
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');
const MiniCssExtractPlugin = require('mini-css-extract-plugin');

module.exports = (_, argv) => {
  const isDevelopment = argv.mode !== 'production';

  return {
    entry: './src/index.js',
    output: {
      filename: 'bundle.js',
      path: path.resolve(__dirname, 'build'),
      clean: true,
    },
    devServer: {
      port: 3000,
      hot: true,
    },
    devtool: isDevelopment ? 'eval-source-map' : 'source-map',
    module: {
      rules: [
        {
          test: /\.(js)$/,
          exclude: /node_modules/,
          use: {
            loader: 'babel-loader',
            options: {
              cacheDirectory: true,
              cacheCompression: false,
              compact: !isDevelopment,
            },
          },
        },
        {
          test: /\.css$/,
          use: [MiniCssExtractPlugin.loader, 'css-loader'],
        },
      ],
    },
    plugins: [
      new HtmlWebpackPlugin({ template: './index.html' }), //
      new MiniCssExtractPlugin({ filename: 'style.css' }),
    ],
    performance: {
      hints: isDevelopment ? 'warning' : 'error',
    },
  };
};
```

### babel.config.js

```
module.exports = {
  presets: [
    [
      '@babel/preset-env',
      {
        targets: '> 1% and last 2 versions',
      },
    ],
  ],
};
```

### .editorconfig

```
root = true

[*]
indent_style = space
indent_size = 2
end_of_line = lf
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = true
```

### .vscode/settings.json

```
{
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "files.trimTrailingWhitespace": true,
  "editor.formatOnSave": true,
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  },
  "prettier.useEditorConfig": true,
  "prettier.enable": true,
}
```

### package.json scripts

```
"scripts": {
  "test": "yarn run cypress open",
  "prod": "webpack serve --mode=production",
  "dev": "webpack serve --mode=development",
  "build": "webpack --mode=production"
},
```
