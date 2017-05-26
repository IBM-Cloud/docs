---

copyright:
  years: 2015, 2016
lastupdated: "2017-02-24"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# IBM WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} 入門
{: #getting_started}

{{site.data.keyword.IBM}} WebSphere Application Server in {{site.data.keyword.Bluemix}} は、{{site.data.keyword.Bluemix_notm}} 上でホストされるクラウド環境で、事前定義済みの WebSphere Application Server Liberty、Traditional Network Deployment、または Traditional WebSphere Java EE インスタンスを迅速にセットアップできるようにするサービスです。
{: shortdesc}

## WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} の概要
{: #overview}

WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} は、事前構成された Traditional WebSphere および Liberty プロファイルのサーバーを利用者に提供します。これは、ゲスト・オペレーティング・システムへの root アクセス権限を持つ仮想マシン・ゲストでホストされます。
サービスを作成するときに、*Liberty*、*Traditional ND*、または *Traditional WebSphere* のいずれかを選択します。

**注:** 利用者は、新規の *Traditional ND* または *Traditional WebSphere* インスタンスを作成するときに、V8.5 と V9.0 のどちらかを選択できるようになりました。

使い慣れた WebSphere 管理操作を使用し、基盤オペレーティング・システムへの全アクセス権限を持つことができます。
既存のスクリプトを再使用可能で、独自のフレームワークまたはサード・パーティーのフレームワークで動作させるために必要なシステム微調整を行います。
オンプレミスの WebSphere 構成と同様に、WebSphere Application Server Liberty、ND、または Traditional のサービスを管理するために、管理センターと管理コンソールが提供されています。

WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} Network Deployment プランは、2 つ以上の仮想マシンを使用する WebSphere Application Server Network Deployment セル環境で構成されています。1 つ目の仮想マシンには、Deployment Manager と IBM HTTP Server が含まれており、残りの仮想マシンには、Deployment Manager に統合されたカスタム・ノード (ノード・エージェント) が含まれています。既存の wsadmin スクリプトを使用して WebSphere 構成を作成するか、WebSphere 管理コンソールを使用して手動で環境を作成します。これらの新機能により、すべてのミドルウェア・エンタープライズ・アプリケーションの重要な側面であるクラスター環境をセットアップすることができます。クライアントは、トポロジーをクラスター化して、2 つ以上のインスタンスに要求をロード・バランシングすることを選択できるようになりました。


WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} Liberty Core プランには、Liberty Collective の使用が含まれています。Liberty Collective は、Liberty プロファイル (サーバー) のグループの管理ドメインであり、2 つ以上の仮想マシンで構成されています。1 つ目の仮想マシンには、Liberty 集合の制御点である集合コントローラー Liberty サーバーが含まれています。Liberty 集合に加え、この仮想マシンには、Web ブラウザーからアプリケーションへのアクセスが可能な IBM HTTP Server も含まれています。残りの仮想マシンは、集合メンバーが常駐する集合ホスト (Liberty プロファイル・サーバー) です。Liberty 管理センター機能も、Liberty コントローラー・サーバーで有効になります。

次の図は、WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} Network Deployment セル環境と Liberty 集合環境のアーキテクチャーを示しています。

図 1. Network Deployment セルと Liberty 集合のアーキテクチャー

![図 1。Network Deployment セルと Liberty 集合のアーキテクチャー](images/CellCollectiveDiagram.gif)

**注**: 上の*図 1* で、Deployment Manager または集合コントローラーと IBM HTTP Server との連結を表すパターンは、開発およびテストの目的を想定しています。また、WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} では、実動適用および運用上の必要性に合わせたインストール済みソフトウェアの再構成を、オンプレミスの場合と同様に自由に行うことができます。さらに、厳密な実働要件については、IBM 営業担当員にご連絡ください。隔離されたネットワーキングおよび計算リソースを提供する単一テナントの IBM WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} オファリングについてご説明します。


## 稼働環境
{: #operational_environment}

IBM WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} は、利用者がアプリケーションをデプロイするための共有環境にゲスト (仮想マシン) を戻すサービスです。VPN によって、汎用ポート・スキャンや他の一方的なネットワーク・ベースの攻撃からパブリック・サービスが保護されます。
ただし、サービス・インスタンスへのアクセスに使用するサービス VPN は、
複数の {{site.data.keyword.Bluemix_notm}}
組織およびユーザーの間で共有される可能性があるため、注意する必要があります。
仮想マシンでは、IaaS リソースの共有プールから、計算、メモリー、および入出力のリソースを提供します。


計算、メモリー、および入出力の個々のリソースは共有環境で仮想マシンによって実行されるため、サービス構成が異なる可能性があります。
特定の各サービス・インスタンスの構成は、IBM WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} サービスのダッシュボードおよびポータルから表示できます。

IBM WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} は、仮想マシン・インスタンスを提供します。それらのインスタンスにより、クライアントは単純なポータルを使用してエンタープライズの WebSphere Application Server デプロイメントを一貫性のある反復可能な方法で作成および管理し、非常に柔軟にアプリケーションをチューニングします。ユーザーは、事前構成済みの WebSphere Application Server Liberty、ND、または Traditional の仮想マシンを、ホストされたクラウド環境で稼働させることができます。ユーザーは既存の WebSphere Application Server アプリケーションを {{site.data.keyword.Bluemix_notm}} にマイグレーションし、基盤 OS およびミドルウェアを完全に制御できます。

## 価格設定について
{: #pricing_strategy}

IBM WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} では、メモリーを大量に使用するアプリケーションを使用するお客様が、仮想マシンを大きくして環境を適正なサイズにできるように、T シャツ・サイズで表記されたインスタンスが用意されています。クライアントは、プロビジョンされた WebSphere Application Server コンポーネントまたは単一システムの特定のリソース・サイズを、最大 32 GB RAM 仮想マシンまで選択することができます。

以下の表は、2016 年 4 月 1 日時点の米国ドル (USD) 表示による IBM WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} プラン料金を示しています。

*表 1. Liberty Core のプラン*

| **T シャツ** | **vCPU** | **RAM (GB)** | **HD (GB)** | **料金/時** |       
|:-------------:|:----------:|:--------------:|:-------------:|:--------------:|
| S | 1 | 2 | 12 | $0.21 |
| M | 2 | 4 | 25 | $0.42 |
| L | 4 | 8 | 50 | $0.84 |
| XL | 8 | 16 | 100 | $1.68 |
| XXL | 16 | 32 | 200 | $3.36 |

*表 2. WebSphere Application Server Base のプラン*

| **T シャツ** | **vCPU** | **RAM (GB)** | **HD (GB)** | **料金/時** |       
|:-------------:|:----------:|:--------------:|:-------------:|:--------------:|
| S | 1 | 2 | 12 | $0.30 |
| M | 2 | 4 | 25 | $0.60 |
| L | 4 | 8 | 50 | $1.20 |
| XL | 8 | 16 | 100 | $2.40 |
| XXL | 16 | 32 | 200 | $4.80 |

*表 3. WebSphere Application Server ND のプラン*

| **T シャツ** | **vCPU** | **RAM (GB)** | **HD (GB)** | **料金/時** |       
|:-------------:|:----------:|:--------------:|:-------------:|:--------------:|
| S | 1 | 2 | 12 | $0.70 |
| M | 2 | 4 | 25 | $1.40 |
| L | 4 | 8 | 50 | $2.80 |
| XL | 8 | 16 | 100 | $5.60 |
| XXL | 16 | 32 | 200 | $11.20 |

<p></p>

IBM WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} は、以下の課金単位に従って提供されます。

*  *インスタンス時間*: 「インスタンス」は、IBM WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} サービスの特定の構成へのアクセスとして定義されます。クライアントは、請求期間中に導入されているサービスの各インスタンスについて、時間単位で、または 1 時間に満たない時間に対して、課金されます。各「インスタンス時間」は月次払いであり、インスタンスの使用が 1 カ月に満たない場合は、使用率が按分されます。

例えば、ND プランを使用する場合、1 インスタンスは、2 GB RAM と 12 GB HD を備えた 1vCPU に相当します。したがって、1 つの制御ノードと 8 つのカスタム・ノードでセルを構成することを選択した場合は、9 ノード (インスタンス) について課金されます。

**注**: 最小請求処理は、カスタム・ノードまたは Liberty ホスト当たり 0.25 インスタンス時間に設定されています。上記の例では、少なくとも 15 分に対して構成された 1 制御ノードおよび 1 カスタム・ノードが最小課金 (0.25 × インスタンス数) に相当します。

**注**: 一定量の計算、メモリー、入出力のリソースのために、停止状態の累積インスタンスについて 5 % 減額して課金されます。IP アドレス 10 個およびメモリー 64 GB を超えない決まった数の停止インスタンスに管理されます。

# 関連リンク
{: #rellinks}
## 一般
{: #general}
* [WASdev](https://developer.ibm.com/wasdev/){: new_window}
* [WebSphere Application Server V9 の資料](http://www.ibm.com/support/knowledgecenter/SSEQTP_9.0.0/as_ditamaps/was900_welcome_base.html){: new_window}
