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

L'environnement d'exécution Ruby dans {{site.data.keyword.Bluemix}} repose sur le pack ruby_buildpack.
Le pack ruby_buildpack fournit un environnement d'exécution complet pour les applis Ruby.
{: shortdesc}

Le pack ruby_buildpack est utilisé si votre appli comporte un fichier Gemfile dans son répertoire racine. Il utilisera alors un programme de mise en bundle pour installer vos dépendances.

## Application de démarrage
{: #starter_application}

{{site.data.keyword.Bluemix}} propose une application de démarrage Ruby.  L'application de démarrage Ruby est une appli Ruby simple qui fournit un modèle que vous pouvez utiliser pour votre appli.
Vous pouvez expérimenter cette application et effectuer des modifications, puis les
envoyer par commande push vers l'environnement {{site.data.keyword.Bluemix}}. Voir [Utilisation des applications de démarrage](/docs/cfapps/starter_app_usage.html) pour obtenir de l'aide.

## Versions d'environnement d'exécution
{: #runtime_versions}

Vous pouvez spécifier la version de Ruby à utiliser par votre application dans le fichier Gemfile de votre application. Exemple :


```
  source 'https://rubygems.org'
  ruby '2.1.7'
  gem 'sinatra', '>= 0'
  gem 'haml', '>= 0'
  gem 'json', '>=0'
```
{: codeblock}

Si aucune version n'est spécifiée, la version 2.2.4 est choisie par défaut.

### Versions disponibles :
{: #available_versions}

Les versions de Ruby suivantes sont disponibles dans le [pack de construction Ruby](https://github.com/cloudfoundry/ruby-buildpack/releases/tag/v1.6.16) qui est installé dans {{site.data.keyword.Bluemix}} :

* 2.1.8
* 2.1.9
* 2.2.3
* 2.2.4
* 2.3.0

Si votre application requiert une version de Ruby qui n'est pas répertoriée, vous pouvez
utiliser le [pack de construction Ruby](https://github.com/cloudfoundry/ruby-buildpack) externe pour la déployer.

# rellinks
{: #rellinks}
## general
{: #general}
* [Cloud Foundry buildpack for Ruby](https://github.com/cloudfoundry/cf-buildpack-ruby)
* Documentation [Ruby on Rails](http://api.rubyonrails.org/)
