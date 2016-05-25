---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 記憶體限制與 Liberty 建置套件
{: #memory_limits}

*前次更新：2016 年 3 月 23 日*

當您使用 Liberty 建置套件部署應用程式時，必須指定記憶體限制。

**避免問題**

* 使用 Liberty 建置套件部署且記憶體限制為 256 MB 的 "Hello World" Servlet，可能無法正確地部署及執行。
如果部署，它執行時會接近 256M 的限制。請考慮指定最少 512M 作為記憶體限制，即使是簡單的應用程式也一樣。


## 記憶體限制與 Liberty 建置套件
{: #memory_limits_and_liberty}


當您使用
Liberty 建置套件部署應用程式時，會提示您輸入「記憶體限制」。


若要判斷指定什麼記憶體限制，則必須瞭解您不是指定 Java 應用程式資料堆的大小。您是在指定整個處理程序能夠使用的記憶體量。這個量包含下列元件所使用的記憶體：

* 監看儲存器所使用的記憶體。
* 用來將核心延伸和系統檔案庫對映到處理程序的記憶體。
* 用於 jvm 可執行檔、jvm 工作資料堆、jit 空間和壓縮參照的記憶體。
* 用於類別（應用程式伺服器和應用程式）、執行緒堆疊及直接 IO 緩衝區的記憶體。
* Java 應用程式資料堆所使用的記憶體。

您可以在 [Thanks for the memory](http://www.ibm.com/developerworks/library/j-nativememory-linux/) 這篇 developerWorks 文章中，找到 JVM 記憶體用量的相關資訊。

當您部署應用程式時，會監視整個處理程序的記憶體用量。如果記憶體用量超出您在應用程式部署時指定的記憶體限制，則核心會停止該處理程序。這個動作發生時不會有警告，而可能以下列方式表現：

* 如果在應用程式部署期間超出記憶體限制，您會收到發生失敗的訊息。您可能會看到應用程式在飄動。您可能會看到應用程式試圖多次啟動，但一直不成功。或者，您可能會收到訊息，指出應用程式部署失敗。
* 如果應用程式在服務中時超出記憶體限制，則會停止該處理程序。Cloud Foundry 會試圖重新啟動應用程式。應用程式可能會重新啟動，但它有某段時間無法使用。

# 相關鏈結
## 一般
* [Liberty 執行時期](index.html)
* [Liberty 設定檔概觀](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
