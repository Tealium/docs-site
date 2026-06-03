---
title: UserWayタグの構成
description: この記事では、Tealium iQタグ管理アカウントでUserWayタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/userway-tag/
---
UserWayは、ウェブサイトの既存のコードをリファクタリングすることなくADA準拠を確保するための高度なウェブサイトアクセシビリティソリューションを作成します。UserWayのRaaS™とTealiumを使用すると、ユーザーはWCAG 2.1、ADA、ATAG 2.0、EN 301-549、およびセクション508の規制に簡単に準拠することができます。これらは、米国および国際的な政府機関および規制機関が必要とするものです。

## タグのヒント

* マッピングを使用してタグの構成を上書きまたは動的に構成します。

## タグの構成

新しいタグを追加するためにタグマーケットプレイスに移動します。タグの追加方法については、[タグの概要]()の記事を参照してください。

タグを追加する際には、以下の構成を行います：

* **Data-account**: シングルテキストフィールド

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。ロードルールについての詳細は、[ロードルール]()のドキュメンテーションを参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 共通

|変数| 説明|
|---| ---|
|UserWay APIバージョンを取得。| `(getVersion)`|
|UserWayアクセシビリティメニューアイコンを表示。| `(iconVisibilityOn)`|
|UserWayアクセシビリティメニューアイコンを非表示。| `(iconVisibilityOff)`|
|UserWayアクセシビリティアイコンの表示を切り替え。| `(iconVisibilityToggle)`|

### ウィジェットメソッド

|変数| 説明|
|---| ---|
|ウィジェットメニューを開くか閉じる。| `(widgetToggle)`|
|ウィジェットメニューを開く。| `(widgetOpen)`|
|ウィジェットメニューを閉じる。| `(widgetClose)`|
|すべてのウィジェット機能をリセット。| `(resetAll)`|

### キーボードナビゲーション

|変数| 説明|
|---| ---|
|キーボードナビゲーションを有効または無効にする。| `(keyboardNavToggle)`|
|キーボードナビゲーションを有効にする。| `(keyboardNavEnable)`|
|キーボードナビゲーションを無効にする。| `(keyboardNavDisable)`|

### ビッグカーソル

|変数| 説明|
|---| ---|
|ビッグカーソルを有効または無効にする。| `(bigCursorToggle)`|
|ビッグカーソルを有効にする。| `(bigCursorEnable)`|
|ビッグカーソルを無効にする。| `(bigCursorDisable)`|

### リーディングガイド

|変数| 説明|
|---| ---|
|リーディングガイドを有効または無効にする。| `(readingGuideToggle)`|
|リーディングガイドを有効にする。| `(readingGuideEnable)`|
|リーディングガイドを無効にする。| `(readingGuideDisable)`|

### コントラスト機能

|変数| 説明|
|---| ---|
|コントラスト機能を有効または無効にする。| `(contrastToggle)`|
|コントラスト機能を有効にする、整数値は `1` から `4` または空。| `(contrastEnable)`|
|コントラスト機能を無効にする。| `(contrastDisable)`|

### ビッグテキスト

|変数| 説明|
|---| ---|
|ビッグテキスト機能を有効または無効にする。| `(bigTextToggle)`|
|ビッグテキスト機能を有効にする、整数値は `1` から `4` または空。| `(bigTextEnable)`|
|ビッグテキスト機能を無効にする。| `(bigTextDisable)`|

### ハイライト機能

|変数| 説明|
|---| ---|
|ハイライト機能を有効または無効にする。| `(highlightToggle)`|
|ハイライト機能を有効にする。| `(highlightEnable)`|
|ハイライト機能を無効にする。| `(highlightDisable)`|

### 読みやすいフォント

|変数| 説明|
|---| ---|
|読みやすいフォント機能を有効または無効にする。| `(legibleFontsToggle)`|
|読みやすいフォント機能を有効にする。| `(legibleFontsEnable)`|
|読みやすいフォント機能を無効にする。| `(legibleFontsDisable)`|

### テキスト間隔

|変数| 説明|
|---| ---|
|テキスト間隔機能を有効または無効にする。| `(textSpacingToggle)`|
|テキスト間隔機能を有効にする、整数値は `1` から `3` または空。| `(textSpacingEnable)`|
|テキスト間隔機能を無効にする。| `(textSpacingDisable)`|

### ReadPage

|変数| 説明|
|---| ---|
|**Read Page** 機能の読み上げ速度を有効化、無効化、または変更する。| `(readPageToggle)`|
|Read Page機能を有効にする。| `(readPageEnable)`|
|Read Page機能を無効にする。| `(readPageDisable)`|

### PageStructure

|変数| 説明|
|---| ---|
|事前定義された **headers** タブを持つページ構造ビューを有効にする。| `(pageStructureHeaders)`|
|事前定義された **landmarks** タブを持つページ構造ビューを有効にする。| `(pageStructureLandmarks)`|
|事前定義された **links** タブを持つページ構造ビューを有効にする。| `(pageStructureLinks)`|
|ページ構造機能を無効にする。| `(pageStructureDisable)`|

### ツールチップ

|変数| 説明|
|---| ---|
|ツールチップ機能を有効または無効にする。| `(tooltipsToggle)`|
|ツールチップ機能を有効にする。| `(tooltipsEnable)`|
|ツールチップ機能を無効にする。| `(tooltipsDisable)`|

### アニメーションの停止

|変数| 説明|
|---| ---|
|アニメーション停止機能を有効または無効にする。| `(stopAnimationToggle)`|
|アニメーション停止機能を有効にする。| `(stopAnimationEnable)`|
|アニメーション停止機能を無効にする。| `(stopAnimationDisable)`|

### クイックアクセシビリティメニュー

|変数| 説明|
|---| ---|
|クイックアクセシビリティメニューを開く。| `(openQuickAccessibilityMenu)`|

### ウィジェット構成

|変数| 説明|
|---| ---|
|ウィジェットの言語を動的に更新。ページのリフレッシュは必要ありません。| `(changeWidgetLanguage)`|

