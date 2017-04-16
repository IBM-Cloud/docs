---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 태그 기반 알림 
{: #push-ios-main-tags}
마지막 업데이트 날짜: 2017년 1월 16일
{: .last-updated}

태그 기반 알림 메시지는 특정 태그를 구독하는 모든 디바이스가 대상입니다. 태그를 정의한 다음 태그를 사용하여 메시지를 전송 및 수신할 수 있습니다.  

먼저 애플리케이션에 대한 태그를 작성하고, 태그 구독을 설정한 다음, 태그 기반 알림을 시작해야 합니다. [REST API ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://mobile.{DomainName}/imfpush/){: new_window}을 사용하여 태그 기반 알림을 전송하려면, 메시지 리소스에 게시할 때 "tagNames"가 제공되는지 확인하십시오.  
