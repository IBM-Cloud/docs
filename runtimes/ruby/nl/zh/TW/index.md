{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

*前次更新：2016 年 1 月 12 日*

# Ruby 執行時期
{: #ruby_runtime}

{{site.data.keyword.Bluemix}} 上的 Ruby 執行時期採用 ruby_buildpack 技術。
ruby_buildpack 提供 Ruby 應用程式的完整執行時期環境。
{: shortdesc}

如果應用程式的根目錄中有 Gemfile，則會使用 ruby_buildpack。接著會使用「連結器」來安裝相依關係。

## 入門範本應用程式
{: #starter_application}

{{site.data.keyword.Bluemix}} 提供 Ruby 入門範本應用程式。Ruby 入門範本應用程式是一種簡單 Ruby 應用程式，提供可用於應用程式的範本。您可以實驗入門範本應用程式，以及變更 {{site.data.keyword.Bluemix}} 環境，並將變更推入其中。如需使用入門範本應用程式的說明，請參閱[使用入門範本應用程式](../../cfapps/starter_app_usage.html)。

## 執行時期版本
{: #runtime_versions}

您可以在應用程式的 Gemfile 中指定應用程式要使用的 Ruby 版本，例如：


```
  source 'https://rubygems.org'
  ruby '2.1.7'
  gem 'sinatra', '>= 0'
gem 'haml', '>= 0'
gem 'json', '>=0'```
{: codeblock}

未指定版本時，依預設會選擇 2.2.2 版。

### 可用的版本：
{: #available_versions}

目前安裝於 {{site.data.keyword.Bluemix}} 的 [Ruby 建置套件](https://github.com/cloudfoundry/ruby-buildpack/releases/tag/v1.6.7?cm_mc_uid=02162397679414470795470&cm_mc_sid_50200000=1447951462)提供下列 Ruby 版本：

* 2.0.0
* 2.1.6
* 2.1.7
* 2.2.2
* 2.2.3

如果您的應用程式需要未列出的 Ruby 版本，可以使用外部 [Ruby 建置套件](https://github.com/cloudfoundry/ruby-buildpack)來部署應用程式。

## 相關鏈結
{: #related_links}
* [Cloud Foundry for Ruby 建置套件](https://github.com/cloudfoundry/cf-buildpack-ruby)
* [Ruby on Rails 文件](http://rubyonrails.org/documentation/)
