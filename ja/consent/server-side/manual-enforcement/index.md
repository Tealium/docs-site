---
title: サーバーサイドでの手動同意強制の実施
description: 訪問レベルのサーバーサイドシナリオで同意を手動で強制する方法、および自動強制が無効になっておりConsent Orchestrationを使用していない場合のイベントレベルのシナリオについて学びます。
url: https://docs.tealium.com/ja/consent/server-side/manual-enforcement/
---
イベントレベルのアクティベーションに手動強制を使用する場合は、より効率的な自動強制を提供するConsent Orchestrationへの移行を検討してください。Consent Orchestrationを有効にすると、レガシーなイベントレベルのサーバーサイド強制が無効になり、置き換えられます。詳細については、[Consent Orchestrationについて]()を参照してください。

AudienceStreamで訪問レベルの同意を強制する必要がある場合や、自動イベントレベルの同意強制を無効にしてConsent Orchestrationを使用していない場合には、手動強制が必要です。自動強制を無効にする方法については、[サーバーサイド同意管理]()を参照してください。

## EventStreamコネクタアクション、機能、およびEventStoreの構成

1. イベントレベルの`consent attributes`を特定します。

    * 上記の指示に従って自動強制を無効にしている場合、Tealium Consent Managerを使用している場合、許可されたユーザー同意のカテゴリーを含む文字列の配列である`consent_categories_granted`がWebイベントにあります。

    * サードパーティの同意マネージャーを使用している場合、`consent attributes`は数、名前、またはタイプが異なる場合がありますが、各イベントには関連する同意情報が公開されている必要があります。

    * イベントから同意決定を解析するために必要なロジックの複雑さに応じて、参照用の簡略化されたバージョンを作成できます。

    * これらの属性にラベルを付けることをお勧めします。

1. 各イベントフィードに適切なイベントレベルの`consent attributes`を含め、同意されたデータのみがアクティブ化されるようにします。

      ![](/images/server-side/image1.png)

## AudienceStreamコネクタ、機能、およびAudienceStoreの構成

1. 訪問プロファイルの同意を調整するための訪問レベルの`consent attributes`を作成します：
    * これらはイベントレベルの`consent attributes`に基づいており、訪問の最新の調整されたクロスデバイス同意の状態を明確に反映する必要があります。
    * これらの属性にラベルを付けることをお勧めします。

1. 同意されたデータのみがアクティブ化されるように、各オーディエンスに適切な訪問レベルの`consent attributes`を含めます。
    ![](/images/server-side/image5.png)

### AudienceDBでのAudienceStreamプロファイル処理のブロック

オーディエンスルールは、訪問プロファイルの構築やAudienceDBへの書き込みを防ぎません。

特定の条件下でプロファイルをブロックする必要がある場合は、AudienceStream Event Filterで使用する別の文字列属性を構成します。たとえば、`has_audiencestream_consent`という新しいイベント文字列属性を作成し、訪問が適切な同意を提供した場合（イベントレベルの`consent attributes`に基づいて）`true`になるように構成します。

![](/images/server-side/image2.png)

## ベストプラクティス

* チーム間の混乱を避けるために、すべての同意属性に明確なラベルを付けます。
* 現在の同意ポリシーに合わせて、強制ロジックを定期的に見直します。
* 可能であれば、手動構成を減らすためにイベントレベルの強制にConsent Orchestrationを使用します。
