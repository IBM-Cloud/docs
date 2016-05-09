---

 

copyright:

  years: 2015 2016

 

---

{:shortdesc: .shortdesc}

# Servicios VCAP

*Última actualización: 15 de marzo de 2016*


La variable de entorno VCAP_SERVICES es un objeto JSON que contiene
información que puede utilizar para interactuar con una instancia de servicio en
{{site.data.keyword.Bluemix_notm}}.
{:shortdesc}


## Recuperación del valor de la variable de entorno VCAP_SERVICES
{:retrieving}

La variable de entorno VCAP_SERVICES es un objeto JSON que contiene
información que puede utilizar para interactuar con una instancia de servicio en
{{site.data.keyword.Bluemix_notm}}. La información incluye el nombre de instancia de servicio, la credencial y el URL de conexión a la instancia de servicio. Estos valores se llenan en la variable de entorno VCAP_SERVICES cuando se enlaza la aplicación a una instancia de servicio en {{site.data.keyword.Bluemix_notm}}.

El valor de la variable de entorno VCAP_SERVICES está disponible solo cuando se enlaza una instancia de servicio a la aplicación. Puede visualizar las variables de entorno de la aplicación mediante el mandato siguiente:
```
cf env APP_NAME
```
