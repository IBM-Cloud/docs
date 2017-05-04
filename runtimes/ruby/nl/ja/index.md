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

{{site.data.keyword.Bluemix}} の Ruby ランタイムには ruby_buildpack が採用されています。
ruby_buildpack は、Ruby アプリケーションのための完全なランタイム環境を提供します。
{: shortdesc}

ruby_buildpack は、アプリケーションのルート・ディレクトリーに Gemfile がある場合に使用されます。続いて、Bundler を使用して依存関係がインストールされます。

## スターター・アプリケーション
{: #starter_application}

{{site.data.keyword.Bluemix}} には、Ruby スターター・アプリケーションが用意されています。Ruby スターター・アプリケーションは、アプリケーションで使用可能なテンプレートを提供する、シンプルな Ruby アプリケーションです。スターター・アプリケーションを試し、{{site.data.keyword.Bluemix}} 環境に対して変更を行い、プッシュすることができます。スターター・アプリケーションの使用に関するヘルプについては、[『スターター・アプリケーションの使用』](/docs/cfapps/starter_app_usage.html)を参照してください。

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

バージョンを指定しない場合は、デフォルトでバージョン 2.2.4 が選択されます。

### 使用可能なバージョン:
{: #available_versions}

現在 {{site.data.keyword.Bluemix}} にインストールされている [Ruby ビルドパック](https://github.com/cloudfoundry/ruby-buildpack/releases/tag/v1.6.16)では、以下のバージョンの Ruby が使用できます。

* 2.1.8
* 2.1.9
* 2.2.3
* 2.2.4
* 2.3.0

アプリケーションが、リストされていないバージョンの Ruby を必要とする場合は、外部の [Ruby ビルドパック](https://github.com/cloudfoundry/ruby-buildpack)を使用してアプリケーションをデプロイできます。

# 関連リンク
{: #rellinks notoc}
## 一般
{: #general notoc}
* [Cloud Foundry buildpack for Ruby, Sinatra and Rails](https://github.com/cloudfoundry/cf-buildpack-ruby)
* [Ruby on Rails の資料 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://api.rubyonrails.org/)
