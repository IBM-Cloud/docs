---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-08"

---

# Configuración de {{site.data.keyword.amashort}} para la autenticación personalizada
{: #custom-dash}


Para utilizar la autenticación personalizada con su app móvil, debe registrar un reino de autenticación personalizado y el URL base del proveedor de identidad personalizado en el panel de control del servicio de {{site.data.keyword.amashort}}.

## Antes de empezar
{: #custom-dash-begin}
Debe tener lo siguiente:
* Una instancia de un servicio {{site.data.keyword.amafull}}.
* Disponga de una aplicación de proveedor de identidad.

## Configuración de la autenticación personalizada en el panel de control de {{site.data.keyword.amafull}}
{: #custom-dash-config}
Utilice el panel de control de {{site.data.keyword.amafull}} para configurar la autenticación personalizada.

1. Abra el servicio en el panel de control de {{site.data.keyword.amafull}}.
1. En el separador **Gestionar**, active **Autorización**.
1. Expanda la sección **Personalizada**.
1. Especifique el **Nombre de dominio** y el **URL de proveedor de identidad personalizado**. El valor **URI de redirección de su aplicación web** sólo es necesario para aplicaciones web.

## Pasos siguientes
{: #next-steps}
* [Configuración de la autenticación personalizada para Android](custom-auth-android.html)
* [Configuración de la autenticación personalizada para iOS](custom-auth-ios-swift-sdk.html)
* [Configuración de la autenticación personalizada para Cordova](custom-auth-cordova.html)
