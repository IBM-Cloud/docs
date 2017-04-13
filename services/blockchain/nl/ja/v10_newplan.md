---

copyright:
  years: 2017
lastupdated: "2017-03-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# High Security Business Network (HSBN) vNext Beta
{: #etn_overview}

**HSBN vNext Beta** は、ブロックチェーン・ビジネス・ネットワークを生成するための、すぐに使用可能なソリューションを提供します。このサービスは、素早くお客様にネットワークをプロビジョンし、リソースを容易に管理および保守するためのモニターを提供します。この単純なネットワーク形成および管理プロセスにより、ビジネス・ソリューションの開発とデプロイに、より多くの時間と注意を向けることができます。
{:shortdesc}

**HSBN vNext Beta** ネットワークは、ネットワーク・リソース (ピア、オーダー・ノード、CA、ソース・コード、台帳) がすべて **IBM Secure Service Container** (SSC) 内に格納されている、LinuxONE 上の高度に保護された環境で実行されます。以下の機能があります。
* 対等通信のパフォーマンスの最適化
* 高可用性と、スケーラビリティーのためのフレームワーク 
* ハードウェア暗号化、改ざん防止暗号鍵、および安全に暗号化された仮想マシン
* 改ざん防止ソフトウェアを用いたセキュア・ブート
* root アクセスなし
* FIPS コンプライアンス、高度な EAL 保護、監査適合性、および暗号最適化

**HSNB vNext Beta** プランのサブスクリプションには、以下のネットワーク・リソースのサポートも含まれています。

- 異常終了フォールト・トレラント順序付けサービス
- メンバーごとに 2 つのピア
- 最大 5 人までの追加ネットワーク・メンバー
- メンバーごとに 5 個のインスタンス化されたチェーンコード
- メンバー固有の認証局
- 最大 100 個のチャネル
- デフォルトのガバナンス・ポリシー (すべてのメンバーが管理者であり、ネットワークへの参加の招待を発行できる)

環境セキュリティー機能について詳しくは、『[IBM Secure Service Container](etn_ssc.html)』のセクションを参照してください。

## HSBN vNext Beta プランの使用
{: #use_hsbn}

### プランへのアクセス

IBM Blockchain on Bluemix の **HSBN vNext Beta** プランは、要求によって供与されます。Bluemix カタログから HSBN vNext Beta を選択し、サービス・インスタンスを作成すると、最新のベータ版への参加の要求が IBM Blockchain チームに送信されます。承認されると、プランへの参加の招待 E メールが送られます。指示に従って HSBN vNext Beta プランのダッシュボードを起動してください。

HSBN vNext Beta ダッシュボードで、以下の 3 つのオプションからいずれかを選択します。
1. **「ネットワーク・クイック・スタート (Network Quick Start)」**: HSBN vNext Beta ネットワークを作成し、他の Bluemix 組織を、参加するように招待します。
2. **「ネットワークに参加 (Join Network)」**: 他の HSBN vNext Beta ネットワークへの参加の招待を表示します。
3. **「ネットワークのモニター (Monitor Network)」**: ネットワーク・リソース (ピア、チャネル、およびチェーンコード) を管理します。

<!-- to do - the rest of this page final edit -->

### サンプル・シナリオ

大理石の製造メーカーが、IBM Blockchain ネットワークを利用して、さまざまに異なるベンダーとのトランザクションを処理したいものとします。その仕組みを説明します。すべてのネットワーク・メンバーと、公表されている大理石リポジトリーの現在の状態を含む、コンソーシアム・チャネルを作成できます。このチャネルで発生するすべてのトランザクションは、ネットワーク上のすべてのメンバーが、表示および照会できます。ただし、プライバシーや機密保持の懸念に対処するために、「サブチャネル」 (スタンドアロン・チャネル) を作成することもできます。例えば、特定の一連の条件を満たしていれば、特定のベンダーにディスカウント価格を提示する場合について考えます。このトランザクションはサブチャネルで実行でき、大理石の供給全体に対するその後の影響はコンソーシアム・チャネルで更新されます。あるいは、コンソーシアム・チャネルでは提供されていない特定のクラスの大理石を取引したい場合も考えられます。この場合、単にスタンドアロン・チャネルで必要な関係者とトランザクションを行い、コンソーシアム・チャネルの台帳は影響を受けません。チャネルによりプライバシーのための強力なメカニズムが提供されます。すべてのチャネルに固有の台帳があり、チャネルをサブスクライブして認証されたメンバーのみが台帳と対話できるためです。  

### ネットワークの作成
{: create_a_network}
ネットワークは以下のコンポーネントで構成されています。
* トランザクションを認証し、順序付けしてチャネルの台帳のブロックにまとめる処理を担当する順序付けサービス
* 各メンバーのネットワーク・コンポーネントの ID 資料の発行を担当するメンバー固有の認証局 (CA)
* トランザクションを実行およびコミットし、チャネル台帳を保守するメンバー固有のピア

ブロックチェーン・サービスのダッシュボードで、**「ネットワーク・クイック・スタート (Network Quick Start)」**ボタンをクリックし、ウィザードに従います。
1. **「ネットワークの名前を指定 (Name your Network)」**ページで、 ブロックチェーン・ネットワーク名と、自分のメンバー ID を表す会社名を入力し、**「次へ」**をクリックします。
2. 次の**「メンバーを招待 (Invite members)」**ページで、招待したい参加者の関連組織情報を指定します。それぞれに、ネットワークへの参加時にピアと CA がプロビジョンされ、すべてのネットワーク・メンバーが、参加したどのチャネルでも台帳を維持することになります。<br>
   **注:** ネットワークに最大 5 人までのメンバーを招待できます。
3. **「ガバナンス・ルールの定義 (Define Governance Rules)」**ページに、ネットワーク・ポリシー設定が表示されます。デフォルトでは、ネットワーク内のどのメンバーでも新規チャネルの作成とメンバーの招待を実行できます。  
4. **「証明書の生成 (Generate Certificate)」**ページで、**「自動生成 (Auto generated)」**オプションを使用して、組織のネットワーク・コンポーネントの証明書を作成します。これらの x509 証明書はユーザーに公開されていません。  
5. 最後に、**「サマリーの確認 (Review summary)」**ページでネットワークの構成を確認し、**「完了」**をクリックして、ネットワークをブートストラップします。

このプロセスにより、ネットワークの初期セットアップが完了します。

### ネットワークへの参加
{: invite_members}

ネットワークの初期化後に、自分が参加を招待されたネットワークおよび参加の手順を示す E メールが、招待されるメンバーに対して送信されます。招待されるメンバーの HSBN vNext プラン・ダッシュボードで**「保留中の招待 (Pending invites)」**ボタンが有効になります。ネットワークに参加するには、ボタンをクリックします。

1. リストでネットワークを選択し、**「ネットワークに参加 (Join Network)」**をクリックします。
2. 次の画面でガバナンス・ルールを確認し、**「次へ」**をクリックします。
3. **「証明書の生成 (Generate Certificate)」**ページで、組織名を入力し、**「自動生成 (Auto generated)」**オプションを選択します。
4. **「ネットワーク・サマリーの確認 (Review Network Summary)」**ページで、ネットワークの設定を確認し、**「完了」**をクリックします。設定には、ネットワークへの参加の招待を受け取った**「招待された参加者 (Invited Participants)」**も表示されます。

チャネルの作成およびチェーンコードのインストール/インスタンス化の手順については、『[モニター](v10_dashboard.html)』を参照してください。

<!-- I think all of this is adequately covered in the Monitor Section; and we already tell the story in the Sample Scenario topic above -->


<!-- From Jeff: Agreed. Commenting out all the rest sections on the page.


### Creating new channels
{: prepare_private_channels}

With the latest HSBN vNext plan, you can create a private channel, install a customized chaincode, complete the trade, and update the inventory number upon the other parties in the network make a query or propose a new transaction.

1. On the HSBN vNext plan dashboard, select **Enter Monitor**.
2. Select **Channels**, and click **New Channel**.
3. On the **Create a Channel** page, enter the channel name and choose the company that you want to make trade with by adding members. Then, click **Create** to create another private consortium channel.
4. Select **Chaincode** after you click the **Enter Monitor** button on the dashboard. You can view the chaincode that are already installed on your peer, or install a new chaincode to the peer.<br>
  **Note:** You can install at most 5 chaincode apps per peer.
5. Click **Install Chaincode** to install the smart contract to the peer. A smart contract, also known as chaincode, is the programmatic code installed and instantiated onto a channel’s peers by an appropriately authorized member. End users then invoke chaincode through a client-side application that interfaces with a network peer. Chaincode runs network transactions, which if validated, are appended to the shared ledger and modify world state. Chaincode can be developed for business contracts, asset definitions, and collectively-managed decentralized applications. You can download [this sample code](https://github.com/hyperledger/fabric/blob/master/examples/chaincode/go/marbles02/marbles_chaincode.go){: new_window} to your local environment for testing.

**Note:** After you install the chaincode onto the peer, you must instantiate the chaincode by providing the initial arguments. In the case of the Marbles sample chaincode, you can input `marble1, blue, 35` in a comma separated list to indicate that you have 35 blue marble1 for trade.


### Commencing transactions
{: commence_txs}

To make transactions within your network, the trading parties must:
* Join the same channel within the network.
* Install the same version of the chaincode onto the peer that represents each organization.


Each successful transaction results in a new block appended to the blockchain, and the ledger in the levelDB updated with the new state. Other members in the network can query the ledger or the transaction history to decide the next transaction.



### Monitoring your network
{: monitor_network}

You can perform the following tasks after you click the **Enter Monitor** button on the dashboard:
* Create new channels and invite other members to join your channels to trade privately.
* Install new chaincodes to your peer to initiate or participate into new trade.
* View the changes of blocks, transactions, chaincode invocations.
* View the log on your peer.
* View the information of resources that your organization owns.
* Export a JSON file containing the low-level networking information for each of your components (such as enrollID/enrollSecret for your CA).  

See the [HSBN vNext Beta dashboard](v10_dashboard.md) for more information about the usage of each panel on the dashboard. 


-->
