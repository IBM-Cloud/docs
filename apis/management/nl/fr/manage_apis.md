---

copyright:
  years: 2017
lastupdated: "2017-04-13"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Gestion des API
{: #manage_apis}

Après avoir intégré votre API afin de la gérer et de la surveiller grâce au système de gestion d'API, vous pouvez afficher et modifier ses paramètres. Si vous n'avez pas intégré votre API, vous devez en intégrer une en procédant comme indiqué dans [Création d'API à partir d'actions {{site.data.keyword.openwhisk_short}}](manage_openwhisk_apis.html). 

Pour gérer les paramètres de votre API, procédez comme suit : 

Si vous avez créé une API, et qu'elle est déjà ouverte dans l'interface, vous pouvez ignorer les trois premières étapes. 

1. Sélectionnez l'API que vous souhaitez gérer en choisissant une action sur le tableau de bord du service {{site.data.keyword.openwhisk_short}}, si les informations de votre API ne sont pas déjà affichées.
2. Si nécessaire, sélectionnez l'onglet **APIs**. 
3. Si nécessaire, sélectionnez l'API à gérer. Une fois la connexion établie, vous pouvez afficher et mettre à jour les sélections suivantes : 
    * Summary
    * Definition
    * Sharing
    * API Explorer
4. Sélectionnez le curseur Expose Managed API pour l'activer et exposer votre API. Remarque : Il n'est pas possible de définir certains paramètres lorsque l'API n'est pas exposée.  

## Récapitulatif des paramètres des API
{: #overview_api}

L'onglet Summary est sélectionné par défaut lorsque vous choisissez une API ; il comporte deux sections :
* Properties - La section Properties affiche les informations suivantes :
    * Informations de base sur l'API
	* Règles de sécurité
	* Informations sur les limites de fréquence
    * Détails du partage
* Analytics and Logging - La section Analytics and Logging affiche les statistiques suivantes : 
	* Nombre de réponses et temps de réponse moyen au cours du dernier intervalle de temps que vous indiquez 
    * Nombre d'appels API par minute, au format graphique
    * 100 dernières réponses dans un tableau de journal des réponses (Response Log) 
	
Le graphique *Responses* illustre rapidement le nombre de réponses reçues par votre API, ainsi que la répartition du statut des réponses. Cela peut vous aider à savoir si vous recevez une majorité de réponses d'erreur. Une majorité de réponses d'erreur peut signifier que votre trafic est plus important que ce que vous avez autorisé dans les paramètres de fréquence. Pour afficher la répartition numérique des réponses par code de réponse, survolez l'icône d'information. Voici les codes de réponse courants : 
* 200  OK
* 201  Created (Créé)
* 302  Found (Trouvé)
* 304  Not Modified (Non modifié)
* 400  Bad Request (Demande incorrecte)
* 401  Unauthorized (Non autorisé)
* 403  Forbidden (Interdit)
* 500  Internal Server Error (Erreur de serveur interne)
* 503  Service Unavailable (Service non disponible)

Le tableau Response Log contient les détails des 100 dernières réponses. Vous pouvez trier ces informations selon les entrées d'une colonne en sélectionnant l'en-tête de colonne approprié. Vous pouvez rechercher des entrées spécifiques dans le tableau Response Log à l'aide de la barre *Search responses*. Si vous souhaitez avoir davantage d'informations sur un événement, sélectionnez-le ou sélectionnez **View Details** dans le menu de liste des options (trois points verticaux) situé en regard de l'entrée concernée.


## Edition des paramètres d'API
{: #settings_api}

Dans l'onglet **Definition**, vous pouvez mettre à jour les informations de base concernant votre API. Ces informations incluent la documentation, le nom et l'URL de base. Utilisez la section Security and Rate Limiting pour indiquer un appel et une limite d'intervalle afin de veiller à ce que seul un certain nombre d'appels soient effectués par seconde, par minute ou par heure. Vous pouvez également demander une authentification lors de la création d'appels d'API afin d'empêcher toute utilisation non voulue de vos données, ou pour rassembler des statistiques sur l'API.

Pour modifier les paramètres d'une API, procédez comme suit : 

1. Dans le tableau de bord de gestion de l'API, cliquez sur l'onglet **Definition**. 
2. Vous pouvez nommer ou mettre à jour le nom de votre API et importer une définition d'API dans la section API Info.
3. La section Security and Rate Limiting vous permet de mettre à jour les règles suivantes : 
    * Require API key - Indique si l'appel API doit être traité uniquement si la clé d'API correcte est fournie. La valeur par défaut ne requiert pas de clé supplémentaire. 
    * Security method - Lorsque l'option de clé d'API est sélectionnée, indique si le traitement de l'API requiert uniquement la clé d'API, ou s'il nécessite la clé d'API et la valeur confidentielle de l'API. 
    * Location of the API key and secret - En fonction des paramètres de la méthode, indique la manière dont les informations de sécurité de votre API sont incluses dans l'appel. Les noms d'appel précisent le mode d'identification des informations de sécurité. 
    * Limit API call rate - Définit le nombre d'appels API autorisés pendant un intervalle de temps spécifié ; vous pouvez définir ce nombre pour chaque clé. Notez que le type burst-type de la méthode rate-limiting est utilisé. La fréquence moyenne des appels d'API est calculée pendant la durée totale de l'intervalle de temps que vous indiquez dans la fréquence. Si la fréquence des appels API pendant un intervalle excède la fréquence moyenne des appels API, les appels peuvent être refusés pendant un certain temps, jusqu'à la limite de durée indiquée dans la fréquence.    
    * OAuth provider - Permet de s'assurer que seuls les utilisateurs dotés des paramètres de sécurité corrects peuvent accéder à vos API grâce à la mise en place d'OAuth pour les données d'identification de connexion aux réseaux sociaux des fournisseurs, tels que Google, Facebook, IBM et GitHub.
4. Enable CORS - Cross-origin requests (CORS) active certaines demandes limitées provenant d'un autre domaine. 
5. Cliquez sur **Save**.

## Partage des API
{: #share_api}

Vous pouvez partager des API avec d'autres utilisateurs dans ou en dehors de votre organisation {{site.data.keyword.Bluemix_notm}}.

Lorsque vous partagez vos API avec d'autres, dans ou en dehors de votre organisation {{site.data.keyword.Bluemix_notm}}, vous pouvez créer des clés pour vos API. Chaque API gérée prend en charge 5 clés qui peuvent être créées et affectées à cette API. En envoyant une clé unique à un individu ou une société, vous pouvez suivre certaines statistiques sur le mode d'utilisation de l'API. Vous pouvez ainsi connaître le nombre d'appels envoyés à votre API par cette personne ou cette société. 

Vous pouvez également désactiver une clé ou limiter le nombre d'appels provenant d'une clé. Cela peut s'avérer utile pendant les tests, l'équilibrage de charge et la monétisation, ou lors de la résolution de certains problèmes liés à la sécurité.   

1. Dans le tableau de bord de gestion de l'API, cliquez sur l'onglet **Sharing**. 
2. Dans la section Sharing within {{site.data.keyword.Bluemix_notm}} Organization, sélectionnez **Share API with all users in my Bluemix organization** si vous voulez rendre votre API disponible pour d'autres personnes avec un accès à votre organisation {{site.data.keyword.Bluemix_notm}}. Vous devez sélectionner cette option pour générer une clé. 
3. Cliquez sur **Create API Key** afin de créer une clé unique pour votre API. La boîte de dialogue Create API Key s'affiche. La clé d'API est générée automatiquement.
4. Utilisez la clé d'API pour savoir quel utilisateur accède à l'API en envoyant à un utilisateur une clé unique. La passerelle peut savoir quelle la clé (et quel client) génère l'appel. 
5. Cliquez sur l'icône **Menu** (trois points verticaux) en regard de la clé pour éditer ou supprimer cette clé d'API.

La section Sharing Outside of {{site.data.keyword.Bluemix_notm}} Organization vous permet de partager votre API avec des utilisateurs qui ne disposent pas d'un compte {{site.data.keyword.Bluemix_notm}}. Cette méthode de partage fournit un lien direct qui permet d'affiche les informations concernant votre API dans l'explorateur d'API. L'API contient un bouton permettant de l'exécuter dans la vue API Explorer. Pour demander un lien vers votre API, procédez comme suit :

1. Dans la section Sharing Outside of {{site.data.keyword.Bluemix_notm}} Organization, cliquez sur **Create API Key**. La boîte de dialogue Create API Key s'affiche. Vous remarquerez que l'utilisateur dispose d'une valeur confidentielle que vous ne contrôlez pas. 
2. Indiquez un nom unique pour la clé d'API.
3. Sélectionnez **Create key**. 
4. Envoyez le lien API Portal Link au client qui ne dispose pas d'un compte {{site.data.keyword.Bluemix_notm}}. La clé d'API et la valeur confidentielle (le cas échéant) sont incluses dans le lien ; vous pouvez ainsi déterminer quelle clé a généré le lien. 
  
Le lien de la documentation de l'API ouvre l'API dans l'onglet **API Explorer**.

## Affichage et test dans l'explorateur d'API
{: #explore_api}

Sélectionnez l'onglet API Explorer pour afficher le html généré à partir de votre document Swagger.  

L'explorateur d'API affiche toutes les actions et la documentation de l'API qui s'appliquent à l'API. Vous pouvez afficher les opérations et les actions, ainsi que leur description, et tester l'API à partir de l'interface utilisateur. Vous pouvez également télécharger le document Swagger afin de réutiliser son contenu. 

Pour tester l'API, procédez comme suit :
1. *Examples* est sélectionné par défaut. Il s'agit d'un exemple du code de l'API sélectionnée. 
2. Modifiez le format de l'exemple, si nécessaire, en sélectionnant un langage dans le menu situé en regard du langage indiqué. 
3. Sélectionnez **Try it**.
4. Sélectionnez **Call operation**. 

La réponse à la question s'affiche.   
