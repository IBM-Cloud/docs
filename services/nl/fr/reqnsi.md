---

copyright:
  years: 2015, 2016

---


{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}


#Services
{: #services}
*Dernière mise à jour : 20 janvier 2016*

Vous trouverez les services disponibles dans le **catalogue** sous **Services**, dans l'interface utilisateur
{{site.data.keyword.Bluemix}}.
{:shortdesc}


Des services prédéfinis sont disponibles dans {{site.data.keyword.Bluemix_notm}} pour les applications mobiles. {{site.data.keyword.Bluemix_notm}} simplifie l'implémentation, l'hébergement et la mise à l'échelle de ces services pour vos applications mobiles. Vous pouvez vous concentrer sur la logique et la conception de l'application.

{{site.data.keyword.Bluemix_notm}} héberge et gère des services middleware pour les applications Web. Les développeurs peuvent spécifier les services middleware dont ils ont besoin. {{site.data.keyword.Bluemix_notm}} met ensuite à disposition de nouvelles instances des services middleware spécifiés et lie ces instances à l'application.

{{site.data.keyword.Bluemix_notm}}
présente les services de deux façons : par catégorie de services et par type de support de service.



<dl>
<dt><strong>Catégorie</strong></dt>
<dd>Les services {{site.data.keyword.Bluemix_notm}} sont organisés dans différentes catégories. Dans chaque
catégorie de services, les services créés par IBM sont répertoriés en premier, suivis des services de tiers, puis des services de communauté.</dd>
<dt><strong>Support</strong></dt>
<dd>Plusieurs niveaux de support existent pour les services {{site.data.keyword.Bluemix_notm}}. Le tableau
suivant décrit les informations de support générales pour les services {{site.data.keyword.Bluemix_notm}} :

</dd>
</dl>



|Type	|Description	|Détails du support|
|:------|:--------------|:--------------|
|IBM	|Service fourni par IBM et généralement disponible.	|Les problèmes considérés comme un défaut d'un service fourni par IBM généralement disponible sont traités. Le support dépend de la
gravité que vous définissez. Pour plus d'informations sur la gravité des tickets, voir
[Contacter le service de support](../support/index.html#contacting-bluemix-support){: new_window}.|
|Tiers	|Service fourni par une société autre qu'IBM.	|Le support des services de tiers est assuré par le fournisseur de service. Si IBM examine un
problème et détermine qu'il s'agit d'un défaut d'un service de tiers, elle n'est pas obligée de fournir un correctif. IBM partagera son analyse avec le
fournisseur de service de tiers si nécessaire.|
|Communauté	|Service fourni par une communauté open source.	|Le support des services de communauté est assuré par la communauté des développeurs
{{site.data.keyword.Bluemix_notm}}. Si IBM examine un problème et détermine qu'il s'agit d'un défaut d'un service de communauté, elle n'est pas
obligée de fournir un correctif.|
|Bêta	|Service qui n'est pas prêt pour la phase de production et qui se trouve au stade d'essai de développement. Un service bêta peut aider les équipes de développement et marketing à évaluer la valeur d'un service avant de le rendre généralement disponible.	|Les
problèmes
identifiés comme défauts dans un service bêta fourni par IBM sont pris en charge, mais IBM n'est pas obligée de fournir un correctif. De plus, le ticket de problème sera associé à une gravité de 3 ou 4 si
applicable. Pour des informations sur la gravité des tickets, voir [Contacter le service de support](../support/index.html#contacting-bluemix-support){: new_window}.|
*Tableau 1. Informations sur le support des services {{site.data.keyword.Bluemix_notm}}*




{{site.data.keyword.Bluemix_notm}}
propose également des services expérimentaux que vous pouvez essayer. Pour afficher tous les services expérimentaux, les conteneurs boilerplate et les
contextes d'exécution, connectez-vous à {{site.data.keyword.Bluemix_notm}}, faites défiler le catalogue jusqu'à la fin, puis cliquez sur le
**catalogue {{site.data.keyword.Bluemix_notm}} Lab**.

Les services expérimentaux peuvent
être instables et faire l'objet de modifications entraînant leur incompatibilité avec les versions précédentes. L'utilisation de ces services dans des
environnements de production n'est pas recommandée. Le support des services expérimentaux est assuré par la communauté des développeurs {{site.data.keyword.Bluemix_notm}}. Si IBM examine un problème et
détermine qu'il s'agit d'un défaut d'un service expérimental, elle n'est pas obligée de fournir un correctif.

Pour utiliser un service dans l'interface utilisateur {{site.data.keyword.Bluemix_notm}}, l'interface de ligne de commande cf, IBM
{{site.data.keyword.Bluemix_notm}} DevOps Services, ou tout outil pris en charge, procédez comme suit :

1. Créez une instance du service. Dans la plupart des cas, l'instance de service peut être créée en même temps que l'application.

2. Identifiez l'application qui utilise la nouvelle instance de service. Pour les applications Web, vous pouvez spécifier que plusieurs applications utilisent la même instance de service, ce qui permet notamment le partage de données.

3. Ecrivez le code dans votre application pour interaction avec le service.

##Services par région

Les services ne sont pas tous disponibles dans toutes les régions {{site.data.keyword.Bluemix_notm}}. Le tableau ci-dessous affiche le
services qui sont fournis par IBM.



|Service	|Disponible dans la région Sud des Etats-Unis	|Disponible dans la région Europe-Royaume-Uni |Disponible dans la région Australie-Sydney|
|:----------|:------------------------------|:------------------|:------------------|
|{{site.data.keyword.activedeployshort}}	|Oui		|Oui		|Non|
|{{site.data.keyword.alchemyapishort}} 		|Oui	   	|Oui  		|Oui|
|{{site.data.keyword.appsecshort}}		|Oui		|Non		|Non|
|{{site.data.keyword.alertnotificationshort}}|Oui		|Non			|Non		|
|{{site.data.keyword.APS_DA}}			|Oui		|Non		|Non|
|{{site.data.keyword.APS_MA}}			|Oui		|Non		|Non|
|{{site.data.keyword.amashort}}			|Oui		|Oui		|Oui|
|{{site.data.keyword.hadoopst}}			|Oui		|Non		|Non|
|{{site.data.keyword.APIM}}			|Oui		|Oui		|Non|
|{{site.data.keyword.autoscaling}}		|Oui		|Oui		|Oui|
|{{site.data.keyword.bigicloudst}}		|Oui		|Non		|Non|
|{{site.data.keyword.rules_short}}		|Oui		|Oui		|Non|
|{{site.data.keyword.cloudint}}			|Oui		|Oui		|Non|
|{{site.data.keyword.cloudant}}			|Oui		|Oui		|Non|
|{{site.data.keyword.conceptexpansionshort}}	|Oui		|Oui		|Oui|
|{{site.data.keyword.conceptinsightsshort}}	|Oui		|Oui		|Oui|
|{{site.data.keyword.dashdbshort}}		|Oui		|Oui		|Non|
|{{site.data.keyword.datacshort}}		|Oui		|Oui		|Oui|
|{{site.data.keyword.DB2OnCloud_short}}		|Oui		|Oui		|Oui|
|{{site.data.keyword.deliverypipeline}}		|Oui		|Oui		|Non|
|{{site.data.keyword.dialogshort}}		|Oui		|Oui		|Oui|
|{{site.data.keyword.documentconversionshort}}	|Oui		|Oui		|Oui|
|{{site.data.keyword.creshort}}			|Oui		|Non		|Non|
|{{site.data.keyword.game}}			|Oui		|Oui		|Oui|
|{{site.data.keyword.geospatialshort_Geospatial}}	|Oui	|Oui		|Non|
|{{site.data.keyword.globalizationshort}}	|Oui		|Non		|Non|
|{{site.data.keyword.dataworks_short}}		|Oui		|Oui		|Non|
|{{site.data.keyword.twittershort}}		|Oui		|Oui		|Oui|
|{{site.data.keyword.weather_short}}		|Oui		|Oui		|Oui|
|{{site.data.keyword.IntegrationTestingshort}}	|Oui		|Oui		|Non|
|{{site.data.keyword.iot_short}}		|Oui		|Non		|Non|
|{{site.data.keyword.keymanagementserviceshort}}|Non		|Oui		|Non|
|{{site.data.keyword.languagetranslationshort}}	|Oui		|Oui		|Non|
|{{site.data.keyword.messagehub}}		|Oui		|Oui		|Non|
|{{site.data.keyword.messageresonanceshort}}	|Oui		|Oui		|Non|
|{{site.data.keyword.APS_MAiOS}} 		|Oui		|Non		|Non|
|{{site.data.keyword.macm_short}}		|Oui		|Oui		|Oui|
|{{site.data.keyword.mobilemam}}		|Oui		|Oui		|Non|
|{{site.data.keyword.mobiledata}}		|Oui		|Oui		|Non|
|{{site.data.keyword.manda}}			|Oui		|Oui		|Non|
|{{site.data.keyword.mqa}}			|Oui		|Oui		|Non|
|{{site.data.keyword.mql}}			|Oui		|Oui		|Non|
|{{site.data.keyword.nlclassifierlshort}} 	|Oui 		|Oui 		|Oui|
|{{site.data.keyword.objectstorageshort}}	|Oui		|Non		|Non|
|{{site.data.keyword.personalityinsightsshort}}	|Oui		|Oui		|Oui|
|{{site.data.keyword.mobilepush}}Push		|Oui		|Oui		|Non|
|Push for iOS 8					|Oui		|Oui		|Non|
|{{site.data.keyword.questionandanswershort}}	|Oui		|Oui		|Oui|
|{{site.data.keyword.rapidApps}}		|Oui		|Oui		|Non|
|{{site.data.keyword.relationshipextractionshort}}	|Oui	|Oui		|Oui|
|{{site.data.keyword.retrieveandrankshort}}	|Oui 		|Oui 		|Oui|
|{{site.data.keyword.SecureGateway}}		|Oui		|Oui		|Non|
|{{site.data.keyword.servicediscoveryshort}}	|Oui		|Non		|Non|
|{{site.data.keyword.sescashort}}		|Oui		|Oui		|Oui|
|{{site.data.keyword.ssofull}}			|Oui		|Non		|Non|
|{{site.data.keyword.speechtotextshort}}	|Oui 		|Oui	 	|Oui|
|{{site.data.keyword.sqldb}}			|Oui		|Oui		|Non|
|{{site.data.keyword.staticanalyzershort}}	|Oui		|Oui		|Non|
|{{site.data.keyword.streaminganalyticsshort}}	|Oui		|Non		|Non|
|{{site.data.keyword.texttospeechshort}} 	|Oui 		|Oui	 	|Oui|
|{{site.data.keyword.times}}			|Oui		|Oui		|Non|
|{{site.data.keyword.toneanalyzershort}} 	|Oui 		|Oui 		|Oui|
|{{site.data.keyword.trackplan}}		|Oui		|Oui		|Non|
|{{site.data.keyword.tradeoffanalyticsshort}}	|Oui		|Oui		|Oui|
|{{site.data.keyword.visualinsightsshort}}	|Oui		|Oui		|Oui|
|{{site.data.keyword.visualizationrenderingshort}} |Oui		|Oui		|Non|
|{{site.data.keyword.workflow}}			|Oui		|Oui		|Non|
|{{site.data.keyword.workloadscheduler}}	|Oui		|Oui		|Non|
|{{site.data.keyword.xpagesservice_short}}	|Oui		|Oui		|Non|
*Tableau 2. Disponibilité des services*


# Ajout d'un service à votre application
{: #add_service}
*Dernière mise à jour : 8 mars 2016*

{{site.data.keyword.Bluemix}} dispose d'une liste de services qu'il gère pour les développeurs. Pour
ajouter un service que votre application pourra utiliser, vous devez demander une instance de ce service et configurer l'application afin qu'elle
interagisse avec le service.

Vous pouvez afficher tous les services qui sont disponibles dans {{site.data.keyword.Bluemix_notm}} comme suit :

* Depuis l'interface utilisateur {{site.data.keyword.Bluemix_notm}}. Affichez le catalogue {{site.data.keyword.Bluemix_notm}}.
* Depuis l'interface de ligne de commande cf. Utilisez la commande **cf marketplace**.
* Depuis votre propre application. Utilisez l'[API Services GET
/v2/services](http://apidocs.cloudfoundry.org/197/services/list_all_services.html){: new_window}.

Vous pouvez sélectionner le service dont vous avez besoin pendant le développement des applications. Une fois la sélection effectuée,
{{site.data.keyword.Bluemix_notm}} interagit avec le service et effectue les opérations nécessaires pour mettre à
disposition les ressources du service. Le processus de mise à disposition peut varier en fonction des types de service. Par exemple, un service de base de données crée une base de données, un service de notification push pour des applications mobiles génère des informations de configuration.

{{site.data.keyword.Bluemix_notm}} fournit les ressources d'un service à votre application par le biais d'une
instance de service. Une instance de service peut être partagée entre plusieurs applications Web.

Vous pouvez aussi utiliser des services qui sont hébergés dans d'autres régions, si ces services sont disponibles dans ces régions. Ils doivent être accessibles depuis Internet et posséder des noeuds finaux d'API. Vous devez coder manuellement votre application pour l'utilisation
de ces services de la même façon que vous codez les applications externes ou les outils tiers pour l'utilisation des services
{{site.data.keyword.Bluemix_notm}}. Pour plus d'informations, voir [Utilisation des services {{site.data.keyword.Bluemix_notm}} avec des
applications externes et des outils tiers](#accser_external).



## Demande de nouvelle instance de service
{: #req_instance}

Pour demander une nouvelle instance de service, vous devez employer l'interface utilisateur
{{site.data.keyword.Bluemix_notm}} ou l'interface de ligne de commande cf.

**Remarque :** lorsque vous spécifiez le nom du service, évitez d'utiliser des caractères autres que des caractères alphabétiques
ou numériques, car vous risquez de
générer des résultats imprévisibles.

Si vous utilisez l'interface utilisateur {{site.data.keyword.Bluemix_notm}} pour demander une instance de service, procédez comme suit :

1. Dans le **catalogue** {{site.data.keyword.Bluemix_notm}}, cliquez sur la vignette du service à ajouter. La page des détails du
service s'ouvre.

2. Dans le panneau Ajout de service, sélectionnez l'application à laquelle lier cette instance de service dans la liste **Appli**.

3. Entrez un nom dans la zone **Nom du service**. Un nom de service par défaut est fourni. Vous pouvez le changer dans la zone ou le
conserver.

4. Renseignez les autres zones et effectuez les sélections requises, puis cliquez sur **Créer**.

Si vous utilisez l'interface de ligne de commande cf pour demander une instance de service, procédez comme suit :

1. Utilisez la commande **cf marketplace** pour rechercher le nom et le plan du service dont vous avez besoin.

2. Utilisez la commande suivante pour créer une instance de service, où nom_service est le nom du service, plan_service est le plan du service et
instance_service est le nom à utiliser pour cette instance de service :

    ```
    cf create-service nom_service plan_service instance_service
    ```

3. Utilisez la commande suivante pour lier l'instance de service à une application, où nom_app est le nom de l'application et instance_service est
le nom de l'instance de service :

    ```
    cf bind-service nom_app instance_service
    ```

Vous ne pouvez lier une instance de service qu'aux instances d'application se trouvant dans le même espace ou la même organisation. Toutefois,
vous pouvez utiliser des instances de service provenant d'autres espaces ou d'autres organisations, à l'instar d'une application externe. Au lieu de
créer une liaison, utilisez les données d'identification afin de configurer directement votre instance d'application. Pour plus d'informations sur la façon
dont les applications externes utilisent les services {{site.data.keyword.Bluemix_notm}}, voir [Utilisation des
services {{site.data.keyword.Bluemix_notm}} avec des applications externes](#accser_external){: new_window}.


## Configuration de votre application pour l'interaction avec un service 
{: #config}

Une fois que vous avez lié une instance de service à votre application, vous devez configurer votre application pour
qu'elle interagisse avec le service.

Chaque service peut nécessiter un mécanisme différent pour communiquer avec les applications. Ces mécanismes sont documentés dans la définition de service, dont vous disposez lorsque vous développez des applications. Pour assurer une cohérence, les mécanismes sont requis pour que votre application interagisse avec le service.

* Pour interagir avec des services de base de données, utilisez les
informations fournies par {{site.data.keyword.Bluemix_notm}}, comme l'ID utilisateur, le mot de passe et l'URI
d'accès pour l'application.
* Pour interagir avec des services de back end mobile, utilisez les informations fournies par
{{site.data.keyword.Bluemix_notm}}, comme l'identité de l'application, les informations de sécurité propres au
client et l'URI d'accès pour l'application. En général, les services mobiles fonctionnent en contexte les uns avec les autres de sorte que les informations
de contexte, comme le nom du développeur de l'application et l'utilisateur qui utilise l'application, puissent être partagées entre les services.
* Pour interagir avec des applications Web ou le code de cloud côté client pour les applications mobiles, utilisez les informations fournies par
{{site.data.keyword.Bluemix_notm}}, comme les données d'identification d'exécution dans la variable
d'environnement *VCAP_SERVICES* de l'application. La valeur de la variable d'environnement *VCAP_SERVICES* est la sérialisation
d'un objet JSON. La variable contient les données d'exécution requises pour interagir avec les services auxquels l'application est liée. Le format des données varie selon les services. Reportez-vous à la documentation du service pour plus de détails sur la manière d'interpréter chaque élément d'information.

Si un service que vous liez à une application tombe en panne, il se peut que l'application s'arrête ou présente des erreurs. {{site.data.keyword.Bluemix_notm}} ne redémarre pas automatiquement l'application pour assurer la reprise à la suite de ces problèmes. Envisagez de coder votre application afin d'identifier les pannes et
d'assurer la reprise après une indisponibilité, une exception ou une panne de connexion. Voir la rubrique de traitement des incidents
[Les applications ne sont pas redémarrées
automatiquement](../troubleshoot/index.html#ts_topmenubar) pour plus d'informations.

## Utilisation des services {{site.data.keyword.Bluemix_notm}} avec des applications externes
{: #accser_external}

Vous pouvez disposer d'applications créées et exécutées en dehors de {{site.data.keyword.Bluemix_notm}}, mais également utiliser des outils tiers. Si
des services {{site.data.keyword.Bluemix_notm}} fournissent des noeuds finaux accessibles depuis Internet,
vous pouvez utiliser ces services dans vos applications locales ou dans des outils tiers.

Pour autoriser une application externe ou un outil tiers à utiliser un service {{site.data.keyword.Bluemix_notm}}, procédez comme suit :

1. Demandez une instance du service.
    1. Dans le tableau de bord de l'interface utilisateur {{site.data.keyword.Bluemix_notm}}, cliquez sur **Utiliser des services
ou des API**. Le catalogue s'affiche.
    2. Dans le catalogue, sélectionnez le service de votre choix en cliquant sur la vignette correspondante. La page des détails du
service s'ouvre.
    3. Dans la fenêtre Ajout de service, conservez la sélection **Laisser non lié** pour la liste **Appli**. Cette sélection signifie que le service n'est pas connecté à une application {{site.data.keyword.Bluemix_notm}}.
    4. Faites toutes les sélections requises. Cliquez ensuite sur **Créer**. Une instance de service est créée et le tableau de
bord du service s'affiche.
2. Dans le panneau de navigation de gauche du tableau de bord du service, vous pouvez sélectionner **Données d'identification pour le service** pour
afficher ou ajouter des données d'identification au format JSON. Utilisez la clé d'API affichée comme données d'identification pour vous connecter à l'instance de service.

Votre application qui s'exécute en dehors de {{site.data.keyword.Bluemix_notm}} peut désormais accéder au
service {{site.data.keyword.Bluemix_notm}}.

**Remarque :** si vous souhaitez supprimer des instances de service ou consulter les informations de facturation, vous devez
revenir à votre tableau de bord dans l'interface
utilisateur afin de gérer les instances de service.

## Création d'une instance de service fournie par l'utilisateur
{: #user_provide_services}

Certaines de vos ressources peuvent être gérées hors de {{site.data.keyword.Bluemix_notm}}. Si vous
disposez des données d'identification permettant d'accéder à ces ressources externes depuis Internet, vous pouvez créer des instances de service
{{site.data.keyword.Bluemix_notm}} fournies par l'utilisateur afin de représenter vos ressources externes et de
communiquer avec elles.

Pour créer une instance de service fournie par l'utilisateur et la lier à une application, procédez comme suit :

1. Créez une instance de service fournie par l'utilisateur avec la commande **cf create-user-provided-service** ou **cf
cups** :
    * Pour créer une instance de service fournie par l'utilisateur générale, utilisez l'option **-p** et séparez les noms de paramètre par une
virgule. L'interface de ligne de commande cf vous invite alors à entrer chaque paramètre. Par exemple :
        ```
        cf cups testups1 -p "hôte, port, nombd, nomutilisateur, motdepasse"
        host> pubsub01.exemple.com
        port> 1234
        dbname> sampledb01
        username> pubsubuser
        password> p@$$w0rd
        Création du service fourni par l'utilisateur testups1 dans l'organisation my-org / l'espace dev en tant que user@sample.com...
        OK
        ```

    * Pour créer une instance de service qui envoie des informations à un logiciel de gestion de journal tiers, utilisez l'option **-l** et
spécifiez la destination fournie par le logiciel de gestion de journal tiers. Par exemple :

        ```
        cf cups testups2 -l syslog://example.com
        Création du service fourni par l'utilisateur testups2 dans l'organisation my-org / l'espace dev en tant que user@sample.com...
        OK
        ```

    Pour mettre à jour un ou plusieurs paramètres de l'instance de service fournie par l'utilisateur, utilisez la commande **cf
update-user-provided-service** ou **cf uups**.

    * Pour mettre à jour une instance de service fournie par l'utilisateur générale, utilisez l'option **-p** et spécifiez les clés et les
valeurs des paramètres dans un objet json. Par exemple :

        ```
        cf uups testups1 -p "{\"username\":\"pubsubuser2\",\"password\":\"p@$$w0rd2\"}"
        Mise à jour du service fourni par l'utilisateur testups1 dans l'organisation my-org / l'espace dev en tant que user@sample.com...
        OK
        ```

    * Pour créer une instance de service qui envoie des informations à un logiciel de gestion de journal tiers, utilisez l'option -l. Par exemple :

        ```
        cf uups testups2 -l syslog://example2.com
        Mise à jour du service fourni par l'utilisateur testups2 dans l'organisation my-org / l'espace dev en tant que user@sample.com...
        OK
        ```

2. Liez l'instance de service à votre application avec la commande cf bind-service. Par exemple :

	```
	cf bind-service mon_app testups1
	Liaison du service testups1 à l'application mon_app dans l'organisation my-org / l'espace dev en tant que user@sample.com...
	OK
	```

A présent, vous pouvez configurer votre application afin d'utiliser les ressources externes. Pour des informations sur la configuration de votre
application pour l'interaction avec un service, voir [Configuration de votre application pour l'interaction avec un
service](#config){: new_window}.

## Utilisation des services dans une autre région
{: #cross_region_service}

Si une instance de service est créée et liée à des applications dans une région, vous pouvez l'utiliser dans une autre région de l'une des façons
suivantes :

  * Utilisez les données d'identification du service pour configurer votre instance d'application directement. Voir
[Utilisation des services {{site.data.keyword.Bluemix_notm}} avec des applications externes](#accser_external){: new_window}
pour des détails.
  * Créez un service fourni par l'utilisateur comme pont.
    
	Supposez que vous vous trouviez dans la région dans laquelle vous voulez utiliser l'instance de service. Pour utiliser une instance de service qui
existe dans une autre région, procédez comme suit :

      1. Passez dans la région dans laquelle l'instance de service existe. Dans la barre de menu {{site.data.keyword.Bluemix_notm}} supérieure, développez
**Région** ou cliquez sur l'icône **Région**, puis sélectionnez la région dans laquelle l'instance de service existe.

      2. Récupérez les données d'identification et les paramètres de connexion depuis la variable d'environnement VCAP_SERVICES de l'instance de service
dans la région dans laquelle le service existe. Procédez comme suit :

	       1. Dans le tableau de bord {{site.data.keyword.Bluemix_notm}}, cliquez sur la vignette de votre application. La page Présentation
s'affiche.
	       2. Dans le panneau de navigation de gauche, cliquez sur **Variables d'environnement**. Les détails de la variable d'environnement *VCAP_SERVICES* sont affichés dans le panneau de droite. Enregistrez le contenu JSON pour
l'instance de service.

      3. Passez dans la région dans laquelle vous voulez utiliser l'instance de service. Dans la barre de menu {{site.data.keyword.Bluemix_notm}}
supérieure, développez **Région** ou cliquez sur l'icône **Région**, puis sélectionnez la région dans laquelle
utiliser l'instance de service.

      4. Créez une instance de service fournie par l'utilisateur en utilisant les données d'identification et les paramètres de connexion que vous avez
enregistrés depuis la variable d'environnement *VCAP_SERVICES*. Pour plus d'informations sur la création d'une instance de service fournie par l'utilisateur, voir [Création d'une instance de service fournie par l'utilisateur](#user_provide_services){: new_window}.

      5. Liez l'instance de service fournie par l'utilisateur à votre application avec la commande suivante :

	     ```
	     cf bind-service mon_app instance_service_fournie_par_utilisateur
	     ```






## Utilisation des services dans un autre service
{: #s2s_binding}

L'autorisation d'accès au service permet à un service d'accéder à un autre service directement. Vous pouvez autoriser et configurer l'accès d'une
instance de service à d'autres instances de service dans le tableau de bord {{site.data.keyword.Bluemix_notm}}.

Pour utiliser une instance de service depuis un autre service, procédez comme suit :

1. Dans le tableau de bord {{site.data.keyword.Bluemix_notm}}, cliquez sur la vignette du service auquel accéder. Le tableau de bord du
service s'ouvre.
2. Dans le panneau de navigation de gauche, cliquez sur *Gérer* pour autoriser la liaison depuis d'autres instances de service à
l'aide de la console de l'instance de service.
3. Si vous voulez refuser à d'autres services l'accès à l'instance de service, cliquez sur *Autorisation d'accès au service* dans le
panneau de navigation de gauche, puis utilisez *Révoquer* pour supprimer la liaison de service. 

# rellinks
{: #rellinks}

## general
{: #general}

* [Liaison d'un service via l'interface utilisateur {{site.data.keyword.Bluemix_notm}}](../cfapps/ee.html#ee_bindui)
* [Extraction de VCAP_SERVICES](../cli/vcapsvc.html#retrieving)


