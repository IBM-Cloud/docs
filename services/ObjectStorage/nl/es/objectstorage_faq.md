---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# FAQ {: #faq}

Estas preguntas más frecuentes proporcionan respuestas a preguntas comunes sobre el servicio de {{site.data.keyword.objectstorageshort}}.
{: shortdesc}


## ¿Qué cuentas y planes de pago puedo utilizar para {{site.data.keyword.objectstorageshort}}? {: #account-payment}

El servicio de {{site.data.keyword.objectstorageshort}} ofrece dos opciones de planes: Gratuito y Estándar. El [precio](https://www.ibm.com/cloud-computing/bluemix/pricing/) varía en función del plan escogido.

<table>
<caption> Tabla 1. Comparación de los planes Gratuito y Estándar </caption>
  <tr>
    <th> Plan gratuito </th>
    <th> Plan estándar </th>
  </tr>
  <tr>
    <td> Sólo permite que exista una instancia de servicio en una organización {{site.data.keyword.Bluemix_notm}} a la vez </td>
    <td> Instancias de servicio ilimitadas </td>
  </tr>
  <tr>
    <td> Disponible para todo el mundo </td>
    <td> Disponible sólo para las cuentas de pago de {{site.data.keyword.Bluemix_notm}} y los usuarios internos de IBM </td>
  </tr>
  <tr>
    <td> Gratuito </td>
    <td> Pago según uso o suscripción a planes de pago </td>
  </tr>
  <tr>
    <td> Incluye un límite de uso de almacenamiento introductorio de 5 GB </td>
    <td> Almacenamiento ilimitado </td>
  </tr>
</table>

**Atención**: Los usuarios que trabajan con una cuenta de prueba de {{site.data.keyword.Bluemix_notm}} pueden utilizar el plan Gratuito. Una vez que caduque el tiempo de la versión de prueba, la instancia de servicio asociada de {{site.data.keyword.objectstorageshort}} se inhabilitará, lo que significa que no podrá acceder a la cuenta de almacenamiento. Tras un periodo de 30 días, se depurará la cuenta de {{site.data.keyword.Bluemix_notm}} y se suprimirán todos los datos. Para evitar la pérdida de datos, actualice a una [Cuenta de pago de {{site.data.keyword.Bluemix_notm}}](/docs/admin/account.html) lo antes posible.

## ¿Cómo puedo cambiar mi plan? {: #changeplan}  
Las instancias que se crean mediante el plan Beta o Gratuito se pueden actualizar al plan Estándar. La organización asociada debe ser una cuenta de pago de {{site.data.keyword.Bluemix_notm}}. Las cuentas de versión de prueba con instancias de Object Storage no se pueden actualizar al plan Estándar, y las instancias del plan Estándar no se pueden degradar a otros planes. Al actualizar, la instancia de servicio y los datos del cliente se moverán al nuevo plan.

Para actualizar:
1.	En la interfaz de usuario de {{site.data.keyword.objectstorageshort}}, pulse **Plan**.
2.	Seleccione **Estándar** como el plan nuevo y, a continuación, pulse **Guardar**.

También puede [modificar el plan de pago](/docs/pricing/index.html#changing) mediante la interfaz de línea de mandatos.

## ¿Cómo se me cobrará y facturará por mi uso de {{site.data.keyword.objectstorageshort}}? {: #charge-bill}

El servicio {{site.data.keyword.objectstorageshort}} sólo le cobrará por lo que utilice.  No existen cargos ni compromisos para empezar a utilizar el servicio. No se le cargará por las solicitudes de API ni por tráfico de red de datos entrante.

{{site.data.keyword.objectstorageshort}} se factura en función del uso de almacenamiento durante el ciclo de facturación. Esto incluye todos los datos de objetos en contenedores que haya creado dentro de su organización de {{site.data.keyword.Bluemix_notm}}.

Se aplica un cargo de Transferencia de datos salientes siempre que se lean datos desde cualquiera de sus contenedores de objetos a través de la red pública. Todo el ancho de banda que se consume en el ciclo de facturación se factura como Ancho de banda saliente público.

Al final del ciclo de facturación, {{site.data.keyword.Bluemix_notm}} le facturará automáticamente por el uso durante dicho periodo de facturación. Puede ver sus cargos para el período de facturación actual a través de los informes de {{site.data.keyword.Bluemix_notm}}.

## ¿Son mi región de {{site.data.keyword.Bluemix_notm}} y mi región de almacenamiento lo mismo? {: #region}

El servicio de {{site.data.keyword.objectstorageshort}} da soporte a las regiones de almacenamiento Dallas y Londres. Estas regiones de almacenamiento son independientes de la región {{site.data.keyword.Bluemix_notm}}, como por ejemplo EE.UU.-Sur y Reino Unido, en la que se crea la instancia de servicio de {{site.data.keyword.objectstorageshort}}. Si crea una instancia en la región de {{site.data.keyword.Bluemix_notm}} EE.UU.-Sur, puede leer y grabar datos en cualquier región de almacenamiento Dallas o Londres. La región de almacenamiento defaultsbased en la región de {{site.data.keyword.Bluemix_notm}}. Puede conmutar regiones seleccionando otra región en la lista desplegable de la IU.
