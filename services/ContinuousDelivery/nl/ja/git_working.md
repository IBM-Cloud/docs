---

copyright:
  years: 2015, 2017
lastupdated: "2017-4-11"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:screen:.screen}
{:codeblock:.codeblock}

# Git Repos and Issue Tracking での作業 (試験段階)
{: #git_working}

IBM によってホストされ、[GitLab Community Edition ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://about.gitlab.com/){:new_window}上に構築されている Git リポジトリーおよび Issue Tracker を使用して、チームでの共同作業およびソース・コードの管理を行います。
{: shortdesc}

Git Repos and Issue Tracking ツール統合は、以下に示す多くの方法でチームのコード管理と共同作業をサポートします。
   * コードの安全性を保つ、きめ細かいアクセス制御を通じて Git リポジトリーを管理する
   * マージ要求を介してコードを検討し、コラボレーションを強化する
   * Issue Tracker を介して問題を追跡し、アイデアを共有する
   * Wiki システム上にプロジェクトを文書化する

**注:** このツール統合は GitLab Community Edition 上に構築され、IBM によって Bluemix 上でホストされているため、一部の GitLab オプションは使用できません。例えば、Delivery Pipeline は、Bluemix の継続的統合と継続的デリバリーを提供しているため、GitLab の継続的統合フィーチャーはサポートされません。さらに、管理機能は、IBM によって管理されているため使用できません。

## ファイルおよびリポジトリーのサイズ制限
{: #git_limits}

ファイルは、厳密に 100 MB に制限されています。推奨されているリポジトリー・サイズ制限は 1 GB です。リポジトリーが 1 GB を超えると、リポジトリー・サイズの削減を要求する E メールを受け取る可能性があります。

## 認証のための個人用アクセス・トークンまたは SSH 鍵の作成    
{: #git_authentication}

ローカル Git リポジトリーから `clone` または `push` などのリモート Git 操作を完了するには、個人用アクセス・トークンまたは SSH 鍵を使用して GitLab の認証を行う必要があります。

* 個人用アクセス・トークンをセットアップするには、[Personal access tokens (個人用アクセス・トークン) ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://git.ng.bluemix.net/help/api/README.html#personal-access-tokens){:new_window}を参照してください。
* SSH 鍵をセットアップするには、[SSH ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://git.ng.bluemix.net/help/ssh/README){:new_window} または [How to create your SSH Keys (SSH 鍵の作成方法) ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://git.ng.bluemix.net/help/gitlab-basics/create-your-ssh-keys){:new_window}を参照してください。SSH 認証を使用してリポジトリーにアクセスするには、プロキシーおよびファイアウォールの追加構成が必要な場合があります。

**注:** 個人用アクセス・トークンまたは SSH 鍵を認証に使用するには、Git をローカルにセットアップする必要があります。手順については、[Start using Git on the command line (コマンド・ラインでの Git の使用の開始) ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://git.ng.bluemix.net/help/gitlab-basics/start-using-git){:new_window}を参照してください。
