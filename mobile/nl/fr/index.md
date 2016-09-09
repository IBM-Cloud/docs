---

copyright:
  years: 2016

---
{:new_window: target="_blank"}

# Création de projets mobiles depuis le tableau de bord Mobile
{: #mobile}
Dernière mise à jour : 21 juillet 2016
{: .last-updated} 

Avec les services {{site.data.keyword.Bluemix}} Mobile, vous pouvez intégrer des services de cloud prégénérés, gérés et
évolutifs dans vos applications
mobiles sans dépendre des technologies de l'information. Ainsi, vous pouvez vous consacrer à la construction de vos applications mobiles au lieu de vous préoccuper des complexités liées à la gestion de
l'infrastructure de back end.

Le tableau de bord Mobile fournit une expérience intégrée sur {{site.data.keyword.Bluemix_notm}}. Vous pouvez créer facilement des projets mobiles depuis le tableau de bord. Avec la vue **Projets**, vous pouvez gérer tous les projets dans un même emplacement. La vue **Services** affiche vos instances de services mobiles existantes.

Pour afficher le tableau de bord Mobile, cliquez sur la catégorie **Mobile** depuis votre accueil {{site.data.keyword.Bluemix_notm}} .
Accueil <img src="images/mobile_dashboard.jpg" alt="{{site.data.keyword.Bluemix_notm}}">

Pour démarrer, cliquez sur le bouton de création d'un nouveau projet depuis la vue **Projet** du tableau de bord mobile.

## Présentation des services {{site.data.keyword.Bluemix_notm}} Mobile
{: #mobile_services_overview}

Le tableau suivant décrit les services {{site.data.keyword.Bluemix_notm}} Mobile disponibles. Vous pouvez utiliser des services individuels depuis le catalogue {{site.data.keyword.Bluemix_notm}} ou les intégrer dans votre projet mobile.

<table summary="Ce tableau décrit les services {{site.data.keyword.Bluemix_notm}} Mobile et fournit des liens vers la documentation des services">
<caption>Tableau 1. Services {{site.data.keyword.Bluemix_notm}} Mobile</caption>
<th>Service {{site.data.keyword.Bluemix_notm}} Mobile</th>
<th>Description</th>
<tr>
<td> <img src="images/mobile_analytics_icon.png" alt="icône {{site.data.keyword.mobileanalytics_short}}"><br/>{{site.data.keyword.mobileanalytics_short}} (Experimental)</td>
<td valign="top">Utilisez le service {{site.data.keyword.mobileanalytics_full}} pour mesurer l'état, le comportement et le contexte des vos applications mobiles, vos utilisateurs mobiles et vos périphériques mobiles.<br/><br/>
Découvrez plus en détails le fonctionnement de ce service dans la documentation <a href="../services/mobileanalytics/index.html" alt="lien vers la documentation {{site.data.keyword.mobileanalytics_short}}">{{site.data.keyword.mobileanalytics_short}}</a>.
</td>
</tr>
<tr>
<td><img src="images/catalog_icons-05.png" alt="{{site.data.keyword.amashort}} service icon"><br/>{{site.data.keyword.amashort}}</td>
<td valign="top">Utilisez le service {{site.data.keyword.amafull}} pour ajouter une fonctionnalité de sécurité à votre application mobile. Vous pouvez configurer l'authentification et les fournisseurs d'identité pour que les utilisateurs puissent se connecter dans l'application avec leurs comptes Google ou Facebook existants.<br/><br/>
Découvrez plus en détails le fonctionnement de ce service dans la documentation <a href="../services/mobileaccess/index.html" alt="lien vers la documentation {{site.data.keyword.amashort}}">{{site.data.keyword.amashort}}</a>.</td>
</tr>
<tr>
<td><img src="images/MFPFoundation_icon.png" alt="icône du service {{site.data.keyword.mobilefoundation_short}}"><br/> {{site.data.keyword.mobilefoundation_short}}</td>
<td valign="top">Utilisez le service {{site.data.keyword.mobilefoundation_long}} pour accélérer la configuration d'un environnement {{site.data.keyword.mfp_full}} depuis lequel vous pouvez développer, tester et utiliser des applications mobiles d'entreprises.<br/><br/>
Découvrez plus en détails le fonctionnement de ce service dans la documentation <a href="../services/mobilefoundation/index.html" alt="lien vers la documentation {{site.data.keyword.mobilefoundation_short}}">{{site.data.keyword.mobilefoundation_short}}  </a>.</td>
</tr>
<tr>
<td><img src="images/mqa_icon.png" alt="icône du service {{site.data.keyword.mqa}}"><br/>{{site.data.keyword.mqa}}</td>
<td valign="top">Utilisez le service {{site.data.keyword.mqafull}} pour découvrir et configurer des services de qualité mobile pour vos applications. Vous pouvez afficher des mesures de qualité de haut niveau pour vos applications mobiles afin de pouvoir comprendre rapidement les problèmes des applications sur lesquelles vous travaillez. Ces mesures incluent des informations sur les pannes, les bogues, les commentaires des utilisateurs et leur sentiment. En prenant connaissance de ces informations, vous pouvez déterminer s'il est nécessaire d'analyser de façon plus approfondie certains problèmes spécifiques.<br/><br/>
Découvrez plus en détails le fonctionnement de ce service dans la documentation <a href="../services/MobileQualityAssurance/index.html" alt="lien vers la documentation {{site.data.keyword.mqa}}">{{site.data.keyword.mqa}}</a>.</td>
</tr>
<tr>
<td><img src="images/catalog_icons-09.png" alt="Icône Push Notifications"><br/>{{site.data.keyword.mobilepushshort}}</td>
<td valign="top">Utilisez le service {{site.data.keyword.mobilepushfull}} pour envoyer et gérer des notifications push mobiles ciblant les plateformes iOS et Android. Il gère le
mappage des utilisateurs de votre application à leurs périphériques ainsi que la plateforme des périphériques, et traite la distribution des
notifications
push aux périphériques. Avec ce service, vous pouvez envoyer des diffusions, des monodiffusions (en fonction de l'ID utilisateur ou de l'ID de
périphérique) et des étiquettes (ou rubriques) en fonction de notifications push aux utilisateurs de votre application mobile.<br/><br/>
Découvrez plus en détails le fonctionnement de ce service dans la documentation <a href="../services/mobilepush/index.html" alt="lien vers la documentation {{site.data.keyword.mobilepushshort}}">{{site.data.keyword.mobilepushshort}}</a>.</td>
</table>

## Intégration des services mobiles
{: #services_integration}
Vous pouvez intégrer vos services {{site.data.keyword.Bluemix_notm}} Mobile existants, comme {{site.data.keyword.mobilepushshort}} et {{site.data.keyword.cloudant}}, dans votre projet.

#### Intégration de {{site.data.keyword.mobilepushshort}}
{: #push_integration}

Pour intégrer votre service {{site.data.keyword.mobilepushshort}} existant, procédez comme suit :

1. Cliquez sur votre instance de service {{site.data.keyword.mobilepushshort}}.
2. Cliquez sur **Options pour application mobile** et copiez les valeurs **Route** et **AppGuid**.

   **Remarque **: votre service {{site.data.keyword.mobilepushshort}} doit être lié à une application pour afficher **Options pour application mobile**.

3. Retournez à la vue **Projets** du tableau de bord Mobile.
4. Cliquez sur votre projet pour l'éditer.
5. Cliquez sur **Push** et activez les notifications.
6. Fournissez la valeur **AppGuid**, que vous avez copiée précédemment, dans la zone **App ID**.
7. Fournissez la valeur **Route**, que vous avez copiée précédemment, dans la zone **App Route URL**.

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


# Liens connexes
{: #rellinks}

<!-- links to internal services don't work
## {{site.data.keyword.Bluemix_notm}} Mobile services
{: #general}
* [Mobile Analytics (Experimental)](../services/mobileanalytics/index.html){: new_window}
* [Mobile Client Access](../services/mobileaccess/index.html){: new_window}
* [Mobile Foundation](../services/mobilefoundation/index.html){: new_window}
* [Mobile Quality Assurance)](../services/MobileQualityAssurance/index.html){: new_window}
* [Push Notifications](../services/mobilepush/index.html){: new_window}
-->

## Articles de blogue
{: #general}
* [Blog Post: Introducing the Bluemix Mobile dashboard](https://developer.ibm.com/bluemix/2016/07/08/new-bluemix-mobile-dashboard/){: new_window}
* [Blog Post: Bluemix Mobile, Part 1: Creating a Store Catalog application](https://developer.ibm.com/bluemix/2016/07/13/bluemix-mobile-creating-store-catalog-app-part1/){: new_window}
* [Blog Post: Bluemix Mobile, Part 2: Integrating custom Bluemix backend into the Store Catalog app](https://developer.ibm.com/bluemix/2016/07/14/bluemix-mobile-integrating-custom-backend-part2/){: new_window}
 
## Tutoriels et exemples
{: #samples}
* [Mobile Backend for Bluemix](https://github.com/ibm-bluemix-mobile-services/mobiledashboard-storecatalog-backend){: new_window}

