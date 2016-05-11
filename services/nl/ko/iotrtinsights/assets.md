---

copyright:
  years: 2015,2016

---

{:shortdesc: .shortdesc}

# 자산 관리 {: #manage-assets}

{{site.data.keyword.iotrtinsights_full}}의 강력한 기능 중 하나는 관리 자산에 디바이스를 맵핑하고 자산에 맵핑된 모든 디바이스에 적용되는 규칙을 작성하는 것입니다.
{: shortdesc}

예를 들어 모니터링할 단일 자산에 여러 개의 디바이스와 다수의 센서가 포함되어 있을 수 있습니다.

>**팁:** 자산을 업데이트하거나 수정할 때 맵핑 프로시저를 반복할 수 있습니다. 컨텍스트 및 맵핑 파일의 `action` 매개변수를 사용하여 자산과 디바이스를 추가하고 제거할 수 있습니다.

디바이스를 자산에 맵핑하려면 다음을 수행하십시오. 
1. 자산의 목록을 작성하고 CSV 파일로 저장하십시오.
이 파일은 자산 관리 소프트웨어의 자산 데이터를 포함합니다.
샘플 파일 형식:
```
ASSETNUM,ASSETTYPE,AS_DESCRIPTION,AS_DESCRIPTION_LD,INSTALLDATE,AS_ITEMNUM,AS_ITEMSETID,AS_LOCATION,PRIORITY,PURCHASEPRICE,REPLACECOST,SERIALNUM,AS_SITEID,AS_STATUS,ACTION  
5001,FACILITIES,New Asset 1,,2015-03-16,1001,ITEMSET,CONFRMA1,1,1000,1200,123451,MYSITE,OPERATING,+    
5002,FACILITIES2,New Asset 2,,2015-03-16,1001,ITEMSET,CONFRMA1,1,1000,1200,123452,MYSITE,OPERATING,+
```
{: codeblock}

  여기서:  
  - ASSETNUM - **필수:** 시스템의 자산 ID 번호입니다. (12)
  - ASSETTYPE - 자산의 유형입니다. (15)
  - AS_DESCRIPTION - 자산의 간략한 설명입니다. (100)
  - AS_DESCRIPTION_LD - 자산의 완전한 설명입니다. (32,000)
  - INSTALLDATE - (yyyy-MM-dd 형식의 날짜) 자산이 설치된 날짜입니다.
  - AS_ITEMNUM - 자산에 대한 관련 항목 번호입니다. (30)
  - AS_ITEMSETID - 자산에 대한 항목 세트 번호입니다. (8)
  - AS_LOCATION - 자산의 위치입니다. (12)
  - PRIORITY - (정수) 자산 우선순위입니다. (12)
  - PURCHASEPRICE - (10진수) 자산의 구매 가격입니다. (10.2)
  - REPLACECOST - (10진수) 자산을 교체하는 비용입니다. (10.2)
  - SERIALNUM - 자산 일련 번호입니다. (64)
  - AS_SITEID - 자산이 설치된 사이트의 ID입니다. (8)
  - AS_STATUS - 자산의 상태입니다. (20)
  - ACTION - `+` 기호는 자산이 추가됨을 의미하고 `-` 기호는 자산이 제거됨을 의미합니다.  
  >**팁:** 소괄호 안의 숫자는 문자열의 최대 길이를 나타냅니다. 지시되지 않는 한, 매개변수 형식은 대소문자가 혼합된 영숫자 문자입니다.

5. 자산 및 디바이스 맵핑 목록을 작성하고 CSV 파일로 저장하십시오.
  이 파일은 자산 목록에 있는 가져온 자산을 사용자의 {{site.data.keyword.iot_short}} 디바이스에 맵핑하는 데 사용됩니다.
  샘플 파일 형식:
```
  sourceType,sourceId,targetType,targetId,action  
  d:orgid:iot-device-type,device001,asset,5001,+  
  d:orgid:iot-device-type,device002,asset,5002,+  
  d:orgid:iot-device-type,device003,asset,5002,+  
  ```
  {: screen}   

  여기서:
    - sourceType - 디바이스에 대한 다음 {{site.data.keyword.iot_short}} 데이터로 구성됩니다. 
      - orgid - 사용자의 {{site.data.keyword.iot_short}} 조직 ID
      - iot-device-type - 사용자의 {{site.data.keyword.iot_short}} 디바이스 유형  
    - sourceID - 사용자의 {{site.data.keyword.iot_short}} 디바이스 ID  
    - targetType - 단어 `asset`을 사용하여 자산 맵핑을 작성합니다.
    - targetID - 작성한 컨텍스트 파일의 자산에 대한 ASSETNUM 항목
    - action - `+` 기호는 자산이 맵핑됨을 의미하고 `-` 기호는 자산이 맵핑에서 제거됨을 의미합니다.
2. 관리자로 {{site.data.keyword.iotrtinsights_short}} 콘솔에 로그인하십시오. 
2. **디바이스 > 디바이스 그룹 관리**로 이동하여 **자산 가져오기**를 클릭하십시오.  
3. 작성한 자산 파일을 찾아 선택하십시오. 
4. ![작성 아이콘](images/create.png "작성 아이콘")을 클릭하여 자산 목록을 작성하십시오.
3. 작성한 자산 및 디바이스 맵핑 파일을 찾아 선택하십시오. 
4. ![작성 아이콘](images/create.png "작성 아이콘")을 클릭하여 자산 목록을 작성하십시오.
5. **디바이스 > 디바이스 그룹 관리**로 이동하여 자산 중 하나를 클릭하고 자산에 맵핑한 디바이스 목록을 보십시오.
