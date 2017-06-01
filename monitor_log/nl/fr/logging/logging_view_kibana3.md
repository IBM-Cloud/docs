---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-22"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Analyse de journaux dans Kibana 3 (obsolète)
{: #analyzing_logs_Kibana3}

Dans {{site.data.keyword.Bluemix}}, vous pouvez utiliser la plateforme de visualisation et d'analyse open source Kibana pour surveiller, rechercher, analyser et visualiser des données dans différents graphiques, par exemple, des diagrammes et des tableaux. Utilisez Kibana pour effectuer des tâches analytiques avancées.
{:shortdesc}

Vous pouvez lancer Kibana en procédant de l'une des manières suivantes :

* A partir du tableau de bord d'applications Cloud Foundary

    Vous pouvez accéder à vos journaux pour une application CF spécifique dans Kibana, dans le contexte de cette application spécifique.
    
    La requête utilisée pour filtrer les données affichées dans le tableau de bord extrait des entrées de journal pour l'application Cloud Foundry. Les informations de journal affichées par défaut par le tableau de bord Kibana sont toutes liées à une seule et même application Cloud Foundry et à toutes ses instances. Pour plus d'informations, voir [Accès au tableau de bord Kibana depuis le tableau de bord Bluemix](logging_view_kibana3.html#launch_Kibana_from_bluemix).

* A partir d'un lien de navigateur direct

    Vous souhaiterez peut-être lancer votre tableau de bord Kibana personnalisé qui agrège les données provenant de services au sein d'un espace {{site.data.keyword.Bluemix}} fourni.
    
    La requête utilisée pour filtrer les données affichées dans le tableau de bord extrait des entrées de journal pour un espace dans l'organisation {{site.data.keyword.Bluemix}}. Les informations de journal affichées par le tableau de bord Kibana comprennent notamment des enregistrements relatifs à toutes les ressources déployées dans l'espace de l'organisation {{site.data.keyword.Bluemix}} à laquelle vous êtes connectée. Pour plus d'informations, voir [Accès au tableau de bord Kibana depuis un navigateur Web](logging_view_kibana3.html#launch_Kibana_from_browser).
    
    Vous pouvez également modifier ou supprimer la requête initiale et ajouter d'autres requêtes. Pour plus d'informations, voir [Filtrage de vos journaux d'application Cloud Foundry à l'aide de requêtes dans Kibana](kibana3/logging_kibana_query.html#logging_kibana_query).


Kibana est une interface basée sur un navigateur qui vous permet de personnaliser des tableaux de bord que vous pouvez ensuite utiliser pour analyser des données de journal et effectuer des tâches de gestion avancées. 

Dans {{site.data.keyword.Bluemix}}, vous pouvez analyser des données à l'aide du tableau de bord Kibana par défaut disponible pour chaque application Cloud Foundry et pour chaque espace de votre organisation. Par défaut, ces tableaux de bord affichent toutes les données disponibles depuis les 24 dernières heures via un panneau incluant une ligne Histogramme et une ligne Tableau d'événements. 

Pour limiter les informations affichées via n'importe quel tableau de bord par défaut, vous pouvez ajouter des requêtes et des filtres à un tableau de bord par défaut. Vous pouvez ensuite sauvegarder le tableau de bord pour le réutiliser ultérieurement. 

Les données affichées dans un tableau de bord Kibana sont contrôlées par la requête. Pour modifier les informations affichées dans un tableau de bord, vous pouvez modifier la requête, ajouter plusieurs requêtes, puis sauvegarder le tableau de bord. Vous pouvez personnaliser, sauvegarder et partager et plusieurs tableaux de bord simultanément. C'est ainsi que Kibana affiche des informations sur une application dans votre espace, par exemple.

Vous pouvez également configurer des filtres à partir des zones de journal, par exemple, message_type et instance_ID. Pour plus d'informations, voir [Format de journal Kibana](logging_view_kibana3.html#kibana_log_format_cf). Vous pouvez activer ou désactiver dynamiquement ces filtres. Le tableau de bord affiche les entrées de journal correspondant à la requête et aux critères de filtrage que vous activez. Pour plus d'informations, voir [Filtrage de données dans un tableau de bord Kibana](logging_view_kibana3.html#filter_data_kibana_dashboard).

Pour visualiser les données, vous pouvez configurer des panneaux. Kibana inclut différents panneaux, tels que des tableaux, des tendances et des histogrammes, que vous pouvez utiliser pour analyser les informations. Vous pouvez ajouter, retirer et réorganiser des panneaux dans le tableau de bord. L'objectif de chaque panneau est différent. Certains panneaux sont organisés en lignes qui fournissent les résultats d'une ou de plusieurs requêtes. D'autres panneaux affichent des documents ou des informations personnalisées. Pour plus d'informations, voir [Personnalisation d'un tableau de bord Kibana](logging_view_kibana3.html#customize_kibana_dashboard).

Après avoir personnalisé un tableau de bord, vous pouvez choisir l'une des actions suivantes :

* Vous pouvez sauvegarder le tableau de bord pour le réutiliser ultérieurement. Pour plus d'informations, voir [Sauvegarde d'un tableau de bord Kibana](logging_view_kibana3.html#save_Kibana_dashboard).

* Vous pouvez exporter ou partager un lien direct vers un tableau de bord Kibana avec un autre utilisateur. Pour plus d'informations, voir [Exportation et partage de vos tableaux de bord Kibana](kibana3/logging_kibana_export_share_dashboard.html#sexporting_sharing_kibana_dash).

* Vous pouvez incorporer le tableau de bord dans une page Web. Pour pouvoir visualiser un tableau de bord incorporé, un utilisateur doit disposer des droits d'accès nécessaires pour accéder à Kibana.

Pour plus d'informations, voir la documentation [Kibana ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://www.elastic.co/guide/en/kibana/current/index.html){: new_window}.

**Remarque :** Kibana 3 et Kibana 4 sont pris en charge. La version Kibana 3 est obsolète.


##  Accès au tableau de bord Kibana depuis le tableau de bord Bluemix
{: #launch_Kibana_from_bluemix}

La requête utilisée pour filtrer les données affichées dans le tableau de bord extrait des entrées de journal pour l'application Cloud Foundry. Les informations de journal affichées par défaut par le tableau de bord Kibana sont toutes liées à une seule et même application Cloud Foundry et à toutes ses instances.

Pour visualiser les journaux d'une application Cloud Foundry dans Kibana, procédez comme suit :

1. Connectez-vous à {{site.data.keyword.Bluemix_notm}}, puis cliquez sur le nom d'application dans le tableau de bord {{site.data.keyword.Bluemix_notm}} **Applications**. La page des détails de l'application s'ouvre.
    
2. Dans la barre de navigation, cliquez sur **Journaux**. L'onglet Journaux s'affiche. 
    
3. Cliquez sur **Vue avancée**. Le tableau de bord **Kibana 3** s'affiche.

Si vous ne voyez aucun journal, ajustez le sélecteur de période situé dans l'en-tête.

Pour plus d'informations sur la personnalisation d'un tableau de bord Kibana, voir [l'article de blogue ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/){: new_window} ou la documentation [Kibana ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://www.elastic.co/guide/en/kibana/current/index.html){: new_window}.

##  Accès au tableau de bord Kibana depuis un navigateur Web
{: #launch_Kibana_from_browser}

La requête utilisée pour filtrer les données affichées dans le tableau de bord extrait des entrées de journal pour un espace dans l'organisation {{site.data.keyword.Bluemix}}. Les informations de journal affichées par le tableau de bord Kibana comprennent notamment des enregistrements relatifs à toutes les ressources déployées dans l'espace de l'organisation {{site.data.keyword.Bluemix}} à laquelle vous êtes connectée.

Procédez comme suit pour ouvrir un tableau de bord Kibana depuis un navigateur :

1. Ouvrez [https://logmet.<span class="keyword" data-hd-keyref="DomainName">NomDomaine</span>](https://logmet.{DomainName}) pour vous connecter à l'interface utilisateur Kibana.

2. Sélectionnez l'onglet **Kibana 3** pour utiliser Kibana 3. Sélectionnez l'onglet **Kibana 4** pour utiliser Kibana 4. Le tableau de bord Kibana par défaut s'affiche. 

Si vous ne voyez aucun journal, ajustez le sélecteur de période situé dans l'en-tête.

Pour plus d'informations sur la personnalisation d'un tableau de bord Kibana, voir [l'article de blogue ![Icône de lien externe](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/){: new_window} our la documentation [Kibana ![Icône de lien externe](../icons/launch-glyph.svg "External link icon")](https://www.elastic.co/guide/en/kibana/current/index.html){: new_window}.



## Filtrage des données dans un tableau de bord Kibana
{: #filter_data_kibana_dashboard}

Dans {{site.data.keyword.Bluemix}}, vous pouvez analyser des données à l'aide du tableau de bord Kibana par défaut fourni pour chaque ressource ou pour chaque espace {{site.data.keyword.Bluemix}}. Par défaut, ces tableaux de bord affichent toutes les données disponibles depuis les 24 dernières heures. Vous pouvez toutefois limiter les informations affichées par un tableau de bord. Vous pouvez ajouter des requêtes et des filtres à un tableau de bord par défaut, puis sauvegarder ce dernier afin de le réutiliser ultérieurement.

Dans un tableau de bord, vous pouvez ajouter plusieurs requêtes et filtres. Une requête définit un sous-ensemble d'entrées de journal.  Un filtre affine la sélection de données en incluant ou en excluant des informations. 

La liste suivante présente des exemples de filtrage de données pour les applications Cloud Foundry :
* Si vous recherchez dans vos journaux des informations qui contiennent des termes clés, vous pouvez créer des requêtes afin d'effectuer un filtrage à l'aide de ces termes. Kibana vous permet de comparer visuellement des requêtes sur le tableau de bord. Pour plus d'informations, voir [Filtrage de vos journaux d'application Cloud Foundry à l'aide de requêtes dans Kibana](kibana3/logging_kibana_query.html#logging_kibana_query).

* Si vous recherchez des informations pour une période donnée, vous pouvez filtrer les données par période. Pour plus d'informations, voir [Filtrage de vos journaux d'application Cloud Foundry par période dans Kibana](kibana3/logging_kibana_filter_by_time_period.html#logging_kibana_time_filter).

* Si vous recherchez des informations pour un ID d'instance donné, vous pouvez filtrer les données par ID d'instance. Pour plus d'informations, voir [Filtrage de vos journaux d'application Cloud Foundry par ID d'instance dans Kibana](kibana3/logging_kibana_filter_by_instance_id.html#logging_kibana_instance_id) et [Filtrage de vos journaux d'application Cloud Foundry par ID d'application connu dans Kibana](kibana3/logging_kibana_filter_by_known_application_id.html#logging_kibana_known_application_id).

* Si vous recherchez des informations pour un composant donné, vous pouvez filtrer les données par composant (type de journal). Pour plus d'informations, voir [Filtrage de vos journaux d'application Cloud Foundry par type de journal dans Kibana](kibana3/logging_kibana_filter_by_component.html#logging_kibana_component_filter).

* Si vous recherchez des informations, par exemple, des messages d'erreur, vous pouvez filtrer les données par type de message. Pour plus d'informations, voir [Filtrage de vos journaux d'application Cloud Foundry par type de message dans Kibana](kibana3/logging_kibana_filter_by_message_type.html#logging_kibana_message_type_filter).

## Personnalisation d'un tableau de bord Kibana
{: #customize_kibana_dashboard}

Différents types de tableaux de bord peuvent être personnalisés pour visualiser et analyser les données, par exemple :
* Tableau de bord de type single-cf-app : tableau de bord qui affiche des informations sur une application Cloud Foundry.  
* Tableau de bord de type Multi-cf-app : tableau de bord qui affiche des informations sur toutes les applications Cloud Foundry déployées dans le même espace {{site.data.keyword.Bluemix}}. 

Lorsque vous personnalisez un tableau de bord, vous pouvez configurer des requêtes et des filtres pour sélectionner un sous-ensemble des données de journal à afficher via le tableau de bord.

Pour visualiser les données, vous pouvez configurer des panneaux. Kibana inclut différents panneaux, tels que des tableaux, des tendances et des histogrammes, que vous pouvez utiliser pour analyser les informations. Vous pouvez ajouter, retirer et réorganiser des panneaux dans le tableau de bord. L'objectif de chaque panneau est différent. Certains panneaux sont organisés en lignes qui fournissent les résultats d'une ou de plusieurs requêtes. D'autres panneaux affichent des documents ou des informations personnalisées. Par exemple, vous pouvez configurer un graphique à barres, un graphique circulaire ou un tableau pour visualiser les données et les analyser.  


## Sauvegarde d'un tableau de bord Kibana
{: #save_Kibana_dashboard}

Procédez comme suit pour sauvegarder un tableau de bord Kibana après l'avoir personnalisé :

1. Dans la barre d'outils, cliquez sur l'icône de **sauvegarde**.

2. Entrez un nom pour le tableau de bord.

    **Remarque :** Si vous tentez de sauvegarder un tableau de bord avec un nom contenant des espaces vides, l'opération échoue.

3. En regard de la zone du nom, cliquez sur l'icône de **sauvegarde**.



## Analyse des journaux via un tableau de bord Kibana
{: #analyze_kibana_logs}

Après avoir personnalisé un tableau de bord Kibana, vous pouvez visualiser et analyser les données via ses panneaux. 

Pour rechercher des informations, vous pouvez épingler ou libérer des requêtes. 

* Vous pouvez épingler une requête au tableau de bord, ce qui active automatiquement la recherche.
* Pour retirer un contenu du tableau de bord, vous pouvez désactiver une requête.

Pour filtrer des informations, vous pouvez activer ou désactiver des filtres. 

* Vous pouvez cocher la case **Basculer** ![](images/logging_toggle_include_filter.jpg) dans un filtre pour l'activer.   
* Vous pouvez décocher la case **Basculer** ![](images/logging_toggle_exclude_filter.jpg) dans un filtre pour le désactiver. 

Les diagrammes et graphiques présents dans votre tableau de bord affichent les données. Vous pouvez utiliser les diagrammes et les graphiques présents dans votre tableau de bord pour surveiller les données. 

Par exemple, avec un tableau de bord de type single-cf-app, les informations affichées concernent une application Cloud Foundry. Les données que vous pouvez visualiser et analyser sont limitées à cette application. Vous pouvez utiliser le tableau de bord pour analyser les données de toutes les instances de l'application. Vous pouvez comparer des instances. Vous pouvez filtrer les informations par ID d'instance. 

Vous pouvez définir et épingler une requête pour chaque ID d'instance au tableau de bord. 

![Tableau de bord avec des requêtes épinglées](images/logging_kibana_dash_activate_query.jpg)

Vous pouvez ensuite activer ou désactiver des requêtes individuelles en fonction des informations d'instance que vous souhaitez afficher dans le tableau de bord. 

L'illustration suivante présente une requête activée et une requête désactivée :

![Tableau de bord avec des requêtes épinglées](images/logging_kibana_dash_deactivate_query.jpg)

Si vous souhaitez comparer 2 instances dans un histogramme, vous pouvez définir deux requêtes dans le même tableau de bord, une pour chaque ID d'instance. Vous pouvez leur affecter un alias et une couleur unique afin de les identifier facilement. Kibana traite plusieurs requêtes en les reliant par un opérateur OR logique. 

L'illustration suivante présente le panneau permettant de configurer un alias et une couleur pour une requête, d'épingler celle-ci au tableau de bord et de la désactiver :

![Tableau de bord permettant de configurer une requête](images/logging_kibana_query_def.jpg)



## Format de journal Kibana pour les applications Cloud Foundry
{: #kibana_log_format_cf}

Vous pouvez configurer un tableau de bord Kibana afin d'afficher les zones suivantes pour chaque entrée de journal :

<dl>
<dt><strong>@timestamp</strong></dt>
<dd>
<pre class="pre screen"><code>aaaa-MM-jjTHH:mm:ss:SS-0500</code></pre>
<p>Heure à laquelle l'événement a été consigné. L'horodatage est défini à la milliseconde près.</p>
</dd>

<dt><strong>@version</strong></dt>
<dd>
<p></p>
</dd>

<dt><strong>ALCH_TENANT_ID</strong></dt>
<dd>
<p>ID de la ressource {{site.data.keyword.Bluemix_notm}}.</p>
</dd>

<dt><strong>_id</strong></dt>
<dd>
<p>ID unique de votre document de journal.</p>
</dd>

<dt><strong>_index</strong></dt>
<dd>
<p>Index de votre entrée de journal.</p>
</dd>

<dt><strong>_type</strong></dt>
<dd>
<p>Type de journal, par exemple, <samp>syslog</samp>.</p>
</dd>

<dt><strong>app_name</strong></dt>
<dd>
<p>Nom de votre application {{site.data.keyword.Bluemix_notm}}.</p>
</dd>

<dt><strong>application_id</strong></dt>
<dd>
<p>ID unique de votre application {{site.data.keyword.Bluemix_notm}}.</p>
</dd>

<dt><strong>host</strong></dt>
<dd>
<p>Nom de l'application ayant produit les données de journal.</p>
</dd>

<dt><strong>instance_id</strong></dt>
<dd>
<p>ID d'instance de l'instance d'application ayant produit les données de journal.</p>
</dd>

<dt><strong>module</strong></dt>
<dd>
<p></p>
</dd>

<dt><strong>loglevel</strong></dt>
<dd>
<p>Niveau de gravité de l'événement consigné.</p>
</dd>

<dt><strong>message</strong></dt>
<dd>
<pre class="pre screen"><code>&lt;<var class="keyword varname">Message</var>&gt;</code></pre>
<p>Message émis par le composant. Il varie selon le contexte.</p>
</dd>

<dt><strong>message_type</strong></dt>
<dd>
<pre class="pre screen"><code>OUT</code></pre>
<p>Flux dans lequel le message de journal est écrit. <samp class="ph codeph">OUT</samp> désigne le flux <samp class="ph codeph">stdout</samp> et
<samp class="ph codeph">ERR</samp> désigne le flux <samp class="ph codeph">stderr</samp>.</p>
</dd>

<dt><strong>org_id</strong></dt>
<dd>
<p>ID unique de votre organisation {{site.data.keyword.Bluemix_notm}}.</p>
</dd>

<dt><strong>org_name</strong></dt>
<dd>
<p>Nom de l'organisation {{site.data.keyword.Bluemix_notm}} dans laquelle votre application est constituée en préproduction.</p>
</dd>

<dt><strong>origin</strong></dt>
<dd>
<p></p>
</dd>

<dt><strong>source_id</strong></dt>
<dd>
<pre class="pre screen"><code>[App/0]</code></pre>
<p>Composant qui génère les journaux. La liste suivante décrit les journaux provenant de chaque composant :</p>

<dl>
<dt><strong>API</strong></dt>
<dd>Réponses consignées dans les appels API qui demandent une modification de l'état de votre application.</dd>

<dt><strong>APP</strong></dt>
<dd>Réponses consignées à partir de votre application.</dd>

<dt><strong>CELL</strong></dt>
<dd>Réponses consignées à partir de la cellule Diego qui indiquent lorsqu'une application démarre, s'arrête ou tombe en panne.</dd>

<dt><strong>LGR</strong></dt>
<dd>Réponses consignées à partir du composant Loggregator qui indiquent des problèmes au niveau du processus de journalisation.</dd>

<dt><strong>RTR</strong></dt>
<dd>Réponses consignées à partir du composant Router lorsque celui-ci route des demandes HTTP vers votre application.</dd>

<dt><strong>SSH</strong></dt>
<dd>Réponses consignées à partir de la cellule Diego lorsqu'un utilisateur accède à un conteneur d'applications à l'aide de la commande **cf ssh**.</dd>

<dt><strong>STG</strong></dt>
<dd>Réponses consignées à partir de la cellule Diego sur Droplet Execution Agent lorsque votre application est constituée en préproduction ou reconstituée en préproduction.</dd>
</dl>
</dd>

<dt><strong>space_name</strong></dt>
<dd>
<p>Nom de l'espace {{site.data.keyword.Bluemix_notm}} dans lequel votre application est constituée en préproduction.</p>
</dd>

<dt><strong>timestamp</strong></dt>
<dd>
<p>Heure à laquelle l'événement a été consigné. L'horodatage est défini à la milliseconde près.</p>
</dd>

<dt><strong>_type</strong></dt>
<dd>
<p>Type de journal, par exemple, <samp>syslog</samp>.</p>
</dd>
</dl>




