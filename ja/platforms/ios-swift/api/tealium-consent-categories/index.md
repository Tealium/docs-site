---
title: TealiumConsentCategories
description: Tealiumの同意カテゴリに関するメソッドを提供します。
url: https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-consent-categories/
---
## クラス: `TealiumConsentCategories`

以下は、iOS（Swift）の`TealiumConsentCategories`クラスの一般的に使用されるメソッドをまとめたものです。

| メソッド | 説明 |
| ----- | ------ |
| [`all`](#all) | サポートされているすべての同意カテゴリのリストを返します。 |
| [`consentCategoriesStringArrayToEnum()`](#consentcategoriesstringarraytoenum) | 同意したカテゴリを列挙型として返し、同意したカテゴリの文字列配列から変換します。 |

### `all `

サポートされているすべての同意カテゴリのリストを返します。

```swift
TealiumConsentCategories.all
```

| 戻り値の型 | 説明 |
| --- | --- |
| `[TealiumConsentCategories]` | 実装されているすべての同意カテゴリ。 |

以下の同意カテゴリが`[TealiumConsentCategories]`から利用可能です：

```swift
[.analytics
.affiliates
.displayAds
.email
.personalization
.search
.social
.bigData
.mobile
.engagement
.monitoring
.cdm
.cdp
.cookiematch
.misc]
```

### `consentCategoriesStringArrayToEnum()`

同意したカテゴリを列挙型として返し、同意したカテゴリの文字列配列から変換します。無効な文字列値は結果の配列から省略されます。

```swift
consentCategoriesStringArrayToEnum(categories)
```

| パラメータ | 型 |  説明 | 例 |
| --- | --- | --- | --- |
| `categories` | `[String]` | TealiumConsentCategoriesの配列に変換するための文字列の配列 | `[&#34;analytics&#34;, &#34;bigData&#34;]` |
