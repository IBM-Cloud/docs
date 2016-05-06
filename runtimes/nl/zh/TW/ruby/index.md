---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Ruby
{: #ruby_runtime}
*前次更新：2016 年 3 月 16 日*

{{site.data.keyword.Bluemix}} 上的 Ruby 執行時期是採用 ruby_buildpack 技術。
ruby_buildpack 為 Ruby 應用程式提供完整的執行時期環境。
{: shortdesc}

如果您應用程式的根目錄含有 Gemfile，則會使用 ruby_buildpack。然後，它將使用「連結器」來安裝您的相依關係。

## 入門範本應用程式
{: #starter_application}

{{site.data.keyword.Bluemix}} 提供 Ruby 入門範本應用程式。Ruby 入門範本應用程式是簡單的 Ruby 應用程式，提供可以讓您用於應用程式的範本。您可以用入門範本應用程式進行實驗，並進行及推送對 {{site.data.keyword.Bluemix}} 環境的變更。如需關於使用入門範本應用程式的協助，請參閱[使用入門範本應用程式](../../cfapps/starter_app_usage.html)。

## 執行時期版本
{: #runtime_versions}

您可以在應用程式的 Gemfile 中指定應用程式要使用的 Ruby 版本，例如：


```
  source 'https://rubygems.org'
  ruby '2.1.7'
  gem 'sinatra', '>= 0'
  gem 'haml', '>= 0'
  gem 'json', '>=0'
```
{: codeblock}

如果未指定版本，依預設會選擇 2.2.2 版。

### 可用的版本：
{: #available_versions}

目前安裝在 {{site.data.keyword.Bluemix}} 中的 [Ruby 建置套件](https://github.com/cloudfoundry/ruby-buildpack/releases/tag/v1.6.7?cm_mc_uid=02162397679414470795470&cm_mc_sid_50200000=1447951462)提供下列 Ruby 版本：

* 2.0.0
* 2.1.6
* 2.1.7
* 2.2.2
* 2.2.3

如果您的應用程式需要未列出的 Ruby 版本，您可以使用外部 [Ruby 建置套件](https://github.com/cloudfoundry/ruby-buildpack)來部署該應用程式。

# 相關鏈結
## 一般
* [Cloud Foundry buildpack for Ruby, Sinatra and Rails](https://github.com/cloudfoundry/cf-buildpack-ruby)
* [Ruby on Rails 文件](http://rubyonrails.org/documentation/)
