---

copyright:
  years: 2016
lastupdated:  "2016-11-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Initiation à {{site.data.keyword.mobilefoundation_short}}
{: #gettingstartedtemplate}

{{site.data.keyword.mobilefoundation_long}} accélère la
configuration d'un environnement {{site.data.keyword.mfp_full}} qui
vous permet de développer, tester et faire fonctionner des applications mobiles
d'entreprise. {{site.data.keyword.mobilefoundation_short}} est
disponible dans deux plans de service différents : Developer et
Professional 1 Application.
{:shortdesc}

<!-- The Professional 1 Application plan allows the {{site.data.keyword.mobilefoundation_short}} server to be deployed on a scalable container group.--> Grâce au plan Professional 1 Application, vous pouvez
gérer une application unique créée sur l'une quelconque ou l'ensemble des plateformes d'exploitation prises
en charge, comme Android, iOS, Windows ou Web mobile. Le plan Developer <!-- does not support {{site.data.keyword.mobilefoundation_short}} deployment on a container group with more than 1 node. This plan --> convient particulièrement au développement et au test.

## Initiation au plan {{site.data.keyword.mobilefoundation_short}}: Developer

Après avoir créé une instance de
{{site.data.keyword.mobilefoundation_short}}: Developer, vous pouvez
commencer à générer votre canal d'accès mobile en quelques clics.

*	Pour créer une instance de serveur
{{site.data.keyword.mobilefirst_notm}} avec la configuration par
défaut, cliquez sur **Start Basic Server**.

  `L'instance de serveur de base est dotée d'un seul noeud, d'1 Go de mémoire.`

* Pour créer une instance de serveur
{{site.data.keyword.mobilefirst_notm}} avec la configuration avancée de
la topologie, de la sécurité et d'autres paramètres de configuration du
serveur, cliquez sur **Start Server with Advanced
Configuration**. Pour
plus d'informations, voir
[Paramétrage
d'une configuration avancée](c_using_mfs_p1.html#using_mfs_advanced_p1).

## Initiation au plan {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application

Après avoir créé une instance du service
{{site.data.keyword.mobilefoundation_short}}: Professional 1
Application, vous pouvez commencer à générer votre canal d'accès mobile en
procédant comme suit :

1.  Connectez-vous à un service
{{site.data.keyword.dashdbshort}}: Enterprise Transactional
existant sur {{site.data.keyword.Bluemix_notm}}.

    1.  Sélectionnez l'{{site.data.keyword.Bluemix_notm}} `organisation` dans laquelle l'instance de service {{site.data.keyword.dashdbshort_notm}} existe.

    + Depuis la liste des espaces disponibles dans `Organisation`, sélectionnez l'élément `Espace` {{site.data.keyword.Bluemix_notm}} dans lequel se trouve l'instance de service {{site.data.keyword.dashdbshort_notm}},

    + Sélectionnez également le nom du service (`Service
Name`) et les données d'identification
(`Credentials`) {{site.data.keyword.dashdbshort_notm}}
pour la connexion à l'instance de service
{{site.data.keyword.dashdbshort_notm}}.

    + Testez la connexion à l'instance de service
{{site.data.keyword.dashdbshort_notm}}: Enterprise Transactional
sélectionnée en cliquant sur **Test Connection**.

    + Cliquez sur **Add**, puis sur
**Continue** dans la fenêtre en incrustation vous demandant
de confirmer la sélection du service {{site.data.keyword.dashdbshort_notm}}. Cela permet de créer les tables requises dans l'instance de service de base de
données {{site.data.keyword.dashdbshort_notm}} configurée.

    **Remarque :** Une fois que vous avez ajouté une connexion {{site.data.keyword.dashdbshort_notm}} à l'instance {{site.data.keyword.mobilefoundation_short}}, vous ne pouvez plus la modifier.

2.  Créez et démarrez le serveur.

    * Pour créer une instance de serveur
{{site.data.keyword.mobilefirst_notm}} avec la configuration par
défaut, cliquez sur **Start Basic Server**.

      `L'instance de serveur de base est dotée d'un seul noeud, d'1 Go de mémoire.`

    * Pour créer une instance de serveur
{{site.data.keyword.mobilefirst_notm}} avec la configuration avancée de
la topologie, de la sécurité et d'autres paramètres de configuration du
serveur, cliquez sur **Start Server with Advanced
Configuration**. Pour plus d'informations, voir
[Paramétrage d'une
configuration avancée](c_using_mfs_p2.html#using_mfs_advanced_p2).

Accédez à la page [Using the Mobile Foundation service to set up MobileFirst Server<!-- on IBM Containers-->](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/bluemix/using-mobile-foundation/) pour vous initier à {{site.data.keyword.mobilefoundation_short}}.

##  Limitations connues

* L'interface utilisateur du service {{site.data.keyword.mobilefoundation_short}} n'utilise pas le modèle spécifique à l'environnement local sélectionné par l'utilisateur pour l'affichage des nombres.


# Liens connexes
{: #rellinks}

## Liens connexes
{: #general}

*	[Documentation
du produit IBM MobileFirst Platform Foundation V8.0.0](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window}
*	[IBM MobileFirst Platform Developer Center](https://mobilefirstplatform.ibmcloud.com){: new_window}
