---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 리치 미디어 알림 사용
{: #interactive-notifications}
마지막 업데이트 날짜: 2017년 1월 11일
{: .last-updated}


iOS 10 이상에서 리치 미디어 {{site.data.keyword.mobilepushshort}}를 사용할 수 있습니다. 오디오, 동영상, GIF 및 이미지가 포함된 푸시 알림을 보낼 수 있습니다. 

iOS 10에서 리치 푸시를 받을 애플리케이션을 설정하려면 다음 단계를 완료하십시오.  

1. Xcode에서 **파일** > **새로 작성** > **대상** > **알림 서비스 확장기능**을 선택하십시오.
2. `UNNotificationServiceExtension`의 `didReceive()` 메소드에서 코드를 추가하십시오.
```
BMSPushRichPushNotificationOptions.didReceive(request, withContentHandler: contentHandler)
```
	
푸시 대시보드에서 리치 미디어 {{site.data.keyword.mobilepushshort}}를 보내려면 메시지, 제목, 부제목 및 attachmentURL 필드를 지정하십시오.
