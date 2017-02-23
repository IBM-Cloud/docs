---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-03"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Identification et résolution des problèmes liés à {{site.data.keyword.iot_short_notm}}
{: #ts}

Voici les réponses aux questions fréquentes sur l'identification et la résolution des problèmes liés à l'utilisation d'{{site.data.keyword.iot_full}} sur {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

## Problème lors de l'accès à votre organisation {{site.data.keyword.iot_short_notm}}
{: #access-expiry-problem}

Vous ne pouvez pas vous connecter à une organisation {{site.data.keyword.iot_short_notm}} dont vous êtes propriétaire.
{:shortdesc}

Vous ne pouvez pas vous connecter à votre organisation {{site.data.keyword.iot_short_notm}} directement en utilisant l'URL de l'organisation ou en utilisant `https://internetofthings.ibmcloud.com`.
{: tsSymptoms}

Votre accès à votre organisation {{site.data.keyword.iot_short_notm}} est peut-être arrivé à expiration. Les organisations {{site.data.keyword.iot_short_notm}} qui ont été créées à l'aide de {{site.data.keyword.Bluemix}} utilisent des profils utilisateur temporaires par défaut.
{: tsCauses}

Vous pouvez résoudre ce problème en accédant à votre organisation {{site.data.keyword.iot_short_notm}} à l'aide de {{site.data.keyword.Bluemix_notm}} et en modifiant les paramètres d'expiration de votre profil utilisateur. Pour modifier les paramètres d'expiration de votre profil utilisateur :

1. Dans votre tableau de bord {{site.data.keyword.Bluemix_notm}}, ouvrez votre service {{site.data.keyword.iot_short_notm}}. 
2. Cliquez sur **Membres** dans la barre de navigation. 
3. Cliquez sur l'icône **Editer**.
4. Désélectionnez la zone **L'accès arrive à expiration** et cliquez sur **Sauvegarder**.
{: tsResolve}

## Problème lors de la connexion à {{site.data.keyword.iot_short_notm}}
{: #connection_problem}

Votre connexion à {{site.data.keyword.iot_short_notm}} s'interrompt de manière inattendue.
{:shortdesc}

Lorsque vous tentez de vous connecter à {{site.data.keyword.iot_short_notm}}, une erreur s'affiche sur votre terminal ou votre application.
{: tsSymptoms}

Il est possible que deux terminaux tentent de se connecter avec le même ID de client et les mêmes données d'identification. Une seule connexion unique est autorisée par ID de client. Vous ne pouvez pas avoir deux connexions simultanées utilisant le même ID. Les applications peuvent partager la même clé d'API, mais MQTT requiert que l'ID de client soit toujours unique.
{: tsCauses}

Pour résoudre ce problème, vous pouvez vérifier que deux terminaux ne tentent pas de se connecter en utilisant les mêmes données d'identification.
{: tsResolve}

## Déconnexion par intermittence d'un terminal à {{site.data.keyword.iot_short_notm}}
{: #disconnection_problem}

La connexion de votre terminal à {{site.data.keyword.iot_short_notm}} s'interrompt par intermittence de manière inattendue.
{:shortdesc}

Un terminal connecté au service {{site.data.keyword.iot_short_notm}} est déconnecté par intermittence. Il se reconnecte, mais il est de nouveau déconnecté de manière inattendue au bout d'un certain temps.
{: tsSymptoms}

Il se peut que lorsque vous vous connectez, vous utilisiez une valeur trop faible pour une option de commande ping MQTT, ce qui peut donner l'impression qu'un dépassement de délai d'attente s'est produit pour la connexion. Par exemple, si MQTT client est défini de manière incorrecte, les commandes ping ne sont pas reçues à temps, et la connexion prend fin.
{: tsCauses}

Pour résoudre ce problème, vous pouvez vérifier que vous avez correctement défini les paramètres ping et KeepAlive pour votre connexion.   
{: tsResolve}


## Aide et support pour {{site.data.keyword.iot_short_notm}}
{: #gettinghelp}

Si vous avez des problèmes ou de questions quand vous utilisez {{site.data.keyword.iot_short_notm}}, vous pouvez obtenir de l'aide en recherchant des informations précises ou en posant des questions via un forum. Vous pouvez également ouvrir un ticket de demande de service.

Si vous utilisez les forums pour poser une question, libellez votre question de sorte qu'elle soit vue par les équipes de développement {{site.data.keyword.Bluemix_notm}}.

* Si vous avez des questions techniques concernant le développement ou le déploiement d'une application avec {{site.data.keyword.iot_short_notm}}, publiez-les sur [Stack Overflow ![](../../icons/launch-glyph.svg)](http://stackoverflow.com/search?q=watson-iot+ibm-bluemix){:new_window} et ajoutez les étiquettes "ibm-bluemix" et "watson-iot".
<!--Insert the appropriate dW Answers tag for your service for <service_keyword> in URL below:  -->
* Pour des questions relatives au service et aux instructions de mise en route, utilisez le forum [IBM developerWorks dW Answers ![](../../icons/launch-glyph.svg)](https://developer.ibm.com/answers/topics/watson-iot/?smartspace=bluemix){:new_window}. Ajoutez les étiquettes "watson-iot" et "bluemix".

Voir la rubrique décrivant [comment obtenir de l'aide![](../../icons/launch-glyph.svg)](https://www.{DomainName}/docs/support/index.html#getting-help){: new_window} pour plus d'informations sur l'utilisation des forums. 

Pour plus d'informations sur l'ouverture d'un ticket de demande de service IBM, sur les niveaux de support disponibles ou les niveaux de gravité des tickets, voir la rubrique décrivant [comment contacter le support![](../../icons/launch-glyph.svg)](https://www.{DomainName}/docs/support/index.html#contacting-support){: new_window}.
