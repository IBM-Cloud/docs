---

copyright:
  years: 2016
lastupdated: "2016-10-06"

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# 疑難排解
{: #troubleshooting}

以下是關於在 {{site.data.keyword.Bluemix_notm}} 上使用 {{site.data.keyword.iotinsurance_full}} 的常見疑難排解問題解答。
{:shortdesc}

## 部署應用程式時的問題
{: #deployingapps}

如果在 {{site.data.keyword.Bluemix_notm}} 組織中沒有足夠的記憶體，您可能無法部署 {{site.data.keyword.iotinsurance_short}} 的應用程式。您可以減少應用程式使用的記憶體，或是增加帳戶的記憶體配額。

### 發生什麼事

當您開啟 {{site.data.keyword.iotinsurance_short}} 服務時，未啟用「部署」功能，且您無法部署任何應用程式。

### 發生的原因

您的組織必須有至少 2 GB 的可用記憶體，才能啟用「部署」功能。試用帳戶的記憶體配額上限為 2 GB。如果您建立了非 {{site.data.keyword.iotinsurance_short}} 的服務或應用程式，您的組織便沒有足夠的記憶體可部署 {{site.data.keyword.iotinsurance_short}} 應用程式。

### 如何修正

您可以增加帳戶的記憶體配額，或是減少服務及應用程式使用的記憶體。

  - 若要增加帳戶的記憶體配額，您可以[將試用帳戶轉換成付費帳戶](https://console.ng.bluemix.net/docs/pricing/index.html#pay-accounts)。

  - 若要快速減少使用中的記憶體，請移除非 {{site.data.keyword.iotinsurance_short}} 的所有服務及應用程式。重新啟動 {{site.data.keyword.iotinsurance_short}} 服務，讓變更生效。

  - 針對具有超過 2 GB 總記憶體的付費帳戶，您可能可以藉由調整其他應用程式或服務使用的記憶體量而避免移除它們。如需相關資訊，請參閱[已超出組織的記憶體限制](https://console.ng.bluemix.net/docs/troubleshoot/ts_apps.html#ts_outofmemory)。
