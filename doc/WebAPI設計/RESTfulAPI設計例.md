# RESTful API設計例

ユーザー(user)とユーザーの書いた記事(article)をリソースとするWebアプリのAPIを考えてみる。

## リソースの定義

    User = {
      id: number,
      name: string,
      bio: string,
      password: string,
      email: string,
      createdAt: string
    }

    Article = {
      id: number,
      userId: number,
      title: string,
      tag: string[],
      body: string,
      createdAt: string,
    }

## API設計

### ユーザー系

| URL               | メソッド   | アクション    |
| ----------------- | ------ | -------- |
| v1/users          | GET    | ユーザー一覧取得 |
| v1/users/{userId} | GET    | ユーザー詳細取得 |
| v1/users          | POST   | ユーザー新規作成 |
| v1/users/{userId} | PUT    | ユーザー情報更新 |
| v1/users/{userId} | DELETE | ユーザー削除   |

### 記事系

| URL                     | メソッド   | アクション   |
| ----------------------- | ------ | ------- |
| v1/articles             | GET    | 記事一覧を取得 |
| v1/articles/{articleId} | GET    | 記事詳細を取得 |
| v1/articles             | POST   | 記事を新規投稿 |
| v1/articles/{articleId} | PUT    | 記事を編集   |
| v1/articles/{articleId} | DELETE | 記事を削除   |

### いいね

| URL                          | メソッド   | アクション    |
| ---------------------------- | ------ | -------- |
| v1/articles/{articleId}/like | PUT    | いいねをつける  |
| v1/articles/{articleId}/like | DELETE | いいねを解除する |
