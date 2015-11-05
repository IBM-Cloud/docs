{:new_window: target="_blank"} 
{:shortdesc: .shortdesc}

#{{site.data.keyword.Bluemix_notm}} dédié
{: #dedicated}

*Dernière mise à jour : 20 octobre 2015*

{{site.data.keyword.Bluemix}} est une plateforme à normes ouvertes reposant sur le cloud
qui permet de construire, d'exécuter et de gérer des applications. Avec l'environnement {{site.data.keyword.Bluemix_notm}} dédié, vous bénéficiez
de la puissance et de la simplicité de {{site.data.keyword.Bluemix_notm}}., et
ce dans votre propre environnement SoftLayer dédié, connecté de façon sécurisée à l'environnement {{site.data.keyword.Bluemix_notm}} public et à
votre propre réseau. {:shortdesc}

L'environnement {{site.data.keyword.Bluemix_notm}} dédié inclut un catalogue privé qui affiche les services
dédiés disponibles exclusivement pour vous. Il inclut également des services supplémentaires qui sont à votre disposition depuis l'environnement
{{site.data.keyword.Bluemix_notm}} public.

L'environnement {{site.data.keyword.Bluemix_notm}} dédié s'appuie sur SoftLayer pour que vous puissiez bénéficier de l'infrastructure de cloud la plus performante. Chaque centre de données applique des contrôles rigoureux de sécurité 24 heures sur 24, 7 jours sur 7. 
Vous et IBM accédez à votre instance {{site.data.keyword.Bluemix_notm}} dédiée via un tunnel de réseau privé virtuel et un réseau local virtuel privé.

![{{site.data.keyword.Bluemix_notm}}
dédié](images/detaileddedicated.png "{{site.data.keyword.Bluemix_notm}} dédié")

*Figure 1. Diagramme détaillé de l'environnement {{site.data.keyword.Bluemix_notm}} dédié*

Les environnements {{site.data.keyword.Bluemix_notm}} dédiés appliquent les mêmes normes de sécurité que
l'environnement {{site.data.keyword.Bluemix_notm}} public en termes d'infrastructure, de fonctionnement et de
sécurité physique. Toutefois, l'accès des développeurs à l'environnement {{site.data.keyword.Bluemix_notm}}
dédié est contrôlé par vos stratégies LDAP, qui peuvent être configurées par l'équipe
{{site.data.keyword.Bluemix_notm}} lorsqu'elle configure votre environnement. Dans l'environnement dédié,
vous pouvez gérer les rôles utilisateur et les droits. Voir [Gestion des utilisateurs et des droits](../admin/index.html#oc_useradmin) pour des détails.


L'environnement {{site.data.keyword.Bluemix_notm}} dédié est fourni avec tous les contextes d'exécution
{{site.data.keyword.Bluemix_notm}} et 128 Go de mémoire pour les applications.

De plus, il existe un ensemble de services inclus par défaut, ainsi que des ensembles facultatifs que vous pouvez choisir pour votre instance dédiée. 

| **Type**        | **Nom**            | **Description** |      
|-----------------|-------------------|-------------------|
| Inclus | {{site.data.keyword.autoscaling}} | Augmentez ou diminuez dynamiquement la capacité de traitement de votre application en fonction de règles. Avec ce service,
vous bénéficiez d'une utilisation illimitée dans votre environnement {{site.data.keyword.Bluemix_notm}} dédié. |
| Inclus | {{site.data.keyword.datacshort}} | Ce service fournit une grille de données en mémoire qui prend en charge des scénarios de mise en cache distribuée
pour vos
applications. Il inclut 50 Go de mémoire cache interne. |
| Inclus | {{site.data.keyword.cloudant}} | Base de données NoSQL d'IBM qui fournit une couche de données JSON dont les performances sont élevées
(compatible avec CouchDB). Inclut 1,6 To et jusqu'à 3000 demandes d'API par seconde. |
| Facultatif | {{site.data.keyword.sqldb}} | IBM {{site.data.keyword.sqldbfull}} Database for {{site.data.keyword.Bluemix_notm}}
ajoute une base de données relationnelle complète à votre application. {{site.data.keyword.sqldb}} fournit une base de données gérée permettant de traiter les charges de
travail transactionnelles et Web exigeantes liées à votre activité. |
| Facultatif | {{site.data.keyword.mql}} | IBM {{site.data.keyword.mqlfull}} for {{site.data.keyword.Bluemix_notm}} est un service de messagerie reposant sur le cloud qui fournit une messagerie souple et facile à
utiliser pour les applications {{site.data.keyword.Bluemix_notm}}. {{site.data.keyword.mql}} constitue une solution d'administration simple pour la messagerie. 
Vous pouvez utiliser {{site.data.keyword.mql}} pour rendre vos applications plus réactives et plus évolutives, et vous pouvez partager et décharger le travail entre des
applications à l'aide d'une API puissante et simple.  |
| Facultatif | {{site.data.keyword.dashdbshort}} | Utilisez dashDB pour stocker les données relationnelles, notamment les types spéciaux tels que les
données géospatiales. Ensuite, analysez ces données avec l'analyse intégrée avancée ou SQL, comme l'analyse
prédictive et l'exploration de données, l'analyse avec R et l'analyse géospatiale. |

*Tableau 1. Services dédiés*

##Configuration de l'environnement {{site.data.keyword.Bluemix_notm}} dédié
{: #setupdedicated}

L'environnement {{site.data.keyword.Bluemix_notm}} dédié a été conçu pour fournir une version privée
de l'offre d'environnement {{site.data.keyword.Bluemix_notm}} public. Vous pouvez utiliser les services et les contextes d'exécution {{site.data.keyword.Bluemix_notm}} pour répondre
à vos besoins informatiques dans un compte SoftLayer hébergé par IBM. 

IBM fournit l'accès à l'environnement {{site.data.keyword.Bluemix_notm}} dédié par le biais d'une connexion sécurisée par mot de passe. Vous
pouvez accéder aux services, aux contextes d'exécution et aux ressources associées, et déployer et retirer des applications
{{site.data.keyword.Bluemix_notm}}. IBM utilise plusieurs emplacements SoftLayer afin de distribuer l'environnement {{site.data.keyword.Bluemix_notm}} dédié, pour que l'emplacement de votre version privée puisse être proche de vous.

Pour configurer votre version privée de {{site.data.keyword.Bluemix_notm}} :

<ol>
<li>Prenez contact avec votre représentant de compte IBM ou avec <a href="https://console.ng.bluemix.net/?direct=classic/#/contactUs/cloudOEPaneId=contactUs" target="_blank">{{site.data.keyword.Bluemix_notm}}</a> pour commencer.</li>
<li>Le prix mensuel dépend des services dédiés que vous voulez utiliser, et comprend un abonnement à tous les services
{{site.data.keyword.Bluemix_notm}} publics. Vous recevez ensuite une facture pour tous les éléments que vous
utilisez au-delà de ce contrat d'abonnement.
	<ol type="a">
	<li>Décidez avec IBM du tarif correspondant à votre instance {{site.data.keyword.Bluemix_notm}} dédiée.	Le prix mensuel dépend des services dédiés que vous voulez utiliser, et comprend un abonnement à tous les services
{{site.data.keyword.Bluemix_notm}} publics. Vous recevez ensuite une facture pour tous les éléments que vous
utilisez au-delà de ce contrat d'abonnement.</li>
	<li>Identifiez les échéances pour chaque phase de configuration de votre instance {{site.data.keyword.Bluemix_notm}} dédiée.</li>
	</ol>
	</li>
<li>Sélectionnez l'<a href="http://www.softlayer.com/data-centers" target="_blank">emplacement du centre de données SoftLayer</a> pour votre instance dédiée. Ensuite, votre plateforme dédiée et votre
compte sont créés. Pour votre compte, vous identifiez les personnes de votre organisation à affecter aux rôles nécessaires à la configuration et à
l'exécution
de votre instance dédiée. A chaque rôle correspond un interlocuteur IBM.<br />
<p>Rôles du client : </p>
<dl>
<dt>**Contact du service Achats (Procurement focal)**</dt>
<dd>Collabore avec l'interlocuteur IBM pour établir votre environnement {{site.data.keyword.Bluemix_notm}} dédié, notamment en identifiant les
personnes dans votre organisation devant travailler sur certains aspects du projet. Ce rôle supervise la sélection de pattern, les accords commerciaux et
les accords relatifs à l'accès aux ressources du client. Le contact du service Achats est le contact général pour la configuration de
l'instance
dédiée.</dd>
<dt>**Agent de conformité (Compliance officer)**</dt>
<dd>Collabore avec l'interlocuteur IBM pour sélectionner une topologie et une option de déploiement répondant à vos exigences en matière de sécurité.
Ce rôle collabore avec le consultant en conformité d'IBM pour déterminer quels sont les patterns de déploiement qui permettent d'atteindre les buts et les
objectifs de conformité. </dd>
<dt>**Spécialiste réseau (Network Specialist)**</dt>
<dd>Collabore avec l'interlocuteur IBM sur les plans de réseau pour le déploiement {{site.data.keyword.Bluemix_notm}}.
Ce rôle fournit les exigences à l'interlocuteur IBM, avec qui il collabore pour établir un plan d'implémentation. A la fin de la phase d'installation et de
vérification, il confirme que la configuration du réseau est conforme aux standard d'entreprise.
</dd>
<dt>**Contact DevOps (DevOps focal)**</dt>
<dd>Collabore avec l'interlocuteur IBM pour planifier et appliquer les mises à jour de maintenance nécessaires pour la plateforme, les services et les
contextes d'exécution {{site.data.keyword.Bluemix_notm}}. Ce rôle collabore également avec l'interlocuteur IBM sur la configuration de votre
instance {{site.data.keyword.Bluemix_notm}} dédiée.</dd>
</dl>
<p>Rôles d'IBM : </p>
<dl>
<dt>**Gestionnaire des mises à disposition IBM (IBM provisioning manager)**</dt>
<dd>Collabore avec le contact du service Achats pour établir l'environnement client. </dd>
<dt>**Consultant en conformité IBM (IBM compliance consultant)**</dt>
<dd>Collabore avec l'agent de conformité du client pour sélectionner une topologie et une option de déploiement répondant à vos exigences en matière de
sécurité.</dd>
<dt>**Spécialiste réseau IBM (IBM network specialist)**</dt>
<dd>Collabore avec le spécialiste réseau du client afin d'établir les plans de réseau pour le déploiement.
Ce rôle collabore avec le client afin de collecter les exigences et de créer un plan d'implémentation. Il effectue également des tests automatisés pour
vérifier le résultat physique du plan d'implémentation.
</dd>	
<dt>**Contact Devops IBM (IBM DevOps focal)**</dt>
<dd>Collabore avec le contact DevOps du client sur l'installation et la maintenance continue de la topologie de déploiement. Ce rôle collabore avec le
client afin de planifier et d'effectuer les mises à jour nécessaires pour la plateforme et les services.
</dd>
</dl>
</li>
<li>Définissez et établissez la connectivité du réseau entre votre réseau d'entreprise et votre instance {{site.data.keyword.Bluemix_notm}} dédiée.
	<ol type="a">
	<li>IBM installe une infrastructure de surveillance et de sécurité pour l'instance dédiée.</li>
	<li>IBM installe les services dédiés exclusifs que vous avez sélectionnés.</li>
	<li>Vous fournissez la configuration réseau et des noeuds finaux pour des
éléments, tels que les adresses IP ou les pare-feux, et l'accès à LDAP pour l'intégration à {{site.data.keyword.Bluemix_notm}}.</li>
	</ol>
</li>
<li>Identifiez et affectez des rôles pour votre équipe d'administration de l'environnement.
	<ol type="a">
	<li>IBM configure l'accès réseau et LDAP en fonction des éléments que vous avez fournis. L'accès administrateur est accordé aux contacts que vous désignez. Vous devez également désigner un contact pour le support et la facturation.</li>
	<li>IBM configure un catalogue mixte dans votre environnement dédié qui répertorie vos services dédiés et plusieurs des services {{site.data.keyword.Bluemix_notm}} publics.</li>
	<li>Vous validez la configuration du réseau et du pare-feu ainsi que l'accès et le noeud final LDAP.</li>
	</ol>
</li>
</ol>

##Gestion de votre instance dédiée
{: #maintaindedicated}

IBM gère et installe les mises à jour et les correctifs qu'elle juge nécessaires pour la plateforme, les contextes d'exécution et les services de
l'environnement {{site.data.keyword.Bluemix_notm}} dédié.

**Important** : IBM se réserve le droit d'interrompre des services afin de procéder à une maintenance d'urgence si nécessaire. IBM
peut changer les heures de maintenance planifiées et vous fera part de tels changements et de toute information relative à la maintenance d'urgence. 

Les types suivants de maintenance sont requis pour l'environnement {{site.data.keyword.Bluemix_notm}}
dédié :
<dl>
<dt>**Fenêtres de maintenance standard**</dt>
<dd>Les services utilisent des fenêtres de maintenance standard prédéfinies qui peuvent entraîner leur indisponibilité.
IBM n'exige pas l'approbation du client avant de procéder à la maintenance, mais tente de réduire
l'impact sur vos services.
<br />
<br />
IBM envoie des messages de diffusion concernant les changements qui sont planifiés pour chaque fenêtre de maintenance par courrier électronique, par
téléphone ou par d'autres moyens.<br />
<br />
**Important** : certains services peuvent ne pas être disponibles au cours de la période de maintenance.</dd>

<dt>**Fenêtre de maintenance mensuelle**</dt>
<dd>La fenêtre de maintenance mensuelle est convenue entre vous et IBM dans une fenêtre de 21 jours. Vous pouvez fournir à IBM des dates ou des heures
spécifiques qui ne vous conviennent pas dans la fenêtre de 21 jours. IBM tente de planifier les mises à jour en dehors de ces dates ou de ces heures. En
fonction des demandes, IBM vous communique la fenêtre de maintenance planifiée. Les fenêtres de maintenance mensuelle n'ont généralement pas d'impact
sur l'environnement Bluemix dédié en cours d'exécution.
<br />
<br />
**Remarque :** si vous ne proposez pas d'heure spécifique pour la mise à jour, la maintenance est appliquée automatiquement à la fin de
la fenêtre.
<br />
<br />
Accédez à **ADMINISTRATION > SYSTEM INFORMATION** pour afficher les mises à jour en attente, définir des dates d'indisponibilité et
approuver des mises à jour. Pour plus d'informations sur les notifications et la planification des mises à jour en attente, voir
<a href="../admin/index.html#oc_system">Affichage des informations système</a>. </dd>
	
<dt>**Autre**</dt>
<dd>IBM entend regrouper les maintenances pouvant avoir un impact sur vos services, en particulier la disponibilité de votre environnement
{{site.data.keyword.Bluemix_notm}} dédié, de vos
contextes d'exécution et de vos services, dans les mises à jour standard et mensuelles.
D'autres fenêtres de maintenance peuvent être utilisées exceptionnellement pour la gestion de l'environnement. IBM fera de son mieux pour limiter l'impact
sur vos activités pendant ces fenêtres de maintenance et vous avertira à l'avance. </dd>
</dl>

Pour configurer la maintenance de votre instance dédiée, collaborez avec votre représentant de compte IBM afin de convenir d'une fenêtre pour la
maintenance standard.
