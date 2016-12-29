---

copyright:
  years: 2014, 2016
lastupdated: "2016-12-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}



# 管理存取權

存取控制清單可以用來管理服務的存取。[管理使用者](/docs/services/ObjectStorage/os_access_types.html)在管理服務實例時，可以授權讀取權和寫入權，以及移除存取權。
{: shortdesc}


可以使用 Swift CLI 或 Bluemix 使用者介面來管理存取控制清單。管理存取權之前，請確定您已配置服務且開始儲存物件。管理存取權時有一些事項要牢記。
  * 當使用者建立容器時，他們會自動被授與對該容器的管理專用權。
  * 存取控制清單不適用於服務實例、儲存空間帳戶，或無法在專案層次上使用。只能在容器層次管理存取權。
  * 請務必驗證已[移除](/docs/services/ObjectStorage/os_remove_access.html)對容器的存取權。
