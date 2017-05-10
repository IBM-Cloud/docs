---

copyright:
  years: 2015, 2017
lastupdated: "2016-08-30"

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# {{site.data.keyword.GlobalizationPipeline_short}} 문제점 해결
{: #globalizationpipelinets}


다음은 {{site.data.keyword.GlobalizationPipeline_short}} 사용에 대한 일반적인 질문에 대한 답변입니다.
{:shortdesc}


## 내 앱의 이름이 올바르게 번역되지 않음
{: #problem1}

일부 문자열의 생성된 번역이 예상과 다릅니다.
{:shortdesc}

리소스 파일 번역 시, 제품 이름 또는 기타 고유 명사가 포함된 문자열은 적절하게 번역되지 않습니다.
{: tsSymptoms}

종종 제품 이름 또는 고유 명사는 특히 이름에 실제 단어가 포함된 경우 다른 언어로 적절히 번역되지 않습니다. 이러한 유형의 단어 및 구문 번역 시, 특정 언어로 해당 단어의 의미에 따라 번역된 텍스트의 의미가 영어 이름과 다를 수 있습니다.
{: tsCauses}

사용하기 전에 제품 이름의 번역을 테스트하고, 문제점이 발견되면 그에 따라 텍스트 또는 번역을 수정하십시오. 기계 번역 사용 시 쓰기 스타일 팁에 대해서는 [기계 번역 팁](./tips.html#globalizationpipeline_tips)을 참조하십시오.
{: tsResolve}



## 리소스 파일을 업로드할 수 없음
{: #problem2}

업로드하려는 리소스 파일이 허용되지 않습니다.
{:shortdesc}

새 번역 번들에 리소스 파일을 추가하거나 번역될 기존의 리소스 파일을 업데이트할 때, 오류가 발생합니다.
{: tsSymptoms}

{{site.data.keyword.GlobalizationPipeline_short}}에서는 다음 유형의 리소스 파일만 허용합니다. Java™ .properties, JSON 및 AMD I18N
{: tsCauses}

업로드되는 리소스 파일이 다음 유형 중 하나인지 확인하십시오.
{: tsResolve}
* Java .properties
* JSON
* AMD I18N



## 내 리소스 파일이 너무 커서 업로드할 수 없음
{: #problem3}

업로드하려는 리소스 파일이 허용되지 않습니다.
{:shortdesc}

번역 프로젝트에 리소스 파일을 추가하거나 업데이트할 때, 파일의 일부가 너무 커서 오류가 발생합니다.
{: tsSymptoms}

{{site.data.keyword.GlobalizationPipeline_short}}에서는 특정 크기 요구사항과 일치하는 리소스 파일만 허용할 수 있습니다.
{: tsCauses}

리소스 파일이 다음 가이드라인을 따르는지 확인하십시오.
{: tsResolve}
* 각 키는 최대 256자일 수 있습니다.
* 각 값은 최대 2048자일 수 있습니다.
* 각 번역 프로젝트에는 최대 500개의 키/값 쌍이 포함될 수 있습니다.
* 리소스 파일은 2MB보다 클 수 없습니다.




## 문자열에 포함된 변수 주변의 공백이 일치하지 않음
{: #problem5}

번역 이후 변수 주변에 사용된 공백이 항상 동일하지는 않습니다.
{:shortdesc}

문자열 내에 포함된 변수 주변에 사용된 공백이 번역 이후 언어 간에 항상 일치하지는 않습니다.
{: tsSymptoms}

기계 번역 엔진이 자연어로 작업하도록 디자인되고, 프로그래밍 언어로 사용된 특정 구문을 처리하는 방법을 항상 인식하거나 알 수 있는 것은 아닙니다. 따라서, 일반 텍스트와 혼합된 구문의 처리가 다를 수 있습니다.
{: tsCauses}

{{site.data.keyword.GlobalizationPipeline_short}}에서는 변수를 나타내는 데 공통적으로 사용된 "{}" 패턴을 현재 인식하고 내부에 포함된 컨텐츠의 기존 형식을 유지합니다.
{: tsResolve}
