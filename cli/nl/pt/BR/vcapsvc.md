---



copyright:

  years: 2015，2017

lastupdated: "2016-03-15"


---

{:shortdesc: .shortdesc}

# Serviços VCAP


A variável de ambiente VCAP_SERVICES é um objeto JSON
que contém informações que podem ser usadas para interagir com uma instância de serviço
no {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}


## Recuperando o valor da variável de ambiente VCAP_SERVICES
{:retrieving}

A variável de ambiente VCAP_SERVICES é um objeto JSON
que contém informações que podem ser usadas para interagir com uma instância de serviço
no {{site.data.keyword.Bluemix_notm}}. As informações incluem o nome da instância de serviço, a credencial e a URL de conexão com a instância de serviço. Esses valores são preenchidos na variável de ambiente VCAP_SERVICES quando o seu aplicativo está ligado a uma instância de serviço no {{site.data.keyword.Bluemix_notm}}.

O valor da variável de ambiente VCAP_SERVICES está disponível somente ao ligar uma instância de serviço a seu aplicativo. É possível visualizar as variáveis do ambiente de aplicativos usando o comando a seguir:
```
cf env APP_NAME
```
