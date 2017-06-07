---



copyright:

  years: 2016, 2017
lastupdated: "2017-03-17"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Cambiar a IBMid 
Ahora la autenticación en SoftLayer utiliza el IBMid para proporcionar un inicio de sesión único para todo {{site.data.keyword.Bluemix_notm}}. Las cuentas existentes de SoftLayer se están habilitando para poder cambiar a la autenticación mediante IBMid. Un asistente de migración le guiará por este cambio. 
{:shortdesc}

Cuando empiece el proceso de cambiar a un IBMid, siempre podrá cancelar el proceso de cambio antes de finalizarlo. Sin embargo, cada vez que inicie una sesión, se mostrará el indicador para cambiar a un IBMid. Cada cuenta de SoftLayer que piense enlazar a la cuenta de {{site.data.keyword.Bluemix_notm}} debe ser propiedad de un IBMid exclusivo con una dirección de correo electrónico exclusiva.

Para cambiar desde su cuenta de SoftLayer existente a un IBMid, siga los siguientes pasos: 
1. Inicie una sesión en su cuenta de SoftLayer y pulse **Aceptar** cuando se visualice una solicitud para cambiar a un IBMid. 

   Si es un usuario maestro y no ve el indicador para cambiar a un IBMid en el {{site.data.keyword.slportal}}, [póngase en contacto con el equipo de soporte de IBM](/docs/support/index.html#contacting-support) para obtener ayuda. 
  
   Si con anterioridad inició una sesión y pulso **Más tarde** en la solicitud, y desea cambiar a la autenticación de IBMid en la sesión actual, vaya a la página Editar perfil de usuario y pulse **Cambiar a IBMid**.

2. Siga las indicaciones del asistente para crear el IBMid. 

   Especifique una dirección de correo electrónico que no utilice actualmente ningún otro IBMid. Esta dirección de correo electrónico sirve como el nombre de usuario para el nuevo IBMid, y es adónde se envía su código de registro después de que se cree su IBMid. Más tarde podrá actualizar la dirección de correo electrónico asociada al IBMid, pero no podrá cambiar el nombre de usuario. 

3. Cuando reciba el código de registro, pulse en el enlace en el correo electrónico o copie el URL en un navegador y especifique su código de registro. 

   El código de registro es válido durante 7 días y solo se puede utilizar una vez.
  
4. Después de enviar su código de registro, utilice el IBMid para iniciar una sesión en {{site.data.keyword.slportal}}.

   En el indicador de inicio de sesión de la cuenta, vaya a la sección **Inicio de sesión de cuenta de IBMid** y pulse **Iniciar sesión con IBMid**. No utilice los campos el **Nombre de usuario** y **Contraseña** que ha utilizado previamente con su ID de SoftLayer.

Si es un nuevo cliente, se le solicitará su IBMid existente o que cree un nuevo IBMid al crear su pedido.  
  * Para utilizar un IBMid existente, escriba el nombre de usuario o la dirección de correo electrónico del IBMid si es exclusivo (es decir, no compartido con varios IBMid).

  
  * Para crear un nuevo IBMid, escriba una dirección de correo electrónico que no utilice actualmente ningún otro IBMid. Esta dirección de correo electrónico es el nombre de usuario para el IBMid, y es adónde se enviará su código de registro después de que se cree su IBMid. Más tarde podrá actualizar la dirección de correo electrónico asociada al IBMid, pero no podrá cambiar el nombre de usuario.  
  
Para resolver cualquier problema de inicio de sesión con su IBMid, consulte [Resolución de problemas para acceder a Bluemix](/docs/troubleshoot/ts_accessing.html#accessing).

## Habilitación de cuentas de usuario para la autenticación del IBMid
{: #link_accounts_resellers}

En algunos casos, para que un usuario pueda cambiar a un IBMid, el concesionario o distribuidor debe habilitar la cuenta para que utilice la autenticación de IBMid.  

  * Es necesario habilitar la autenticación con el IBMid para cada cuenta de usuario existente a la que desee enlazar una cuenta de Bluemix. A continuación, cada usuario debe completar el proceso de cambiar a un IBMid utilizando el asistente de migración, tal como se describió en la sección anterior. Póngase en contacto con el [soporte de IBM](/docs/support/index.html#contacting-support) para habilitar una cuenta de SoftLayer existente para utilizar la autenticación de IBMid.  
  
  * Para garantizar que las nuevas cuentas de usuario se creen con un IBMid, se debe establecer el atributo `CREATE_NEW_ACCOUNT_WITH_IBMid_AUTHENTICATION` en la cuenta de usuario maestro inmediato. Póngase en contacto con el [soporte de IBM](/docs/support/index.html#contacting-support) o su proveedor para establecer el atributo para sus cuentas.   

## Cómo enlazar cuentas de usuario de IBMid
{: #link_user_accounts}

Después de que sus cuentas de usuario se hayan cambiado a la autenticación de IBMid, los concesionarios y distribuidores pueden enlazar cuentas de SoftLayer y de {{site.data.keyword.Bluemix_notm}} para un uso combinado de los recursos de plataforma e infraestructura. 

**Nota**:
  * El usuario maestro de la cuenta a la que se está enlazando debe tener un IBMid. 
  * Cada cuenta de usuario que enlace a una cuenta de {{site.data.keyword.Bluemix_notm}} debe ser propiedad de un IBMid exclusivo con una dirección de correo electrónico exclusiva. A pesar de que un único IBMid puede poseer varias cuentas de SoftLayer, debe cambiar el usuario maestro para que sea un IBMid exclusivo para cada cuenta. Póngase en contacto con el [equipo de soporte de IBM SoftLayer ![icono de enlace externo](../icons/launch-glyph.svg)](https://knowledgelayer.softlayer.com/topic/support){: new_window} para cambiar el usuario maestro de una cuenta de SoftLayer. 
  * Cuando añada nuevos usuarios a una cuenta enlazada, debe añadirlos tanto a la cuenta de SoftLayer como a la cuenta de {{site.data.keyword.Bluemix_notm}} de forma que puedan acceder a todas las funcionalidades de la consola unificada.  
  
Siga estos pasos para enlazar cada cuenta a una cuenta de {{site.data.keyword.Bluemix_notm}}:
1. Para enlazar a una cuenta de {{site.data.keyword.Bluemix_notm}} existente o para crear una nueva, inicie una sesión en su cuenta de SoftLayer como usuario maestro y pulse el enlace {{site.data.keyword.Bluemix_notm}}. 

   El IBMid que es el usuario maestro de la cuenta de SoftLayer debe ser el propietario de la cuenta {{site.data.keyword.Bluemix_notm}} a la que se va a enlazar.  
   
2. Siga las indicaciones del asistente, incluida la adición de los usuarios de la cuenta de SoftLayer a la cuenta de {{site.data.keyword.Bluemix_notm}}.
3. Después de que haya enlazado la cuenta, informe al usuario final de cada cuenta para que migre a un IBMid siguiendo el procedimiento que se ha descrito en la sección anterior. 

**Recomendación**: Migre únicamente cuentas de usuario final a IBMid. No migre cuentas derivadas, que son cuentas padre de cuentas de usuario final y no contienen recursos. Los usuarios de cuentas derivadas que migren a un IBMid pierden la posibilidad de iniciar una sesión en el Brand Agent Portal (BAP).   
  
