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

El tiempo de ejecución de Ruby en {{site.data.keyword.Bluemix}} está basado en el ruby_buildpack.
El ruby_buildpack proporciona un entorno de ejecución completo para apps Ruby.
{: shortdesc}

El ruby_buildpack se utiliza si la app tiene un Gemfile en el directorio raíz. A continuación, utilizará Bundler para instalar las dependencias.

## Aplicación de inicio
{: #starter_application}

{{site.data.keyword.Bluemix}} proporciona una aplicación de inicio Ruby.  La aplicación de inicio Ruby es una sencilla app Ruby que ofrece una plantilla que puede utilizar para su app. Puede experimentar con la app de iniciador, y realizar y enviar por push cambios en el entorno de {{site.data.keyword.Bluemix}}.  Consulte [Utilización de las aplicaciones de inicio](/docs/cfapps/starter_app_usage.html) para obtener ayuda con el uso de la aplicación de inicio.

## Versiones de tiempo de ejecución
{: #runtime_versions}

Puede especificar la versión de Ruby que utilizará la app en el Gemfile de la aplicación, por ejemplo:


```
  source 'https://rubygems.org'
  ruby '2.1.7'
  gem 'sinatra', '>= 0'
  gem 'haml', '>= 0'
  gem 'json', '>=0'
```
{: codeblock}

Cuando no se especifique una versión, se elegirá la versión 2.2.4 de forma predeterminada.

### Versiones disponibles:
{: #available_versions}

Las siguientes versiones de Ruby están disponibles en el
[paquete de compilación de Ruby](https://github.com/cloudfoundry/ruby-buildpack/releases/tag/v1.6.16)
actualmente instalado en {{site.data.keyword.Bluemix}}:

* 2.1.8
* 2.1.9
* 2.2.3
* 2.2.4
* 2.3.0

Si la app requiere una versión de Ruby que no aparece en la lista,
puede utilizar el
[paquete de compilación de Ruby](https://github.com/cloudfoundry/ruby-buildpack) externo para
desplegar la app.

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [Paquete de compilación de Cloud Foundry para Ruby](https://github.com/cloudfoundry/cf-buildpack-ruby)
* [Documentación de Ruby on Rails ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://api.rubyonrails.org/)
