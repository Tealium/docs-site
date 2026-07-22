---
title: PulsePoint HCP365ピクセルタグ構成ガイド
description: この記事では、PulsePoint HCP365ピクセルタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/pulsepoint-hcp365-tag/
---
HCP365は、Signalプラットフォームの最初のセルフサービス製品で、HCPオーディエンスがNPIレベルでブランドのデジタルタッチポイントにどのように、いつ自然に関与するかを明らかにします。HCP365ピクセルは、ページレベルの情報をPulsePointシステムに送信します。

## タグのヒント

*  標準パラメータを上書きするためにマッピングを使用します。

## タグの構成

タグマーケットプレイスに移動して新しいタグを追加します。タグの追加方法については、[タグの概要](https://docs.tealium.com/about-tags/)の記事を参照してください。

タグを追加する際には、以下の構成を行います：

*  **PulsePointコンテナピクセル**：各クライアントに固有のPulsePointコンテナピクセル
*  **トークン**：ブランドのPulsePoint内部識別子（例：Merck広告主は複数のブランドを持っているため、複数のトークンがあります）

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。ロードルールについての詳細は、[ロードルール](https://docs.tealium.com/about-load-rules/)のドキュメンテーションを参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

| 変数 | 説明 |
| --- | --- |
| PulsePointコンテナピクセル (`p`) | `String` |
| トークン (`token`) | `String` |
| ベースURL (`base_url`) | `String` |
| CCPAオプトアウト (`us_privacy`) (必須) | `String` |
| タグが発火されたページのURL (`url`) (必須) | `String` |
| ページのリファラー (`rr`) (必須) | `String` |
| ピクセルに追加情報を渡すための追加パラメータ (`param1`) | `String` |
| ピクセルに追加情報を渡すための追加パラメータ (`param2`) | `String` |
| ピクセルに追加情報を渡すための追加パラメータ (`param3`) | `String` |
| ピクセルに追加情報を渡すための追加パラメータ (`param4`) | `String` |
| ピクセルに追加情報を渡すための追加パラメータ (`param5`) | `String` |
| タグがフォーム送信時に発火する場合のフォーム詳細 (`frmtext`) | `String` |
| クリックされたリンクのテキストまたはダウンロードされたドキュメントの名前 (`clktext`) | `String` |

