---

copyright:

years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# API
{: #api_overview}

Plusieurs API sont disponibles à des fins de développement de code pour les terminaux, les passerelles et les applications qui se connectent à {{site.data.keyword.iot_full}}.

Les API HTTP sont protégés via l'authentification de base HTTP. Lorsque vous générez une clé d'API à l'aide du tableau de bord, une clé et un jeton d'authentification s'affichent. Pour plus d'informations sur les clés d'API et les jetons, voir [Connexion de clé d'API](../platform_authorization.html#api-key).


## A propos des API HTTP
{: #api_about}

Après vous être enregistré auprès de votre propre organisation, vous recevez un ID d'organisation composé de 6 caractères qui est requis dans le nom d'hôte pour tout appel API HTTP. L'URL de base de votre organisation est accessible à l'adresse suivante :

https://<**orgId**>.internetofthings.ibmcloud.com/api/v0002

Pour authentifier les demandes émises vers l'API d'application, affectez la clé d'API au nom d'utilisateur et le jeton d'authentification au mot de passe.

Pour les API de messagerie, utilisez l'adresse suivante :

https://<**orgId**>.messaging.internetofthings.ibmcloud.com/api/v0002

## API HTTP
{: #api_http}

API                     | A utiliser pour...       
------------- | -------------
[Administration des organisations ![Icône de lien externe](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/orgAdmin.html){: new_window} | Configurer  une organisation (y compris la création et la suppression de terminaux), vérifier l'utilisation, le statut de service, et diagnostiquer les problèmes de connexion.
[Sécurité ![Icône de lien externe](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/security.html){: new_window} | Gérer les invitations et l'authentification des utilisateurs, l'autorisation d'utilisateur, les clés d'API et les terminaux.
[Gestion des informations ![Icône de lien externe](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/info-mgmt.html){: new_window} |  Accéder aux données d'événement de terminal et obtenir et mettre à jour des emplacements de terminal et obtenir des informations météorologiques pour ces emplacements. **Remarque :** Les informations météorologiques dépendent de l'intégration des données de The Weather Company.
[The Weather Company ![Icône de lien externe](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/info-mgmt.html#!/Device_Location_Weather){: new_window} | Intégrer des données provenant de Weather Company à vos terminaux existants.
[Gestion des terminaux ![Icône de lien externe](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/deviceMgmt.html){: new_window} | Interagir avec des terminaux gérés à l'aide du protocole de gestion des terminaux.
[Messagerie ![Icône de lien externe](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/http-messaging.html){: new_window}   | Publier des événements et envoyer des commandes à l'aide de HTTP.



## API HTTP d'extension
{: #api_extension}

API                     | A utiliser pour...       
------------- | -------------
[Extension AT&T ![Icône de lien externe](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/ext-atnt.html){: new_window} | Administrer des terminaux AT&T.
[Extension Jasper ![Icône de lien externe](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/ext-jasper.html){: new_window} | Administrer des terminaux Jasper.
[Extension Orange ![Icône de lien externe](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/ext-orange.html){: new_window} | Afficher les données de carte SIM à partir des terminaux qui sont connectés à votre organisation {{site.data.keyword.iot_short_notm}} et exécuter l'installation d'une carte SIM Orange.

## API HTTP bêta
{: #api_beta}

API                     | A utiliser pour...       
------------- | -------------
[Sécurité de passerelle ![Icône de lien externe](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-gateway-beta.html){: new_window}   | Vérifier et affecter des rôles à des terminaux de passerelle.
[Sécurité de terminal ![Icône de lien externe](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-devices-beta.html){: new_window} | Vérifier et affecter des rôles à des terminaux.
[Mappage d'interface ![Icône de lien externe](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html){: new_window}   |   Mapper et accéder à des données de terminal à l'aide d'interfaces.
