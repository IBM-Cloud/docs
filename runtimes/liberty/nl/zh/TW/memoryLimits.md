---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-18"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 記憶體限制與 Liberty 建置套件
{: #memory_limits}

當您使用 Liberty 建置套件部署應用程式時，必須指定記憶體限制。

## 避免問題

使用 Liberty 建置套件部署且記憶體限制為 256 MB 的 "Hello World" Servlet，可能無法正確地部署及執行。
如果部署，它執行時會接近 256M 的限制。請考慮指定最少 512M 作為記憶體限制，即使是簡單的應用程式也一樣。


## 記憶體限制與 Liberty 建置套件
{: #memory_limits_and_liberty}


當您使用
Liberty 建置套件部署應用程式時，會提示您輸入「記憶體限制」。


若要判斷指定什麼記憶體限制，則必須瞭解您不是指定 Java 應用程式資料堆的大小。您是在指定整個處理程序能夠使用的記憶體量。這個量包含下列元件所使用的記憶體：

* 監看容器所使用的記憶體。
* 用來將核心延伸和系統檔案庫對映到處理程序的記憶體。
* 用於 jvm 可執行檔、jvm 工作資料堆、jit 空間和壓縮參照的記憶體。
* 用於類別（應用程式伺服器和應用程式）、執行緒堆疊及直接 IO 緩衝區的記憶體。
* Java 應用程式資料堆所使用的記憶體。

您可以在 [Thanks for the memory](http://www.ibm.com/developerworks/library/j-nativememory-linux/) 這篇 developerWorks 文章中，找到 JVM 記憶體用量的相關資訊。

當您部署應用程式時，會監視整個處理程序的記憶體用量。如果記憶體用量超出您在應用程式部署時指定的記憶體限制，則核心會停止該處理程序。這個動作發生時不會有警告，而可能以下列方式表現：

* 如果在應用程式部署期間超出記憶體限制，您會收到發生失敗的訊息。您可能會看到應用程式在飄動。您可能會看到應用程式試圖多次啟動，但一直不成功。或者，您可能會收到訊息，指出應用程式部署失敗。
* 如果應用程式在服務中時超出記憶體限制，則會停止該處理程序。Cloud Foundry 會試圖重新啟動應用程式。應用程式可能會重新啟動，但它有某段時間無法使用。

## 指定資料堆記憶體
{: #specifying_heap_memory}

您可以使用各種方式來自訂配置給應用程式的資料堆記憶體數量上限。

*  使用 JVM_ARGS 環境變數及 -Xmx 引數。例如，若要將資料堆大小上限設為 512M，請使用下列指令，並重新編譯打包應用程式。

```
    $ cf set-env myapp JVM_ARGS -Xmx512m
```
{: codeblock}

* 如果您的應用程式是[伺服器目錄](optionsForPushing.html#server_directory)或[包裝伺服器](optionsForPushing.html#packaged_server)，則可以在 jvm.options 檔案中指定 -Xmx 引數。

* 您可以使用 JBP_CONFIG_IBMJDK 環境變數來指定資料堆大小比例。heap_size_ratio 是浮點數值，可指定要配置給資料堆的可用記憶體數量。例如，若要將一半的可用記憶體配置給資料堆，請發出下列指令，並重新編譯打包應用程式。

```
    $ cf set-env myapp JBP_CONFIG_IBMJDK "heap_size_ratio: 0.50"
```
{: codeblock}
