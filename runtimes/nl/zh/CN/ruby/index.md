---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Ruby
{: #ruby_runtime}
*上次更新时间：2016 年 3 月 16 日*

{{site.data.keyword.Bluemix}} 上的 Ruby 运行时由 ruby_buildpack 提供支持。ruby_buildpack 为 Ruby 应用程序提供了完整的运行时环境。
{: shortdesc}

如果您应用程序的根目录中包含 Gemfile，那么将使用 ruby_buildpack。然后，它将使用 Bundler 来安装依赖项。

## 入门模板应用程序
{: #starter_application}

{{site.data.keyword.Bluemix}} 提供了 Ruby 入门模板应用程序。Ruby 入门模板应用程序是一个简单的 Ruby 应用程序，它提供了一个可供您的应用程序使用的模板。您可以尝试使用该入门模板应用程序来进行更改并将更改推送到 {{site.data.keyword.Bluemix}} 环境。有关使用入门模板应用程序的帮助，请参阅[使用入门模板应用程序](../../cfapps/starter_app_usage.html)。

## 运行时版本
{: #runtime_versions}

您可以在您应用程序的 Gemfile 文件中为您的应用程序指定要使用的 Ruby 版本，例如：


```
  source 'https://rubygems.org'
  ruby '2.1.7'
  gem 'sinatra', '>= 0'
gem 'haml', '>= 0'
gem 'json', '>=0'```
{: codeblock}

如果未指定版本，缺省情况下会选择 V2.2.2。

### 可用版本：
{: #available_versions}

{{site.data.keyword.Bluemix}} 中当前安装的 [Ruby buildpack](https://github.com/cloudfoundry/ruby-buildpack/releases/tag/v1.6.7?cm_mc_uid=02162397679414470795470&cm_mc_sid_50200000=1447951462) 内提供了以下 Ruby 版本：

* 2.0.0
* 2.1.6
* 2.1.7
* 2.2.2
* 2.2.3

如果您应用程序所需的 Ruby 版本没有列在上述列表中，那么可以使用外部 [Ruby buildpack](https://github.com/cloudfoundry/ruby-buildpack) 来部署应用程序。

# 相关链接
## 常规
* [用于 Ruby 的 Cloud Foundry buildpack](https://github.com/cloudfoundry/cf-buildpack-ruby)
* [Ruby on Rails 文档](http://rubyonrails.org/documentation/)
