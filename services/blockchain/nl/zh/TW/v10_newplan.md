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


# 高安全性商業網路 (HSBN) vNext 測試版
{: #etn_overview}

**HSBN vNext 測試版**提供一種可立即啟用的解決方案，來產生區塊鏈商業網路。此服務會快速佈建網路，並提供監視器來輕鬆管理及維護資源。這個形成及控管網路的直接明確程序，讓您可以將更多的時間和注意力放在開發及部署商業解決方案。
{:shortdesc}

**HSBN vNext 測試版**網路是在 LinuxONE 的高安全環境中執行，在此環境中，網路資源（對等節點、排序節點、憑證管理中心、原始碼、分類帳）都包含在 **IBM Secure Service Container** (SSC) 內。特性包括：
* 對等式通訊的效能最佳化
* 高可用性及可擴充性架構 
* 硬體加密、防竄改加密金鑰及安全加密虛擬機器
* 具有防竄改軟體的安全啟動
* 無 root 存取權
* FIPS 相符性、高 EAL 保護、審核性及加密最佳化

訂閱 **HSNB vNext 測試版**方案支援下列網路資源：

- 損毀容錯排序服務
- 每個成員有 2 個對等節點
- 最多 5 個額外的網路成員
- 每個成員有 5 個實例化鏈碼
- 成員特定憑證管理中心
- 最多 100 個通道
- 預設控管原則（所有成員都是管理者，因此可以發出加入網路的邀請）

如需環境安全特性的詳細資料，請參閱 [IBM Secure Service Container](etn_ssc.html) 小節。

## 使用 HSBN vNext 測試版方案
{: #use_hsbn}

### 方案存取

IBM Blockchain on Bluemix **HSBN vNext 測試版**方案是依要求授與。當您從「Bluemix 型錄」中選取「HSBN vNext 測試版」並建立服務實例時，會將您參與最新測試版的要求傳送給 IBM Blockchain 團隊。核准之後，您將會接收到參與方案的電子郵件邀請；請遵循指示來啟動「HSBN vNext 測試版」方案儀表板。

在「HSBN vNext 測試版」儀表板上，從以下三個選項中進行選取：
1. **網路快速入門**：建立「HSBN vNext 測試版」網路，並邀請其他「Bluemix 組織」加入。
2. **加入網路**：檢視讓您加入其他「HSBN vNext 測試版」網路的邀請。
3. **監視器網路**：管理您的網路資源：對等節點、通道及鏈碼。

<!-- to do - the rest of this page final edit -->

### 範例情境

假設您是大理石製造商，並且想要運用 IBM Blockchain 網路與不同的供應商進行交易。運作方式為何？您可以建立包含所有網路成員的聯盟通道，以及公開可用大理石儲存庫的現行狀態。網路上的所有成員都可以看到及查詢在此通道上進行的任何交易。不過，您也可以建立「次通道」或獨立式通道，以符合隱私權及機密性需求。例如，如果特定供應商符合一組特定條件，則會將更好的價格提供給他們。此交易可以在次通道上進行，進而影響聯盟通道上所更新的整體大理石供應。或者，您可能想要交易聯盟通道上未提供的特定類別的大理石。您只要與獨立式通道的必要當事人交易，聯盟通道的分類帳將不受影響。通道提供一個功能強大的隱私權機制，因為它們都會有唯一分類帳，而且只有訂閱及鑑別通道的成員才能與分類帳互動。  

### 建立網路
{: create_a_network}
網路包含下列元件：
* 排序服務，負責鑑別交易並將它們排序到通道的分類帳區塊。
* 成員特定憑證管理中心 (CA)，負責發出每一個成員的網路元件的身分資料。
* 成員特定對等節點，可執行及確定交易並維護通道分類帳。

在區塊鏈服務的儀表板上，按一下**網路快速入門**按鈕，並遵循精靈：
1. 在**命名網路**頁面上，輸入將代表您成員身分的區塊鏈網路名稱及公司名稱，然後按**下一步**。
2. 在下一個**邀請成員**頁面上，指定您想要邀請的參與者的相關組織資訊。每一項都會在加入網路時獲佈建一個對等節點及憑證管理中心，而且所有網路成員都會針對任何他們已加入的通道維護一個分類帳。<br>
   **附註：**您最多可以邀請 5 位成員加入網路。
3. 在**定義控管規則**頁面上，您將會看到網路原則設定。依預設，網路中的任何人都可以建立新的通道，並邀請成員。  
4. 在**產生憑證**頁面上，使用**自動產生的**選項來建立您組織的網路元件的憑證。這些 x509 憑證不會向使用者公開。  
5. 最後，在**檢閱摘要**頁面上，檢閱網路的配置，然後按一下**完成**來引導網路。

這個程序會完成網路的起始設定。

### 加入網路
{: invite_members}

起始設定網路之後，受邀者將會接收到一封電子郵件，指出您獲邀加入的網路及加入指示。受邀者將會看到 HSBN vNext 方案儀表板上已啟用**擱置邀請**按鈕。按一下此按鈕，以加入網路：

1. 選取清單上的網路，然後按一下**加入網路**。
2. 在下一個畫面上，檢閱控管規則，然後按**下一步**。
3. 在**產生憑證**頁面上，輸入「組織名稱」，然後選取**自動產生的**選項。
4. 在**檢閱網路摘要**頁面上，檢閱網路的設定，然後按一下**完成**。這些設定也會顯示已收到加入網路邀請的**受邀參與者**。

如需建立通道以及安裝/實例化鏈碼的指示，請參閱[監視器](v10_dashboard.html)。

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
