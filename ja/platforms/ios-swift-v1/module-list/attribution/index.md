---
title: アトリビューションモジュール
description: 各トラッキングコールにユーザーリセット可能な広告識別子（IDFA）を追加し、オプションでApple Search Ads APIを実装してアトリビューション情報を収集します。
url: https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/attribution/
---

## 使用方法

アトリビューションモジュールは、各トラッキングコールにユーザーリセット可能な広告識別子（IDFA）を追加し、オプションでApple Search Ads APIを実装してアトリビューション情報を収集します。Apple Search Adsの詳細については[こちら](https://searchads.apple.com/v/advanced/help/pdf/attribution-api.pdf)をご覧ください。

このモジュールの使用はオプションです。その機能について読んで、必要かどうかを判断してください。なぜなら、それは追加の依存関係を導入します。あなたはAppleに対して、なぜIDFAを使用しているのかを説明する必要があります。IDFAの使用を申告しない場合、Appleはあなたのアプリを拒否します。IDFAの使用と拒否についての詳細は[こちら](https://developer.apple.com/app-store/review/rejections/)をご覧ください。

以下のプラットフォームがサポートされています：

* iOS

## 要件

* UIKit
* AdSupport
* iAd

## インストール

CocoaPodsまたはCarthageでアトリビューションモジュールをインストールします。

### CocoaPods

CocoaPodsでアトリビューションモジュールをインストールするには、以下のpodをPodfileに追加します：  
```ruby
pod &#39;tealium-swift/TealiumAttribution&#39;
```

フレームワークは自動的にインスタンス化されます。`TealiumCore` podに依存しています。iOSのCocoaPodsインストールについての詳細は[こちら](/ja/platforms/ios-swift-v1/install/#cocoapods)をご覧ください。


### Carthage

Carthageでアトリビューションモジュールをインストールするには、以下の手順を実行します：

1. Xcodeでアプリターゲットの一般構成ページに移動します。

2. 次のフレームワークを**Embedded Binaries**セクションに追加します：  
    ```ruby
    TealiumAttribution.framework
    ```

フレームワークは自動的にインスタンス化されます。`TealiumCore`に依存しています。追加のインポートステートメントは必要ありません。iOSのCarthageインストールについての詳細は[こちら](/ja/platforms/ios-swift-v1/install/#carthage)をご覧ください。


## データレイヤー
モジュールが有効な間、以下の変数が各トラッキングコールで送信されます：

| 変数名 | 説明 | 例 |
| --- | --- | --- |
| `ad_campaign_id` | 対応する広告のキャンペーンID | `1234567890` |
| `ad_campaign_name` |  対応する広告のキャンペーン名 | `CampaignName` |
| `ad_creativeset_id` | 対応する広告が一部であったクリエイティブセットのID。 | `456093` |
| `ad_creativeset_name` | 対応する広告が一部であったクリエイティブセットの名前。| `Beast Images` |
| `ad_group_id` |  対応する広告のキャンペーングループID | `1234567890` |
| `ad_group_name` |  対応する広告のキャンペーングループ名| `AdGroupName` |
| `ad_keyword` | 対応する広告クリックにつながる広告インプレッションを駆動したキーワード| `Keyword` |
| `ad_keyword_matchtype` | これは、Broad、Exact、またはSearch Matchのいずれかである可能性があります。 | `Exact` |
| `ad_org_id` |  対応する広告のキャンペーン組織ID | `OrgID` |
| `ad_org_name` |  対応する広告のキャンペーン組織名 | `OrgName` |
| `ad_purchase_date` | ユーザーが初めてアプリをダウンロードした日時。`iadconversion-type = &#34;Redownload&#34;`の場合、これは元の購入日を表します。これはApple Search Adに関連していたかもしれませんし、いなかったかもしれません。| `2016-12-05T17:31:40Z` |
| `ad_region` | このインストールを駆動したキャンペーンに関連する国または地域を識別します。 | `US` |
| `ad_user_clicked_ last_30_days` | ユーザーがアプリをダウンロードする30日前にSearch Adsのインプレッションをクリックしたかどうかを示すブール値 | [`true`, `false`] |
| `ad_user_conversion_type` | アプリの新規ダウンロードまたは再ダウンロードを識別します| `Download` |
| `ad_user_date_ clicked` | ユーザーが対応する広告をクリックした日時| `2016-12-05T17:31:40Z` |
| `ad_user_date_ converted` | ユーザーがアプリをダウンロードした日時| `2016-12-05T17:31:40Z` |
| `device_advertising_ enabled` | ユーザーが広告トラッキングを許可したかどうかを示すブール値（`false`の場合、広告IDはゼロの文字列として表示されます）| [`true`, `false`] |
| `device_advertising_ id` | ユーザーリセット可能な広告識別子（IDFA）| `6D92078A-8246...` |
| `device_advertising_ vendor_id` | 同一ベンダーからの同一デバイス上のすべてのアプリで同じであることが保証された一意のID（RDNSバンドル識別子の最初の2部分が同じアプリ。例えば、com.tealiumまたはcom.acme）| `6D92078A-8246...` |


`ad_`で始まる変数は、Search Adsが[TealiumConfig](/ja/platforms/ios-swift-v1/api/tealium-config/)オブジェクトで明示的に有効にされている場合にのみ有効になります。これらの変数はAppleのサーバーからアプリの寿命中に一度だけ取得されますが、永続的な変数として保存されるため、将来のアプリの起動時に利用可能です。