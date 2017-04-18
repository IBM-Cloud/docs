---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:new_window: target="_blank"}

# 開發應用程式 
{: #develop-apps-IDS}

*前次更新：2015 年 12 月 7 日*  

您可以使用整合開發環境 (IDE) 或文字編輯器來開發應用程式，或是使用 {{site.data.keyword.jazzhub}}。
{: shortdesc}

## 使用 Bluemix DevOps Services 開發應用程式
{: #dev_ops}

您可以使用 {{site.data.keyword.jazzhub_short}} 在雲端中開發、追蹤和計劃應用程式，然後將其部署至 {{site.data.keyword.Bluemix_notm}}。只要幾分鐘，就可以從原始碼變成執行中的應用程式。  

{{site.data.keyword.jazzhub_short}} 提供兩項服務：{{site.data.keyword.trackplan}} 及 {{site.data.keyword.deliverypipeline}}。{{site.data.keyword.trackplan}} 服務適用於敏捷規劃。{{site.data.keyword.deliverypipeline}} 服務可自動化建置和部署。您可以在 {{site.data.keyword.Bluemix_notm}}「型錄」中找到這些服務。若要進一步瞭解如何使用它們，請參閱[開始使用 Track & Plan](../services/TrackPlan/index.html#gettingstartedtemplate) 及[開始使用 Delivery Pipeline](../services/DeliveryPipeline/index.html#getstartwithCD)。 

{{site.data.keyword.jazzhub_short}} 也提供適用於原始檔控制的 Git Hosting，以及可用來編輯、管理和部署程式碼的 Web IDE。在應用程式中，按一下**新增 GIT** 鏈結（位於應用程式「概觀」頁面的右上角），以啟用 Git Hosting。然後，您可以按一下**編輯程式碼**，以在 Web IDE 中編輯應用程式的程式碼。從 Web IDE Shell 中，您可以利用內容輔助來執行 cf 指令。例如，只要鍵入下列指令，即可取得所有 Cloud Foundry 指令的清單：  
```
help cfo
```
{:pre}
