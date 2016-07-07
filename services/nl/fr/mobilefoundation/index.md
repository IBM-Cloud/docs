---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Initiation à {{site.data.keyword.mobilefoundation_short}}
{: #gettingstartedtemplate}

*Dernière mise à jour : 15 juin 2016*
{: .last-updated}

{{site.data.keyword.mobilefoundation_long}} accélère la
configuration d'un environnement {{site.data.keyword.mfp_full}} qui
vous permet de développer, tester et faire fonctionner des applications mobiles
d'entreprise. {{site.data.keyword.mobilefoundation_short}} est
disponible dans deux plans de service différents : Developer et
Professional 1 Application.
{:shortdesc}

Le plan Professional 1 Application permet de déployer le serveur
{{site.data.keyword.mobilefoundation_short}} sur un groupe de
conteneurs évolutif. Grâce au plan Professional 1 Application, vous pouvez
gérer une application unique créée sur l'une des plateformes d'exploitation prises
en charge, comme Android, iOS, Windows ou Web mobile. Le plan Developer ne
prend pas en charge le déploiement de
{{site.data.keyword.mobilefoundation_short}} sur un groupe de
conteneurs comportant plusieurs noeuds. Ce plan convient davantage au
développement et au test.

## Initiation au plan {{site.data.keyword.mobilefoundation_short}}: Developer

Après avoir créé une instance de
{{site.data.keyword.mobilefoundation_short}}: Developer, vous pouvez
commencer à générer votre canal d'accès mobile en quelques clics. 

*	Pour créer une instance de serveur
{{site.data.keyword.mobilefirst_notm}} avec la configuration par
défaut, cliquez sur **Start Basic Server**.

  `Cette instance est dotée d'un seul noeud, d'1 Go de mémoire et d'une capacité de stockage de
64 Go.`

* Pour créer une instance de serveur
{{site.data.keyword.mobilefirst_notm}} avec la configuration
avancée de la topologie, de la sécurité et d'autres paramètres de
configuration du serveur, cliquez sur **Start Server with Advanced Configuration**. Pour
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

    1.  Dans la liste des espaces disponibles de
l'`Organisation` en cours, sélectionnez
l'`Espace` {{site.data.keyword.Bluemix_notm}} dans
lequel l'instance de service {{site.data.keyword.dashdbshort_notm}}
existe.

    2.  Sélectionnez également le nom du service (`Service
Name`) et les données d'identification
(`Credentials`) {{site.data.keyword.dashdbshort_notm}}
pour la connexion à l'instance de service
{{site.data.keyword.dashdbshort_notm}}.

    3.  Testez la connexion à l'instance de service
{{site.data.keyword.dashdbshort_notm}}: Enterprise Transactional
sélectionnée en cliquant sur **Test Connection**.

    4.  Cliquez sur **Add**, puis sur
**Continue** dans la fenêtre en incrustation vous demandant
de confirmer la sélection du service {{site.data.keyword.dashdbshort_notm}}. 
Cela permet de créer les tables requises dans l'instance de service de base de
données {{site.data.keyword.dashdbshort_notm}} configurée. 

2.  Créez et démarrez le serveur.

    * Pour créer une instance de serveur
{{site.data.keyword.mobilefirst_notm}} avec la configuration par
défaut, cliquez sur **Start Basic Server**.

      `Cette instance est dotée d'un seul noeud, d'1 Go de mémoire et d'une capacité de stockage de
64 Go.`

    * Pour créer une instance de serveur
{{site.data.keyword.mobilefirst_notm}} avec la configuration avancée de
la topologie, de la sécurité et d'autres paramètres de configuration du
serveur, cliquez sur **Start Server with Advanced
Configuration**. Pour plus d'informations, voir
[Paramétrage d'une
configuration avancée](c_using_mfs_p2.html#using_mfs_advanced_p2).

Accédez à la page [Using the Mobile Foundation service to set up MobileFirst Server on IBM Containers](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/ibm-containers/using-mobile-foundation/) pour vous initier à {{site.data.keyword.mobilefoundation_short}}.

# Liens connexes
{: #rellinks}

## Liens connexes
{: #general}

*	[Documentation
du produit IBM MobileFirst Platform Foundation V8.0.0](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window}
*	[IBM MobileFirst Platform Developer Center](https://mobilefirstplatform.ibmcloud.com){: new_window}
