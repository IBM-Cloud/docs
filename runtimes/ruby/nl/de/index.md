{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

*Letzte Aktualisierung: 12. Januar 2016*

# Ruby-Laufzeit
{: #ruby_runtime}

Die Ruby-Laufzeit unter {{site.data.keyword.Bluemix}} basiert auf dem Ruby-Buildpack (ruby_buildpack).
Das Ruby-Buildpack (ruby_buildpack) stellt eine vollständige Laufzeitumgebung für die
Ruby-App bereit.
{: shortdesc}

Das Ruby-Buildpack wird verwendet, wenn Ihre App im Stammverzeichnis eine GEM-Datei enthält. Für die Installation Ihrer Abhängigkeiten wird dann der Bundler verwendet.

## Starteranwendung
{: #starter_application}

{{site.data.keyword.Bluemix}} stellt eine Ruby-Starteranwendung zur Verfügung.  Die Ruby-Starteranwendung ist eine einfache Ruby-App, die eine Vorlage bereitstellt, die Sie für Ihre App nutzen können. Sie können die Starter-App ausprobieren und Änderungen vornehmen und diese dann per Push-Operation an die {{site.data.keyword.Bluemix}}-Umgebung übertragen.  Hilfeinformationen zur Verwendung der Starteranwendung finden Sie im Thema zur [Verwendung der Starteranwendungen](../../cfapps/starter_app_usage.html).

## Laufzeitversionen
{: #runtime_versions}

Sie können die Version von Ruby, mit der Ihre App arbeiten soll, in der GEM-Datei Ihrer Anwendung angeben; Beispiel:


```
  source 'https://rubygems.org'
  ruby '2.1.7'
  gem 'sinatra', '>= 0'
  gem 'haml', '>= 0'
  gem 'json', '>=0'
```
{: codeblock}

Wird keine Version angegeben, wird Version 2.2.2 standardmäßig ausgewählt.

### Verfügbare Versionen:
{: #available_versions}

Im derzeit in {{site.data.keyword.Bluemix}} installierten
[Ruby-Buildpack](https://github.com/cloudfoundry/ruby-buildpack/releases/tag/v1.6.7?cm_mc_uid=02162397679414470795470&cm_mc_sid_50200000=1447951462)
sind die folgenden Ruby-Versionen verfügbar:

* 2.0.0
* 2.1.6
* 2.1.7
* 2.2.2
* 2.2.3

Wenn für Ihre App eine Ruby-Version erforderlich ist, die
nicht aufgeführt ist, können Sie das externe
[Ruby-Bildpack](https://github.com/cloudfoundry/ruby-buildpack) für
die Bereitstellung der App verwenden.

## ZUGEHÖRIGE LINKS
{: #related_links}
* [Cloud Foundry-Buildpack für Ruby](https://github.com/cloudfoundry/cf-buildpack-ruby)
* [Dokumentation zu Ruby on Rails](http://rubyonrails.org/documentation/)
