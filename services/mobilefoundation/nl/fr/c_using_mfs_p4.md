---

copyright:
  years: 2016, 2017
lastupdated:  "2017-02-17"

---

#	Utilisation du plan Professional Per Capacity
{: #using_mobilefoundation_p4}

Avec le plan Professional Per Capacity, les utilisateurs
peuvent créer un certain nombre d'applications mobiles avec
plusieurs systèmes d'exploitation mobiles.
Une fois que vous avez créé l'instance de service
{{site.data.keyword.mobilefoundation_short}}: Professional Per Capacity, lisez la procédure ci-après pour commencer à l'utiliser.

## Conditions prérequises
{: #prerequisites_p4}

Prenez connaissance des éléments suivants avant de configurer
l'instance de service
{{site.data.keyword.mobilefoundation_short}}: Professional Per Capacity.
* {{site.data.keyword.mobilefoundation_short}}:
Professional Per Capacity est pris en charge uniquement avec les
plans {{site.data.keyword.Bluemix_notm}}
{{site.data.keyword.dashdbshort_notm}}: Enterprise
Transactional (prenant en charge OLTP).

* Vous devez avoir accès aux données d'identification de l'instance de service {{site.data.keyword.dashdbshort_notm}} avant de pouvoir configurer les paramètres de votre instance de service {{site.data.keyword.mobilefoundation_short}}.

**Remarque** : L'instance de service {{site.data.keyword.dashdbshort_notm}} peut exister dans n'importe quel `espace` de votre {{site.data.keyword.Bluemix_notm}} `organisation` ou de n'importe quelle autre `organisation` à laquelle vous avez accès. Assurez-vous que vous disposez des droits nécessaires pour accéder à l'`espace` dans lequel l'instance de service {{site.data.keyword.dashdbshort_notm}} service existe.


## Ajout de la connexion à la base de données
{: #configure_dashdb_p4}

###  Premières étapes
{: #firststeps_p4}

Une fois que vous avez créé l'instance de service {{site.data.keyword.mobilefoundation_short}}: Professional Per Capacity, lisez la procédure ci-après pour commencer à l'utiliser.

### Configuration de la connexion à l'instance de service dashDB
{: #connect_dashdb_p4}

Une fois l'instance de service {{site.data.keyword.mobilefoundation_short}}: Professional Per Capacity créée, la page
*Présentation* s'affiche et vous devez y spécifier les informations de connexion à l'instance de service
{{site.data.keyword.dashdbshort_notm}} for Transactions à laquelle l'instance de service
{{site.data.keyword.mobilefoundation_short}} doit se connecter.

**Remarque :** Si vous disposez déjà d'une instance de service {{site.data.keyword.dashdbshort_notm}} for
Analytics: Enterprise for Transactions, vous pouvez configurer votre instance Mobile Foundation pour utiliser celle-ci pour se connecter à
l'instance de service {{site.data.keyword.mobilefoundation_short}}.

Vous pouvez également créer une nouvelle instance de service {{site.data.keyword.dashdbshort_notm}} for Transactions
si vous n'en avez encore aucune.

Procédez comme suit pour créer une nouvelle instance de service dashDB for Transactions :

1. Sur la page *Présentation*, sélectionnez la section **Créer un service**.

+ Sélectionnez `Oui` pour l'option **Configuration de haute disponibilité** si vous désirez
disposer d'une instance de service {{site.data.keyword.dashdbshort_notm}} for Transactions à haute disponibilité.

+ Examinez les détails du plan et cliquez sur **Créer**.

Une nouvelle instance de service {{site.data.keyword.dashdbshort_notm}} for Transactions: EnterpriseForTransactions2.8.500 est créée, ce qui vous
procure une instance {{site.data.keyword.dashdbshort_notm}} dédiée dotée de 8 Go de mémoire RAM, de 2 vCPU (UC virtuelles) et de 500 Go d'espace de stockage.

Procédez comme suit pour vous connecter à une instance de service {{site.data.keyword.dashdbshort_notm}} existante ou à l'instance de service {{site.data.keyword.dashdbshort_notm}} for Transactions que vous venez de créer :

1. Sélectionnez l'{{site.data.keyword.Bluemix_notm}} `organisation` dans laquelle l'instance de service {{site.data.keyword.dashdbshort_notm}} existe.

+ Depuis la liste des espaces disponibles dans `Organisation`, sélectionnez l'élément `Espace` {{site.data.keyword.Bluemix_notm}} dans lequel se trouve l'instance de service {{site.data.keyword.dashdbshort_notm}},   
**Remarque :** Si l'`organisation` et l'`espace` dans lesquels réside votre instance de service {{site.data.keyword.dashdbshort_notm}} ne figurent pas dans la liste, vérifiez que vous êtes membre de cette `organisation` et de cet `espace`. Vous
devez être affecté au rôle *Développeur* dans l'organisation et l'espace vu que le service {{site.data.keyword.mobilefoundation_short}}
accède aux données d'identification du service {{site.data.keyword.dashdbshort_notm}}.

+ Sélectionnez également le nom du service (`Service
Name`) et les données d'identification
(`Credentials`) {{site.data.keyword.dashdbshort_notm}}
pour la connexion à l'instance de service
{{site.data.keyword.dashdbshort_notm}}.

+  Testez la connexion à l'instance de service {{site.data.keyword.dashdbshort_notm}} spécifiée.

+  Cliquez sur **Ajouter**. Cela permet de créer les tables requises dans l'instance de service de base de
données {{site.data.keyword.dashdbshort_notm}} configurée.

Après quelques secondes, vous pouvez accéder à la page `Overview` qui fournit des tutoriels et des vidéos facilitant vos premiers pas avec le service {{site.data.keyword.mobilefoundation_short}}.

**Remarque** : Vous ne pouvez pas modifier l'instance de service {{site.data.keyword.dashdbshort_notm}} configurée pour être utilisée par votre instance de service {{site.data.keyword.mobilefoundation_short}}. Vous pouvez toutefois utiliser la même instance de service {{site.data.keyword.dashdbshort_notm}} sur plusieurs instances de service {{site.data.keyword.mobilefoundation_short}}, car chaque instance de service {{site.data.keyword.mobilefoundation_short}} crée son propre schéma dans l'instance de service {{site.data.keyword.dashdbshort_notm}} sélectionnée.

## Démarrage du serveur MobileFirst
{: #start_mobilefoundation_p4}

* Pour démarrer {{site.data.keyword.mfserver_short_notm}} avec les paramètres par défaut, cliquez sur **Start Basic Server**.

* Cette option affecte les paramètres suivants à un serveur {{site.data.keyword.mfserver_long_notm}} :
    -  2 noeuds avec 1 Go de mémoire chacun. Cette taille
convient pour des activités de développement et des activités de
test sommaires et pour des charges de travail à faible échelle.

    -	Le `nom_d'utilisateur` et le
`mot_de_passe` sont générés automatiquement pour
vous. Vous pouvez y accéder une fois que le serveur est en opération.

L'implantation de votre serveur débute. Ce processus prend environ 10 minutes et une fenêtre de message indique la progression de l'opération. A son terme, un tableau de bord s'affiche et présente les éléments suivants :

  -	L'état du serveur que vous exécutez (état, taille).

  -	La route de serveur créée pour vous. Utilisez cette route dans votre application mobile pour vous connecter à {{site.data.keyword.mfserver_short_notm}}.

  -	Votre `nom_d'utilisateur` personnel et votre `mot_de_passe` pour accéder à la console {{site.data.keyword.mfp_oc_short_notm}}. Le `mot_de_passe` est masqué. Cliquez sur l'icône **Show Password** pour le visualiser.

*	Cliquez sur **Launch Console** pour ouvrir la console {{site.data.keyword.mfp_oc_short_notm}}.


<!--This console runs inside the container.--> Elle vous permet de gérer vos applications, adaptateurs et
périphériques mobiles, ainsi que l'utilisation de votre serveur en
tant que serveur dorsal mobile, l'envoi de notifications push, etc.

##  Ajout d'un serveur Mobile Analytics
{: #adding_analytics_server_p4}

 Vous pouvez maintenant surveiller votre application mobile sur un serveur {{site.data.keyword.mobilefirst}} en ajoutant un serveur Mobile Analytics à l'instance de service {{site.data.keyword.mobilefoundation_short}}.

 Le plan Professional crée le serveur Mobile Analytics dans un
groupe de conteneurs, l'utilisateur peut personnaliser la
configuration en sélectionnant le nombre de noeuds de conteneur dans
le groupe de conteneurs.

 Les utilisateurs peuvent aussi connecter des volumes aux conteneurs pour conserver les données. Le volume une fois sélectionné ne peut être changé. L'espace de partage de fichiers par défaut disponible pour l'utilisateur est de 20 Go. Si l'utilisateur a besoin d'un espace de stockage supplémentaire pour conserver des données d'analyse, il est invité à acheter un partage de fichiers supplémentaire et à créer un volume en utilisant ce partage de fichier. Il peut ensuite sélectionner ce nouveau volume lors du déploiement du serveur d'analyse.

 Pour plus d'informations sur l'ajout de volumes dans {{site.data.keyword.containerlong}}, voir [Stockage de données persistantes dans un volume à l'aide du tableau de bord {{site.data.keyword.Bluemix_notm}} ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/docs/containers/container_volumes_ov.html#container_volumes_ui.html){: new_window}.

* Cliquez sur commande d'ajout d'analyse pour ajouter le serveur Mobile Analytics à l'instance de service {{site.data.keyword.mobilefoundation_short}}.

* Vous pouvez utiliser la configuration de serveur Mobile
Analytics : la configuration de serveur minimum prise en charge
pour le serveur d'analyse est de 2
noeuds avec un 1 Go de mémoire chacun, et vous pouvez choisir de
créer un serveur d'analyse avec une configuration maximum de 32
noeuds avec 16 Go de mémoire chacun.

Le processus de mise à disposition commence. Ce processus prend environ 10 minutes et une fenêtre de
message indique la progression de l'opération.  

* Lancez MobileFirst Analytics depuis {{site.data.keyword.mfp_oc_short_notm}}.

* La connexion unique est activée entre {{site.data.keyword.mfserver_short_notm}} et le serveur Mobile Analytics. Le serveur Mobile Analytics est configuré avec les mêmes clés LTPA et données d'identification de l'utilisateur que celles du serveur {{site.data.keyword.mfserver_short_notm}}. Vous pouvez vous servir des mêmes
`nom_d'utilisateur` et
`mot_de_passe` pour vous connecter à la console
Mobile Analytics que ceux utilisés pour la connexion à
{{site.data.keyword.mfp_oc_short_notm}}.

Pour plus d'informations sur MobileFirst Analytics, accédez au site [MobileFirst Foundation Operational Analytics ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/analytics/){: new_window}.

**Remarque :** le serveur Mobile Analytics est retiré quand vous supprimez l'instance de service {{site.data.keyword.mobilefoundation_short}} ou si vous tentez de recréer le serveur {{site.data.keyword.mfserver_short_notm}}.

##  Suppression du serveur Mobile Analytics
{: #deleting_analytics_server_p4}

Vous pouvez à présent supprimer depuis le tableau de bord du service {{site.data.keyword.mobilefoundation_short}} le serveur
Mobile Analytics qui a été ajouté à l'instance de service {{site.data.keyword.mobilefoundation_short}} .

* Cliquez sur **Supprimer le serveur Analytics** pour supprimer le serveur Mobile Analytics qui a été ajouté à l'instance de service
{{site.data.keyword.mobilefoundation_short}}.

 Ceci a pour effet de supprimer le groupe de conteneurs Analytics. Cette opération prend environ 10 minutes. Vous pouvez actualiser l'écran pour examiner le
statut mis à jour. Une fois les conteneurs Analytics supprimés, le bouton **Ajouter un serveur Analytics** est réactivé pour vous permettre
éventuellement d'ajouter à nouveau le serveur Mobile Analytics.

## Re-création du serveur MobileFirst
{: #recreate_mobilefoundation_p4}

*	Cliquez sur **Recreate** pour recréer le
serveur.

* Cette action arrête votre serveur existant et supprime les données. Une nouvelle instance de serveur est créée avec une version mise à jour, si elle est disponible. Cette action prend quelques minutes avant de s'achever.

**Remarque** : Toutes les données provenant de votre instance de serveur précédente, y compris les informations sur les applications et les adaptateurs, sont conservées dans l'instance de service {{site.data.keyword.dashdbshort_notm}} configurée ; elles sont utilisées pour recréer le serveur.

##	Paramétrage d'une configuration avancée
{: #using_mfs_advanced_p4}

L'option **Start Server with Advanced Configuration** de la page `Overview` permet de créer le serveur avec des paramètres avancés ou personnalisés. Vous pouvez également mettre à jour les paramètres du serveur pour personnaliser sa configuration en cliquant sur l'onglet **Configuration**. {{site.data.keyword.mobilefoundation_short}} vous permet d'accéder à certains paramètres avancés.

*	Dans l'onglet **Topology**, vous pouvez sélectionner la taille du serveur, ainsi que le nombre d'instances de serveur dont vous avez besoin. Le serveur par défaut doté d'1 Go est idoine pour le développement et des tests sommaires.
  - Sélectionnez la taille appropriée pour votre serveur compte tenu de vos besoins.

  - **Nodes** affiche le nombre de noeuds créés.

      - Vous pouvez créer un parc de serveurs {{site.data.keyword.mobilefirst}} en configurant le nombre de noeuds à cet endroit. La configuration minimum prise en charge est de 2 noeuds avec un 1 Go
de mémoire chacun, et la configuration
maximum prise en charge est de 32 noeuds avec 16 Go de mémoire chacun.

Pour plus de détails, voir la documentation [{{site.data.keyword.mobilefoundation_long}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window}.
