---
sidebar_position: 2
---

# バックエンド
ここにはバックエンドの仕様等をまとめています。  
基本的な仕様はバックエンド起動時にOpenAPIで自動でまとめられます。  
それをSwagger UIで見るには`/docs`にアクセスしましょう。  
このドキュメントでのエンドポイントについての説明は不足しがちですが、`/docs`にある場合はわざと不足させるので、そう言った際は`/docs`をご確認ください。

## Bot(RT本体)専用エンドポイント
`Authorization`をヘッダーで必要としている一部エンドポイント(シャード管理用エンドポイント等)はBot専用のエンドポイントとなっています。  
このヘッダーに入れる署名は、Bot側プログラムのBotのインスタンスの`signature`という属性から取得が可能です。  
入れる場合は`Authorization: Rt <ここに署名>`のように入れてください。  
なお、Botのインスタンスには、このヘッダーを辞書形式で作る関数`make_auth_headers`があります。

## エラー時のレスポンスについて
エラー時は以下のような形式でデータが返されます。うまく使ってください。
```js
{
  "brief": "簡単なエラーの説明",
  "type": "エラータイプ", // エラーの種類。ステータスコードが400のエラーの場合でも、複数の種類のエラーがあり得る場合がある。そういう際にどのエラーなのかを識別するためのエラー。もし一種類しかない場合は基本的に`"general"`とするべきである。
  "just_show": false, // ユーザーにエラー内容を報告するだけでいいかどうか。これが`true`ならただユーザーにこう言うエラーが起きたと伝えればいいが、`false`の場合はプログラムがおかしいことによって発生している可能性が高く、ユーザーにエラーを報告するだけでなく開発者側も何かしらの対応をする必要が高いことを示す。
  "context": ..., // 追加データ。エラーについての情報をユーザーに提供するためのデータや、代わりの動作をしたりするのに必要なデータを入れたりする。
}
```

## 429エラーについて
いくつかのエンドポイントはリクエストしすぎると429エラーが発生します。  
そう言ったエンドポイントのドキュメンテーションには「五秒に一回」といった説明がありますが、初めてエラーになる前の3回程は429エラー発生を見逃すように大抵はなっています。

## その他
ログインは`/api/discord/login`にてできます。
