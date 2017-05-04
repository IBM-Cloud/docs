---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-07"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Terminaux et fournisseurs pris en charge
{: #supportedcloud}

{{site.data.keyword.iotinsurance_full}} prend en charge l'intégration avec de nombreux fournisseurs de cloud et terminaux.
{: shortdesc}

## Terminaux pris en charge par fournisseur
{: #supportedvendors}
Le tableau suivant répertorie les fournisseurs et les terminaux pris en charge par {{site.data.keyword.iotinsurance_short}} et décrit le type d'intégration. Les types d'intégration suivants sont disponibles :

  - **{{site.data.keyword.iot_short_notm}}** : le terminal ou le concentrateur publie les événements de capteur directement dans {{site.data.keyword.iot_short_notm}}. {{site.data.keyword.iotinsurance_short}} peut traiter les événements de capteur directement ou après leur modification par le transformateur {{site.data.keyword.iotinsurance_short}}.

  - **Cloud-à-cloud** : le terminal ou le concentrateur publie les événements de capteur dans un cloud tiers. Le transformateur {{site.data.keyword.iotinsurance_short}} lit ces événements à partir du cloud tiers et les publie dans {{site.data.keyword.iot_short_notm}}.

<table>
<thead>
<tr>
<th>Nom du fournisseur</th>
<th>Type d'intégration</th>
<th>Terminaux testés</th>
<th>Informations sur le fournisseur </th>
</tr>
</thead>
<tbody>
<tr>
<td>Bosch E-Call</td>
<td>{{site.data.keyword.iot_short_notm}}.  
Une application de passerelle a été écrite pour tester l'intégration.</td>
<td>Bosch Retrofit E-Call</td>
<td>[Site Web du fournisseur ![Icône de lien externe](../../icons/launch-glyph.svg)](http://www.bosch-connectivity.com/en/what_we_offer/products_and_solutions_1/retrofit_ecall/connected_devices_3){: new_window}</td>
</tr>
<tr>
<td>EnOcean</td>
<td>{{site.data.keyword.iot_short_notm}}</td>
<td>
<ul>
<li>Bouton</li>
<li>Contact</li>
<li>Température</li>
</ul>
</td>
<td>[Site Web du fournisseur ![Icône de lien externe](../../icons/launch-glyph.svg)](https://www.enocean.com/en/</td>){: new_window}
</tr>
<tr>
<td>WiButler (iExergy)</td>
<td>{{site.data.keyword.iot_short_notm}}</td>
<td>
<ul>
<li>Détecteur de fumée</li>
<li>Bouton</li></td>
</ul>
<td>[Site Web du fournisseur ![Icône de lien externe](../../icons/launch-glyph.svg)](https://www.wibutler.com/en_GB){: new_window}</td>
</tr>
<tr>
<td>Wink</td>
<td>Cloud-à-cloud</td>
<td>Fuite d'eau</td>
<td>[Site Web du fournisseur ![Icône de lien externe](../../icons/launch-glyph.svg)](https://www.wink.com/){: new_window}</td>
</tr>
<tr>
<td>Yanzi</td>
<td>{{site.data.keyword.iot_short_notm}} et cloud-à-cloud</td>
<td>Aucun capteur n'a été testé.</td>
<td>[Site Web du fournisseur ![Icône de lien externe](../../icons/launch-glyph.svg)](https://ibm.ent.box.com/notes/126680846739){: new_window}</td>
</tr>
</tbody>
</table>

## Intégration de terminaux et de clouds fournisseur
{: #integratingdevices}
Vous pouvez intégrer vos terminaux et clouds fournisseur avec {{site.data.keyword.iotinsurance_short}}. Les sections suivantes décrivent les procédures d'intégration et proposent des exemples d'enregistrement utilisateur pour chaque fournisseur.

Pour plus d'informations sur l'intégration des capteurs et des terminaux, voir [Kit d'outils de terminal](iotinsurance_device_toolkit.html) :


### EnOcean
#### Procédure d'intégration
  1. Créez une passerelle dans l'instance {{site.data.keyword.iot_short_notm}} connectée à {{site.data.keyword.iotinsurance_short}}.
  2. Connectez le concentrateur EnOcean à la passerelle {{site.data.keyword.iot_short_notm}}.
  3. Ajoutez l'identificateur de passerelle à l'enregistrement utilisateur dans {{site.data.keyword.iotinsurance_short}}.

#### Exemple d'enregistrement utilisateur

```
{
    "username": "utilisateur@exemple.com",
    "password": "",
    "accessLevel": "13",
    "fullname": "John Doe",
    "email": "utilisateur@exemple.com",
    "phonenumber": "+123456789",
    "address": {
      ...
    },
    "gatewayIds": [
      "digital-concepts-gateway1"
    ],
    ...
}
```

### WiButler (iExergy)

#### Procédure d'intégration
L'intégration avec les données WiButler est actuellement prise en charge en tant que démonstration de faisabilité ou aperçu technique uniquement et n'est pas destinée à une utilisation en production. Le matériel WiButler requiert une mise à jour du microcode pour transmettre les données à {{site.data.keyword.iot_short_notm}}.

#### Exemple d'enregistrement utilisateur

```
{
    "username": "utilisateur@exemple.com",
    "password": "",
    "accessLevel": "13",
    "fullname": "John Doe",
    "email": "utilisateur@exemple.com",
    "phonenumber": "+123456789",
    "address": {
      ...
    },
    "gatewayIds": [
      "Wibutler-Gateway-ID"
    ],
    ...
}
```

### Wink

#### Procédure d'intégration

**Option 1**
  1. Obtenez les [jetons d'autorisation Wink ![Icône de lien externe](../../icons/launch-glyph.svg)](http://docs.winkapiv2.apiary.io/#){: new_window}.
  2. Ajoutez le jeton d'autorisation à l'utilisateur correspondant dans le système {{site.data.keyword.iotinsurance_short}} à l'aide de l'API {{site.data.keyword.iotinsurance_short}}.

**Option 2**  
Procédez à l'intégration avec l'application mobile (obsolète). Cette méthode fonctionne uniquement avec la version 1.0 d'{{site.data.keyword.iotinsurance_short}}.

#### Exemple d'enregistrement utilisateur

```
{
  "username": "utilisateur@exemple.com",
  "password": "",
  ....
  "deviceID": "528DB5CA-7F3D-4478-A4EB-994E7F118B6B",
  "assets": [
    {
      "name": "default",
      "providers": [
        {
          "name": "wink",
          "tokens": {
            "data": {
              "access_token": "fjyw9nN_YhU-fZU9kCqTQ6Ijsr_9XdvO",
              "refresh_token": "OOMyB8JGCHgjOHku8zp2Yrevoeci48Ou",
              "token_type": "bearer",
              "token_endpoint": "https://api.wink.com/oauth2/token",
              "scopes": "full_access"
            },
            "errors": [],
            "pagination": {},
            "access_token": "fjyw9nN_YhU-fZU9kCqTQ6Ijsr_9XdvO",
            "refresh_token": "OOMyB8JGCHgjOHku8zp2Yrevoeci48Ou",
            "token_type": "bearer",
            "token_endpoint": "https://api.wink.com/oauth2/token",
            "scopes": "full_access"
          }
        }
      ]
    }
  ]
}

```

### Yanzi
#### Procédure d'intégration
**Option 1**  
  Ajoutez les données d'identification du cloud Yanzi dans le fichier yanzi-config.json de l'annuaire du fournisseur dans le référentiel du transformateur.  L'objet "yanziCloud" est l'emplacement correct des données d'identification.  

**Option 2**  
  Yanzi utilise une intégration cloud-à-cloud entre le cloud Yanzi et {{site.data.keyword.iot_short_notm}}. L'autorisation pour cette intégration survient dans le cloud Yanzi. Une fois l'autorisation terminée, le cloud Yanzi envoie les événements à {{site.data.keyword.iot_short_notm}}. Vous devez également ajouter les données d'identification de l'instance {{site.data.keyword.iot_short_notm}} dans le fichier yanzi-config.json de l'annuaire du fournisseur dans le référentiel du transformateur à l'aide de l'objet "iotfCredentials".

#### Exemple d'enregistrement utilisateur

```
{
  "yanziCloud": {
      "cirrusHost": "wss://",
      "username": "",
      "password": "",
      "locationId": "",
      "unitDid": ""
  },
  "iotfCredentials": {
      "org": "",
      "apiKey": "",
      "apiToken": "",
      "type": "shared",
      "mqtt_host": "gbdprt.messaging.internetofthings.ibmcloud.com",
      "domain": "internetofthings.ibmcloud.com"
  }
}
```

### Données Weather Company
#### Procédure d'intégration
L'intégration avec les données Weather Company est actuellement prise en charge en tant que démonstration de faisabilité ou aperçu technique uniquement et n'est pas destinée à une utilisation en production.

Fournissez une adresse pour l'extraction des conditions météorologiques en cours (température extérieure) de The Weather Company pour un emplacement spécifique.



#### Exemple d'enregistrement utilisateur

```
{ "username": "johndoe",
   "fullname": "John Doe",
    "firstname": "John",
    "lastname": "Doe",
    "password": "",
     "accessLevel": 13,
     "address": "24, avenue du Château, 78000 Versailles, France",
     ...
}

```
