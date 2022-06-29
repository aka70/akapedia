# lint-staged

以下のコマンドを実行するといい感じに設定ファイルを作成してくれる。
```shell
npx mrm@2 lint-staged
```

lint-stagedのおすすめ設定
```json
{
  "lint-staged": {
    "**/*.{js,ts,tsx}": [
      "eslint --cache --fix",
      "prettier --write"
    ],
    "*.{css,md}": "prettier --write"
  },
}
```
