---

copyright:
years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 將基本通知傳送至 Web 瀏覽器
{: #web_notifications}
前次更新：2017 年 1 月 11 日
{: .last-updated}

開發應用程式之後，您可以傳送推送通知。 

1. 選取**傳送通知**，然後選擇 **Web 通知**作為**傳送至**選項來編寫訊息。 
2. 在**訊息**欄位中，鍵入需要遞送的訊息。
3. 您可以選擇提供選用設定：
  - **通知標題**：這是將顯示為訊息警示標題的文字。
  - **通知圖示 URL**：如果需要使用應用程式通知圖示來遞送您的訊息，請在此欄位中提供該圖示的鏈結。
  - **存活時間**：通知伺服器訊息的有效性。
4. 針對傳送給 Safari 瀏覽器的 Web 通知，還需要一些其他資訊：
  - **動作**：這是動作按鈕的標籤。
  - **URL 引數**：需要與此通知一起使用的 URL 引數。請確定這是以 JSON 陣列的格式提供。 
 
下列影像顯示儀表板中的 Web 通知選項。

  ![通知畫面](images/DashboardWebpush.jpg)


## 後續步驟
  {: #next_steps_tags}

順利設定基本通知之後，即可選擇配置標籤型通知及進階選項。

將這些 {{site.data.keyword.mobilepushshort}} Service 特性新增至您的應用程式。
若要使用標籤型通知，請參閱[標籤型通知](c_tag_basednotifications.html)。
若要使用進階通知選項，請參閱[進階通知](t_advance_badge_sound_payload.html)。



