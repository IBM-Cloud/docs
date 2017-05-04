---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-22"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}



<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->

# 데이터 백업
{{site.data.keyword.cloudantfull}} 데이터베이스를 복제하여 {{site.data.keyword.iotinsurance_full}} 데이터를 백업할 수 있습니다.
{:shortdesc}

다음 표에는 {{site.data.keyword.iotinsurance_full}}에 저장된 {{site.data.keyword.iotinsurance_short}} 데이터베이스가 있습니다. 

*표 1: {{site.data.keyword.iotinsurance_short}} 데이터베이스*

DB 이름| 변경 빈도| 변경 이유 | 백업 필수 | 설명
------------- | -------------| -------------| -------------| -------------
favorites|관리|새 관리자 조치|예|-
Devices|관리|새 디바이스나 사용자 추가 또는 제거|예| Transformer가 메모리에 테이블을 동적으로 생성하고 디바이스 제공업체의 데이터로 채웁니다. 직접 연결된 게이트웨이의 경우 이 테이블에 디바이스를 저장합니다.
hazardevents|랜덤|새 실드 이벤트 발견|예|-
Jscode|관리|배치된 실드의 새 JS 코드|예*| 이 관리자는 선택적으로 백업을 건너뛰고 새 JS 코드 버전을 배치할 수 있습니다.
Promotions|관리|새 프로모션 추가|예|-
shieldassociations|관리|새 사용자 또는 실드 추가|예|-
Shields|관리|새 실드 추가|예|-
Users|관리|새 사용자 추가|예|-
aggregation|-|-|아니오|다시 빌드할 수 있습니다.
aggregationschedule|-|-| 아니오|다시 빌드할 수 있습니다.

{{site.data.keyword.iotinsurance_short}} 데이터를 백업하려면 다음 단계를 수행하십시오. 

## 복제본 {{site.data.keyword.cloudant_short_notm}} 인스턴스 작성
{: #createinstance}
[{{site.data.keyword.cloudant}} 복제 지시사항 ![외부 아이콘](../../icons/launch-glyph.svg)](https://docs.cloudant.com/replication.html)을 사용하여 복제본 {{site.data.keyword.cloudant}} 인스턴스를 작성하십시오. 재해 복구 시 사용할 수 있게 원래 {{site.data.keyword.iotinsurance_short}} 서비스와 다른 위치에 복제본을 작성하십시오. 예를 들어, 원래 인스턴스가 댈러스에 있다면 런던에 복제본을 둘 수 있습니다. 

## 신임 정보 및 URL 찾기
{: #locate_credentials}
원래 {{site.data.keyword.cloudant}} 인스턴스 와 복제된 인스턴스의 신임 정보와 URL을 찾으십시오. 
1. {{site.data.keyword.cloudant}} 서비스를 엽니다. 
2. 서비스 이름 아래에 있는 **서비스 신임 정보** 탭을 클릭합니다. 
3. **신임 정보 보기**를 클릭합니다. 
4. 사용자 이름, 비밀번호, URL을 기록합니다. 

## 새 복제 태스크 작성
{: #create_replication}
백업해야 하는 개별 데이터베이스의 복제 태스크를 작성하십시오. 백업이 필요한 데이터베이스는 이전 섹션의 표 1에 나열되어 있습니다. 

1. {{site.data.keyword.Bluemix_notm}} 콘솔을 엽니다. 

2. 원래 {{site.data.keyword.cloudant}} 서비스를 엽니다. 

3. **시작**을 클릭하여 {{site.data.keyword.cloudant}} 대시보드를 엽니다. 

4. 메뉴에서 **복제**를 선택합니다.

5. 소스 데이터베이스 섹션에서 원래 데이터베이스의 URL을 입력하십시오. 개별 데이터베이스 URL의 형식은 https://<CloudantbaseURL>/<database_name>과 같습니다. 예를 들어, hazardevents 데이터베이스의 URL은 https://<CloudantbaseURL>/hazardevents입니다. 

6. 대상 데이터베이스 섹션에서 새 데이터베이스의 URL을 입력하십시오. 

7. **중요:** **이 복제를 연속 작성**을 선택하지 마십시오. 연속 복제를 수행하면 성능에 심각한 영향을 줄 수 있습니다. 

8. **데이터 복제**를 클릭합니다.  

9. (선택사항) 후속 복제 태스크에서 이전 데이터를 겹쳐쓰기 때문에 CSV 파일로 데이터를 내보내는 것이 좋습니다. 지시사항은 [Cloudant JSON을 CSV, RSS 또는 iCal로 내보내기 ![외부 링크 아이콘](../../icons/launch-glyph.svg)](https://developer.ibm.com/clouddataservices/2015/09/22/export-cloudant-json-as-csv-rss-or-ical/){: new_window}를 참조하십시오. 

10. 각각의 데이터베이스에 대해 이 단계를 반복하십시오. 

## 백업 실행
{: #run_backup}
복제 태스크를 작성한 후에는 언제든 백업을 다시 실행할 수 있습니다. 
1. {{site.data.keyword.Bluemix_notm}} 콘솔을 엽니다. 
2. 원래 {{site.data.keyword.cloudant}} 서비스를 엽니다. 
3. **시작**을 클릭하여 {{site.data.keyword.cloudant}} 대시보드를 엽니다. 
4. 메뉴에서 **복제**를 클릭한 다음 **모든 복제**를 선택합니다. 
5. 모든 데이터베이스를 선택하고 개별 복제를 다시 실행합니다. **활성 복제**를 클릭하여 진행 중인 작업의 상태를 확인합니다. 
6. 모든 복제가 완료되면 데이터를 CSV 플랫 파일로 내보낼 수 있습니다. 

## 데이터 복원
{: #restore_data}
복제된 데이터베이스에서 데이터를 복원하거나 저장된 CSV 파일에서 로드하여 데이터를 복원할 수 있습니다. 
1. {{site.data.keyword.Bluemix_notm}} 콘솔을 엽니다. 
2. {{site.data.keyword.iotinsurance_short}} 서비스를 중지합니다. 
3. 다음 방법 중 하나로 데이터를 복원합니다. 
  - CSV 백업 파일에서 기본 Cloudant 인스턴스로 직접 데이터를 로드합니다. 
  - 복제된 데이터베이스를 소스로 원래 데이터베이스를 대상으로 사용하는 복제 태스크를 작성합니다. 이 태스크는 복제된 데이터를 원래 데이터베이스로 이동합니다. 
4. 다음 스크립트를 실행하여 디자인 문서를 다시 작성하고 참조 무결성을 복원합니다. 스크립트는 [{{site.data.keyword.iotinsurance_short}} API 예제 GitHub 사이트 ![외부 링크 아이콘](../../icons/launch-glyph.svg)](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/){: new_window}에 있습니다. 
  - iot4i-api/wearable-framework/auto-create/create.sh - 이 스크립트는 {{site.data.keyword.cloudant}} 내에 디자인 문서를 다시 작성합니다. 
  - iot4i-api/wearable-framework/health/check-relations - 이 스크립트는 참조 무결성을 다시 설정합니다. 예를 들어, 이 스크립트는 실드를 삭제하였으나 사용자 연관이 남아 있는 케이스를 수정합니다. 
