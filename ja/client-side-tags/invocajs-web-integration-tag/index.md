---
title: InvocaJS Web統合タグ構成ガイド
description: この記事では、TealiumアカウントでInvocaJS Web統合タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/invocajs-web-integration-tag/
---## タグのヒント

* Invoca Network IDとTag IDは厳密に数値です。
* カスタムマーケティングデータを維持するためにマッピングを使用します。
* タグに変数をマッピングした後、Invocaユーザーインターフェースに対応するマーケティングデータフィールドを追加します：
  * マーケティングデータフィールドを追加するために、Invocaの担当者に連絡してください。
  * マーケティングデータフィールド名はデータマッピングと一致する必要はありません。
  * データソースタイプは次のようになります：**JavaScriptデータレイヤー**
  * データソース名は次のようになります：`localStorage.getItem(&#34;inv_TEALIUM_MAPPING&#34;)`  
`TEALIUM_MAPPING`はあなたのカスタムデータマッピングの名前と一致する必要があります。

## タグの構成

タグマーケットプレイスに移動して新しいタグを追加します。タグを追加する一般的な手順については、[タグ概要]()の記事を読んでください。

タグを追加する際、以下の構成を構成します：

* **Invoca Network ID**
  * Invoca Network IDは、あなたのInvocaネットワーク（アカウント）に割り当てられたユニークなIDです。
* **Invoca Tag ID**
  * Invoca Tag IDは、あなたのInvocaネットワーク内で作成する各タグに割り当てられたユニークなIDです。
* **データセンター**：データセンターリージョンは、どのInvocaコンテンツ配信ネットワーク（CDN）がタグを提供するかを決定します。

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。タグ宛先に変数をマッピングする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。
