---

copyright:
  years: 2016, 2017
lastupdated: "2016-10-13"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 高安全性商業網路
{: #etn_overview}


IBM Blockchain「高安全性商業網路」是在隔離且高度安全的環境中執行，這讓它與其他雲端管理的供應項目不同。作業系統、網狀架構及節點全部存在於 IBM Secure Service Container，可提供企業客戶預期從 z Systems 技術獲得的安全與屹立不搖等級。IBM Secure Service Container 也會提供對等式通訊、可用性、可擴充性、硬體加密、防竄改加密金鑰以及安全加密 VM 等的效能最佳化。  
{:shortdesc}

環境 (LinuxONE on z) 包含有四個對等節點、實作 PBFT 並啟用「成員資格服務」的網路，並且是在應用程式容器中執行。應用程式容器會保護在系統內執行的區塊鏈軟體、鏈碼及資料。可以簽署、認證及加密安全啟動內的區塊鏈軟體；而且一旦安裝在應用程式容器中之後即不可竄改。平台的 root 使用者及系統管理者無法存取或查看安全容器內容。LinuxONE on z 提供 FIPS 相符性、高「評估保證層次」保護、高度可審核的作業環境，以及加密最佳化。

如需安全特性的詳細資料，請參閱 [IBM Secure Service Container](etn_ssc.html) 小節。
