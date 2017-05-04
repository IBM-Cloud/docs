---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Ruby
{: #ruby_runtime}

{{site.data.keyword.Bluemix}}의 Ruby 런타임은 ruby_buildpack을 통해 제공됩니다.
ruby_buildpack은 Ruby 앱을 위한 완전한 런타임 환경을 제공합니다.
{: shortdesc}

ruby_buildpack은 앱의 루트 디렉토리에 Gemfile이 있는 경우 사용됩니다. 이는 Bundler를 사용하여 사용자 종속 항목을 설치합니다. 

## 스타터 애플리케이션
{: #starter_application}

{{site.data.keyword.Bluemix}}는 Ruby 스타터 애플리케이션을 제공합니다. Ruby 스타터 애플리케이션은 앱에 사용할 수 있는 템플리트를 제공하는 단순한 Ruby 앱입니다. 스타터 앱을 사용하여 시험해 볼 수 있으며 {{site.data.keyword.Bluemix}} 환경을 변경하고 변경사항을 푸시할 수
있습니다. 스타터 애플리케이션 사용에 대한 도움말은 [스타터 애플리케이션 사용](/docs/cfapps/starter_app_usage.html)을 참조하십시오. 

## 런타임 버전
{: #runtime_versions}

애플리케이션의 Gemfile에서 앱이 사용할 Ruby 버전을 지정할 수 있습니다, 


```
  source 'https://rubygems.org'
  ruby '2.1.7'
  gem 'sinatra', '>= 0'
  gem 'haml', '>= 0'
  gem 'json', '>=0'
```
{: codeblock}

버전이 지정되지 않은 경우 기본적으로 버전 2.2.4가 선택됩니다.

### 사용 가능한 버전: 
{: #available_versions}

다음 Ruby 버전은 현재
{{site.data.keyword.Bluemix}}에 설치된 [Ruby 빌드팩](https://github.com/cloudfoundry/ruby-buildpack/releases/tag/v1.6.16)에서
사용 가능합니다. 

* 2.1.8
* 2.1.9
* 2.2.3
* 2.2.4
* 2.3.0

나열되지 않은 Ruby 버전이 애플리케이션에 필요한 경우
외부
[Ruby 빌드팩](https://github.com/cloudfoundry/ruby-buildpack)을
사용하여 애플리케이션을 배치할 수 있습니다. 

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [Ruby에 대한 Cloud Foundry 빌드팩](https://github.com/cloudfoundry/cf-buildpack-ruby)
* [Ruby on Rails 문서 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://api.rubyonrails.org/)
