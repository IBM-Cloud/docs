---

Copyright : 2015, 2016
  
---

# Configuration de {{site.data.keyword.amashort}} pour l'authentification personnalisée
{: #custom-dash}
Pour utiliser l'authentification personnalisée avec votre appli mobile, vous devez enregistrer un domaine d'authentification personnalisé et l'adresse URL de base de votre fournisseur d'identité personnalisé dans le tableau de bord du service {{site.data.keyword.amashort}}.

## Avant de commencer
{: #custom-dash-begin}
* Lisez la rubrique [Initiation](getting-started.html).
* Protégez votre application de back end avec le SDK serveur de {{site.data.keyword.amashort}}.  Pour plus d'informations, voir la rubrique [Protection des ressources](protecting-resources.html).
* Une application de fournisseur d'identité personnalisée doit être active.

## Configuration de l'authentification personnalisée dans le tableau de bord {{site.data.keyword.Bluemix}}
{: #custom-dash-config}
Utilisez le tableau de bord {{site.data.keyword.amashort}} pour configurer l'authentification personnalisée.

1. Ouvrez votre appli dans le tableau de bord {{site.data.keyword.Bluemix}}.

1. Cliquez sur **Options pour application mobile** et notez la valeur de **Route** (`applicationRoute`)
et **Identificateur global unique de l'application** (`applicationGUID`). Vous aurez besoin de ces valeurs lors de l'initialisation du SDK.

1. Cliquez sur la vignette {{site.data.keyword.amashort}}. Le tableau de bord {{site.data.keyword.amashort}} se charge.

1. Cliquez sur la vignette **Personnalisé**.

1. Entrez le **Nom de domaine** et l'**URL de base** de votre fournisseur d'identité personnalisé et sauvegardez vos modifications.

## Etapes suivantes
{: #next-steps}
* [Configuration de l'authentification personnalisée pour Android](custom-auth-android.html)
* [Configuration de l'authentification personnalisée pour iOS](custom-auth-ios.html)
* [Configuration de l'authentification personnalisée pour Cordova](custom-auth-cordova.html)
