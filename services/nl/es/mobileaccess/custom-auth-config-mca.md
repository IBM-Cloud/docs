---

copyright:
  años: 2015, 2016
  
---

# Configuración de {{site.data.keyword.amashort}} para la autenticación personalizada
{: #custom-dash}
Para utilizar la autenticación personalizada con su app móvil, debe registrar un reino de autenticación personalizado y el URL base del proveedor de identidad personalizado en el panel de control del servicio de {{site.data.keyword.amashort}}.

## Antes de empezar
{: #custom-dash-begin}
* Consulte [Cómo empezar](getting-started.html).
* Proteja la aplicación de fondo con el SDK del servidor de {{site.data.keyword.amashort}}.  Para obtener más información, consulte [Protección de recursos](protecting-resources.html).
* Disponga de una aplicación de proveedor de identidad personalizado en ejecución.

## Configuración de la autenticación personalizada en el panel de control de {{site.data.keyword.Bluemix}}
{: #custom-dash-config}
Utilice el panel de control de {{site.data.keyword.amashort}} para configurar la autenticación personalizada.

1. Abra la app en el panel de control de {{site.data.keyword.Bluemix}}.

1. Pulse **Opciones móviles** y anote los valores correspondientes a **Ruta** (`applicationRoute`) y a **Identificador exclusivo global de la app** (`applicationGUID`).Necesitará estos valores cuando inicialice el SDK.

1. Pulse el mosaico de {{site.data.keyword.amashort}}. Se cargará el panel de control de {{site.data.keyword.amashort}}.

1. Pulse el mosaico **Personalizado**. 

1. Introduzca el **Nombre de reino** y el **URL base** del proveedor de identidad personalizado y guarde los cambios.

## Próximos pasos
{: #next-steps}
* [Configuración de la autenticación personalizada para Android](custom-auth-android.html)
* [Configuración de la autenticación personalizada para iOS](custom-auth-ios.html)
* [Configuración de la autenticación personalizada para Cordova](custom-auth-cordova.html)
