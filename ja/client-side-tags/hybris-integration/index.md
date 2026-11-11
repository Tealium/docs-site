---
title: Hybris統合
description: この記事では、Hybris統合タグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/hybris-integration/
---
## 前提条件

* Tag Managementアカウント。
* B2C Commerce Acceleratorを含む、展開およびビルド済みのhybris v5.0.1以降。

## 定義

* Universal Data Object（UDO）＝キーと値のペアで構成されるデータレイヤーオブジェクト。   
 このオブジェクトは、グローバルJavaScriptオブジェクト`utag_data`としてページ内に生成されます。Tealiumの`utag.js`は、タグのベースデータレイヤーとして`utag_data`を使用します。
* Tealiumアカウント＝Tag Managementの購入時に割り当てられたアカウント。
* Tealiumプロファイル＝Webサイトに対応する特定のWebプロパティ名。

## アドオンのインストール

**GitHubリポジトリ**：`https://github.com/Tealium/integration-hybris`

1. `tealiumiqaddon`ディレクトリを`${HYBRIS_BIN}/custom`に配置します。このディレクトリは、リポジトリ内の`/hybris/bin/custom/`フォルダーにあります。
1. &lt;extension dir="$\{HYBRIS_BIN\}/custom/tealiumiqaddon"/\\&gt;を`config/localextensions.xml`に追加します。
1. 次のコマンドを使用して、`tealiumiqaddon`を`yacceleratorstorefront`に追加します。  
  - `sudo ant addoninstall -Daddonnames="tealiumiqaddon"  `
  - `DaddonStorefront.yacceleratorstorefront="yacceleratorstorefront"`
1. 次のファイルを更新します。  
  * `${HYBRIS_BIN\}/ext-template/yacceleratorstorefront/web/webroot/WEB-INF/tags/desktop/template/master.tag`では、次の内容を追加します。<br>ファイルの先頭に&lt;%@ taglib prefix="tealiumiqaddon" tagdir="/WEB-INF/tags/addons/tealiumiqaddon/shared/analytics" %&gt;<br>&lt;head&gt;タグの後に&lt;tealiumiqaddon:sync/&gt;<br>&lt;body&gt;タグの後に&lt;tealiumiqaddon:tealium/&gt;
  * `${HYBRIS_BIN}/custom/tealiumiqaddon/project.properties.template`では、次の内容を変更します。<br>**tealiumiqaddon.account**、**tealiumiqaddon.profile**、**tealiumiqaddon.target**を、Tag Managementアカウント固有の情報に変更します。<br>HTMLページの&lt;head&gt;に`utag.sync.js`を挿入する場合は、`tealiumiqaddon.utagSyncEnabled = 1`に変更します。この機能は任意であり、デフォルトでは無効になっています。

## カスタムデータの追加

デフォルトでは、このアドオンは標準的なEコマース変数の包括的なリストを提供します。これらのデフォルト値がインストール環境に十分でない場合は、デフォルトのページタイプを拡張したり、新しいカスタムページタイプを作成したりできます。

1. インターフェイス`com.tealium.dataconnector.hybris.HybrisDataConverter.HybrisCustomDataConverter`を実装する新しいクラスを作成し、インターフェイスのすべてのメソッドを実装します。  
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

1. インターフェイスのいずれのメソッドにも値を追加しない場合は、必ず`udo`オブジェクトを返してください。
```
@Override
public UDO homePage(UDO udo) {
	return udo;
}
```

1. デフォルトページの値を追加または変更するには、そのページのオーバーライドメソッドに処理を追加します。  
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

1. 値を含む新しいページタイプを追加するには、クラスに静的変数を追加し、`addCustomPages`メソッドに新しいページを追加します。
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

1. 次のファイルを変更します。   
 `${HYBRIS_BIN\}/custom/tealiumiqaddonweb/webroot/WEB-INF/tags/addons/tealiumiqaddon/shared/analytics/data.tag`
  * `CLASS_NAME`をクラス名（例：`TealiumCustomData`）に置き換えます。
  * 新しいクラスを追加します：&lt;%@ tag import="com.tealium.dataconnector.hybris. CLASS_NAME "%&gt;
  * 新しいクラスをHybrisDataConverterに登録します：&lt;%HybrisDataConverter.registerCustomDataClass("ID", new CLASS_NAME ()); %&gt;

## 完了

hybrisを再ビルドして再起動します。

* `sudo ant all`
* `sudo ./hybrisserver.sh`

## デフォルトのデータソース

### すべてのページ

|ソース|説明|
|---|---|
|`page_name`|ユーザーに分かりやすいページ名が格納されます|
|`site_region`|地域またはローカライズ版を示す値（例：`en_US`）が格納されます|
|`site_currency`|サイトに表示される通貨（例：`USD`）が格納されます|
|`page_type`|ユーザーに分かりやすいページタイプ（例：カートページ）が格納されます|

### 検索ページ

|ソース|説明|
|---|---|
|`search_results`|検索クエリによって返された結果の件数が格納されます|
|`search_keyword`|ユーザーが実行した検索クエリが格納されます|

### カテゴリページ

|ソース|説明|
|---|---|
|`page_category_name`|ユーザーに分かりやすいカテゴリ名（例：ホーム電）が格納されます|

### 商品ページ

|ソース|説明|
|---|---|
|`product_id`|商品IDが格納されます。複数の値はカンマで区切る必要があります|
|`product_sku`|商品のSKUが格納されます。複数の値はカンマで区切る必要があります|
|`product_name`|商品名が格納されます。複数の値はカンマで区切る必要があります|
|`product_brand`|商品のブランドが格納されます。複数の値はカンマで区切る必要があります|
|`product_category`|商品のカテゴリが格納されます。複数の値はカンマで区切る必要があります|
|`product_subcategory`|商品のサブカテゴリが格納されます。複数の値はカンマで区切る必要があります|
|`product_unit_price`|商品の単価が格納されます。複数の値はカンマで区切る必要があります|

### カートページ

|ソース|説明|
|---|---|
|`product_id`|商品IDが格納されます。複数の値はカンマで区切る必要があります|
|`product_sku`|商品のSKUが格納されます。複数の値はカンマで区切る必要があります|
|`product_name`|商品名が格納されます。複数の値はカンマで区切る必要があります|
|`product_brand`|商品のブランドが格納されます。複数の値はカンマで区切る必要があります|
|`product_category`|商品のカテゴリが格納されます。複数の値はカンマで区切る必要があります|
|`product_subcategory`|商品のサブカテゴリが格納されます。複数の値はカンマで区切る必要があります|
|`product_unit_price`|商品の単価が格納されます。複数の値はカンマで区切る必要があります|
|`product_quantity`|商品の数量が格納されます。複数の値はカンマで区切る必要があります|
### 注文確認

|ソース|説明|
|---|---|
|`order_id`|注文IDまたはトランザクションIDが含まれます|
|`order_subtotal`|注文の支払いタイプが含まれます|
|`order_payment_type`|注文の支払いタイプが含まれます|
|`order_total`|注文の合計金額が含まれます|
|`order_discount`|注文の割引額（該当する場合）が含まれます|
|`order_shipping`|注文の配送料が含まれます|
|`order_tax`|注文の税額が含まれます|
|`order_currency`|トランザクションに関連付けられた通貨（例：USD）が含まれます|
|`order_coupon_code`|注文のクーポンコードが含まれます|
|`order_type`|注文／カートが含まれます|
|`product_id`|商品IDが含まれます。複数の値はカンマで区切る必要があります|
|`product_sku`|商品SKUが含まれます。複数の値はカンマで区切る必要があります|
|`product_name`|商品名が含まれます。複数の値はカンマで区切る必要があります|
|`product_brand`|商品ブランドが含まれます。複数の値はカンマで区切る必要があります|
|`product_category`|商品カテゴリが含まれます。複数の値はカンマで区切る必要があります|
|`product_subcategory`|商品サブカテゴリが含まれます。複数の値はカンマで区切る必要があります|
|`product_unit_price`|商品の単価が含まれます。複数の値はカンマで区切る必要があります|
|`product_quantity`|商品の数量が含まれます。複数の値はカンマで区切る必要があります|
|`customer_email`|顧客のメールアドレスが含まれます|

### 顧客情報ページ

|ソース|説明|
|---|---|
|`customer_name`|顧客のユーザー名が含まれます|
|`customer_email`|顧客のメールアドレスが含まれます|
|`gender`|敬称に基づく顧客の性別が含まれます|