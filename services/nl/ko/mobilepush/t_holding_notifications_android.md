---

copyright:
 years: 2015, 2016

---

# Android의 보류 알림
{: #hold-notifications-android}

애플리케이션이 백그라운드로 전환될 경우 애플리케이션에 전송되는 푸시 알림을 보류하고자 할 수 있습니다. 알림을 보류하려면 푸시 알림을 처리하는 활동의 onPause() 메소드에서 hold() 메소드를 호출하십시오. 

```
@Override
protected void onPause() {
    super.onPause();


    if (push != null) {
push.hold();
    }
} 
```
