---
title: エンドポイント構成の更新
description: この記事では、ファーストパーティドメインを構成した後にエンドポイント構成を更新する方法について説明します。
url: https://docs.tealium.com/ja/iq-tag-management/administration/first-party-domains/update-endpoints/
---
ファーストパーティドメインの構成と検証が完了した後、Tealium iQタグ管理および[Tealium Collect]()でファーストパーティドメインを使用するために、エンドポイント構成を更新する必要があります。


<blockquote>
この記事の情報は、ファーストパーティドメインを使用して作成されたCNAMEおよびAレコードにのみ適用されます。
</blockquote>


## タグ管理

Tealium iQタグ管理でファーストパーティドメインを使用するには、以下の変更を行う必要があります：

* Universal Tag (`utag.js`) のコードスニペットをインストールされているすべての場所で更新します。
* パブリッシングURLを構成します。


<blockquote>
Tealiumの環境スイッチャーはファーストパーティドメインをサポートしています。ただし、環境スイッチャーの**Basic**オプションはファーストパーティドメインでは機能しません。**Advanced**タブの**URLリダイレクト**オプションを使用してください。詳細については、[Tealium Tools: Environment Switcher](https://docs.tealium.com/ja/iq-tag-management/tealium-tools/environment-switcher/)を参照してください。
</blockquote>


### ユニバーサルタグのローディングスクリプトを更新

ユニバーサルタグのコードスニペットを更新するには、以下の手順に従います：

1. 管理メニューで**Code Center**をクリックします。
1. **Choose Domain**の下で、ファーストパーティドメインを選択します。  
    ![](https://docs.tealium.com/images/iq-tag-management/first-party-data-code-center.png)

例のコードスニペットは、ファーストパーティドメインを使用するように更新されます。

ファーストパーティドメインの現行バージョンでは、UniversalタグのURLにはプロファイル名と環境のみがパスに含まれ、アカウント名と`utag`部分は省略されます。

ファーストパーティドメインの以前のバージョンや、ほとんどの他のシナリオでは、アカウント名と`utag`部分が含まれます。例えば：

`https://tags.tiqcdn.com/utag/example-account/example-profile/prod/utag.js`

ファーストパーティドメインの現行バージョンの次のコードスニペット例では、`tags.tealiumecommerce.com/ecomm/prod`のコードスニペットが次のようになります：


```
<!-- 非同期でスクリプトをロード -->
<script type="text/javascript">
    (function(a,b,c,d){
    a='**https://tags.tealiumecommerce.com/ecomm/prod/utag.js**';
    b=document;c='script';d=b.createElement(c);d.src=a;d.type='text/java'+c;d.async=true;
    a=b.getElementsByTagName(c)[0];a.parentNode.insertBefore(d,a);
    })();
</script>
```

### パブリッシングURLを更新


<blockquote>
プロファイルに複数のファーストパーティドメインが構成されている場合は、[プロファイルに複数のファーストパーティドメインがある場合のパブリッシングURLの更新](#update-publishing-urls-when-a-profile-has-multiple-first-party-domains)を参照して、パブリッシングURLを更新する方法についての情報をご覧ください。
</blockquote>


パブリッシングURLは、各デフォルト環境の追加の`utag.#.js`ファイルをロードする場所を決定します。パブリッシングURLが更新されていない場合、`utag.js`の後にロードされるベンダータグファイルはドメインから発信されません。

パブリッシングURLを構成するには、次の手順を使用します：

1. 管理メニューで**Configure Publish Settings**をクリックします。
1. **Publishing URLs**までスクロールダウンし、ファーストパーティドメインを使用する各環境のURLを入力します。例えば、`tags.example.com`や`collect.example.com`です。
    ![](https://docs.tealium.com/images/iq-tag-management/first-party-domains-publishing-urls.png)  
    **Publish Dev URL**: `//sub.your_domain.com/your_profile/dev/`  
    **Publish QA URL**: `//sub.your_domain.com/your_profile/qa/`  
    **Publish Prod URL**: `//sub.your_domain.com/your_profile/prod/`
1. **Save**をクリックします。
1. 保存して公開します。

### プロファイルに複数のファーストパーティドメインがある場合のパブリッシングURLの更新

プロファイルに複数のファーストパーティドメインが構成されている場合、クライアント側のメニューからパブリッシングURLを更新することはできません。

パブリッシングURLを更新するために、以下のようなスクリプトを追加する必要があります。例のパスをページに適切なパスに置き換えてください（これは同時に更新される`utag.js`の含まれるパスと一致します）。このスクリプトは`utag.js`のURLを指定するスクリプトの前に追加する必要があります。

```
<script>
window.utag_cfg_ovrd = window.utag_cfg_ovrd || {} ;
window.utag_cfg_ovrd.path = '//tags.example.com/main/prod/'
</script>
```

詳細については、[Settings](https://docs.tealium.com/platforms/javascript/settings/)を参照してください。

## Tealium Collectエンドポイントの更新

Tealium EventStream API HubまたはTealium AudienceStream CDPでファーストパーティドメインを使用するには、Tealium Collectのインストール時にデータ収集URLを更新する必要があります。ウェブサイトの場合、これには[Tealium Collectタグ]()の**Tealium Collectエンドポイント**フィールドを構成することが含まれます。ビジターサービスを使用する場合は、ビジターサービスオーバーライドも提供する必要があります。

Tealium Collectタグを更新するには、次の手順を使用します：

1. **Tags**に移動し、Tealium Collectタグを展開します。
1. **Tealium Collectエンドポイント**フィールドに、ファーストパーティドメインエンドポイントを入力します。  
例：`sub.your_domain.com/your_account/your_profile/2/i.gif`
1. **Visitor Service Override**フィールドに、ビジターサービスURLを入力します。プロトコルとパスは省略します。例：`your-visitor-service.example.com`
1. **Apply**をクリックします。


<blockquote>
サブドメインごとに別々のCollectタグを使用する必要があります。値を動的にマッピングするための拡張機能が使用されない限り。
</blockquote>

