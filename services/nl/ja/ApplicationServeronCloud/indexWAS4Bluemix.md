---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# IBM WebSphere Application Server for Bluemix 入門
{: #getting_started}

*最終更新日: 2016 年 4 月 8 日*

{{site.data.keyword.IBM}} WebSphere Application Server for {{site.data.keyword.Bluemix}} は、Bluemix 上でホストされるクラウド環境において、事前構成済みの WebSphere Application Server Liberty、Network Deployment、または従来型のインスタンスでの迅速なセットアップを容易にするサービスです。
{: shortdesc}

## WebSphere Application Server for Bluemix の概要
{: #overview}

WebSphere Application Server for Bluemix は、事前構成された従来型の WebSphere サーバーおよび Liberty プロファイル・サーバーを利用者に提供します。これは、ゲスト・オペレーティング・システムへの root アクセス権限を持つ仮想マシン・ゲストでホストされます。
サービスを作成するときに、*Liberty*、*ND*、*従来型の WebSphere* のいずれかを選択します。

使い慣れた WebSphere 管理操作を使用し、基盤オペレーティング・システムへの全アクセス権限を持つことができます。
既存のスクリプトを再使用可能で、独自のフレームワークまたはサード・パーティーのフレームワークで動作させるために必要なシステム微調整を行います。
オンプレミスの WebSphere 構成と同様に、WebSphere Application Server Liberty、ND、または従来型のサービスを管理するために、管理センターと管理コンソールが提供されています。

**注**: WebSphere Application Server for Bluemix Network Deployment プランに機能が追加されました。このプランは、2 つ以上の仮想マシンを使用する WebSphere Application Server Network Deployment セル環境で構成されています。1 つ目の仮想マシンには、デプロイメント・マネージャーと IBM HTTP Server が含まれており、残りの仮想マシンには、デプロイメント・マネージャーに連合されたカスタム・ノード (ノード・エージェント) が含まれています。既存の wsadmin スクリプトを使用して WebSphere 構成を作成するか、WebSphere 管理コンソールを使用して手動で環境を作成します。これらの新機能により、ユーザーは高可用性、フェイルオーバー、およびスケーラビリティーに対してクラスター環境をセットアップすることができます。クラスター化はすべてのミドルウェア・エンタープライズ・アプリケーションの重大な側面であり、クライアントは、トポロジーをクラスター化して、2 つ以上のインスタンスに要求をロード・バランシングすることを選択できるようになりました。


WebSphere Application Server for Bluemix Liberty Core プランにも、機能が追加されました。このプランには、Liberty プロファイル (サーバー) のグループの管理ドメインであり、2 つ以上の仮想マシンで構成される Liberty 集合の使用が含まれています。1 つ目の仮想マシンには、Liberty 集合の制御点である集合コントローラー Liberty サーバーが含まれています。Liberty 集合に加え、この仮想マシンには、Web ブラウザーからアプリケーションへのアクセスが可能な IBM HTTP Server も含まれています。残りの仮想マシンは、集合メンバーが常駐する集合ホスト (Liberty プロファイル・サーバー) です。Liberty 管理センター機能も、Liberty コントローラー・サーバーで有効になります。

次の図は、WebSphere Application Server for Bluemix Network Deployment セル環境と Liberty 集合環境のアーキテクチャーを示しています。

![図 1。Network Deployment セルと Liberty 集合のアーキテクチャー](images/CellCollectiveDiagram.gif)

## 稼働環境
{: #operational_environment}

IBM WebSphere Application Server for Bluemix は、利用者がアプリケーションをデプロイするための共有環境にゲスト (仮想マシン) を戻すサービスです。VPN によって、汎用ポート・スキャンや他の一方的なネットワーク・ベースの攻撃からパブリック・サービスが保護されます。
ただし、サービス・インスタンスへのアクセスに使用するサービス VPN は、複数の Bluemix 組織およびユーザーの間で共有される可能性がある点に注意することが重要です。仮想マシンでは、IaaS リソースの共有プールから、計算、メモリー、および入出力のリソースを提供します。
アプリケーションを専用環境で実行したい場合は、IBM 営業担当員にご連絡ください。専用の IBM WebSphere Application Server for Bluemix オファリングについてご説明します。

計算、メモリー、および入出力の個々のリソースは共有環境で仮想マシンによって実行されるため、サービス構成が異なる可能性があります。
特定の各サービス・インスタンスの構成は、IBM WebSphere Application Server for Bluemix サービスのダッシュボードおよびポータルから表示できます。

**注**: IBM WebSphere Application Server for Bluemix は、メモリーを大量に使用するアプリケーションを使用するクライアントに、より大きな仮想マシンによって環境を適正化するオプションを提供するようになりました。クライアントは、プロビジョンされた WebSphere Application Server コンポーネントまたは単一システムの特定のリソース・サイズを、最大 32 GB RAM 仮想マシンまで選択することができます。

## 価格設定について
{: #pricing_strategy}

IBM WebSphere Application Server for Bluemix は、仮想マシン・インスタンスを提供します。それらのインスタンスにより、クライアントは単純なポータルを使用してエンタープライズの WebSphere Application Server デプロイメントを一貫性のある反復可能な方法で作成および管理し、非常に柔軟にアプリケーションをチューニングします。ユーザーは、事前構成済みの WebSphere Application Server Liberty、ND、または従来型の仮想マシンを、ホストされたクラウド環境で稼働させることができます。ユーザーは既存の WebSphere Application Server アプリケーションを Bluemix にマイグレーションし、基盤 OS およびミドルウェアを完全に制御できます。

IBM WebSphere Application Server for Bluemix は、以下の課金単位に従って提供されます。

*  *インスタンス時間*: 「インスタンス」は、IBM WebSphere Application Server for Bluemix サービスの特定の構成へのアクセスとして定義されます。クライアントは、請求期間中に導入されているサービスの各インスタンスについて、時間単位で、または 1 時間に満たない時間に対して、課金されます。各「インスタンス時間」は月次払いであり、インスタンスの使用が 1 カ月に満たない場合は、使用率が按分されます。

例えば、ND プランを使用する場合、1 インスタンスは、2 GB RAM と 12 GB HD を備えた 1vCPU に相当します。したがって、1 つの制御ノードと 8 つのカスタム・ノードでセルを構成することを選択した場合は、9 ノード (インスタンス) について課金されます。

**注**: 最小請求処理は、カスタム・ノードまたは Liberty ホスト当たり 0.25 インスタンス時間に設定されています。上記の例では、少なくとも 15 分に対して構成された 1 制御ノードおよび 1 カスタム・ノードが最小課金 (0.25 × インスタンス数) に相当します。

# 関連リンク
## 一般
* [WASdev](https://developer.ibm.com/wasdev/){: new_window}
* [WebSphere Application Server の資料](http://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/as_ditamaps/was855_welcome_ndmp.html){: new_window}
* [WebSphere Application Server traditional v9 ベータの資料](http://www.ibm.com/support/knowledgecenter/SSEQTP_9.0.0/as_ditamaps/was900_welcome_base.html){: new_window}
