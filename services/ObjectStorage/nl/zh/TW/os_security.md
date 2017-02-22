---

copyright:
  years: 2014, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}



# 管理存取權

存取控制清單可以用來管理服務的存取。[管理使用者](/docs/services/ObjectStorage/os_access_types.html)可以授與讀取權及寫入權，以及移除權。
{: shortdesc}

使用使用者介面或 Swift CLI 管理存取權之前，請確定您已配置服務且開始儲存物件。

使用存取控制清單時，請記住下列幾點：
  * 當使用者建立容器時，他們會自動被授與對該容器的管理專用權。
  * 存取控制清單不適用於服務實例、儲存空間帳戶，或無法在專案層次上使用。只能在容器或物件層次管理存取權。
  * 務必驗證已[移除](/docs/services/ObjectStorage/os_remove_access.html)對容器的存取權。
