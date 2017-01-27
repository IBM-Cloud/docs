---

copyright:
  years: 2014, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# 管理物件

您可以使用 Swift CLI、API 或 Bluemix 使用者介面來管理物件和容器。
{: shortdesc}

在可以管理物件之前，請確定您已[鑑別](/docs/services/ObjectStorage/os_authenticate.html)您的服務實例、[產生](/docs/services/ObjectStorage/os_credentials.html)服務認證，並[配置](/docs/services/ObjectStorage/os_configuring.html) Swift CLI。

管理物件時，請記住下列幾點：
  * 您可以儲存的資料量沒有限制，但每次上傳不得超過 5 GB。如果您需要上傳大於 5 GB 的檔案，請遵循[儲存大型物件](/docs/services/ObjectStorage/os_large_files.html)中的步驟。
  * Swift 沒有真正的目錄結構，但您可以新增[現有目錄](/docs/services/ObjectStorage/os_directories.html)到您的指令。
  * 為了避免意外改寫檔案，請[設定物件版本化](/docs/services/ObjectStorage/os_versioning.html)。
  * 您可以[排定時間](/docs/services/ObjectStorage/os_deletion.html)來刪除物件。
