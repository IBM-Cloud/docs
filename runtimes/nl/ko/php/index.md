{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

*마지막 업데이트 날짜: 2016년 1월 4일*

# PHP 런타임
{: #php_runtime}

{{site.data.keyword.Bluemix}}의 PHP 런타임은 php_buildpack 기반입니다.
php_buildpack은 PHP 앱을 위한 전체 런타임 환경을 제공합니다.
{: shortdesc}

다음 조건에 해당하는 경우 php_buildpack이 사용됩니다. 
* 앱에 composer.json 파일이 포함되어 있거나 
* 앱에 *.php 파일이 포함되어 있거나 
* 앱이 ${WEBDIR} 변수를 [options.json](https://github.com/cloudfoundry/php-buildpack/blob/master/docs/config.md) 파일에 정의하고 해당 변수가 앱 내의 기존 디렉토리로 설정되어 있습니다. 

## 스타터 애플리케이션
{: #starter_application}

{{site.data.keyword.Bluemix}}는 PHP 스타터 앱을 제공합니다. PHP 스타터 애플리케이션은 사용자가 앱에 사용할 수 있는 템플리트를 제공하는 단순 PHP 앱입니다. 스타터 앱을 실험해 보고
필요한 변경사항을 작성하고 이를 {site.data.keyword.Bluemix}} 환경에 푸시할 수 있습니다. 스타터 앱 사용에 대한 지원이 필요한 경우 [스타터 애플리케이션 사용](../../cfapps/starter_app_usage.html)을 참조하십시오. 

## 런타임 버전
{: #runtime_versions}

composer.json 파일에서 앱이 사용할 PHP 버전을 지정할 수 있습니다. 예를 들면, 다음과 같습니다. 

```
{
    "version": "1.5"
}
```
{: codeblock}
자세한 정보는 [Composer
플랫폼 패키지](https://getcomposer.org/doc/02-libraries.md#platform-packages)를 참조하십시오.

버전이 지정되지 않으면 기본적으로 버전 5.5.30이 선택됩니다.

### 사용 가능한 버전: 
{: #available_versions}

다음은 현재 {{site.data.keyword.Bluemix}}에 설치되어 있는 [PHP
빌드팩](https://github.com/cloudfoundry/php-buildpack/releases/tag/v4.1.5)에서 사용 가능한 PHP 버전입니다. 

* 5.4.44
* 5.4.45
* 5.5.29
* 5.5.30
* 5.6.30
* 5.6.13
* 5.6.714

앱에서 목록에 없는 PHP 버전을 필요로 하는 경우 앱을 배치하기 위해 외부 [PHP 빌드팩](https://github.com/cloudfoundry/php-buildpack.git)을 사용할 수 있습니다. 

## 학습서 및 샘플
{: #tutorials_and_samples}
* [REST API 빌드 및 배치](http://www.ibm.com/developerworks/library/wa-deployrest-app/)
* [모바일 친화 칼로리 계산기 빌드 및 배치](http://www.ibm.com/developerworks/library/mo-bluemix-php-nutritionix-angularjs/)

## 관련 링크
{: #related_links}
* [PHP용 Cloud Foundry 빌드팩](https://github.com/cloudfoundry/php-buildpack.git)
