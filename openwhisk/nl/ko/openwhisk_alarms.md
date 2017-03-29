---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Alarm 패키지 사용
{: #openwhisk_catalog_alarm}

`/whisk.system/alarms` 패키지를 사용하여 지정된 빈도로 트리거를 실행할 수 있습니다. 이는 매시간마다 시스템 백업 조치를 호출하는 등의 반복 작업 또는 태스크를 설정하는 데 유용합니다. 

패키지에는 다음 피드가 포함됩니다.

| 엔티티 | 유형 | 매개변수 | 설명 |
| --- | --- | --- | --- |
| `/whisk.system/alarms` | 패키지 | - | 알람 및 주기적 유틸리티 |
| `/whisk.system/alarms/alarm` | 피드 | cron, trigger_payload, maxTriggers | 정기적으로 트리거 이벤트 실행 |


## 정기적으로 트리거 이벤트 실행
{: #openwhisk_catalog_alarm_fire}

`/whisk.system/alarms/alarm` 피드는 지정된 빈도로 트리거 이벤트를 실행하기 위해 알람 서비스를 구성합니다. 매개변수는 다음과 같습니다.

- `cron`: 협정 세계시(UTC)로 트리거를 실행할 시점을 표시하는 UNIX crontab 구문 기반의 문자열입니다. 문자열은 공백으로 구분되는 다섯 개 필드의 시퀀스입니다(`X X X X X`).
cron 구문 사용에 대한 세부사항은 http://crontab.org를 참조하십시오. 다음은 문자열로 표시하는 빈도의 몇 가지 예입니다. 

  - `* * * * *`: 매분의 처음.
  - `0 * * * *`: 매시간의 처음.
  - `0 */2 * * *`: 2시간마다(예: 02:00:00, 04:00:00, ...)
  - `0 9 8 * *`: 매월 8번째 날의 9:00:00AM(UTC).

- `trigger_payload`: 이 매개변수의 값은 트리거가 실행될 때마다 트리거의 컨텐츠가 됩니다.

- `maxTriggers`: 이 한계에 도달하면 트리거 실행이 중지됩니다. 기본값은 1,000,000입니다. 이를 무한(-1)으로 설정할 수 있습니다. 

다음은 트리거 이벤트에서 `name` 값과 `place` 값을 사용하여 2분마다 한 번 실행할 트리거를 작성하는 예입니다. 

  ```
  wsk trigger create periodic \
    --feed /whisk.system/alarms/alarm \
    --param cron "*/2 * * * *" \
    --param trigger_payload "{\"name\":\"Odin\",\"place\":\"Asgard\"}"
  ```
  {: pre}

생성된 각 이벤트는 `trigger_payload` 값에서 지정된 값을 매개변수로 포함합니다. 이 경우, 각 트리거 이벤트는 `name=Odin` 및 `place=Asgard` 매개변수를 갖게 됩니다.

**참고**: `cron` 매개변수도 여섯 개 필드의 사용자 정의 구문을 지원합니다. 여기서, 첫 번째 필드는 초를 나타냅니다.
이 사용자 정의 cron 구문 사용에 대한 세부사항은 다음을 참조하십시오. https://github.com/ncb000gt/node-cron
다음은 여섯 개 필드를 사용한 표기법의 예입니다.
  - `*/30 * * * * *`: 30초마다.

