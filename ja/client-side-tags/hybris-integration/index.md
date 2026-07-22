---
title: Hybris統合
description: この記事では、Hybris統合タグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/hybris-integration/
---
## 前提条件

* Tealium IQアカウント。
* hybris v5.0.1+が展開およびビルドされ、B2C Commerce Acceleratorが含まれています。

## 定義

* Universal Data Object (UDO) = キーと値のペアのData Layerオブジェクト。   
 このオブジェクトは、グローバルJavaScriptオブジェクト`utag_data`としてページに生成されます。Tealiumの`utag.js`は、タグの基本Data Layerとして`utag_data`を使用します。
* Tealiumアカウント = Tealium iQの購入に割り当てられたアカウント。
* Tealiumプロファイル = あなたのウェブサイトの特定のウェブプロパティ名。

## アドオンのインストール

**Githubリポジトリ**: `https://github.com/Tealium/integration-hybris`

1. `tealiumiqaddon`ディレクトリを`${HYBRIS_BIN}/custom`に配置します。このディレクトリはリポジトリの`/hybris/bin/custom/`フォルダにあります。
1. `config/localextensions.xml`に&lt;extension dir="$\{HYBRIS_BIN\}/custom/tealiumiqaddon"/\\&gt;を追加します。
1. `yacceleratorstorefront`に`tealiumiqaddon`を追加します。以下を使用します:  
  - `sudo ant addoninstall -Daddonnames="tealiumiqaddon"  `
  - `DaddonStorefront.yacceleratorstorefront="yacceleratorstorefront"`
1. 次のファイルを更新します:  
  * `${HYBRIS_BIN\}/ext-template/yacceleratorstorefront/web/webroot/WEB-INF/tags/desktop/template/master.tag`に以下を追加します:<br>&lt;%@ taglib prefix="tealiumiqaddon" tagdir="/WEB-INF/tags/addons/tealiumiqaddon/shared/analytics" %&gt;をファイルの先頭に追加します。<br>&lt;tealiumiqaddon:sync/&gt;を&lt;head&gt;タグの後に追加します。<br>&lt;tealiumiqaddon:tealium/&gt;を&lt;body&gt;タグの後に追加します。
  * `${HYBRIS_BIN}/custom/tealiumiqaddon/project.properties.template`を変更します:<br> **tealiumiqaddon.account**,**tealiumiqaddon.profile**, および **tealiumiqaddon.target**をあなたのTealium IQアカウント固有の情報に変更します。<br>`tealiumiqaddon.utagSyncEnabled = 1`を変更して、`utag.sync.js`の注入をHTMLページの&lt;head&gt;に有効にします。この機能はオプションで、デフォルトでは無効になっています。

## カスタムデータの追加

デフォルトでは、アドオンは標準的なe-commerce変数の包括的なリストを提供します。これらのデフォルト値があなたのインストールに十分でない場合は、デフォルトのページタイプを拡張したり、新しいカスタムページタイプを作成したりできます。

1. `com.tealium.dataconnector.hybris.HybrisDataConverter.HybrisCustomDataConverter`インターフェースを実装する新しいクラスを作成し、インターフェースのすべてのメソッドを実装します。  
```
package com.tealium.dataconnector.hybris;
import com.tealium.dataconnector.hybris.HybrisDataConverter.HybrisCustomDataConverter;
import com.tealium.dataconnector.hybris.HybrisDataConverter.HybrisCustomPageTypeCustomData;
import com.tealium.util.udohelpers.UDO;
import com.tealium.util.udohelpers.exceptions.UDOUpdateException;
public class TealiumCustomData implements HybrisCustomDataConverter {
	// ... add unimplemented methods of interface.
}
```

1. インターフェースのメソッドに値を追加**しない**場合は、`udo`オブジェクトを返すようにします。
```
@Override
public UDO homePage(UDO udo) {
	return udo;
}
```

1. デフォルトページに値を追加または変更するには、そのページのオーバーライドメソッドに追加します。  
```
@Override
public UDO searchPage(UDO udo) {
	try {
		udo.setValue("page_name", "new search page name");
		udo.setValue("custom_key", "custom_value");
		} catch (UDOUpdateException e) {
			e.printStackTrace();
	    }
		return udo;
	 }
```

1. 値を持つ新しいページタイプを追加するには、クラスに静的変数を追加し、新しいページを`addCustomPages`メソッドに追加します:
```
public class TealiumCustomData implements HybrisCustomDataConverter {
private static Map<String, HybrisCustomPageTypeCustomData> customPagesMap;
@Override
public Map<String, HybrisCustomPageTypeCustomData> getHybrisCustomPageTypes() {
	return customPagesMap;
}
//... other methods
@Override
public void addCustomPages() {
	if (customPagesMap == null){
	    customPagesMap = new HashMap<>();
	}
		customPagesMap.put("custom_one", new HybrisCustomPageTypeCustomData(){
	@Override
	public UDO getCustomDataUdo(UDO udo) {
		try {
		     udo.setValue("page_name", "custom page 1");
		     udo.setValue("custom_page1_key", "custom value");
		    } catch (UDOUpdateException e) {
			e.printStackTrace();
		    }
		    return udo;
	        }
	});
	customPagesMap.put("custom_two", new HybrisCustomPageTypeCustomData(){
	@Override
	public UDO getCustomDataUdo(UDO udo) {
		try {
			udo.setValue("page_name", "custom page 2");
			udo.setValue("custom_page2_key", "custom value");
		    } catch (UDOUpdateException e) {
			e.printStackTrace();
		    }
		return udo;
		}
	});
	}
}
```

1. 変更します:   
 `${HYBRIS_BIN\}/custom/tealiumiqaddonweb/webroot/WEB-INF/tags/addons/tealiumiqaddon/shared/analytics/data.tag`
  * `CLASS_NAME`をあなたのクラス名に置き換えます（例えば、`TealiumCustomData`）
  * 新しいクラスを追加します: &lt;%@ tag import="com.tealium.dataconnector.hybris. CLASS_NAME "%&gt;
  * 新しいクラスをHybrisDataConverterに登録します: &lt;%HybrisDataConverter.registerCustomDataClass("ID", new CLASS_NAME ()); %&gt;

## 完了

hybrisを再ビルドして再起動します。

* `sudo ant all`
* `sudo ./hybrisserver.sh`

## デフォルトのデータソース

### 全ページ

|ソース| 説明|
|---| ---|
|`page_name`| ユーザーフレンドリーなページ名を含みます|
|`site_region`| 地域またはローカライズされたバージョンの値を含みます。例えば、`en_US`|
|`site_currency`| サイトに表示される通貨を含みます。例えば、`USD`|
|`page_type`| ユーザーフレンドリーなページタイプを含みます。例えば、カートページ|

### 検索ページ

|ソース| 説明|
|---| ---|
|`search_results`| 検索クエリで返された結果の数を含みます|
|`search_keyword`| ユーザーが行った検索クエリを含みます|

### カテゴリーページ

|ソース| 説明|
|---| ---|
|`page_category_name`| ユーザーフレンドリーなカテゴリー名を含みます。例えば、ホーム電|

### 商品ページ

|ソース| 説明|
|---| ---|
|`product_id`| 商品IDを含みます。複数の値はカンマで区切られます|
|`product_sku`| 商品SKUを含みます。複数の値はカンマで区切られます|
|`product_name`| 商品名を含みます。複数の値はカンマで区切られます|
|`product_brand`| 商品ブランドを含みます。複数の値はカンマで区切られます|
|`product_category`| 商品カテゴリーを含みます。複数の値はカンマで区切られます|
|`product_subcategory`| 商品サブカテゴリーを含みます。複数の値はカンマで区切られます|
|`product_unit_price`| 商品の単価を含みます。複数の値はカンマで区切られます|

### カートページ

|ソース| 説明|
|---| ---|
|`product_id`| 商品IDを含みます。複数の値はカンマで区切られます|
|`product_sku`| 商品SKUを含みます。複数の値はカンマで区切られます|
|`product_name`| 商品名を含みます。複数の値はカンマで区切られます|
|`product_brand`| 商品ブランドを含みます。複数の値はカンマで区切られます|
|`product_category`| 商品カテゴリーを含みます。複数の値はカンマで区切られます|
|`product_subcategory`| 商品サブカテゴリーを含みます。複数の値はカンマで区切られます|
|`product_unit_price`| 商品の単価を含みます。複数の値はカンマで区切られます|
|`product_quantity`| 商品の数量を含みます。複数の値はカンマで区切られます|

### 注文確認

|ソース| 説明|
|---| ---|
|`order_id`| 注文またはトランザクションIDを含みます|
|`order_subtotal`| 注文の支払いタイプを含みます|
|`order_payment_type`| 注文の支払いタイプを含みます|
|`order_total`| 注文の合計値を含みます|
|`order_discount`| 注文の割引（ある場合）を含みます|
|`order_shipping`| 注文の送料を含みます|
|`order_tax`| 注文の税金額を含みます|
|`order_currency`| トランザクションに関連する通貨を含みます。例えば、USD'|
|`order_coupon_code`| 注文のクーポンコードを含みます|
|`order_type`| 注文/カートを含みます|
|`product_id`| 商品IDを含みます。複数の値はカンマで区切られます|
|`product_sku`| 商品SKUを含む; 複数の値はカンマで区切る|
|`product_name`| 商品名を含む; 複数の値はカンマで区切る|
|`product_brand`| 商品ブランドを含む; 複数の値はカンマで区切る|
|`product_category`| 商品カテゴリを含む; 複数の値はカンマで区切る|
|`product_subcategory`| 商品サブカテゴリを含む; 複数の値はカンマで区切る|
|`product_unit_price`| 商品の単価を含む; 複数の値はカンマで区切る|
|`product_quantity`| 商品の数量を含む; 複数の値はカンマで区切る|
|`customer_email`| 顧客のメールアドレスを含む|

### 顧客情報ページ

|ソース| 説明|
|---| ---|
|`customer_name`| 顧客のユーザー名を含む|
|`customer_email`| 顧客のメールアドレスを含む|
|`gender`| 敬称に基づく顧客の性別を含む|