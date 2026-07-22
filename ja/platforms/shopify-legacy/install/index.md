---
title: インストール
description: この記事では、Tealium Shopifyインテグレーションを使用してShopifyテーマをカスタマイズし、Tealiumを使用する方法について説明します。
url: https://docs.tealium.com/ja/platforms/shopify-legacy/install/
---

<blockquote>
Tealium Shopifyインテグレーションは現在、Shopifyバージョン2.0をサポートしていません。代わりに、Webピクセルを使用してサーバーサイドに直接ネットワークリクエストを送信するために、[Tealium Shopify アプリ](https://docs.tealium.com/ja/platforms/shopify/)を使用することができます。
</blockquote>


## 動作原理

ShopifyでTealiumを使用するには、Shopifyテーマをカスタマイズして、Tealium Shopifyインテグレーションと共にTealiumコードを使用する必要があります。Tealiumコードは、Universal Data Object（UDO）を提供し、サイトの各ページで必要なTealiumアセットを読み込みます。

注文ステータスページのコードスニペットは、チェックアウトの「ありがとうございます」ページにも表示されます。コードスニペットは、コンバージョン追跡のためのUDOを提供します。注文ステータスページは注文後に再訪される可能性があるため、2回のコンバージョン追跡を行わないようにするために、Tealium iQタグ管理でロジックを設定することをお勧めします。

`checkout.liquid`ファイルをロードするShopify Plusの顧客のみが`checkout.liquid`ファイルにアクセスできます。このインテグレーションは現在、チェックアウトフローをサポートしていません。ただし、他のページで使用されているパターンに従って独自の`checkout.liquid`を実装することができます。

## セットアップ手順

TealiumインテグレーションのためにShopifyテーマをカスタマイズするには、次の手順に従ってください：

1. [Tealium設定を有効にする](#enable-tealium-settings)。
1. [utag.jsとオンページデータレイヤーをインストールする](#install-utagjs-and-on-page-data-layer)。
1. [注文ステータスページのスクリプトをインストールする](#install-script-for-order-status-page)。
1. （Shopify Plusの顧客向け）[チェックアウトプロセスのスクリプトをインストールする](#install-script-for-checkout-shopify-plus-only)。
<blockquote>
Shopifyは2024年8月13日に`checkout.liquid`テーマファイルを廃止する予定です。詳細については、[Shopify.devドキュメント：アップグレード](https://shopify.dev/docs/apps/checkout#upgrade)を参照してください。
</blockquote>


### Tealium設定を有効にする

次のJSONオブジェクトをShopifyテーマの[Config/settings_schema.json](https://help.shopify.com/themes/development/theme-editor/settings-schema)ファイルのJSON配列にコピーして貼り付けます。このJSONオブジェクトにより、テーマのTealium固有の設定が有効になります。

```json
{
  "name": "Tealium",
  "settings": [
    {
      "type": "text",
      "id": "tealium_account",
      "label": "アカウント",
      "info": "アカウント名"
    },
    {
      "type": "text",
      "id": "tealium_profile",
      "label": "プロファイル",
      "default": "main",
      "info": "どのプロファイルからタグを読み込むか",
      "placeholder": "main"
    },
    {
      "type": "text",
      "id": "tealium_environment",
      "label": "環境",
      "default": "prod",
      "info": "どの環境からタグを読み込むか",
      "placeholder": "prod"
    },
    {
      "type": "checkbox",
      "id": "tealium_enabled",
      "label": "有効にする",
      "default": false,
      "info": "Tealiumを有効にするにはチェックを入れます"
    }
  ]
}
```

テーマをカスタマイズする際に、**一般設定**タブでTealium固有の設定を編集します。

### utag.jsとオンページデータレイヤーをインストールする

Shopifyストアに`utag.js`をインストールし、オンページデータレイヤーを設定するには、次の手順に従ってください。このプロセスでは、[Tealium Integration for Shopify GitHubリポジトリ](https://github.com/Tealium/integration-shopify)で提供される特定のスニペットをShopifyテーマに追加する必要があります。これらのスニペットにより、ストア内のさまざまなページタイプでのトラッキングと分析に必要なUniversal Data Object（UDO）の実装が可能になります。

#### ステップ1 - テーマのコードにアクセスする

1. Shopifyアカウントにログインします。
1. **オンラインストア > テーマ**に移動して現在のテーマを表示します。
1. 編集したいテーマを見つけ、**アクション**ドロップダウンメニューをクリックし、**コードを編集**を選択します。または、テーマの**カスタマイズ**ボタンをクリックしてコードエディタに直接アクセスすることもできます。

#### ステップ2 - UDO実装スニペットを追加する

1. [Tealium Integration for Shopify GitHubリポジトリ](https://github.com/Tealium/integration-shopify)にアクセスして、さまざまなページタイプに対するUDO実装のための必要なコードスニペットをダウンロードします。
1. Shopifyテーマのコードエディタで、**スニペット**フォルダをクリックして展開します。
1. GitHubリポジトリから適切なスニペットをShopifyテーマエディタの**スニペット**フォルダにドラッグアンドドロップします。詳細については、[Shopify.devドキュメント：テーマスニペット](https://help.shopify.com/themes/development/templates#snippets)を参照してください。

#### ステップ3 - テンプレートでスニペットを参照する

1. スニペットを追加した後、**テンプレート**フォルダをクリックして展開します。
1. 各テンプレートに対応するテンプレートに、関連するUDOスニペットへの参照をテンプレートファイルの先頭に挿入します。これらの参照により、各ページタイプのデータレイヤーが正しく初期化されます。

    たとえば、データレイヤーを製品ページに統合するには、`product.liquid`テンプレートを次のように編集します：
    * `product.liquid`ファイルの先頭に、**スニペット**フォルダに追加した`product_udo`スニペットを含めるために、次の行を追加します：

      ```liquid
      {% include 'product_udo' %}
      ```

    * この行は、テンプレートファイル内の既存のコンテンツの前に配置する必要があります。これにより、他のスクリプトが実行される前にデータレイヤーが初期化されます。`product.liquid`テンプレートは、`product_udo`スニペットを含めた後、次のようになります：

      ```liquid
      {% include 'product_udo' %}

      {% comment %}
        product.liquidテンプレートの内容は/sections/product-template.liquidにあります
      {% endcomment %}

      {% section 'product-template' %}

      <script>
        // 各テンプレートのshop.stringsのデフォルト値をオーバーライドします。
        // 代替製品テンプレートでは、カートに追加ボタン、売り切れ、利用できない状態の値を変更できます。
        theme.productStrings = {
          addToCart: {{ 'products.product.add_to_cart' | t | json }},
          soldOut: {{ 'products.product.sold_out' | t | json }},
          unavailable: {{ 'products.product.unavailable' | t | json }}
        }
      </script>
      ```

    * 異なるページタイプに対応する各テンプレートに対してこのプロセスを続け、`product_udo`の代わりに適切なスニペット名を使用します。一般的に、スニペットの名前とそれに対応するテンプレートの名前は似ており、スニペット名には`_udo`の接尾辞はありません。たとえば：
      * ホームページである`index.liquid`テンプレートの場合、`home_udo`スニペットを含めます。
      * `404.liquid`のような汎用テンプレートの場合、広範なカバレッジを確保するために`page_udo`スニペットを使用します。詳細については、[Shopify.devドキュメント：テーマアーキテクチャ](https://help.shopify.com/themes/development/templates)を参照してください。
1. テンプレートに`include`ステートメントを追加した後、**保存**をクリックして変更を適用します。
1. 変更が正常に適用されていることを確認するために、Webブラウザで開発者コンソールを開き、`utag.data`を検査します。

### 注文ステータスページのスクリプトをインストールする

他のページとは異なり、注文ステータスページには管理設定へのアクセス権がありませんので、Tealiumアカウント情報を再設定する必要があります。次の手順に従ってこれらの設定を定義します：

1. Shopify管理画面から**設定**をクリックし、**チェックアウト**をクリックします。
1. **チェックアウト**設定で、ページの一番下にある**注文ステータスページ**までスクロールします。
1. **追加スクリプト**に次のコードを追加します：

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

    <!-- スクリプトを非同期で読み込む -->
    <script type="text/javascript">
        (function(a,b,c,d){
        a='//tags.tiqcdn.com/utag/{{ settings.tealium_account }}/{{ settings.tealium_profile }}/{{ settings.tealium_environment }}/utag.js';
        b=document;c='script';d=b.createElement(c);d.src=a;d.type='text/java'+c;d.async=true;
        a=b.getElementsByTagName(c)[0];a.parentNode.insertBefore(d,a);
        })();
    </script>
    {% else %}
    <!-- 注文確認ページのTealiumアカウント情報を設定してください。 -->
    {% endif %}
    ```

    詳細については、[Shopifyヘルプセンター：注文ステータスページ](https://help.shopify.com/themes/customization/order-status)を参照してください。

1. `tealium_enabled`を`true`に設定します。
1. `tealium_account`、`tealium_profile`、および`tealium_environment`の変数を設定で構成した内容に合わせて設定します。

### チェックアウトのスクリプトをインストールする（Shopify Plusのみ）

この手順は、`checkout.liquid`ファイルを使用してチェックアウトフロー全体に`utag.js`を統合したいShopify Plusの顧客向けです。

#### `checkout.liquid`にアクセスする

* **Shopify Plusの顧客**：すでにアクセスできない場合は、`checkout.liquid`ファイルへのアクセスをリクエストすることができます。このファイルはチェックアウトプロセス中に`utag.js`をロードします。このファイルを以前に変更していない場合は、インストールを進める前にShopifyサポートに連絡してアクセスを取得する必要があります。
* **Shopify Plus以外の顧客**：Shopifyサポートは、Shopify Plusアカウントを持たない顧客には`checkout.liquid`ファイルへのアクセス権限を付与しません。この制限により、チェックアウトページなどの重要なページには`utag.js`がインストールされません。ただし、前の手順を完了することで、ショッピングカートや注文確認ページなど、他の重要なページに`utag.js`がインストールされることが保証されます。

#### インストール手順

1. `checkout_udo.liquid`ファイルを開きます。
2. 10行目のプレースホルダーをTealium iQアカウントとプロファイル情報で置き換えます。
3. 変更したコンテンツをコピーし、Shopifyのチェックアウトリキッドファイルに貼り付けます。
4. 変更内容を保存し、統合が正常に機能するかテストします。


<blockquote>
このチェックアウトコードは基本的なテンプレートとして機能します。Shopifyサイトの特定の要件とセットアップに応じて、最適なパフォーマンスを得るためにカスタマイズが必要な場合があります。
</blockquote>


## リリースノート

#### 1.0.2

* インテグレーションの機能をより明確に反映するように`README`を更新しました。
* `order_status`スニペットを更新して、より多くのデータとより良い変数名を含めました。
* 機能をよりよく反映するために、`checkout.liquid`を`order_status.liquid`に名前を変更しました。

#### 1.0.1

* `global_udo_vars`スニペットの変数名のスペルミスを修正しました。`customer_loggedin`を`customer_logged_in`に置き換えました。

#### 1.0.0 初版リリース

* ShopifyテーマをカスタマイズしてTealiumを統合するために必要なすべてのスニペットと設定。
* テーマのカスタマイズ手順。

## ライセンス

このソフトウェアの使用は、このリポジトリに含まれるファイルのライセンス契約の条件と規定に従うものとします。ファイルをダウンロードまたは使用する前に、ライセンスをお読みください。これらのファイルのいずれかをダウンロードまたは使用することにより、ライセンス契約に拘束され、その契約を遵守することに同意したものとみなされます。
