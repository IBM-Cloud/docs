---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-13"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 應用程式連線

若要將應用程式連接至 {{site.data.keyword.iot_full}}，您必須使用 API 金鑰和記號來連接，或在 {{site.data.keyword.Bluemix_notm}} 中直接將應用程式連結至 {{site.data.keyword.iot_short_notm}}。您可以使用存取儀表板來授與存取權。
{:shortdesc}

## API 金鑰連線
{: #api-key}
將應用程式連接至 {{site.data.keyword.iot_short_notm}} 組織時，會使用 API 金鑰。應用程式需要有 API 金鑰才能連接至組織，而且要有必須與該 API 金鑰搭配使用的唯一鑑別記號。  

如需應用程式連線的相關資訊，請參閱開發人員文件中的[應用程式的 MQTT 連線功能 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://docs.internetofthings.ibmcloud.com/applications/mqtt.html){: new_window}。

若要建立新的 API 金鑰及鑑別記號配對，請執行下列步驟：  
1.	在 {{site.data.keyword.iot_short_notm}} 儀表板中，移至**應用程式 > API 金鑰**。  
2.	按一下**產生 API 金鑰**。  
  
**重要事項：**記下 API 金鑰和記號配對。鑑別記號是不可回復的。如果您遺失或忘記此記號，則需要重新登錄 API 金鑰，來產生新的鑑別記號。
 - API 金鑰的範例為 `a-organization_id-a84ps90Ajs`  
 - 記號的範例為 `MP$08VKz!8rXwnR-Q*`  
3.	新增註解，以在儀表板中識別 API 金鑰，例如：用來連接我的應用程式的金鑰。
4.	按一下**完成**。



## Bluemix 連結連線
{: #bluemix-binding}
您可以從 {{site.data.keyword.Bluemix_notm}} 將應用程式連結至 {{site.data.keyword.iot_short_notm}} 組織。透過連結應用程式，它就只能與相同空間或組織中的服務實例通訊。您可以在 VCAP_SERVICES 環境變數中，找到應用程式與服務實例通訊所需的全部資料。如果您的應用程式連結至多個服務，則 VCAP_SERVICES 變數會包含每一個服務實例的連線資訊。  

不過，您可以使用其他空間或組織中的服務實例，方法與外部應用程式相同。如果不建立連結，您可以使用認證來直接配置應用程式實例。如需相關資訊，請參閱 {{site.data.keyword.Bluemix_notm}} 文件中的[要求新的服務實例](https://console.{DomainName}/docs/services/reqnsi.html#req_instance)。

若要查看連結至與組織相關聯之 Bluemix 服務實例的 Bluemix 應用程式詳細資料，請移至**應用程式 > Bluemix 應用程式**。  
