---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 임시 URL 작성 {: #create-temporary-url}

*마지막 업데이트 날짜: 2016년 10월 19일*
{: .last-updated}

임시 URL은 추가 인증할 필요 없이 오브젝트를 다운로드하기 위해 지정된 기간 동안 사용할 수 있는 추측하기 어려운 긴 URL입니다.
{: shortdesc}


1. 다음 명령을 사용해서 계정 정보를 인쇄하여 인증 정보를 식별하십시오. 

    ```
swift stat
```
    {: pre}
    
    **참고**: 계정 필드를 찾아 *계정* 뒤에 있는 전체 문자열(`AUTH_` 포함)을 기록해 두십시오.
2. 비밀 키를 설정하십시오.사용자가 선택하는 무엇이든 이 키가 될 수 있지만 우수 사례는 추측하기 어려운 긴 임의의 문자열을 선택하는 것입니다. 키를 설정하려면 다음 명령을 실행하십시오. 

    ```
swift post -m "Temp-URL-Key:<key>"
```
    {: pre}
    
3. 다음 명령을 실행하여 `Temp-URL-Key`가 설정되었는지 확인하십시오. 

    ```
swift stat
```
    {: pre}
    
4. 다음 명령을 실행하여 임시 URL을 작성하십시오. 

    ```
swift tempurl GET <seconds> <path> <key>
```
    {: pre}
    
    다음 표에서는 Swift `tempurl` 명령에서 사용하는 위치 인수에 대해 설명합니다.
    <table>
      <tr>
        <th> 인수 </th>
        <th> 설명 </th>
      </tr>
      <tr>
        <td> [method] </td>
        <td> GET을 사용하여 다운로드하고 PUT을 사용하여 업로드합니다. </td>
      </tr>
      <tr>
        <td> [seconds] </td>
        <td> 임시 URL을 사용할 수 있는 시간(초)입니다. </td>
      </tr>
      <tr>
        <td> [path] </td>
        <td> `/v1/<auth_account>/<container_name>/<object_name>`으로 표현되는 오브젝트의 전체 경로입니다. 자세한 정보는 [{{site.data.keyword.objectstorageshort}} URL 문서](/os_api.html#access-points)를 참조하십시오. </td>
      </tr>
      <tr>
        <td> [key] </td>
        <td> 2단계에서 설정한 비밀 키입니다. </td>
      </tr>
    </table>
    *표 2: tempurl 위치 인수*
5. (*선택사항*): 전체 URL을 가져오려면 리턴된 URL을 클러스터 이름에 추가하십시오. 그런 다음 전체 URL을 사용하여 호환 가능한 HTTP 클라이언트(예: cURL, wget 또는 Firefox)를 통해 오브젝트를 다운로드할 수 있습니다. 
