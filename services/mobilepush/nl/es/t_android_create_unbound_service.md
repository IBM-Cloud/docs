---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Creación de un servicio {{site.data.keyword.mobilepushshort}} desenlazado para Android
{: #create_android_unbound}
Última actualización: 11 de enero de 2017
{: .last-updated}

Cree una instancia del servicio {{site.data.keyword.mobilepushshort}}. Puede utilizar la instancia del servicio {{site.data.keyword.mobilepushshort}} sin enlazar ninguna aplicación de fondo.

1. Enlace la instancia del servicio {{site.data.keyword.mobilepushshort}} a una aplicación de Bluemix. Al hacerlo, podrá ver que todos los detalles relacionados con el servicio están almacenados en formato JSON en la variable de entorno VCAP_SERVICES. 

![Enlace de un servicio Notificación push](images/unbound_1.jpg)
 2. Pulse **Enlazar** y elija la instancia del servicio {{site.data.keyword.mobilepushshort}} que desee enlazar. Cuando la aplicación esté enlazada con el servicio {{site.data.keyword.mobilepushshort}}, la información del servicio se almacenará en formato JSON en la variable de entorno VCAP_SERVICES de su aplicación. Por ejemplo: 
```
 	{
    "imfpush_Dev": [
   {
         "name": "myname_sampleUnbound",
         "label": "imfpush_Dev",
         "plan": "Basic",
         "credentials": null
      }
    ]
    }
```
	{: codeblock}
