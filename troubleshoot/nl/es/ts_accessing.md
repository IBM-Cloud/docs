---

copyright:
  years: 2015, 2017
  
lastupdated: "2017-01-11"

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 



# Resolución de problemas de acceso a {{site.data.keyword.Bluemix_notm}} 
{: #accessing}


Algunos de los problemas generales de acceso a {{site.data.keyword.Bluemix}} pueden ser que un usuario no pueda iniciar una sesión en {{site.data.keyword.Bluemix_notm}}, que una cuenta se haya bloqueado en estado pendiente, etc. Sin embargo, en muchos de los casos, puede solucionar estos problemas siguiendo unos sencillos pasos. 
{:shortdesc}

## No se puede iniciar la sesión en {{site.data.keyword.Bluemix_notm}}
{: #ts_unabletologin}

Debe tener una cuenta válida de {{site.data.keyword.Bluemix_notm}} para iniciar sesión.


Cuando intente iniciar sesión en {{site.data.keyword.Bluemix_notm}}, verá uno de los siguientes mensajes de error: 
{: tsSymptoms} 

 * Desde el Portal de cliente
  
   `Ha llegado a esta página porque la autenticación ha sido satisfactoria; sin embargo, este ID de IBM no está asociado con ninguna cuenta de IBM Cloud. Si cree que esto es un error, póngase en contacto con el Propietario de la cuenta o el Usuario maestro.`

 * Desde la consola de {{site.data.keyword.Bluemix_notm}}
  
  `Ha llegado a esta página porque la autenticación ha sido satisfactoria; sin embargo, este ID de IBM no está asociado a ninguna cuenta de {{site.data.keyword.Bluemix_notm}}.`


Uno de los motivos más probables por los que ha obtenido este mensaje de error es que aún no tiene creada ninguna cuenta de {{site.data.keyword.Bluemix_notm}} o tiene que conmutar a la autenticación del ID de IBM. 
{: tsCauses} 
 

Siga el proceso de registro para crear una cuenta de {{site.data.keyword.Bluemix_notm}} o póngase en contacto con el usuario maestro o con el administrador de la cuenta para cambiar al ID de IBM. 
{: tsResolve}

En función de cómo se haya configurado su cuenta, se podrán aplicar algunas de estas opciones de inicio de sesión: 
 * Los usuarios de SoftLayer con ID de SoftLayer deben iniciar sesión a través del [Portal de cliente ![icono de enlace externo](../icons/launch-glyph.svg)](https://control.softlayer.com){: new_window}.
 * Los usuarios de SoftLayer con un ID de IBM y con o sin una cuenta de Bluemix enlazada pueden iniciar sesión mediante el [Portal de cliente ![icono de enlace externo](../icons/launch-glyph.svg)](https://control.softlayer.com){: new_window} para abrir el Portal de cliente de SoftLayer o mediante la [consola de Bluemix ![icono de enlace externo](../icons/launch-glyph.svg)](https://console.{DomainName}){: new_window} para abrir el panel de control Infraestructura. 
 * Los usuarios de Bluemix sin una cuenta de SoftLayer enlazada deben iniciar sesión mediante la consola de Bluemix.
 * Los usuarios de Bluemix con una cuenta de SoftLayer enlazada pueden iniciar sesión mediante la [consola de Bluemix ![icono de enlace externo](../icons/launch-glyph.svg)](https://console.{DomainName}){: new_window} o el [Portal de cliente ![icono de enlace externo](../icons/launch-glyph.svg)](https://control.softlayer.com){: new_window}.
 

## La contraseña no es válida
{: #ts_logintobm}

Debe tener un ID de IBM válido para poder iniciar sesión en la consola de {{site.data.keyword.Bluemix_notm}}.

Cuando intente iniciar sesión en {{site.data.keyword.Bluemix_notm}}, verá el siguiente mensaje de error: 
{: tsSymptoms} 

`La contraseña introducida no es correcta.
`

El ID de IBM y la contraseña que utiliza para iniciar sesión en {{site.data.keyword.Bluemix_notm}} no son válidos.
{: tsCauses} 
 
Para obtener un ID de IBM y una contraseña válidos, vaya a la página Mi perfil de IBM y siga los pasos siguientes:
{: tsResolve}
  * Si ya se ha registrado para un ID de IBM y desea comprobar si el ID y la contraseña son válidos, pulse **Iniciar sesión** y especifique el ID de IBM y la contraseña en la página Iniciar sesión. Si ha olvidado su contraseña, pulse **¿Ha olvidado su contraseña?** en la página Iniciar sesión para restablecer la contraseña. Si ha olvidado el ID de IBM o sigue teniendo problemas con su contraseña, póngase en contacto con el centro de atención al cliente de registro de IBM a nivel mundial para obtener ayuda. 
  * Si no tiene un ID de IBM, pulse **Registrar** para registrarse para un ID de IBM y una contraseña. 



## No se puede iniciar sesión con un nombre de usuario de Softlayer
{: #ts_softlayer_username}

Debe tener un ID de IBM y contraseña válidos para poder iniciar una sesión en {{site.data.keyword.Bluemix_notm}}.


Al intentar iniciar sesión en la consola de {{site.data.keyword.Bluemix_notm}} con el nombre de usuario de Softlayer, recibirá el mensaje siguiente: 
{: tsSymptoms} 

`No hemos reconocido este ID de IBM o correo electrónico.`

Debe tener un ID de IBM para iniciar sesión para utilizar el panel de control Infraestructura de la consola de Bluemix.
{: tsCauses} 
 
Si es un usuario de SoftLayer que está utilizando un ID de SoftLayer, debe conmutar a la autenticación del ID de IBM en el Portal de cliente de cada cuenta que tiene acceso antes de poder iniciar sesión utilizando la autenticación del ID de IBM. 

Póngase en contacto con el usuario maestro o con el administrador de la cuenta para cambiar al ID de IBM. 
{: tsResolve}



## Hay cambios sin guardar
{: #ts_unsaved_changes}


Al navegar en la página de detalles de aplicaciones, es posible que no pueda realizar las acciones y es posible que se le solicite que guarde los cambios para poder continuar. 


Cuando intente comprobar la app o los servicios en la página de detalles de la app, seguirá recibiendo el siguiente mensaje de error:
{: tsSymptoms} 

`Hay cambios sin guardar en la página app_name. Guarde o cancele los cambios.`


Cuando desplace el ratón sobre el campo **INSTANCES** o **MEMORY QUOTA** del panel de tiempo de ejecución, los valores cambiarán. Este comportamiento es mediante diseño; sin embargo, el mensaje de error le solicitará que guarde los valores de instancia o de memoria para poder navegar fuera de la página. 
{: tsCauses}


Cierre la ventana de mensajes y, a continuación, pulse el botón **RESET** en el panel de tiempo de ejecución. 
{: tsResolve} 

  
    
## La migración tras error automática entre regiones de {{site.data.keyword.Bluemix_notm}} no está disponible
{: #ts_failover}

No puede utilizar la migración tras error automática entre regiones de {{site.data.keyword.Bluemix_notm}}. Sin embargo, puede utilizar un proveedor de DNS que dé soporte a la migración tras error entre varias direcciones IP como solución temporal.
 

Cuando una región de {{site.data.keyword.Bluemix_notm}} deja de estar disponible, las apps que se ejecutan en dicha región tampoco están disponibles, aunque las mismas apps se estén ejecutando en otra región de {{site.data.keyword.Bluemix_notm}}.
{: tsSymptoms}

 
{{site.data.keyword.Bluemix_notm}} aún no proporciona migración tras error automática entre una región y otra.
{: tsCauses}

 
Puede utilizar un proveedor de DNS que dé soporte a la migración tras error inteligente entre varias direcciones IP y configurar manualmente los valores de DNS para habilitar la migración tras error automática entre regiones de {{site.data.keyword.Bluemix_notm}}. Disponen de esta función los proveedores de DNS NSONE, Akamai, Dyn.
{: tsResolve}

Cuando configure los valores de DNS, debe especificar las direcciones IP públicas de las regiones de {{site.data.keyword.Bluemix_notm}} en la que se ejecutan sus apps. Para obtener la dirección IP pública de una región de {{site.data.keyword.Bluemix_notm}}, utilice el mandato `nslookup`. Por ejemplo, puede escribir el siguiente mandato en una ventana de línea de mandatos:
```
nslookup stage1.mybluemix.net
```



## La cuenta está pendiente
{: #ts_accntpding}

Si la cuenta está pendiente, no puede iniciar una sesión en {{site.data.keyword.Bluemix_notm}}.

 
Después de registrarse para una cuenta de prueba de {{site.data.keyword.Bluemix_notm}}, es posible que no pueda iniciar una sesión en {{site.data.keyword.Bluemix_notm}}. Verá en su lugar el siguiente mensaje:
{: tsSymptoms}

<code>Su cuenta está pendiente. Debe esperar hasta 24 horas a recibir una confirmación por correo electrónico y debe comprobar la carpeta spam. Si transcurrido este tiempo no ha recibido la confirmación por correo electrónico, póngase en contacto con el <a href="http://ibm.biz/bluemixsupport.com" target="_blank">equipo de soporte de Bluemix<img src="../icons/launch-glyph.svg" alt="icono de enlace externo"></a>.</code>


Después de registrarse para una cuenta de prueba de {{site.data.keyword.Bluemix_notm}}, recibirá un correo electrónico de confirmación. Debe pulsar el enlace del correo electrónico de confirmación para completar el proceso de registro.
{: tsCauses} 

El correo electrónico de confirmación se envía a la dirección de correo electrónico que ha especificado. Consulte la bandeja de entrada de la carpeta de correo basura. Si no ha recibido el correo electrónico de confirmación, póngase en contacto con el [equipo de soporte de {{site.data.keyword.Bluemix_notm}}![icono de enlace externo](../icons/launch-glyph.svg)](http://ibm.biz/bluemixsupport.com){: new_window}.  
{: tsResolve}



## No se pueden añadir usuarios a una organización
{: #ts_adduser}

Puede invitar a más de un usuario a trabajar en la misma organización. Solo puede invitar a los usuarios a su organización si es el propietario de la cuenta o si es gestor y miembro de la organización.
 

No ve el enlace **Invitar a un nuevo usuario** en la sección **Gestionar organizaciones**. 
{: tsSymptoms}

 

Únicamente los siguientes usuarios de {{site.data.keyword.Bluemix_notm}}
pueden invitar a usuarios a una organización:
{: tsCauses}
  * El propietario de la cuenta de la organización
  * Gestores de la organización que también son miembros, no colaboradores,
de la organización
  
En {{site.data.keyword.Bluemix_notm}}
puede ser miembro o colaborador de una organización:

<dl><dt>Colaborador</dt>
<dd>Es colaborador de una organización si ya dispone de una
cuenta de {{site.data.keyword.Bluemix_notm}}
y alguien le ha invitado a la organización.</dd>
<dt>Miembro</dt>
<dd>Es miembro de una organización si no dispone de una cuenta de {{site.data.keyword.Bluemix_notm}}, pero alguien le invita a la organización y se registra en {{site.data.keyword.Bluemix_notm}} desde la invitación.</dd>
</dl>


No puede invitar a usuarios a su organización si es
colaborador, incluso si se le ha asignado
como gestor de la organización.

**Nota:** Todos los gestores de la organización, incluidos los que
son colaboradores, pueden añadir, modificar y
eliminar los usuarios que ya están en la organización.

 

Si no puede invitar usuarios a su organización
y necesita otro rol para hacerlo, póngase en contacto con el gestor de la organización
para cambiar el rol. Para identificar el gestor de la organización, siga estos pasos:
{: tsResolve}

  1. Vaya al panel de control de {{site.data.keyword.Bluemix_notm}}. Desde la barra de menús, pulse el elemento de menú **Soporte** y pulse **Gestionar organizaciones**.
  2. Vaya a la organización y consulte la información sobre el gestor de la organización en el separador **USUARIOS**.  
  
Si no puede invitar usuarios porque es colaborador y no un miembro, debe suprimir la cuenta anterior de {{site.data.keyword.Bluemix_notm}} y luego se le debe invitar como un miembro de la organización. Para suprimir la cuenta anterior y unirse como miembro, complete los siguientes pasos: 

  1. Póngase en contacto con el [equipo de soporte de {{site.data.keyword.Bluemix_notm}}![icono de enlace externo](../icons/launch-glyph.svg)](http://ibm.biz/bluemixsupport){: new_window} para abrir una incidencia de soporte y solicitar que se suprima la cuenta. Si tiene datos asociados con su antigua cuenta que desea guardar y moverlos a la nueva cuenta, incluya es información en el correo. 
  2. Cuando se suprima la cuenta, tendrá un usuario con el rol de gestor de la organización y le invitará a unirse como gestor. Luego, inicie sesión en {{site.data.keyword.Bluemix_notm}} desde la invitación. 




## No se da soporte al registro por lotes de usuarios
{: #ts_batchregistration}

Cuando registre usuarios para {{site.data.keyword.Bluemix_notm}},
debe registrar cada usuario por separado.
 

{{site.data.keyword.Bluemix_notm}} no ofrece la posibilidad de registrar varios usuarios a la vez.
{: tsSymptoms}
 

{{site.data.keyword.Bluemix_notm}} no da soporte al registro por lotes de usuarios. Para registrar usuarios para {{site.data.keyword.Bluemix_notm}}, debe registrar cada usuario por separado.
{: tsCauses}
 

Para registrar varios usuarios para {{site.data.keyword.Bluemix_notm}},
debe completar los pasos siguientes para cada usuario:
{: tsResolve}

  1. Pulse **REGISTRARSE** en la consola de {{site.data.keyword.Bluemix_notm}}.
  2. Complete los pasos siguiendo el asistente.

    

## La página {{site.data.keyword.Bluemix_notm}} no se puede cargar
{: #ts_err}

Cuando utilice la consola de {{site.data.keyword.Bluemix_notm}}, es posible que no pueda cargar una página de {{site.data.keyword.Bluemix_notm}}. En su lugar verá los mensajes de error BXNUI0001E o BXNUI0016E.
 

Es posible que vea uno de los siguientes mensajes de error cuando utilice la consola de {{site.data.keyword.Bluemix_notm}}:
{: tsSymptoms}

`BXNUI0001E: La página no se ha cargado porque Bluemix no ha detectado si existe una sesión.`


`BXNUI0016E: Las apps y servicios no se han recuperado porque no se ha cargado una página de Bluemix.`

 
Puede llevar a cabo una o varias de estas acciones si es necesario:
{: tsResolve}

  * Renueve o reinicie el navegador.
  * Finalice la sesión de {{site.data.keyword.Bluemix_notm}} y vuélvala a iniciar.
  * Utilice la modalidad de navegación privada del navegador. 
  * Borre las cookies y la memoria caché del navegador.
  * Utilice otro navegador. Para obtener información sobre las versiones de los navegadores a las que da soporte {{site.data.keyword.Bluemix_notm}}, consulte [Requisitos previos de {{site.data.keyword.Bluemix_notm}}![icono de enlace externo](../icons/launch-glyph.svg)](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}.
  * Si ha instalado la interfaz de línea de mandatos cf, escriba el mandato `cf
apps` para ver si la app se está ejecutando.
  
  
  
  
  

