---
title: Monitaタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでMonitaタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/monita-tag/
---
Monitaはタグ監視プラットフォームです。どのタグやピクセルが配信され、どのデータが送信されているかを示すリアルタイムダッシュボードを提供します。Monitaは、ビジネス条件が違反された場合やPII（個人を特定できる情報）が検出された場合にリアルタイムでアラートを送信することもできます。

Monitaのタグコードは、ページの読み込み前にライブラリとして読み込まれるように設計されています。したがって、このタグをインストールするためにTealiumタグマーケットプレイスを使用する代わりに、[JavaScript Extension]()を使用してください。

## タグ構成

### Monitaモニター構成

Monitaタグをインストールする前に、Monitaモニターを[構成する](https://docs.google.com/document/d/1X--Dyl3Pdnp2JJKzX1ckAx41cGDRkvTaX-AiHrS0QbY/edit)必要があります。Monitaモニターを構成するには、次の手順を実行します：

1. Monitaにサインアップし、オンボーディング画面に詳細を入力します。
1. **Monitoring**をクリックします。
1. **Select Tag Manager**のピックリストから、**Tealium**を選択します。
1. ドメインまたはドメインを入力します。
1. **&#43; NEW VENDOR**をクリックします。
1. 監視するベンダーを選択します。
1. **Save**をクリックします。

インストールガイドが表示されます。その指示に従い、コードブロックをノートパッドにコピーします。

### Monitaタグ構成

Monitaタグをインストールするには、次の手順を実行します：

1. **Extensions**に移動し、**&#43; Add Extension**をクリックします。
1. **Advanced**をクリックし、**JavaScript Code**の隣にある**&#43; Add**をクリックします。
1. **Title**の下に、`Monita`と入力します。
1. **Scope**ドロップダウンから、**Pre Loader**を選択します。
1. **Edit Load Order**をクリックし、Monita拡張機能を`1`に構成します。
1. Monitaからのコードブロックを拡張機能構成にコピーします。
1. 保存して公開します。
