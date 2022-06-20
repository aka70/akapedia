# RESTful APIの設計

## 用語

|用語|定義|
----|---- 
|リソース|データの一部（例：ユーザー）|
|コレクション|リソースのグループ（例：ユーザーリスト）|
|URL|リソースやコレクションの場所（例：/user）|

## URL設計

- URLにケバブケースを使う(例: /user-orders)
- コレクションで始まり、識別子で終わる
- (例: GET /users/:userId)
- リソースAPIにURLに動詞を含めない。HTTPメソッドで操作を表現する。(例: PUT /users/:userId)
- 非リソースURLには動詞を使う。(例: POST /mail/resend)
- モニタリング用のAPIを作成する**必要がある** 
  - `/health` 200 OKを返す
  - `/version` APIのバージョンを返す
  - `/debug`と`/status`もあると良い
- APIをバージョン管理する(例: /v1/users)

## リクエスト設計
- GETのエンドポイントを作る場合は`limit`,`offset`,`field`パラメーターを受け入れられるようにするとフロントエンドでの処理が楽になる。(例: GET /users?offset=5?limit=5?fields=id,name)
- 認証トークンをGETパラメーターに含めないようにする。(ブラウザの履歴やサーバーのログに残ってしまうので) 変わりにリクエストヘッダーで送るようにする。(例: Authorization: Bearer xxxxxx)
- `Content-type`は必ず指定するようにする。`application/x-www-form-urlencoded`より`application/json`を使ったほうが良さげ。
- `application/json`を使用する場合、プロパティはキャメルケースにする。(例: {userId: 1})
- ネストされたリソースURLにリレーションを使う
  - `GET /users/2/articles`: ユーザー2の全記事を取得
  - `GET /users/3/articles/3`: ユーザー3の記事3を取得
  - `PUT /users/2/articles/32`: ユーザー2の記事32を更新する(PUTはリソースURLにのみ使う)
  - `POST /users`: 新しいユーザーを作成する(POSTはコレクションURLに使う) 

|メソッド|アクション|
----|---- 
|GET|リソース取得|
|POST|リソース新規作成|
|PUT|リソース更新|
|DELETE|リソース削除|
|PATCH|リソース(一部)更新|

## レスポンス設計
- レスポンスにリソースの総数を含める
```
例: 
{
    users: [
        ...
    ],
    total: 34
}
```
- HTTPステータスコードを正しく返す[参考](https://developer.mozilla.org/ja/docs/Web/HTTP/Status)
- エラーの際はエラーの原因と解決方法をレスポンスに含めると親切
```
TwitterAPIのレスポンスの例
{
  "errors": [
    {
      "message": "Bad Authentication data",
      "code": 215
    }
  ]
}
```
