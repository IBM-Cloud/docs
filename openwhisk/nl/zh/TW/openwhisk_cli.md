---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# {{site.data.keyword.openwhisk_short}} CLI

{{site.data.keyword.openwhisk_short}} 提供功能強大的指令行介面，允許完全管理系統的所有層面。

## 設定 {{site.data.keyword.openwhisk_short}} CLI 

您可以使用 {{site.data.keyword.openwhisk_short}} 指令行介面 (CLI) 來設定名稱空間及授權金鑰。移至[配置 CLI](https://new-console.{DomainName}/openwhisk/cli){: new_window}，並遵循指示進行安裝。

您必須設定兩個必要內容，才能使用 CLI：

1. 您要使用的 {{site.data.keyword.openwhisk_short}} 部署的 **API 主機**（名稱或 IP 位址）。
2. 授與您存取 {{site.data.keyword.openwhisk_short}} API 的**授權金鑰**（使用者名稱及密碼）。

執行下列指令，以設定 API 主機：

```
wsk property set --apihost openwhisk.ng.bluemix.net
```
{: pre} 

如果您知道您的授權金鑰，則可以配置 CLI 使用它。 

執行下列指令，以設定「授權金鑰」：

```
wsk property set --auth <authorization_key>
```
{: pre}

**提示：**依預設，OpenWhisk CLI 會將內容集儲存在 `~/.wskprops` 中。您可以透過設定 `WSK_CONFIG_FILE` 環境變數來變更此檔案的位置。 

若要驗證 CLI 設定，請嘗試[建立及執行動作](./index.html#openwhisk_start_hello_world)。

## 使用 {{site.data.keyword.openwhisk_short}} CLI

已配置環境之後，即可開始使用 {{site.data.keyword.openwhisk_short}} CLI 來執行下列動作：

* 在 {{site.data.keyword.openwhisk_short}} 上，執行您的程式碼 Snippet 或動作。請參閱[建立及呼叫動作](./openwhisk_actions.html)。
* 使用觸發程式及規則，讓動作回應事件。請參閱[建立觸發程式及規則](./openwhisk_triggers_rules.html)。
* 瞭解套件如何組合動作以及配置外部事件來源。請參閱[使用及建立套件](./openwhisk_packages.html)。
* 探索套件的型錄，以及使用外部服務（例如 [Cloudant 事件來源](./openwhisk_cloudant.html)）來加強應用程式。請參閱[使用啟用 OpenWhisk 功能的服務](./openwhisk_catalog.html)。

## 配置 CLI 以使用 HTTPS Proxy

CLI 可以設定成使用 HTTPS Proxy。若要設定 HTTPS Proxy，必須建立稱為 `HTTPS_PROXY` 的環境變數。變數必須設為 HTTPS Proxy 的位址，而其埠的格式如下：`{PROXY IP}:{PROXY PORT}`。
