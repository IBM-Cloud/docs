---

copyright:
  years: 2014, 2016
---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}


# Cómo empezar con {{site.data.keyword.objectstorageshort}} {: #getting-started-with-object-storage}

*Última actualización: 19 de octubre de 2016*
{: .last-updated}

{{site.data.keyword.objectstoragefull}} proporciona almacenamiento de datos de nube no estructurado. Puede almacenar y acceder al contenido, al igual que crear y conectarse de forma interactiva a las aplicaciones y servicios.
{: shortdesc}

Algunos casos de uso comunes para el servicio de {{site.data.keyword.objectstorageshort}} son:

* Copia de seguridad de datos de volumen desde las instancias
* Utilización de una ubicación intermediaria al transferir grandes cantidades de datos
* Transferencia de datos entre entornos que no están conectados directamente
* Función de repositorio central



{{site.data.keyword.objectstorageshort}} público de {{site.data.keyword.Bluemix_notm}} proporciona acceso a una cuenta Swift {{site.data.keyword.objectstorageshort}} completa para gestionar los datos. El cifrado del lado del proveedor no se proporciona.


1.	Suministre la instancia de servicio desde el catálogo de {{site.data.keyword.Bluemix_notm}}. Configure la instancia y pulse **Crear**. Si al principio ha seleccionado la opción **Dejar sin enlazar** en el campo **App**, aún puede enlazar la instancia de servicio a su aplicación {{site.data.keyword.Bluemix_notm}} más tarde.
2. En el panel de control de la instancia del servicio, cree un contenedor para empezar a almacenar objetos.
3. Añada un archivo al contenedor o grupo desde el menú desplegable **Acciones**.
4. Para probar el acceso a los objetos, pulse **Descargar** y revise el archivo.
5. Cuando esté listo para conectar la instancia a una aplicación, configure las credenciales de servicio y [enlace el servicio](https://new-console.stage1.ng.bluemix.net/docs/services/reqnsi.html#add_service).



# Enlaces relacionados
{: #rellinks}

## Referencia de API
{: #api}
* [OpenStack {{site.data.keyword.objectstorageshort}} (Swift) API v1](http://developer.openstack.org/api-ref-objectstorage-v1.html){: new_window}
* [OpenStack Identity (Keystone) API v3.0](http://developer.openstack.org/api-ref-identity-v3.html){: new_window}

## SDK
{: #sdk}
* [OpenStack Software Development Kits (SDK)](https://wiki.openstack.org/wiki/SDKs){: new_window}

## Guías de aprendizaje y ejemplos
{: #samples}
* [Conexión a IBM {{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}} con Java](https://developer.ibm.com/recipes/tutorials/connecting-to-ibm-object-storage-for-bluemix-with-java/){: new_window}
* [Uso de Python para acceder a su {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.objectstorageshort}}](https://developer.ibm.com/recipes/tutorials/use-python-to-access-your-bluemix-object-storage/){: new_window}
* [Uso de PHP para aprovechar {{site.data.keyword.objectstorageshort}}](https://developer.ibm.com/recipes/tutorials/use-php-to-leverage-object-storage-for-bluemix/){: new_window}

## Tiempos de ejecución compatibles
{: #buildpacks}
* [Liberty for Java](https://www.ng.bluemix.net/docs/runtimes/liberty/index.html){: new_window}
* [SDK for Node.js](https://www.ng.bluemix.net/docs/runtimes/nodejs/index.html){: new_window}
* [Ir](https://www.ng.bluemix.net/docs/runtimes/go/index.html){: new_window}
* [PHP](https://www.ng.bluemix.net/docs/runtimes/php/index.html){: new_window}
* [Python](https://www.ng.bluemix.net/docs/runtimes/python/index.html){: new_window}
* [Ruby](https://www.ng.bluemix.net/docs/runtimes/ruby/index.html){: new_window}
* [Compilaciones de la comunidad](https://www.ng.bluemix.net/docs/starters/byob.html){: new_window}


## Enlaces relacionados
{: #general}
* [Hoja de precios de IBM {{site.data.keyword.Bluemix_notm}}](https://www.ng.bluemix.net/#/pricing){: new_window}
* [Requisitos previos de IBM {{site.data.keyword.Bluemix_notm}}](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
