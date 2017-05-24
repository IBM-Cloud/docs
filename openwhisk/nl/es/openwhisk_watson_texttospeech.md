---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-21"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Uso del paquete Watson Text to Speech
{: #openwhisk_catalog_watson_texttospeech}

El paquete `/whisk.system/watson-textToSpeech` ofrece una forma cómoda de invocar API Watson para convertir el texto a voz.

El paquete incluye las acciones siguientes.

| Entidad | Tipo | Parámetros | Descripción |
| --- | --- | --- | --- |
| `/whisk.system/watson-textToSpeech` | paquete | usuario, contraseña | Paquete para convertir texto en habla |
| `/whisk.system/watson-textToSpeech/textToSpeech` | acción | payload, voice, accept, encoding, username, password | Convertir texto en audio |

**Nota**: el paquete `/whisk.system/watson` está en desuso, incluida la acción `/whisk.system/watson/textToSpeech`.

## Configuración del paquete Watson Text to Speech en Bluemix

Si utiliza OpenWhisk desde Bluemix, OpenWhisk crea automáticamente enlaces de paquete para sus instancias de servicio de Bluemix Watson.

1. Cree una instancia de servicio Watson Text to Speech en el [panel de control](http://console.ng.Bluemix.net) de Bluemix.
  
  Asegúrese de recordar el nombre de la instancia de servicio y la organización y el espacio de Bluemix en el que se encuentra.
  
2. Actualizar los paquetes de su espacio de nombres. La renovación crea automáticamente un enlace de paquete para la instancia de servicio de Watson que ha creado.
  
  ```
  wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_Watson_TextToSpeech_Credentials-1
  ```
  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_Watson_TextToSpeec_Credentials-1 private
  ```
  
  
## Configuración de un paquete Watson Text to Speech fuera de Bluemix

Si no utiliza OpenWhisk en Bluemix o si quiere configurar Watson Text to Speech fuera de Bluemix, debe crear manualmente un enlace de paquete para el servicio de Watson Text to Speech. Necesita el nombre de usuario del servicio de Watson Text to Speech y la contraseña.

- Cree un enlace de paquete configurado para el servicio de Watson Speech to Text.
  
  ```
  wsk package bind /whisk.system/watson-speechToText myWatsonTextToSpeech -p username MYUSERNAME -p password MYPASSWORD
  ```
  {: pre}
  

## Conversión de texto a habla

La acción `/whisk.system/watson-speechToText/textToSpeech` convierte texto en un texto hablado. Los parámetros son según se indica a continuación:

- `username`: el nombre de usuario de la API de Watson.
- `password`: contraseña de la API de Watson.
- `payload`: texto que se debe convertir en habla.
- `voice`: voz de la persona que habla.
- `accept`: formato del archivo de audio.
- `encoding`: codificación de los datos binarios del habla.


- Invoque la acción `textToSpeech` en el enlace del paquete para convertir el texto.
  
  ```
  wsk action invoke myWatsonTextToSpeech/textToSpeech --blocking --result --param payload 'Hey.' --param voice 'en-US_MichaelVoice' --param accept 'audio/wav' --param encoding 'base64'
  ```
  {: pre}
  ```json
  {
    "payload": "<base64 encoding of a .wav file>"
  }
  ```
  
