---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-01"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Kit de herramientas de cobertura
{: #iot4i_shield_toolkit}
Utilice coberturas para proteger la propiedad y los usuarios identificando riesgos y creando las respuestas automatizadas adecuadas. Utilice o modifique las coberturas que se incluyen en la biblioteca de coberturas de {{site.data.keyword.iotinsurance_short}} o bien cree e implemente sus propias coberturas utilizando las instrucciones y ejemplos a continuación.
{:shortdesc}

## Acerca de las coberturas.
Una cobertura es un conjunto de reglas y acciones definidas que se activan por condiciones específicas en la entrada recibida desde un sensor. Por ejemplo, podría crear una cobertura con una regla que provoque que se envíe un mensaje de texto cuando el sensor detecte una fuga de agua.

## Utilización de coberturas de la biblioteca de coberturas de {{site.data.keyword.iotinsurance_short}}

Encontrará un amplio surtido de coberturas predefinidas en la [biblioteca de coberturas de {{site.data.keyword.iotinsurance_short}} ![Icono de enlace externo](../../icons/launch-glyph.svg)](https://github.com/ibm-watson-iot/ioti-shields){: new_window}. Consulte el archivo README del sitio para obtener instrucciones para descargar y empezar a utilizar las coberturas.

## Creación de su propia cobertura
En este ejemplo se muestra cómo configurar el entorno, definir una cobertura, crear un usuario y asociar la cobertura con el usuario.  De forma opcional, también puede crear promociones y riesgos simulados.  

En las siguientes secciones se muestran ejemplos de código para crear una cobertura simple para fugas de agua. Encontrará un conjunto completo de código disponible en el [repositorio GitHub iot4i-api-examples-nodejs](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/).

### Requisitos previos
Antes de comenzar, asegúrese de que se cumplan los siguientes requisitos previos:

- [Node.js](https://nodejs.org/en/) instalado en su sistema.  
- Un entorno de ejecución habilitado para Node.js como Eclipse.
- Software Git y acceso al [repositorio de código fuente de GitHub para los ejemplos de API](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs).   También puede descargar el [archivo con los archivos del código fuente](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/archive/master.zip).
- Código fuente preparado.  
  Para preparar el código fuente, realice estos pasos:
  1. Clone o descargue el [repositorio de código fuente de GitHub](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs) a su sistema.
  2. Instale los requisitos previos de fuente abierta del proyecto utilizando una línea de mandatos para ir a la carpeta que contiene los archivos de código fuente clonados, y ejecutando el mandato `npm install`.

### Configuración del entorno
{: #environment}
Para configurar el entorno para enviar llamadas REST API, debe configurar el URL para la API en el archivo config.js. El URL del agregador puede ignorarse en este contexto.

```
var config = module.exports = {
  api: "https//iot4insurance-api-<uniqueid>.mybluemix.net",
  aggregator: "https//iot4i-aggregator-<uniqueid>.mybluemix.net",
  credentials : {
    user: "Admin",
    pass: "<password from IoT4I service credentials>"
  }
};
```

### Creación de una definición de cobertura
{: #create_shield_def}

Método: POST  
API: /shield  
https://iot4i-docs-api.mybluemix.net/dist/#!/shield/addShield

Cree una definición de cobertura en el archivo createShield.js.  En el siguiente ejemplo se muestra una cobertura simple que detecta una fuga de agua.

```
var shield = {
  "UUID": "26",
  "name": "demoShield",
  "type": "Environmental Measurements",
  "description": "Detect water leaks",
  "image": "shieldWater",
  "canBeDisabled": false,
  "hazardDetectionOnCloud": true,
  "jsCodeMethod": "demoShield",
  "actions": [
     "pushios"
  ],
  "potentialClaimAmount": "10",
  "shieldParameters": []
};

```

siendo:
- **UUID** - El identificador exclusivo universal (UUID) de la cobertura.
- **actions** - Una lista de acciones que se activan cuando se crea un riesgo. En este ejemplo, la información sobre el riesgo se envía a la aplicación del usuario utilizando una notificación push IOS.

### Creación de un código de cobertura
{: #create_shield_code}
Cree un código de cobertura en el archivo shieldCode.js para definir cómo el motor de coberturas procesa una carga útil.

En el siguiente ejemplo se muestra un código de cobertura que se puede utilizar para procesar una carga útil de fuga de agua para la cobertura mostrada en los ejemplos anteriores.

```
var shieldCode = {
  "name": "demoshield",
  "shieldUUID": "26",
  "type": "shield",
  "code": code.toString()
};

```

Cada código de cobertura contiene recursos que se definen en las sentencias resource/shield.js. Cada uno de los siguientes recursos incluye un ejemplo que puede utilizarse con la cobertura, la carga útil y el usuario de los ejemplos anteriores.

  - Nombre de la cobertura  
  ```
  var DEMO_SHIELD_NAME = "demoshield";
  ```

  - Retraso de cobertura - El retraso en milisegundos entre riesgos.  
  ```
  var DEMO_SHIELD_DELAY = 5000;
  ```

  - Identificador exclusivo universal de cobertura (UUID)  
  ```
  var DEMO_SHIELD_UUID = 26;
  ```

  - Condición de entrada - La condición y los atributos necesarios para que el motor de coberturas procese la carga útil. En el ejemplo, la condición es que la carga útil debe contener el atributo **liquid_detected**.  
  ```
  var demoEntryCondition = function(payload) {
    return (payload.liquid_detected)
  };
  ```

  - Safelet - El núcleo de la cobertura que calcula y ejecuta un algoritmo para determinar si existe un riesgo. En el siguiente ejemplo, el único atributo necesario es **liquid_detected**, pero se puede utilizar safelets para definir algoritmos complejos.  
  ```
  var demoSafelet = function(payload) {
    return (payload.liquid_detected);
  };
  ```

  - Message - El mensaje que se envía al usuario si se procesa el riesgo.
  ```
  var demoMessage = function(payload) {
    return (constructMessage(payload, DEMO_SHIELD_UUID, 'demoHazard', 'a demo shield activated!'));
  };
  ```

  - Ejecución de la cobertura - La función que se utiliza para ejecutar la cobertura directamente, en lugar de esperar a que el motor de coberturas ejecute todas las coberturas relevantes automáticamente.  
  ```
  var demoShield = function(payload) {
    var shield = getShieldByName(DEMO_SHIELD_NAME);
    return (commonShield (payload, shield));
  };
  ```

  - Register shield - Una función predefinida a la cual debe llamarse en el código de cobertura para registrar la cobertura en el motor de coberturas. El valor **undefined** en el ejemplo representa la función de preprocesamiento, que no es necesaria en este ejemplo concreto. En algunas coberturas, la función de preprocesamiento se puede utilizar para reajustar los datos en la carga útil. Por ejemplo, si las lecturas de temperatura se notifican en Fahrenheit y safelet requiere Celsius, la función de preprocesamiento puede utilizarse para convertir las temperaturas al valor requerido.  
  ```
  registerShield(DEMO_SHIELD_UUID, DEMO_SHIELD_NAME, demoEntryCondition, undefined, demoSafelet, demoMessage, DEMO_SHIELD_DELAY);
  ```

### Creación de un usuario
{: #create_user}

Método: POST  
API: /user  
https://iot4i-docs-api.mybluemix.net/dist/#!/user/addUser

Cree un usuario en el archivo createUser.js. El siguiente ejemplo muestra cómo crear un único usuario.

```
var user = {
  "username": "user1",
  "fullname": "John Doe",
  "firstname": "John",
  "lastname": "Doe",
  "password": "user1234",
  "accessLevel": "100",
  "address": "42 Wallaby Way, Sydney",
  "email": "user@example.com",
  "deviceID": "user1",
  "deviceType": "wink",
  "type": "wink"
};

```

siendo:
- **username** - La clave exclusiva para el usuario que se utiliza para identificar todas las entidades asociadas al usuario, como dispositivos, coberturas y promociones.
- **password** - Solo el hash de la contraseña que se almacena en la base de datos.
- **DeviceId** - El identificador que se utiliza para registrar el usuario en {{site.data.keyword.iot_full}}. El valor es el mismo que el nombre de usuario.
- **accessLevel** - El valor define los puntos finales de API a los que puede acceder el usuario:
  - 100 - aplicación móvil
  - 10 - panel de control
  - 1 - administrador del sistema

### Creación de una asociación de coberturas
{: #create_shield_assoc}

Método: POST  
API: /user  
https://iot4i-docs-api.mybluemix.net/dist/#!/shieldassociation/addShieldAssociation

Cree una asociación de coberturas que vincule la cobertura con el usuario en createUserShieldAssociation.js.

En el siguiente ejemplo se muestra una asociación de coberturas para la cobertura y el usuario que se han creado en las secciones anteriores.

```
var userShield = {
  "shieldUUID": "26",
  "username": "user1",
  "hazardDetectionOnCloud": true
};

```



### Creación de un riesgo simulado
{: #create_sim_hazard}

Método: POST  
API: /sendPayloadToMQTT  
https://iot4i-docs-api.mybluemix.net/dist/#!/global/sendPayloadToMQTT

Puede crear una carga útil de riesgo simulado para probar sus coberturas.

El siguiente ejemplo muestra cómo crear una carga útil que activa la cobertura creada en el ejemplo anterior y envía una alerta al usuario asociado.

```
var parameters {
  "payload": {
    "sensor_pod_id": "190107",
    "name": "Sensor",
    "manufacturer_device_model": "leakSMART",
    "device_manufacturer": "leaksmart",
    "model_name": "leakSMART Sensor",
    "upc_code": "waxman_sensor",
    "hub_id": "379652",
    "lat_lng": [null, null],
    "location": "",
    "status": "online",
    "liquid_detected": true,
    "usr": "user1",
    "activation": "2016-06-20T12:05:02.776Z"
  },
  "outputtype": "evt",
  "devicetype": "wink",
  "deviceid": "wink",
  "type": "wink"
};

```


### Creación de una promoción
{: #create_promotion}

{{site.data.keyword.iotinsurance_short}} puede enviar promociones al propietario del hogar mediante la aplicación móvil. Cree promociones utilizando el archivo createPromotion.js.

El siguiente ejemplo muestra cómo crear una promoción para un fontanero autorizado.

```
var promotion = {
  "title": "Promotion 9",
  "description": "Contact one of our authorized plumbers to install your water leak detection solution.",
  "buttonTitle": "Call Now",
  "type": "1",
  "phone": "+015555555555",
  "username": "user1",  
};

```

De forma opcional, puede desplegar la aplicación móvil y utilizar [las instrucciones del repositorio GitHub ioti-mobile](https://github.com/ibm-watson-iot/ioti-mobile) para conectarse como el usuario que ha creado en la sección anterior.

# Enlaces relacionados
{: #rellinks}

## Referencia de API
{: #api}
* [API de {{site.data.keyword.iotinsurance_short}}](https://iot4i-api-docs.mybluemix.net/){:new_window}
* [Ejemplos de API de {{site.data.keyword.iotinsurance_short}}](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/#iot-for-insurance-api-examples){:new_window}

## Enlaces relacionados
{: #general}
* [Foro de soporte para desarrolladores](https://developer.ibm.com/answers/search.html?f=&type=question&redirect=search%2Fsearch&sort=relevance&q=%2B[iot]%20%2B[bluemix])
* [Foro de soporte de Stack Overflow](http://stackoverflow.com/questions/tagged/ibm-bluemix)
