---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# PHP
{: #php_runtime}
*마지막 업데이트 날짜: 2016년 3월 16일*

{{site.data.keyword.Bluemix}}의 PHP 런타임은 php_buildpack을 통해 제공됩니다.
php_buildpack은 PHP 앱을 위한 완전한 런타임 환경을
제공합니다.
{: shortdesc}

php_buildpack은 다음과 같은 조건에서 사용됩니다. 
* 앱에 composer.json 파일이 있는 경우. 또는
* 앱에 *.php 파일이 있는 경우. 또는
* 앱이 [options.json](https://github.com/cloudfoundry/php-buildpack/blob/master/docs/config.md) 파일에 ${WEBDIR} 변수를 정의하고, 해당 변수가 앱에 있는 기존 디렉토리로 설정된 경우.

## 스타터 애플리케이션
{: #starter_application}

{{site.data.keyword.Bluemix}}는 PHP 스타터 애플리케이션을 제공합니다. PHP 스타터 애플리케이션은 앱에 사용할 수 있는 템플리트를 제공하는 단순한 PHP 앱입니다. 스타터 앱을 사용하여 시험해 볼 수 있으며 {site.data.keyword.Bluemix}} 환경을 변경하고 변경사항을 푸시할 수
있습니다. 스타터 애플리케이션 사용에 대한 도움말은 [스타터 애플리케이션 사용](../../cfapps/starter_app_usage.html)을 참조하십시오. 

## 런타임 버전
{: #runtime_versions}

composer.json 파일에서 앱이 사용할 PHP 버전을 지정할 수 있습니다. 예: 

```
{
    "version": "1.5"
}
```
{: codeblock}
자세한 정보는 [작성기 플랫폼 패키지](https://getcomposer.org/doc/02-libraries.md#platform-packages)를 참조하십시오.

버전이 지정되지 않은 경우 기본적으로 버전 5.5.30이 선택됩니다. 

### 사용 가능한 버전: 
{: #available_versions}

다음 PHP 버전은 현재
{{site.data.keyword.Bluemix}}에 설치된 [PHP 빌드팩](https://github.com/cloudfoundry/php-buildpack/releases/tag/v4.1.5)에서
사용 가능합니다. 

* 5.4.44
* 5.4.45
* 5.5.29
* 5.5.30
* 5.6.30
* 5.6.13
* 5.6.14

나열되지 않은 PHP 버전이 애플리케이션에 필요한 경우
외부
[PHP 빌드팩](https://github.com/cloudfoundry/php-buildpack.git)을
사용하여 애플리케이션을 배치할 수 있습니다. 

# 관련 링크
## 샘플
* [REST API 빌드 및 배치](http://www.ibm.com/developerworks/library/wa-deployrest-app/)
* [모바일 친화 칼로리 카운터 빌드 및 배치](http://www.ibm.com/developerworks/library/mo-bluemix-php-nutritionix-angularjs/)
## 일반
* [PHP에 대한 Cloud Foundry 빌드팩](https://github.com/cloudfoundry/php-buildpack.git)
