---

copyright:
  years: 2015, 2016
lastupdated: "2017-02-24"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 保守および VM の更新
{: #maintenance_and_vm_updates}

## 保守方針
{: #maintenance_strategy}

IBM WebSphere Application Server in Bluemix は定期的に更新されており、新しいサービス・インスタンスが最新のフィックスパックとパッチを使用して作成されるようにしています。クラウドによって、ミドルウェア管理で新しいサービス・インスタンスの容易かつ迅速なプロビジョンが実現されます。
多くの利用者が、保守を適用したいときに、新しいサービス・インスタンスにアップグレードすると見込まれます。
長期に存続するサービス・インスタンスを保持したい利用者には、保守リポジトリーをミドルウェアと基盤の稼働ゲストに使用できます。
これらのリポジトリーを使用して、オンプレミスの場合と同様に環境を保守できます。

## VM の更新

以下のセクションでは、仮想マシン・システムの変更の適用方法について説明します。

VM の更新は、他の通常の RHEL システムと同じように行えます。
Red Hat パッケージ・マネージャーの「Yum」を使用して、パッケージのインストール、更新、アンインストール、その他の各種作業を行えます。

IBM の Red Hat Satellite Server からこうした更新を受け取るように、システムがセットアップされます。
このサテライトでは、Yum パッケージ・マネージャーによって Red Hat Network から安全でセキュアなパッケージを提供します。

Satellite Server は IBM が管理するもので、ご使用のシステムからこれを変更することはできません。

詳しくは、[
Applying package updates on Red Hat Enterprise Linux](https://access.redhat.com/articles/11258#rhel6){: new_window} および
[Yum, the Red Hat package manager](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/ch-yum.html){: new_window} を参照してください。
