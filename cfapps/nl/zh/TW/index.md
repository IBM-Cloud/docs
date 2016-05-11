---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc} 
{:new_window: target="_blank"}

# 建立 Cloud Foundry 應用程式
*前次更新：2016 年 4 月 18 日*

使用 {{site.data.keyword.Bluemix}}，即可在 {{site.data.keyword.Bluemix_notm}} 使用者介面中建立您的應用程式。建立之後，您可以決定要繼續使用使用者介面、使用 cf 指令行介面，還是使用 {{site.data.keyword.jazzhub_title}} 來開發、追蹤、計劃及部署您的應用程式。
{:shortdesc}

在 {{site.data.keyword.Bluemix_notm}} 中建立應用程式時，請從入門範本開始。*入門範本* 是一種範本，包括預先定義的服務，以及使用特定建置套件進行配置的應用程式碼。入門範本有兩種類型：樣板及執行時期。

*樣板* 是一種儲存器，它是針對應用程式及其相關聯執行時期環境，以及特定網域的預先定義服務。例如，Mobile Cloud 樣板包括 Node.js 執行時期，以及 Mobile Data、Mobile Application Security 和 Push 服務。此外，也包括 SDK 及範例應用程式，以便開始開發用來存取這些服務的行動式應用程式。

*執行時期* 是用來執行應用程式的資源集。{{site.data.keyword.Bluemix_notm}} 提供執行時期環境作為不同類型之應用程式的儲存器。執行時期環境會以建置套件的方式，整合到 {{site.data.keyword.Bluemix_notm}}，並會自動配置以供使用，且幾乎不需要維護。

若要開始建立您的應用程式，請採取下列步驟：
  1. 在 {{site.data.keyword.Bluemix_notm}} 使用者介面中，移至「儀表板」。
  2. 按一下**建立應用程式**。
  3. 按一下 **WEB**，然後遵循引導式體驗來選擇入門範本、指定名稱，並選取您想要用來撰寫程式碼的方式。
  4. 完成引導式體驗之後，按一下**檢視應用程式概觀**。應用程式的「概觀」會顯示在「儀表板」中。
  5. 您可以在 Bluemix 使用者介面中的應用程式「概觀」上，按一下**新增服務或 API**，以將服務新增至您的應用程式。從型錄中瀏覽並選取服務，或捲動至型錄結尾，然後按一下 **{{site.data.keyword.Bluemix_notm}} 實驗性服務**來瀏覽實驗性服務。或者，您可以使用 cf 指令行介面。請參閱「用於處理應用程式的選項」。
  6. 在應用程式「概觀」上，按一下「新增 Git」，以將您的應用程式原始檔儲存在 Git 儲存庫中，並建立由 Git 管理的專案。您也可以從 {{site.data.keyword.jazzhub_title}} 中部署應用程式。

**附註：**如果您連結至應用程式的服務損毀，應用程式可能會停止執行或發生錯誤。{{site.data.keyword.Bluemix_notm}} 不會自動重新啟動應用程式，以從這些問題中回復。請考慮撰寫應用程式碼，以識別運行中斷、異常狀況和連線失敗，並從其中回復。如需相關資訊，請參閱「應用程式不會自動重新啟動疑難排解」主題。

## 用於處理應用程式的選項

建立應用程式之後，有幾個選項可讓您繼續新增服務至應用程式，以及繼續建置並部署應用程式：

<dl><dt>cf 指令行介面</dt>
<dd>使用 cf 指令行介面來更新應用程式、建立服務實例，或將服務連結至應用程式。您也可以使用 cloud-cli 指令行介面來建立、更新及刪除服務供應項目。</dd>
<dt>{{site.data.keyword.Bluemix_notm}} user interface</dt>
<dd>使用 {{site.data.keyword.Bluemix_notm}} 使用者介面來建置應用程式，包括挑選要結合的服務和執行時期，以解決您的商業問題。</dd>
<dt>{{site.data.keyword.jazzhub_title}}</dt>
<dd>使用 {{site.data.keyword.jazzhub_title}} 在雲端中建立應用程式，並將其部署至 {{site.data.keyword.Bluemix_notm}}。{{site.data.keyword.jazzhub_title}} 所提供的服務包括 Track & Plan 和 Delivery Pipeline（列在 {{site.data.keyword.Bluemix_notm}}「型錄」的 DevOps 下），以及 Web IDE 和 Git Hosting。</dd>
</dl>

## 提示

開發 Web 應用程式請使用下列提示：

<dl><dt>持續性</dt>
<dd>請不要為您的應用程式指定任何本端儲存體。應用程式的每一個實例（即使只有一個實例在執行中）都可以隨時重新啟動，或移至不同的虛擬機器，這麼做一般是為了達到負載平衡。當移動或刪除該應用程式時，會一併消除儲存在本端儲存體中的所有內容。
請使用其中一個 Bluemix 資料儲存庫服務來持續保存。</dd>
<dt>資源限制</dt>
<dd>請注意試用帳戶可使用的資源數量限制。限制如下所示：<table style="width:100%">
  <th>資源類型</th>	<th>數量限制</th>
<tr><td>跨所有應用程式使用的服務數目</td> <td>10</td>
<tr><td>所有應用程式使用的記憶體</td> <td>	2 G</td>
<tr><td>路徑數目</td> <td>500</td>
</table>
</dd></dl>

*表 1. 試用帳戶的 {{site.data.keyword.Bluemix_notm}} 資源限制*
