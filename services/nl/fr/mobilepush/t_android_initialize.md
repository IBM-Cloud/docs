---

Copyright :
  Années : 2015, 2016

---

# Initialisation du logiciel SDK Push pour les applis Android
{: #android_initialize}

Le code d'initialisation se trouve généralement dans la méthode onCreate de l'activité principale de votre application Android.

Cliquez sur le lien **Options pour application mobile** dans le tableau de bord de votre application Bluemix pour obtenir la route et l'identificateur global unique de l'application. Utilisez ces valeurs pour vos paramètres de route et d'identificateur global unique d'application. Modifiez le fragment de code pour qu'il utilise les paramètres appRoute et appGUID de votre appli Bluemix.


##Initialisation du logiciel SDK de base

```
// Initialisez le logiciel SDK pour Java (Android) avec la route et l'identificateur global unique d'application IBM Bluemix
BMSClient.getInstance().initialize(getApplicationContext(), "applicationRoute","applicationGUID", bluemixRegion:"Location where your app Hosted");
```


**appRoute**

Spécifie la route qui a été affectée à l'application serveur que vous avez créée dans Bluemix.

**AppGUID**

Spécifie la clé unique qui a été affectée à l'application que vous avez créée dans Bluemix. Cette
valeur est sensible à la casse.

**bluemixRegionSuffix**

Indique l'emplacement où l'application est hébergée. Vous pouvez utiliser l'une des trois valeurs suivantes :

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY

##Initialisation du logiciel SDK Push du client

```
//Initialisez le logiciel SDK Push du client pour Java
MFPPush push = MFPPush.getInstance();
push.initialize(getApplicationContext());
```
