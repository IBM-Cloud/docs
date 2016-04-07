---

copyright:
  years: 2015,2016

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 連接及檢視裝置
{: #iotrtinsights_task}
*前次更新：2016 年 2 月 11 日*

{{site.data.keyword.iotrtinsights_short}} 使用 {{site.data.keyword.iot_short}} 進行裝置存取及資料擷取。您連接至 {{site.data.keyword.iot_short}} 的裝置會自動連接至 {{site.data.keyword.iotrtinsights_short}}。
{: shortdesc}

如果您是連接新類型的裝置，則還必須配置訊息綱目來對映裝置資料點、設定單位，以及指名裝置類型。如果您的裝置屬於已配置的裝置類型，則其資料會自動顯示在儀表板中。

## 新增裝置
{: #iotrtinsights_subtask}

若要新增裝置，請執行下列動作：  
新增裝置的程序包含兩個步驟。首先，您將裝置新增至 {{site.data.keyword.iot_short}}，然後配置 {{site.data.keyword.iotrtinsights_short}} 取用及顯示裝置資料的方式。
1. 將裝置新增至 {{site.data.keyword.iot_short}}。
> **提示：**如果您已部署 Internet of Things 電話應用程式，則 iotphone 裝置已新增至 *iot-phone-iotf-service* {{site.data.keyword.iot_short}}，因此可以跳過此步驟。  

  若要將新裝置新增至 {{site.data.keyword.iot_short}}，請參閱 [{{site.data.keyword.iot_full}} 文件](https://www.ng.bluemix.net/docs/services/IoT/index.html)及 [{{site.data.keyword.iot_short}} 裝置連線秘訣](https://developer.ibm.com/recipes/?post_type=tutorials&s=IoTF)。
2. 在 {{site.data.keyword.iotrtinsights_short}} 中配置裝置。  
  1. 以管理者使用者身分登入 {{site.data.keyword.iotrtinsights_short}} 主控台。
  9. 移至**裝置 > 瀏覽裝置**，並驗證已列出您新增的裝置。
  > **提示：**從資料來源重新整理裝置清單的頻率是一分鐘一次。按一下**重新整理**，立即更新裝置清單。
  3. 移至**裝置 > 管理綱目**，然後按一下**新增訊息綱目**。  
  4. 輸入訊息綱目的名稱，例如：`New message schema`。
  5. 按一下**鏈結新的資料來源**，然後選取對應至 {{site.data.keyword.iot_short}} 實例及裝置的資料來源及裝置類型。選擇性地輸入事件名稱，僅收集該事件的資料，或保留 `+` 萬用字元以收集所有事件。如需如何識別裝置的事件類型的相關資訊，請參閱[這裡](#identify-datapoints "識別資料點")。  
  >**重要事項：**每一個訊息綱目都必須要有唯一的資料來源、裝置類型與事件名稱組合。若要建立特定資料來源與裝置類型組合的多個綱目，請為每一個訊息綱目指定唯一的事件名稱，而不是使用預設 `+` 萬用字元。   
  6. 在裝置儀表板中，新增您要併入的一個以上資料點。
    您可以從已連接的裝置中選取資料點，或手動新增資料點。可用的資料點定義於裝置所傳送訊息的有效負載中。如需 {{site.data.keyword.iot_short}} 有效負載格式的相關資訊，請參閱 {{site.data.keyword.iot_short}} 文件中的[訊息有效負載](https://docs.internetofthings.ibmcloud.com/messaging/payload.html "訊息有效負載")主題。   
    > **提示：**您可以手動建立虛擬資料點，以修改或合併類型為整數或浮點的現有資料點。例如，如果裝置資料點 temp 傳回華氏溫度值，但您要改成使用攝氏，則可以使用下列函數 *temp_c=(temp-32)/1.8* 來建立虛擬資料點 *temp_c*。然後，您可以在規則條件中使用虛擬的 *temp_c* 資料點，而不使用即時的 *temp* 資料點。在儀表板中，虛擬資料點是透過虛線底線進行識別。    

  <dl>
  <dt>從已連接的裝置中進行選取</dt>
  <dd>
  <ol>
    <li>按一下**從已連接的裝置中進行選取**。</li>  
    <li>在「新增資料點」對話框中，選取要新增的一個以上資料點，然後按一下**確定**。</li>   
    <li>即會新增選取的資料點，並且說明設為資料點名稱。按一下清單中的資料點來進行編輯，以及新增其他屬性（例如感應器類型、資料類型及小數位數）。</li>
  </ol>
  </dd>
  <dt>手動新增</dt>
  <p><b>提示：</b>若要建立[巢狀資料點結構](schemas.html)，請先新增資料類型為 Parent 的資料點。在資料點表格中，您接著可以按一下 ![「新增子項」圖示](images/add_child.png "新增子項")，以新增一個以上的子項資料點。</p>
  <dd>
  <ol>
    <li>按一下**手動新增**。</li>
    <li>選取**即時資料點**或**虛擬資料點**</br></li>
    <li>定義下列資料點資訊：
    <ul>  
     <li> 資料點 - 您[在 {{site.data.keyword.iot_short}} 儀表板](#identify-datapoints "識別資料點")中找到的資料點 ID。例如：  
   `id`、`ts`、`lat`  </li>
     <li>說明 - 資料點的簡要說明。在儀表板中顯示資料點時，會使用此說明。</li>
     <li>虛擬資料點函數 - 新增一個以上的元件，以定義有效的函數。您可以使用資料點、數值及算術運算子（例如 +、-、\*、/、( 及 )）來建置您的函數。</li>
     <li>資料類型 - 資料點的資料類型：  
   `String`、`Integer`、`Float` 或 `Parent`。</li>
     <li>感應器類型 - 選擇性地選取如何解譯儀表板中的資料點。根據類型與感應器類型組合，您的儀表板小組件可能會有其他視覺化選項。如需感應器類型及視覺化選項的相關資訊，請參閱[儀表板小組件](dashboards.html#dashboard-widget "儀表板小組件")。</li>
     <li>資料點圖示 - 選擇性地選取圖示來代表儀表板小組件中的資料點。</li>
     <li>最小值/最大值 - 選用項目，僅限整數及浮點：如果輸入最大值及最小值，則裝置資料可以顯示為儀表板中的量規。</li>
     <li>資料單位 - 選用項目：資料點的資料單位。例如：  
     `C`、`Mph`  </li>
     <li> 小數位數 - 選用項目，僅限浮點：裝置資料中所包括的小數位數。</li>
    </ul>
    </li>
  </ol>
  </dd>
  </dl>
   8. 按一下**確定**，以建立訊息綱目。
   9. 移至**裝置 > 瀏覽裝置**，然後按一下新增的裝置來驗證已顯示即時裝置資料，以及已正確地對映資料點。

## 在 {{site.data.keyword.iot_short}} 儀表板中識別資料點及事件。
{: #identify-datapoints}
   在 {{site.data.keyword.iot_short}} 儀表板中，可以找到裝置的資料點及事件類型。
   >**提示：**如果您使用 Internet of Things 電話應用程式作為 IoT 裝置，則可以使用 sensorData 事件及下列資料點來配置訊息綱目：
   >- d.id - 裝置 ID
   >- d.ts - 時間戳記
   >- d.lat - 緯度
   >- d.lng - 經度
   >- d.ax - X 加速
   >- d.ay - Y 加速
   >- d.az - Z 加速
   >- d.oa - Alpha 移動
   >- d.ob - Beta 移動
   >- d.og - Gamma 移動
   >其中 d.*datapoint* 指出資料點巢狀於訊息有效負載的母項類型 d 資料點下方。

   1. 從 Bluemix 儀表板中，按一下 Internet of Things 磚。  
   >**附註：**如果您使用的是 Internet of Things 電話應用程式，請按一下 *iot-phone-iotf-service* 磚。  
   2. 按一下**啟動儀表板**，以開啟 {{site.data.keyword.iot_short}} 儀表板。
   3. 移至**裝置**頁面。
   4. 按一下裝置，以開啟裝置詳細資料頁面。
     向下捲動至**感應器資訊**區段，以查看裝置的可用事件及資料點清單。當您在 {{site.data.keyword.iotrtinsights_short}} 中配置裝置時，需要此資訊。
