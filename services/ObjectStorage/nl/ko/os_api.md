---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

## Swift REST API를 사용하여 {{site.data.keyword.objectstorageshort}}에 액세스 {: #using-swift-restapi}
*마지막 업데이트 날짜: 2016년 10월 19일*
{: .last-updated}

명령행 클라이언트 인터페이스(예: cURL)에서 Swift REST API를 사용하거나 애플리케이션에서 API를 호출할 수 있습니다.
{: shortdesc}

### {{site.data.keyword.objectstorageshort}} URL 생성 {: #access-points}

{{site.data.keyword.objectstorageshort}} API와 상호작용하려면 다음과 같이 {{site.data.keyword.objectstorageshort}} URL을 생성하십시오.
  ```
https://<access point>/<API version>/AUTH_<project ID>/<container namespace>/<object namespace>
  ```
  {: pre}

<table>
  <tr>
    <th> URL 조각 </th>
    <th> 정의 </th>
  </tr>
  <tr>
    <td> API 버전 </td>
    <td> 버전 1: v1 </td>
  </tr>
  <tr>
    <td> 계정 정보 </td>
    <td> 프로젝트 ID이며 접두부가 결합되어 있습니다. UI에서 찾을 수 있습니다. </td>
  </tr>
  <tr>
    <td> 컨테이너 네임스페이스 </td>
    <td> 컨테이너의 이름입니다. UI에서 찾을 수 있습니다. </td>
  </tr>
  <tr>
    <td> 오브젝트 네임스페이스 </td>
    <td> 파일 또는 오브젝트의 이름입니다. UI에서 찾을 수 있습니다. </td>
  </tr>
  <tr>
    <td> 액세스 지점</td>
    <td> 런던: https://lon.objectstorage.open.softlayer.com/
    <br> 댈러스: https://dal.objectstorage.open.softlayer.com/ </br> </td>
  </tr>
</table>

*표 1. 설명되는 {{site.data.keyword.objectstorageshort}} URL 조각*

예:

![예제 이미지에 표시된 {{site.data.keyword.objectstorageshort}} URL 조각](images/Swift_URL.png)


### {{site.data.keyword.objectstorageshort}} API {: #openstack-reference}

{{site.data.keyword.objectstorageshort}} REST API 옵션과 예제의 전체 목록은 [OpenStack Swift API 전체 참조](http://developer.openstack.org/api-ref-objectstorage-v1.html)를 참조하십시오. 
