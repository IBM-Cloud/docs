---



copyright:

  years: 2016, 2017
lastupdated: "2017-05-02"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# IBM {{site.data.keyword.Bluemix_notm}} 標準帳戶測試版 
{: #betaintro}

{{site.data.keyword.Bluemix}} 標準帳戶測試版引進了新的免費帳戶，提供新的方式來在 {{site.data.keyword.Bluemix_notm}} 公用雲端工作。標準帳戶永不到期，不像 30 天的 {{site.data.keyword.Bluemix_notm}} 試用。您可以繼續使用 {{site.data.keyword.Bluemix_notm}} 應用程式，而不必擔心時間限制。
{:shortdesc}

參與標準帳戶測試版只能依據邀請。在您接受邀請並建立標準帳戶之後，可以邀請朋友和同事來參與測試版。  

## {{site.data.keyword.Bluemix_notm}} 標準帳戶簡介
{: #standardaccount}

您可能好奇標準帳戶與試用帳戶相較有何差別。下表彙總關於 {{site.data.keyword.Bluemix_notm}} 標準帳戶的重要詳細資料。 

|標準帳戶的新增功能 |    
|-----------------|
| 帳戶永不到期。 |
| Cloud Foundry 應用程式可以同時存取最多 256 MB 的免費運行環境記憶體。 |
| 您可以存取免費的 Cloudant NoSQL DB 和 Internet of Things Platform 精簡方案，並且即將推出更多服務。 |
| 如果長達 10 天沒有開發活動，您的應用程式將會休眠。 |
| 您的服務實例會在 30 天無活動之後刪除。 |
{:caption="表 1. 標準帳戶的新增功能" caption-side="top"}

|試用帳戶轉換時有哪些事情維持不變？ | 
|-----------------|
|帳戶免費 -- 您不需要信用卡。 |
|Cloudant NoSQL DB 和 Internet of Things Platform 的任何精簡實例。這些服務每一項都可以有一個精簡實例轉移到您的新帳戶。 |
|您的組織、空間及相關聯的團隊成員存取設定會維持相同。可以有一個組織轉移到您的新帳戶。 |
|{{site.data.keyword.Bluemix_notm}} 支援層次維持相同。 |
{:caption="表 2. 未變更的內容" caption-side="top"}

**附註**：如果您的試用帳戶未轉換，您會看到一則解釋原因的訊息。您的現有試用帳戶中可能有多個組織，或是無法轉移的應用程式。您可以採取適當的動作，然後嘗試重新轉換帳戶。

註冊標準帳戶之後，您可以邀請團隊成員在您的組織及空間中分工合作、檢視您的用量、建立空間、更新帳戶設定檔，以及管理組織。如需相關資訊，請參閱[管理帳戶](/docs/admin/adminpublic.html#account)。

## 精簡方案
{: #liteplans}
   
精簡方案也提供於隨收隨付制帳戶，其結構是免費配額。您可以安心使用專案，而不會有產生意外帳單的風險。配額可能會運作一段特定時間，例如一個月，或是根據一次性的使用而運作。以下是精簡方案配額的部分範例：

<ul>
<li>已登錄裝置的數目上限。</li>
<li>應用程式連結的數目上限。</li>
<li>加密資料儲存空間限制，例如 1 GB。</li>
<li>已佈建的傳輸容量。</li>
</ul> 

在標準帳戶中，您可以使用 {{site.data.keyword.Bluemix_notm}} 型錄中有精簡方案的所有項目。精簡方案很容易找。依預設，當您開啟型錄時，具有精簡方案的所有服務會顯示，並標示精簡標記 ![精簡標記](../icons/Lite.svg)。請選取服務，以檢視相關聯精簡方案的詳細資料。

## 標準帳戶的可用功能
{: #whatsavailable}

在標準帳戶中，Cloud Foundry 應用程式可以同時存取最多 256 MB 的運行環境記憶體。如果超過您的配置配額，您可以停止部分應用程式，以釋放運行環境記憶體。 

在標準帳戶測試版期間，下列服務提供精簡方案：

<ul>
<li>Cloudant NoSQL DB</li>
<li>Internet of Things Platform</li>
</ul>

我們將新增至這份服務清單，因此請持續留意！

達到配額限制時，會停止您的應用程式，或是停用您的服務。如果精簡方案指定配額是以月為基準提供，資源用量會在每月一日重設，您便可以繼續使用該服務。當您接近配額限制，或是已達到配額限制時，您會收到一封通知電子郵件。 

您可以針對每個精簡方案佈建 1 個實例。 

**附註**：這些限制僅適用於標準帳戶。您隨時都可以升級到隨收隨付制或訂閱計費帳戶。您只需要為您使用超過免費額度的部分付費。如需「隨收隨付制」及「訂閱」帳戶的相關資訊，請參閱[帳戶類型](/docs/pricing/index.html#pay-accounts)。

## 開發活動
{: #devactivity}

為了協助標準帳戶使用者最妥善地管理資源，我們建置了一些以開發活動和用量為基礎的效率特性：

 * 您的應用程式沒有開發活動長達 10 天之後將會進入休眠。這在您想要處理新應用程式時很有用，因為您不會達到 256 MB 記憶體配額限制。若要喚醒應用程式，請在 Cloud Foundry 指令行或 {{site.data.keyword.Bluemix_notm}} 主控台再度開始使用它們。 
 
 以下列出將喚醒應用程式的所有指令：
  * cf push
  * cf restate
  * cf restart
  * cf ssh
  * cf scale
  * cf stop
  * cf start
  * cf create-route
  * cf map-route
  * cf unmap-route
  * cf delete-route
  * cf enable-ssh
  * cf disable-ssh

 **附註**：如果您的應用程式已啟用 ssh，則 `cf enable-ssh` 及 `cf disable-sh` 指令將不會喚醒您的應用程式。 

 * 如果您的精簡方案服務沒有活動的時間長達 30 天，便會刪除。因此您想要建立新實例時不必刪除無活動的實例。現在只有 Internet of Things Platform 服務使用此特性。 
 
 登入 Internet of Things Platform 服務實例儀表板即可維持 Internet of Things Platform 精簡實例在作用中。
 
## 參與標準帳戶測試版
{: #betainvitation}

如果您獲選參與測試版，會有一封邀請寄到與您 {{site.data.keyword.Bluemix_notm}} 試用帳戶相關聯的電子郵件位址。收到邀請之後，請完成電子郵件中的指示，註冊標準帳戶。 

有興趣參與標準帳戶測試版？問問您的朋友和同事吧。如果他們已受邀加入測試版，並建立了標準帳戶，他們也可以邀請您。 
