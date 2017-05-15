---

copyright:
  years: 2015, 2017
lastupdated: "2016-07-12"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# 기계 번역 팁
{: #globalizationpipeline_tips}


기계 번역은 대략적인 소스 텍스트의 의미를 제공하는 데 효율적일 수 있습니다. 그러나 기계 번역의 품질 및 유용성은 사용하는 기계 번역 엔진 및 대상 언어에 따라 크게 다릅니다. 기계 번역 품질의 주요 요인 중 하나는 소스 자체의 품질입니다. 구어적 표현, 불완전한 문장, 잘못된 구두법 및 애매한 단어 및 구문이 있는 소스 텍스트는 정확히 번역되지 않을 수 있습니다.
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} 앱 UI를 작성할 때, 몇 가지의 기본 쓰기 가이드라인에 따르면 소스 언어 뿐 아니라 기계 번역의 품질도 개선할 수 있습니다.

또한, 원어민에게 기계 번역의 검토 및 편집을 요청하십시오. 앱 사용자로부터 피드백도 수집하십시오. 사용자가 번역의 유용성과 정확성을 가장 잘 판단할 수 있습니다.

## 쓰기 스타일 팁
{: #writingstyletips}

* **짧은 길이부터 중간 길이 단순 문장까지 사용(5 - 20개의 단어):** 기계 번역 엔진에서는 종종 세미콜론이 있는 문장을 포함하여 복합적이고 복잡한 문장을 번역하기가 어렵습니다. 한 문장에 하나의 의미를 나타내십시오. 문장에 두 개의 능동형 동사가 포함되어 두 개의 의미를 나타내는 경우 문장을 두 개의 문장으로 구분하십시오. 또한 기계 번역 엔진에는 충분한 문맥을 제공할 수 없을 정도로 짧은 문장은 구문 분석하기가 어렵습니다. 
* **구문 금지:** 가능한 경우 항상 완전한 문장을 사용하십시오. 구문은 표제 및 하위 표제에는 사용될 수 있지만, 간결한 표제 스타일 쓰기는 피하십시오. 완전한 문장을 사용하여 목록을 소개하십시오.
* **숙어, 속어 및 전문용어 금지:** 글자 그대로의 번역으로 뜻이 통하지 않는 구문을 바꾸십시오. 예를 들어, "on the fly"를 "dynamic"으로 "on the other hand"를 "alternatively"로 "keep in mind"를 "remember"로 바꾸십시오.
* **유머, 풍자, 구어적 표현, 이모티콘 및 은유를 피하십시오.**
* **간단 명료화:** 불필요한 텍스트 및 중복성을 제거하십시오. 예를 들어, "It is useful to remember that large values increase the response time"을 "Large values increase the response time"으로 바꾸십시오.
* **대문자로만 작성된 문장 금지:** 대문자는 단어의 의미에 단서를 제공합니다. 예를 들어, "BILL"을 쓰는 경우 기계 번역 엔진은 이름 "Bill"을 의미하는지 단어 "bill"을 의미하는지 여부를 판별할 수 없습니다.
* **애매한 단어 금지:** 예를 들어, "after" 또는 "when"의 자리에 "once"를 사용하지 마십시오. "although" 또는 "whereas"의 자리에 "while"을 사용하지 마십시오. "might" 또는 "can"을 의미하는 경우 "may"를 사용하지 마십시오.
* **대명사 금지:** 가능한 경우 명사 또는 명사 구문을 반복하십시오. 대명사 "it"이 특히 문제가 됩니다.
* **가능한 경우 능동태로 쓰기:** 능동형 문장이 일반적으로 수동형 문장보다 명확합니다. 예를 들어, "The most efficient path is determined" 대신 "The utility determines which path is most efficient"를 쓰십시오.
* **문화적으로 특정한 정보를 피하십시오.**
* **기계 번역 엔진이 제품 이름을 번역할 수 있음에 주의:** 다수의 국가에서 기존의 영어 제품 이름을 유지하지만, 기계 번역 엔진은 특히 이름에 실제 단어가 포함된 경우 제품 이름을 번역하려고 할 수 있습니다. 제품 이름을 사용하기 전에 해당 번역을 테스트하십시오. 문제점이 발견되면 그에 따라 텍스트 또는 번역을 수정하십시오.
* **모든 정보가 하나의 언어로 작성되는지 확인:** 텍스트에 다른 언어로 된 하나 또는 두 개의 단어가 포함된 경우에도 기계 번역 엔진에서는 모든 정보가 하나의 언어로 되어 있다고 가정할 수 있습니다. 예를 들어, 텍스트에 "en route"(프랑스어)가 포함된 경우 기계 번역 엔진이 영어 단어의 경우와 같이 해당 단어를 계속 번역하려고 시도합니다.
* **홍보 문구 금지:** 홍보 문구는 종종 특정 문화에 대한 대중의 생각에 따라 달라집니다. 기계 번역 엔진은 이러한 종류의 홍보 문구를 정확하게 번역하기 어려우니 피하십시오.
* **목록 항목이 완전하고 유사한지 확인:** 예를 들어, 하나의 항목이 동사로 시작되는 경우 모든 항목이 동사로 시작되는지 확인하십시오.
* **please 및 thank you 사용 금지:** 이러한 단어가 부적절하거나 일부 문화에서는 건방지게 보일 수 있습니다.
* **숫자가 아닌 형식으로 날짜 쓰기:** 숫자로 된 날짜 형식은 국가에 따라 다릅니다. 월 이름, 일 및 연도를 작성하십시오. 예를 들어, 9/01/03 대신 2003년 9월 1일을 사용하십시오. 이는 2003년 9월 1일 또는 2003년 1월 9일로 해석될 수도 있습니다.

## 문법 팁
{: #grammartips}

* **적절한 구두법 사용:** 마침표 및 쉼표를 생략하면 기계 번역 엔진이 정보를 잘못 해석할 수 있습니다.
* **주어가 해당 동사와 일치하는지 확인:** 복수형 주어에 복수형 동사를 쓰고 단수형 주어에 단수형 동사를 쓰는지 확인하십시오.
* **단순 현재 시제 동사 사용:** 다수의 기타 언어에는 능동태/수동태 및 시제와 같은 영어 동사의 특성이 없습니다. 가능하면 미래 및 과거 시제를 피하십시오. 예를 들어, "If you run this program, DB2® will return an error message"를 "If you run this program, DB2 returns an error message"로 다시 쓸 수 있습니다.
* **대명사가 해당 선행사와 일치하는지 확인:** 예를 들어, "A user should first determine their tasks"는 "Users should first determine their tasks"로 다시 써야 합니다.
* **현수 수식어 금지:** 수식하려고 하는 명사를 수식하도록 적합한 수식어를 쓰십시오. 예를 들어, "While typing in commands, the program does not send any messages to you"는 "While typing in commands, you do not receive any messages from the program"으로 다시 쓸 수 있습니다.
* **이중 부정 금지:** 예를 들어, "Do not omit the date"를 "Include the date."로 바꿀 수 있습니다.
* **문장 시작 시 동사의 부정사(to write)를 피하고 분사(writing) 및 과거 분사(wrote) 양식 표시:** 이러한 동사 양식은 번역하는 데 종종 애매하고 어렵습니다.
* **명사 문자열 금지:** 복합 명사 구문(예: "special filter factor estimate considerations")을 3개의 단어까지로만 제한하십시오.
* **여러 문법 카테고리의 단어 사용 금지:** 영어에서 많은 단어(예: "default")가 명사 또는 동사일 수 있습니다. 이 구조는 여러 다른 언어의 경우에는 적용되지 않습니다. 각 단어를 사용하는 방법을 일치시키십시오. 예를 들어, 항상 "default"를 명사로 사용하십시오.
* **문장의 요소가 유사한지 확인:** 예를 들어, 문장 내 목록에 모두 명사 또는 모두 동사를 사용하십시오. 명사 및 동사를 혼용하지 마십시오.
* **필수 단어 생략 금지:** 예를 들어, "The file names are displayed in uppercase characters and the file extensions in lowercase" 대신 "The file names are displayed in uppercase characters and the file extensions are displayed in lowercase characters"를 사용하십시오. 단어 "that"을 사용하여 필요에 따라 의미를 명확하게 하십시오. 예를 들어, "If you determine the problem is a missing file"을 "If you determine that the problem is a missing file"로 바꾸십시오.
* **대시를 삽입구로 사용 금지:** 예를 들어, "When you get to this point - the point when all data has been loaded - you need to test the system"을 쓰지 마십시오. 대시를 쉼표로 바꾸거나 문장을 다시 쓰십시오.
 
## 용어 팁
{: #terminologytips}

* **용어를 일관되게 사용:** 동일한 것을 나타내는 데 여러 용어를 사용하지 마십시오. 둘 이상의 것을 가리키는 데 하나의 용어를 사용하지 마십시오.
* **전문 용어에 대한 설명을 포함하십시오.**
* **기타 환경 및 컨텍스트에서 여러 의미를 포함하는 용어 금지:** 이러한 용어에는 "billion," "domestic" 및 "foreign"이 있습니다.
* **일관되고 표준화된 대문자 표시, 하이픈 사용 및 단어 조합 사용:** 예를 들어, "fix pack" 대신 "fix pack"을 쓰십시오.
* **용어가 고유 명사인 경우가 아니면 소문자를 사용하십시오.**
* **특수 기호 금지:** # 기호를 사용해야 하는 경우 파운드 기호로 이를 참조하지 마십시오. 대신, 이를 숫자 기호(#)로 호출하십시오.
* **약어 금지:** 기계 번역 엔진이 공통 약어(예: IBM 및 DB2)를 인식할 수도 있지만, 모든 약어를 인식하지는 않습니다. 가능하면 약어를 피하십시오. 라틴 약어(예: "i.e." 및 "etc.")를 사용하지 마십시오.

## 구두법 팁
{: #punctuationtips}

* **"and or"을 나타내는 데 슬래시 사용 금지:** 문장을 다시 써서 정확한 의미를 표시하십시오. 예를 들어, "You can view the draft copy and/or the review copy"를 "You can view the draft copy, the review copy, or both"로 다시 쓸 수 있습니다.
* **(s)를 추가하여 복수형 표시 금지:** "one or more" 구문을 사용하거나 복수형 양식만 사용하십시오.
* **and를 의미하는 데 앰퍼샌드(&)를 사용하지 마십시오.**
* **쉼표를 사용하여 문장 내 목록의 항목을 분리하고 목록의 접속사 앞에 쉼표 배치:** 예를 들어, "Select your company, location, and profession"입니다.

## 맞춤법 팁
{: #spellingtips}

* **맞춤법 검사:** 단어의 맞춤법이 잘못되면 번역 오류가 발생할 수 있습니다. 항상 오자를 검사하십시오!
* **정확한 맞춤법 사용:** 대문자 및 소문자 사용을 포함하여 용어, 약어 및 고유 명사의 맞춤법이 항상 정확한지 확인하십시오.

## 시각적 프리젠테이션 팁
{: #visualtips}

* **그래픽의 텍스트를 피하십시오.**
* **강조 형식을 사용하지 마십시오.**

