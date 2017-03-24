---

copyright:
  years: 2017
lastupdated: "2017-03-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Configuration des fournisseurs d'identité
{: #setting-up-idp}

Vous pouvez configurer Facebook, Google, ou les deux, pour authentifier vos applications et autoriser l'accès aux ressources de back-end protégées.
{:shortdesc}


## Facebook
{: #facebook}

Configurez le service {{site.data.keyword.appid_short}} pour utiliser Facebook comme fournisseur d'identité.

<!--- ### Sequence diagram
{: #facebook-sequence-diagram}--->

### Obtention d'un ID et d'une valeur confidentielle d'application auprès de Facebook
{: #getting-facebook-appid}

Pour utiliser Facebook comme fournisseur d'identité sur vos applications mobiles ou Web, vous devez ajouter et configurer la plateforme de site Web sur votre application Facebook.

1. Connectez-vous à votre compte sur le site Facebook for Developers. Pour plus d'informations sur la création d'une nouvelle application Facebook, voir <a href="https://developers.facebook.com/docs/apps/register" target="_blank">Creating an application<img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.
2. Notez l'ID et la valeur confidentielle de l'application Facebook. Vous aurez besoin de ces informations pour configurer votre projet Web pour authentification dans votre tableau de bord du service.
3. Ajoutez la plateforme Web et indiquez l'URL du site.
4. Dans la liste des produits, sélectionnez **Facebook Login**.
5. Dans la zone des URL de redirection OAuth valides, entrez l'URL de noeud final de rappel du serveur d'autorisation. Vous pouvez ajouter cette valeur après avoir configuré votre service {{site.data.keyword.appid_short_notm}} dans les étapes suivantes.
6. Cliquez sur **Sauvegarder les modifications**.

### Configuration de {{site.data.keyword.appid_short_notm}} pour l'authentification Facebook
{: #configuring-facebook-appid}

Une fois que vous disposez de votre ID et de votre valeur confidentielle d'application Facebook et que votre application Facebook for Developers est configurée pour servir des clients Web, vous pouvez éditer l'authentification Facebook depuis votre tableau de bord de service.

1. Depuis l'onglet **Gérer** de votre tableau de bord de service, sélectionnez **Facebook** et cliquez sur **Editer**.
2. Entrez l'ID et la valeur confidentielle d'application Facebook obtenus auprès du site Web Facebook for Developers.
3. Copiez l'URI mentionné dans la zone **URI de redirection pour Facebook for Developers**. Collez cet URI dans la zone **URI de redirection OAuth valides** de la section **Facebook Login** du portail des développeurs Facebook.
4. Cliquez sur **Sauvegarder**.
5. Facultatif : pour configurer l'authentification pour les applications Web, entrez l'URI de redirection dans la zone des URI de redirection de votre application Web. Cette valeur définie par le développeur est utilisée pour accéder à l'URI de redirection à l'issue du processus d'authentification.


## Google
{: #google}

Configurez le service {{site.data.keyword.appid_short_notm}} pour utiliser Google comme fournisseur d'identité.

<!--- ### Sequence diagram
{: #google-sequence-diagram}--->

### Obtention d'un ID client et d'une valeur confidentielle auprès de Google
{: #google-client-id}

Pour utiliser Google comme fournisseur d'identité, procurez-vous un ID client et une valeur confidentielle Google, puis créez un projet dans la console de développeur Google.

1. Ouvrez votre application dans la console de développeur Google.
2. Ajoutez l'API Google+.
3. Créez des données d'identification à l'aide d'OAuth. Dans la zone **Type d'application**, sélectionnez **Application Web**. Dans la zone des **URI de redirection autorisés**, entrez l'URI de redirection App ID. Vous pouvez identifier l'URI d'autorisation de redirection App ID depuis l'écran de configuration Google du tableau de bord du service.
4. Sauvegardez vos modifications. Notez l'ID client et la valeur confidentielle Google.




### Configuration de {{site.data.keyword.appid_short_notm}} pour l'authentification Google
{: #google-client-appid}

Une fois que vous disposez de votre ID et de votre valeur confidentielle Google et que votre console Google Developers est configurée pour servir les clients Web, vous pouvez éditer l'authentification Google depuis votre tableau de bord de service.

1. Depuis l'onglet **Gérer** de votre tableau de bord du service, sélectionnez **Google** et cliquez sur **Editer**.
3. Entrez l'ID client et la valeur confidentielle Google obtenus dans la console Google Developers.
4. Copiez l'URI mentionné dans la zone **URI de redirection pour Google for Developers**. Collez cet URI dans la zone **URI de redirection autorisés** sous l'entrée **Restrictions** de la section **ID client pour application Web** du portail des développeurs Google.
5. Cliquez sur **Sauvegarder**.
6. Facultatif : pour configurer l'authentification pour les applications Web, entrez l'URI de redirection dans la zone des URI de redirection d'application Web. Cette valeur définie par le développeur est utilisée pour accéder à l'URI de redirection à l'issue du processus d'authentification.



<!---[## Bring your own OAuth2/OIDC identity provider
{: #oauth2}

### About
{: #oauth2-about}
### Sequence diagram
{: #oauth2-sequence-diagram}
### Configuring AppID for BYOIDP OAuth2 authentication
{: #oauth2-appid} SHAWNA: Is this Interconnect?]--->
