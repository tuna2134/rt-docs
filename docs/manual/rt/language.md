# 言語設定
ユーザーおよびサーバー全体の言語設定です。  
デフォルトの設定は英語です。

## 設定方法
### ダッシュボード
...
### コマンド `/language`
言語を設定するためのコマンドです。
引数は二つあり、一つ目の引数でサーバーの設定なのか実行者の設定なのかを指定し、二つ目の引数で言語を指定します。  

### 例
- `/language server ja`
  サーバーの言語を日本語にする。
- `/language user en`
  このコマンドを実行した人の言語を英語とする。

## 優先順位について
「デフォルトの設定 < サーバーの言語設定 < ユーザーの言語設定」のような優先順位でRTが表示するメッセージの言語は変わります。  
例えば、何もしていない場合は英語の言語設定となり、サーバーに日本語が設定されているときは、何もしていない人の言語が日本語になります。