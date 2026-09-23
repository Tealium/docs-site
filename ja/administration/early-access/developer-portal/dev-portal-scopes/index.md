---
title: 開発者ポータルのスコープ
description: Tealiumの複合スコープがAPIトークンでのリソースとアクションへのアクセスをどのように制御するかを理解します。
url: https://docs.tealium.com/ja/administration/early-access/developer-portal/dev-portal-scopes/
---
スコープは、アプリケーションが実行できるリソースとアクションに対するきめ細かなアクセス制御を提供します。各サブスクリプションは、構成したスコープに基づいて特定のAPIエンドポイントへのアクセスを許可します。

APIをサブスクライブする際には、アプリケーションが必要とするスコープを選択します。最小権限の原則を適用し、アプリケーションが実際に必要とするスコープのみを要求してください。詳細については、[サブスクリプション](https://docs.tealium.com/dev-portal-subscriptions/)を参照してください。

## 複合スコープ

Tealiumは、単一の文字列で完全なアクセスコンテキストをエンコードする複合スコープを使用します：

```none
{account}:{profile}:{apiFamily}:{apiVersion}:{resource}:{action}
```

| コンポーネント | 説明 | 例 |
|---|---|---|
| アカウント | スコープが適用されるTealiumアカウント | `my-company` |
| プロファイル | アカウント内のプロファイル。すべてのプロファイルには `*` を使用します。 | `main`, `*`, `prod-web` |
| APIファミリー | スコープが認証するAPI。API自体から取得され、選択するものではありません。 | `cdp-api`, `context-api` |
| APIバージョン | そのAPIのバージョン。すべてのバージョンをカバーするには `*` を使用します。 | `2026-07`, `*` |
| リソース | アクセスされるリソースのタイプ | `labels`, `audiences`, `events` |
| アクション | リソースに対して許可される操作 | `read`, `write`, `delete`, `manage` |

例えば：

* `my-account:main:cdp-api:2026-07:labels:read`：`my-account`の`main`プロファイルで、CDP APIのバージョン2026-07のラベルを読み取ります。
* `my-account:*:cdp-api:2026-07:audiences:write`：`my-account`のすべてのプロファイルでオーディエンスを書き込みます。
* `my-account:main:cdp-api:2026-07:*:*`：APIが提供するすべてのスコープ、後に追加されたスコープも含みます。
* `my-account:main:cdp-api:*:labels:read`：CDP APIのすべてのバージョンでラベルを読み取ります。

アスタリスク (`*`) ワイルドカードは任意の位置で使用でき、そのセグメントのすべての値に一致します。APIが提供するすべてのスコープを要求するには、リソースとアクションの位置に `*` が必要です：`{account}:{profile}:{apiFamily}:{apiVersion}:*:*`。単一の末尾のアスタリスクは異なる形式であり、以下で説明するエンジンワイルドカードです。

## エンジンレベルのスコープ

Context APIのような一部のAPIでは、アカウントとプロファイルへのアクセスに加えて、エンジンレベルの認証が必要です。これらのAPIのトークンには、エンジンレベルの複合スコープが含まれます：

```none
{account}:{profile}:{apiFamily}:{apiVersion}:{engineId}
```

| コンポーネント | 説明 | 例 |
|---|---|---|
| アカウント | スコープが適用されるTealiumアカウント | `my-company` |
| プロファイル | アカウント内のプロファイル | `main`, `prod-web` |
| APIファミリー | スコープが認証するAPI | `context-api` |
| APIバージョン | そのAPIのバージョン | `2026-06`, `*` |
| エンジンID | 特定のMomentsエンジン | `e01ce645-3964-...`。プロファイル内のすべてのエンジンには `*` を使用します。 |

例えば：

* `my-account:main:context-api:2026-06:e01ce645-3964-4343-9a0c-7d165e653b35`：`my-account`の`main`プロファイルで特定のエンジンへのアクセス。
* `my-account:main:context-api:2026-06:*`：`my-account`の`main`プロファイル内のすべてのエンジンへのアクセス。

エンジン強制APIへのサブスクリプションがリソーススコープも付与する場合、それらは単一のスコープに組み合わされます：

```none
{account}:{profile}:{apiFamily}:{apiVersion}:{engineId}:{resource}:{action}
```

例えば、`my-account:main:context-api:2026-06:e01ce645-3964-4343-9a0c-7d165e653b35:actions:read`はそのエンジンからアクションを読み取ります。

エンジンスコープは、サブスクリプション時または[サードパーティアプリアクセス](https://docs.tealium.com/dev-portal-third-party-app-access/)を通じてリソース所有者がエンジンアクセスを付与する際に、自動的にトークンに追加されます。エンジンスコープは手動で要求する必要はありません。それらは付与プロセス中に行われたエンジン選択から派生します。