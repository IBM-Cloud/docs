---

 

copyright:

  years: 2016
lastupdated: "2016-09-09"
 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Implementación de canales de información
{: #openwhisk_feeds}

OpenWhisk da soporte a una API abierta, donde cualquier usuario puede exponer un servicio productor de sucesos como un **canal de información** en un **paquete**.   En esta sección se describen las opciones de arquitectura e implementación para proporcionar canales de información propios.

Este material está pensado para usuarios avanzados de OpenWhisk que deseen publicar sus propios canales de información.  La mayoría de los usuarios de OpenWhisk pueden omitir esta sección.

## Arquitectura de canal de información

Existen al menos 3 patrones de arquitectura para crear un canal de información: **Ganchos**, **Sondeo** y **Conexiones**.

### Ganchos
En el patrón *Ganchos*, se configura un canal de información utilizando un recurso [webhook](https://en.wikipedia.org/wiki/Webhook) expuesto por otro servicio.   En esta estrategia, se configura un webhook en un servicio externo para PUBLICAR directamente en un URL y activar un desencadenante.  Esta es, sin duda, la opción más fácil y atractiva para implementar canales de información de baja frecuencia.

### Sondeo
En el patrón "Sondeo", se organiza una *acción* de OpenWhisk para sondear un punto final periódicamente y obtener datos nuevos.
La creación de este patrón es relativamente fácil, pero la frecuencia de los sucesos estará limitada, como es lógico, por el intervalo de sondeo.

### Conexiones
En el patrón "Conexiones", se configura un servicio independiente en algún lugar para mantener una conexión persistente con una fuente de canal de información.    La implementación basada en conexión puede interactuar con un punto final de servicio mediante un sondeo largo o configurar una notificación push.


## Diferencia entre el canal de información y el desencadenante

Los canales de información y los desencadenantes están muy relacionados, pero técnicamente son conceptos distintos.   

- OpenWhisk procesa **sucesos** que fluyen en el sistema.

- Un **desencadenante** es el nombre técnico de una clase de suceso.   Cada suceso pertenece exactamente a un desencadenante; por analogía, un desencadenante parece un *tema* de un sistema pub/sub basado en temas.    Una **regla** *T -> A* significa que "cuando llega un evento desde el desencadenante *T*, se invoca la acción *A* con la carga útil del desencadenante.

- Un **canal de información** es una corriente de sucesos que pertenecen a un desencadenante *T*.    Un canal de información se controla mediante una **acción de canal de información** que gestiona la creación, supresión, pausa y reanudación de la corriente de sucesos que forman el canal de información.    La acción de canal de información suele interactuar con los servicios externos que producen los sucesos, mediante la API REST que gestiona las notificaciones.

##  Implementación de acciones de canal de información

La *acción de canal de información* es una *acción* de OpenWhisk normal, pero debe aceptar los siguientes parámetros:
* **lifecycleEvent**: uno de 'CREATE', 'DELETE', 'PAUSE' o 'UNPAUSE'
* **triggerName**: el nombre completo del desencadenante que contiene los eventos producidos desde este canal de información.
* **authKey**: las credenciales de autenticación básicas del usuario de OpenWhisk propietario del desencadenante que se acaba de mencionar

La acción de canal de información también puede aceptar otros parámetros necesarios para gestionar el canal de información.  Por ejemplo, la acción de canal de información de los cambios de cloudant espera recibir parámetros que incluyan *'dbname'*, *'username'*, etc.

Cuando el usuario crea un desencadenante desde la CLI con el parámetro **--feed**, el sistema invoca automáticamente la acción de canal de información con los parámetros apropiados.

Por ejemplo, supongamos que el usuario ha creado un enlace de `mycloudant` para el paquete `cloudant` con el nombre de usuario y la contraseña como parámetros de enlace.  Cuando el usuario emita el siguiente mandato desde la CLI,

`wsk trigger create T --feed mycloudant/changes -p dbName myTable`

entonces el sistema realizará una acción parecida a la siguiente:

`wsk action invoke mycloudant/changes -p lifecycleEvent CREATE -p triggerName T -p authKey <userAuthKey> -p password <password value from mycloudant binding> -p username <username value from mycloudant binding> -p dbName mytype`

La acción de canal de información llamada *cambios* obtiene estos parámetros y se espera que realice las acciones necesarias para configurar una secuencia de sucesos desde Cloudant, con la configuración adecuada, dirigida al desencadenante *T*.    

Para el canal de información *cambios* de Cloudant, la acción se pone en contacto directamente con un servicio *desencadenante de cloudant* implementado con una arquitectura basada en conexión.   A continuación, se abordan las otras arquitecturas.

Se produce un protocolo de acción de canal de información similar para `wsk trigger delete`.    

## Implementación de canales de información con ganchos

Es fácil configurar un canal de información mediante un gancho si el productor del suceso admite un recurso webhook/callback.

Con este método *no es necesario* configurar ningún servicio persistente fuera de OpenWhisk.  Toda la gestión de canales de información se produce de forma natural a través de las *acciones de canal de información* de OpenWhisk, que negocian directamente con una API webhook de terceros.

Al invocarse con el mandato `CREATE`, la acción del canal de información simplemente instala un webhook para otro servicio, solicitando al servicio remoto que PUBLIQUE notificaciones en el URL de `fireTrigger` pertinente en OpenWhisk.

El webhook debería dirigirse para enviar notificaciones a un URL como:

`POST /namespaces/{namespace}/triggers/{triggerName}`

El formulario con la solicitud POST se interpretará como un documento JSON que define los parámetros en el suceso desencadenante.
Las reglas de OpenWhisk pasan los parámetros del desencadenante a las acciones para activarlas como resultado del suceso.

## Implementación de canales de información con sondeo

Es posible configurar una *acción* de OpenWhisk para sondear un origen de canal de información completamente dentro de OpenWhisk, sin necesidad de configurar conexiones persistentes o servicios externos.

Para los canales de información que no disponen de webhook, pero no necesitan un volumen elevado ni tiempos de respuesta de latencia bajos, el sondeo es una opción atractiva.

Para configurar un canal de información basado en sondeos, la acción de canal de información sigue los siguientes pasos cuando se llama al mandato `CREATE`:

1.   La acción de canal de información configura un desencadenante periódico (*T*) con la frecuencia deseada, utilizando el canal de información `whisk.system/alarms`.
2.   El desarrollador del canal de información crea una acción `pollMyService` que simplemente sondea el servicio remoto y devuelve los sucesos nuevos.
3.  La acción de canal de información configura una *regla* *T -> pollMyService*.

Este procedimiento implementa un desencadenante basado en sondeo utilizando únicamente acciones de OpenWhisk, sin necesidad de un servicio independiente.

## Implementación de canales de información mediante Conexiones

Las 2 opciones de arquitectura anteriores son fáciles y rápidas de implementar. Sin embargo, si desea un canal de información de alto rendimiento, no existe ningún sustituto para conexiones persistentes, sondeo largo o técnicas similares.

Puesto que las acciones de OpenWhisk deben ser de ejecución corta, una acción no puede mantener una conexión persistente con un tercero. En lugar de eso, se debe configurar un servicio independiente (fuera de OpenWhisk) que se ejecute continuamente.   Este servicio se denomina *servicio de proveedor*.  Un servicio de proveedor puede mantener conexiones con orígenes de sucesos de terceros que soporten el sondeo largo u otras notificaciones basadas en conexiones.   
El servicio de proveedor debe proporcionar una API REST que permita a la *acción de canal de información* controlar el canal de información.   El servicio de proveedor actúa como un proxy entre el proveedor de suceso y OpenWhisk (cuando recibe sucesos de un tercero, los envía a OpenWhisk activando un desencadenante).

El canal *cambios* de Cloudant es el ejemplo canónico (configura un servicio `cloudanttrigger` que media entre las notificaciones de Cloudant a través de una conexión persistente y desencadenantes de OpenWhisk).

El canal de información *alarma* se implementa con un patrón parecido.

La arquitectura basada en conexión es la opción de rendimiento más alto, pero impone más sobrecarga en las operaciones en comparación con las arquitecturas de sondeo y gancho.   
