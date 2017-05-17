---

copyright:
  years: 2016, 2017
lastupdated: "2017-05-02"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# 啟用 SMS 及語音傳訊
{: #supportedcloud}

{{site.data.keyword.iotinsurance_full}} 支援與 Twilio 的整合，以啟用 SMS 及語音傳訊。Twilio 是一種協力廠商應用程式，可安裝在 {{site.data.keyword.Bluemix_notm}} 儀表板中。
{: shortdesc}

## 必要條件
若要啟用語音傳訊，您必須有授權 Twilio 帳戶及 Twilio 呼叫方電話號碼。如果您使用 Twilio 免費帳戶，則也必須授權電話號碼來接收呼叫或訊息。如需相關資訊，請參閱 [Twilio 文件 ![外部鏈結圖示](../../icons/launch-glyph.svg)](https://support.twilio.com/hc/en-us/articles/223136107-How-does-Twilio-s-Free-Trial-work-){:new_window}。

## 建立及配置 Twilio 實例
1. 在已安裝 {{site.data.keyword.iotinsurance_short}} 的相同 {{site.data.keyword.Bluemix_notm}} 組織及空間中，建立 Twilio 實例。
    1. 登入 [{{site.data.keyword.Bluemix_notm}}](https://console.ng.bluemix.net)。
    2. 選取**型錄**標籤。
    3. 找到服務型錄的「行動」區段，然後按一下 **Twilio**。

    **提示：**按一下[這裡 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.ng.bluemix.net/catalog/services/twilio/){: new_window}，以直接移至 Twilio 頁面。
    {: tip}

    4. 在 Twilio 頁面上，提供認證，並連結應用程式，如下所示：

      1. 輸入 `Twilio-00` 作為服務名稱。**重要事項：**您必須使用 `Twilio-00`，才能順利連接至 {{site.data.keyword.iotinsurance_short}}。

      2. 輸入 Twilio 認證。

      3. 在**連接至**功能表中，選取 iot4i-action-engine 應用程式，以將 Twilio 實例連結至 {{site.data.keyword.iotinsurance_short}}。

      4. 按一下**建立**。  

    即會在環境中安裝 Twilio 應用程式。一則訊息會提示您重新編譯打包或重新啟動 iot4i-action-engine 應用程式來啟用連結。您可以立即重新啟動，或等待重新啟動，直到您在下一步中新增環境變數。

2. 針對 iot4i-action-egine 元件，建立稱為 TWILIO_FROM_NUMBER 的環境變數。
    1. 從 Bluemix 儀表板中，開啟 iot4i-action-engine 應用程式。
    2. 選取**運行環境**，然後按一下**環境變數**。
    3. 在**使用者定義**區段中，按一下**新增**。
    4. 在「名稱」直欄中輸入 `TWILIO_FROM_NUMBER`，然後在「值」直欄中輸入 Twilio 語音及可啟用 SMS 功能的數字。
    5. 按一下**儲存**。

3. 按一下「路徑」按鈕旁的「重新啟動」圖示，以重新啟動 Iot4i-action-engine 應用程式。

## 將 SMS 及語音動作新增至防護

若要將 SMS 及語音功能新增至防護，您必須將下列動作新增至防護定義：
  - `send-sms`
  - `phone-call`

如需包含動作清單之防護的範例，請參閱[建立範例防護範例 ![外部鏈結圖示](../../icons/launch-glyph.svg)](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/blob/master/bl/shield.js){:new_window}。在此範例中，SMS 及語音動作可以新增至包含 `email` 及 `pushios` 動作的動作清單。

如需建立防護的相關資訊，請參閱[使用防護工具箱](iotinsurance_shield_toolkit.html)。
