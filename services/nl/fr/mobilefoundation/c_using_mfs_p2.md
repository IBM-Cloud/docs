---

copyright:
  years: 2016

---

#	Utilisation de {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application
{: #using_mobilefoundation_p2}


Une fois que vous avez créé l'instance de service
{{site.data.keyword.mobilefoundation_short}}: Professional 1
Application, lisez la procédure ci-après pour commencer à l'utiliser. 

## Conditions prérequises
{: #prerequisites_p2}

Prenez connaissance des éléments suivants avant de configurer l'instance
de service {{site.data.keyword.mobilefoundation_short}}: Professional 1
Application.
* {{site.data.keyword.mobilefoundation_short}}: Professional 1
Application est pris en charge uniquement avec les plans {{site.data.keyword.Bluemix_notm}}
{{site.data.keyword.dashdbshort_notm}}: Enterprise Transactional
(prenant en charge OLTP).

* L'instance de service {{site.data.keyword.dashdbshort_notm}}
et ses données d'identification doivent être disponibles pour que vous puissiez
configurer les paramètres de l'instance de service {{site.data.keyword.mobilefoundation_short}}.

**Remarque **: L'instance de service
{{site.data.keyword.dashdbshort_notm}} peut exister dans n'importe
quel *Espace* de votre *Organisation*
{{site.data.keyword.Bluemix_notm}}.  

## Configuration de l'instance de service {{site.data.keyword.mobilefoundation_short}}:
Professional 1 Application
{: #configure_dashdb_p2}

###  Premières étapes
{: #firststeps_p2}

Une fois que vous avez créé l'instance de service
{{site.data.keyword.mobilefoundation_short}}: Professional 1
Application, procédez comme indiqué ci-après pour commencer à utiliser le
service :

* Acceptez les dispositions du contrat de licence
d'{{site.data.keyword.mfp_full_notm}} V8.0.0.0.

* Entrez vos données d'identification
{{site.data.keyword.Bluemix_notm}}. Vous autorisez ainsi le service à
apporter des modifications dans votre espace
{{site.data.keyword.Bluemix_notm}} et à créer des conteneurs
{{site.data.keyword.containerlong}} qui hébergent votre serveur
{{site.data.keyword.mobilefirst_notm}}.


### Configuration de la connexion à l'instance de service {{site.data.keyword.dashdbshort_notm}}
{: #connect_dashdb_p2}

Une fois l'instance de service
{{site.data.keyword.mobilefoundation_short}}:
Professional 1 Application créée, la page *Overview* s'affiche et
vous permet d'indiquer les informations de connexion à l'instance de service {{site.data.keyword.dashdbshort_notm}}: Enterprise Transactional.

* Indiquez l'organisation
(**Organization**) et l'espace (**Space**)
{{site.data.keyword.Bluemix_notm}} dans lesquels l'instance de
service {{site.data.keyword.dashdbshort_notm}}: Enterprise
Transactional existe.
* Choisissez le nom de service (**Service Name**) de
l'instance de service {{site.data.keyword.dashdbshort_notm}} que
vous souhaitez utiliser avec votre instance de service
{{site.data.keyword.mobilefoundation_short}} ; effectuez votre
sélection dans la liste déroulante si plusieurs instances de service
{{site.data.keyword.dashdbshort_notm}} sont créées. 
* Sélectionnez les données d'identification
(**Credentials**) de l'instance de service
{{site.data.keyword.dashdbshort_notm}} sélectionnée.

* Cliquez sur **Test Connection** pour vérifier que
votre instance de service {{site.data.keyword.dashdbshort_notm}}
est disponible, puis sur **Save**.

**Remarque **: Vous ne pourrez pas modifier
l'instance de service {{site.data.keyword.dashdbshort_notm}}
configurée pour être utilisée par votre instance de service
{{site.data.keyword.mobilefoundation_short}}. Vous pourrez
toutefois utiliser la même instance de service
{{site.data.keyword.dashdbshort_notm}} sur plusieurs instances de
service {{site.data.keyword.mobilefoundation_short}}, car chaque
instance de service {{site.data.keyword.mobilefoundation_short}}
crée son propre schéma dans l'instance de service
{{site.data.keyword.dashdbshort_notm}} sélectionnée.

* Après quelques secondes, vous pouvez accéder à la page
*Overview* qui fournit des tutoriels et des vidéos facilitant vos
premiers pas avec le service {{site.data.keyword.mobilefoundation_short}}.

### Démarrage du serveur {{site.data.keyword.mobilefirst}}
{: #start_mobilefoundation_p2}

* Pour démarrer {{site.data.keyword.mfserver_short_notm}} avec
les paramètres par défaut, cliquez sur **Start Basic Server**.

![Start Basic Server](images/start_basic_server.png "Figure 1. Start Basic Server")
{: screen}
* Cette option affecte les paramètres suivants à un serveur
{{site.data.keyword.mfserver_long_notm}} :
    -  1 Go de mémoire et 64 Go de stockage. Cette taille est suffisante
pour un contexte de développement et des activités de test sommaires.

    -	Le *nom_d'utilisateur* et le *mot_de_passe* sont générés automatiquement pour vous. Vous pouvez y accéder une fois que le
serveur est en opération.

L'implantation de votre serveur débute. Ce processus prend environ 10 minutes et une fenêtre de
message indique la progression de l'opération. A son terme, un tableau de bord s'affiche et présente les éléments suivants :

  -	Le statut du serveur que vous exécutez (état, taille, stockage).

  -	La route du serveur créé pour vous. Utilisez cette route pour joindre votre serveur mobile depuis l'Internet public. Vos applications mobiles utilisent cette
route pour accéder au serveur.

  -	Votre *nom_d'utilisateur* personnel et votre
*mot_de_passe* pour accéder à la console
{{site.data.keyword.mfp_oc_short_notm}}. Le *mot_de_passe*
est masqué. Cliquez sur l'icône en forme d'oeil pour le visualiser.

*	Cliquez sur **Launch Console** pour ouvrir la
console {{site.data.keyword.mfp_oc_short_notm}}.

![Launch Console](images/launch_console.png "Figure 2. Launch Console")
{: screen}

Cette console s'exécute dans le conteneur. Elle vous permet de gérer vos
applications et périphériques mobiles, l'utilisation de votre serveur en tant
que serveur dorsal mobile, l'envoi de notifications push, etc. 

### Recréation du serveur {{site.data.keyword.mobilefirst}} 
{: #recreate_mobilefoundation_p2}

*	Cliquez sur **Recreate** pour recréer le serveur. 

![Recreate](images/recreate.png "Figure 3. Recreate")
{: screen}

* Cette action arrête votre serveur existant et le supprime. Une
nouvelle instance de serveur est créée. Cette action prend quelques minutes avant de s'achever.

**Remarque **: Toutes les données provenant de votre
instance de serveur précédente, y compris les informations sur les applications
et les adaptateurs, sont conservées dans l'instance de service
{{site.data.keyword.dashdbshort_notm}} configurée ; elles pourront
être à nouveau utilisées une fois le serveur recréé.

##	Paramétrage d'une configuration avancée
{: #using_mfs_advanced_p2}

L'option **Start Server with Advanced Configuration**
de la page *Overview* permet de créer le serveur avec des
paramètres avancés ou personnalisés. Vous pouvez également mettre à jour les paramètres du serveur
pour personnaliser sa configuration en cliquant sur l'onglet **Configuration**. 
{{site.data.keyword.mobilefoundation_short}} vous permet d'accéder à
certains paramètres avancés. 

*	L'onglet **Topology** vous permet de sélectionner
la taille de topologie de votre conteneur. Le serveur par défaut doté d'1 Go
est idoine pour le développement et des tests sommaires, mais peut s'avérer
insuffisant, par exemple, pour tester la charge. 
  - Sélectionnez la taille appropriée pour votre serveur compte tenu de
vos besoins. 

  - **Nodes** affiche le nombre de noeuds créés. 
      - Vous pouvez configurer le nombre minimal et maximal de noeuds
requis dans vos groupes {{site.data.keyword.IBM_notm}} Container. Les
groupes de conteneurs permettent d'assurer une haute disponibilité et une évolutivité.

      - Vous pouvez créer un parc
de serveurs {{site.data.keyword.mobilefirst}} en configurant le nombre
de noeuds à cet endroit. 

Pour plus de détails, reportez-vous à la
[documentation
d'{{site.data.keyword.mobilefoundation_long}}](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window}. 
