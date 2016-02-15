{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

*마지막 업데이트 날짜: 2016년 1월 12일*

# Ruby 런타임
{: #ruby_runtime}

{{site.data.keyword.Bluemix}}의 Ruby 런타임은 ruby_buildpack 기반입니다.
ruby_buildpack은 Ruby 앱에 대한 전체 런타임 환경을
제공합니다.
{: shortdesc}

앱의 루트 디렉토리에 Gemfile이 있는 경우 ruby_buildpack이 사용됩니다. 그런 다음 종속 항목을 설치하는 데 번들러를 사용합니다. 

## 스타터 애플리케이션
{: #starter_application}

{{site.data.keyword.Bluemix}}는 Ruby 스타터 애플리케이션을 제공합니다. Ruby 스타터 애플리케이션은 단순 Ruby 앱으로 사용자가 앱에 사용할 수 있는 템플리트를 제공합니다. 스타터 앱을 사용해 보고
변경사항을 작성하여 {{site.data.keyword.Bluemix}} 환경에 푸시할 수 있습니다. 스타터 애플리케이션 사용에 대한 지원이 필요한 경우 [스타터 애플리케이션 사용](../../cfapps/starter_app_usage.html)을 참조하십시오. 

## 런타임 버전
{: #runtime_versions}

애플리케이션의 Gemfile에 앱에서 사용할 Ruby 버전을 지정할 수 있습니다. 예를 들면, 다음과 같습니다. 


```
  source 'https://rubygems.org'
  ruby '2.1.7'
  gem 'sinatra', '>= 0'
gem 'haml', '>= 0'
gem 'json', '>=0'```
{: codeblock}

버전을 지정하지 않은 경우 기본적으로 버전 2.2.2를 선택합니다.

### 사용 가능한 버전: 
{: #available_versions}

다음은 현재 {{site.data.keyword.Bluemix}}에 설치되어 있는 [Ruby
빌드팩](https://github.com/cloudfoundry/ruby-buildpack/releases/tag/v1.6.7?cm_mc_uid=02162397679414470795470&cm_mc_sid_50200000=1447951462)에서 사용 가능한 Ruby 버전입니다. 

* 2.0.0
* 2.1.6
* 2.1.7
* 2.2.2
* 2.2.3

앱에서 나열되지 않은 Ruby 버전이 필요한 경우 앱을 배치하려고
외부 [Ruby 빌드팩](https://github.com/cloudfoundry/ruby-buildpack)을
사용할 수 있습니다. 

## 관련 링크
{: #related_links}
* [Ruby용 Cloud Foundry 빌드팩](https://github.com/cloudfoundry/cf-buildpack-ruby)
* [Ruby on Rails 문서](http://rubyonrails.org/documentation/)
