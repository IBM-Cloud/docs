---

copyright:
years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Blockchain on z
{: #zblockchain}
前次更新：2016 年 7 月 8 日
{: .last-updated}



您可以使用 Bluemix 專用供應項目中的 Blockchain 服務搭配 z/OS，來建立私密且安全的數位資產，然後透過具有許可權的網路快速且安全地進行交易。*（其他資訊為簡要說明的一部分）*
{:shortdesc}


* 此內容量是否足以單獨一個小節？還是要將它當成「關於」下的內嵌主題？
* 預期 PBFT、「安全」、「效能」及「支援」的相關資訊。


## PBFT
{: #PBFT}

「實用拜占庭容錯 (PBFT)」是一項根據部署進行插入及配置的種子共識通訊協定。`obcpbft` 套件是種子 [PBFT](http://dl.acm.org/citation.cfm?id=571640 "PBFT") 共識通訊協定的實作，其提供驗證者之間的共識，而不管作為*拜占庭*（亦即，懷有惡意或以無法預期方式失敗）之驗證者的臨界值。在預設配置中，PBFT 及 Sieve 設計成在至少 *3t+1* 個驗證者（抄本）上執行，最多可容忍 *t* 個可能有缺陷（包括惡意或*拜占庭*）的抄本。若要進一步瞭解核心 PBFT 函數，請參閱 Linux Foundation 之 Hyperledger Project 的[通訊協定規格](https://github.com/hyperledger/fabric/blob/master/docs/protocol-spec.md#fabric)小節。 

觀看[![預覽](http://img.youtube.com/vi/EKa5Gh9whgU/0.jpg)](http://www.youtube.com/watch?v=EKa5Gh9whgU)

*（需要指出使用者必須知道 PBFT 的實際原因。PBFT 在 Blockchain on Z 支援中扮演的角色，以及其與此支援的關係。）*


### 支援的失敗案例
{: #failure}

*這裡說明支援的失敗案例及不支援的失敗案例。*

*（Barry Mosakowski/Raleigh/IBM 或 Tuan Dang/Raleigh/IBM 可以提供更多詳細資料。）*

### z/OS 的專用供應項目可用性
{: #Availability}

*根據 PBFT 測試的可用性及可用性預期。*

*（需要更多詳細資料。）*

### 驗證 PBFT 的基本功能
{: #Test PBFT}

*（Gari 的輸入。需要 Jason 有關如何執行測試步驟（包括擷取畫面）的更多詳細資料。）*

若要驗證基本 PBFT 功能，請採取下列步驟：

1. 針對網路中的一個以上對等節點，提交交易。
2. 驗證至少有 *2f+1* 個（在此情況下，為 3 個）對等節點的狀態相同。*（如何驗證？需要測試案例詳細資料。）*

  *使用 REST API 的範例*
3. 在儀表板上，按一下按鈕以停止對等節點 4。*（使用儀表板中的「停止對等節點」功能來停止對等節點 4。需要測試案例來說明詳細作業。）*
4. 驗證網路繼續處理。*（如何驗證？）*
5. 在儀表板上，按一下按鈕以停止對等節點 3。
6. 驗證網路停止處理。
7. 在儀表板上，按一下按鈕以重新啟動對等節點 3。

如果對等節點 3 擷取並更新，且網路繼續處理，您可以使用基本 PBFT 功能。

**附註：**
* 重新啟動對等節點 3 之後，您需要等待逾時，然後才能將新的交易提交給對等節點 3。

* 在網路停止處理時傳送至作用中對等節點的交易會放入緩衝區中，並在網路繼續處理之後提交至網路。

## Blockchain on Z 的環境
{: #z environment}

若要使用 Bluemix 專用供應項目中的 Blockchain 服務搭配 z/OS，請確定您的環境符合下列需求：

* 執行 PBFT 與成員資格服務的四個對等節點的網路。若要進一步瞭解成員資格服務，請參閱 Linux Foundation 之 Hyperledger Project 的[通訊協定規格](https://github.com/hyperledger/fabric/blob/master/docs/protocol-spec.md#fabric)小節。 
* 沒有共用電腦或記憶體的隔離網路。
* 網路內的隔離對等節點。
* 受到保護而使雲端系統管理者無法存取的系統。

區塊鏈監視器提供區塊鏈環境的概觀，並且會擷取關於您網路的詳細資料。若要進一步瞭解區塊鏈環境及其監視方式，請參閱[使用區塊鏈監視器管理鏈碼](https://new-console.ng.bluemix.net/docs/services/blockchain/ibmblockchainmonitor.html)及[區塊鏈的範例應用程式及指導教學](https://new-console.ng.bluemix.net/docs/services/blockchain/ibmblockchain_tutorials.html)。

## 安全

*不在文件中提供安全資訊嗎？*

## 效能

*不在文件中提供效能資訊嗎？*

## 取得客戶支援

如果您使用 Bluemix 專用供應項目中的 Blockchain 服務搭配 z/OS 時遭遇問題，請遵循 IBM Bluemix 疑難排解程序。如需如何取得協助的相關資訊，請參閱[疑難排解](https://new-console.ng.bluemix.net/docs/troubleshoot/troubleshoot.html)。
