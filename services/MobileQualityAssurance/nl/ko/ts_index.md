---

copyright:
  years: 2012, 2017
  
lastupdated: "2017-01-25"  

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 



# {{site.data.keyword.mqa}} 문제점 해결 
{: #tsmqa}
다음은 {{site.data.keyword.mqa}} 사용에 대한 몇 가지 일반적인 질문에 대한 답변입니다.
{:shortdesc}

## JavaScript 하이브리드 빌드 실패
{: #ts_js_build_fail}

IBM MobileFirst Platform Foundation의 JavaScript&tm; 하이브리드 SDK 컴포넌트가 앱에 있고 필수 코드가 추가된 경우에도 JavaScript 하이브리드 {{site.data.keyword.mqa}} 애플리케이션 빌드는 실패합니다. 


{{site.data.keyword.mqa}} 애플리케이션 빌드를 실행하려고 시도하는 경우 빌드가 실패합니다.
{: tsSymptoms notoc} 


1. Android 및 iOS 플랫폼의 하이브리드 SDK 컴포넌트가 프로젝트에 설치되지 않았습니다.
2. 설치되어 있는 Android 및 iOS 플랫폼 특정 하이브리드 SDK 컴포넌트가 설치된 JavaScript SDK 컴포넌트와 호환되지 않습니다. 
3. 기본 Android SDK와 기본 iOS SDK 중 하나 또는 둘 다 설치되어 있지만 Android 및 iOS 플랫폼의 하이브리드 SDK 컴포넌트가 설치되지 않았습니다.
{: tsCauses notoc} 
 

이 문제 해결을 위한 일부 제안사항에는 다음 단계가 포함됩니다.
{: tsResolve notoc}
  1.  필수 Android 및 iOS 플랫폼의 하이브리드 SDK 컴포넌트를 모두 설치하고 앱이 지원하는 플랫폼의 필수 기본 Android SDK 또는 기본 iOS SDK를 각각 설치해야 합니다.  
  2. Android 및 iOS 플랫폼 특정 하이브리드 SDK 컴포넌트가 JavaScript 컴포넌트의 주 버전 번호와 동일하거나 이상(최대 다음 주 버전)인지 확인하십시오. 다음 표에 예제가 있습니다.
  
| JavaScript 컴포넌트 버전 | 플랫폼의 컴포넌트 버전 | 호환 가능 여부 |
|---------: |------------: |------------: |
| 1.2.3 | 1.2.3 | 예 |
| 1.2.3 | 1.2.1 | 아니오 |
| 1.2.3 | 1.3.2 | 예 |
| 1.2.3 | 2.0.0 | 아니오 |

  3. Android 및 iOS 플랫폼의 하이브리드 SDK 컴포넌트를 설치해야 합니다. 앱이 해당 플랫폼에서 실행되는 경우 기본 Android SDK 및 기본 iOS SDK가 필요하면, 하이브리드 애플리케이션에서 각 플랫폼에 대해 Android 및 iOS 플랫폼의 하이브리드 SDK 컴포넌트가 설치되어 있어야 합니다.

  
## 감성 분석을 열거나 테스트 앱을 분배할 수 없음
{: #ts_sent_fail}

감성 분석을 열거나 테스트 앱을 분배할 수 없습니다.

브라우저에서 팝업 창이 차단되어 있기 때문에 감성 분석을 열거나 테스트 앱을 분배할 수 없습니다.
{: tsSymptoms notoc} 

Mobile Quality Assurance는 팝업 창과 쿠키를 사용하여 Mobile Quality Assurance 서버와 통신합니다.
{: tsCauses notoc}


Mobile Quality Assurance 및 Mobile Quality Assurance 서버 간에 통신을 설정하려면, 팝업 창과 쿠키를 허용하도록 브라우저 설정을 구성해야 할 수 있습니다. 예를 들어, 사용자 인터페이스에서 옵션(예: 감성 점수)을 클릭하면 Mobile Quality Assurance가 서버와 통신하지 못하게 될 수 있습니다. 팝업 창과 쿠키가 차단된 경우에는 감성 분석이 표시되지 않습니다. 브라우저 설정 구성 방법에 대한 자세한 정보는 특정 브라우저에 대한 문서를 참조하십시오.
{: tsResolve notoc}


## 만료된 애플리케이션을 실행할 수 없음
{: #ts_app_expired}

Mobile Quality Assurance 애플리케이션을 실행할 수 없습니다. 

Mobile Quality Assurance 애플리케이션을 실행하려고 시도하는 경우 다음 메시지가 표시됩니다. 애플리케이션이 만기되었으므로 지금 실행할 수 없습니다.
{: tsSymptoms notoc} 

애플리케이션이 Mobile Quality Assurance 빌드 페이지에서 사용 안함으로 표시됩니다.
{: tsCauses notoc}


Mobile Quality Assurance 빌드 페이지를 확인하여 사용 안함으로 표시되는 애플리케이션이 없는지 확인하십시오. 일반적으로 테스터(애플리케이션 자체를 통해)에게 특정 버전의 빌드를 사용하지 않도록 알려주기 위해 애플리케이션이 사용 안함으로 표시됩니다. Mobile Quality Assurance 빌드 페이지에서 설정에 대한 자세한 정보는 IBM Knowledge Center의 빌드 관리를 참조하십시오.
{: tsResolve notoc}

