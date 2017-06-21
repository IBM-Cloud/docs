---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-20"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 將裝置資料視覺化
{: #visualizingdata_data}

此範例可協助您將 {{site.data.keyword.iot_full}} 組織中已登錄裝置的即時及歷程資料視覺化。
{:shortdesc}

## 開始之前
{: #byb}

您必須先進行下列動作，才能將資料視覺化：

- 向 {{site.data.keyword.iot_short_notm}} 組織登錄裝置。
- 確定裝置將事件傳送至 {{site.data.keyword.iot_short_notm}}。
- 從 Github 儲存庫[下載視覺化範例](https://github.com/ibm-watson-iot/rickshaw4iot/archive/master.zip)，並解壓縮 .zip 檔。
- 從 {{site.data.keyword.Bluemix_notm}} [安裝 cf 指令行工具](../../starters/install_cli.html)。

## 在 {{site.data.keyword.Bluemix_notm}} 中執行範例
{: #running_sample}

1. 使用 Node.js SDK，在 {{site.data.keyword.Bluemix_notm}} 中建立應用程式。記下應用程式名稱和應用程式的主機名稱，將應用程式上傳至 {{site.data.keyword.Bluemix_notm}} 時，會需要此資訊。
2. 完成下列步驟，以將 node.JS 應用程式連結至 {{site.data.keyword.Bluemix_notm}} 儀表板中的 {{site.data.keyword.iot_short_notm}} 實例：

  a. 在 {{site.data.keyword.Bluemix_notm}} 儀表板中，按一下您已建立的 Node.JS 應用程式。

  b. 按一下**連結服務或 API**，然後選取 {{site.data.keyword.iot_short_notm}} 服務，並按一下**新增**。
3. 使用 cf 指令行工具，切換目錄到已解壓縮的視覺化範例套件，並執行下列指令，以連接至 {{site.data.keyword.Bluemix_notm}}。
```
cf api https://api.ng.bluemix.net
```
4. 接下來，使用下列指令來登入 {{site.data.keyword.Bluemix_notm}}：
```
cf login -u <your_bluemix_login_id>
```
如果您不使用預設的組織和空間，可以使用：
```
cf target-o <your_bluemix_org> -s dev
```

5. 編輯 `manifest.yml` 檔案，並使用下列格式來更新主機和應用程式名稱：
```
applications:
 - disc quota: 1024M
   host: <your_bluemix_hostname>
   name: <your_bluemix_appname>
   command: node ap.js
   path:
   domain: mybluemix.net
   instances: 1
   memory: 128M
```
6. 使用下列指令來部署您的視覺化範例：
```
cf push <your_application_name>
```
7. 在瀏覽器中，輸入下列 URL：
```
http://<your_application_name>.mybluemix.net
```

組織中的所有裝置都會列在裝置下拉功能表中。選取時，您應該會看到裝置傳送至 {{site.data.keyword.iot_short_notm}} 服務的即時視覺化資料。若要查看歷程資料，請按一下**歷程資料**按鈕。

## 自訂範例
{: #customize_sample}

這個範例應用程式是以 node.js 架構撰寫的獨立式 Web 應用程式。此範例會將 {{site.data.keyword.iot_short_notm}} 中已登錄裝置所傳送的事件視覺化。此範例使用下列工具：

- Express：Node.js Web 應用程式架構
- JQuery：使用者介面和 Ajax 呼叫
- Rickshaw：圖形視覺化工具
- Paho：MQTT 用戶端

範例應用程式的結構具有下列目錄：

- Public
- CSS：樣式表
- Images
- JS：主要 JavaScript 邏輯檔案
- Historian：用於歷程視覺化的程式碼
- Realtime：用於即時視覺化的程式碼
- Uicontroller.js：用於控制使用者介面的程式碼
- Routes：路徑邏輯和 Web 應用程式
- Utils：公用程式函數，用於進行 HTTP 呼叫
- Views：使用者介面檔案，以 Jade 撰寫
- Rickshaw 圖表程式庫可用來繪圖即時和歷程資料的圖形。

## 自訂即時資料顯示畫面
{: #customize_real_time_display}

包含即時資料之圖形視覺化程式碼的目錄為 `public/ja/realtime`。若要自訂圖形邏輯，可以編輯 `public/js/historian/realtimeGraph.js`。

參照 Paho MQTT 程式庫來訂閱裝置主題以及從 {{site.data.keyword.iot_short_notm}} 接收裝置事件的檔案，位於 `public/js/historian/realtime.js`。

裝置事件會傳遞至 `realtimeGraph.js` 檔案，以繪製圖形。

如需更詳細的開發人員指引，請造訪 [GitHub Wiki ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/ibm-watson-iot/rickshaw4iot/wiki){:new_window}。
