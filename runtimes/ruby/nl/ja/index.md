{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

*最終更新日: 2016 年 1 月 12 日*

# Ruby ランタイム
{: #ruby_runtime}

{{site.data.keyword.Bluemix}} の Ruby ランタイムでは、ruby_buildpack が採用されています。
ruby_buildpack は、Ruby アプリのための完全なランタイム環境を提供します。
{: shortdesc}

ruby_buildpack は、アプリのルート・ディレクトリーに Gemfile がある場合に使用されます。その後、Bundler を使用して依存関係がインストールされます。

## スターター・アプリケーション
{: #starter_application}

{{site.data.keyword.Bluemix}} は Ruby スターター・アプリケーションを提供します。Ruby スターター・アプリケーションは、ご使用のアプリに使用できるテンプレートを提供するシンプルな Ruby アプリです。このスターター・アプリを試し、{{site.data.keyword.Bluemix}} 環境に変更を加えてプッシュすることができます。スターター・アプリケーションの使用に関するヘルプについては、[「スターター・アプリケーションの使用 (Using the starter applications)」](../../cfapps/starter_app_usage.html)を参照してください。

## ランタイム・バージョン
{: #runtime_versions}

アプリケーションの Gemfile で、アプリで使用する Ruby のバージョンを指定できます。例えば、次のとおりです。


```
  source 'https://rubygems.org'
  ruby '2.1.7'
  gem 'sinatra', '>= 0'
gem 'haml', '>= 0'
gem 'json', '>=0'```
{: codeblock}

バージョンが指定されていない場合、デフォルトでバージョン 2.2.2 が選択されます。

### 使用可能なバージョン:
{: #available_versions}

{{site.data.keyword.Bluemix}} に現在インストールされている [Ruby ビルドパック](https://github.com/cloudfoundry/ruby-buildpack/releases/tag/v1.6.7?cm_mc_uid=02162397679414470795470&cm_mc_sid_50200000=1447951462)では、以下の Ruby のバージョンを使用できます。

* 2.0.0
* 2.1.6
* 2.1.7
* 2.2.2
* 2.2.3

ご使用のアプリが必要とする Ruby のバージョンがリストにない場合は、
外部の [Ruby ビルドパック](https://github.com/cloudfoundry/ruby-buildpack)を使用して、アプリをデプロイできます。

## 関連リンク
{: #related_links}
* [Ruby 用 Cloud Foundry ビルドパック](https://github.com/cloudfoundry/cf-buildpack-ruby)
* [Ruby on Rails 資料](http://rubyonrails.org/documentation/)
