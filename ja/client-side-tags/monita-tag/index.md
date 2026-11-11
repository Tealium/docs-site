---
title: Monitaタグ構成ガイド
description: この記事では、タグ管理アカウントでMonitaタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/monita-tag/
---
Monitaはタグ監視プラットフォームです。配信されているタグやピクセル、およびそれらが送信しているデータをリアルタイムのダッシュボードで確認できます。また、ビジネス上の条件に違反した場合や、PII（個人を特定できる情報）が検出された場合に、リアルタイムでアラートを送信できます。

Monitaのタグコードは、ページが読み込まれる前にライブラリとして読み込まれるように設計されています。そのため、このタグのインストールにはTealiumタグマーケットプレイスではなく、[JavaScript拡張機能](https://docs.tealium.com/javascript-code-extension/)を使用してください。

## タグの構成

### Monitaモニターの構成

Monitaタグをインストールする前に、Monitaのサイトで[Monitaモニターを構成](https://docs.google.com/document/d/1X--Dyl3Pdnp2JJKzX1ckAx41cGDRkvTaX-AiHrS0QbY/edit)する必要があります。Monitaモニターを構成するには、次の手順を実行します。

1. Monitaに登録し、オンボーディング画面に必要な情報を入力します。
1. **Monitoring**をクリックします。
1. **Select Tag Manager**選択リストから、**Tealium**を選択します。
1. ドメインを入力します。複数ある場合は、すべてのドメインを入力します。
1. **+ NEW VENDOR**をクリックします。
1. 監視するベンダーを選択します。
1. **Save**をクリックします。

インストールガイドが表示されます。その手順に従い、コードブロックをメモ帳にコピーします。

### Monitaタグの構成

Monitaタグをインストールするには、次の手順を実行します。

1. **Extensions**に移動し、**+ Add Extension**をクリックします。
1. **Advanced**をクリックし、**JavaScript Code**の横にある**+ Add**をクリックします。
1. **Title**に`Monita`と入力します。
1. **Scope**ドロップダウンから、**Pre Loader**を選択します。
1. **Edit Load Order**をクリックし、Monita拡張機能を`1`に構成します。
1. Monitaからコピーしたコードブロックを拡張機能の構成に貼り付けます。
1. 保存してパブリッシュします。