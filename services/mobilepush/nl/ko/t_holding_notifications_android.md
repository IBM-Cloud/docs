---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Android의 보류 알림
{: #hold-notifications-android}
마지막 업데이트 날짜: 2017년 1월 11일
{: .last-updated}

애플리케이션이 백그라운드로 전환되는 경우 {{site.data.keyword.mobilepushshort}} 서비스에서 애플리케이션에 전송되는 알림을 보유할 수 있습니다. 알림을 보류하려면 {{site.data.keyword.mobilepushshort}}를 처리하는 활동의 onPause() 메소드에서 hold() 메소드를 호출하십시오. 

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
