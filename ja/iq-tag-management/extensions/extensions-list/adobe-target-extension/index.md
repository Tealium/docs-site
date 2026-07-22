---
title: Adobe Target 拡張機能
description: Adobe Target 拡張機能を使用すると、Tealium iQを通じてAdobe Targetタグによってロードされるテストを制御できます。この記事では、Tealium iQアカウントでAdobe Target拡張機能を構成する方法について説明します。
url: https://docs.tealium.com/ja/iq-tag-management/extensions/extensions-list/adobe-target-extension/
---

<blockquote>
現在、お使いのウェブサイトがAdobe Test & Target拡張機能とタグを使用している場合、Adobe Targetを実装する前に特別な考慮が必要です。[Adobe Test & Targetからの移行](#migration)のセクションをご覧ください。
</blockquote>


## 拡張機能の追加と構成

![](https://docs.tealium.com/images/iq-tag-management/tealium-iq---tag-management.png)

1. **タイトル:** これはTealium固有のフィールドです。拡張機能を特定しやすくするために、説明的なタイトルを入力してください。特に同じ拡張機能の複数のインスタンスを持っている場合はそうです。
1. **スコープ:** この拡張機能のスコープを**Adobe Target**に構成する必要があります。
1. **要素タイプ:** **DOM ID**または**xPath**のいずれかを選択します。ページの構造が変更されるとxPath識別子が変更される可能性があるため、要素を識別するにはDOM IDの使用を推奨します。  
    
<blockquote>
ページで要素が見つからない場合、タグはmboxへの呼び出しをトリガーしません。
</blockquote>


1. **識別子:** ここに要素のDOM IDまたはxPath識別子の値を入力します。
1. **Mod位置:** 識別した要素に関連して新しいコンテンツを配置したい場所を指定します：
    * **ノードの前に**: 識別した要素の前にコンテンツを配置します。
    * **ノードの後に**: 識別した要素の後にコンテンツを配置します。
    * **ノードの始まりに**: 識別した要素の始まりにコンテンツを配置します。
    * **ノードの終わりに**: 識別した要素の終わりにコンテンツを配置します。
    * **ノードのコンテンツを置き換える**: 要素のコンテンツを置き換えます。
    * **ノードを置き換える**: 要素全体を置き換えます。
    * **ノードのコンテンツを置き換える（デフォルトを残す）**: 要素のコンテンツを置き換えますが、AdobeのTargetサービスが一時的に利用できない場合は、テストコンテンツの代わりにデフォルトのコンテンツが表示されます。Flicker Free機能を使用する場合は、このMod位置を選択する必要があります。  
    
<blockquote>
ほとんどの場合、**Mod位置**オプションを**ノードのコンテンツを置き換える（デフォルトを残す）**に構成し、そのままにすることをお勧めします。
</blockquote>


1. **mBox Div ID:** テストのmBox IDを入力します。Adobeがこれを提供します。
1. **静的パラメーター:** このフィールドに静的パラメーターをクエリ文字列形式で追加できます。つまり、それらをアンパサンド(`&`)で区切ります。
1. **条件:** 拡張機能がコンテンツを変更するタイミングと場所を決定する論理ステートメントを作成します。

拡張機能の構成の右上隅にあるプラスボタンをクリックして、コンテンツ変更エントリを追加します。代わりに拡張機能を複製することもできますが、この拡張機能のすべてのエントリが拡張機能のロード条件を共有するため、1つの拡張機能に複数のエントリを保持する方がすっきりします。

### utag.sync.jsの要件

Tealium iQで実装された多くのA/Bテストツールと同様に、Adobe Targetは`utag.js`の同期バージョンである`utag.sync.js`の使用を必要とします。Adobe Target拡張機能を追加すると、プロファイルの[公開構成]()で**utag.sync.jsファイルを生成する**オプションが自動的にオンになります。すでにページの`<head>`セクションで`utag.sync.js`を使用している場合は、それ以上のアクションは必要ありません。そうでない場合は、Code Centerで生成されたutagコードを更新する必要があります。

詳細については、[utag.sync.jsの使用]()および[Code Centerへのアクセス]()に関する記事をご覧ください。

## Adobe Enterprise Cloudの使用

Adobe Enterprise CloudをAdobe Targetと併用するお客様は、Adobe Enterprise CloudのタグがAdobe Targetのタグより先にロードされる必要があることに注意してください。Adobe Enterprise Cloudの使用はオプションです。

## Adobe Test and Targetからの移行

Tealium iQで以前利用可能だったAdobe Test & Targetソリューションの完全な代替として、Adobe Targetタグと拡張機能が導入されました。既存のAdobe Test & Target実装からAdobe Targetへの移行にあたって考慮すべき事項のリストは次のとおりです。

### Adobe Test and Targetとの互換性

Adobe TargetとTest & Targetのタグは同じプロファイル上で共存することができます。ただし、それぞれが独自の拡張機能を使用する必要があります。

## タグと拡張機能の可用性の変更

### タグ

以前はタグマーケットプレイスで「Adobe Target (async)」および「Adobe Target (sync)」としてラベル付けされていたAdobe Test & Targetタグは、Adobe Targetのリリースにより非推奨となり、タグマーケットプレイスでは単に**Adobe Target**と呼ばれる単一のタグに置き換えられました。Tealium iQプロファイルに残っているTest & Targetタグは、Adobe Test & Target拡張機能がそのプロファイルでアクティブである限り、引き続きアクティブで機能し続けます。

### 拡張機能

Test & Target拡張機能は、Adobe Target拡張機能と並行して拡張機能マーケットプレイスで提供され続けますが、Test & Targetタグ専用に機能します。ただし、両方の拡張機能を同時にアクティブにすることはできません。詳細は、次の移行手順のセクションをご覧ください。

## 移行手順の順序

Adobe Test & TargetからAdobe Targetへの実装に切り替えるには、次の手順を順番に実行する必要があります：

1. Tealium iQプロファイルでTest & Target拡張機能を非アクティブ化します。
1. タグマーケットプレイスからAdobe Targetタグを追加します。
1. 拡張機能マーケットプレイスからAdobe Target拡張機能を追加し、新しいAdobe Targetタグに拡張機能のスコープを構成してください。
1. この時点で、Tealium iQプロファイルにあるAdobe Test & Targetタグを削除することができます。Test & Target拡張機能なしでは機能しなくなるためです。
