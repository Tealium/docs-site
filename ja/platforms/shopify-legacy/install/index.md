---
title: インストール
description: この記事では、Tealium Shopify（レガシー）統合でTealiumを使用するために、Shopifyテーマをカスタマイズする方法について説明します。
url: https://docs.tealium.com/ja/platforms/shopify-legacy/install/
---

<blockquote>
Tealiumは現在、Shopifyサイトでタグ管理を使用できるShopifyアプリをShopifyマーケットプレイスで提供しています。詳細については、[Tealium Shopifyアプリについて]()を参照してください。
</blockquote>


## 仕組み

ShopifyでTealiumを使用するには、Tealium Shopify（レガシー）統合のTealiumコードを使用するようにShopifyテーマをカスタマイズする必要があります。Tealiumコードはユニバーサルデータオブジェクト（UDO）を提供し、サイトの各ページで必要なTealiumアセットを読み込みます。

注文状況ページ用のコードスニペットは、チェックアウトの「Thank you」ページにも表示されます。このコードスニペットは、コンバージョントラッキング用のUDOを提供します。注文後に注文状況ページが再度閲覧される可能性があるため、コンバージョンが二重にトラッキングされないよう、タグ管理でロジックを構成することをお勧めします。

チェックアウトファネル全体で`utag.js`を読み込む`checkout.liquid`ファイルにアクセスできるのは、Shopify Plusのお客様のみです。現在、この統合はチェックアウトファネルをサポートしていません。ただし、他のページで使用されているパターンに従って、独自の`checkout.liquid`を実装できます。

## 構成手順

Tealium統合用にShopifyテーマをカスタマイズするには、次の手順を実行します。

1. [Tealium構成を有効にする](#enable-tealium-settings)。
1. [utag.jsとページ上のデータレイヤーをインストールする](#install-utagjs-and-on-page-data-layer)。
1. [注文状況ページ用のスクリプトをインストールする](#install-script-for-order-status-page)。
1. （Shopify Plusのお客様向け）[チェックアウトプロセス用のスクリプトをインストールする](#install-script-for-checkout-shopify-plus-only)。
<blockquote>
Shopifyは、2024年8月13日に`checkout.liquid`テーマファイルを廃止します。詳細については、[Shopify.devドキュメント：アップグレード](https://shopify.dev/docs/apps/checkout#upgrade)を参照してください。
</blockquote>


### Tealium構成を有効にする

次のJSONオブジェクトをコピーし、Shopifyテーマの[Config/settings_schema.json](https://help.shopify.com/themes/development/theme-editor/settings-schema)ファイル内のJSON配列に貼り付けます。このJSONオブジェクトにより、テーマのTealium固有の構成が有効になります。

```json
{
  "name": "Tealium",
  "settings": [
    {
      "type": "text",
      "id": "tealium_account",
      "label": "Account",
      "info": "Name of your acount"
    },
    {
      "type": "text",
      "id": "tealium_profile",
      "label": "Profile",
      "default": "main",
      "info": "Which profile to load your tags from",
      "placeholder": "main"
    },
    {
      "type": "text",
      "id": "tealium_environment",
      "label": "Environment",
      "default": "prod",
      "info": "Which environment to load your tags from",
      "placeholder": "prod"
    },
    {
      "type": "checkbox",
      "id": "tealium_enabled",
      "label": "Enable",
      "default": false,
      "info": "Check to enable Tealium"
    }
  ]
}
```

テーマをカスタマイズするときに、**一般構成**タブでTealium固有の構成を編集します。

### utag.jsとページ上のデータレイヤーをインストールする

次の手順に従って、Shopifyストアに`utag.js`をインストールし、ページ上のデータレイヤーを構成します。このプロセスでは、[Tealium Integration for Shopify GitHubリポジトリ](https://github.com/Tealium/integration-shopify)で提供されている特定のスニペットをShopifyテーマに追加します。これらのスニペットにより、ストア内のさまざまなページタイプでのトラッキングと分析に必要なユニバーサルデータオブジェクト（UDO）の実装が有効になります。

#### ステップ1 - テーマのコードにアクセスする

1. Shopifyアカウントにログインします。
1. **オンラインストア > テーマ**に移動し、現在のテーマを表示します。
1. 編集するテーマを見つけ、**アクション**ドロップダウンメニューをクリックして、**コードを編集**を選択します。または、テーマの**カスタマイズ**ボタンをクリックして、コードエディターに直接アクセスできます。

#### ステップ2 - UDO実装スニペットを追加する

1. [Tealium Integration for Shopify GitHubリポジトリ](https://github.com/Tealium/integration-shopify)にアクセスし、さまざまなページタイプでUDOを実装するために必要なコードスニペットをダウンロードします。
1. Shopifyテーマのコードエディターで、**スニペット**フォルダーをクリックして展開します。
1. GitHubリポジトリから適切なスニペットをドラッグし、Shopifyテーマエディターの**スニペット**フォルダーにドロップします。詳細については、[Shopify.devドキュメント：テーマスニペット](https://help.shopify.com/themes/development/templates#snippets)を参照してください。

#### ステップ3 - テンプレートでスニペットを参照する

1. スニペットを追加した後、**テンプレート**フォルダーをクリックして展開します。
1. 各ページタイプ（商品、ホーム、会社概要など）に対応するテンプレートについて、テンプレートファイルの先頭に関連するUDOスニペットへの参照を挿入します。これらの参照により、ページタイプごとにデータレイヤーが正しく初期化されます。
  
    たとえば、商品ページにデータレイヤーを統合するには、次のように`product.liquid`テンプレートを編集します。
    * `product.liquid`ファイルの先頭に次の行を追加し、先ほど**スニペット**フォルダーに追加した`product_udo`スニペットを組み込みます。

      ```liquid
      {% include 'product_udo' %}
      ```

    * 他のスクリプトが実行される前にデータレイヤーが初期化されるように、この行はテンプレートファイル内の既存のコンテンツより前に配置する必要があります。`product_udo`スニペットを組み込んだ後の`product.liquid`テンプレートは、次のようになります。

      ```liquid
      {% include 'product_udo' %}

      {% comment %}
        The contents of the product.liquid template can be found in /sections/product-template.liquid
      {% endcomment %}

      {% section 'product-template' %}

      <script>
        // Override default values of shop.strings for each template.
        // Alternate product templates can change values of
        // add to cart button, sold out, and unavailable states here.
        theme.productStrings = {
          addToCart: {{ 'products.product.add_to_cart' | t | json }},
          soldOut: {{ 'products.product.sold_out' | t | json }},
          unavailable: {{ 'products.product.unavailable' | t | json }}
        }
      </script>
      ```

    * 異なるページタイプに対応する各テンプレートについて、`product_udo`の代わりに適切なスニペット名を使用して、このプロセスを繰り返します。通常、スニペット名と対応するテンプレート名はよく似ていますが、スニペット名には`_udo`サフィックスが付きます。例：
      * `index.liquid`テンプレート（ホームページ）には、`home_udo`スニペットを組み込みます。
      * `404.liquid`などの汎用テンプレートには、幅広く対応できるように`page_udo`スニペットを使用します。
      詳細については、[Shopify.devドキュメント：テーマアーキテクチャ](https://help.shopify.com/themes/development/templates)を参照してください。
1. テンプレートに`include`ステートメントを追加した後、**保存**をクリックして変更を適用します。
1. 変更を確認するには、Webブラウザーで開発者コンソールを開き、`utag.data`を調べます。
### 注文状況ページへのスクリプトのインストール

他のページとは異なり、注文状況ページからは管理構成にアクセスできないため、Tealiumアカウント情報を再構成する必要があります。次の手順に従って構成を定義します。

1. Shopify管理画面で、**構成**をクリックしてから**チェックアウト**をクリックします。
1. **チェックアウト**構成で、ページ下部付近にある**注文状況ページ**までスクロールします。
1. **追加スクリプト**に、次のコードを追加します。

    ```liquid
    <script>
      {
        "product_price": [
        {% for line_item in checkout.line_items %}
          "{{ line_item.price | money_without_currency }}"{% unless forloop.last %},{% endunless %}
        {% endfor %}
        ],
        "product_name": [
        {% for line_item in checkout.line_items %}
          "{{ line_item.title }}"{% unless forloop.last %},{% endunless %}
        {% endfor %}
        ],
        "product_sku": [
        {% for line_item in checkout.line_items %}
          "{{ line_item.sku }}"{% unless forloop.last %},{% endunless %}
        {% endfor %}
        ],

        "page_name": "{{ page_title }}",
        "language_code": "{{ shop.locale }}",

        {% if customer %}
          "customer_logged_in": "true",
          "customer_id": "{{ customer.id }}",
          "customer_email": "{{ customer.email }}",
          "customer_first_name": "{{ customer.first_name }}",
          "customer_last_name": "{{ customer.last_name }}",

          {% if customer.default_address %}
            "country_code": "{{ customer.default_address.country_code }}",
          {% endif %}

        {% else %}
          "customer_loggedin": "false",
        {% endif %}

        {% if cart %}
          "cart_total_items": "{{ cart.item_count }}",
          "cart_total_value": "{{ cart.total_price | money_without_currency }}",
        {% endif %}

        "page_type": "order"
      }
    </script>

    <!-- Loading script asynchronously -->
    <script type="text/javascript">
        (function(a,b,c,d){
        a='//tags.tiqcdn.com/utag/{{ settings.tealium_account }}/{{ settings.tealium_profile }}/{{ settings.tealium_environment }}/utag.js';
        b=document;c='script';d=b.createElement(c);d.src=a;d.type='text/java'+c;d.async=true;
        a=b.getElementsByTagName(c)[0];a.parentNode.insertBefore(d,a);
        })();
    </script>
    {% else %}
    <!-- Configure your Tealium account information for the order confirmation page. -->
    {% endif %}
    ```

    詳細については、[Shopifyヘルプセンター：注文状況ページ](https://help.shopify.com/themes/customization/order-status)を参照してください。

1. `tealium_enabled`を`true`に構成します。
1. `tealium_account`、`tealium_profile`、`tealium_environment`変数を、構成で構成した内容と一致するように構成します。

### チェックアウトへのスクリプトのインストール（Shopify Plusのみ）

この手順は、`checkout.liquid`ファイルを使用してチェックアウトファネル全体に`utag.js`を統合するShopify Plusのお客様を対象としています。

#### `checkout.liquid`へのアクセス

* **Shopify Plusのお客様**：`checkout.liquid`ファイルにまだアクセスできない場合は、アクセス権をリクエストできます。このファイルは、チェックアウト処理中に`utag.js`を読み込みます。このファイルを以前に変更したことがない場合は、インストールを続行する前にShopifyサポートへ連絡してアクセス権を取得する必要があります。
* **Shopify Plus以外のお客様**：Shopifyサポートは、Shopify Plusアカウントをお持ちでないお客様に`checkout.liquid`ファイルへのアクセス権を付与しません。この制限により、チェックアウトページに`utag.js`スクリプトをインストールすることはできません。ただし、前述の手順を完了することで、ショッピングカートや注文確認ページなど、その他の重要なページには`utag.js`がインストールされます。

#### インストール手順

1. `checkout_udo.liquid`ファイルを開きます。
2. 10行目のプレースホルダーを、Tag Managementのアカウント情報とプロファイル情報に置き換えます。
3. 変更した内容をコピーし、ShopifyのチェックアウトLiquidファイルに貼り付けます。
4. 変更を保存し、統合が想定どおりに機能することをテストで確認します。


<blockquote>
このチェックアウトコードは、基本テンプレートとして機能します。最適なパフォーマンスを実現するために、Shopifyサイト固有の要件や構成に応じたカスタマイズが必要になる場合があります。
</blockquote>


## リリースノート

#### 1.0.2

* 統合の機能がより明確に伝わるように、`README`を更新しました。
* より多くのデータと分かりやすい変数名を含めるように、`order_status`スニペットを更新しました。
* 機能をより適切に表すため、checkout.liquidの名前を`order_status.liquid`に変更しました。

#### 1.0.1

* global_udo_varsスニペット内の変数名のスペルミスを修正しました。`customer_loggedin`を`customer_logged_in`に置き換えました。

#### 1.0.0 初回リリース

* Tealiumと統合するためにShopifyテーマをカスタマイズする際に必要な、すべてのスニペットと構成。
* テーマをカスタマイズするための手順。

## ライセンス

本ソフトウェアの使用には、[LICENSE.txt](https://github.com/Tealium/integration-shopify/blob/master/LICENSE.txt)ファイルに記載されているライセンス契約の条件が適用されます。このリポジトリに含まれるファイルをダウンロードまたは使用する前に、ライセンスをお読みください。これらのファイルをダウンロードまたは使用することにより、ライセンス契約に拘束され、その条件を遵守することに同意したものとみなされます。