---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Ruby
{: #ruby_runtime}
*最終更新日時: 2016 年 3 月 16 日*

{{site.data.keyword.Bluemix}} の Ruby ランタイムには ruby_buildpack が採用されています。
ruby_buildpack は、Ruby アプリケーションのための完全なランタイム環境を提供します。
{: shortdesc}

ruby_buildpack は、アプリケーションのルート・ディレクトリーに Gemfile がある場合に使用されます。続いて、Bundler を使用して依存関係がインストールされます。

## スターター・アプリケーション
{: #starter_application}

{{site.data.keyword.Bluemix}} には、Ruby スターター・アプリケーションが用意されています。Ruby スターター・アプリケーションは、アプリケーションで使用可能なテンプレートを提供する、シンプルな Ruby アプリケーションです。スターター・アプリケーションを試し、{{site.data.keyword.Bluemix}} 環境に対して変更を行い、プッシュすることができます。スターター・アプリケーションの使用に関するヘルプについては、[『スターター・アプリケーションの使用』](../../cfapps/starter_app_usage.html)を参照してください。

## ランタイム・バージョン
{: #runtime_versions}

アプリケーションで使用する Ruby のバージョンは、以下の例のように、アプリケーションの Gemfile で指定できます。


```
  source 'https://rubygems.org'
  ruby '2.1.7'
  gem 'sinatra', '>= 0'
  gem 'haml', '>= 0'
  gem 'json', '>=0'
```
{: codeblock}

バージョンを指定しない場合は、デフォルトでバージョン 2.2.2 が選択されます。

### 使用可能なバージョン:
{: #available_versions}

現在 {{site.data.keyword.Bluemix}} にインストールされている [Ruby ビルドパック](https://github.com/cloudfoundry/ruby-buildpack/releases/tag/v1.6.7?cm_mc_uid=02162397679414470795470&cm_mc_sid_50200000=1447951462)では、以下のバージョンの Ruby が使用できます。

* 2.0.0
* 2.1.6
* 2.1.7
* 2.2.2
* 2.2.3

アプリケーションが、リストされていないバージョンの Ruby を必要とする場合は、外部の [Ruby ビルドパック](https://github.com/cloudfoundry/ruby-buildpack)を使用してアプリケーションをデプロイできます。

# 関連リンク
## 一般
* [Cloud Foundry buildpack for Ruby, Sinatra and Rails](https://github.com/cloudfoundry/cf-buildpack-ruby)
* [Ruby on Rails の資料](http://rubyonrails.org/documentation/)
