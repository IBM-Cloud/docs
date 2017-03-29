---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Cloudant 패키지 사용
{: #openwhisk_catalog_cloudant}
`/whisk.system/cloudant` 패키지를 사용하면 Cloudant 데이터베이스를 사용하여 작업할 수 있습니다. 다음 조치 및 피드를 포함합니다.

| 엔티티 | 유형 | 매개변수 | 설명 |
| --- | --- | --- | --- |
| `/whisk.system/cloudant` | 패키지 | dbname, host, username, password | Cloudant 데이터베이스와 함께 작동 |
| `/whisk.system/cloudant/read` | 조치 | dbname, id | 데이터베이스에서 문서 읽기 |
| `/whisk.system/cloudant/write` | 조치 | dbname, overwrite, doc | 데이터베이스에 문서 쓰기 |
| `/whisk.system/cloudant/changes` | 피드 | dbname, maxTriggers | 데이터베이스에 대한 변경 시 트리거 이벤트 실행 |

다음 주제에서는 `/whisk.system/cloudant` 패키지 내에서의 Cloudant 데이터베이스 설정, 연관된 패키지 구성 및 조치 및 피드 사용에 대해 설명합니다.

## Bluemix에서 Cloudant 데이터베이스 설정
{: #openwhisk_catalog_cloudant_in}

Bluemix의 OpenWhisk를 사용하는 경우, OpenWhisk는 Bluemix Cloudant 서비스 인스턴스에 대한 패키지 바인딩을 자동으로 작성합니다. Bluemix의 OpenWhisk 및 Cloudant를 사용하지 않는 경우에는 다음 단계로 건너뛰십시오.

1. Bluemix [대시보드](http://console.ng.Bluemix.net)에서 Cloudant 서비스 인스턴스를 작성하십시오.

  서비스 인스턴스의 이름, 사용자가 속한 Bluemix 조직 및 영역을 기억하십시오.

2. 사용자가 이전 단계에서 사용한 Bluemix 조직 및 영역에 해당되는 네임스페이스에 OpenWhisk CLI가 있는지 확인하십시오.

  ```
  wsk property set --namespace myBluemixOrg_myBluemixSpace
  ```
  {: pre}

  또는 `wsk property set --namespace`를 사용하여 액세스 가능한 목록에서 네임스페이스를 설정할 수 있습니다.

3. 네임스페이스 내의 패키지를 새로 고치십시오. 일반적으로 새로 고치기는 사용자가 작성한 Cloudant 서비스 인스턴스에 대한 패키지 바인딩을 작성합니다.

  ```
  wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_testCloudant_Credentials-1
  ```

  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_testCloudant_Credentials-1 private binding
  ```

  Bluemix Cloudant 서비스 인스턴스에 해당하는 패키지 바인딩의 완전한 이름이 표시됩니다.

4. 이전에 작성된 패키지 바인딩이 Cloudant Bluemix 서비스 인스턴스 호스트 및 신임 정보로 구성되었는지 확인하십시오.

  ```
  wsk package get /myBluemixOrg_myBluemixSpace/Bluemix_testCloudant_Credentials-1 parameters
  ```
  {: pre}
  ```
  ok: got package /myBluemixOrg_myBluemixSpace/Bluemix_testCloudant_Credentials-1, displaying field parameters
  ```
  ```json
  [
      {
          "key": "username",
          "value": "cdb18832-2bbb-4df2-b7b1-Bluemix"
      },
      {
          "key": "host",
          "value": "cdb18832-2bbb-4df2-b7b1-Bluemix.cloudant.com"
      },
      {
          "key": "password",
          "value": "c9088667484a9ac827daf8884972737"
      }
      ]
  ```

## Bluemix 외부에서 Cloudant 데이터베이스 설정
{: #openwhisk_catalog_cloudant_outside}

Bluemix에서 OpenWhisk를 사용하지 않거나 Bluemix 외부에서 Cloudant 데이터베이스를 설정하려면 Cloudant 계정의 패키지 바인딩을 수동으로 작성해야 합니다. Cloudant 계정 호스트 이름, 사용자 이름, 비밀번호가 필요합니다. 

1. Cloudant 계정에 대해 구성된 패키지 바인딩을 작성하십시오. 

  ```
  wsk package bind /whisk.system/cloudant myCloudant -p username MYUSERNAME -p password MYPASSWORD -p host MYCLOUDANTACCOUNT.cloudant.com
  ```
  {: pre}

2. 패키지 바인딩이 있는지 확인하십시오.

  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myNamespace/myCloudant private binding
  ```


## Cloudant 데이터베이스에 대한 변경 청취
{: #openwhisk_catalog_cloudant_listen}

`changes` 피드를 사용하여 Cloudant 데이터베이스에 대한 모든 변경 시 트리거를 실행하도록 서비스를 구성할 수 있습니다.매개변수는 다음과 같습니다.

- `dbname`: Cloudant 데이터베이스의 이름입니다.
- `maxTriggers`: 이 한계에 도달하면 트리거 실행이 중지됩니다. 기본값은 무한(infinite)입니다.


1. 앞에서 작성한 패키지 바인딩의 `changes`를 사용하여 트리거를 작성하십시오. `/myNamespace/myCloudant`를 사용자의 패키지 이름으로 대체하십시오.

  ```
  wsk trigger create myCloudantTrigger --feed /myNamespace/myCloudant/changes --param dbname testdb
  ```
  {: pre}
  ```
  ok: created trigger feed myCloudantTrigger
  ```

2. 활성화를 위해 폴링하십시오.

  ```
wsk activation poll
  ```
  {: pre}

3. Cloudant 대시보드에서 기존 문서를 수정하거나 새 문서를 작성하십시오.

4. 각 문서 변경에 대한 `myCloudantTrigger` 트리거의 새 활성화를 관찰하십시오.
  
  **참고**: 새 활성화를 관찰할 수 없으면 Cloudant 데이터베이스에 대한 읽기 및 쓰기에 관한 후속 절을 참조하십시오. 아래의 읽기 단계와 쓰기 단계를 테스트하면 Cloudant 신임 정보가 올바른지 확인하는 데 유용합니다. 
  
  이제 규칙을 작성하고 규칙을 조치에 연관시켜 문서 업데이트에 반응할 수 있습니다.
  
  생성된 이벤트의 컨텐츠에 다음 매개변수가 있습니다.
  
  - `id`: 문서 ID입니다.
  - `seq`: Cloudant에서 생성한 시퀀스 ID입니다. 
  - `changes`: 오브젝트의 배열이며 각각 문서의 개정 ID를 포함하는 `rev` 필드를 가집니다.
  
  트리거 이벤트의 JSON 표시는 다음과 같습니다.
  
  ```json
  {
      "id": "6ca436c44074c4c2aa6a40c9a188b348",
      "seq": "2-g1AAAAL9aJyV-GJCaEuqx4-BktQkYp_dmIfC",
      "changes": [
          {
              "rev": "2-da3f80848a480379486fb4a2ad98fa16"
          }
      ]
  }
  ```
  
## Cloudant 데이터베이스에 쓰기
{: #openwhisk_catalog_cloudant_write}

조치를 사용하여 `testdb`라는 Cloudant 데이터베이스에 문서를 저장할 수 있습니다. 이 데이터베이스가 Cloudant 계정에 존재하는지 확인하십시오.

1. 앞에서 작성한 패키지 바인딩 내의 `write` 조치를 사용하여 문서를 저장하십시오. `/myNamespace/myCloudant`를 사용자의 패키지 이름으로 대체하십시오.

  ```
  wsk action invoke /myNamespace/myCloudant/write --blocking --result --param dbname testdb --param doc "{\"_id\":\"heisenberg\",\"name\":\"Walter White\"}"
  ```
  {: pre}
  ```
  ok: invoked /myNamespace/myCloudant/write with id 62bf696b38464fd1bcaff216a68b8287
  ```
  ```json
  {
    "id": "heisenberg",
    "ok": true,
    "rev": "1-9a94fb93abc88d8863781a248f63c8c3"
  }
  ```

2. 문서를 Cloudant 대시보드에서 찾아서 문서가 존재하는지 확인하십시오.

  `testdb`에 대한 대시보드 URL은 다음과 유사합니다. `https://MYCLOUDANTACCOUNT.cloudant.com/dashboard.html#database/testdb/_all_docs?limit=100`.


## Cloudant 데이터베이스에서 읽기
{: #openwhisk_catalog_cloudant_read}

조치를 사용하여 `testdb`라는 Cloudant 데이터베이스에서 문서를 페치할 수 있습니다. 이 데이터베이스가 Cloudant 계정에 존재하는지 확인하십시오.

- 앞에서 작성한 패키지 바인딩 내의 `read` 조치를 사용하여 문서를 페치하십시오. `/myNamespace/myCloudant`를 사용자의 패키지 이름으로 대체하십시오.

  ```
  wsk action invoke /myNamespace/myCloudant/read --blocking --result --param dbname testdb --param id heisenberg
  ```
  {: pre}
  ```json
  {
    "_id": "heisenberg",
    "_rev": "1-9a94fb93abc88d8863781a248f63c8c3",
    "name": "Walter White"
  }
  ```

## 조치 시퀀스와 변경 트리거를 사용하여 Cloudant 데이터베이스에서 문서 처리
{: #openwhisk_catalog_cloudant_read_change notoc}
규치에서 조치 시퀀스를 사용하여 Cloudant 변경 이벤트와 관련된 문서를 페치하여 처리할 수 있습니다.

문서를 처리하는 조치의 샘플 코드입니다.
```javascript
function main(doc){
  return { "isWalter:" : doc.name === "Walter White"};
}
```

Cloudant에서 문서를 처리하는 조치를 작성하십시오. 
```
wsk action create myAction myAction.js
```
{: pre}

데이터베이스에서 문서를 읽기 위해 Cloudant 패키지의 `read` 조치를 사용할 수 있습니다.
`read` 조치는 조치 시퀀스를 작성하기 위해 `myAction`으로 구성될 수 있습니다. 
```
wsk action create sequenceAction --sequence /myNamespace/myCloudant/read,myAction
```
{: pre}

`sequenceAction` 조치는 새 Cloudant 트리거 이벤트에서 조치를 활성화하는 규칙에 사용될 수 있습니다. 
```
wsk rule create myRule myCloudantTrigger sequenceAction
```
{: pre}

**참고**: Cloudant `changes` 트리거는 더 이상 지원되지 않는 `includeDoc` 매개변수를 지원하는 데 사용되었습니다.
  `includeDoc`으로 이전에 작성했던 트리거를 다시 작성해야 합니다. 트리거를 다시 작성하려면 다음 단계를 수행하십시오. 
  ```
  wsk trigger delete myCloudantTrigger
  ```
  {: pre}
  ```
  wsk trigger create myCloudantTrigger --feed /myNamespace/myCloudant/changes --param dbname testdb
  ```
  {: pre}

  위에서 설명된 예제를 사용하여 변경된 문서를 읽고 기존 조치를 호출하기 위한 조치 시퀀스를 작성할 수 있습니다.
  더 이상 유효하지 않은 모든 규칙을 사용 안함으로 설정하고 조치 시퀀스 패턴을 사용하여 새 규칙을 작성하십시오. 

