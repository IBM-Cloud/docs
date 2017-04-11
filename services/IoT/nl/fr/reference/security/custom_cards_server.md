---

copyright:
  years: 2016, 2017
lastupdated: "2016-11-29"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Sécurisation du serveur de cartes personnalisées
{: #securing_custom_cards}

Les serveurs de cartes personnalisées sont des serveurs Web standard qui hébergent le code javascript de cartes personnalisées. Pour assurer l'intégrité de votre environnement {{site.data.keyword.iot_short_notm}}, vous devez sécuriser votre serveur de cartes personnalisées en exécutant les étapes de sécurisation des données source de carte décrites dans cette rubrique.
{:shortdesc}

**Important :** Actuellement, les cartes personnalisées sont fournies à titre expérimental et l'extension Cartes personnalisées est activée par session de navigation. La configuration de la connexion des cartes personnalisées et les packages de cartes ne sont pas partagés à l'échelle de votre organisation {{site.data.keyword.iot_short_notm}}.

## Exigences de rôle {{site.data.keyword.Bluemix_notm}}
{: #roles_requirements}

Vous devez disposez des droits d'administrateur {{site.data.keyword.iot_short_notm}} pour créer une connexion à un serveur de cartes personnalisées.

## Remarques relatives à la sécurité du serveur de cartes personnalisées
{: #server_requirements}

Les exigences suivantes sont définies par {{site.data.keyword.iot_short_notm}} :
- L'accès au répertoire qui prend en charge le contenu de carte personnalisée sur le serveur ne doit pas nécessiter de données d'identification.  
Aucune authentification n'est fournie au serveur de cartes personnalisées lors de l'établissement de la connexion pour l'accès et le chargement des cartes personnalisées.
- Le serveur doit utiliser le protocole HTTPS.
- Le serveur doit prendre en charge les connexions de partage de ressources d'origine croisée.  

La protection du code de cartes personnalisées et du serveur de cartes proprement dit nécessite que ce dernier soit localisé et sécurisé à l'aide d'une défense en profondeur. Cela inclut la protection via un pare-feu afin de restreindre l'accès au serveur de cartes personnalisés.

Le traitement de cartes personnalisées s'effectue toujours entre le navigateur d'un utilisateur et le serveur de cartes personnalisées. Le service {{site.data.keyword.iot_short_notm}} de back end n'est jamais impliqué dans le traitement ou l'ajustement des informations et du code de cartes personnalisées.

Il n'existe aucune restriction sur le code JavaScript que vous choisissez de déployer dans vos cartes sur le serveur de cartes personnalisées. Le code Javascript des cartes personnalisées a accès à toutes les informations contenues dans le navigateur, tout comme n'importe quelle autre carte qui s'exécute sur le tableau de bord.  Assurez-vous que le code est fourni au navigateur par le bon serveur de cartes personnalisées pour l'affichage et le traitement des cartes personnalisées.

Les cartes exécutent leur code dans votre session de navigation {{site.data.keyword.iot_short_notm}} exactement tel qu'il est écrit. De plus, la connexion au serveur de cartes personnalisées est créée sans qu'aucune donnée d'identification ne soit communiquée au serveur de cartes personnalisées. Le navigateur d'un utilisateur peut se connecter à n'importe quel serveur de cartes personnalisées configuré.

Il est essentiel de configurer uniquement des serveurs de cartes personnalisées connus et sécurisés pour fournir des cartes personnalisées aux tableaux de bord de vos utilisateurs.   
