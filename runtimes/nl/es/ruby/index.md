{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

*Última actualización: 12 de enero de 2016*

# Tiempo de ejecución de Ruby
{: #ruby_runtime}

El tiempo de ejecución de Ruby en {{site.data.keyword.Bluemix}} está basado en ruby_buildpack.
ruby_buildpack proporciona un entorno de tiempo de ejecución completo para la app de Ruby.
{: shortdesc}

ruby_buildpack se utiliza si la app tiene un Gemfile en el directorio raíz. A continuación, utilizará Bundler para instalar las dependencias.

## Aplicación de inicio
{: #starter_application}

{{site.data.keyword.Bluemix}} proporciona una aplicación de inicio de Ruby. La aplicación de inicio de Ruby es una app de Ruby simple que proporciona una plantilla que puede utilizar para la app. Puede experimentar con la app de iniciador, y realizar y enviar por push cambios en el entorno de {{site.data.keyword.Bluemix}}. Consulte [Utilización de las aplicaciones de iniciador](../../cfapps/starter_app_usage.html) para obtener ayuda con la utilización de la aplicación de inicio.

## Versiones de tiempo de ejecución
{: #runtime_versions}

Puede especificar la versión de Ruby que utilizará la app en el Gemfile de la aplicación, por ejemplo:


```
  source 'https://rubygems.org'
  ruby '2.1.7'
  gem 'sinatra', '>= 0'
gem 'haml', '>= 0'
gem 'json', '>=0'```
{: codeblock}

Cuando no se especifica la versión, se escoge la versión 2.2.2 de forma predeterminada.

### Versiones disponibles:
{: #available_versions}

Las siguientes versiones de Ruby están disponibles en el
[Paquete de compilación de Ruby](https://github.com/cloudfoundry/ruby-buildpack/releases/tag/v1.6.7?cm_mc_uid=02162397679414470795470&cm_mc_sid_50200000=1447951462)
instalado actualmente en {{site.data.keyword.Bluemix}}:

* 2.0.0
* 2.1.6
* 2.1.7
* 2.2.2
* 2.2.3

Si la app requiere una versión de Ruby que no aparece en la lista,
puede utilizar el
[paquete de compilación de Ruby](https://github.com/cloudfoundry/ruby-buildpack) externo para
desplegar la app.

## ENLACES RELACIONADOS
{: #related_links}
* [Paquete de compilación de Cloud Foundry para Ruby](https://github.com/cloudfoundry/cf-buildpack-ruby)
* [Documentación de Ruby on Rails](http://rubyonrails.org/documentation/)
