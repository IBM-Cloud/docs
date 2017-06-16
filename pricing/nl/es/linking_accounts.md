---



copyright:

  years: 2015, 2017
lastupdated: "2017-04-12"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Cómo enlazar las cuentas de Bluemix y SoftLayer
{: #unifyingaccounts}

Puede enlazar las cuentas de {{site.data.keyword.Bluemix_notm}} y SoftLayer para hacer uso de los recursos combinados. Cuando enlace las cuentas de {{site.data.keyword.Bluemix_notm}} y Softlayer, recibirá una factura única de {{site.data.keyword.Bluemix_notm}}. Si ya tiene una cuenta de {{site.data.keyword.Bluemix_notm}}, la facturación a través de {{site.data.keyword.Bluemix_notm}} para los recursos de SoftLayer será efectiva para el nuevo ciclo de facturación que empieza una vez que se han enlazado las cuentas.

**Importante:** todas las cuentas vinculadas en {{site.data.keyword.Bluemix_notm}} deben ser cuentas Pago según uso. Puede crear una nueva cuenta de Pago según uso, enlazar a una cuenta de Pago según uso existente o enlazar con una cuenta de prueba existente (que deberá entonces actualizar a una cuenta de Pago según uso).   
No puede enlazar a cuentas de {{site.data.keyword.Bluemix_notm}} de suscripción. 

Para enlazar cuentas debe ser un usuario maestro en la cuenta de Softlayer. 

Cuando se enlacen sus cuentas: 

* Debe utilizar las credenciales de ID de IBM para acceder a sus cuentas tanto de SoftLayer como de {{site.data.keyword.Bluemix_notm}}.
* Cualquier descuento existente de SoftLayer se aplicará en cargos de {{site.data.keyword.Bluemix_notm}}.
* Recibirá una factura en dólares de Estados Unidos (USD).
* Puede supervisar el uso de los recursos de {{site.data.keyword.BluSoftlayer}} en la consola de {{site.data.keyword.Bluemix_notm}}.

**Atención: ** una vez haya enlazado las cuentas, no podrá desenlazarlas.   

Como usuario maestro, complete los siguientes pasos para enlazar sus cuentas de {{site.data.keyword.Bluemix_notm}} y SoftLayer: 

 1. Desde {{site.data.keyword.slportal}}, haga clic en **Enlaza a una cuenta {{site.data.keyword.Bluemix_notm}}**.
 2. Lea y acepte las condiciones para enlazar cuentas de SoftLayer y {{site.data.keyword.Bluemix_notm}}.
 3. Cuando se le solicite, proporcione la dirección de correo electrónico asociada con su cuenta de {{site.data.keyword.Bluemix_notm}}. Si no tiene ninguna cuenta de {{site.data.keyword.Bluemix_notm}}, especifique la dirección de correo electrónico que desea utilizar y siga las instrucciones para ser invitado a {{site.data.keyword.Bluemix_notm}} y crear una cuenta.

Después de enlazar sus cuentas, **Ir a {{site.data.keyword.Bluemix_notm}}** estará disponible en la barra de menús de la consola de SoftLayer. Al hacer clic en este enlace, accederá a la página de inicio de sesión de {{site.data.keyword.Bluemix_notm}}.

## Facturación para el uso de {{site.data.keyword.Bluemix_notm}} cuando las cuentas están enlazadas
{: #bill_usage}

Una vez que haya enlazado sus cuentas de facturación de {{site.data.keyword.Bluemix_notm}} y SoftLayer, el siguiente ciclo de facturación se cargará en una única factura de {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

El ciclo de uso de {{site.data.keyword.Bluemix_notm}} se basa en meses naturales, por lo que la cuenta se factura cada mes el día de facturación que se estableció para su acuerdo de cargo. Con SoftLayer, el ciclo de uso empieza al empezar a utilizar SoftLayer, por lo que la facturación es cada mes, el día en el que se registró para la cuenta de SoftLayer. 

Cuando las cuentas estén enlazadas, el uso de {{site.data.keyword.Bluemix_notm}} seguirá midiéndose para el ciclo mensual y dicho uso se facturará en una factura de {{site.data.keyword.Bluemix_notm}}. A partir del día 1 del siguiente mes, los cargos de {{site.data.keyword.Bluemix_notm}} y SoftLayer se combinarán en la factura de {{site.data.keyword.Bluemix_notm}}.

Por ejemplo, si enlazó las cuentas el 16 de abril del 2017, recibirá una factura de Bluemix para su uso de abril. Según cuándo haya enlazado las cuentas, podrá obtener una factura independiente para el uso de SoftLayer. Su uso de mayo para SoftLayer y {{site.data.keyword.Bluemix_notm}} se facturará mediante su cuenta de {{site.data.keyword.Bluemix_notm}}.

![Resumen del enlace de cuentas de Bluemix y SoftLayer](/docs/pricing/BluemixSoftLayerBill.svg)

Una vez que se enlacen las facturas, la factura de {{site.data.keyword.Bluemix_notm}} listará los distintos cargos para cada recurso que haya utilizado. 
