---
title: バージョン4.50+の注記
description: バージョン4.50+の変更点と最新バージョンへの更新方法について学びます。
url: https://docs.tealium.com/ja/platforms/javascript/version-4-50/
---
すべてのリリースノートについては、[Tealium for Javascriptリリースノート](?filter=tealium-universal-tag)をご覧ください。

----

最新の修正とエンリッチメントを活用するために、[`utag.js`テンプレートを更新](https://support.tealiumiq.com/en/support/solutions/articles/36000363470)してください。

### バージョン4.50以降への更新

バージョン4.50以降への更新時にスムーズな移行を確保するために、以下の手順を推奨します：


<blockquote>
Tealium CollectタグとすべてのアクティブなConsent管理テンプレート、特にEvent Logging機能を更新してください。
</blockquote>


* 同じサイトで複数のiQプロファイルを実行している場合、以下の手順を完了して、サイト上の`utag.js`のすべてのインスタンスが新しいクッキーの動作を同時に開始し、競合や互換性の問題を防ぎます：
    1. すべての`utag.js`テンプレートを最新バージョンに更新します。
    1. 各プロファイルで[`split_cookie`](https://docs.tealium.com/settings/#split_cookie)オーバーライドを`false`に構成して、過去のバージョンのutag.jsとの互換性を保つためにレガシークッキーの動作を使用します。
    1. すべての`utag.js`テンプレートが更新され、レガシークッキーの動作を維持するために`split_cookie`オーバーライドを構成したら、すべてのプロファイルでクッキーオーバーライドを同時に削除できます。

* Tealium Collectタグ以外でVisitor ID (`v_id`)に依存している場合は、`always_set_v_id`オプションを`true`に構成して、その値がタイムリーに構成されるようにします。Visitor IDの使用の最も一般的な例は次のとおりです：
  * Cookie syncタグ。
  * `tealium_visitor_id`をAdobeやGA4などの分析タグにマッピングし、トラブルシューティングとダウンストリームデータウェアハウスでの使用。

詳細については、[構成：`always_set_v_id`](https://docs.tealium.com/ja/platforms/javascript/settings/#always_set_v_id)をご覧ください。