---

copyright:
  years: 2015, 2017
lastupdated: "2017-4-11"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:screen:.screen}
{:codeblock:.codeblock}

# Git Repos and Issue Tracking (ベタ版)
{: #git_working}

IBM によってホストされ、[GitLab Community Edition ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://about.gitlab.com/){:new_window}上に構築されている Git リポジトリおよび Issue Tracker を使用して、チムでの共同作業およびソス・コドの管理を行います。
{: shortdesc}

Git Repos and Issue Tracking ツル統合は、以下に示す多くの方法でチムのコド管理と共同作業をサポトします。
   * コドの安全性を保つ、きめ細かいアクセス制御を通じて Git リポジトリを管理する
   * マジ要求を介してコドを検討し、コラボレションを強化する
   * Issue Tracker を介して問題を追跡し、アイデアを共有する
   * Wiki システム上にプロジェクトを文書化する

**注:** このツル統合は GitLab Community Edition 上に構築され、IBM によって Bluemix 上でホストされているため、一部の GitLab オプションは使用できません。例えば、Delivery Pipeline は、Bluemix の継続的統合と継続的デリバリを提供しているため、GitLab の継続的統合フィチャはサポトされません。さらに、管理機能は、IBM によって管理されているため使用できません。

## ファイルおよびリポジトリのサイズ制限
{: #git_limits}

ファイルは、厳密に 100 MB に制限されています。推奨されているリポジトリ・サイズ制限は 1 GB です。リポジトリが 1 GB を超えると、リポジトリ・サイズの削減を要求する E メルを受け取る可能性があります。

## Git Repos and Issue Tracking をロカルで使用する
{: #git_authentication}

Git Repos and Issue Tracking に保管されている Git リポジトリにはロカルからアクセスできます。ロカルで Git をセットアップする手順については、[Start using Git on the command line (コマンド・ラインでの Git の使用の開始) ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://git.ng.bluemix.net/help/gitlab-basics/start-using-git){:new_window} を参照してください。

### 認証のための個人用アクセス・トクンまたは SSH 鍵の作成  
ロカル Git リポジトリから `clone` または `push` などのリモト Git 操作を完了するには、個人用アクセス・トクンまたは SSH 鍵を使用して GitLab の認証を行う必要があります。

* 個人用アクセス・トクンをセットアップするには、[Personal access tokens (個人用アクセス・トクン) ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://git.ng.bluemix.net/help/api/README.html#personal-access-tokens){:new_window}を参照してください。
* SSH 鍵をセットアップするには、[SSH ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://git.ng.bluemix.net/help/ssh/README){:new_window} または [How to create your SSH Keys (SSH 鍵の作成方法) ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://git.ng.bluemix.net/help/gitlab-basics/create-your-ssh-keys){:new_window}を参照してください。SSH 認証を使用してリポジトリにアクセスするには、プロキシおよびファイアウォルの追加構成が必要な場合があります。
