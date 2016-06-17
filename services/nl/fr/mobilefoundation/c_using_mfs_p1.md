---

copyright:
  years: 2016

---

#	Utilisation de {{site.data.keyword.mobilefoundation_short}}: Developer
{: #using_mobilefoundation_p1}

Une fois que vous avez créé l'instance de service
{{site.data.keyword.mobilefoundation_short}}: Developer, procédez
comme indiqué ci-après commencer à utiliser le service : 

* Acceptez les dispositions du contrat de licence d'{{site.data.keyword.mfp_full_notm}} V8.0.0.0.

* Entrez vos données d'identification
{{site.data.keyword.Bluemix_notm}}. Vous autorisez ainsi le service à
apporter des modifications dans votre espace
{{site.data.keyword.Bluemix_notm}} et à créer des conteneurs
{{site.data.keyword.containerlong}} qui hébergent votre serveur {{site.data.keyword.mobilefirst_notm}}.

Au bout de quelques secondes, vous pouvez accéder à la page *Vue
d'ensemble* sur {{site.data.keyword.Bluemix_notm}}, laquelle vous permet d'accéder à des tutoriels et des vidéos
facilitant vos premiers pas avec le service {{site.data.keyword.mobilefoundation_short}}.

## Démarrage du serveur {{site.data.keyword.mobilefirst}}
{: #start_mobilefoundation_p1}
* Pour démarrer le serveur
{{site.data.keyword.mfserver_short_notm}} avec les paramètres par
défaut, cliquez sur **Start Basic Server**.

![Start Basic Server](images/start_basic_server.png "Figure 1. Start Basic Server")
{: screen}

Cette option affecte les paramètres suivants à un serveur {{site.data.keyword.mfserver_long_notm}} :
*	1 Go de mémoire et 64 Go de stockage. Cette taille est suffisante pour un contexte de développement et des activités de test
sommaires.

*	Le *nom_d'utilisateur* et le *mot_de_passe* sont générés automatiquement pour vous. Vous pouvez y accéder une fois que le
serveur est en opération.

Le processus de mise à disposition commence. Ce processus prend environ 10 minutes et une fenêtre de
message indique la progression de l'opération. A son terme, un tableau de bord s'affiche et présente les éléments suivants :
*	Le statut du serveur que vous exécutez (état, taille, stockage).

*	La route du serveur créé pour vous. Utilisez cette route pour joindre votre serveur mobile depuis l'Internet public. Vos applications mobiles utilisent cette
route pour accéder au serveur.

*	Votre *nom_d'utilisateur* personnel et votre *mot_de_passe*
pour accéder à la console {{site.data.keyword.mfp_oc_short_notm}}. Le
*mot_de_passe* est masqué. Cliquez sur l'icône en forme d'oeil pour le visualiser.

*	Cliquez sur **Launch Console** pour lancer la
console {{site.data.keyword.mfp_oc_short_notm}}.

![Launch Console](images/launch_console.png "Figure 2. Launch Console")
{: screen}

Cette console s'exécute dans le conteneur. Elle vous permet de gérer
vos applications et périphériques mobiles, l'utilisation de votre serveur en
tant que serveur dorsal mobile, l'envoi de notifications push, etc. 

## Re-création du serveur {{site.data.keyword.mobilefirst}} 
{: #recreate_mobilefoundation_p1}

*	Cliquez sur **Recreate** pour re-créer le serveur. 

![Recreate](images/recreate.png "Figure 3. Recreate")
{: screen}

* Cette action arrête votre serveur existant et le supprime. Toutes les
données de votre serveur mobile sont perdues. Une nouvelle instance de serveur
est créée. Cette action prend quelques minutes avant de s'achever.

##	Paramétrage d'une configuration avancée
{: #using_mfs_advanced_p1}

L'option **Start Server with Advanced Configuration**
de la page *Overview* permet de créer le serveur avec des
paramètres avancés ou personnalisés. Vous pouvez également mettre à jour les paramètres du serveur
pour personnaliser sa configuration en cliquant sur l'onglet **Configuration**. {{site.data.keyword.mobilefoundation_short}}
vous permet d'accéder à certains paramètres avancés. 

*	L'onglet **Topology** vous permet de sélectionner
la taille de topologie de votre conteneur. Le serveur par défaut doté d'1 Go
est idoine pour le développement et des tests sommaires, mais peut s'avérer
insuffisant, par exemple, pour tester la charge. 
  - Sélectionnez la taille appropriée pour votre serveur compte tenu de
vos besoins.   


* **Nodes** affiche le nombre de noeuds créés. Cette
zone  n'est pas modifiable dans {{site.data.keyword.mobilefoundation_short}}: Developer. Vous
pouvez voir le nombre de noeuds obtenus dans vos groupes
{{site.data.keyword.IBM_notm}} Container. Les
groupes de conteneurs permettent d'assurer une haute disponibilité et une évolutivité.

Pour plus de détails, reportez-vous à la
[documentation
d'{{site.data.keyword.mobilefoundation_long}}](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window}. 
