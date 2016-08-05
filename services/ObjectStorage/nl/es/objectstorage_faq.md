{:new_window: target="_blank"}

# FAQ {: #faq} 

*Última actualización: 18 de julio de 2016*
{: .last-updated}


## ¿Cómo varían los precios en función del plan que escoja? {: #plan-price}
El precio varía en función del plan escogido. Para ver más información sobre precios, consulte la [Hoja de precios de IBM Bluemix](https://console.ng.bluemix.net/pricing/){: new_window} o utilice la [Calculadora](https://console.ng.bluemix.net/?direct=classic/#/pricing/cloudOEPaneId=pricing&paneId=pricingSheet){: new_window} para realizar estimaciones más detalladas.


## ¿Qué cuentas y planes de pago puedo utilizar para {{site.data.keyword.objectstorageshort}}? {: #account-payment}
El servicio de {{site.data.keyword.objectstorageshort}} viene con varias opciones de planes. A partir de nuestro release de disponibilidad general, se ofrecen dos planes en este momento: Estándar y Gratuito. El plan Estándar sólo está disponible para las cuentas pagadas de {{site.data.keyword.Bluemix_notm}}, ya sean Pago según uso o Suscripción, y para usuarios internos de IBM. El plan Estándar incluye una Concesión de crédito gratuita de 5 GB introductoria en el uso de almacenamiento por cuenta.

Las cuentas de prueba que aún están activas podrán utilizar el plan Gratuito, que permite existir sólo una instancia en una Organización de {{site.data.keyword.Bluemix_notm}}. Una vez que caduque el tiempo en la versión de prueba de {{site.data.keyword.Bluemix_notm}}, se inhabilitará la instancia de servicio de {{site.data.keyword.objectstorageshort}} asociada, lo que significa que no se puede acceder a la cuenta de almacenamiento mediante la interfaz de usuario ni mediante la línea de mandatos de {{site.data.keyword.Bluemix_notm}}. Tras un periodo de gracia de 30 días, se depurará la cuenta de {{site.data.keyword.Bluemix_notm}}, y se suprimirán todos los datos. Para evitar la pérdida de datos, se recomienda actualizar a una cuenta de pago de {{site.data.keyword.Bluemix_notm}} lo antes posible. Para actualizar la cuenta, pulse en el menú de gestión de usuarios y seleccione **Cuenta**, que proporciona instrucciones sobre el proceso de actualización.

## ¿Cómo puedo cambiar mi plan? {: #changeplan}  
Las instancias que se crean mediante el plan Beta o Gratuito se pueden actualizar al plan Estándar. La organización asociada debe ser una cuenta de pago de {{site.data.keyword.Bluemix_notm}}. Las cuentas de versión de prueba con instancias de {{site.data.keyword.objectstorageshort}} no se pueden actualizar al plan Estándar, y las instancias del plan Estándar no se pueden degradar a otros planes. Al actualizar, la instancia de servicio y los datos del cliente se moverán al nuevo plan.

Para actualizar el plan:
1.	En la interfaz de usuario de {{site.data.keyword.objectstorageshort}}, pulse **Plan**.
2.	Seleccione **Estándar** como el plan nuevo y, a continuación, pulse **Guardar**.

También puede modificar el plan de pago mediante la interfaz de línea de mandatos. Para obtener más información, consulte [Cómo cambiar el plan](../../pricing/index.html#changing).


## ¿Cómo se me cobrará y facturará por mi uso de {{site.data.keyword.objectstorageshort}}? {: #charge-bill}

El servicio {{site.data.keyword.objectstorageshort}} sólo le cobrará por lo que utilice.  No existe tarifa mínima, cargos de configuración ni compromisos para empezar a utilizar el servicio. No hay ningún cargo por solicitud de API ni por tráfico de red de datos entrante.

Su uso de {{site.data.keyword.objectstorageshort}} se factura en función del uso de almacenamiento durante el ciclo de facturación. Esto incluye todos los datos de objetos en contenedores que haya creado bajo su cuenta de organización de {{site.data.keyword.Bluemix_notm}}. 

Se aplica un cargo de Transferencia de datos salientes siempre que se lean datos desde cualquiera de sus contenedores de objetos a través de la red pública. El Ancho de banda saliente público se factura para todo el ancho de banda consumido en el ciclo de facturación.

Los componentes de la métrica de los precios de {{site.data.keyword.objectstorageshort}} son los siguientes:
* Uso de almacenamiento - 0,04 $ por GB al mes
* Transferencia de datos salientes pública - 0,09 por GB al mes 

Al final del ciclo de facturación, {{site.data.keyword.Bluemix_notm}} le facturará automáticamente por el uso correspondiente al período de facturación actual. Puede ver sus cambios para el período de facturación actual a través de los informes de {{site.data.keyword.Bluemix_notm}}.

El plan de servicio estándar publicado para Londres y Dallas tiene los mismos precios.

## ¿Cómo se efectúa la réplica de datos en {{site.data.keyword.objectstorageshort}}? {: #replication}
El servicio de {{site.data.keyword.objectstorageshort}} conserva tres copias de sus datos, que se replican a través de múltiples nodos de almacenamiento. Para obtener más información, consulte el documento [OpenStack Swift Replication](http://docs.openstack.org/developer/swift/overview_replication.html){: new_window}.

