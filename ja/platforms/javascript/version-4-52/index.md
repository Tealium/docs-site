---
title: バージョン4.52+に関する注意事項
description: バージョン4.52+の変更点と最新バージョンへの更新方法について学びましょう。
url: https://docs.tealium.com/ja/platforms/javascript/version-4-52/
---
すべてのリリースノートについては、[Tealium for Javascriptリリースノート](?filter=tealium-universal-tag)をご覧ください。

----

## 概要

バージョン4.52では、シングルページアプリケーション（SPA）のサポートが向上し、GoogleのInteraction to Next Paint（INP）スコアの最適化、ファーストパーティ構成でのセッションカウントの改善、およびいくつかのバグ修正とパフォーマンスの更新が行われています。

## バージョン4.52&#43;の重要な注意事項

バージョン4.52&#43;の変更を実装する前に、以下の注意事項を確認してください：

* **早期トラッキングイベントのためのキュー：** キュースニペットはバージョン4.52以降でのみ使用してください。それ以前のバージョンで追加すると、`utag.js`の実行が阻止されます。
* **ファーストパーティ、リバースプロキシ、または自己ホスト構成のセッションカウント：** ファーストパーティまたはリバースプロキシ構成を使用しているお客様は、重複セッションを避けるために以前のカスタムセッションカウントロジックを削除してください。自己ホスト構成の場合は、請求リクエストを無効にするためにTealiumサポートに連絡してください。

## 早期トラッキングイベントのためのキュー

このバージョンでは、トラッキング機能（`utag.view`、`utag.link`、`utag.track`）のキューシステムが追加され、ページロード時にすぐに利用可能になります。以前は、これらの機能は`utag.js`が完全にロードされるまで機能せず、SPAで早すぎる呼び出しによりエラーやイベントの損失が発生していました。

早期トラッキングイベントを確実にキャプチャするために、次のキューイングスニペットを[`utag.js`ローダースクリプト](/ja/platforms/javascript/install/#universal-tag-utagjs)の前にできるだけ早くページコードに配置する必要があります：

このスニペットはバージョン4.52以降でのみ使用してください。それ以前のバージョンで追加すると、`utag.js`の実行が阻止されます。

```javascript
&lt;script type=&#34;text/javascript&#34;&gt;
  (function(w){
    if(w.utag) return; var u=w.utag={}; u.e=[]; u.view=function(a,b,c){u.e.push({a:a,b:b,c:c,d:&#34;view&#34;})};
    u.link=function(a,b,c){u.e.push({a:a,b:b,c:c,d:&#34;link&#34;})};
    u.track=function(d,a,b,c){typeof d===&#34;object&#34; ? u.e.push({a:d.data,b:(d.cfg?d.cfg.cb:null),c:(d.cfg?d.cfg.uids:undefined),d:d.event}): u.e.push({a:a,b:b,c:c,d:d});
    };
  })(window);
&lt;/script&gt;
```

このスニペットを追加することで、早期トラッキングイベントがキューに入れられ、`utag.js`が実行されるとすぐに処理されます。キューに入れられたイベントは受け取った順に処理されます。

uTagローダースクリプト自体を変更しないでください。これにより、初期化プロセスの妨げになったり、トラッキングやタグの実行に予期せぬ動作が発生する可能性があります。

## ノンブロッキングタグオプション

新しい`nonblocking_tags`構成は、タグをノンブロッキングにする方法を提供し、タグの非同期ロードを可能にすることでInteraction to Next Paint（INP）スコアを改善するのに役立ちます。デフォルトでは、タグはブロッキングであり、トラッキングの実行を保証しますが、大規模またはリソースを多く消費するタグの場合、ページのロード時間が遅れる可能性があります。`nonblocking_tags`を有効にすることで、INPスコアをSEOで優先する顧客のパフォーマンスが最適化されます。

詳細については、[構成：`nonblocking_tags`](/ja/platforms/javascript/settings/#nonblocking_tags)および[Interaction to Next Paint（INP）とTealium iQ](https://tealium.com/blog/customer-data-platform/interaction-to-next-paint-inp-and-tealium-iq/)を参照してください。

## ファーストパーティ構成のセッションカウント

以前はカスタム構成が必要だったファーストパーティまたはリバースプロキシ構成にセッションカウントを追加します。新しい構成はセッションカウントを標準化し、カスタムスクリプトを必要とせずにファーストパーティ環境の精度を向上させます。

* ファーストパーティまたはリバースプロキシ構成を使用しているお客様は、重複セッションを避けるために以前のカスタムセッションカウントロジックを削除してください。
* 自己ホスト構成の場合は、請求リクエストを無効にするためにTealiumサポートに連絡してください。

## パフォーマンスの向上

このリリースには、以下のパフォーマンス向上が含まれています：

* **クッキーの読み取りを最小限に抑える**  
複数または複雑なクッキーがあるページのパフォーマンスを向上させるために、不要なクッキーの読み取りを最小限に抑える更新が行われました。`utag_main`クッキーは、クッキーベースのトラッキングやデータ保存に影響を与えることなく、繰り返しの読み取りを避けます。このエンリッチメントはバージョン4.52で自動的に適用されます。
* 長期にわたる一貫性のない挙動に対処し、予期せぬトラッキング問題を引き起こす可能性があるものを修正しました。これらの修正により、特に高度な実装においてTealium iQがより予測可能になります：
    * **Before Load RulesスコープのJavascript拡張**：Before Load Rulesにスコープされたすべての拡張は、UIDによって呼び出されたタグであっても、ページロードごとに一度だけ実行されます。従来の動作を維持するには、`suppress_before_load_rules_with_uids`を`true`に構成してください。詳細については、[構成：`suppress_before_load_rules_with_uids`](/ja/platforms/javascript/settings/#suppress_before_load_rules_with_uids)を参照してください。
    * **イベント属性の上書き**：すべての`tealium_*`イベント属性は、`tealium_visitor_id`と`tealium_event`を除いて、Tealiumによって生成された値によって自動的に上書きされます。これにより、データレイヤーで手動で構成された`tealium_*`属性との競合が防止されます。