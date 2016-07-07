---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 配置 {{site.data.keyword.mobilefoundation_short}} 伺服器的自訂網域
{: #configcustomdomain}

*前次更新：2016 年 6 月 15 日*
{: .last-updated}

{{site.data.keyword.mobilefoundation_short}} 在 {{site.data.keyword.containerlong}} 佈建一個 {{site.data.keyword.mfserver_short_notm}} 作為容器群組。容器群組將對映到一個 URL，其網域名稱是根據 {{site.data.keyword.Bluemix_notm}} **地區**。您也可以自行配置自訂網域。
{:shortdesc}

容器群組建立時的 URL 或路徑，預設網域名稱是根據 {{site.data.keyword.Bluemix_notm}} `地區`。

*表 1. 應用程式網域名稱，根據 {{site.data.keyword.Bluemix_notm}} 中的地區*

  |網域 |  地區  |    
  |:----- | :----- |    
  |`mybluemix.net` | 美國達拉斯  |    
  |`eu-gb.mybluemix.net` | 英國倫敦  |    
  |`au-syd.mybluemix.net`  | 澳洲雪梨 |  

您需要執行下列步驟配置自訂網域，才能使用自己的網域：

1.	藉由選擇其中一個支援的方案，建立 {{site.data.keyword.mobilefoundation_short}} 服務實例來建立 {{site.data.keyword.mfserver_short_notm}} 實例。

+ 將您想要使用的自訂網域，新增至您的 {{site.data.keyword.Bluemix_notm}} `組織`。移至**管理組織 > 網域 > 新增網域**，以新增您自己的網域。

+ 設定容器群組的路徑以使用您的自訂網域。

+ 移至網域的 DNS 提供者，然後新增 CNAME 項目，它會將您網域的資料流量遞送到預設的 {{site.data.keyword.Bluemix_notm}} 路徑，容器群組便在其中執行。

+ 如果您想要為自訂網域配置 `https`，則請在 {{site.data.keyword.Bluemix_notm}} 中上傳網域的 SSL 憑證。若要這麼做，請移至**管理組織 > 網域**、選取您要配置 SSL 憑證的自訂網域、按一下**上傳憑證**來上傳網域的 SSL 憑證。如需相關資訊，請參閱 [SSL Certificates and Bluemix Custom Domains](https://developer.ibm.com/bluemix/2014/09/28/ssl-certificates-bluemix-custom-domains/)。
