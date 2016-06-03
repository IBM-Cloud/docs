---

copyright:
  years: 2015, 2016

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 

# {{site.data.keyword.Bluemix_notm}} 存取疑難排解 
{: #accessing}

*前次更新：2016 年 5 月 16 日*

一般在存取 {{site.data.keyword.Bluemix}} 時發生的問題，可能包括使用者無法登入 {{site.data.keyword.Bluemix_notm}}、帳戶陷入擱置狀態，等等。然而，在許多情況下，您可以依照下列一些簡單的步驟，從這些問題中回復。
{:shortdesc}

## 無法登入 {{site.data.keyword.Bluemix_notm}}
{: #ts_logintobm}

您必須具有有效的 IBM ID 及密碼才能登入 {{site.data.keyword.Bluemix_notm}}。


嘗試登入 {{site.data.keyword.Bluemix_notm}} 時，您看到下列錯誤訊息：
{: tsSymptoms} 

`底下所輸入的 IBM ID 及/或密碼不正確。請重試。`


您用來登入 {{site.data.keyword.Bluemix_notm}} 的 IBM ID 及密碼無效。
{: tsCauses} 
 

若要取得有效的 IBM ID 及密碼，請移至「我的 IBM 設定檔」頁面，然後完成下列其中一個步驟：
{: tsResolve}
  * 如果您已登錄一個 IBM ID，而想要檢查您的 ID 及密碼是否有效，請按一下**登入**，並在「登入」頁面上輸入您的 IBM ID 及密碼。如果您忘記密碼，請按一下「登入」頁面右邊的**忘記密碼**來重設密碼。如果您忘記 IBM ID 或是持續有密碼的問題，請與 Worldwide IBM Registration Help Desk 聯絡以取得協助。 
  * 如果您沒有 IBM ID，請按一下**登錄**來登錄一個 IBM ID 及密碼。 
  
**附註：**對於 IBM 員工而言，IBM ID 可能與內部網路登入 ID 不同。 





## 您有未儲存的變更
{: #ts_unsaved_changes}


在應用程式詳細資料頁面上進行瀏覽時，可能無法執行任何動作，系統可能會提示您儲存變更後才能繼續。 


在應用程式詳細資料頁面上嘗試檢查應用程式或服務時，總是收到下列錯誤訊息：
{: tsSymptoms} 

`您在頁面 app_name 中有未儲存的變更。請儲存或取消這些變更。`


在執行時期窗格的**實例**或**記憶體配額**欄位上捲動滑鼠時，值就會變更。這是有意這樣設計的；但是，當您要離開該頁面時，會有錯誤訊息提示您儲存記憶體或實例設定。
{: tsCauses}


關閉訊息視窗，然後按一下執行時期窗格中的**重設**按鈕。
{: tsResolve} 




    
    
## {{site.data.keyword.Bluemix_notm}} 地區之間的自動失效接手無法使用
{: #ts_failover}

您無法在 {{site.data.keyword.Bluemix_notm}} 地區之間使用自動失效接手。不過，您可以使用支援在多個 IP 位址之間進行失效接手的 DNS 提供者，作為暫行解決方法。
 

當 {{site.data.keyword.Bluemix_notm}} 地區變成無法使用時，在該地區中執行的應用程式也會無法使用，即使相同應用程式正在另一個 {{site.data.keyword.Bluemix_notm}} 地區中執行亦然。
{: tsSymptoms}

 
{{site.data.keyword.Bluemix_notm}} 尚未提供從一個地區到另一個地區的自動失效接手。
{: tsCauses}

 
您可以使用支援在多個 IP 位址之間進行智慧型失效接手的 DNS 提供者，並且手動配置 DNS 設定，以啟用 {{site.data.keyword.Bluemix_notm}} 地區之間的自動失效接手。具有此功能的 DNS 提供者包括 NSONE、Akamai、Dyn。
{: tsResolve}

當您配置 DNS 設定時，必須指定應用程式執行所在之 {{site.data.keyword.Bluemix_notm}} 地區的公用 IP 位址。若要取得 {{site.data.keyword.Bluemix_notm}} 地區的公用 IP 位址，請使用 `nslookup` 指令。例如，您可以在指令行視窗鍵入下列指令：
```
nslookup mybluemix.net
```



## 帳戶擱置
{: #ts_accntpding}

如果您的帳戶擱置，您便無法登入 {{site.data.keyword.Bluemix_notm}}。

 
在登錄取得 {{site.data.keyword.Bluemix_notm}} 試用帳戶之後，您可能無法登入 {{site.data.keyword.Bluemix_notm}}。相反地，您看到下列訊息：
{: tsSymptoms}

<code>您的帳戶處於擱置狀態。請稍候，最晚 24 小時即會收到電子郵件確認信，同時也請檢查垃圾郵件資料夾。如果您仍未收到電子郵件確認，請聯絡 <a href="http://ibm.biz/bluemixsupport.com" target="_blank">Bluemix 支援中心</a>。</code>在登錄取得 {{site.data.keyword.Bluemix_notm}} 試用帳戶之後，您會收到一封確認電子郵件。您必須按一下此封確認電子郵件中的鏈結，才能完成登錄程序。
{: tsCauses} 

確認電子郵件會寄送到您提供的電子郵件位址。請檢查您的收件匣以及垃圾郵件資料夾。如果您尚未收到確認電子郵件，請與 [{{site.data.keyword.Bluemix_notm}} 支援中心](http://ibm.biz/bluemixsupport.com){: new_window}聯絡。  
{: tsResolve}



## 無法將使用者新增至組織
{: #ts_adduser}

您可以邀請多位使用者在相同的組織下工作。唯有您是帳戶擁有者，或同時為組織的管理員與成員時，才能邀請使用者加入您的組織。
 

您無法在**管理組織**區段中看到**邀請新使用者**鏈結。
{: tsSymptoms}

 

只有下列 {{site.data.keyword.Bluemix_notm}} 使用者可以邀請使用者加入組織：
{: tsCauses}
  * 組織的帳戶擁有者
  * 同時為組織成員（非合作人員）的組織管理員
  
在 {{site.data.keyword.Bluemix_notm}} 中，您可以是組織的成員或合作人員：

<dl><dt>合作人員</dt>
<dd>如果您已有 {{site.data.keyword.Bluemix_notm}} 帳戶，而別人邀請加入組織，則您是組織的合作人員。</dd>
<dt>成員</dt>
<dd>如果您沒有 {{site.data.keyword.Bluemix_notm}} 帳戶，但某人邀請您加入組織，且您透過該邀請註冊 {{site.data.keyword.Bluemix_notm}}，則您是組織的成員。</dd>
</dl>


如果您是組織的合作人員，即使已將您指派為組織管理員，您也無法邀請使用者加入您的組織。

**附註：**所有組織管理員（包括身為組織合作人員者）都可以新增、修改及移除已經在組織中的使用者。

 

如果您無法邀請使用者加入您的組織，而需要不同的角色來完成這項動作，請與組織管理員聯絡，以變更角色。若要識別您的組織管理員，請完成下列步驟：
{: tsResolve}

  1. 移至 {{site.data.keyword.Bluemix_notm}}「儀表板」，按一下頂端功能表列中的**帳戶和支援**圖示 ![帳戶和支援](images/account_support.svg)，然後選取**管理組織**。
  2. 移至您的組織，然後檢視**使用者**標籤上的組織管理員資訊。  
  
如果您因自己是合作人員（而非成員）而無法邀請使用者，則您必須刪除先前的 {{site.data.keyword.Bluemix_notm}} 帳戶，然後受邀以組織成員的身分加入帳戶。若要刪除先前的帳戶並以成員的身分加入帳戶，請完成下列步驟： 

  1. 聯絡 [{{site.data.keyword.Bluemix_notm}} 支援](http://ibm.biz/bluemixsupport){: new_window}，以開啟一個支援問題單，並要求刪除您的帳戶。如果您的資料與要儲存並移至新帳戶的舊帳戶相關聯，請在電子郵件中包括此資訊。 
  2. 刪除您的帳戶之後，請讓具有組織管理員角色的使用者，邀請您以組織管理員的身分加入組織。然後，透過該邀請註冊 {{site.data.keyword.Bluemix_notm}}。 




## 不支援批次登錄使用者
{: #ts_batchregistration}

當您向 {{site.data.keyword.Bluemix_notm}} 登錄使用者時，必須個別登錄每一個使用者。
 

{{site.data.keyword.Bluemix_notm}} 不提供同時登錄多個使用者的功能。
{: tsSymptoms}
 

{{site.data.keyword.Bluemix_notm}} 不支援批次登錄使用者。若要向 {{site.data.keyword.Bluemix_notm}} 登錄使用者，必須個別登錄每一個使用者。
{: tsCauses}
 

若要向 {{site.data.keyword.Bluemix_notm}} 登錄多個使用者，您必須為每個使用者完成下列步驟：
{: tsResolve}

  1. 按一下 {{site.data.keyword.Bluemix_notm}} 使用者介面右上角的**註冊**。
  2. 遵循精靈指示來完成步驟。

    

## 無法載入 {{site.data.keyword.Bluemix_notm}} 頁面
{: #ts_err}

當您使用 {{site.data.keyword.Bluemix_notm}} 使用者介面時，您可能無法載入 {{site.data.keyword.Bluemix_notm}} 頁面。反之，可能會看到錯誤訊息 BXNUI0001E 或 BXNUI0016E。
 

當您使用 {{site.data.keyword.Bluemix_notm}} 使用者介面時，您可能會看到下列其中一則錯誤訊息：
{: tsSymptoms}

`BXNUI0001E: 由於 Bluemix 未偵測到階段作業是否存在，因此未載入頁面。`


`BXNUI0016E: 由於未載入 Bluemix 頁面，因此未擷取應用程式及服務。`

 

您可以視需要完成下列其中一個以上的動作：
{: tsResolve}

  * 重新整理或重新啟動瀏覽器。
  * 登出 {{site.data.keyword.Bluemix_notm}} 然後再重新登入。
  * 使用瀏覽器的專用瀏覽模式。 
  * 清除瀏覽器的 Cookie 及快取。
  * 使用不同的瀏覽器。如需 {{site.data.keyword.Bluemix_notm}} 支援的瀏覽器版本的相關資訊，請參閱 [{{site.data.keyword.Bluemix_notm}} 必要條件](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}。
  * 如果您已安裝 cf 指令行介面，請輸入 `cf apps` 指令來查看您的應用程式是否正在執行中。
  
  
  
  
  
## {{site.data.keyword.Bluemix_notm}} 頂端功能表列消失
{: #ts_topmenubar}

調整瀏覽器視窗大小或使用行動式裝置時，您可能無法看到 {{site.data.keyword.Bluemix_notm}} 頂端功能表列。


縮小瀏覽器視窗大小或使用行動式裝置時，{{site.data.keyword.Bluemix_notm}} 頂端功能表列會消失。當頂端功能表列消失時，顯示為堆疊行圖示的側邊欄功能表會出現在左上角。
{: tsSymptoms}

 

{{site.data.keyword.Bluemix_notm}} 使用者介面有具回應力的設計。檢視環境變更時，{{site.data.keyword.Bluemix_notm}} 使用者介面的佈置可能也會變更。
{: tsCauses}
 

請改用左上角的側邊欄功能表。
{: tsResolve}








# 管理應用程式疑難排解
{: #managingapps}

管理應用程式的一般問題可能包括無法更新應用程式、未顯示雙位元組字元等問題。然而，在許多情況下，您可以依照下列一些簡單的步驟，從這些問題中回復。
{:shortdesc}





## 無法將應用程式切換為除錯模式
{: #ts_debug}

如果 Java 虛擬機器 (JVM) 版本是第 8 版或更舊版本，則您可能無法啟用除錯模式。 


在您選取**啟用應用程式除錯**之後，工具會嘗試將應用程式切換為除錯模式。然後，Eclipse 工作台會開始除錯階段作業。工具順利啟用除錯模式時，Web 應用程式狀態會顯示`更新模式`、`開發中`及`除錯中`。
{: tsSymptoms}

不過，工具無法啟用除錯模式時，Web 應用程式狀態只會顯示`更新模式`及`開發中`，並不會顯示`除錯中`。工具可能也會在「主控台」視圖中顯示下列錯誤訊息：

```
bluemixMgmgClient - ???? [pool-1-thread-1] .... ERROR --- ClientProxyImpl: Cannot create the websocket connections for MyWebProj
com.ibm.ws.cloudoe.management.client.exception.ApplicationManagementException: javax.websocket.DeploymentException: The HTTP request to initiate the  WebSocket connection failed
at com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl.onNewClientSocket(ClientProxyImpl.java:161)
at com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl$RunServerTask.run(ClientProxyImpl.java:267)
at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:522)
at java.util.concurrent.FutureTask.run(FutureTask.java:277)
at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1153)
at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:628)
at java.lang.Thread.run(Thread.java:785)
Caused by: javax.websocket.DeploymentException: The HTTP request to initiate the WebSocket connection failed
at  org.apache.tomcat.websocket.WsWebSocketContainer.connectToServer(WsWebSocketContainer.java:315)
at  com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl.onNewClientSocket(ClientProxyImpl.java:158)
... 6 more
Caused by: java.util.concurrent.TimeoutException
at org.apache.tomcat.websocket.AsyncChannelWrapperSecure$WrapperFuture.get(AsyncChannelWrapperSecure.java:505)
at org.apache.tomcat.websocket.WsWebSocketContainer.processResponse(WsWebSocketContainer.java:542)
at org.apache.tomcat.websocket.WsWebSocketContainer.connectToServer(WsWebSocketContainer.java:296)
... 7 more
[2016-01-15 13:33:51.075] bluemixMgmgClient - ????  [pool-1-thread-1] .... ERROR --- ClientProxyImpl: Cannot create the  websocket connections for MyWebProj
com.ibm.ws.cloudoe.management.client.exception.ApplicationManagementException: javax.websocket.DeploymentException: The HTTP request to initiate the  WebSocket connection failed
at com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl.onNewClientSocket(ClientProxyImpl.java:161)
at com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl$RunServerTask.run(ClientProxyImpl.java:267)
at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:522)
at java.util.concurrent.FutureTask.run(FutureTask.java:277)
at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1153)
at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:628)
at java.lang.Thread.run(Thread.java:785)
Caused by: javax.websocket.DeploymentException: The HTTP request to initiate the WebSocket connection failed
at org.apache.tomcat.websocket.WsWebSocketContainer.connectToServer(WsWebSocketContainer.java:315)
at com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl.onNewClientSocket(ClientProxyImpl.java:158)
... 6 more
Caused by: java.util.concurrent.TimeoutException
at org.apache.tomcat.websocket.AsyncChannelWrapperSecure$WrapperFuture.get(AsyncChannelWrapperSecure.java:505)
at org.apache.tomcat.websocket.WsWebSocketContainer.processResponse(WsWebSocketContainer.java:542)
at org.apache.tomcat.websocket.WsWebSocketContainer.connectToServer(WsWebSocketContainer.java:296)
... 7 more
```
 

下列 Java 虛擬機器 (JVM) 版本無法建立除錯階段作業：IBM JVM 7、IBM JVM 8 及舊版 Oracle JVM 8。
{: tsCauses}

如果您的工作台 JVM 為上述其中一種版本，則可能會在建立除錯階段作業時發生問題。您的工作台 JVM 版本一般是本端電腦的系統 JVM。您的系統 JVM 與執行中 Bluemix Java 應用程式的 JVM 不同。Bluemix Java 應用程式幾乎一律會在 IBM JVM 上執行，但有時會在 OpenJDK JVM 上執行。
  

若要檢查 IBM Eclipse Tools for Bluemix 所執行的 Java 版本，請完成下列步驟：
{: tsResolve}

  1. 在 IBM Eclipse Tools for Bluemix 中，選取**說明** > **關於 Eclipse** > **安裝詳細資料** > **配置**。
  2. 從清單中尋找 `eclipse.vm` 內容。下列這一行是 `eclipse.vm` 內容範例：
	
	```
	eclipse.vm=C:\Program Files\IBM\ibm-java-sdk-80-win-x86_64\bin\..\jre\bin\j9vm\jvm.dll
	```

  3. 在指令行中，從 Java 安裝的 `bin` 目錄中輸入 `java -version`。即會顯示 IBM JVM 版本資訊。

如果您的工作台 JVM 是 IBM JVM 7 或 8，或舊版 Oracle JVM 8，請完成下列步驟來切換至 Oracle JVM 8：

  1. 下載並安裝 Oracle JVM 8，如需詳細資料，請參閱 [Java SE 下載](http://www.oracle.com/technetwork/java/javase/downloads/index.html){: new_window}。
  2. 重新啟動 Eclipse。
  3. 檢查 `eclipse.vm` 內容是否指向新的 Oracle JVM 8 安裝。







## 無法執行所要求的動作
{: #ts_authority}

您可能沒有適當的存取權，無法完成動作。

 

當您嘗試執行服務實例或應用程式實例的動作時，無法完成所要求的動作，並且看到下列其中一個錯誤訊息：
{: tsSymptoms}

`BXNUI0514E: You are not a developer for any of the spaces in the <orgName> organization.`


`Server error, status code: 403, error code: 10003, message: You are not authorized to perform the requested action.`

 

您沒有執行動作所需的適當權限層級。
{: tsCauses}

  

若要取得適當的權限層級，請使用下列其中一種方法：
{: tsResolve}
 * 選取另一個您具有開發人員角色的組織及空間。 
 * 要求組織管理者將您的角色變更為開發人員，或建立空間，然後將開發人員角色指派給您。如需詳細資料，請參閱[管理組織](../admin/orgs_spaces.html)。
 

 


## 因為授權錯誤，所以無法存取 {{site.data.keyword.Bluemix_notm}} 服務
{: #ts_vcap}

如果服務認證寫在您的應用程式中，則您的應用程式存取 {{site.data.keyword.Bluemix_notm}} 服務時可能會發生授權錯誤。 

配置應用程式與 {{site.data.keyword.Bluemix_notm}} 服務通訊之後，即將應用程式部署至 {{site.data.keyword.Bluemix_notm}}。不過，您無法使用應用程式來存取 {{site.data.keyword.Bluemix_notm}} 服務，而且會收到授權錯誤。
{: tsSymptoms}

寫在應用程式中的認證可能不正確。每次重建服務時，用來存取它的認證都會變更。
{: tsCauses}


請使用 VCAP_SERVICES 環境變數中的連線參數，而不是將認證寫在應用程式中。使用 VCAP_SERVICES 環境變數中連線參數的方法會根據程式語言而不同。例如，針對 Node.js 應用程式，您可以使用下列指令：
{: tsResolve}

```
process.env.VCAP_SERVICES
```
如需可在其他程式語言中使用之指令的相關資訊，請參閱 [Java](http://docs.run.pivotal.io/buildpacks/java/java-tips.html#env-var){: new_window} 及 [Ruby](http://docs.run.pivotal.io/buildpacks/ruby/ruby-tips.html#env-var){: new_window}。 
 

 
 




## 無法使用 IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} 來部署應用程式
{: #ts_bm_tools_facet}

當不受支援的資料類型套用至 Eclipse 專案時，您可能無法使用 IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} 將您的應用程式部署至 {{site.data.keyword.Bluemix_notm}}。 

 

您可以使用 Cloud Foundry CLI，順利地將應用程式部署至 {{site.data.keyword.Bluemix_notm}}。然而，您無法使用 IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} 將應用程式部署至 {{site.data.keyword.Bluemix_notm}}，並且看到此錯誤訊息：`不支援專案資料類型 <facet_name>。`例如，`不支援專案資料類型 Cloud Foundry 獨立式應用程式 1.0 版。`
{: tsSymptoms}

 

IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} 會依專案資料類型將專案對映至 {{site.data.keyword.Bluemix_notm}} 執行時期。資料類型可定義 Eclipse 中 Java EE 專案的需求，並作為執行時期配置的一部分，以便不同的執行時期與不同的專案相關聯。如果 IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} 不支援套用至專案的資料類型，您可能無法使用 IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} 來部署應用程式。
{: tsCauses}


您必須從 Eclipse 專案中移除資料類型，才能使用 IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} 來部署應用程式。
{: tsResolve} 

若要移除資料類型，請在 IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} 中，針對專案按一下**專案 > 內容 > 專案資料類型**。然後，清除不受支援之資料類型的勾選框。 



## 收到 502 錯誤的閘道錯誤
{: #ts_502_error}

如果您在 {{site.data.keyword.Bluemix_notm}} 上與應用程式互動時，收到「502 錯誤的閘道」錯誤，請檢查 {{site.data.keyword.Bluemix_notm}} 狀態頁面，然後採取相應的動作。

 

您收到開頭為「502 錯誤的閘道」的錯誤訊息。例如，您可能會看到 `502 錯誤的閘道：已登錄的端點無法處理要求。`
{: tsSymptoms}

 

「錯誤的閘道」錯誤通常發生在您所造訪網站使用 Proxy 伺服器來儲存及中繼來自管理網站之主要伺服器的資料時。主要伺服器及 Proxy 伺服器可能未適當連接，因此您在瀏覽器視窗中看到 HTTP 狀態碼 502。此狀態碼表示網站的主要伺服器未收到它預期來自 Proxy 伺服器的 HTTP 實作。
{: tsCauses}

其他較少見的「錯誤的閘道」錯誤原因，包括網際網路服務供應商 (ISP) 脫離、不正確的防火牆配置及瀏覽器快取錯誤。 

 

如果您懷疑 {{site.data.keyword.Bluemix_notm}} 服務已關閉，請先檢查 [{{site.data.keyword.Bluemix_notm}} 狀態](https://developer.ibm.com/bluemix/support/#status){: new_window}頁面。您可能想要使用另一個 {{site.data.keyword.Bluemix_notm}} 地區的服務作為暫行解決方法。詳細資訊位於[使用另一個地區的服務](../services/reqnsi.html#cross_region_service){: new_window}。如果服務狀態正常，請嘗試下列步驟來解決問題：
{: tsResolve}

  * 重試動作：
    * 按鍵盤上的 F5 以重新載入頁面，或者按一下重新整理按鈕。如果此步驟無效，請清除瀏覽器的快取及 Cookie，然後再重新載入。
	* 使用不同的瀏覽器。
	* 將路由器、數據機及電腦重新開機。將這些裝置重新開機可清除導致錯誤 502 的許多種錯誤。 
  * 等待並於稍後再試一次。在部分情況下，暫時問題可能是由於網際網路服務供應商或 {{site.data.keyword.Bluemix_notm}} 服務所造成。您可能要等待暫時問題獲得解決。
  * 如果問題仍然存在，請與 {{site.data.keyword.Bluemix_notm}} 支援中心聯絡。如需相關資訊，請參閱[與 {{site.data.keyword.Bluemix_notm}} 支援中心聯絡](../support/index.html#contacting-bluemix-support){: new_window}。 




## 已超出磁碟限額
{: #ts_disk_quota}

如果您已耗盡磁碟空間，可以手動修改磁碟限額以取得更多磁碟空間。

  

當您耗盡磁碟空間時，可能會看到一則指出已超出磁碟限額的訊息。為解決此問題，您可能已嘗試擴充應用程式實例以取得更多磁碟空間。例如，您可能透過變更應用程式詳細資料頁面上的記憶體配額，從 256 MB 擴充為 1256 MB。不過，因為磁碟限額保持不變，所以您並未取得更多磁碟空間。
{: tsSymptoms}


配置給應用程式的預設磁碟限額是 1 GB。如果您需要更多磁碟空間，則必須手動指定磁碟限額。
{: tsCauses}

 
請使用下列其中一種方法來指定您的磁碟限額。您可以指定的磁碟限額上限是 2 GB。如果 2 GB 仍然不夠，請嘗試使用外部服務，例如 [Object Storage](../services/ObjectStorage/index.html){: new_window}。
{: tsResolve}

  * 在 manifest.yml 檔案中，新增下列項目：
    ```
	disk_quota: <disk_quota>
	```
  * 當您將應用程式推送至 {{site.data.keyword.Bluemix_notm}} 時，使用 **-k** 選項與 `cf push` 指令搭配：
```
	cf push appname -p app_path -k <disk_quota>
	```

	
	
## 無法新增 Git 儲存庫
{: #ts_cannot_addgit}

在「儀表板」上建立應用程式之後，您按一下「新增 GIT」以建立 Git 儲存庫，但無法繼續。



當您按一下**新增 GIT** 時，會開啟視窗，並發生下列其中一個問題：
{: tsSymptoms} 

  * 視窗會停滯並顯示空白畫面。
  * 訊息指出協力廠商 Cookie 有問題存在。



您的瀏覽器可能配置為避免設定 Cookie。該 Cookie 必須從 {{site.data.keyword.Bluemix_notm}} 主控台的環境定義內，從 hub.jazz.net 網際網路網域中的 IBM® Bluemix DevOps Services 網站設定。
{: tsCauses}  

 

您可以使用下列其中一種方法來修正此問題：
{: tsResolve}

  * 遵循從 {{site.data.keyword.Bluemix_notm}} 主控台開啟之視窗中的指示。按一下按鈕。隨即暫時性地開啟另一個瀏覽器視窗。在該視窗中，DevOps Services 會設定鑑別 Cookie。
  * 在另一個瀏覽器分頁中，前往 https://hub.jazz.net 並登入。回到 {{site.data.keyword.Bluemix_notm}} 主控台，然後重新整理頁面。再按一下**新增 GIT**。
  * 變更瀏覽器設定，以啟用協力廠商 Cookie，然後再按一下「新增 GIT」。如需關於配置設定的詳細資料，請參閱瀏覽器的文件：
    * [Mozilla Firefox](https://support.mozilla.org/en-US/kb/enable-and-disable-cookies-website-preferences#w_how-do-i-change-cookie-settings){: new_window}
	* [Google Chrome](https://support.google.com/chrome/answer/95647){: new_window}
	* [Apple Safari](https://support.apple.com/kb/PH17191){: new_window}
	* [Microsoft Internet Explorer](http://windows.microsoft.com/en-us/internet-explorer/delete-manage-cookies#ie=ie-11){: new_window} 如果那些暫行解決方法無法修正問題，請傳送電子郵件至 idslogin@jazz.net。



## Android 應用程式無法收到推送通知
{: #ts_push}

無法存取 Google 的特定地區中，Android 應用程式收不到您透過 IBM Push 服務送出的通知。在此情況下，您可以使用協力廠商服務作為暫行解決方法。

 

連結您的 Bluemix 應用程式的 Push 服務，並將訊息傳送至已登錄的裝置。不過，在特定地區，Android 平台上開發的應用程式收不到您的通知。
{: tsSymptoms}

 
IBM Push 服務使用「Google 雲端通訊 (GCM)」服務，將通知分派至 Android 平台上開發的行動式應用程式。若要讓 Android 應用程式收到通知，行動式應用程式必須可存取「Google 雲端通訊 (GCM)」服務。在 Android 應用程式無法呼叫到 GCM 服務的地區，Android 應用程式即無法接收推送通知。
{: tsCauses}

 
請使用不依賴 GCM 服務的協力廠商服務（例如 [Pushy](https://pushy.me){: new_window}、[igetui](http://www.getui.com/){: new_window} 及 [jpush](https://www.jpush.cn/){: new_window}），作為暫行解決方法。
{: tsResolve}



## 已超出組織的服務限制
{: #ts_servicelimit}

如果您是試用帳戶使用者，可能會在超出組織的服務限制時，無法在 {{site.data.keyword.Bluemix_notm}} 中建立應用程式。
 

嘗試在 {{site.data.keyword.Bluemix_notm}} 中建立應用程式時，您看到下列錯誤訊息：
{: tsSymptoms}

`BXNUI2032E: 未建立 <service_instances> 資源。聯絡 Cloud Foundry 以建立資源時發生錯誤。Cloud Foundry 訊息："You have exceeded your organization's services limit."`



當您超出帳戶可用的服務實例數目限制時，就會發生這個錯誤。試用帳戶的服務實例數目上限是 10。
{: tsCauses} 

 

請刪除不需要的任何服務實例，或移除您可以擁有之服務實例數目的限制。
{: tsResolve}
 
  * 若要刪除服務實例，您可以使用 {{site.data.keyword.Bluemix_notm}} 使用者介面或指令行介面。若要使用 {{site.data.keyword.Bluemix_notm}} 使用者介面來刪除服務實例，請完成下列步驟：
	  1. 在 {{site.data.keyword.Bluemix_notm}}「儀表板」上，按一下左窗格中的**服務**。隨即顯示服務磚。 
	  2. 在您想要刪除的服務磚上，按一下**功能表**圖示。
	  3. 按一下**刪除服務**。刪除服務實例之後，系統會提示您重新編譯打包服務實例所連結的應用程式。若要使用指令行介面來刪除服務實例，請完成下列步驟：
	  1. 鍵入 `cf unbind-service <appname> <service_instance_name>`，將服務實例與應用程式取消連結。
	  2. 鍵入 `cf delete-service <service_instance_name>`，以刪除服務實例。
	  3. 刪除服務實例之後，您可能會想要鍵入 `cf restage <appname>`，以重新編譯打包服務實例所連結的應用程式。
  * 若要移除您可以擁有之服務實例數目的限制，請將您的試用帳戶轉換成付費帳戶。如需如何將試用帳戶轉換成付費帳戶的相關資訊，請參閱[如何變更方案](../pricing/index.html#changing){: new_window}。

  
  
## 執行檔無法在 {{site.data.keyword.Bluemix_notm}} 上執行
{: #ts_executable}

在不同環境中開發及建置的執行檔，可能無法在 {{site.data.keyword.Bluemix_notm}} 上執行。 

 

在不同環境中開發及建置的執行檔，無法在 {{site.data.keyword.Bluemix_notm}} 上執行。
{: tsSymptoms}

 

如果您想要推送至 {{site.data.keyword.Bluemix_notm}} 的內容已經是執行檔，表示該內容先前就已建置好，不需要在 {{site.data.keyword.Bluemix_notm}} 上建置。在此情況下，執行檔不需要任何建置套件，就可以在 {{site.data.keyword.Bluemix_notm}} 上執行。不過，您必須明確地向 {{site.data.keyword.Bluemix_notm}} 指出不需要任何建置套件。
{: tsCauses}

 

當您將執行檔推送至 {{site.data.keyword.Bluemix_notm}} 時，必須指定 null-buildpack，表示不需要任何建置套件。請使用 **-b** 選項搭配 `cf push` 指令來指定 null-buildpack：
{: tsResolve}

```
cf push appname -p <app_path> -c <start_command> -b <null-buildpack>
```
例如：
```
cf push appname -p <app_path> -c ./RunMeNow -b https://github.com/ryandotsmith/null-buildpack
```


## 已超出組織的記憶體限制
{: #ts_outofmemory}

如果您是試用帳戶使用者，則超出組織的記憶體限制時，您可能無法將應用程式部署至 {{site.data.keyword.Bluemix_notm}}。您可以減少應用程式所使用的記憶體，或增加帳戶的記憶體配額。 



將應用程式部署至 {{site.data.keyword.Bluemix_notm}} 時，您看到下列錯誤訊息：
{: tsSymptoms} 

`FAILED Server error, status code: 400, error code: 100005, message: You have exceeded your organization's memory limit.`

 

當組織剩餘的記憶體數量少於您想要部署之應用程式所需的記憶體數量時，就會發生這個錯誤。試用帳戶的記憶體配額上限為 2 GB。
{: tsCauses}



您可以增加帳戶的記憶體配額，或減少應用程式所使用的記憶體。
{: tsResolve} 

  * 若要增加帳戶的記憶體配額，請將試用帳戶轉換成付費帳戶。如需如何將試用帳戶轉換成付費帳戶的相關資訊，請參閱[付費帳戶](../pricing/index.html#pay-accounts){: new_window}。 
  * 若要減少應用程式所使用的記憶體，請使用 {{site.data.keyword.Bluemix_notm}} 使用者介面或 cf 指令行介面。如果您使用 {{site.data.keyword.Bluemix_notm}} 使用者介面，請完成下列步驟：
	  1. 在 {{site.data.keyword.Bluemix_notm}}「儀表板」上，選取您的應用程式。即會開啟應用程式詳細資料頁面。
	  2. 在「執行時期」窗格中，您可以針對您的應用程式減少記憶體上限及（或）應用程式實例的數目。如果您使用 cf 指令行介面，請完成下列步驟：
	  1. 檢查有多少記憶體用於應用程式：
```
	  cf apps
	  ```
	     cf apps 指令會列出您在現行空間中部署的所有應用程式。也會顯示每個一應用程式的狀態。
      2. 若要減少應用程式所使用的記憶體數量，請減少應用程式實例的數目及（或）記憶體上限：
```
	  cf push <appname> -p <app_path> -i <instance_number> -m <memory_limit>
      ```
	  3. 重新啟動應用程式，讓變更生效。



	  
## 應用程式不會自動重新啟動
{: #ts_apps_not_auto_restarted}


當連結至應用程式的服務停止運作時，不會自動重新啟動應用程式。	  
	  
 

當連結至應用程式的服務損毀時，應用程式可能會發生運作中斷、異常狀況和連線失敗之類的問題。{{site.data.keyword.Bluemix_notm}} 不會自動重新啟動應用程式，以從這些問題中回復。
{: tsSymptoms}



此行為是 Cloud Foundry 的設計。
{: tsCauses} 

 

您可以在指令行介面中鍵入下列指令，以手動重新啟動應用程式：
{: tsResolve}

```
cf push <appname> -p <app_path>
```
此外，您可以將應用程式編碼成可識別運作中斷、異常狀況和連線失敗之類的問題，並從其中回復。 

	  

## 推送應用程式時遺失使用者定義變數
{: #ts_varsnotretained}

當您從 IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} 推送應用程式至 {{site.data.keyword.Bluemix_notm}} 時，您指定的變數會重設，除非您將變數儲存至資訊清單檔。



在您從 IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} 推送應用程式至 {{site.data.keyword.Bluemix_notm}} 之後，您指定的變數會遺失。
{: tsSymptoms} 


唯有在您將指定的變數儲存到資訊清單檔時，才會儲存您指定的變數。
{: tsCauses} 

 

當您從 IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} 推送應用程式至 {{site.data.keyword.Bluemix_notm}} 時，請在「應用程式」精靈的「應用程式詳細資料」頁面中，選取**儲存至資訊清單檔**勾選框。然後，您在精靈中指定的變數便會儲存到應用程式的資訊清單檔。下次開啟精靈時，會自動顯示變數。
{: tsResolve}



## {{site.data.keyword.Bluemix_notm}} Live Sync 圖示未顯示
{: #ts_llz_lkb_3r}

您已在 IBM Bluemix DevOps Services 中建立應用程式，但是 IBM Bluemix Live Sync 圖示未顯示在 Web IDE 中。

 

當您在 DevOps Services Web IDE 中編輯 Node.js 應用程式時，未顯示 {{site.data.keyword.Bluemix_notm}} 即時編輯、快速重新啟動和除錯圖示。
{: tsSymptoms}

 

在下列情況下，無法使用這些圖示：
{: tsCauses}

  * `manifest.yml` 檔案未儲存在專案的最上層。
  * 您的應用程式儲存在子目錄中，而不是專案的最上層，但卻未於 `manifest.yml` 檔案中指定該子目錄的路徑。
  * 應用程式未包含 `package.json` 檔案。


請使用下列其中一種方法來解決問題：
{: tsResolve} 

  * 如果 `manifest.yml` 檔案未儲存在專案的最上層，請將它儲存在那裡。
  * 如果應用程式儲存在子目錄中，請在 `manifest.yml` 檔案中指定該子目錄的路徑。
  ```
   path: path_to_application
   ```
  * 在與應用程式相同的目錄中，建立 `package.json` 檔案。

  
  
  

  
  

  
  
## 在 {{site.data.keyword.Bluemix_notm}} 上找不到組織
{: #ts_orgs}

在使用 {{site.data.keyword.Bluemix_notm}} 地區時，可能找不到 {{site.data.keyword.Bluemix_notm}} 上的組織。
  
 

您可以順利登入 {{site.data.keyword.Bluemix_notm}} 使用者介面，但無法利用 cf 指令行介面或 Eclipse 外掛程式推送應用程式。
{: tsSymptoms}

嘗試使用 cf 指令行介面將應用程式推送至 {{site.data.keyword.Bluemix_notm}} 時，您看到下列其中一則錯誤訊息，且訊息中指定了組織名稱： 

`尋找組織時發生錯誤`

`找不到組織`


嘗試使用 Cloud Foundry Eclipse 外掛程式將應用程式推送至 {{site.data.keyword.Bluemix_notm}} 時，您看到下列錯誤訊息：

`找不到 cloudspace。`



這個問題的發生原因是未指定您要使用之地區的 API 端點，而您在尋找的組織可能在不同的地區中。
{: tsCauses} 

   
  
如果您使用 cf 指令行介面將應用程式推送至 {{site.data.keyword.Bluemix_notm}}，請輸入 cf api 指令，並指定地區的 API 端點。例如，輸入下列指令以連接 {{site.data.keyword.Bluemix_notm}} 歐洲英國地區：
{: tsResolve}

```
cf api https://api.eu-gb.bluemix.net
```
如果您使用 Eclipse 工具將應用程式推送至 {{site.data.keyword.Bluemix_notm}}，則必須先建立 {{site.data.keyword.Bluemix_notm}} 伺服器，並指定您組織建立所在 {{site.data.keyword.Bluemix_notm}} 地區的 API 端點。如需使用 Eclipse 工具的相關資訊，請參閱[使用 IBM Eclipse Tools for Bluemix 部署應用程式](../manageapps/eclipsetools/eclipsetools.html){: new_window}。  
  
  


## 無法建立應用程式路徑
{: #ts_hostistaken}

將應用程式部署至 {{site.data.keyword.Bluemix_notm}} 時，如果指定的主機名稱已被使用，則無法建立應用程式路徑。



將應用程式部署至 {{site.data.keyword.Bluemix_notm}} 時，您看到下列錯誤訊息：
{: tsSymptoms} 

`Creating route hostname.domainname ... FAILED Server error, status code: 400, error code: 210003, message: The host is taken: hostname`



如果已使用指定的主機名稱，則會發生此問題。
{: tsCauses} 


  
在您使用的網域內，您指定的主機名稱必須是唯一的。若要指定不同的主機名稱，請使用下列其中一種方法：
{: tsResolve} 

  * 如果您使用 `manifest.yml` 檔案來部署應用程式，請在 host 選項中指定主機名稱。
```
    host: <hostname>	
	```
  * 如果您從命令提示字元部署應用程式，請搭配使用 `cf push` 指令與 **-n** 選項。
```
    cf push <appname> -p <app_path> -n <hostname>
    ```


## WAR 應用程式無法使用 cf push 指令進行推送
{: #ts_cf_war}

如果未正確地指定應用程式位置，則可能無法使用 cf push 指令將保存的 Web 應用程式部署至 {{site.data.keyword.Bluemix_notm}}。
	


使用 `cf push` 指令將 WAR 應用程式上傳至 {{site.data.keyword.Bluemix_notm}} 時，您看到此錯誤訊息：`編譯打包錯誤：無法取得實例，因為編譯打包失敗。`
{: tsSymptoms} 

 

如果未指定 WAR 檔，或未指定 WAR 檔的路徑，則可能會發生此問題。
{: tsCauses}

 	
	
請使用 **-p** 選項來指定 WAR 檔，或新增 WAR 檔的路徑。例如：
{: tsResolve}

```
cf push MyUniqueAppName01 -p app.war
```

```
cf push MyUniqueAppName02 -p "./app.war"
```
如需 `cf push` 指令的相關資訊，請輸入 `cf push -h`。 	





## 將 Liberty 應用程式推送至 {{site.data.keyword.Bluemix_notm}} 未適當地顯示雙位元組字元
{: #ts_doublebytes}

如果未適當地配置 Servlet 或 JSP 檔的 Unicode 支援，則可能無法適當地顯示雙位元組字元。

 

將 Liberty 應用程式推送至 {{site.data.keyword.Bluemix_notm}} 時，無法適當地顯示應用程式內所指定的雙位元組字元。
{: tsSymptoms}

 

如果未適當地配置 Servlet 或 JSP 檔的 Unicode 支援，則可能會發生此問題。
{: tsCauses}


您可以在 Servlet 或 JSP 檔內使用下列程式碼：
{: tsResolve} 

  * 在 Servlet 原始檔中
    ```
	response.setContentType("text/html; charset=UTF-8");
	```
  * 在 JSP 中
    ```
	<meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
	```
	
	
	

## 無法部署 Node.js 應用程式
{: #ts_nodejs_deploy}

當您更新 Node.js 應用程式或部署 Node.js 應用程式到 {{site.data.keyword.Bluemix_notm}} 時可能遭遇問題。



當您更新 Node.js 應用程式或部署 Node.js 應用程式到 {{site.data.keyword.Bluemix_notm}} 時，可能會看到下列其中一則錯誤訊息：
{: tsSymptoms} 

`應用程式未順利由任何可用的建置套件偵測到。`


`實例（索引 0）無法開始接受連線。`


`無法取得實例，因為編譯打包失敗。`


 

下列原因是問題的可能原因：
{: tsCauses}
 
  * 未指定啟動指令。
  * 部署 Node.js 應用程式所需的檔案從應用程式中遺漏，或是放在非根目錄的資料夾中。
  


	
請根據導致問題的原因採取下列動作：
{: tsResolve} 

  * 以下列其中一種方法指定啟動指令： 
      * 使用 cf 指令行介面。例如：
```
		cf push MyUniqueNodejs01 -p app_path -c "node app.js"
		```
	  * 使用 [package.json](https://docs.npmjs.com/json){: new_window} 檔案。例如：
	    ```
		{
      ...
  	   "scripts": {
	 		 "start": "node app.js"
 	   }
	}
	    ```
	  * 使用 `manifest.yml` 檔案。例如：
	    ```
		applications:
  name: MyUniqueNodejs01
  ...
  command: node app.js
  ...
        ```

  * 確定 `package.json` 檔案存在於您的 Node.js 應用程式中，以讓 Node.js 建置套件能辨識應用程式。此外，您必須將這個檔案放在應用程式的根目錄。下列範例顯示簡單的 `package.json` 檔案：
	```
	{
        "name": "MyUniqueNodejs01",
        "version": "0.0.1",
        "description": "A sample package.json file",
        "dependencies": {
                "express": "3.4.x",
                "jade": "1.1.x"
        },
        "engines": {
                "node": "0.10.x"
        },
        "scripts": {
                  "start": "node app.js"
        }
 }
    ```
	
如需 Node.js 應用程式的相關提示，請參閱 [Tips for Node.js Applications](http://docs.cloudfoundry.org/buildpacks/node/node-tips.html){: new_window}。	




## 將 {{site.data.keyword.Bluemix_notm}} Liberty 應用程式從 Bluemix DevOps Services 匯入至 Eclipse 之後，`server.xml` 檔案中出現配置錯誤
{: #ts_eclipse}

如果您在將 {{site.data.keyword.Bluemix_notm}} Liberty 應用程式從 IBM Bluemix DevOps Services 匯入至 Eclipse 之後，於 `server.xml` 檔案中看到配置錯誤，則可能需要移除專案中的 `server.xml` 檔案。 

 

將 {{site.data.keyword.Bluemix_notm}} Liberty 應用程式從 {{site.data.keyword.Bluemix_notm}} DevOps Services 匯入至 Eclipse 之後，從「Eclipse 問題」視圖中，在 `server.xml` 檔案內看到配置錯誤。
{: tsSymptoms}

 

Liberty 建置套件會使用 `server.xml` 檔案來配置應用程式，並且在將 Liberty 應用程式推送至 {{site.data.keyword.Bluemix_notm}} 時產生 `runtime-vars.xml` 檔案。將應用程式匯入至 Eclipse 時，本端環境中沒有 `runtime-vars.xml` 檔案。
{: tsCauses}

 

您可以移除專案中的 server.xml 檔案，來解決此問題。將應用程式推送為 WAR 應用程式時，此建置套件會動態建立 `server.xml` 檔案。如需相關資訊，請參閱 [Liberty for Java](../runtimes/liberty/index.html){: new_window}。
{: tsResolve}
	
	
## 使用自訂建置套件無法編譯打包應用程式
{: #ts_bp_compilation}

如果自訂建置套件內的 Script 無法執行，則可能無法使用該建置套件將應用程式部署至 {{site.data.keyword.Bluemix_notm}}。



使用自訂建置套件將應用程式部署至 {{site.data.keyword.Bluemix_notm}} 時，您看到此錯誤訊息：`無法編譯打包應用程式，因此沒有可顯示的實例。`
{: tsSymptoms} 


如果 Script（例如偵測 Script、編譯 Script 及釋放 Script）無法執行，則可能會發生此問題。
{: tsCauses}

 

您可以使用 [git update](http://git-scm.com/docs/git-update-index){: new_window} 指令，將每一個 Script 的許可權變更為「可執行」。例如，您可以鍵入 `git update --chmod=+x script.sh`。
{: tsResolve}
	
	
	
## 無法將應用程式從 DevOps Services 部署至 {{site.data.keyword.Bluemix_notm}}
{: #ts_devops_to_bm}

如果應用程式內沒有 `manifest.yml` 檔案，則可能無法將應用程式從 IBM Bluemix DevOps Services 推送至 {{site.data.keyword.Bluemix_notm}}。

 

將應用程式從 DevOps Services 部署至 {{site.data.keyword.Bluemix_notm}} 時，可能會顯示此錯誤訊息：`偵測不到支援的應用程式類型`。
{: tsSymptoms}

 

因為 DevOps Services 需要 `manifest.yml` 檔案，才能將應用程式部署至 {{site.data.keyword.Bluemix_notm}}，所以可能會發生此問題。
{: tsCauses}

 

若要解決此問題，您必須建立 `manifest.yml` 檔案。如需如何建立 `manifest.yml` 檔案的相關資訊，請參閱[應用程式資訊清單](../manageapps/depapps.html#appmanifest){: new_window}。
{: tsResolve}	
	




## 無法推送 Meteor 應用程式
{: #ts_meteor}

如果未正確地指定建置套件，則可能無法將 Meteor 應用程式推送至 {{site.data.keyword.Bluemix_notm}}。

 

當您將 Meteor 應用程式部署至 {{site.data.keyword.Bluemix_notm}} 時，可能會看到此錯誤訊息：`無法編譯打包應用程式，因此沒有可顯示的實例。`
{: tsSymptoms}


此問題的發生原因是未針對 Meteor 應用程式提供內建的建置套件。您必須使用自訂建置套件。
{: tsCauses} 


 

若要針對 Meteor 應用程式使用自訂建置套件，請使用下列其中一種方法：
{: tsResolve}

  * 如果您使用 `manifest.yml` 檔案來部署應用程式，請使用 buildpack 選項指定自訂建置套件的 URL 或名稱。例如：
  ```
  buildpack: https://github.com/Sing-Li/bluemix-bp-meteor
  ```
  * 如果您從命令提示字元部署應用程式，請使用 `cf push` 指令，並使用 **-b** 選項指定自訂建置套件。例如：
  ```
	cf push appname -p app_path -b https://github.com/Sing-Li/bluemix-bp-meteor 
	```
	
  

    
## 「部署至 {{site.data.keyword.Bluemix_notm}} 按鈕」未部署應用程式
{: #deploytobluemixbuttondoesntdeployanapp}

如果您按一下「部署至 {{site.data.keyword.Bluemix_notm}}」按鈕，但發現未複製 Git 儲存庫，或是未部署應用程式，請嘗試使用下列問題的疑難排解方法。
  * [無法建立 Bluemix DevOps Services 專案](#project-cannot-be-created)
  * [在 DevOps Services 中找不到且無法複製 Git 儲存庫](#repo-not-found)
  * [已在 DevOps Services 中複製 Git 儲存庫，但應用程式未部署至 {{site.data.keyword.Bluemix_notm}}](#repo-cloned-app-not-deployed)
如需如何建立該按鈕的相關資訊，請參閱『建立「部署至 {{site.data.keyword.Bluemix_notm}}」按鈕』。

### 無法建立 Bluemix DevOps Services 專案
{: #project-cannot-be-created}

如果您發現無法建立 DevOps Services 專案，可能是因為您的 IBM {{site.data.keyword.Bluemix_notm}} 帳戶已過期。



您按一下**部署至 Bluemix** 按鈕，但「建立專案」步驟未順利完成。
{: tsSymptoms} 


您的 {{site.data.keyword.Bluemix_notm}} 帳戶可能已過期。
{: tsCauses} 

請使用下列其中一種方法來修正問題：
{: tsResolve}

  * 登入 {{site.data.keyword.Bluemix_notm}}，並更新您的帳戶資訊。
  * 再按一下**部署至 Bluemix** 按鈕。


### 在 DevOps Services 中找不到且無法複製 Git 儲存庫
{: #repo-not-found}

如果您發現未複製 Git 儲存庫，可能是因為儲存庫或按鈕 Snippet 有問題。



您按一下**部署至 Bluemix** 按鈕，但是在 DevOps Services 中找不到且無法複製 Git 儲存庫。「複製儲存庫」步驟未順利完成。因此，無法將應用程式部署至 {{site.data.keyword.Bluemix_notm}}。
{: tsSymptoms} 

此問題的可能發生原因如下：
{: tsCauses} 

  * Git 儲存庫可能不存在或無法存取。
  * 按鈕 Snippet 的 HTML 或 Markdown 可能有問題。
  * URL 中可能有特殊字元、查詢參數或片段的問題，導致無法正確地存取 Git 儲存庫。

請使用下列其中一種方法來修正問題：
{: tsResolve}

  * 驗證您的 Git 儲存庫已存在、可公開存取，而且 URL 正確無誤。
  * 驗證 Snippet 未包含任何 HTML 或 Markdown 錯誤。
  * 如果特殊字元、查詢參數或片段導致 Git 儲存庫 URL 發生問題，請在按鈕 Snippet 中將 URL 編碼。
  

  
  
### 已在 DevOps Services 中複製 Git 儲存庫，但應用程式未部署至 {{site.data.keyword.Bluemix_notm}}
{: #repo-cloned-app-not-deployed}

如果您發現未部署應用程式，可能是儲存庫中的程式碼有問題。
     


您按一下**部署至 Bluemix** 按鈕，且已在 DevOps Services 中複製 Git 儲存庫，但應用程式未部署至 {{site.data.keyword.Bluemix_notm}}。「部署至 Bluemix」步驟未順利完成。
{: tsSymptoms} 

此問題的可能發生原因如下：
{: tsCauses}  

  * 可能是您的 {{site.data.keyword.Bluemix_notm}} 空間中沒有足夠的空間可以部署應用程式。 
  * `manifest.yml` 檔案中可能未宣告必要的服務。
  * `manifest.yml` 檔案中可能宣告必要的服務，但是該服務已在目標空間中。
  * 可能是儲存庫中的程式碼有問題。若要診斷此問題，請檢閱部署所產生的建置和部署日誌：
  1. 當「部署至 Bluemix」步驟未順利完成時，請按一下先前「配置管線」步驟中的鏈結，以開啟 Delivery Pipeline。
  2. 識別失敗的建置或部署編譯打包。
  3. 在失敗的編譯打包中，按一下**檢視日誌及歷程**。
  4. 尋找錯誤訊息。
   
請使用下列其中一種方法來修正問題：
{: tsResolve}

  * 如果錯誤訊息指出 {{site.data.keyword.Bluemix_notm}} 空間中沒有足夠的空間可以部署應用程式，請以其他空間作為目標。
  * 如果錯誤訊息指出 `manifest.yml` 檔案中未宣告必要的服務，請通知儲存庫擁有者必須新增必要的服務。
  * 如果錯誤訊息指出目標空間中已經有必要的服務，請選取其他的空間來使用。
  * 如果錯誤訊息指出建置有問題，請修正導致無法建置應用程式的任何程式碼問題。若要驗證程式碼沒有任何問題，請使用 Git 指令來建置程式碼：
    1. 複製 Git 儲存庫：
    ```
    git clone <git_repository_URL>
    ```
	2. 開啟應用程式目錄：
	```
	cd <appname>
	```
	3. 建立應用程式：
	```
	<appname> create
	```
	4. 必要的話，請佈建附加程式。
	5. 新增任何必要的配置變數。
	6. 推送程式碼：
	```
	git push <appname> master
	```
	7. 驗證已正確建置應用程式。
	8. 必要的話，請執行後置部署指令：
	```
	<appname> run
	```
	9. 開啟應用程式，並驗證其運作正常：
	```
	<appname> open
	```
	



# 管理帳戶疑難排解
{: #managingaccounts}

您可能會在管理帳戶時遇到問題，例如不同的應用程式共用相同的網域名稱、管理者無法檢視所有組織等等。然而，在許多情況下，您可以依照下列一些簡單的步驟，從這些問題中回復。
{:shortdesc}


## 帳戶處於非作用中
{: #ts_accnt_inactive}

如果帳戶處於非作用中，則您無法在 {{site.data.keyword.Bluemix_notm}} 中建立應用程式。您必須與支援團隊聯絡以修正此問題。



嘗試在 {{site.data.keyword.Bluemix_notm}} 中建立應用程式時，您看到下列錯誤訊息：
{: tsSymptoms} 

`BXNUI0096E: 未建立應用程式。您的帳戶處於非作用中狀態，因為它已取消或已暫停。`


當帳戶遭到取消或暫停時，{{site.data.keyword.Bluemix_notm}} 帳戶的狀態會變成非作用中。
{: tsCauses}

 

若要重新啟動您的帳戶，請與 [{{site.data.keyword.Bluemix_notm}} 支援中心](http://ibm.biz/bluemixsupport.com){: new_window}聯絡。在電子郵件中，您必須包含下列資訊：
{: tsResolve}

  * 您用來登入 {{site.data.keyword.Bluemix_notm}} 的 IBM ID。
  * 您的應用程式建立所在的組織名稱。此資訊可幫助支援團隊判斷您是否已在組織內獲指派正確的角色或成員資格。



## 沒有空間與現行組織相關聯
{: #ts_no_space}

如果沒有空間與您的現行組織相關聯，則您無法建立應用程式。



嘗試在 {{site.data.keyword.Bluemix_notm}} 中建立應用程式時，您看到下列錯誤訊息：
{: tsSymptoms} 


`BXNUI0097E: 在新增應用程式之前，必須至少有一個空間與您的組織和地區相關聯。在「儀表板」上，按一下「建立空間」。建立空間後，請重試。`



{{site.data.keyword.Bluemix_notm}} 中的應用程式必須在組織下的空間內建立。
{: tsCauses} 

 

若要建立空間，請使用下列其中一種方法：
{: tsResolve}
 
  * 在 {{site.data.keyword.Bluemix_notm}}「儀表板」上，選取您要在其中建立空間的組織，然後按一下**建立空間**。
  * 在 cf 指令行介面中，鍵入 ```cf create-space <space_name> -o <organization_name>```。
  
  
  
  
## 不同應用程式的網域名稱相同
{: #ts_domain_diff}

您可能注意到 {{site.data.keyword.Bluemix_notm}} 中有數個應用程式共用相同的 URL。

 

將相同的 URL 路徑指派給空間內的不同應用程式時，可能會發生此問題。
{: tsCauses}

例如，您將 myApp1 應用程式推送至 {{site.data.keyword.Bluemix_notm}}，並將網域設為 "mynewapp.mybluemix.net"。然後，將另一個 myApp2 應用程式推送至相同的空間，並將它的其中一個 URL 路徑設為 "mynewapp.mybluemix.net"。路徑現在對映至兩個應用程式。

 

這是 {{site.data.keyword.Bluemix_notm}} 的支援行為，而且您可以使用此作法，讓應用程式升級達到零中斷時間。如需相關資訊，請參閱藍綠部署。
{: tsResolve}
  
	
	





## 無法新增信用卡
{: #ts_addcc}

您無法提交信用卡資訊，以將試用帳戶轉換為「隨收隨付制」帳戶。

 

「新增信用卡」頁面上的「提交」按鈕會被停用。
{: tsSymptoms}

 

若您的資訊未正確地填入「新增信用卡」頁面中，即會發生此問題。
{: tsCauses}

 

請完成下列步驟，以解決此問題：
{: tsResolve}

  1. 在「新增信用卡」頁面上，填入聯絡資訊、聯絡地址及帳單地址區段中的所有必要欄位。
  2. 選取**我已閱讀並同意 IBM 條款**，然後按一下**提交**。即會顯示**選取付款方法**區段。
  3. 輸入信用卡上的信用卡號碼、信用卡到期日及安全碼。然後，按一下**提交**。





# 執行時期疑難排解
{: #runtimes}

您在使用 IBM® Bluemix™ 執行時期時可能會遇到問題。然而，在許多情況下，您可以依照下列一些簡單的步驟，從這些問題中回復。
{:shortdesc}


## 推送應用程式時從快取載入了已作廢的建置套件
{: #ts_loading_bp}


您推送應用程式時可能無法使用最新的建置套件元件。您可以使用具有內建機制的建置套件，以避免載入已作廢的元件，或者您可以刪除應用程式快取目錄中的內容，然後才推送或重新編譯打包應用程式。 

 

當您在建置套件更新之後推送或重新編譯打包應用程式時，不會自動載入最新的建置套件元件。因此，您的應用程式會使用已作廢的建置套件元件。將不會實作自從您前次推送應用程式後已套用至建置套件的更新。
{: tsSymptoms}



部分建置套件未配置為自動從網際網路下載所有更新的元件，以確保您隨時使用最新的版本。
{: tsCauses} 

 

您可以使用具有內建機制的建置套件來避免載入已作廢的元件。下列建置套件是其中兩個範例：
{: tsResolve}

  * [Cloud Foundry Java 建置套件](https://github.com/cloudfoundry/java-buildpack){: new_window}。這個建置套件具有內建的機制，可以確保使用最新版本的建置套件。如需此機制運作方式的相關資訊，請參閱 [extending-caches.md](https://github.com/cloudfoundry/java-buildpack/blob/master/docs/extending-caches.md){: new_window}。 
  * [Cloud Foundry Node.js 建置套件](https://github.com/cloudfoundry/nodejs-buildpack){: new_window}。這個建置套件功能與使用環境變數類似。為了讓 Node.js 建置套件能每次從網際網路下載 node 模組，請在 cf 指令行介面中，鍵入下列指令：
```
  set NODE_MODULES_CACHE=false
  ```
如果您使用的建置套件未提供自動載入最新元件的機制，可以手動刪除快取目錄中的內容，然後採取下列步驟來重新推送應用程式：
  1. 移出空值建置套件的分支，例如 https://github.com/ryandotsmith/null-buildpack。如需如何移出分支的相關資訊，請參閱 [Git Basics - Getting a Git Repository](http://www.git-scm.com/book/en/v2/Git-Basics-Getting-a-Git-Repository){: new_window}。  
  2. 將下行新增到 `null-buildpack/bin/compile` 檔案並確定變更。如需如何確定變更的相關資訊，請參閱 [Git Basics - Recording Changes to the Repository](http://www.git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository){: new_window}。
```
  rm -rfv $2/*
  ```
  3. 使用下列指令，用已修改的空值建置套件推送應用程式，以刪除快取。完成此步驟之後，應用程式快取目錄中的所有內容都會刪除。
```
  cf push appname -p app_path -b <modified_null_buildpack>
  ```
  4. 使用下列指令，用您想要使用的最新建置套件來推送應用程式：
```
  cf push appname -p app_path -b <latest_buildpack>
  ```
  
	


## PHP 建置套件產生的 NOTICE 訊息
{: #ts_phplog}

您可能會在日誌中看到包含 NOTICE 的訊息。您可以變更記載層次，以停止記載這些訊息。	
	
 

當您使用 PHP 建置套件將應用程式推送至 Bluemix 時，可能會看到包含 `NOTICE` 的訊息：
{: tsSymptoms}

```
• 2015-01-26T15:00:59.70+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: [pool www] 'user' directive is ignored when FPM is not running as root
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: [pool www] 'user' directive is ignored when FPM is not running as root
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: fpm is running, pid 93
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: ready to handle connections
```



在 PHP 建置套件中，error_log 參數可用來定義記載層次。依預設，`error_log` 參數的值為 **stderr notice**。下列範例顯示 Cloud Foundry 所提供之 PHP 建置套件的 `nginx-defaults.conf` 檔案中的預設記載層次配置。如需相關資訊，請參閱 [cloudfoundry/php-buildpack](https://github.com/cloudfoundry/php-buildpack/blob/ff71ea41d00c1226d339e83cf2c7d6dda6c590ef/defaults/config/nginx/1.5.x/nginx-defaults.conf){: new_window}。
{: tsCauses} 

```
daemon off;
error_log stderr notice;
pid @{HOME}/nginx/logs/nginx.pid;
```

 	
	
`NOTICE` 訊息是參考資訊，不一定表示有發生問題。若要停止記載這些訊息，您可以在建置套件的 nginx-defaults.conf 檔案中，將記載層次從 stderr notice 變更為 stderr error。例如：
{: tsResolve}

```
daemon off;
error_log stderr error;
pid @{HOME}/nginx/logs/nginx.pid;
```
如需如何變更預設記載配置的相關資訊，請參閱 [error_log](http://nginx.org/en/docs/ngx_core_module.html#error_log){: new_window}。
	

## 無法將協力廠商的 Python 檔案庫匯入 {{site.data.keyword.Bluemix_notm}}
{: #ts_importpylib}

您可能無法將協力廠商的 Python 檔案庫匯入 {{site.data.keyword.Bluemix_notm}}。將配置檔新增至 Python 應用程式的根目錄中，即可解決這個問題。


當您嘗試匯入協力廠商的 Python 檔案庫（例如 `web.py` 檔案庫）時，`cf push` 指令會失敗。
{: tsSymptoms}


 

當 Python 應用程式的配置資訊遺失時，就會發生這個問題。
{: tsCauses}


 

若要解決此問題，請在 Python 應用程式的根目錄中，新增 `requirements.txt` 檔案及 `Procfile` 檔案。下列資訊是假設您要匯入 web.py 檔案庫：
{: tsResolve}

  1. 在 Python 應用程式的根目錄中，新增 `requirements.txt` 檔案。`requirements.txt` 檔案可指定 Python 應用程式所需的檔案庫套件，以及套件的版本。下列範例顯示 `requirements.txt` 檔案的內容，其中 `web.py==0.37` 表示將要下載的 `web.py` 檔案庫版本為 0.37，而 `wsgiref==0.1.2` 表示 web.py 檔案庫所需的 Web 伺服器閘道介面版本為 0.1.2。
	 ```
	 web.py==0.37
     wsgiref==0.1.2
	 ```
	如需如何配置 `requirements.txt` 檔案的相關資訊，請參閱[需求檔案](https://pip.readthedocs.org/en/1.1/requirements.html)。 
	 
  2. 在 Python 應用程式的根目錄中，新增 `Procfile` 檔案。`Procfile` 檔案必須包含 Python 應用程式的啟動指令。在下列指令中，*yourappname* 是 Python 應用程式的名稱，而 *PORT* 是 Python 應用程式必須用來接收應用程式使用者要求的埠號。*$PORT* 是選用項目。如果您未於啟動指令中指定 PORT，則會改用應用程式內部的 `VCAP_APP_PORT` 環境變數下的埠號。
```
	web: python <yourappname>.py $PORT
	```
您現在可以將協力廠商的 Python 檔案庫匯入 {{site.data.keyword.Bluemix_notm}} 了。	



## 已停用「實例詳細資料」頁面上的「動作」按鈕
{: #ts_actionsbutton}



已停用「實例詳細資料」頁面上的「動作」按鈕。
{: tsSymptoms} 

 

此問題的發生原因如下：
{: tsCauses}

  * 應用程式不是 Java™ Web 應用程式。Runtime Management Utilities (RMU) 只支援使用 Liberty 建置套件所部署的 Web 應用程式。
  * 應用程式不是使用內嵌的 Liberty 建置套件所部署。
  * 應用程式是使用舊版 Liberty 建置套件所部署。



如果問題是舊版 Liberty 建置套件所造成，請在 {{site.data.keyword.Bluemix_notm}} 中重新部署應用程式。否則，您可以將下列用戶端應用程式日誌檔提供給支援團隊：
{: tsResolve} 

  * logs/messages.log
  * logs/stdout.log
  * logs/stderr.log
  

  
  
## 開啟追蹤或傾出視窗時需要認證
{: #ts_username}


 

開啟追蹤或傾出視窗時，需要使用者名稱及密碼。
{: tsSymptoms}

 

此問題的發生原因是登入階段作業逾時。
{: tsCauses}

 

解決方案是重新輸入使用者名稱及密碼。
{: tsResolve}




## 追蹤或傾出作業執行時發生錯誤
{: #ts_target}

 

當追蹤或傾出作業在執行時顯示錯誤訊息。訊息指出應用程式的目標實例不在執行中狀態：
{: tsSymptoms}

```
實例 0：已順利設定追蹤規格
實例 2：已順利設定追蹤規格
實例 1：應用程式 abcd 的目標實例 1 未處於執行中狀態。
實例 3：已順利設定追蹤規格
實例 4：已順利設定追蹤規格
```



此問題的發生原因如下：
{: tsCauses} 

  * 只有執行中應用程式實例才有追蹤或傾出管理功能。無法對已停止、啟動中或已損毀的應用程式實例執行追蹤或傾出作業。
  * 開啟追蹤或傾出對話框時，應用程式實例的狀態為變更中。 
  


解決方案是關閉視窗，然後再重新開啟。
{: tsResolve} 



## 實例具有不同的 traceSpecification 配置
{: #ts_different_config}

 

對於某個應用程式的不同實例，您可能會看到不同的 traceSpecification 配置。
{: tsSymptoms}

 

此問題的發生原因如下：
{: tsCauses}

  * 您先前可能已變更一個以上實例的配置。如果您變更某個實例的 traceSpecification 配置，則它不會套用至相同應用程式的其他實例。例如，您的應用程式使用 log4j，而且您具有這個應用程式的兩個實例。您可以將實例 0 的記載層次從 info 變更為 debug，但實例 1 的記載層次仍為 info。 
  * 應用程式橫向擴充，並具有新的實例。RMU 不會將現有實例的 traceSpecification 配置套用至新的橫向擴充實例。新的實例會使用預設配置。例如，您的應用程式使用 log4j，而且它有一個實例。您可以將此實例的記載層次從 info 變更為 debug。進行這項變更之後，如果您將應用程式橫向擴充至兩個實例，則新實例的記載層次是 info，而非 debug。
  


這是預期的行為。
{: tsResolve} 





## 已超出磁碟限額
{: #ts_diskquota}

您可能會在應用程式日誌中看到已超出磁碟限額。

 

您在應用程式的日誌中看到`已超出磁碟限額`訊息。
{: tsSymptoms}



此問題是下列其中一個原因所導致：
{: tsCauses} 

  * 傾出檔案是與執行中應用程式實例一起產生，而且檔案會耗盡配置的磁碟限額。一個應用程式實例的磁碟限額預設為 1 GB。您可以按一下**儀表板 > 應用程式 > 應用程式執行時期**，來檢查您的磁碟使用情形。下列範例顯示兩個應用程式實例的執行時期資訊（包括磁碟使用情形）：
```
    Instance	State	CPU	Memory Usage	Disk Usage


	0		Running	1.0%	344.8MB/512MB	236.8MB/1GB
	2		Running	2.3%	361.2MB/512MB	235.7MB/1GB
    ```
  * 磁碟限額受限於現行組織配額。
  
  


您可以使用下列其中一種方法來解決這個問題：
{: tsResolve} 

  * 在下載傾出檔案之後刪除它們。
  * 在部署資訊清單中包括下列項目，以較大的磁碟限額來重新部署應用程式：
    ```
	disk_quota: 2048
	```
	
	


