---
title: ConsentCategory
description: Tealium for Android（Kotlin）によって提供されるConsentCategoryクラスとメソッドのリファレンスガイド。
url: https://docs.tealium.com/ja/platforms/android-kotlin/api/consent-category/
---
## クラス: `ConsentCategory`

以下は、Kotlinの`ConsentCategory`クラスの一般的に使用されるメソッドをまとめたものです。

| メソッド | 説明 |
| ----- | ------ |
| [`ALL`](#all) | サポートされているすべての同意カテゴリのリストを返します |
| [`consentCategory(String)`](#consentcategory-string) | 与えられたStringに関連するConsentCategoryを返します。それ以外の場合はnull |
| [`consentCategories(Set&lt;String&gt;)`](#consentcategories-set-string) | 与えられたStringsに関連する`ConsentCategory`オブジェクトのセットを返します。無効なエントリは無視されます。 |


### `ALL`

利用可能なすべての`ConsentCategory`アイテムの完全なセットを返します。

```java
ConsentCategory.ALL
```

以下は、利用可能なカテゴリの全セットです：

```java
setOf(
    AFFILIATES,
    ANALYTICS,
    BIG_DATA,
    CDP,
    COOKIEMATCH,
    CRM,
    DISPLAY_ADS,
    EMAIL,
    ENGAGEMENT,
    MOBILE,
    MONITORING,
    PERSONALIZATION,
    SEARCH,
    SOCIAL,
    MISC
)
```

### `consentCategory(String)`

与えられたStringに対応する`ConsentCategory`を返します。パラメータは大文字小文字を区別しません。

```java
ConsentCategory.consentCategory(&#34;cdp&#34;) // ConsentCategory.CDPを返します
```

### `consentCategories(Set&lt;String&gt;)`

与えられたStringsに対応する`ConsentCategory`オブジェクトのセットを返します。パラメータは大文字小文字を区別しません。

```java
ConsentCategory.consentCategories(setOf(&#34;cdp&#34;, &#34;invalid&#34;, &#34;email&#34;))
// setOf(ConsentCategory.CDP, ConsentCategory.EMAIL)を返します
```
