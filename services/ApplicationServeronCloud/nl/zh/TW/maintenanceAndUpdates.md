---

copyright:
  years: 2015, 2016
lastupdated: "2017-02-24"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 維護及 VM 更新項目
{: #maintenance_and_vm_updates}

## 維護策略
{: #maintenance_strategy}

會定期更新 IBM WebSphere Application Server in Bluemix，確保使用現行修正套件及修補程式來建立新的服務實例。雲端為中介軟體管理帶來了輕鬆而快速的新服務實例佈建。我們預期許多消費者會在想要套用維護時升級至新的服務實例。針對那些要保留長期存留之服務實例的消費者，會有中介軟體及基礎作業訪客可用的維護儲存庫。這些儲存庫讓使用者能維護其環境，就像使用內部部署時一樣。

## VM 更新項目

下列區段說明如何套用虛擬機器系統的變更。

您可以像任何其他一般 RHEL 系統一樣更新 VM。藉由使用 Red Hat 套件管理程式 "Yum"，您可以安裝、更新、解除安裝套件，以及對它們進行各種其他的作業。

您的系統已設定為從 IBM 的 Red Hat Satellite Server 接收這些更新項目。這個衛星提供您來自 Red Hat Network 的 Yum 套件管理程式的安全套件。

Satellite Server 由 IBM 管理，且無法從您的系統修改。

如需相關資訊，請參閱 [Applying package updates on Red Hat Enterprise Linux 6](https://access.redhat.com/articles/11258#rhel6){: new_window} 及 [Yum](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/ch-yum.html){: new_window}（Red Hat 套件管理程式）。
