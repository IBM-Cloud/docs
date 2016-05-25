---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Liberty for Java
{: #liberty_runtime}

*前次更新：2016 年 3 月 23 日*

{{site.data.keyword.Bluemix}} 上的 Liberty for Java 應用程式採用 liberty-for-java 建置套件的技術。除了 Liberty 設定檔之外，liberty-for-java 建置套件還提供一個完整的執行時期環境來執行 Java EE 7 和 OSGi 應用程式。它支援例如 Spring 的熱門架構，且包含了 IBM JRE。WebSphere Liberty 讓您能進行極適合雲端的快速應用程式開發。
{: shortdesc}

## 偵測
{: #detection}
當部署下列類型的應用程式時，會使用 Liberty 建置套件：
* [WAR 檔](optionsForPushing.html#stand_alone_apps)
* [EAR 檔](optionsForPushing.html#stand_alone_apps)
* [Liberty 伺服器目錄](optionsForPushing.html#server_directory)
* [Liberty 包裝伺服器](optionsForPushing.html#packaged_server)
* Java main
* [Distzip](https://github.com/cloudfoundry/ibm-websphere-liberty-buildpack/blob/master/docs/container-distZip.md)

## 入門範本應用程式
{: #starter_application}
{{site.data.keyword.Bluemix}} 提供數個 Liberty 入門範本應用程式。Liberty 入門範本應用程式是簡單的 Liberty 應用程式，提供可以讓您使用的範本。您可以用入門範本應用程式進行實驗，並進行及推送對 Bluemix 環境的變更。如需關於使用入門範本應用程式的協助，請參閱[使用入門範本應用程式](../../cfapps/starter_app_usage.html)。

# 相關鏈結
## 一般
* [Liberty 設定檔概觀](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
* [管理 Liberty 應用程式](../../manageapps/app_mng.html#Utilities)
* [使用 IBM Eclipse Tools for Bluemix 部署應用程式](../../manageapps/eclipsetools/eclipsetools.html#eclipsetools)
* [開始使用 IBM Monitoring and Analytics for Bluemix 服務](../../services/monana/index.html#monana_oview)
## 範例
* [Cloud Foundry 架構實驗室](https://developer.ibm.com/bluemix/docs/category/cloud-foundry-docs/)
