---

copyright:
  years: 2017
lastupdated: "2017-02-07"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 使用 Oracle JRE
{: #using_oraacle_jre}

您可以選擇使用 Oracle JRE 在 Bluemix 上執行 Liberty 應用程式。若要這麼做，您必須
* 在可供建置套件下載的位置管理 JRE、
* 管理 `index.yml` 檔案，該檔案提供所管理 JRE 的位置，並且
* 將您的應用程式配置為使用該 JRE。

## 管理 JRE 和 index.yml
{: #hosting_jre}

Oracle JRE 檔案必須在 Web 伺服器上進行管理，而 Liberty 建置套件必須能夠從該伺服器下載此檔案。您可以使用任何可用的伺服器機能在 Bluemix 上管理它，也可以在某個公用的位置上管理它。必須以指定 JRE 檔相關詳細資料的 `index.yml` 檔案來配置伺服器。完成下列步驟，以管理 JRE 及 `index.yml` 檔案：
  1. 取得 Oracle JRE。請注意，JRE 必須是適用於 Unix 64 位元作業系統的版本，並且必須是 `tar.gz` 檔案。
  2. 在 Liberty 建置套件可下載的位置管理 JRE 檔案。 
  3. 確定您在該管理位置提供 `index.yml` 檔案。`index.yml` 檔案必須包含一個項目，其中包含 Oracle JRE 的版本 ID，後面接著一個冒號，以及該 JRE 檔位置的完整 URL。`index.yml` 的格式如下：
```
   ---
   jre_version: https://hostingLocation/jreName.tar.gz
```
{: codeblock}

    * 例如：
    ```
       ---
       1.8.0_91: https://myHostingApp.ng.bluemix.net/jre-8u91-fcs-bin-b14-linux-x64-01_apr_2016.tar.gz
    ```

## 配置應用程式
{: #configure_app}

必須在 Liberty 應用程式上設定兩個環境變數。必須設定 *JBP_CONFIG_OPENJDK* 來指定 `index.yml` 檔案的位置，並且必須將 *JVM* 環境變數設為 *openjdk*，以配置建置套件來使用替代的 JRE。

針對 JBP_CONFIG_OPENJDK 變數，該值為
```
   'repository_root: "https://locationToIndexYml"'
```
{: codeblock}

若要進行此設定，您可以發出像這樣的指令：
```
   $ cf se myApp JBP_CONFIG_OPENJDK 'repository_root: https://myHostingApp.ng.bluemix.net'
```
{: codeblock}

請注意，*repository_root* URL 未包括 `index.yml`，只是會在其位置之前停止。

若要設定 JVM 環境變數，請發出像這樣的指令：
```
   $ cf se myApp JVM 'openjdk'
```
{: codeblock}

**附註**：您必須在設定環境變數之後，重新編譯打包應用程式。

## 確認
{: #confirmation}

若要確認所使用的是預期的 JRE，請檢查編譯打包日誌以尋找類似於下列內容的訊息：
```
   -----> Downloading OpenJdk 1.8.0_91 from https://myHostingApp.ng.bluemix.net/jre-8u91-fcs-bin-b14-linux-x64-01_apr_2016.tar.gz (6.2s)
```
{: codeblock}

# 相關鏈結
{: #rellinks notoc}
## 一般
{: #general notoc}
* [Liberty 運行環境](index.html)
* [Liberty 設定檔概觀](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
