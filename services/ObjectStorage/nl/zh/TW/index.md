---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-11"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}



# 開始使用 {{site.data.keyword.objectstorageshort}}  {: #getting-started-with-object-storage}


{{site.data.keyword.objectstoragefull}} 提供非結構化雲端資料儲存空間。您可以儲存及存取內容，以及透過互動方式組合及連接至應用程式和服務。
{: shortdesc}

{{site.data.keyword.objectstorageshort}} 服務的一些常見使用案例如下：

* 從您的實例備份磁區資料
* 用來作為傳送大量資料時的媒介位置
* 在未直接連接的環境之間傳送資料
* 充當中央儲存庫


「{{site.data.keyword.Bluemix_notm}} 公用 {{site.data.keyword.objectstorageshort}}」可讓您存取完整佈建的 Swift {{site.data.keyword.objectstorageshort}} 帳戶，以管理您的資料。並不提供提供者端加密。


1.	從 {{site.data.keyword.Bluemix_notm}} 型錄中佈建服務實例。請配置實例，然後按一下**建立**。如果您一開始在**應用程式**欄位中選擇**維持不連結**選項，稍後仍然可以將服務實例連結至 {{site.data.keyword.Bluemix_notm}} 應用程式。
2. 在服務實例儀表板中，建立容器，以開始儲存物件。
3. 從**動作**下拉功能表中，將檔案新增至容器。
4. 若要測試對您物件的存取，請按一下**下載**，並檢閱檔案。
5. 當您準備好將實例連接至應用程式時，請設定服務認證，並[連結服務](/docs/services/reqnsi.html#add_service)。



# 相關鏈結
{: #rellinks}

## API 參考資料 
{: #api}
* [OpenStack {{site.data.keyword.objectstorageshort}} (Swift) API v1](http://developer.openstack.org/api-ref-objectstorage-v1.html){: new_window}
* [OpenStack Identity (Keystone) API 3.0 版](http://developer.openstack.org/api-ref-identity-v3.html){: new_window}

## SDK 
{: #sdk}
* [OpenStack Software Development Kits (SDK)](https://wiki.openstack.org/wiki/SDKs){: new_window}

## 指導教學及範例 
{: #samples}
* [Connecting to IBM {{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}} with Java](https://developer.ibm.com/recipes/tutorials/connecting-to-ibm-object-storage-for-bluemix-with-java/){: new_window}
* [Use Python to access your {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.objectstorageshort}}](https://developer.ibm.com/recipes/tutorials/use-python-to-access-your-bluemix-object-storage/){: new_window}
* [Use PHP to leverage {{site.data.keyword.objectstorageshort}}](https://developer.ibm.com/recipes/tutorials/use-php-to-leverage-object-storage-for-bluemix/){: new_window}
* [Use Node js to access Object Storage for Bluemix](https://developer.ibm.com/recipes/tutorials/use-pkgcloud-to-access-ibm-object-storage-for-bluemix-with-node-js/){: new-window}

## 相容的運行環境
{: #buildpacks}
* [Liberty for Java](https://www.ng.bluemix.net/docs/runtimes/liberty/index.html){: new_window}
* [SDK for Node.js](https://www.ng.bluemix.net/docs/runtimes/nodejs/index.html){: new_window}
* [Go](https://www.ng.bluemix.net/docs/runtimes/go/index.html){: new_window}
* [PHP](https://www.ng.bluemix.net/docs/runtimes/php/index.html){: new_window}
* [Python](https://www.ng.bluemix.net/docs/runtimes/python/index.html){: new_window}
* [Ruby](https://www.ng.bluemix.net/docs/runtimes/ruby/index.html){: new_window}
* [社群建置套件](https://www.ng.bluemix.net/docs/starters/byob.html){: new_window}


## 相關鏈結
{: #general}
* [IBM {{site.data.keyword.Bluemix_notm}} 定價單](https://www.ng.bluemix.net/#/pricing){: new_window}
* [IBM {{site.data.keyword.Bluemix_notm}} 必要條件](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
