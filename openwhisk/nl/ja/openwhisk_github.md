---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-23"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# GitHub パッケージの使用
{: #openwhisk_catalog_github}

`/whisk.system/github` パッケージは、
[GitHub API](https://developer.github.com/) を使用するための便利な方法を提供します。

このパッケージには、以下のフィードが含まれています。

| エンティティー | タイプ  | パラメーター | 説明 |
| --- | --- | --- | --- |
| `/whisk.system/github` | パッケージ | username、repository、accessToken | GitHub API と対話 |
| `/whisk.system/github/webhook` | フィード | events、username、repository、accessToken | GitHub アクティビティーでトリガー・イベントを発生させる |

`username`、`repository`、および `accessToken` の各値を使用してパッケージ・バインディングを作成することをお勧めします。バインディングを使用すると、パッケージのフィードを使用するたびに値を指定する必要はありません。

## GitHub アクティビティーによるトリガー・イベントの発生

`/whisk.system/github/webhook` フィードは、指定された GitHub リポジトリーにアクティビティーがある場合にトリガーを発生させるサービスを構成します。パラメーターは次のとおりです。


- `username`: GitHub リポジトリーのユーザー名。
- `repository`: GitHub リポジトリー。
- `accessToken`: ご使用の GitHub パーソナル・アクセス・トークン。[トークンの作成](https://github.com/settings/tokens)時に、必ず repo:status スコープと public_repo スコープを選択してください。また、リポジトリーに既に定義された Web フックがないようにしてください。
- `events`: 対象の [GitHub イベント・タイプ](https://developer.github.com/v3/activity/events/types/)。

以下は、GitHub リポジトリーに新規コミットがあるたびに発生するトリガーを作成する例です。

1. GitHub [ パーソナル・アクセス・トークンを作成します。](https://github.com/settings/tokens).
  
  アクセス・トークンは次のステップで使用します。
  
2. GitHub リポジトリー用に構成されるパッケージ・バインディングを、アクセス・トークンを使用して作成します。
  
  ```
  wsk package bind /whisk.system/github myGit \
    --param username myGitUser \
    --param repository myGitRepo \
    --param accessToken aaaaa1111a1a1a1a1a111111aaaaaa1111aa1a1a
  ```
  {: pre}
  
3. `myGit/webhook` フィードを使用して、GitHub `push` イベント・タイプのトリガーを作成します。
  
  ```
wsk trigger create myGitTrigger --feed myGit/webhook --param events push
  ```
  {: pre}
  
  `git push` を使用して GitHub リポジトリーへのコミットが行われると、Web フックによってトリガーが発生します。トリガーに突き合わせるルールが存在する場合は、関連付けられたアクションが呼び出されます。
アクションは、GitHub Web フック・ペイロードを入力パラメーターとして受け取ります。各 GitHub Web フック・イベントは、類似した JSON スキーマを持っていますが、それぞれのイベント・タイプによって判別される固有のペイロード・オブジェクトです。
ペイロード・コンテンツについては、[GitHub events and payload](https://developer.github.com/v3/activity/events/types/) API の資料を参照してください。
  
