---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 고급 {{site.data.keyword.mobilepushshort}} 사용
마지막 업데이트 날짜: 2017년 1월 23일
{: .last-updated}

iOS 배지, 사운드, 추가 JSON 페이로드, 조치 가능 알림, 보류 알림을 구성합니다. 

## 사운드, 페이로드 및 iOS 배지 구성
{: #badge-sound-payload}

iOS 배지, 사운드 및 추가적인 JSON 페이로드를 구성합니다. 

1. {{site.data.keyword.mobilepushshort}} 대시보드에서 **알림** 탭으로 이동하십시오. 
2. **선택적 필드** 섹션으로 이동하여 다음과 같이 {{site.data.keyword.mobilepushshort}} 기능을 구성하십시오.  
	- **사운드 파일** - 모바일 앱의 사운드 파일을 가리키는 문자열을 입력하십시오. 페이로드에서 사용할 사운드 파일의 문자열 이름을 지정하십시오. 
	- **iOS 배지** - iOS 디바이스의 경우 앱 아이콘의 배지로 표시할 숫자입니다. 이 특성을 비워두면 배지가 변경되지 않습니다. 배지를 제거하려면 이 특성의 값을 0으로 설정하십시오. 
	
### Android

Android 애플리케이션의 `res/raw` 디렉토리에 사운드 파일을 추가하십시오. 알림을 전송하는 동안 {{site.data.keyword.mobilepushshort}}의 사운드 필드에 사운드 파일 이름을 추가하십시오. 

```
"settings":{
     "gcm":{
     "sound":"tt.wav",
	 }
 }  
```
    {: codeblock}	
	
### iOS

```
"settings": {
     "apns" : {
      "badge": 10,
	     "sound": "tt.wav",
	 }
	}
``` 
	{: codeblock}
		
**추가 페이로드** - 이 페이로드는 키-값 쌍이며 {{site.data.keyword.mobilepushshort}}를 사용하여 전송하려는 JSON 오브젝트여야 합니다.

```
{"key":"value", "key2":"value2"}
```
	{: codeblock}

## Android 알림 보류 
{: #hold-notifications-android}

애플리케이션이 백그라운드로 전환되는 경우 {{site.data.keyword.mobilepushshort}}에서 애플리케이션에 전송되는 알림을 보류할 수 있습니다. 알림을 보류하려면 {{site.data.keyword.mobilepushshort}}를 처리하는 활동의 onPause() 메소드에서 hold() 메소드를 호출하십시오. 

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

    
