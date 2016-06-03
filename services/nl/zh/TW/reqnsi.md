---

copyright:
  years: 2015, 2016

---


{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}


#服務
{: #services}
*前次更新：2016 年 1 月 20 日*

您可以在 {{site.data.keyword.Bluemix}} 使用者介面的**型錄**中，在**服務**下找到可用的服務。
{:shortdesc}


{{site.data.keyword.Bluemix_notm}} 中為行動式應用程式提供了預先定義的服務。{{site.data.keyword.Bluemix_notm}} 讓您能輕鬆地為您的行動式應用程式實作、管理及擴充這些行動式服務。您可以將焦點放在應用程式邏輯和應用程式設計。

{{site.data.keyword.Bluemix_notm}} 會管理 Web 應用程式的中介軟體服務。應用程式開發人員可以指定他們需要的中介軟體服務。{{site.data.keyword.Bluemix_notm}} 接著會自動佈建指定中介軟體服務的新實例，並將服務實例連結至應用程式。

{{site.data.keyword.Bluemix_notm}} 以兩種方式顯示服務：依服務種類，以及依服務支援類型。



<dl>
<dt><strong>種類</strong></dt>
<dd>{{site.data.keyword.Bluemix_notm}} 服務會組織成為不同的種類。在每一個服務種類中，IBM 建立的服務會先列出，接著是協力廠商服務，再來則是社群服務。
</dd>
<dt><strong>支援</strong></dt>
<dd>針對 {{site.data.keyword.Bluemix_notm}} 服務提供了多種層次的支援。下表說明 {{site.data.keyword.Bluemix_notm}} 服務的一般支援資訊：</dd>
</dl>



|類型	|說明	|支援詳細資料|
|:------|:--------------|:--------------|
|IBM	|IBM 所提供且正式發行的服務。	|在 IBM 所提供且正式發行的服務中，判定為錯誤的問題會受到支援。支援會根據您設定的嚴重性來提供。如需問題單嚴重性的相關資訊，請參閱[與支援中心聯絡](../support/index.html#contacting-bluemix-support){: new_window}。|
|協力廠商	|由 IBM 以外的公司所提供的服務。	|協力廠商服務支援是由服務提供者所提供。如果是由 IBM 調查問題，且該問題經判定為協力廠商服務中的錯誤，IBM 並不負責提供修正程式。IBM 會視需要與協力廠商服務提供者分享分析資訊。|
|社群	|開放程式碼社群所提供的服務。	|社群服務支援是由「{{site.data.keyword.Bluemix_notm}} Developers 社群」所提供。如果是由 IBM 調查問題，且該問題經判定為社群服務中的錯誤，IBM 並不負責提供修正程式。|
|測試版	|尚未準備好進入正式作業且目前處於開發試用階段的服務。「測試版」服務可協助開發及行銷小組先評量服務價值，再正式發行該服務。	|在 IBM 所提供的測試版服務中判定為錯誤的問題會受到支援，但是 IBM 不負責提供修正程式。此外，還會將問題單的嚴重性指派為 3 或 4（適用時）。如需問題單嚴重性的相關資訊，請參閱[與支援中心聯絡](../support/index.html#contacting-bluemix-support){: new_window}。|
*表 1. {{site.data.keyword.Bluemix_notm}} 服務支援資訊*




{{site.data.keyword.Bluemix_notm}} 也有您可以試用的實驗性服務。若要檢視所有可用的實驗性服務、樣板及執行時期，請登入 {{site.data.keyword.Bluemix_notm}}，捲動至「型錄」底端，然後按一下 **{{site.data.keyword.Bluemix_notm}} 實驗型錄**。

實驗性服務可能不穩定，而且可能會變更，而與較舊版不相容。這些服務不建議用於正式作業環境。實驗性服務支援是透過「{{site.data.keyword.Bluemix_notm}} Developers 社群」所提供。如果是由 IBM 調查問題，且該問題經判定為實驗性服務中的錯誤，則 IBM 不負責提供修正程式。

若要在 {{site.data.keyword.Bluemix_notm}} 使用者介面、cf 指令行介面、IBM {{site.data.keyword.Bluemix_notm}} DevOps Services 或任何支援的工具中使用服務，請採取下列步驟：

1. 建立服務的實例。在大部分情況下，您建立應用程式時可以建立服務實例。


2. 識別使用新服務實例的應用程式。若為 Web 應用程式，您可以指定讓多個應用程式使用相同的服務實例，通常是為了資料共用的目的。


3. 在應用程式中撰寫自己的程式碼，以便與服務互動。

##各地區的服務

並非所有服務都能在每個 {{site.data.keyword.Bluemix_notm}} 地區使用。下表顯示 IBM 所提供的服務。



|服務	|可在美國南部地區使用	|可在歐洲英國地區使用 |可在澳洲雪梨地區使用|
|:----------|:------------------------------|:------------------|:------------------|
|{{site.data.keyword.activedeployshort}}	|是		|是		|否|
|{{site.data.keyword.alchemyapishort}} 		|是	   	|是  		|是|
|{{site.data.keyword.appsecshort}}		|是		|否		|否|
|{{site.data.keyword.alertnotificationshort}}|是		|否			|否		|
|{{site.data.keyword.APS_DA}}			|是		|否		|否|
|{{site.data.keyword.APS_MA}}			|是		|否		|否|
|{{site.data.keyword.amashort}}			|是		|是		|是|
|{{site.data.keyword.hadoopst}}			|是		|否		|否|
|{{site.data.keyword.APIM}}			|是		|是		|否|
|{{site.data.keyword.autoscaling}}		|是		|是		|是|
|{{site.data.keyword.bigicloudst}}		|是		|否		|否|
|{{site.data.keyword.rules_short}}		|是		|是		|否|
|{{site.data.keyword.cloudint}}			|是		|是		|否|
|{{site.data.keyword.cloudant}}			|是		|是		|否|
|{{site.data.keyword.conceptexpansionshort}}	|是		|是		|是|
|{{site.data.keyword.conceptinsightsshort}}	|是		|是		|是|
|{{site.data.keyword.dashdbshort}}		|是		|是		|否|
|{{site.data.keyword.datacshort}}		|是		|是		|是|
|{{site.data.keyword.DB2OnCloud_short}}		|是		|是		|是|
|{{site.data.keyword.deliverypipeline}}		|是		|是		|否|
|{{site.data.keyword.dialogshort}}		|是		|是		|是|
|{{site.data.keyword.documentconversionshort}}	|是		|是		|是|
|{{site.data.keyword.creshort}}			|是		|否		|否|
|{{site.data.keyword.game}}			|是		|是		|是|
|{{site.data.keyword.geospatialshort_Geospatial}}	|是	|是		|否|
|{{site.data.keyword.globalizationshort}}	|是		|否		|否|
|{{site.data.keyword.dataworks_short}}		|是		|是		|否|
|{{site.data.keyword.twittershort}}		|是		|是		|是|
|{{site.data.keyword.weather_short}}		|是		|是		|是|
|{{site.data.keyword.IntegrationTestingshort}}	|是		|是		|否|
|{{site.data.keyword.iot_short}}		|是		|否		|否|
|{{site.data.keyword.keymanagementserviceshort}}|否		|是		|否|
|{{site.data.keyword.languagetranslationshort}}	|是		|是		|否|
|{{site.data.keyword.messagehub}}		|是		|是		|否|
|{{site.data.keyword.messageresonanceshort}}	|是		|是		|否|
|{{site.data.keyword.APS_MAiOS}} 		|是		|否		|否|
|{{site.data.keyword.macm_short}}		|是		|是		|是|
|{{site.data.keyword.mobilemam}}		|是		|是		|否|
|{{site.data.keyword.mobiledata}}		|是		|是		|否|
|{{site.data.keyword.manda}}			|是		|是		|否|
|{{site.data.keyword.mqa}}			|是		|是		|否|
|{{site.data.keyword.mql}}			|是		|是		|否|
|{{site.data.keyword.nlclassifierlshort}} 	|是 		|是 		|是|
|{{site.data.keyword.objectstorageshort}}	|是		|否		|否|
|{{site.data.keyword.personalityinsightsshort}}	|是		|是		|是|
|{{site.data.keyword.mobilepush}}Push		|是		|是		|否|
|Push for iOS 8					|是		|是		|否|
|{{site.data.keyword.questionandanswershort}}	|是		|是		|是|
|{{site.data.keyword.rapidApps}}		|是		|是		|否|
|{{site.data.keyword.relationshipextractionshort}}	|是	|是		|是|
|{{site.data.keyword.retrieveandrankshort}}	|是 		|是 		|是|
|{{site.data.keyword.SecureGateway}}		|是		|是		|否|
|{{site.data.keyword.servicediscoveryshort}}	|是		|否		|否|
|{{site.data.keyword.sescashort}}		|是		|是		|是|
|{{site.data.keyword.ssofull}}			|是		|否		|否|
|{{site.data.keyword.speechtotextshort}}	|是 		|是	 	|是|
|{{site.data.keyword.sqldb}}			|是		|是		|否|
|{{site.data.keyword.staticanalyzershort}}	|是		|是		|否|
|{{site.data.keyword.streaminganalyticsshort}}	|是		|否		|否|
|{{site.data.keyword.texttospeechshort}} 	|是 		|是	 	|是|
|{{site.data.keyword.times}}			|是		|是		|否|
|{{site.data.keyword.toneanalyzershort}} 	|是 		|是 		|是|
|{{site.data.keyword.trackplan}}		|是		|是		|否|
|{{site.data.keyword.tradeoffanalyticsshort}}	|是		|是		|是|
|{{site.data.keyword.visualinsightsshort}}	|是		|是		|是|
|{{site.data.keyword.visualizationrenderingshort}} |是		|是		|否|
|{{site.data.keyword.workflow}}			|是		|是		|否|
|{{site.data.keyword.workloadscheduler}}	|是		|是		|否|
|{{site.data.keyword.xpagesservice_short}}	|是		|是		|否|
*表 2. 服務可用性*


# 將服務新增至您的應用程式
{: #add_service}
*前次更新：2016 年 3 月 8 日*

{{site.data.keyword.Bluemix}} 有一份服務清單，並代表開發人員管理它們。若要新增服務以供應用程式使用，您必須要求此服務的實例，並配置應用程式以與服務互動。

您可以用下列方式查看 {{site.data.keyword.Bluemix_notm}} 中可用的所有服務：


* 從 {{site.data.keyword.Bluemix_notm}} 使用者介面。檢視 {{site.data.keyword.Bluemix_notm}}「型錄」。
* 從 cf 指令行介面。使用 **cf marketplace** 指令。
* 從您自己的應用程式。使用 [GET /v2/services Services API](http://apidocs.cloudfoundry.org/197/services/list_all_services.html){: new_window}。

在開發應用程式時，您可以選取需要的服務。
當您選取時，{{site.data.keyword.Bluemix_notm}} 會與服務互動，並採取必要的步驟以佈建服務資源。不同服務類型的佈建處理程序可能不同。
例如，資料庫服務會建立資料庫，而行動式應用程式的推送通知服務則會產生配置資訊。


{{site.data.keyword.Bluemix_notm}} 會透過使用服務實例，將服務資源提供給應用程式。服務實例可以在 Web 應用程式之間共用。

如果在其他地區中管理的服務能用於那些地區，則您也可以使用那些服務。這些服務必須可從網際網路存取，並具有 API 端點。您必須用您編碼外部應用程式或協力廠商工具以使用 {{site.data.keyword.Bluemix_notm}} 服務的相同方式，手動編碼應用程式來使用這些服務。如需相關資訊，請參閱[讓外部應用程式及協力廠商工具能使用 {{site.data.keyword.Bluemix_notm}} 服務](#accser_external)。



## 要求新的服務實例
{: #req_instance}

若要要求新的服務實例，您必須使用 {{site.data.keyword.Bluemix_notm}} 使用者介面或 cf 指令行介面。

**附註：**當您指定服務名稱時，請避免使用非英文字母或數值字元的字元，因為結果可能無法預期。

如果您使用 {{site.data.keyword.Bluemix_notm}} 使用者介面來要求服務實例，請完成下列步驟：

1. 在 {{site.data.keyword.Bluemix_notm}} **型錄**中，按一下您要新增之服務的磚。
即會開啟「服務詳細資料」頁面。

2. 在「新增服務」窗格中，從**應用程式**清單選取您要將此服務實例連結至其中的應用程式。

3. 在**服務名稱**欄位鍵入名稱。
會提供預設服務名稱。您可以在欄位中變更名稱，或是將它保留不變。

4. 完成其他欄位或選擇，然後按一下**建立**。

如果您使用 cf 指令行介面來要求服務實例，請完成下列步驟：

1. 使用 **cf marketplace** 指令，以尋找所需服務的名稱及方案。

2. 使用下列指令來建立服務實例，其中 service_name 是服務的名稱、service_plan 是服務的方案，而 service_instance 是您要用於此服務實例的名稱。

    ```
    cf create-service service_name service_plan service_instance
    ```

3. 使用下列指令將服務實例連結至應用程式，其中 appname 是應用程式的名稱，而 service_instance 是服務實例的名稱。

    ```
    cf bind-service appname service_instance
    ```

您可以將服務實例僅連結至位於相同空間或組織中的應用程式實例。然而，使用其他空間或組織中的服務實例的方式，與使用外部應用程式的方式一樣。請使用認證直接配置應用程式實例，而非建立連結。如需外部應用程式如何使用 {{site.data.keyword.Bluemix_notm}} 服務的相關資訊，請參閱[讓外部應用程式能使用 {{site.data.keyword.Bluemix_notm}} 服務](#accser_external){: new_window}。


## 配置應用程式以與服務互動 
{: #config}

將服務實例連結至應用程式之後，您必須配置應用程式以與服務互動。

每一個服務可能需要不同的機制來和應用程式通訊。
這些機制記載於服務定義的一部分，以在您開發應用程式時作為參考資訊。
為了一致性，必須要有機制，您的應用程式才能與服務互動。


* 若要與資料庫服務互動，請使用 {{site.data.keyword.Bluemix_notm}} 所提供的資訊（例如，使用者 ID、密碼，以及應用程式的存取 URI）。
* 若要與行動式後端服務互動，請使用 {{site.data.keyword.Bluemix_notm}} 所提供的資訊（例如，應用程式身分（應用程式 ID）、用戶端特有的安全資訊，以及應用程式的存取 URI）。行動式服務通常會彼此合作，以便環境定義資訊（例如，應用程式開發人員的名稱，以及使用應用程式的使用者）能在服務集之間共用。
* 若要與 Web 應用程式或是行動式應用程式的伺服器端雲端程式碼互動，請使用 {{site.data.keyword.Bluemix_notm}} 所提供的資訊（例如，應用程式的 *VCAP_SERVICES* 環境變數中的執行時期認證）。*VCAP_SERVICES*
環境變數的值是 JSON 物件的序列化。
變數包含與應用程式所連結之服務互動時所需要的執行時期資料。
不同服務會有不同的資料格式。
您可能需要閱讀服務文件，以瞭解預期的內容，以及如何解譯每一份資訊。


如果您連結至應用程式的服務當機，應用程式可能會停止執行或發生錯誤。{{site.data.keyword.Bluemix_notm}} 不會自動重新啟動應用程式，以從這些問題中回復。請考慮將應用程式編碼成可識別運作中斷、異常狀況和連線失敗並從其中回復。如需相關資訊，請參閱[應用程式不會自動重新啟動](../troubleshoot/index.html#ts_topmenubar)疑難排解主題。


## 讓外部應用程式能使用 {{site.data.keyword.Bluemix_notm}} 服務
{: #accser_external}

您可能有在 {{site.data.keyword.Bluemix_notm}} 之外建立和執行的應用程式，或是您可能使用協力廠商工具。如果 {{site.data.keyword.Bluemix_notm}} 服務提供可從網際網路存取的端點，您可以使用那些服務來搭配本端應用程式或協力廠商工具。

若要讓外部應用程式或協力廠商工具能使用 {{site.data.keyword.Bluemix_notm}} 服務，請完成下列步驟：

1. 要求服務的實例。
    1. 在 {{site.data.keyword.Bluemix_notm}} 使用者介面的「儀表板」上，按一下**使用服務或 API**。即會顯示「型錄」。
    2. 從「型錄」中，按一下服務磚以選取您想要的服務。即會開啟「服務詳細資料」頁面。
    3. 在「新增服務」視窗中，將**應用程式：**清單選項保持為**維持不連結**。這個選項表示服務將不會連接至 {{site.data.keyword.Bluemix_notm}} 應用程式。
    4. 視需要進行任何其他選擇。然後按一下**建立**。即會建立服務實例，且會顯示服務「儀表板」。
2. 在服務「儀表板」的左導覽窗格中，您可以選取**服務認證**，以使用 JSON 格式檢視或新增認證。使用顯示為認證的 API 金鑰來連接至服務實例。

在 {{site.data.keyword.Bluemix_notm}} 外執行的應用程式現在可以存取 {{site.data.keyword.Bluemix_notm}} 服務。

**附註：**如果您要刪除服務實例或檢查計費資訊，您必須回到使用者介面中的「儀表板」才能管理服務實例。

## 建立使用者提供的服務實例
{: #user_provide_services}

您的資源可能是在 {{site.data.keyword.Bluemix_notm}} 外部進行管理。如果您有認證可從網際網路存取那些外部資源，則可以建立 {{site.data.keyword.Bluemix_notm}} 使用者提供的服務實例來代表外部資源並與之通訊。

若要建立使用者提供的服務實例，並將它連結至應用程式，請完成下列步驟：

1. 使用 **cf create-user-provided-service** 或 **cf cups** 指令，以建立使用者提供的服務實例：
    * 若要建立一般使用者提供的服務實例，請使用 **-p** 選項，並使用逗點區隔參數名稱。cf 指令行介面接著會提示您依次輸入每一個參數。例如：```
        cf cups testups1 -p "host, port, dbname, username, password"
        host> pubsub01.example.com
        port> 1234
        dbname> sampledb01
        username> pubsubuser
        password> p@$$w0rd
        Creating user provided service testups1 in org my-org / space dev as user@sample.com...
        OK
        ```

    * 若要建立將資訊排除至協力廠商日誌管理軟體的服務實例，請使用 **-l** 選項，然後指定協力廠商日誌管理軟體所提供的目的地。例如：

        ```
        cf cups testups2 -l syslog://example.com
        Creating user provided service testups2 in org my-org / space dev as user@sample.com...
        OK
        ```

    如果您要更新使用者提供服務實例的一個以上參數，請使用 **cf update-user-provided-service** 或 **cf uups** 指令。

    * 若要更新一般使用者提供的服務實例，請使用 **-p** 選項，並在 json 物件中指定參數索引鍵和值。
例如：

        ```
        cf uups testups1 -p "{\"username\":\"pubsubuser2\",\"password\":\"p@$$w0rd2\"}"
        Updating user provided service testups1 in org my-org / space dev as user@sample.com...
        OK
        ```

    * 若要建立將資訊排除至協力廠商日誌管理軟體的服務實例，請使用 -l 選項。例如：

        ```
        cf uups testups2 -l syslog://example2.com
        Updating user provided service testups2 in org my-org / space dev as user@sample.com...
        OK
        ```

2. 使用 cf bind-service 指令，將服務實例連結至應用程式。例如：

	```
	cf bind-service myapp testups1
	Binding service testups1 to app myapp in org my-org / space dev as user@sample.com...
	OK
	```

您現在可以將應用程式配置成使用外部資源。如需如何配置應用程式與服務互動的相關資訊，請參閱[配置應用程式以與服務互動](#config){: new_window}。

## 在另一個地區使用服務
{: #cross_region_service}

如果您的服務實例建立並連結到某個地區中的應用程式，則可以使用下列其中一種方法，在另一個地區中使用這個服務實例：

  * 使用服務認證直接配置應用程式實例。如需詳細資料，請參閱[讓外部應用程式能使用 {{site.data.keyword.Bluemix_notm}} 服務](#accser_external){: new_window}。
  * 建立使用者提供的服務作為橋接器。
    
	假設您從想要使用服務實例的地區中開始。若要使用存在於另一個地區的服務實例，請完成下列步驟：

      1. 切換至服務實例所在的地區。在 {{site.data.keyword.Bluemix_notm}} 頂端功能表列，展開**地區**或按一下**地區**圖示，然後選取服務實例存在的地區。

      2. 在服務存在的地區中，從服務實例的 VCAP_SERVICES 環境變數擷取認證及連線參數。請完成下列步驟：


	       1. 在 {{site.data.keyword.Bluemix_notm}}「儀表板」中，按一下您的應用程式磚。即會顯示「概觀」頁面。
	       2. 在左導覽窗格中，按一下**環境變數**。右窗格會顯示 *VCAP_SERVICES* 環境變數詳細資料。請記錄服務實例的 JSON 內容。

      3. 切換至您從想要使用服務實例的地區。在 {{site.data.keyword.Bluemix_notm}} 頂端功能表列，展開**地區**或按一下**地區**圖示，然後選取您想要使用服務實例的地區。

      4. 使用您從 *VCAP_SERVICES* 環境變數記錄的認證及連線參數，建立使用者提供的服務實例。如需如何建立使用者提供的服務實例的相關資訊，請參閱[建立使用者提供的服務實例](#user_provide_services){: new_window}。

      5. 使用下列指令，以將使用者提供的服務實例連結至應用程式：

	     ```
	     cf bind-service myapp user-provided_service_instance
	```






## 在另一個服務中使用服務
{: #s2s_binding}

服務存取授權提供一種方法，讓某個服務直接存取另一個服務。您可以在 {{site.data.keyword.Bluemix_notm}}「儀表板」上授權及配置服務實例對其他服務實例的存取權。

若要使用另一個服務中的服務實例，請完成下列步驟：

1. 在 {{site.data.keyword.Bluemix_notm}}「儀表板」上，按一下您要存取的服務磚。即會顯示服務的儀表板。
2. 在左導覽窗格中，使用服務實例的主控台，按一下*管理* 以授權來自其他服務實例的連結。
3. 如果您要拒絕其他服務對服務實例的存取權，請按一下左導覽窗格中的*服務存取授權*，然後使用*撤銷* 以移除服務連結。 

# 相關鏈結
{: #rellinks}

## 一般
{: #general}

* [使用 {{site.data.keyword.Bluemix_notm}} 使用者介面連結服務](../cfapps/ee.html#ee_bindui)
* [擷取 VCAP_SERVICES](../cli/vcapsvc.html#retrieving)


