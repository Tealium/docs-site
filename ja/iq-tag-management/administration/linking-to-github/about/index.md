---
title: GitHubへのリンクについて
description: この記事では、アクセストークンを使用してGitHubアカウントとiQタグ管理アカウントとの間に安全なリンクを作成する方法について説明します。
url: https://docs.tealium.com/ja/iq-tag-management/administration/linking-to-github/about/
---
リンクが完了すると、[Advanced JavaScript Code extension](https://docs.tealium.com/advanced-javascript-code-extension/)を使用してGitHubリポジトリからファイルを参照し、同期することができます。コードはGitHubに安全に保管されていますが、iQタグ管理の構成で公開することができます。

## 要件

#### GitHubの要件

* GitHubアカウント:
  * 少なくとも1つの公開リポジトリを持っていること（空でも可）。
  * [GitHub個人アクセストークン](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)を持っていること。GitHub Enterprise Serverの場合は、組織によって承認された細分化された個人アクセストークンを使用します。
  * `github.com`または自己ホスト型のGitHub Enterprise Serverでホストされていること。
* GitHubおよびGitHubリポジトリの操作に関する知識と経験。


<blockquote>
GitHubを使用していない場合や公開リポジトリを持っていない場合は、GitHubにリンクする代わりに[iq-javascript-extension-api](https://docs.tealium.com/iq-javascript-extension-api/)を使用することをお勧めします。
</blockquote>


#### Tealiumの要件

* Tealiumアカウントでのアカウント管理権限。

## 仕組み

GitHubとの統合により、GitHubでのコード管理プロセスとiQタグ管理での公開との間でシームレスなワークフローが作成されます。GitHubのユーザー名と[個人アクセストークン](https://github.com/settings/tokens)を使用してGitHubアカウントへのリンクを作成します。Tealiumアカウント内のすべてのプロファイルに対して1つのリンクが必要です。


<blockquote>
リンクを成功させるためには、GitHubアカウントに少なくとも1つの公開または非公開リポジトリが必要です。
</blockquote>


アカウントがリンクされると、リポジトリ内のJavaScriptファイルをiQタグ管理の構成で参照できるようになります。GitHubリポジトリからファイルが参照されると、そのコードはGitHubリポジトリに安全に保管されたままですが、iQタグ管理の構成の一部として公開することができます。

GitHubリポジトリ内の参照されたファイルに変更をコミットすると、iQタグ管理でそれらのファイルを同期して最新バージョンを取得する必要があります。参照されたファイルを同期すると、保存して公開する必要がある未保存の変更が発生します。

## サポートされる機能

GitHub統合をサポートする機能は以下の通りです：

* [Advanced JavaScript Code extension](https://docs.tealium.com/advanced-javascript-code-extension/)