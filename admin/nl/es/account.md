---



copyright:

  years: 2015, 2017
lastupdated: "2017-01-09"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Gestión de la cuenta {{site.data.keyword.Bluemix_notm}}
{: #mngacct}

Vaya al enlace **Cuenta** para establecer notificaciones, ver el uso de cuenta o ver la factura.
{:shortdesc}

## Registro en {{site.data.keyword.Bluemix_notm}}
{: #signup}

Puede registrarse para obtener una cuenta de {{site.data.keyword.Bluemix_notm}} utilizando un ID de IBM existente, creando un nuevo ID de IBM o utilizando un ID federado. Un ID federado es un ID dentro del dominio de una empresa que ha sido registrado con IBM, por lo que el dominio y las credenciales de usuario pueden utilizarse para acceder a aplicaciones web de IBM.  

Es posible utilizar un ID federado para registrarse en {{site.data.keyword.Bluemix_notm}} solo si su empresa ya ha trabajado con IBM para el registro.  El registro del dominio de una empresa con IBM permite que los usuarios puedan iniciar sesión en los productos y servicios de IBM utilizando sus credenciales de usuario de empresa existentes. La autenticación la gestiona el proveedor de identidades de la empresa. Al iniciar sesión en
{{site.data.keyword.Bluemix_notm}} con un ID federado, se le solicita que inicie sesión a través de la página de inicio de sesión de su empresa. Para obtener información sobre la solicitud para registrar el dominio de su empresa u organización con IBM, o para obtener más información sobre el proceso, consulte [Guía de adopción de federación empresarial de ID de IBM ![icono de enlace externo](../icons/launch-glyph.svg)](https://ibm.box.com/v/IBMid-Federation-Guide){: new_window}. Es necesario un patrocinador de IBM, como un abogado de ofertas o un abogado de cliente, al solicitar el registro de ID federados.

| Métodos de inicio de sesión | Detalles |    
|-----------------|---------|
|ID de IBM existente | Si ya tiene un ID de IBM, regístrese en {{site.data.keyword.Bluemix_notm}} con sus credenciales existentes que utilice para otros productos y servicios de IBM. Se le solicitará que especifique un número de teléfono al registrarse. |
|ID de IBM nuevo | Si no aún no tiene un ID de IBM, puede optar por crear uno. El ID de IBM le permite utilizar un nombre de usuario de inicio de sesión para todos los productos y servicios de IBM que utilice, incluyendo {{site.data.keyword.Bluemix_notm}}. Deberá especificar su información personal, incluyendo su nombre y apellido, número de teléfono y contraseña para las nuevas credenciales. Puede utilizar este ID de IBM para iniciar sesión al utilizar otros productos y servicios de IBM.  |
|ID federado | Si la empresa ha solicitado registrar las credenciales de usuario desde el dominio de su empresa con IBM, puede registrarse en {{site.data.keyword.Bluemix_notm}} utilizando las credenciales que ya utilice para el inicio de sesión de su empresa. Se le solicitará que especifique un número de teléfono al registrarse. |
{:caption="Tabla 1. Métodos de inicio de sesión" caption-side="top"}

## Configuración de notificaciones
{: #notifications}

Pulse **Cuenta** &gt; **Notificaciones** para configurar notificaciones de gastos y de cuenta generales. Las notificaciones de gastos están disponibles únicamente para propietarios de cuentas de {{site.data.keyword.Bluemix_notm}} de Pago según uso y Suscripción.

Puede establecer notificaciones de correo electrónico de plataforma para incidencias de
{{site.data.keyword.Bluemix_notm}} y mantenimiento planificado, así como establecer notificaciones de gastos que le avisen cuando la cuenta esté cerca del umbral de gasto que haya especificado. Realice las tareas siguientes para establecer tipos de notificaciones distintos para la cuenta.

### Establecimiento de notificaciones de plataforma

Pulse **Cuenta** &gt; **Notificaciones** &gt; **Plataforma** para establecer notificaciones de correo electrónico para mantenimiento planificado e incidencias de {{site.data.keyword.Bluemix_notm}}. Puede seleccionar o deseleccionar cada opción para habilitar o inhabilitar la notificación por correo electrónico.

<!-- staging only

**Note**: You are always alerted by email about emergencies and pricing changes.

On the **Platform** tab you can also customize notifications for your orgs, spaces, or applications. Complete the following steps to add a customized notification:

<ol>
<li>Select **Add a Notification**.</li>
<li>Use the search field to find the org, application, service, or resource that you want to set a notification for, or expand the item in the pre-populated list.</li>
<li>Select *Email* to set the notification type.</li>
</ol>

staging only end -->

### Establecimiento de notificaciones de gastos
{: #spendingnotifications}

Si es un propietario de cuenta de {{site.data.keyword.Bluemix_notm}} de Pago según uso o Suscripción, puede establecer notificaciones de gasto por correo electrónico. Establezca notificaciones sobre el gasto total de la cuenta, tiempo de ejecución, contenedor y servicio, así como sobre el gasto de servicios individuales, sin incluir los servicios de terceros. Recibe notificaciones al alcanzar el 80%, 90%, y 100% de los umbrales de gasto que especifique. Puede editar cada notificación de gasto en cualquier momento en el que necesite el cambio.

Complete los siguientes pasos para configurar notificaciones por correo electrónico para los límites de gasto:

<ol>
<li>Pulse **Cuenta** &gt; **Notificaciones** &gt; **Gasto**.</li>
<li>Entre un valor numérico para establecer el umbral de gasto para desencadenar una notificación para cada tipo de notificación:<br />
<ul>
<li>Total de cuenta</li>
<li>Total de tiempo de ejecución</li>
<li>Total de servicios</li>
<li>Total de contenedor</li>
<li>Gasto de un servicio específico</li>
</ul>
</li>
<li>Cuando haya terminado, pulse **Guardar**.</li>
</ol>

**Nota**: si tiene una cuenta de prueba, puede actualizarla a una cuenta de Suscripción o Pago según uso para establecer los límites de gasto. Para obtener más información sobre las cuentas Pago según uso y Suscripción, consulte [Cómo se le factura](/docs/pricing/index.html#pay-accounts).

## Visualización de uso
{: #acctusage}

Como propietario de cuenta o gestor de facturación para una organización, puede utilizar la página Panel de control de uso para ver los cargos en tiempo real para los tiempos de ejecución, contenedores, servicios y soporte utilizados cada mes en sus organizaciones. Puede ver el consumo de GB por hora y de servicio de tiempo de ejecución en todas las regiones o seleccionar para ver una región determinada.

Para abrir la página Panel de control de uso, pulse **Cuenta** &gt; *nombre_cuenta* &gt; **Panel de control de uso**. Los gestores de facturación pueden ver los detalles sólo para las organizaciones en las que hay gestores de facturación.

La cuenta se factura al propietario por el uso total en el que han incurrido todas las organizaciones al final de cada ciclo de facturación. Como propietario de cuenta puede filtrar el resumen de uso por región y organización. También puede pulsar un mes concreto para ver el uso para ese mes. Seleccione **Todas las organizaciones** en la lista **organización** para ver el uso para todas las organizaciones de la cuenta.

## Actualización de la información de facturación
{: #account_billing}

Como propietario de cuenta, puede editar, añadir o eliminar información de tarjeta de crédito guardada que está asociada a la cuenta {{site.data.keyword.Bluemix_notm}}. Pulse **Cuenta** &gt; *nombre_cuenta* &gt; **Facturación**.

Si tiene una cuenta de SoftLayer vinculada a su cuenta de {{site.data.keyword.Bluemix_notm}}, consulte [Facturación por el uso de {{site.data.keyword.Bluemix_notm}} cuando las cuentas están vinculadas](/docs/admin/softlayerlink.html#bill_usage) para obtener más información sobre el tipo de facturación.
