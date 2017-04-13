---

copyright:
  years: 2017
lastupdated: "2017-03-07"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# HSBN 已知問題
{: #etn_overview}



已報告下列 HSBN 方案問題：

1. 當使用「高安全性商業網路」，而其會使用 Hyperledger Fabric 0.6.1 版時，如果有超過大約 50 個的 chaincode 部署，建議在開發階段期間定期重設網路。重設網路會移除已部署的 chaincode 及已收集的資料。這讓您有機會移除在反覆運算式開發階段期間為了改善而被取代的舊版 chaincode。如果您是在後置開發階段，則應該監視 chaincode 部署數目，以留下最重要 chaincode 的容量。
2. 執行網路及對等節點的狀態查詢時，收到偶發的「503 服務無法使用」及「502 閘道不正確」錯誤。
3. vp1 的日誌中可能出現「Server.Serve 無法完成安全信號交換」訊息。這是不嚴重的錯誤，而且與網路作業無關。
4. **服務認證**可能無法自行移入；在此情況下，請依下列方式產生認證：

 a) 從「服務儀表板」中，按一下**服務認證**標籤：

  ![服務認證 HSBN](images/hsbn.png "服務認證 HSBN")

 b) 從**服務認證**標籤中，按一下**新建認證**的按鈕：

  ![新建認證 HSBN](images/hsbn1.png "新建認證 HSBN")

c) 即會顯示標題為**新增認證**的新視窗；按一下此視窗底端的**新增**按鈕：

  ![新增認證 HSBN](images/hsbn2.png "新增認證 HSBN")

 d) 現在您的畫面看起來應該與下列範例類似。按一下**檢視認證**將顯示 JSON 有效負載，其中包含 HSBN 實例的「服務認證」。  

  ![已產生認證 HSBN](images/hsbn3.png "已產生認證")


## 取得協助

如需 IBM Blockchain on Bluemix 網路的支援及協助，請參閱[取得支援](ibmblockchain_support.html)。
