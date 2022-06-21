# eslint

# 設定のカスケーディング

ESLint ではリント対象のファイルと同階層の設定ファイルを優先的に使用する。つまり、`src/main/.eslintrc.js`を作成すると`src/main`以下のディレクトリに対して凛と設定を定義できる。electronなどでnodeとブラウザ用で凛とのルールを分けたいときなどに使う。

# 設定ファイル内でのプラグインの指定方法

eslintのプラグインを`npm i -D`でインストールし、 `.eslintrc.js`の`plugins`に指定する。このときプラグインの名前が`eslint-plugin-*`であればその部分を省略できる。`plugins`に指定しただけではルールは有効にならない。有効にしたい場合は`extends`に適用させるルールを指定する。。

## 設定例(React + ts)

```js
module.exports = {
  env: {
    browser: true,
    es2022: true,
  },
  extends: [
    "eslint:recommended",
    "plugin:@typescript-eslint/recommended",
    "plugin:react-hooks/recommended",
    "plugin:react/recommended",
    "prettier"
  ],
  //実行時に追加するグローバル変数
  globals: {
    Atomics: "readonly",
    SharedArrayBuffer: "readonly",
    React: "writable",
  },
  ignorePatterns: ["build"],
  parser: "@typescript-eslint/parser",
  parserOptions: {
    ecmaFeatures: { jsx: true },
    ecmaVersion: 2022,
    sourceType: "module",
    project: "./tsconfig.json",
  },
  plugins: ["@typescript-eslint", "react"],
  rules: {
    // ここに個別対応したいものを書く
  },
  settings: { react: { version: "detect" } },
};
```
