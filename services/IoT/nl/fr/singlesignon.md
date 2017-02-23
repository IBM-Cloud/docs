---

copyright:
  years: 2016, 2017
lastupdated: "2016-10-05"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Configuration et utilisation de {{site.data.keyword.ssoshort}}

Le service {{site.data.keyword.ssofull}} peut être configuré afin de prendre en charge des fournisseurs d'authentification d'utilisateur alternatifs pour votre instance {{site.data.keyword.iot_full}}. {{site.data.keyword.ssoshort}} prend en charge SAML 2.0, IBM Cloud Directory, des fournisseurs sociaux (Facebook, LinkedIn, Google+) et Github.
{: .shortdesc}

## Configuration de {{site.data.keyword.ssoshort}}

Pour configurer {{site.data.keyword.ssoshort}}, procédez comme suit :

1. Dans votre tableau de bord {{site.data.keyword.Bluemix}}, ajoutez un service {{site.data.keyword.ssoshort}}.
2. Configurez les fournisseurs d'authentification que le service {{site.data.keyword.ssoshort}} devra utiliser.

## Création d'une application factice et établissement d'une liaison entre celle-ci et le service {{site.data.keyword.ssoshort}}

Le service {{site.data.keyword.ssoshort}} ne peut pas être lié directement à d'autres services, par conséquent, une application factice doit être créée afin d'extraire les données de configuration requises à partir du service {{site.data.keyword.ssoshort}}.

1. Dans le tableau de bord {{site.data.keyword.Bluemix_notm}}, ajoutez l'application {{site.data.keyword.sdk4nodefull}}.
2. Cliquez sur l'application {{site.data.keyword.sdk4nodefull}} à partir du tableau de bord {{site.data.keyword.Bluemix_notm}}, puis cliquez sur **Lier un service ou une API**.
3. Sélectionnez le service {{site.data.keyword.ssoshort}} et cliquez sur **Ajouter**.
4. L'application {{site.data.keyword.sdk4nodefull}} doit à présent être reconstituée.
5. Cliquez sur l'application {{site.data.keyword.sdk4nodefull}} dans le tableau de bord {{site.data.keyword.Bluemix_notm}}.
6. Sélectionnez le service {{site.data.keyword.ssoshort}} et cliquez sur **Intégrer**.
7. Entrez l'URL Return-to-URL :
`https://<orgid>.internetofthings.ibmcloud.com/get-ibmsso-access-token` où `<orgid>` est l'ID de votre organisation {{site.data.keyword.iot_short_notm}}.

## Configuration de {{site.data.keyword.iot_short_notm}} pour {{site.data.keyword.ssoshort}}

Après avoir lié et configuré l'application {{site.data.keyword.sdk4nodefull}} et le service {{site.data.keyword.ssoshort}}, vous devez configurer {{site.data.keyword.iot_short_notm}}. {{site.data.keyword.iot_short_notm}} peut être configuré à l'aide de l'interface utilisateur {{site.data.keyword.iot_short_notm}} ou de l'API {{site.data.keyword.iot_short_notm}}. Avant de procéder à la configuration à l'aide de l'interface utilisateur ou de l'API, exécutez les étapes suivantes :

1. Cliquez sur l'application {{site.data.keyword.sdk4nodefull}} dans le tableau de bord {{site.data.keyword.Bluemix_notm}}.
2. Cliquez sur **Variables d'environnement** dans la barre de navigation.
3. Copiez les données JSON affichées dans un fichier texte temporaire. Les données JSON doivent se présenter dans le format suivant :
```
{
  "SingleSignOn": [
    {
        "name": "ssoServiceTest",
        "label": "SingleSignOn",
        "plan": "standard"
        "credentials": {
          "secret": "string",
          "tokenEndpointUrl": "string",
          "authorizationEndpointUrl": "string",
          "issuerIdentifier": "string",
          "clientId": "string",
          "serverSupportedScope": [
              "openid"
          ]
        }
    }
}
```

### Configuration de {{site.data.keyword.iot_short_notm}} pour {{site.data.keyword.ssoshort}} à l'aide de l'interface utilisateur

1. Ouvrez le tableau de bord {{site.data.keyword.iot_short_notm}}.
2. Cliquez sur **Extensions** dans la barre de navigation.
3. Cliquez sur **Configurer** sous l'icône {{site.data.keyword.ssoshort}}.
4. Entrez les données de configuration à partir du fichier texte temporaire dans les zones clientID, secret et issuerIdentifier.
5. Cliquez sur **Terminé**.

### Configuration de {{site.data.keyword.iot_short_notm}} pour {{site.data.keyword.ssoshort}} à l'aide de l'API

Pour configurer votre instance {{site.data.keyword.iot_short_notm}} pour {{site.data.keyword.ssoshort}} à l'aide de l'API, vous devez utiliser la méthode `POST` et l'URL `https://<orgID>.internetofthings.ibmcloud.com/api/v0002/authentication/ssoconfig` où `<orgID>` est l'ID de votre organisation {{site.data.keyword.iot_short_notm}}. Vous devez utiliser l'autorisation No Auth ou Basic Auth à l'aide de l'ID et du jeton de votre clé d'API. Le corps doit contenir les données de configuration `secret`, `clientId` et `issuerIdentifier` comme les données JSON au format suivant :
```
{
 "secret": "myclientpwd",
 "clientId": "myclientid",
 "issuerIdentifier": "mybmssoinstance.iam.ibmcloud.com"
}
```

Le statut 200 est renvoyé si l'appel d'API a abouti.
