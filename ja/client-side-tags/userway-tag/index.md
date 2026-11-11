---
title: UserWay タグの構成
description: この記事では、タグ管理アカウントでUserWayタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/userway-tag/
---

UserWayは、既存のWebサイトコードをリファクタリングすることなく、ADAへの準拠を支援する高度なWebサイトアクセシビリティソリューションを提供します。UserWayのRaaS™とTealiumを組み合わせることで、米国および各国の政府機関・規制機関が定めるWCAG 2.1、ADA、ATAG 2.0、EN 301-549、Section 508の各規制への準拠を容易にエンリッチメントできます。

## タグに関するヒント

* マッピングを使用して、タグ構成を上書きまたは動的に構成します。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときに、次の構成を構成します。

* **Data-account**：単一テキストフィールド

## ロードルール

すべてのページでタグをロードするか、タグをロードする条件を構成します。ロードルールの詳細については、[ロードルール](https://docs.tealium.com/about-load-rules/)のドキュメントを参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 共通

|変数|説明|
|---|---|
|UserWay APIのバージョンを取得します。| `(getVersion)`|
|UserWayアクセシビリティメニューアイコンを表示します。| `(iconVisibilityOn)`|
|UserWayアクセシビリティメニューアイコンを非表示にします。| `(iconVisibilityOff)`|
|UserWayアクセシビリティアイコンの表示と非表示を切り替えます。| `(iconVisibilityToggle)`|

### ウィジェットメソッド

|変数|説明|
|---|---|
|ウィジェットメニューを開閉します。| `(widgetToggle)`|
|ウィジェットメニューを開きます。| `(widgetOpen)`|
|ウィジェットメニューを閉じます。| `(widgetClose)`|
|ウィジェットのすべての機能をリセットします。| `(resetAll)`|

### キーボードナビゲーション

|変数|説明|
|---|---|
|キーボードナビゲーションを有効または無効にします。| `(keyboardNavToggle)`|
|キーボードナビゲーションを有効にします。| `(keyboardNavEnable)`|
|キーボードナビゲーションを無効にします。| `(keyboardNavDisable)`|

### 大きなカーソル

|変数|説明|
|---|---|
|大きなカーソルを有効または無効にします。| `(bigCursorToggle)`|
|大きなカーソルを有効にします。| `(bigCursorEnable)`|
|大きなカーソルを無効にします。| `(bigCursorDisable)`|

### リーディングガイド

|変数|説明|
|---|---|
|リーディングガイドを有効または無効にします。| `(readingGuideToggle)`|
|リーディングガイドを有効にします。| `(readingGuideEnable)`|
|リーディングガイドを無効にします。| `(readingGuideDisable)`|

### コントラスト機能

|変数|説明|
|---|---|
|コントラスト機能を有効または無効にします。| `(contrastToggle)`|
|コントラスト機能を有効にします。`1`から`4`までの整数値または空の値を指定します。| `(contrastEnable)`|
|コントラスト機能を無効にします。| `(contrastDisable)`|

### 大きなテキスト

|変数|説明|
|---|---|
|大きなテキスト機能を有効または無効にします。| `(bigTextToggle)`|
|大きなテキスト機能を有効にします。`1`から`4`までの整数値または空の値を指定します。| `(bigTextEnable)`|
|大きなテキスト機能を無効にします。| `(bigTextDisable)`|

### ハイライト機能

|変数|説明|
|---|---|
|ハイライト機能を有効または無効にします。| `(highlightToggle)`|
|ハイライト機能を有効にします。| `(highlightEnable)`|
|ハイライト機能を無効にします。| `(highlightDisable)`|

### 読みやすいフォント

|変数|説明|
|---|---|
|読みやすいフォント機能を有効または無効にします。| `(legibleFontsToggle)`|
|読みやすいフォント機能を有効にします。| `(legibleFontsEnable)`|
|読みやすいフォント機能を無効にします。| `(legibleFontsDisable)`|

### テキスト間隔

|変数|説明|
|---|---|
|テキスト間隔機能を有効または無効にします。| `(textSpacingToggle)`|
|テキスト間隔機能を有効にします。`1`から`3`までの整数値または空の値を指定します。| `(textSpacingEnable)`|
|テキスト間隔機能を無効にします。| `(textSpacingDisable)`|

### ページ読み上げ

|変数|説明|
|---|---|
|**ページ読み上げ**機能を有効化、無効化、または読み上げ速度を変更します。| `(readPageToggle)`|
|ページ読み上げ機能を有効にします。| `(readPageEnable)`|
|ページ読み上げ機能を無効にします。| `(readPageDisable)`|

### ページ構造

|変数|説明|
|---|---|
|あらかじめ**見出し**タブを選択した状態でページ構造ビューを有効にします。| `(pageStructureHeaders)`|
|あらかじめ**ランドマーク**タブを選択した状態でページ構造ビューを有効にします。| `(pageStructureLandmarks)`|
|あらかじめ**リンク**タブを選択した状態でページ構造ビューを有効にします。| `(pageStructureLinks)`|
|ページ構造機能を無効にします。| `(pageStructureDisable)`|

### ツールチップ

|変数|説明|
|---|---|
|ツールチップ機能を有効または無効にします。| `(tooltipsToggle)`|
|ツールチップ機能を有効にします。| `(tooltipsEnable)`|
|ツールチップ機能を無効にします。| `(tooltipsDisable)`|

### アニメーションの停止

|変数|説明|
|---|---|
|アニメーション停止機能を有効または無効にします。| `(stopAnimationToggle)`|
|アニメーション停止機能を有効にします。| `(stopAnimationEnable)`|
|アニメーション停止機能を無効にします。| `(stopAnimationDisable)`|

### クイックアクセシビリティメニュー

|変数|説明|
|---|---|
|クイックアクセシビリティメニューを開きます。| `(openQuickAccessibilityMenu)`|

### ウィジェット構成

|変数|説明|
|---|---|
|ウィジェットの言語を動的に更新します。ページを再読み込みする必要はありません。| `(changeWidgetLanguage)`|