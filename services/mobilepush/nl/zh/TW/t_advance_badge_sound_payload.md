---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

#啟用進階推送通知
前次更新：2017 年 2 月 28 日
{: .last-updated}

配置 iOS 徽章、音效、其他 JSON 有效負載、可採取動作的通知，以及保存通知。

## 配置音效、有效負載以及 iOS 徽章
{: #badge-sound-payload}

配置 iOS 徽章、音效及其他 JSON 有效負載。

1. 在 {{site.data.keyword.mobilepushshort}} 儀表板上，移至**通知**標籤。
2. 移至**選用欄位**區段，以配置 {{site.data.keyword.mobilepushshort}} 特性。 
	- **音效檔** - 輸入指向行動應用程式中音效檔的字串。在有效負載中，指定要使用之音效檔的字串名稱。
	- **iOS 徽章** - 對於 iOS 裝置，這是要顯示為應用程式圖示徽章的號碼。如果沒有此內容，則不會變更徽章。若要移除徽章，請將此內容的值設為 0。
	
### Android
{: #badge-sound-payload_android}

在 Android 應用程式的 `res/raw` 目錄中，新增您的音效檔。傳送通知時，在 {{site.data.keyword.mobilepushshort}} 的音效欄位中新增音效檔名稱。

```
"settings":{
     "gcm":{
     "sound":"tt.wav",
  }
 }  
```
    {: codeblock}	
	
### iOS
{: #badge-sound-payload_ios}

```
"settings": {
     "apns" : {
      "badge": 10,
      "sound": "tt.wav",
  }
}
``` 
	{: codeblock}
		
**其他有效負載** - 此有效負載可以是任意鍵值組，而且必須是您要與 {{site.data.keyword.mobilepushshort}} 一起傳送的 JSON 物件。



```
{"key":"value", "key2":"value2"}
```
	{: codeblock}

## 保存 Android 通知 
{: #hold-notifications-android}

在應用程式進入背景時，您可能會想要 {{site.data.keyword.mobilepushshort}} 保留傳送給應用程式的通知。若要保留通知，請在處理 {{site.data.keyword.mobilepushshort}} 之活動的 onPause() 方法中呼叫 hold() 方法。

```
@Override
protected void onPause() {
    super.onPause();
    if (push != null) {
        push.hold();
    }
} 
```
	{: codeblock}

    
