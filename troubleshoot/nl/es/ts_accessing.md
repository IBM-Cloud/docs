---

copyright:
  years: 2015, 2017
  
lastupdated: "2017-03-02"

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 



# Resolución de problemas de acceso a {{site.data.keyword.Bluemix_notm}} 
{: #accessing}


Algunos de los problemas generales de acceso a {{site.data.keyword.Bluemix}} incluyen dificultades al iniciar una sesión en {{site.data.keyword.Bluemix_notm}} o que una cuenta se haya bloqueado en estado pendiente. En muchos de los casos, puede solucionar estos problemas siguiendo unos sencillos pasos. 
{:shortdesc}

## No se puede iniciar la sesión en {{site.data.keyword.Bluemix_notm}}: Contraseña incorrecta
{: #ts_logintobm}

Debe tener una contraseña válida que esté asociada a su ID de IBM para poder iniciar sesión en la consola de {{site.data.keyword.Bluemix_notm}}.

Debe disponer de una contraseña válida que está asociada con su ID de IBM o su ID de SoftLayer para iniciar una sesión a través del [portal del cliente](https://control.softlayer.com).

Cuando intenta iniciar una sesión en {{site.data.keyword.Bluemix_notm}}, aparece el siguiente mensaje de error: 
{: tsSymptoms} 

`La contraseña introducida no es correcta.
`

El ID de IBM y la contraseña que ha utilizado para iniciar sesión en {{site.data.keyword.Bluemix_notm}} no son válidos.
{: tsCauses} 
 
Utilice una de las soluciones siguientes:
{: tsResolve}
 * Escriba la contraseña correcta. Para comprobar si su ID de IBM y contraseña son válidos, puede ir a la página Mi perfil de IBM, pulsar **Iniciar sesión** y especificar el ID de IBM y la contraseña en la página Iniciar sesión. 
 * Si ha olvidado su contraseña, pulse **¿Ha olvidado su contraseña?** para restablecer la contraseña. Luego vuelva a la [consola de Bluemix](https://console.{DomainName}) o al [portal del cliente](https://control.softlayer.com) y vuelva a iniciar la sesión.
 * Si ha olvidado el ID de IBM o sigue teniendo problemas con su contraseña, póngase en contacto con el centro de atención al cliente de registro de IBM a nivel mundial para obtener ayuda. 
 * Para obtener un ID de IBM y una contraseña válidos, vaya a la página Mi perfil de IBM y pulse **Registro**.
  
**Nota:** si está en la página de inicio de sesión en IBM y el proceso de inicio de sesión se interrumpe por cualquier motivo (por ejemplo, al restablecer su contraseña), vuelva a la [consola de Bluemix](https://console.{DomainName}) o al [portal del cliente](https://control.softlayer.com) y comience de nuevo el proceso de inicio de sesión.
 

## No se puede iniciar la sesión en {{site.data.keyword.Bluemix_notm}}: Credenciales de inicio de sesión no válidas
{: #ts_login_invalid_credentials}

Cuando inicia sesión con su ID de IBM, aparece el siguiente mensaje:
{: tsSymptoms}

`Se han proporcionado credenciales de inicio de sesión no válidas. Si tiene un ID de IBM asociado a su cuenta, inicie la sesión aquí` 

* Ha utilizado un ID de IBM, pero ha intentado iniciar la sesión en el [portal del cliente](https://control.softlayer.com) utilizando el nombre de usuario y contraseña de SoftLayer anteriores. 
{: tsCauses}

* Ha intentado iniciar la sesión en el [portal del cliente](https://control.softlayer.com), pero ha el ID de IBM y la contraseña de los campos Nombres de usuario y Contraseña. 

Pulse **iniciar la sesión aquí** en el mensaje o vaya a la sección de inicio de sesión con cuenta de ID de IBM y pulse **Iniciar la sesión con ID de IBM**.
{: tsResolve}

No utilice los campos **Nombre de usuario** y **Contraseña** que ha utilizado con el ID de Softlayer anterior.


## No se puede iniciar la sesión en {{site.data.keyword.Bluemix_notm}}: ID de IBM o correo electrónico no reconocido
{: #ts_softlayer_username}

Cuando inicia sesión en la consola de {{site.data.keyword.Bluemix_notm}} aparece el siguiente mensaje: 
{: tsSymptoms} 

`No hemos reconocido este ID de IBM o correo electrónico.`

Ha intentado iniciar la sesión en la consola {{site.data.keyword.Bluemix_notm}}, pero no ha utilizado un ID de IBM válido. Por ejemplo, no ha especificado una dirección de correo electrónico completa para el ID de IBM o ha intentado utilizar un nombre de usuario y contraseña de SoftLayer.
{: tsCauses}
 
Debe tener un ID de IBM y contraseña válidos para poder iniciar una sesión en {{site.data.keyword.Bluemix_notm}}.

 * Asegúrese de especificar una dirección de correo electrónico completa para el ID de IBM.
 {: tsResolve}
 * Si es un usuario de SoftLayer con un ID de SoftLayer, debe cambiar a la autenticación del ID de IBM en el Portal de cliente de cada cuenta a la que tiene acceso para poder iniciar una sesión utilizando la autenticación del ID de IBM. 
 Para obtener más información, consulte [Cambio a un ID de IBM](/docs/admin/softlayerlink.html#ibmid_switch).


## No se puede iniciar la sesión en {{site.data.keyword.Bluemix_notm}}: El ID de IBM no está asociada a ninguna cuenta de IBM Cloud
{: #ts_login_noswitch}

Cuando inicia sesión con su ID de IBM, aparece el siguiente mensaje:
{: tsSymptoms}

`Ha llegado a esta página porque la autenticación ha sido satisfactoria; sin embargo, este ID de IBM no está asociado con ninguna cuenta de IBM Cloud. Si cree que esto es un error, póngase en contacto con el Propietario de la cuenta o el Usuario maestro.`

Ha iniciado una sesión desde el [portal del cliente](https://control.softlayer.com) con un ID de IBM válido, pero que no ha cambiado a la autenticación con ID de IBM en SoftLayer.
{: tsCauses} 
 
Siga los pasos siguientes según proceda:
{: tsResolve}
 * Póngase en contacto con el usuario maestro o con el administrador para comprobar que puede cambiar a la autenticación con ID de IBM.
 * Asegúrese de haber llevado a cabo el paso de cambio a ID de IBM en su cuenta de Softlayer. Consulte [Cambio a un ID de IBM](/docs/admin/softlayerlink.html#ibmid_switch).
 * Asegúrese de seguir las acciones del correo electrónico **Asociar su usuario de SoftLayer con un ID de IBM**. Consulte la bandeja de entrada y la carpeta spam para buscar el correo electrónico. Para recuperar el correo electrónico, por ejemplo si ha caducado, vaya a la página Editar perfil de usuario del portal de control y pulse **Reenviar correo electrónico**. Como alternativa, póngase en contacto con el [equipo de soporte de {{site.data.keyword.Bluemix_notm}}![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](http://ibm.biz/bluemixsupport.com){: new_window}.

**Nota:** si ha creado su ID de IBM directamente con ID de IBM, habrá recibido dos correos electrónicos; uno del registro de ID de IBM y otro de Softlayer. Asegúrese de seguir las indicaciones de ambos correos electrónicos.

En función de cómo se haya configurado su cuenta, se podrán aplicar algunas de estas opciones de inicio de sesión: 
 * Los usuarios de SoftLayer con ID de SoftLayer deben iniciar sesión a través del [Portal de cliente](https://control.softlayer.com).
 * Los usuarios de SoftLayer con un ID de IBM y con o sin una cuenta de Bluemix enlazada pueden iniciar sesión mediante el [Portal de cliente](https://control.softlayer.com) para abrir el Portal de cliente de SoftLayer o mediante la [consola de Bluemix](https://console.{DomainName}) para abrir el panel de control Infraestructura. 


## No se puede iniciar la sesión en {{site.data.keyword.Bluemix_notm}}: El ID de IBM no está asociada a ninguna cuenta de {{site.data.keyword.Bluemix_notm}}
{: #ts_unabletologin}

Cuando inicia sesión en {{site.data.keyword.Bluemix_notm}},
aparece el siguiente mensaje: 
{: tsSymptoms} 
 
`Ha llegado a esta página porque la autenticación ha sido satisfactoria; sin embargo, este ID de IBM no está asociado a ninguna cuenta de {{site.data.keyword.Bluemix_notm}}.`

Ha iniciado sesión en la [consola de Bluemix](https://console.{DomainName}) con un ID de IBM válido pero aún no ha creado una cuenta de {{site.data.keyword.Bluemix_notm}}. 
{: tsCauses} 

Para crear una cuenta de {{site.data.keyword.Bluemix_notm}}, siga el proceso de registro. 
{: tsResolve}

En función de cómo se haya configurado su cuenta, se podrán aplicar algunas de estas opciones de inicio de sesión: 
 * Los usuarios de Bluemix sin una cuenta de SoftLayer enlazada deben iniciar sesión mediante la consola de Bluemix.
 * Los usuarios de Bluemix con una cuenta de SoftLayer enlazada pueden iniciar sesión mediante la [consola de Bluemix](https://console.{DomainName}) o el [Portal de cliente](https://control.softlayer.com).
 

## No se puede iniciar la sesión en {{site.data.keyword.Bluemix_notm}}: La consola no se abre
{: #ts_login_stalls}

Cuando inicia una sesión utilizando su ID de IBM, se muestra un mensaje de inicio de sesión correcto, pero no vuelve a la [consola de Bluemix](https://console.{DomainName}) ni al [portal del cliente](https://control.softlayer.com).
{: tsSymptoms}

Utilice una de las soluciones siguientes:
{: tsResolve}
 * Cierre el navegador, borre la memoria caché y las cookies y luego intente de nuevo iniciar la sesión.
 * Asegúrese de iniciar la sesión desde la [consola de Bluemix](https://console.{DomainName}) o desde el [portal del cliente](https://control.softlayer.com) en lugar de hacerlo directamente desde el servicio de autenticación de ID de IBM.
 
 
## No se puede iniciar la sesión en {{site.data.keyword.Bluemix_notm}}: El inicio de sesión con ID de IBM no se completa
{: #ts_login_ibmid}

Cuando inicia una sesión en {{site.data.keyword.Bluemix_notm}}, la autenticación con ID de IBM no se completa.
{: tsSymptoms}

Es posible que haya un problema con el servicio de autenticación de ID de IBM.
{: tsCauses}

Compruebe el estado del servicio en [IBM BlueID ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](https://new.wind.ibmcloud.com/webapp/#/status/a1a0c5d743d94a6a9597087541564d8e){: new_window} y vuélvalo a intentar.
{: tsResolve}


## No se puede iniciar la sesión en {{site.data.keyword.Bluemix_notm}}: La cuenta está pendiente
{: #ts_accntpding}

Si la cuenta está pendiente, no puede iniciar una sesión en {{site.data.keyword.Bluemix_notm}}.
 
Después de registrarse para una cuenta de prueba de {{site.data.keyword.Bluemix_notm}}, es posible que no pueda iniciar una sesión en {{site.data.keyword.Bluemix_notm}}. Se visualiza el mensaje siguiente:
{: tsSymptoms}

<code>Su cuenta está pendiente. Debe esperar hasta 24 horas a recibir una confirmación por correo electrónico y debe comprobar la carpeta spam. Si transcurrido este tiempo no ha recibido la confirmación por correo electrónico, póngase en contacto con el <a href="http://ibm.biz/bluemixsupport.com" target="_blank">soporte de Bluemix</a>.</code>

Después de registrarse para una cuenta de prueba de {{site.data.keyword.Bluemix_notm}}, recibirá un correo electrónico de confirmación. Debe pulsar el enlace del correo electrónico de confirmación para completar el proceso de registro.
{: tsCauses} 

El correo electrónico de confirmación se envía a la dirección de correo electrónico que ha especificado. Consulte la bandeja de entrada de la carpeta spam. Si no ha recibido el correo electrónico de confirmación, póngase en contacto con el [equipo de soporte de {{site.data.keyword.Bluemix_notm}} ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](http://ibm.biz/bluemixsupport.com){: new_window}.  
{: tsResolve}


## Hay cambios sin guardar
{: #ts_unsaved_changes}

Al navegar en la página de detalles de apps, es posible que no pueda realizar las acciones y es posible que se le solicite que guarde los cambios para poder continuar. 

Cuando intente comprobar la app o los servicios en la página de detalles de la app, seguirá recibiendo el siguiente mensaje de error:
{: tsSymptoms} 

`Hay cambios sin guardar en la página app_name. Guarde o cancele los cambios.`

Cuando desplace el ratón sobre el campo **INSTANCIAS** o **CUOTA DE MEMORIA** del panel de tiempo de ejecución, los valores cambiarán. Este comportamiento es mediante diseño; sin embargo, el mensaje de error le solicitará que guarde los valores de instancia o de memoria para poder navegar fuera de la página. 
{: tsCauses}

Cierre la ventana de mensajes y, a continuación, pulse el botón **RESTABLECER** en el panel de tiempo de ejecución. 
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

  1. Vaya al panel de control de {{site.data.keyword.Bluemix_notm}}. Desde la barra de menús, pulse el elemento de menú **Cuenta** y pulse **Gestionar organizaciones**.
  2. Vaya a la organización y consulte la información sobre el gestor de la organización en el separador **USUARIOS**.  
  
Si no puede invitar usuarios porque es colaborador y no un miembro, debe suprimir la cuenta anterior de {{site.data.keyword.Bluemix_notm}} y luego se le debe invitar como un miembro de la organización. Para suprimir la cuenta anterior y unirse como miembro, complete los siguientes pasos: 

  1. Póngase en contacto con el [equipo de soporte de {{site.data.keyword.Bluemix_notm}} ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](http://ibm.biz/bluemixsupport){: new_window} para abrir una incidencia de soporte y solicitar que se suprima la cuenta. Si tiene datos asociados con su antigua cuenta que desea guardar y moverlos a la nueva cuenta, incluya es información en el correo. 
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
siga los pasos siguientes para cada usuario:
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

Lleve a cabo una o varias de estas acciones si es necesario:
{: tsResolve}

  * Renueve o reinicie el navegador.
  * Finalice la sesión de {{site.data.keyword.Bluemix_notm}} y vuélvala a iniciar.
  * Utilice la modalidad de navegación privada del navegador. 
  * Borre las cookies y la memoria caché del navegador.
  * Utilice otro navegador. Para obtener información sobre las versiones de los navegadores a las que da soporte {{site.data.keyword.Bluemix_notm}}, consulte [Requisitos previos de Bluemix](/docs/overview/whatisbluemix.html#prereqs).
  * Si ha instalado la interfaz de línea de mandatos cf, escriba el mandato `cf apps` para ver si la app se está ejecutando.
