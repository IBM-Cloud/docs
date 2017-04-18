---

copyright:
 years: 2015, 2016

---

# Inicialización del SDK push para aplicaciones Android
{: #android_initialize}

Un lugar común para colocar el código de inicialización se encuentra en el método onCreate de la actividad principal en su aplicación Android.

Pulse el enlace **Opciones móviles** en el Panel de control de aplicaciones de Bluemix para obtener la ruta de la aplicación y el applicationGUID. Utilice estos valores para su ruta y GUID de la app. Modifique el fragmento de código para que utilice los parámetros appRoute y appGUID de la aplicación Bluemix.


## Inicializar el SDK principal

```
// Initialize the SDK for Java (Android) with IBM Bluemix AppGUID and route
BMSClient.getInstance().initialize(getApplicationContext(), "applicationRoute","applicationGUID", bluemixRegion:"Location where your app Hosted");
```


**appRoute**

Especifica la ruta que se asigna a la aplicación de servidor que ha creado en Bluemix.

**AppGUID**

Especifica la clave exclusiva asignada a la aplicación que ha creado en Bluemix. Este valor distingue entre mayúsculas y minúsculas.

**bluemixRegionSuffix**

Especifica la ubicación donde se ha alojado la app. Puede utilizar uno de estos tres valores:

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY

## Inicializar el SDK push del cliente

```
//Initialize client Push SDK for Java
MFPPush push = MFPPush.getInstance();
push.initialize(getApplicationContext());
```
