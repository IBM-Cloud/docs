---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-16"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Integración de OpenWhisk con Serverless Framework
{: #openwhisk_goserverless}

[Serverless Framework](https://serverless.com/) es una infraestructura de código abierto para crear aplicaciones sin servidor. Utilizando un sencillo archivo de manifiesto, los desarrolladores pueden definir funciones sin servidor, conectarlas a orígenes de sucesos y declarar los servicios de nube necesarios por su aplicación. La infraestructura gestiona el despliegue de estas aplicaciones sin servidor en los proveedores de la nube. También permite a los desarrolladores supervisar los servicios en un entorno de producción, desplegar actualizaciones y ayudar a casos de depuración de problemas. También ofrece un interesante ecosistema de plugins de otros proveedores para ampliar la funcionalidad de la infraestructura. Aquí es donde interviene OpenWhisk. 
{:shortdesc}

OpenWhisk tiene [su propio plugin de proveedor para Serverless Framework](https://github.com/serverless/serverless-openwhisk). Los desarrolladores que utilizan Serverless Framework puede elegir desplegar sus aplicaciones a cualquier instancia de la plataforma OpenWhisk (alojada en Bluemix, en otra nube o privada). El soporte multiproveedor también significa que mover aplicaciones entre las diferentes plataformas es mucho más sencillo y los desarrolladores pueden desarrollar aplicaciones sin servidor para varias nubes.

## Cómo empezar
{: #openwhisk_goserverless_starting}

Esta es la [Guía de iniciación a OpenWhisk](https://serverless.com/framework/docs/providers/openwhisk/guide/intro/) oficial de Serverless Framework - cubre la instalación, flujo de trabajo de desarrollo, prácticas recomendadas, guía paso a paso para crear y desplegar una aplicación OpenWhisk en funcionamiento y más temas.

En [este vídeo](https://youtu.be/GJY10W98Itc) se explica cómo utilizar Serverless Framework con el plugin de proveedor de OpenWhisk.
## Documentación
{: #openwhisk_goserverless_docs}

[Aquí encontrará](https://serverless.com/framework/docs/providers/openwhisk/) documentación actualizada sobre cómo utilizar OpenWhisk con Serverless Framework.
## Ejemplos
{: #openwhisk_goserverless_samples}
[Repositorio GitHub de ejemplos de Serverless Framework](https://github.com/serverless/examples) contiene ejemplos de OpenWhisk que muestran cómo crear API HTTP, planificadores, funciones de encadenamiento y más.
