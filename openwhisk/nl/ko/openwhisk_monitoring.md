---

copyright:
  years: 2016
lastupdated: "2016-08-02"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# {{site.data.keyword.openwhisk_short}} 대시보드를 사용하여 {{site.data.keyword.openwhisk_short}} 활동 모니터링

[{{site.data.keyword.openwhisk}} 대시보드](https://{DomainName}/whisk/dashboard/)는 활동에 대한 그래픽 요약을 제공합니다. 대시보드를 사용하여 {{site.data.keyword.openwhisk_short}} 조치의 성능 및 상태를 판별하십시오.
{:shortdesc}

언제든지 **다시 로드**를 클릭하여 최신 활성화 로그 데이터로 대시보드를 업데이트할 수 있습니다. 

## 활동 요약
{: #summary}

이 보기는 사용자의 {{site.data.keyword.openwhisk_short}} 환경에 대한 상위 레벨 요약을 제공합니다. **활동 요약** 보기를 사용하여 {{site.data.keyword.openwhisk_short}} 사용 가능 서비스의 전체 상태 및 성능을 모니터링하십시오. 이 보기의 메트릭에서 다음을 수행할 수 있습니다.
* 조치가 호출된 횟수를 보고 서비스의 {{site.data.keyword.openwhisk_short}} 사용 가능 조치의 사용 비율을 판별합니다.
* 모든 조치에 걸쳐 전체 실패 비율을 판별합니다. 오류를 발견하는 경우, **활동 히스토그램** 보기를 보고 오류가 있는 서비스 또는 조치를 격리할 수 있습니다. **활동 로그**를 보고 오류 자체를 격리하십시오.
* 각 조치와 연관된 평균 완료 시간을 보고 조치가 얼마나 잘 수행되는지 판별할 수 있습니다. 

<!-- For tips on improving performance, see troubleshooting? -->

## 활동 타임라인
{: #timeline}

**활동 타임라인** 보기는 과거 및 현재 조치의 활동을 보기 위한 세로 막대 그래프를 표시합니다. 빨간색은 특정 조치 내의 오류를 표시합니다. 이 보기를 **활동 로그**와 연관시키면 오류에 대한 세부사항을 찾을 수 있습니다.

## 활동 히스토그램
{: #histogram}

**활동 히스토그램** 보기는 과거 및 현재 조치의 활동을 보기 위한 가로 막대 그래프를 표시합니다. 빨간색은 특정 조치 내의 오류를 표시합니다. 이 보기를 **활동 로그**와 연관시키면 오류에 대한 세부사항을 찾을 수 있습니다.

## 활동 로그
{: #log}

이 보기에는 활성화 로그의 형식화된 버전이 표시됩니다. 모든 활성화의 세부사항을 표시하지만 새 활성화가 있는지 일 분에 한 번 폴링합니다. 세부사항 로그를 표시하려면 조치를 클릭하십시오.
**참고:** CLI를 사용하여 활동 로그에 출력이 표시되도록 하려면 다음 명령을 사용하십시오. 

  ```
wsk activation poll
  ```
  {: pre}

## 필터링 옵션
{: #filtering}

보려는 조치 로그를 선택하고 로그된 활동의 시간 범위를 선택하십시오.

**참고:** 이러한 필터는 대시보드의 모든 보기에 적용됩니다. 
