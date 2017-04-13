---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-16"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 新增功能
{: #whatsnew}

**HSBN vNext 測試版**方案是以 [Hyperledger Fabric 1.0 版](https://www.hyperledger.org/){:new_window}開放程式碼庫的穩定確定為建置基礎。Hyperledger Fabric 1.0 版會實作模組架構，以提供具復原力、安全且可自訂的平台來建置企業區塊鏈網路。  
{: shortdesc}

**HSBN vNext 測試版**服務會移至單一沙盤推演環境，以提供具有跨各種 Bluemix 組織的資源群組的分散式區塊鏈網路。如需網路架構的相關資訊，請參閱[概觀](v10_netoverview.html)主題。

## 1.0 版的新架構
{:why}

Hyperledger Fabric 架構已在 1.0 版中大幅發展，讓企業級網路聚焦於安全、可擴充性、機密性及效能。對等節點分成兩個特殊運行環境（**背書**及**確定**），而且交易排序的責任會擷取到不同的元件。透過通道提供資料隔離，即可處理隱私權及機密性問題。每個通道都會有分類帳，因此可以自訂網路來支援雙方、多方甚至公開交易的不同組合。

如需網路拓蹼及互動的相關資訊，請檢視 [Hyperledger 架構深入探討](http://hyperledgerdocs.readthedocs.io/en/latest/arch-deep-dive.html){: new_window}小節。

## 其他變更

「HSBN vNext 測試版」方案也包括下列變更：
* [新的儀表板](v10_dashboard.html)容許訂閱者建立區塊鏈網路、邀請成員、加入另一個網路，以及管理資源和資產。
* [1.0 版的新大理石範例鏈碼應用程式](https://github.com/hyperledger/fabric/blob/master/examples/chaincode/go/marbles02/marbles_chaincode.go){: new_window}可啟用具有最新程式碼庫的實驗。
* Hyperledger Fabric 1.0 版中的新[交易流程](http://hyperledger-fabric.readthedocs.io/en/latest/txflow.html)透過在整個交易程序中實作多個檢查點，來確保資料一致性及完整性。
