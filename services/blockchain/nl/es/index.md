---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Cómo empezar con IBM {{site.data.keyword.blockchain}}
{: #gettingstartedtemplate}
Última actualización: 10 de noviembre de 2016
{: .last-updated}

**ATENCIÓN:** Antes de utilizar el plan Desarrollador inicial (Beta) o el plan Red empresarial de alta seguridad (GA), debe leer la información técnica y de soporte en [Información que necesita saber](needtoknow.html).
<br><br>

## Oferta de estado de planes

El plan Desarrollador inicial es un release Beta, y proporciona un entorno de desarrollo multiarrendatario. El plan Red empresarial de alta seguridad es una release GA. El plan Red empresarial de alta seguridad proporciona un entorno de LinuxONE en z de un solo arrendatario altamente seguro, con el aislamiento de código utilizando [IBM Secure Service Container](etn_ssc.html).
<br><br>

## IBM Blockchain en Bluemix

El servicio {{site.data.keyword.blockchainfull}} en Bluemix&reg; ofrece una opción entre dos redes blockchain de desarrollo y prueba de cuatro nodos, con la pulsación de un botón. En lugar de crear una red de blockchain a partir de cero, los desarrolladores puede empezar inmediatamente a escribir aplicaciones y desplegar código de encadenamiento. El servicio de IBM Blockchain en Bluemix es una red autorizada de igual a igual, que se crea encima del código [Hyperledger Fabric v0.6.1](https://github.com/hyperledger/fabric/tree/v0.6) desde Hyperledger Project de Linux Foundation.
{:shortdesc}

Las redes de blockchain se utilizan para intercambiar y realizar el seguimiento de forma segura y eficiente de los activos digitales, y registrar permanentemente todas las transacciones en el libro mayor compartido. Para obtener más información sobre blockchain, consulte el tema [Acerca de blockchain](ibmblockchain_overview.html).
<br><br>

## Eligir el plan de red

Tiene la opción entre dos planes de IBM Blockchain en Bluemix: la **Red de desarrollador inicial ** o **Red empresarial de alta seguridad**. Utilice el gráfico de comparación para elegir el entorno adecuado para usted.

<!-- Commenting our for move to GA status jh 10/07/16
![](images/red_alert.png)  **The High Security Business Network** plan is a limited Beta offering; to select this plan, you must first request preapproval at [IBM Blockchain on IBM Bluemix](http://www-stage.watson.ibm.com/files/blockchain/bluemix.html). -->

| Plan Bluemix:      | Red de desarrollador inicial       | Red empresarial de alta seguridad
| ------------------------- |:--------------------------:|:-----:|
| Estado:    | Beta     | GA |
| Finalidad:  |  Desarrollar y probar niveles de seguridad, rendimiento y disponibilidad |  Simular una red de empresa y probar niveles de seguridad, rendimiento y disponibilidad |
| Nodos:    | 4 nodos + Entidad emisora de certificados     | 4 nodos + Entidad emisora de certificados |
| [Supervisor del panel de control:](ibmblockchainmonitor.html) | Sí | Sí |
| Transacciones confidenciales: | Sí | Sí |
| [Consenso:](etn_pbft.html) | PBFT | PBFT |
| Entorno:     | Multiarrendatario compartido | Único arrendatario aislado |
| [IBM Secure Service Container:](etn_ssc.html) | No | Sí |

<br>
## Iniciar el plan de red

Siga estos pasos para crear y desarrollar una instancia de servicio desenlazado de la red de blockchain.  La red incluye un entorno de desarrollo con nodos de validación y un servicio de seguridad, y le permite desplegar código de encadenamiento, ver registros y crear aplicaciones:

1. En la página [Servicio de {{site.data.keyword.blockchain}}](https://console.ng.bluemix.net/catalog/services/blockchain/), rellene el formulario **Añadir servicio** en el panel de la derecha:
  - **Espacio:** Seleccione **dev**.
  - **App:** Seleccione **Dejar sin enlazar**, o enlace el servicio con una de las aplicaciones de Bluemix.org, **Seleccione una aplicación**.
  - **Nombre de servicio:** Escriba un nombre o valor exclusivo, como por ejemplo, **Blockchain Test Net123**.
  - **Nombre de credencial:** Deje el valor predeterminado.
  - **Plan seleccionado:** Elija **Desarrollador inicial** o **Alta seguridad**.
  - Pulse el botón **CREAR**.
2.  Ahora está en la pantalla **Panel de control de servicio** para el nuevo servicio. Desde aquí, puede **Gestionar** la instancia de la red; pulse **INICIAR** para el supervisor de blockchain.
3.  El supervisor de blockchain visualiza detalles de red, registros en tiempo real, estado de libro mayor actual, las API y plantillas de código de encadenamiento. Utilice el panel de control para cualquiera de las siguientes funciones:
  - Descubrimiento de acceso y rutas de API para iguales de red.
  - Ver todos los contenedores de código de encadenamiento en ejecución.
  - Ver registros en tiempo real y resolver problemas del código de encadenamiento.
  - Ver el escenario mundial para el libro mayor.
  - Acceder a la interfaz de usuario de Swagger e interactuar con la red mediante la API REST.
  - Desplegar uno de los tres ejemplos de código de encadenamiento.


# Enlaces relacionados
{: #rellinks}
## Guías de aprendizaje y ejemplos
{: #samples}
* [IBM Marbles Demo (GitHub)](https://github.com/IBM-Blockchain/marbles)
* [IBM Commercial Paper Demo (GitHub)](https://github.com/IBM-Blockchain/cp-web#readme)
* [IBM Car Lease Demo (Github)](https://github.com/IBM-Blockchain/car-lease-demo/blob/master/README.md)
* [Art Auction Demo (Github)](https://github.com/ITPeople-Blockchain/auction)

## Referencia de la API
{: #api}
* [Interfaz de usuario de Swagger](https://obc-service-broker-staging.stage1.mybluemix.net/swagger)
* [API de Hyperledger Fabric (GitHub)](https://github.com/hyperledger/fabric/tree/v0.6/docs/API)
* [SDK para Node.js de HFC](https://github.com/hyperledger/fabric/tree/v0.6/sdk/node)

## Enlaces relacionados
{: #general}
* [Código de Fabric](https://github.com/hyperledger/fabric)
* [Libro blanco](https://github.com/hyperledger/hyperledger/wiki/Whitepaper-WG)
* [Especificación de protocolo y documentos relacionados](https://github.com/hyperledger/fabric/tree/v0.6/docs)
* [StackOverflow](http://stackoverflow.com/questions/tagged/hyperledger)
* [Linux Foundation](https://www.hyperledger.org/)
* [Novedades de Servicios de Bluemix](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){:new_window}


<!--
[Bluemix Pricing Sheet](https://console.ng.bluemix.net/pricing/)
[IBM Bluemix Prerequisites](https://developer.ibm.com/bluemix/support/#prereqs) -->
