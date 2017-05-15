---

copyright:
  years: 2015, 2017
lastupdated: "2016-10-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 베타 버전에서 리소스 데이터 마이그레이션
{: #globalizationpipeline_betaresourcedatamigration}

{{site.data.keyword.GlobalizationPipeline_full}}의 베타 버전은 GA 버전의 릴리스 이후 일정 기간이 지나면 종료됩니다. 베타 인스턴스의 사용자 데이터는 GA 서비스 인스턴스로 이동하지 않습니다. GA 이후 데이터를 보관하려면 리소스 데이터를 파일로 내보낸 후 새 인스턴스로 가져올 수 있습니다. 참고로, 서비스 대시보드를 통해 이 오퍼레이션을 수행할 수 없습니다. 또한 리소스 데이터를 리소스 파일 형식 중 하나로 내보내도 리소스 항목과 연관된 다른 메타데이터가 유지되지 않습니다.

베타에서 GA로 데이터 마이그레이션을 지원하기 위해 {{site.data.keyword.GlobalizationPipeline_short}}의 Java 명령행 도구에 기능이 추가되었습니다. 도구의 소스가 다음에서 호스팅되며 해당 2진 릴리스가 github 저장소에서 사용 가능합니다. https://github.com/IBM-Bluemix/gp-java-tools 최신 개발 스냅샷이 게시됩니다. [다운로드하십시오.](https://w3-connections.ibm.com/communities/service/html/communityview?communityUuid=589d87cf-d0c7-4e06-ab95-4108547f90aa#fullpageWidgetId=Wa22bb771e29b_4aa9_a114_cfe53fda2cc8&file=5cdaf089-ec7c-4881-b5a0-7ab651491237)

도구가 ***리소스 항목 업로딩***에 대해 베타 릴리스 이후 향상된 REST API를 사용하므로, 대상 서비스 인스턴스가 GA 버전이어야 합니다. 
* 소스: 베타 또는 GA
* 대상: GA만

다국어 지원 서비스 인스턴스의 모든 번들 데이터를 다른 인스턴스에 복사하려면 아래의 명령을 사용하십시오.

```> java -jar gp-cli.jar copy-all-bundles -s <source-service-url> -i <source-instance-id> -u <source-user-id> -p <source-password> --dest-url <dest-service-url> --dest-instance-id <dest-instance-id> --dest-user-id <dest-user-id> --dest-password <dest-password>```


`source/target-service-url` 및 기타 매개변수 값이 소스/대상 서비스의 신임 정보에 있습니다. 예를 들어, 다음과 같습니다.

 

```
{
  "gp-beta": [
    {
      "name": "Globalization Pipeline-7x",
      "label": "gp-beta",
      "plan": "gp-beta-plan",
      "credentials": {
 

      "url": "https://gp-beta-rest.ng.bluemix.net/translate/rest",
        "userId": "bd0b84362c6934d222c3a0a40fc1443b",
        "password": "OGxp6jDqCLCL1ui8kQSPTt1mZDi4EQwu",
        "instanceId": "bd0b84362c6934d222c3a0a40fc1233e"
      }
    }
  ]
}
```
또한 모든 GP CLI가 개별 옵션 `(-s / -i / -u / -p)` 뿐만 아니라 json 형식에서 신임 정보를 지원하도록 업데이트됩니다. 아래와 같은 컨텐츠로 json 파일을 작성할 수 있습니다.

creds.json 
 
```
 {

        "url": "https://gp-rest.stage1.ng.bluemix.net/translate/rest",
        "userId": "36cad58b3a65dc9fe0183208305be137",
        "password": "43F9MRMu9Q8BWRXMLctunUsAe8LTdwq1",
        "instanceId": "b157e3fc63e62d76c50d9f689d7fc965"} 
```
그런 다음 `-j <json-file>`에 따라 파일을 지정할 수 있습니다. `copy/copy-all-bundles` 명령에서 다음을 바꿀 수 있습니다.

```-s https://gp-rest.stage1.ng.bluemix.net/translate/rest -i b157e3fc63e62d76c50d9f689d7fc965 -u 36cad58b3a65dc9fe0183208305be137 -p 43F9MRMu9Q8BWRXMLctunUsAe8LTdwq1```

다음으로 변경됩니다.

`-j creds.json `
 
또는 다음 명령을 통해 한 위치에서 다른 위치로 번들을 복사할 수 있습니다. 

```> java -jar gp-cli.jar copy -s <source-service-url> -i <source-instance-id> -u <source-user-id> -p <source-password> -b <source-bundle-id> --dest-url <dest-service-url> --dest-instance-id <dest-instance-id> --dest-user-id <dest-user-id> --dest-password <dest-password> -d <dest-bundle-id>```


**참고:** 두 개의 추가 매개변수: `-b <source-bundle-id>` 및 `-d <dest-bundle-id>` copy-all-bundles에 대한 항목에 더하여 사용할 수 있습니다. 이 명령은 동일한 인스턴스 내에서 번들을 복사하는 데 사용될 수 있습니다. 이러한 경우, 대상 서비스 신임 정보 매개변수 `(--dest-*)`를 삭제(drop)할 수 있습니다.





위의 명령은 기존의 번들 데이터 및 리소스 항목 데이터를 추출하여 새 위치에 업로드합니다. 프로세스 중 REST 서버에서 제어되는 일부 필드가 업데이트됩니다(예: updatedBy/updatedAt 필드). 또한 이러한 명령이 서비스 바인딩 및 구성 데이터를 복사하지 않으므로 대상 인스턴스에서 MT 서비스를 구성해야 할 수도 있습니다.





예를 들어, 베타 버전이 Watson 언어 번역기를 통해 아랍어 번역을 지원합니다. GA 버전에서는, 아랍어 번역은 이제 무료로 제공되지 않습니다. 베타 데이터를 새 GA 인스턴스로 복사(port)할 때, 이미 번역된 아랍어 컨텐츠는 유지됩니다. 아랍어 번역이 가능하도록 Watson 바인딩을 설정하는 경우가 아니면 소스 언어를 변경해도 아랍어 번역이 자동으로 트리거되지 않습니다. 이는 또한 소스 인스턴스가 GA 버전인 경우입니다. 외부 MT 서비스 바인딩이 GP 인스턴스에 특정합니다. 다른 인스턴스에 대한 바인딩/구성이 자동으로 복사(port)되지 않습니다.




 

