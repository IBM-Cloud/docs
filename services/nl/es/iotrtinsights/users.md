---

copyright:
  años: 2015,2016

---

{:shortdesc: .shortdesc}

# Gestión de usuarios{: #manage-users}

Diseñado para la colaboración en equipo, {{site.data.keyword.iotrtinsights_short}} permite a los administradores añadir más usuarios para acceder a la consola de {{site.data.keyword.iotrtinsights_short}}.
{: shortdesc}

Descripciones de los roles:
- Operador
Los operadores inician la sesión directamente en la consola de {{site.data.keyword.iotrtinsights_short}} para supervisar el flujo de datos el tiempo real de sus dispositivos y grupos de dispositivos. Los operadores también pueden activar y desactivar reglas y modificar los paneles de control editables.  
- Administrador
Además de las tareas que un operador puede realizar, los administradores pueden añadir usuarios, gestionar diseños del panel de control, añadir orígenes de datos y gestionar tipos de dispositivos.  
- Propietario
El rol del propietario se asigna al ID de IBM que ha desplegado la instancia de servicio de {{site.data.keyword.iotrtinsights_short}} en Bluemix. Un propietario tiene los mismos privilegios que un administrador pero no se pueden suprimir.

Para añadir un nuevo usuario:
1. Añada el usuario a {{site.data.keyword.iot_short}}.  
>**Importante:** Si va a añadir un usuario con el rol de administrador, también debe añadir dicho usuario a {{site.data.keyword.iot_short}}.  

  1. Inicie sesión en el panel de control del servicio {{site.data.keyword.iot_short}} que es un origen de datos para el servicio de {{site.data.keyword.iotrtinsights_short}}.  
  2. Vaya a **Acceder > Miembros** y pulse **Añadir miembros**.
  3. Especifique el ID de IBM para el usuario que desee añadir y pulse **Añadir miembros**.
2. Añada el usuario a {{site.data.keyword.iotrtinsights_short}}.
  1. Inicie sesión en la consola {{site.data.keyword.iotrtinsights_short}} como usuario con el rol de administrador o el rol de propietario.
  2. Vaya a **Configurar > Gestionar usuarios**.
  3. Pulse **Añadir nuevo usuario**.
  4. Especifique la dirección de correo electrónico del usuario al que desee invitar, seleccione un rol para el usuario y pulse ![Crear icono.](images/create.png "Crear icono").
Se ha enviado al usuario un correo electrónico que contiene el enlace de la consola web. Si la dirección de correo electrónico ya está asociada con un ID de IBM, el usuario puede iniciar sesión y acceder a la consola directamente. Si no, se solicitará al usuario que cree un ID de IBM gratuito antes de acceder a la consola.  
>**Selección de la instancia de Real-Time Insights:** Los usuarios que tienen acceso a varias instancias de Real-Time Insights como operadores o administradores pueden alternar rápidamente entre estas instancias. En la consola de Real-Time Insights, puede pulsar su nombre de usuario y seleccionar la instancia a la que desee acceder.  
