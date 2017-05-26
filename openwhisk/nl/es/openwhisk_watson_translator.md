---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-21"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Uso del paquete de Watson Translator
{: #openwhisk_catalog_watson_translator}

El paquete `/whisk.system/watson-translator` ofrece una forma cómoda de invocar API Watson a convertir.

El paquete incluye las acciones siguientes.

| Entidad | Tipo | Parámetros | Descripción |
| --- | --- | --- | --- |
| `/whisk.system/watson-translator` | paquete | usuario, contraseña | Paquete de traducción de texto e identificación de idioma  |
| `/whisk.system/watson-translator/translator` | acción | payload, translateFrom, translateTo, translateParam, username, password | Traducir texto |
| `/whisk.system/watson-translator/languageId` | acción | payload, username, password | Identificar idioma |

**Nota**: el paquete `/whisk.system/watson` está en desuso, incluidas las acciones `/whisk.system/watson/translate` y `/whisk.system/watson/languageId`.

## Configuración del paquete de Watson Translator en Bluemix

Si utiliza OpenWhisk desde Bluemix, OpenWhisk crea automáticamente enlaces de paquete para sus instancias de servicio de Bluemix Watson.

1. Cree una instancia de servicio de Watson Translator en su [panel de control](http://console.ng.Bluemix.net) de Bluemix.
  
  Asegúrese de recordar el nombre de la instancia de servicio y la organización y el espacio de Bluemix en el que se encuentra.
  
2. Actualizar los paquetes de su espacio de nombres. La renovación crea automáticamente un enlace de paquete para la instancia de servicio de Watson que ha creado.
  
  ```
  wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_Watson_Translator_Credentials-1
  ```
  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_Watson_Translator_Credentials-1 private
  ```
  
  
## Configuración de un paquete de Watson Translator fuera de Bluemix

Si no utiliza OpenWhisk en Bluemix o si quiere configurar Watson Translator fuera de Bluemix, debe crear manualmente un enlace de paquete para el servicio de Watson Translator. Necesita el nombre de usuario del servicio de Watson Translator y la contraseña.

- Cree un enlace de paquete configurado para el servicio de Watson Translator.

  ```
  wsk package bind /whisk.system/watson-translator myWatsonTranslator -p username MYUSERNAME -p password MYPASSWORD
  ```
  {: pre}


## Traducción de texto

La acción `/whisk.system/watson-translator/translator` traduce texto de un idioma a otro. Los parámetros son según se indica a continuación:

- `username`: el nombre de usuario de la API de Watson.
- `password`: contraseña de la API de Watson.
- `payload`: el texto que se debe traducir.
- `translateParam`: el parámetro de entrada que indica el texto a traducir. Por ejemplo, si es `translateParam=payload`, el valor del parámetro `payload` que se pasa a la acción, se traduce.
- ` translateFrom`: un código de dos dígitos del lenguaje origen.
- `translateTo`: un código de dos dígitos del idioma de destino.

- Invoque la acción `translator` en su enlace de paquete para traducir algún texto de inglés a español.
  
  ```
  wsk action invoke myWatsonTranslator/translator \
  --blocking --result \
  --param payload "Blue skies ahead" --param translateFrom "en" \
  --param translateTo "fr"
  ```
  {: pre}
  ```json
  {
      "payload": "Se esperan cielos despejados"
  }
  ```
  
  
## Identificación del idioma de un texto

La acción `/whisk.system/watson-translator/languageId` identifica el idioma de algún texto. Los parámetros son según se indica a continuación:

- `username`: el nombre de usuario de la API de Watson.
- `password`: contraseña de la API de Watson.
- `payload`: el texto a identificar.

- Invocar la acción `languageId` en su enlace de paquete para identificar el idioma.
  
  ```
  wsk action invoke myWatsonTranslator/languageId \
  --blocking --result \
  --param payload "Ciel bleu a venir"
  ```
  {: pre}
  ```json
  {
    "payload": "Se esperan cielos despejados",
    "language": "es",
    "confidence": 0.710906
  }
  ```
  
