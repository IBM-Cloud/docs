---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 액세스 유형 

{{site.data.keyword.objectstorageshort}} 사용자는 관리자 또는 비관리자일 수 있습니다. 액세스 제어 목록은 컨테이너 레벨에서 관리자가 설정할 수 있습니다.
{: shortdesc}

<table>
<caption> 표 1. 정의된 사용자 역할</caption>
  <tr>
    <th> 관리 사용자(admin) </th>
    <th> 비관리 사용자(member) </th>
  </tr>
  <tr>
    <td> 액세스 제어 관리 </td>
    <td> 기본적으로 서비스 또는 해당 컨테이너에 대한 액세스가 없음 </td>
  </tr>
  <tr>
    <td> 컨테이너를 작성하고 삭제할 수 있음 </td>
    <td> 컨테이너 읽기/쓰기 ACL을 기반으로 하여 조치를 수행할 수 있음 </td>
  </tr>
  <tr>
    <td> 컨테이너에 대해 읽고 쓸 수 있음 </td>
    <td> admin에 의해 결정된 대로 조치를 수행할 수 있음 </td>
  </tr>
</table>


{{site.data.keyword.Bluemix_notm}} 사용자 인터페이스, Cloud Foundry API 또는 Cloud Foundry CLI를 통해 {{site.data.keyword.objectstorageshort}} 사용자를 관리할 수 있습니다.
