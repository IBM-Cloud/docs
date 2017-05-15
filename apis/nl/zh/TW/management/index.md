---

copyright:
  years: 2017
lastupdated: "2017-04-12"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 概觀
{: #index}

您可以在 {{site.data.keyword.Bluemix}} 中透過原生方式管理 API，不論它們是與 {{site.data.keyword.openwhisk_short}} 動作相關聯，還是與不斷加長的整合式 {{site.data.keyword.Bluemix_notm}} 服務（例如 {{site.data.keyword.appconserviceshort}} 服務）清單相關聯。管理 API 可讓您控制用量、增加採用，以及追蹤統計資料。

如下圖所示，API Management 的運作方式是在現有雲端端點前面插入快速且輕量的閘道。閘道（在圖中稱為「API 閘道」）負責回應來自應用程式的送入 API 呼叫。「API 閘道」提供一組綜合性 API 原則來提供安全、資料流量管理、調解、加速及非 HTTP 通訊協定支援。

![「API 閘道」流程。](images/bluemix-native-apim-flow_ow.png "API Management 流程。")

當您公開 API 時，表示將它設定為可供其他人使用。這通常表示讓 API 的使用者對您維護的伺服器上的資訊進行有限的存取。此存取能讓一般使用者有更流暢的客戶體驗，因為他們可以直接從現行介面存取資訊。

您有時候會想要控制伺服器上的一些活動。例如，如果伺服器上在短時間有太多 API 要求，則伺服器可能會超載並關機。若要避免這類狀況，您可以使用 API Management 來管理 API 呼叫率。連接至 API 的輕量型閘道會追蹤 API 的呼叫數目，並強制限制所接受的呼叫數目。API Management 也可讓您藉由記錄特定來源的 API 金鑰，而追蹤來自該來源的 API 呼叫量。API 金鑰是 API 開發團隊提供給 API 使用團隊的唯一字串，可以讓 API 開發人員監視使用團隊要求所產生之呼叫的統計資料。  

{{site.data.keyword.Bluemix_notm}} API Management 提供下列特性：
## API 分析
{: #basic_analytics notoc}

如果您要將 API 用量換算成貨幣，可以使用分析特性來追蹤呼叫用量。您也可以監視用量，以瞭解 API 使用情形，讓您在有足夠資訊的情況下做出如何更新 API 來增加採用的決策。

您可以檢視 API 的下列統計資料：
* 最後一小時或所指定時間間隔的回應數目及平均回應時間。
* 每分鐘的 API 呼叫數目。
* 最後 100 個回應。

## 訂閱的比率限制（API 金鑰）
{: #rate_limit notoc}

您可以強制執行比率限制，來管理應用程式可對 API 進行的呼叫數目。您可以指定比率限制，以限制每秒、每分鐘、每小時只能進行允許的呼叫數目，舉例來說，以便後端不會超載。設定此作業的方式是根據整體 API 或每一個 API 金鑰。

## OAuth
{: #oauth notoc}

若要停止對您所提供資料的不當使用，您可以確定只有具有正確鑑別的使用者才能存取您的 API。您可以透過 OAuth 授權標準來控制對 API 的存取。OAuth 是記號型授權通訊協定，容許第三方網站或應用程式存取使用者資料，而不需要使用者分享個人資訊。

## CORS
{: #cors notoc}

CORS 容許內嵌在網頁中的 Script 能跨網域界限來呼叫 API。這有利於 API 使用者，因為它容許 API 在呼叫它時擷取另一個網域中的資訊。若未啟用 CORS，則會將任何內容擷取都限制為與起源要求相同的網域。如需 CORS 及其實作方式的相關資訊，請參閱 [HTTP access control (CORS) ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.mozilla.org/en-US/docs/Web/HTTP/Access_control_CORS.html){: new_window}。

## 其他 API Management 選項
{: #add_mgt_options notoc}

{{site.data.keyword.openwhisk_short}} 或 App Connect 儀表板的 API Management 標籤中提供這些 API Management 特性。如需較複雜的管理解決方案，您可以升級為完整 {{site.data.keyword.apiconnect_full}} 服務，以存取其他特性，例如詳細分析、API 的包裝策略或開發人員入口網站，以便將 API 社交化。如需 {{site.data.keyword.apiconnect_full}} 服務的相關資訊，請參閱[開始使用 API Connect](https://console.ng.bluemix.net/docs/services/apiconnect/index.html){: new_window}。

如需將 {{site.data.keyword.Bluemix_notm}} 中您管理之 API 升級為 {{site.data.keyword.apiconnect_short}} 服務的相關資訊，請參閱[存取其他 API Management 特性](upgrade.html)。

