---

copyright:
  years: 2016,2017
lastupdated: "2017-04-27"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Iniciación a Compose for etcd
{: #getting-started-with-compose-for-etcd}

etcd es un almacén de valor de claves que aloja los datos siempre correctos que necesita para coordinar y gestionar el clúster del servidor para la gestión de configuración de servidor distribuida. etcd utiliza el algoritmo de consenso RAFT para asegurar la coherencia de datos del clúster. Fuerza el orden en el que tienen lugar las operaciones en los datos, por lo que cada nodo del clúster llega al mismo resultado de la misma forma. {{site.data.keyword.composeForEtcd_full}} añade copias de seguridad automáticas de los datos de configuración almacenados en etcd. Una interfaz administrativa intuitiva le permite supervisar, escalar y administrar el despliegue con facilidad.
{:shortdesc}

**Nota:** Cualquier instancia de servicio de Compose proporcionada antes del 14 de septiembre de 2016 que siga activa se puede seguir utilizando y se puede acceder a ella directamente en [https://www.compose.com/](https://www.compose.com). Se puede acceder directamente a cualquier instancia de servicio de Compose que se proporcione desde este momento en adelante y se utilizará dentro de la cuenta de Bluemix.

Siga estos pasos para iniciarse a {{site.data.keyword.composeForEtcd}}.

1. [Cree una instancia de {{site.data.keyword.composeForEtcd}}](https://console.ng.bluemix.net/catalog/services/compose-for-etcd/).

  Al crear una instancia del servicio, asegúrese de que elige un nombre para el servicio y un nombre de credencial. Deje el servicio desenlazado; puede conectar una aplicación al servicio más adelante utilizando las credenciales proporcionadas cuando se proporcione el servicio. Los distintos valores de credenciales se listan en la sección *Credenciales disponibles*.

2. Conéctese al servicio de {{site.data.keyword.composeForEtcd}}.

Para conectar una app al servicio, utilice las [credenciales](./credentials.html) creadas junto con el servicio. La app de ejemplo muestra cómo utilizar Node.js para conectar a un servicio de {{site.data.keyword.composeForEtcd}}.

Descargue la app de ejemplo [compose-etcd-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-etcd-helloworld-nodejs) y siga las instrucciones del archivo readme. A continuación, en la página de detalles de la aplicación en Bluemix, pulse **Ver APP** para ver el contenido de *ejemplos*.
