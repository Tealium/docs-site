---
title: バージョン4.52以降の注意事項
description: バージョン4.52以降の変更点と、最新バージョンへの更新方法について説明します。
url: https://docs.tealium.com/ja/platforms/javascript/version-4-52/
---
すべてのリリースノートについては、[Tealium for JavaScriptのリリースノート](?filter=tealium-universal-tag)を参照してください。

----

## 概要

バージョン4.52では、シングルページアプリケーション（SPA）のサポートエンリッチメント、GoogleのInteraction to Next Paint（INP）スコアの最適化、ファーストパーティ構成におけるセッションカウントの改善、および複数のバグ修正とパフォーマンス向上が導入されています。

## バージョン4.52以降に関する重要な注意事項

バージョン4.52以降の変更を実装する前に、以下の注意事項を必ず確認してください。

* **早期トラッキングイベント用のキュー：** キュースニペットは、バージョン4.52以降でのみ使用してください。それより前のバージョンに追加すると、`utag.js`が実行されなくなります。
* **ファーストパーティ、リバースプロキシ、またはセルフホスト構成でのセッションカウント：** ファーストパーティまたはリバースプロキシ構成を使用しているお客様は、セッションの重複を避けるため、以前のカスタムセッションカウントロジックを削除する必要があります。セルフホスト構成の場合は、課金リクエストを無効化するためにTealiumサポートへお問い合わせください。

## 早期トラッキングイベント用のキュー

このバージョンでは、トラッキング関数（`utag.view`、`utag.link`、`utag.track`）用のキューシステムが追加され、ページの読み込み直後からこれらの関数を使用できるようになりました。以前は、`utag.js`の読み込みが完全に完了するまでこれらの関数が動作しなかったため、シングルページアプリケーション（SPA）で呼び出しが早すぎると、エラーやイベントの欠落が発生していました。

早期トラッキングイベントを確実に取得するには、ページコード内の可能な限り早い位置で、[`utag.js`ローダースクリプト](https://docs.tealium.com/ja/platforms/javascript/install/#universal-tag-utagjs)より前に、次のキュースニペットを配置する必要があります。


<blockquote>
このスニペットは、バージョン4.52以降でのみ使用してください。それより前のバージョンに追加すると、`utag.js`が実行されなくなります。
</blockquote>


```javascript
<script type="text/javascript">
  (function(w){
    if(w.utag) return; var u=w.utag={}; u.e=[]; u.view=function(a,b,c){u.e.push({a:a,b:b,c:c,d:"view"})};
    u.link=function(a,b,c){u.e.push({a:a,b:b,c:c,d:"link"})};
    u.track=function(d,a,b,c){typeof d==="object" ? u.e.push({a:d.data,b:(d.cfg?d.cfg.cb:null),c:(d.cfg?d.cfg.uids:undefined),d:d.event}): u.e.push({a:a,b:b,c:c,d:d});
    };
  })(window);
</script>
```

このスニペットを追加すると、早期トラッキングイベントがキューに登録され、`utag.js`が実行されるとすぐに処理されます。キューに登録されたイベントは、受信した順序で処理されます。

uTagローダースクリプト自体は変更しないでください。初期化プロセスに干渉したり、トラッキングやタグの実行で予期しない動作を引き起こしたりして、`utag.js`が正常に機能しなくなる可能性があります。

## 非ブロッキングタグオプション

新しい`nonblocking_tags`構成を使用すると、タグを非ブロッキングにできます。タグを非同期で読み込めるようにすることで、Interaction to Next Paint（INP）スコアの改善に役立ちます。デフォルトではタグはブロッキング方式であり、トラッキングを確実に実行できますが、大規模なタグやリソースを大量に消費するタグでは、ページの読み込み時間が遅くなる場合があります。`nonblocking_tags`を有効にすると、SEOのためにINPスコアを重視するお客様向けにパフォーマンスが最適化されます。

詳細については、[構成：`nonblocking_tags`](https://docs.tealium.com/ja/platforms/javascript/settings/#nonblocking_tags)および[Interaction to Next Paint（INP）とタグ管理](https://tealium.com/blog/customer-data-platform/interaction-to-next-paint-inp-and-tealium-iq/)を参照してください。

## ファーストパーティ構成でのセッションカウント

これまでセッションを計測するためにカスタム構成が必要だったファーストパーティまたはリバースプロキシ構成に、セッションカウントが追加されました。この新しい構成により、カスタムスクリプトを使用せずにセッションカウントが標準化され、ファーストパーティ環境での精度が向上します。

* ファーストパーティまたはリバースプロキシ構成を使用しているお客様は、セッションの重複を避けるため、以前のカスタムセッションカウントロジックを削除する必要があります。
* セルフホスト構成の場合は、課金リクエストを無効化するためにTealiumサポートへお問い合わせください。

## パフォーマンスの向上

このリリースには、以下のパフォーマンス向上が含まれています。

* **Cookie読み取りの最小化**  
不要なCookieの読み取りを最小限に抑えるよう更新され、複数または複雑なCookieを使用するページでのパフォーマンスが向上しました。`utag_main` Cookieでは、Cookieベースのトラッキングやデータ保存に影響を与えることなく、反復的な読み取りが行われないようになりました。この機能エンリッチメントは、バージョン4.52で自動的に適用されます。
* 予期しないトラッキング問題を引き起こす可能性があった、従来からの一貫性のない動作に対処しました。これらの修正により、特に高度な実装において、タグ管理の動作がより予測しやすくなります。
    * **Before Load RulesスコープのJavaScript拡張機能**：Before Load Rulesをスコープとするすべての拡張機能が、UIDによって呼び出されたタグについても、ページ読み込みごとに1回実行されるようになりました。従来の動作を維持するには、`suppress_before_load_rules_with_uids`を`true`に構成します。詳細については、[構成：`suppress_before_load_rules_with_uids`](https://docs.tealium.com/ja/platforms/javascript/settings/#suppress_before_load_rules_with_uids)を参照してください。
    * **イベント属性の上書き**：バージョン4.52および4.53では、`tealium_visitor_id`と`tealium_event`を除くすべての`tealium_*`イベント属性が、Tealiumによって生成された値で自動的に上書きされます。バージョン4.54以降、この保護機能はオプトイン方式になります。受信した値によってシステム定義の`tealium_*`属性が上書きされないようにするには、[`disable_tealium_attribute_override`](https://docs.tealium.com/ja/platforms/javascript/settings/#disable_tealium_attribute_override)を`true`に構成します。