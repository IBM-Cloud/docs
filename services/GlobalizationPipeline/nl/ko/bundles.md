---

copyright:
  years: 2015, 2017
lastupdated: "2016-08-30"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# 번들 작업
{: #globalizationpipeline_workingwithbundles}


작성하는 각 번들에는 생성된 번역의 전체 세트 및 리소스 파일의 키 값 쌍이 포함되어 있습니다.
{:shortdesc}

업로드하는 리소스 파일은 다음과 같은 형식으로 되어 있을 수 있으며 앱에서 UI 문자열을 나타내는 키/값 쌍의 양식으로 컨텐츠를 포함해야 합니다.


* 파일 유형: *Java™ 특성 파일(.properties)*<br>
예:
```js
logout=Logout 
back=Back 
examples=Menu 
home=Home 
web=Web 
enterprise=Enterprise 
extra=Resources 
about=About 
settings=Settings 
help=Help 
support=Support 
topics=Topics 
appExitMsg=Are you sure you want to quit the application?
```
* 파일 유형: *AMD I18N(.js)*<br>
예:
```js
define({
    "root": {
       logout: "Logout",
       back: "Back",
       examples: "Menu",
       home: "Home",
       web: "Web",
       enterprise: "Enterprise",
       extra: "Resources",
       about: "About",
       settings: "Settings",
       help: "Help",
       support: "Support",
       topics: "Topics",
       appExitMsg: "Are you sure you want to quit the application?"
    }
});
``` 
* 파일 유형: *JSON(.json)*<br>
예:
```js
{
  "logout": "Logout",
  "back": "Back",
  "examples": "Menu",
  "home": "Home",
  "web": "Web",
  "enterprise": "Enterprise",
  "extra": "Resources",
  "about": "About",
  "settings": "Settings",
  "help": "Help",
  "support": "Support",
  "topics": "Topics",
  "appExitMsg": "Are you sure you want to quit the application?"
}
``` 

또한, 리소스 파일이 다음 가이드라인을 지켜야 합니다.
* 각 키는 최대 255자일 수 있습니다.
* 각 값은 최대 8191자일 수 있습니다.
* 각 번들에는 최대 500개의 키/값 쌍이 포함될 수 있습니다.


## 번들 번역
{: #globalizationpipeline_translatingabundle}

업로드된 리소스 파일만 번역됩니다. [번들 작성](index.html#globalizationpipeline_creatingbundles) 또는 [번들 세부사항으로 수정](bundles.html#globalizationpipeline_modifyingbundles) 시 리소스 파일을 업로드할 수 있습니다.

리소스 파일을 업로드한 후 기본 기계 번역 엔진에서 제공되는 어떤 언어로도 해당 컨텐츠를 번역할 수 있습니다. 선택적으로 [기계 번역 구성](managing_translations.html#globalizationpipeline_service_to_service) 섹션에 설명된 대로 대체 기계 번역 엔진을 선택할 수 있습니다. 기본 엔진은 다음 대상 언어를 지원합니다.

<table>
<thead>
<tr>
<th>대상 언어</th>
</tr>
</thead>
<tbody>
<tr>
<td>중국어</td>
</tr>
<tr>
<td>대만어</td>
</tr>
<tr>
<td>프랑스어</td>
</tr>
<tr>
<td>독일어</td>
</tr>
<tr>
<td>이탈리아어</td>
</tr>
<tr>
<td>일본어</td>
</tr>
<tr>
<td>한국어</td>
</tr>
<tr>
<td>포르투갈어(브라질)</td>
</tr>
<tr>
<td>스페인어</td>
</tr>
</tbody>
</table>

**참고:** {{site.data.keyword.GlobalizationPipeline_short}}의 기본 기계 번역 엔진은 소스 언어로 영어만 지원합니다. 하지만 {{site.data.keyword.GlobalizationPipeline_short}} 내 구성에 사용 가능한 대체 기계 번역 엔진은 영어가 아닌 다른 소스 언어/언어 쌍의 번역을 지원합니다.

번들을 작성하면 **번들** 탭에 추가되어 쉽게 액세스할 수 있습니다. 거기부터 추가 태스크가 번역에서 수행될 수 있습니다.


## 작업할 번들 선택
{: #globalizationpipeline_selectingabundle}

1. **번들** 탭을 클릭하여 작성한 모든 번들을 보십시오.
2. 목록에서 **번들 ID**를 클릭하여 번들에 대한 추가 세부사항을 보거나 **번들 세부사항 보기** 아이콘 ![번들 세부사항 아이콘 보기를 선택하여 번들을 열고 해당 번역으로 작업](images/viewProjectDetailIcon.png)을 조치 열에서 클릭하십시오.

![번들 탭에서 사용 가능한 모든 번들을 보십시오.](images/translationBundles.png)

작업할 번들을 선택한 후 해당 번역의 상태를 보고 언어를 추가하거나 제거하고 번역을 편집하거나 리소스 파일에 대한 업데이트를 제공할 수 있습니다.

번들이 이제 필요하지 않으면 **번들** 탭에서 이를 삭제할 수 있습니다. 번들과 연관된 모든 번역도 삭제됩니다.

## 번들 세부사항 수정
{: #globalizationpipeline_modifyingbundles}

번들을 열면 이에 대한 모든 세부사항을 볼 수 있습니다. 번들에 있는 모든 대상 언어가 각각의 현재 번역 상태와 함께 나열됩니다.

![번들 세부사항 페이지가 번들에 대한 정보 및 해당 번역을 표시합니다.](images/bundleDetails.png)

번들의 각 언어의 상태는 진행 중, 실패 또는 번역됨 중 하나입니다.

| 상태   | 설명        |
|--------|-------------|
| 진행 중 | 기계 번역이 아직 진행 중입니다. |
| 실패   | 리소스 파일이 대상 언어로 번역되는 중에 오류가 발생했습니다. |
| 번역됨 | 대상 언어로의 번역이 완료되었습니다. |

번들이 사용하는 리소스 파일을 업데이트하고 대상 언어를 번들에 추가하며 대상 언어를 번들에서 삭제하고 대상 언어의 생성된 번역을 다운로드할 수 있습니다.

### 번들에서 사용된 리소스 파일 업데이트

1. 소스 언어 옆의 **리소스 업로드** 아이콘 ![이 아이콘을 선택하여 새 리소스 파일 업로드](images/uploadIcon.png)를 조치 열에서 클릭하십시오.
2. **찾아보기**를 클릭하고 업로드할 새 리소스 파일을 선택하십시오.
3. 업로드 중인 리소스 파일의 유형을 선택하십시오.
 * Java 특성 파일
 * AMD I18N
 * JSON
4. **업데이트**를 클릭하여 새 리소스 파일을 업로드하십시오.

새 리소스 파일 또는 업데이트된 리소스 파일에 있는 키/값 쌍이 이미 업로드된 값으로 동기화됩니다. 새 컨텐츠 또는 변경된 컨텐츠만 번역됩니다.

### 번들에 대상 언어 추가

1. **언어 추가** 단추를 클릭하십시오.
2. 모든 사용 가능한 대상 언어가 표시됩니다. 번들에 추가할 언어를 선택하십시오.

선택된 언어에 대한 번역이 즉시 시작됩니다.

### 번들에서 대상 언어 삭제

번들에서 대상 언어를 삭제할 때, 대상 언어 및 연관된 모든 번역을 프로젝트에서 제거합니다. 제거할 대상 언어의 조치 열에서, **이 대상 언어 제거** 아이콘 ![이 대상 언어 제거 휴지통 아이콘 선택](images/trashIcon.png)을 클릭하십시오.

### 대상 언어의 생성된 번역 다운로드

{{site.data.keyword.GlobalizationPipeline_short}}에서는 대상 언어에 대한 번역을 애플리케이션에 통합하는 몇몇 방법을 제공합니다. 리소스 파일로 번역을 다운로드하여 애플리케이션 빌드에 포함할 수 있습니다. 또한 오픈 소스 [SDK](https://github.com/IBM-Bluemix/gp-common) 중 하나를 통해 {{site.data.keyword.GlobalizationPipeline_short}}에서 동적으로 번역을 참조할 수 있습니다. 

<!-- For information on {{site.data.keyword.GlobalizationPipeline_full}} SDKs, see <link>. -->

리소스 파일로 번역을 다운로드하려면 다음을 수행하십시오. 

1. 다운로드할 대상 또는 소스 언어의 **조치** 열에서 **번역 다운로드** 아이콘 ![다운로드 아이콘을 선택하여 대상 언어에 대해 소스 키 또는 번역 다운로드](images/downloadIcon.png)를 클릭하십시오.
2. 파일 형식을 선택하십시오.
3. **다운로드**를 클릭하십시오.
