---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-11"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock: .codeblock}

# Services
{: #services}

La vue **Services** du tableau de bord {{site.data.keyword.Bluemix}} Mobile vous permet de visualiser vos services existants ou de créer de nouveaux services. Le tableau de bord Mobile est un emplacement unique qui permet d'afficher tous les services Bluemix gérés par les projets.  

Si vous supprimez des services de la vue **Services**, ces derniers sont déconnectés du projet qui leur est associé. Vous devez alors créer une nouvelle instance de service si vous voulez reconnecter le service au projet.

## Présentation des services {{site.data.keyword.Bluemix_notm}} Mobile
{: #mobile_services_overview}

Le tableau suivant décrit les services {{site.data.keyword.Bluemix_notm}} Mobile. Vous pouvez utiliser des services individuels depuis le catalogue {{site.data.keyword.Bluemix_notm}} ou les intégrer dans votre projet mobile.

<table summary="Ce tableau décrit les services {{site.data.keyword.Bluemix_notm}} Mobile et fournit des liens vers la documentation des services">
<caption>Tableau 1. Services {{site.data.keyword.Bluemix_notm}} Mobile</caption>
<th>Service {{site.data.keyword.Bluemix_notm}} Mobile</th>
<th>Description</th>
<tr>
<td> Icône du service <img src="images/mobile_analytics_icon.png" alt="{{site.data.keyword.mobileanalytics_short}} "><br/>{{site.data.keyword.mobileanalytics_short}}</td>
<td valign="top">Le service {{site.data.keyword.mobileanalytics_full}} permet d'obtenir plus de détails sur les performances et l'utilisation de vos applications mobiles.<br/><br/> Découvrez plus en détails le fonctionnement de ce service dans la <a href="/docs/services/mobileanalytics/index.html" alt="lien vers la documentation {{site.data.keyword.mobileanalytics_short}}">documentation {{site.data.keyword.mobileanalytics_short}}</a>.
</td>
</tr>
<tr>
<td><img src="images/authentication_icon.png" alt="icône du service {{site.data.keyword.amashort}}"><br/>{{site.data.keyword.amashort}}</td>
<td valign="top">Utilisez le service {{site.data.keyword.amafull}}  pour ajouter des fonctionnalités de sécurité à votre application mobile. Vous pouvez configurer l'authentification et les fournisseurs d'identité pour que les utilisateurs puissent se connecter dans l'application avec leurs comptes Google ou Facebook existants.<br/><br/>
Découvrez plus en détails le fonctionnement de ce service dans la <a href="/docs/services/mobileaccess/index.html" alt="lien vers la documentation {{site.data.keyword.amashort}}">documentation {{site.data.keyword.amashort}}</a>.</td>
</tr>
<tr>
<td><img src="images/MFPFoundation_icon.png" alt="icône du service {{site.data.keyword.mobilefoundation_short}}"><br/>{{site.data.keyword.mobilefoundation_short}}</td>
<td valign="top">Utilisez le service {{site.data.keyword.mobilefoundation_long}} pour accélérer la configuration d'un environnement {{site.data.keyword.mfp_full}} depuis lequel vous pouvez développer, tester et utiliser des applications mobiles d'entreprises.<br/><br/>
Découvrez plus en détails le fonctionnement de ce service dans la <a href="/docs/services/mobilefoundation/index.html" alt="lien vers la documentation {{site.data.keyword.mobilefoundation_short}}">documentation {{site.data.keyword.mobilefoundation_short}}</a>.</td>
</tr>
<tr>
<td><img src="images/mqa_icon.png" alt="icône du service {{site.data.keyword.mqa}}"><br/>{{site.data.keyword.mqa}}</td>
<td valign="top">Utilisez le service {{site.data.keyword.mqafull}} pour découvrir et configurer des services de qualité mobile pour vos applications. Vous pouvez afficher des mesures de qualité de haut niveau pour vos applications mobiles afin de pouvoir comprendre rapidement les problèmes des applications sur lesquelles vous travaillez. Ces mesures incluent des informations sur les pannes, les bogues, les commentaires des utilisateurs et leur sentiment. En prenant connaissance de ces informations, vous pouvez déterminer s'il est nécessaire d'analyser de façon plus approfondie certains problèmes spécifiques.<br/><br/>
Découvrez plus en détails le fonctionnement de ce service dans la <a href="/docs/services/MobileQualityAssurance/index.html" alt="lien vers la documentation {{site.data.keyword.mqa}}">documentation {{site.data.keyword.mqa}}</a>.</td>
</tr>
<tr>
<td>Icône du service <img src="images/push_icon.png" alt="{{site.data.keyword.mobilepushshort}} "><br/>{{site.data.keyword.mobilepushshort}}</td>
<td valign="top">Le service {{site.data.keyword.mobilepushfull}} fournit une plateforme unifiée pour envoyer et gérer des notifications push aux applications mobiles et de navigateur Web et ciblant plusieurs plateformes.
<br/><br/>
Le service {{site.data.keyword.mobilepushshort}} gère le mappage des utilisateurs de votre application à leurs périphériques, à la plateforme du périphérique, aux navigateurs Web et gère la distribution des notifications push à ceux-ci. Vous pouvez envoyer des diffusions, des monodiffusions (basées sur l'ID du périphérique et de l'utilisateur) et également sur des balises (ou des rubriques) sous forme de notifications push aux utilisateurs de votre application mobile et du navigateur Web. Vous pouvez également utiliser un SDK et des API REST pour développer davantage vos applications client.
<br/><br/>
Pour plus d'informations sur le fonctionnement de ce service, reportez-vous à la documentation <a href="/docs/services/mobilepush/index.html" alt="{{site.data.keyword.mobilepushshort}} lien vers la documentation">{{site.data.keyword.mobilepushshort}}</a>.</td>
</table>

## Intégration des services mobiles
{: #services_integration}
Vous pouvez intégrer vos services {{site.data.keyword.Bluemix_notm}} Mobile existants, comme {{site.data.keyword.cloudant}}, dans votre projet.


#### Intégration de {{site.data.keyword.cloudant}}
{: #cloudant_integration}

Pour intégrer votre service {{site.data.keyword.cloudant}} existant, procédez comme suit :

1. Cliquez sur votre instance de service {{site.data.keyword.cloudant}}.
2. Cliquez sur **LAUNCH**.
3. Dans la vue **Databases**, cliquez sur le nom de votre base de données.
4. Cliquez sur **API** et copiez la valeur **API Key** via votre nom de base de données.

   **Remarque** : ne copiez pas le contenu après votre nom de base de données.

5. Cliquez sur **Permissions** > **Generate API Key** et copiez les valeurs **Key** et **Password**.
6. Retournez à la vue **Projets** du tableau de bord Mobile.
7. Cliquez sur votre projet pour l'éditer.
8. Cliquez sur **Data** > **+ Data Source** > **Cloudant**, fournissez le nom de votre source de données puis cliquez sur **Add**.
9. Cliquez sur **Cloudant Config**.
10. Fournissez la valeur **API Key**, que vous avez copiée précédemment, dans la zone **API URL**.
11. Fournissez la valeur **Key**, que vous avez copiée précédemment, dans la zone **User**.
12. Fournissez la valeur **Password**, que vous avez copiée précédemment, dans la zone **Password**.
13. Cliquez sur **Ok**.
