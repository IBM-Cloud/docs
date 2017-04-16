---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-14"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Ruby
{: #ruby_runtime}

Die Laufzeit von Ruby in {{site.data.keyword.Bluemix}} basiert auf dem Buildpack 'ruby_buildpack'.
Das Buildpack 'ruby_buildpack' bietet eine vollständige Laufzeitumgebung für Ruby-Apps.
{: shortdesc}

Das Buildpack 'ruby_buildpack' wird verwendet, wenn im Stammverzeichnis Ihrer App das Element 'Gemfile' enthalten ist. Es wird zum Installieren Ihrer Abhängigkeiten anschließend Bundler verwendet.

## Starteranwendung
{: #starter_application}

{{site.data.keyword.Bluemix}} stellt eine Ruby-Starteranwendung bereit.  Die Ruby-Starteranwendung ist eine einfache Ruby-App, die Sie als Schablone für Ihre App verwenden können. Sie können mit der Starter-App experimentieren, Änderungen an der {{site.data.keyword.Bluemix}}-Umgebung vornehmen und diese mit einer Push-Operation übertragen.  Hilfe zur Verwendung der Starteranwendung finden Sie in [Starteranwendungen verwenden](/docs/cfapps/starter_app_usage.html).

## Laufzeitversionen
{: #runtime_versions}

Sie können die Version von Ruby, die von Ihrer App verwendet werden soll, im Element 'Gemfile' Ihrer Anwendung angeben. Beispiel:


```
  source 'https://rubygems.org'
  ruby '2.1.7'
  gem 'sinatra', '>= 0'
  gem 'haml', '>= 0'
  gem 'json', '>=0'
```
{: codeblock}

Wenn keine Version angegeben ist, wird standardmäßig Version 2.2.4 ausgewählt.

### Verfügbare Versionen:
{: #available_versions}

Folgende Ruby-Versionen stehen im [Ruby-Buildpack](https://github.com/cloudfoundry/ruby-buildpack/releases/tag/v1.6.16) zur Verfügung, das zurzeit in {{site.data.keyword.Bluemix}} installiert ist:

* 2.1.8
* 2.1.9
* 2.2.3
* 2.2.4
* 2.3.0

Wenn für Ihre App eine Ruby-Version erforderlich ist, die nicht aufgelistet ist, können Sie die App mit dem externen [Ruby-Buildpack](https://github.com/cloudfoundry/ruby-buildpack) implementieren.

# Zugehörige Links
{: #rellinks}
## Allgemein
{: #general}
* [Cloud Foundry-Buildpack für Ruby](https://github.com/cloudfoundry/cf-buildpack-ruby)
* [Dokumentation zu Ruby on Rails](http://api.rubyonrails.org/)
