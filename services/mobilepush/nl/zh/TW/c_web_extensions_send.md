---

copyright:
years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 將基本通知傳送至 Chrome Apps and Extensions 
{: #web_extensions_notifications}
前次更新：2017 年 1 月 11 日
{: .last-updated}

開發應用程式之後，您可以傳送推送通知。 

1. 選取**傳送通知**，然後選擇 **Web 通知**作為**傳送至**選項來編寫訊息。 
2. 在**訊息**欄位中，鍵入需要遞送的訊息。
3. 您可以選擇提供選用設定：
  - **通知標題**：這是將顯示為訊息警示標題的文字。
  - **通知圖示 URL**：如果需要使用應用程式通知圖示來遞送您的訊息，請在此欄位中提供該圖示的鏈結。
  - **收合金鑰**：收合金鑰會附加至通知。如果多個具有相同收合金鑰的通知在裝置離線時循序到達，則會予以收合。當裝置上線時，會接收到來自 FCM/GCM 伺服器的通知，並且只會顯示含有相同收合金鑰的最新通知。如果未設定收合金鑰，則會儲存新舊訊息，以供未來遞送。
  - **存活時間**：此值是以秒為單位來設定。如果未指定此參數，則 FCM/GCM 伺服器會儲存訊息四週，並嘗試遞送。有效性會在四週後到期。可能值範圍是從 0 到 2,419,200 秒。
  - **閒置時延遲**：將此值設為 `true` 時，指示 FCM/GCM 伺服器不要在裝置閒置時遞送通知。將此值設為 `false`，則可確保遞送通知，即使裝置閒置也是一樣。
  - **其他有效負載**：指定通知的自訂有效負載值。

下列影像顯示儀表板中的 Chrome Apps and Extensions 通知選項。

  ![通知畫面](images/push_chrome_extns.jpg)
  
## 後續步驟
  {: #next_steps_tags}

順利設定基本通知之後，即可選擇配置標籤型通知及進階選項。

將這些 {{site.data.keyword.mobilepushshort}} Service 特性新增至您的應用程式。
若要使用標籤型通知，請參閱[標籤型通知](c_tag_basednotifications.html)。
若要使用進階通知選項，請參閱[進階通知](t_advance_badge_sound_payload.html)。
