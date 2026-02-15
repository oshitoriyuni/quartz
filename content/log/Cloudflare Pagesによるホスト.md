---
tags:
  - quartz
date: 2026-02-15
---


結論としては失敗してしまったけど、再度チャレンジするときのために記録。

### Quartzのドキュメント

https://quartz.jzhao.xyz/hosting#cloudflare-pages

これを読むとCloudflare Pages推奨のように見えたし、設定も簡単そうだったけどドキュメント通りだとデプロイがうまくできず詰みました。

### Wranglerの設定

上記ドキュメントにはビルドコマンドについて言及されていますが、デプロイコマンドも設定時に要求されます。

デフォルトで`npx wrangler deploy` が入力されていますが、これだけだとビルド失敗するので、なんとかしなければなりません。

#### エラー対応

- missing entry point → エントリーポイントのファイルが見つからない
- a compatibility_date is required when publishing　→ 互換性日付を指定して
- worker name が一致しない

解決策を調べてみたところ、これらの情報は必須らしいので、デプロイコマンドにPATHやオプションを追加するとか、`wrangler.jsonc` を作成して記述する必要があります。

この辺りはwranglerの更新により変動があり、戸惑っている方もインターネットではちらほらいらっしゃるようでした。

### APIの問題

Wranglerについてはなんとかエラーメッセージを見ながらなんとなく対処できそうでしたが、その後もCloudflare APIからエラーが返されてしまい最後までビルドができませんでした。

https://qiita.com/e52yamada/items/325c2c44e7c7c3a52ace

こちらの記事を拝見したところ、最後に書かれているようなsecretの設定が必要だったのかもしれません。

でもそこまで検証する気力がなく、諦めてGitHub Pagesでホストすることにしました。



結果的にはGitHub Pagesの方がスムーズにいきましたが、使っているうちに変更したくなったら再度挑戦したいと思います。