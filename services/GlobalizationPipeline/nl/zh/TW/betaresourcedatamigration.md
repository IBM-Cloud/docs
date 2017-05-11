---

copyright:
  years: 2015, 2017
lastupdated: "2016-10-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 從測試版移轉資源資料
{: #globalizationpipeline_betaresourcedatamigration}


發行 GA 版本後，將於特定期間之後終止 {{site.data.keyword.GlobalizationPipeline_full}} 測試版。測試版實例中的使用者資料不會移至 GA 服務實例。若要保留 GA 之後的資料，您可以將資源資料匯出至檔案，然後匯入至新的實例。請注意，您無法使用服務儀表板來執行此作業。而且，將資源資料匯出至其中一種資源檔格式，將不會保留其他與資源項目相關聯的 meta 資料。

為了支援從測試版到 GA 的資料移轉，已在 {{site.data.keyword.GlobalizationPipeline_short}} 的 Java 指令行工具中新增功能。該工具的原始檔於 https://github.com/IBM-Bluemix/gp-java-tools 上進行管理，而且 github 儲存庫中也會提供其二進位版次。並張貼最新開發 Snapshot。[下載。](https://w3-connections.ibm.com/communities/service/html/communityview?communityUuid=589d87cf-d0c7-4e06-ab95-4108547f90aa#fullpageWidgetId=Wa22bb771e29b_4aa9_a114_cfe53fda2cc8&file=5cdaf089-ec7c-4881-b5a0-7ab651491237)

此工具會在**上傳資源項目**的測試版之後使用 REST API 加強，因此，目的地服務實例必須是 GA 版本。 
* 來源：測試版或 GA
* 目的地：僅限 GA

若要將 Globalization 服務實例中的所有軟體組資料複製到另一個實例，請使用下面的指令：

```
 java -jar gp-cli.jar copy-all-bundles -s <source-service-url> -i <source-instance-id> -u <source-user-id> -p <source-password> --dest-url <dest-service-url> --dest-instance-id <dest-instance-id> --dest-user-id <dest-user-id> --dest-password <dest-password>
```


`source/target-service-url`，以及其他參數值則位於來源/目的地服務的認證中，例如：

 

```
{
  "gp-beta": [
    {
      "name": "Globalization Pipeline-7x",
      "label": "gp-beta",
      "plan": "gp-beta-plan",
      "credentials": {
 

      "url": "https://gp-beta-rest.ng.bluemix.net/translate/rest",
        "userId": "bd0b84362c6934d222c3a0a40fc1443b",
        "password": "OGxp6jDqCLCL1ui8kQSPTt1mZDi4EQwu",
        "instanceId": "bd0b84362c6934d222c3a0a40fc1233e"
      }
    }
  ]
}
```
而且，除了個別選項 `(-s / -i / -u / -p)` 之外，還會更新所有 GP CLI 以支援 json 格式的認證。您可以使用下面這類內容來建立 json 檔案：

creds.json 
 
```
 {

        "url": "https://gp-rest.stage1.ng.bluemix.net/translate/rest",
        "userId": "36cad58b3a65dc9fe0183208305be137",
        "password": "43F9MRMu9Q8BWRXMLctunUsAe8LTdwq1",
        "instanceId": "b157e3fc63e62d76c50d9f689d7fc965"} 
```
然後，您可以透過 `-j <json-file>` 來指定檔案。在 `copy/copy-all-bundles` 指令中，您可以將

```
-s https://gp-rest.stage1.ng.bluemix.net/translate/rest -i b157e3fc63e62d76c50d9f689d7fc965 -u 36cad58b3a65dc9fe0183208305be137 -p 43F9MRMu9Q8BWRXMLctunUsAe8LTdwq1
```

取代為

`-j creds.json `
 
或者，您也可以使用下列指令，將軟體組從某個位置複製到另一個位置： 

```
 java -jar gp-cli.jar copy -s <source-service-url> -i <source-instance-id> -u <source-user-id> -p <source-password> -b <source-bundle-id> --dest-url <dest-service-url> --dest-instance-id <dest-instance-id> --dest-user-id <dest-user-id> --dest-password <dest-password> -d <dest-bundle-id>
```


**附註：**除了 copy-all-bundles 的參數之外，您還可以使用另外兩個參數：`-b <source-bundle-id>` 和 `-d <dest-bundle-id>`。此指令可以用來複製相同實例內的軟體組。在此情況下，您可以省略目的地服務認證參數 `(--dest-*)`。





上述指令會擷取現有軟體組資料和資源項目資料，並將它們上傳至新的位置。在這個處理程序期間，將會更新 REST 伺服器所控制的部分欄位（例如 updatedBy/updatedAt 欄位）。而且，因為這些指令不會複製服務連結和配置資料，所以您可能需要在目的地實例中配置 MT 服務。





例如，測試版透過「Watson 語言翻譯程式」支援阿拉伯文翻譯。在 GA 版本中，不再免費提供阿拉伯文翻譯。當您將測試版資料移植至新的 GA 實例時，將會保留已翻譯的阿拉伯文內容。除非您設定 Watson 連結來啟用阿拉伯文翻譯，否則來源語言中的變更不會自動觸發阿拉伯文翻譯。來源實例為 GA 版本時也是如此。外部 MT 服務連結是 GP 實例特有的；不會自動移植另一個實例的連結/配置。




 

