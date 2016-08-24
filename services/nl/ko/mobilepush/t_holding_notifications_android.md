---

copyright:
 years: 2015, 2016

---

# Android의 보류 알림
{: #hold-notifications-android}
*마지막 업데이트 날짜: 2016년 6월 14일*
{: .last-updated}

애플리케이션이 백그라운드로 전환되는 경우 애플리케이션에 전송된 알림을 푸시 알림 서비스에서 보유하도록 원할 수 있습니다. 알림을 보류하려면 푸시 알림을 처리하는 활동의 onPause() 메소드에서 hold() 메소드를 호출하십시오. 

```
@Override
protected void onPause() {
    super.onPause();

    if (push != null) {
        push.hold();
    }
} 
```
