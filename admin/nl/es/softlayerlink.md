---

 

copyright:

  years: 2016

 

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

<!-- draft - staging only -->

#Enlace de las cuentas de facturación de SoftLayer y {{site.data.keyword.Bluemix_notm}}
{: #softlayerlink}
*Última actualización: 10 de junio de 2016*
{: .last-updated}

Ahora es posible enlazar las cuentas de facturación de SoftLayer y {{site.data.keyword.Bluemix_notm}}. Cuando se enlazan las cuentas, la facturación se realiza a través de SoftLayer tanto para los recursos de SoftLayer como para los de {{site.data.keyword.Bluemix_notm}}. Si ya tiene una cuenta, la facturación de {{site.data.keyword.Bluemix_notm}} a través de SoftLayer será efectiva para el nuevo ciclo de facturación que empiece después de haber enlazado las cuentas.
{:shortdesc}

**Importante:** todas las cuentas vinculadas en {{site.data.keyword.Bluemix_notm}} deben ser cuentas Pago según uso. Se puede crear una cuenta Pago según uso nueva o enlazar con una cuenta existente de este tipo. También puede enlazar una cuenta de prueba, pero se actualizará a una cuenta Pago según uso.   

Una vez que las cuentas estén enlazadas, podrá supervisar el uso de sus recursos {{site.data.keyword.Bluemix_notm}} en la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}. Sin embargo, el la facturación por estos recursos ahora aparecerá en la factura de SoftLayer.

Aunque la cuenta de facturación se enlazará y podrá cambiar entre las cuentas fácilmente, deberá seguir teniendo ID separados para {{site.data.keyword.Bluemix_notm}} y SoftLayer. Siga utilizando su ID de SoftLayer para productos y servicios de SoftLayer y utilice su ID de IBM para productos y servicios de {{site.data.keyword.Bluemix_notm}}. 

**Atención:** una vez que las cuentas estén enlazadas, no podrá desenlazarlas.   

Si tiene una cuenta SoftLayer, y desea enlazar cuentas de SoftLayer y {{site.data.keyword.Bluemix_notm}}, siga estos pasos: 
 1. Desde {{site.data.keyword.slportal}}, haga clic en **Enlaza a una cuenta {{site.data.keyword.Bluemix_notm}}**. 
 2. Lea y acepte las condiciones para enlazar cuentas de SoftLayer y {{site.data.keyword.Bluemix_notm}}. 
 3. Cuando se le solicite, proporcione la dirección de correo electrónico asociada con su cuenta de {{site.data.keyword.Bluemix_notm}}. Si no tiene ninguna cuenta de {{site.data.keyword.Bluemix_notm}}, especifique l a dirección de correo electrónico que desea utilizar y siga las instrucciones para ser invitado a {{site.data.keyword.Bluemix_notm}} y crear una cuenta. 

Debe ser usuario maestro en la cuenta de SoftLayer para enlazar cuentas. 

Después de enlazar las cuentas, la opción **Ir a {{site.data.keyword.Bluemix_notm}}** aparece disponible en la cabecera global de SoftLayer. Al hacer clic en este enlace, accederá a la página de inicio de sesión de {{site.data.keyword.Bluemix_notm}}. Además, **SoftLayer** estará disponible en la cabecera de {{site.data.keyword.Bluemix_notm}}. Al hacer clic en este enlace, accederá a la página de inicio de {{site.data.keyword.slportal}} en una nueva ventana. 


## Uso de créditos para {{site.data.keyword.Bluemix_notm}} cuando las cuentas están enlazadas
{: #slcredit}

Al enlazar las cuentas de facturación de {{site.data.keyword.Bluemix_notm}} y SoftLayer, recibirá un crédito de 200 $ para utilizarlos en {{site.data.keyword.Bluemix_notm}}. El crédito debe utilizarse en el plazo de 30 días después de enlazar las cuentas. 

Para obtener información sobre cómo ver los créditos y la fecha de caducidad, consulte [Ver créditos](https://console.ng.bluemix.net/docs/pricing/index.html#credits).

## Invitación a miembros del equipo de SoftLayer a {{site.data.keyword.Bluemix_notm}}
{: #invite_users}

Puede invitar a los miembros de su equipo de SoftLayer para que se unan a {{site.data.keyword.Bluemix_notm}} al enlazar las cuentas de {{site.data.keyword.Bluemix_notm}} y SoftLayer. También puede invitar a los miembros del equipo de SoftLayer desde la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

Desde la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}, puede invitar a todos los miembros de su cuenta de SoftLayer o bien seleccionar solo a determinados miembros. Al invitar a miembros del equipo, debe establecer el rol de la cuenta de {{site.data.keyword.Bluemix_notm}} para los invitados. Para obtener más información sobre los distintos roles en {{site.data.keyword.Bluemix_notm}}, consulte [Roles de usuario](https://console.ng.bluemix.net/docs/admin/users_roles.html#userrolesinfo).

Debe ser usuario maestro en la cuenta de SoftLayer para invitar a miembros a la cuenta de {{site.data.keyword.Bluemix_notm}}. 

Para invitar a miembros a través de {{site.data.keyword.Bluemix_notm}}:
 1. Vaya al icono **Cuenta y soporte** ![Cuenta y soporte ](images/account_support.svg) > **Cuentas** > **Invitar a miembros**.
 2. Pulse **Añadir** para autenticarse en la cuenta de SoftLayer y ver una lista de los miembros del equipo de su cuenta de SoftLayer. 
 3. Seleccione a los miembros del equipo que desee invitar y pulse **Enviar**.

Puede hacer esta operación las veces que sea necesario a medida que se añaden más miembros a su cuenta de SoftLayer. 
 
El miembro del equipo recibe un correo electrónico que incluye un enlace **Únase a la organización**. Si el miembro no tiene ID de IBM, se le redirige a una página de registro. A continuación, el miembro puede entrar información básica y crear su cuenta de {{site.data.keyword.Bluemix_notm}}.

Para obtener más información sobre cómo invitar a miembros a través de la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}, consulte [Invitar a miembros del equipo](https://console.ng.bluemix.net/docs/admin/users_roles.html#inviteteammembers).

## Utilización de servicios de {{site.data.keyword.Bluemix_notm}} con activos de SoftLayer
{: #bluemix_services}

Puede utilizar servicios de {{site.data.keyword.Bluemix_notm}} públicos basados en API con sus activos de SoftLayer. Todas las API son seguras y están cifradas para proteger sus datos.
{:shortdesc}

Por ejemplo, ¿ha querido alguna vez añadir capacidades cognitivas de Watson a sus aplicaciones que se ejecutan en servidores nativos desde SoftLayer? Puede añadir un servicio como {{site.data.keyword.personalityinsightsshort}} para entender el usuario de la aplicación en cuatro pasos sencillos: 

1. Busque el servicio en el catálogo de {{site.data.keyword.Bluemix_notm}}.
2. Especifique una instancia del servicio con tan solo una pulsaciones. 
3. Configure el servicio para que se ejecute con el código existente copiando las credenciales del servicio y añadiéndolas a la aplicación. 
4. Después de actualizar la aplicación, despliegue la nueva versión en la infraestructura de SoftLayer. 

Puede obtener conocimientos sobre *Insights and Cognitive* invocando las API de Watson desde sus aplicaciones en SoftLayer para personalizarlas. O bien puede utilizar servicios de *Datos y análisis* para realizar un análisis más profundo del rendimiento para sus aplicaciones. Asimismo, puede seleccionar una base de datos como servicio cuando deje la gestión en manos de {{site.data.keyword.Bluemix_notm}}.

Modernice el desarrollo de sus aplicaciones utilizando contenedores con servicios como {{site.data.keyword.activedeployshort}} y {{site.data.keyword.deliverypipeline}}. Luego puede utilizar el servicio {{site.data.keyword.vpn_short}} para regresar de nuevo a SoftLayer y conectar su contenedor de una red privada a la red privada de SoftLayer. Todos los cargos por uso de los recursos y servicios de cálculo se reflejan en la factura de SoftLayer. 

### Servicios de {{site.data.keyword.Bluemix_notm}} basados en API
No todos los servicios de {{site.data.keyword.Bluemix_notm}} pueden utilizarse con SoftLayer. Los siguientes servicios se pueden configurar para ejecutarse con el código de la aplicación:
* {{site.data.keyword.alchemyapishort}}
* {{site.data.keyword.alertnotificationshort}}
* {{site.data.keyword.sparks}}
* {{site.data.keyword.appseccloudshort}}
* {{site.data.keyword.blockchain}}
* {{site.data.keyword.cloudant}}
* {{site.data.keyword.conceptinsightsshort}}
* {{site.data.keyword.iotmapinsights_short}}
* {{site.data.keyword.dashdbshort}}
* {{site.data.keyword.dialogshort}}
* {{site.data.keyword.documentconversionshort}}
* {{site.data.keyword.twittershort}}
* {{site.data.keyword.weather_short}}
* {{site.data.keyword.iotdriverinsights_short}}
* {{site.data.keyword.geospatialshort_Geospatial}}
* {{site.data.keyword.graphshort}}
* {{site.data.keyword.iotelectronics}}
* {{site.data.keyword.languagetranslationshort}}
* {{site.data.keyword.messagehub}}
* {{site.data.keyword.mqa}}
* {{site.data.keyword.mobileappbuilder_short}}
* {{site.data.keyword.mql}}
* {{site.data.keyword.nlclassifierlshort}}
* {{site.data.keyword.objectstorageshort}}
* {{site.data.keyword.personalityinsightsshort}}
* {{site.data.keyword.presenceinsightsshort}}
* {{site.data.keyword.relationshipextractionshort}}
* {{site.data.keyword.retrieveandrankshort}}
* {{site.data.keyword.servicediscoveryshort}}
* {{site.data.keyword.speechtotextshort}}
* {{site.data.keyword.sqldb}}
* {{site.data.keyword.streaminganalyticsshort}}
* {{site.data.keyword.texttospeechshort}}
* {{site.data.keyword.toneanalyzershort}}
* {{site.data.keyword.tradeoffanalyticsshort}}
* {{site.data.keyword.visualinsightsshort}}
* {{site.data.keyword.visualrecognitionshort}}
* {{site.data.keyword.workflow}}
* {{site.data.keyword.workloadscheduler}}

**Nota:** no todos los planes de estos servicios están disponibles. Para utilizar con las cuentas enlazadas, solo están disponibles los planes habilitados para cuentas Pago según uso. Sin embargo, puede utilizar cualquier plan para cualquiera de estos servicios si tiene una cuenta de {{site.data.keyword.Bluemix_notm}} independiente que se factura por separado. 


## Facturación para el uso de {{site.data.keyword.Bluemix_notm}} cunado las cuentas están enlazadas
{: #bill_usage}

Una vez que haya enlazado sus cuentas de facturación de {{site.data.keyword.Bluemix_notm}} y SoftLayer, el siguiente ciclo de facturación se cargará en una única factura de SoftLayer.
{:shortdesc}

El ciclo de uso de {{site.data.keyword.Bluemix_notm}} se basa en meses naturales, por lo que la cuenta se factura el primer día de cada mes. Con SoftLayer, el ciclo de uso empieza al empezar a utilizar SoftLayer, por lo que la facturación es cada mes, el día en el que se registró para la cuenta de SoftLayer. 

Cuando las cuentas estén enlazadas, el uso de {{site.data.keyword.Bluemix_notm}} seguirá midiéndose para el ciclo mensual y dicho uso se facturará en una factura de {{site.data.keyword.Bluemix_notm}}. A partir del día 1 del siguiente mes, los cargos de {{site.data.keyword.Bluemix_notm}} se incluirán en la factura de SoftLayer.

Por ejemplo, si enlazó las cuentas el 16 de abril, recibirá una factura de Bluemix para su uso de abril. El uso de mayo se facturará a través de la cuenta de SoftLayer.

![Resumen del enlace de cuentas de Bluemix y SoftLayer](images/BluemixSoftLayerBill.svg)

Una vez que haya combinado las cuentas de facturación, la cuenta de SoftLayer tendrá una sección de **{{site.data.keyword.Bluemix_notm}}** en la factura de resumen. En la vista de facturación detallada, los cargos de {{site.data.keyword.Bluemix_notm}} se mostrarán como otros servicios y empezarán con "Plan de *"{{site.data.keyword.Bluemix_notm}}..."*.

Para obtener información sobre cómo ver el uso de {{site.data.keyword.Bluemix_notm}}, consulte [Visualización de detalles de uso](https://console.ng.bluemix.net/docs/pricing/index.html#usage).


# rellinks
## general
* [Vídeo: Enlazar cuenta de SoftLayer y Bluemix para una única factura](https://www.youtube.com/watch?v=Xb01idt2NiU&index=1&list=PLzpeuWUENMK2d3L5qCITo2GQEt-7r0oqm)
