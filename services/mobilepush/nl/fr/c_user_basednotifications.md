---

Titre : Activation des notifications push basées sur les utilisateurs

Mots clé : Notifications push basées sur les utilisateurs, userId
copyright:
 years: 2015, 2016

---

# Activation des notifications utilisateur
{: #user_based_notifications}
Dernière mise à jour : 16 août 2016
{: .last-updated}

Les notifications de type {{site.data.keyword.mobilepushshort}} basées sur les utilisateurs sont envoyées vers les utilisateurs d'applications mobiles avec des messages personnalisés. Les notifications basées sur les utilisateurs peuvent aider et pousser certains individus spécifiques à tirer profit de leurs préférences et choix personnels.  

## Enregistrement du périphérique avec l'ID utilisateur
Pour activer les notifications push ciblées par ID utilisateur, prenez soin d'enregistrer le périphérique avec un ID utilisateur et passez aussi la valeur confidentielle clientSecret qui est allouée quand les services {{site.data.keyword.mobilepushshort}} sont provisionnés. L'enregistrement du périphérique échouera en l'absence d'une valeur clientSecret valide.  

L'ID utilisateur peut être toute chaîne fournie par l'application à l'API d'enregistrement de périphérique. En général, une application mobile exécute d'abord un cycle d'authentification au cours duquel l'utilisateur d'application mobile est authentifié auprès d'un service d'authentification comme [{{site.data.keyword.amafull}}](https://console.ng.bluemix.net/docs/services/mobileaccess/index.html). Si l'authentification aboutit, l'ID de l'utilisateur authentifié est alors transféré vers l'API d'enregistrement de périphérique Push en même temps qu'une valeur confidentielle clientSecret. La présence de cette valeur a pour effet que seules les associations autorisées entre les ID utilisateur et les enregistrements de périphériques mobiles sont appliquées.

Préservez la confidentialité de clientSecret et ne procédez jamais à un codage en dur dans l'application mobile. Il existe différents modèles d'initialisation d'application qui peuvent être utilisés pour extraire dynamiquement la valeur confidentielle clientSecret durant l'application. Le diagramme de séquence décrit ce modèle.

![Enable_Push](images/init_client_secret.jpg) 

Vous pouvez aussi enregistrer un périphérique pour qu'il soit associé à un utilisateur anonymous, ce qui demande l'utilisation d'une variante de l'API d'enregistrement de périphérique qui ne requiert pas d'arguments ID utilisateur et clientSecret.   

## Synchronisation de la connexion/déconnexion utilisateur et activation des notifications push 

Vous pouvez choisir de n'envoyer des notifications que si l'utilisateur est connecté. 

Supposez par exemple qu'un périphérique est partagé par une famille ou par une équipe au travail et que vous voulez vous adresser à des utilisateurs spécifiques de la famille ou de l'équipe. Dans un tel cas, il y aura une séquence de connexion/déconnexion qui empêchera l'application d'effectuer un suivi de l'identité de l'utilisateur actuel de l'application. Pour vous assurer que les notifications qui sont envoyées à un utilisateur spécifique ne sont toujours reçues que par cet utilisateur uniquement, invoquez l'API d'enregistrement de périphérique en passant l'ID utilisateur de l'utilisateur connecté. De la même façon, avant de vous déconnecter, appelez l'API de désenregistrement du périphérique. Le séquencement de ces API Push avec les opérations de connexion et de déconnexion garantit que les notifications push qui sont destinées à un utilisateur spécifique ne sont envoyées qu'à cet utilisateur uniquement.
