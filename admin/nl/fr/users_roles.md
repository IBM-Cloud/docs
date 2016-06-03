---



copyright:

  years: 2015, 2016



---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Gestion des membres d'équipe et des rôles 
{: #userroles}
*Dernière mise à jour : 16 mai 2016*

Depuis la page **Répertoire d'équipe** pour votre compte, vous pouvez gérer les membres d'équipe existants et leurs rôles dans votre
organisation et vos espaces, ainsi qu'inviter de nouveaux membres d'équipe. Afin d'accéder au répertoire d'équipe pour votre compte,
cliquez sur l'icône **Compte et support** ![Icône Compte et support](../admin/images/account_support.svg) &gt;
**Compte** &gt; *nom_de_votre_compte* &gt; **Répertoire d'équipe**.
{:shortdesc}

Un propriétaire de compte effectue toutes les opérations sur les organisations et les espaces, y compris la gestion des membres d'équipe et des
rôles qui leur sont affectés. Un responsable de l'organisation peut inviter des membres d'équipe et gérer leurs rôles. Un responsable de l'espace
peut utiliser la page **Gérer les organisations** pour ajouter des membres de compte existants à l'espace et ajuster leurs rôles. Lisez
les informations ci-après pour en savoir plus sur les rôles.


## Rôles
{: #userrolesinfo}

Au niveau du compte, deux rôles permettent l'accès à différentes fonctions de gestion des comptes : 

*Tableau 1. Rôles de compte et droits*

| Rôle de compte  | Droits |    
|----------------|---------|
|Propriétaire | Un propriétaire de compte peut accéder à son profil, au répertoire d'équipe, aux informations de facturation, aux notifications relatives
aux dépenses et au tableau de bord de l'utilisation. Dans la page Répertoire d'équipe, le propriétaire peut inviter de nouveaux membres d'équipe et
ajuster les rôles. Il peut également ajouter des offres promotionnelles, définir ou changer la limite de facturation, définir l'accès aux services et gérer
les organisations et les espaces.
 |
|Membre | Un membre peut accéder à son profil, au répertoire d'équipe, aux crédits du compte et aux limites de facturation dans l'en-tête
{{site.data.keyword.Bluemix_notm}}. Toutefois, dans la page Répertoire d'équipe, un membre ne peut afficher que les membres d'équipe
existants sur le compte.  |

 Les nouveaux membres d'équipe sont ajoutés en tant que membre du compte. Vous pouvez affecter des rôles d'organisation et d'espace aux invités afin
d'activer des vues et des droits spécifiques dans {{site.data.keyword.Bluemix_notm}}. Les nouveaux membres d'équipe ajoutés à une organisation
possèdent le rôle Auditeur de l'organisation par défaut.
Pour un espace spécifique, vous pouvez choisir d'affecter le rôle Développeur ou Auditeur aux invités.
Une fois que vos invités ont accepté l'invitation et rejoint {{site.data.keyword.Bluemix_notm}}, vous pouvez éditer leurs rôles dans la page
**Répertoire d'équipe**. 

Les rôles suivants peuvent être affectés au niveau de l'organisation : 

*Tableau 2. Rôles d'organisation et droits*

| Rôle d'organisation  | Droits |    
|-------------------|-------------|
|Responsable  | Un responsable de l'organisation peut créer, éditer ou supprimer des espaces dans l'organisation, afficher l'utilisation et le quota
de l'organisation, inviter des membres d'équipe dans l'organisation, définir quels sont les membres qui ont accès à l'organisation ainsi que les rôles de
ces membres dans l'organisation, et gérer des domaines personnalisés pour l'organisation.
 |
|Responsable de la facturation  | Un responsable de la facturation peut afficher des informations sur l'utilisation des contextes d'exécution et des
services pour l'organisation dans la page Tableau de bord de l'utilisation.   |
|Auditeur | Un auditeur de l'organisation peut afficher le contenu des applications et des services dans l'organisation. Il peut également
afficher les membres d'équipe dans l'organisation et les rôles qui leur sont affectés, ainsi que le quota pour l'organisation. Ce rôle est affecté à
tous les invités par défaut. |

Les rôles suivants peuvent être affectés au niveau de l'espace : 

*Tableau 3. Rôles d'espace et droits*

| Rôle d'espace  | Droits |    
|------------|-------------|
|Responsable  | Un responsable de l'espace peut ajouter des membres d'équipe existants et gérer les rôles dans l'espace. Il peut également afficher le
nombre d'instances, les liaisons de service et l'utilisation des ressources pour chaque application dans l'espace.
 |
|Développeur | Un développeur de l'espace peut créer, supprimer et gérer des applications et des services dans l'espace. Certaines tâches de gestion
impliquent le déploiement d'applications, le démarrage ou l'arrêt d'applications, le changement de nom d'une application, la suppression d'une application,
le changement de nom d'un espace, la liaison d'un service ou l'annulation de la liaison d'un service à une application ainsi que l'affichage du nombre
d'instances, des liaisons de service et de l'utilisation des ressources pour chaque application dans l'espace.
De plus, le développeur de l'espace peut associer une adresse URL interne ou externe à une application dans l'espace.
   |
|Auditeur | Un auditeur de l'espace dispose de l'accès en lecture à toutes les informations sur l'espace, telles que le nombre d'instances, les liaisons de
service et l'utilisation des ressources pour chaque application dans l'espace.
 |

**Remarque** : les membres d'équipe qui possèdent le rôle de responsable ou de développeur de l'espace peuvent accéder à la
variable
d'environnement VCAP_SERVICES. Toutefois, un membre d'équipe possédant le rôle d'auditeur ne peut pas y accéder. 

## Invitation de membres d'équipe 
{: #inviteteammembers}

Les propriétaires de compte et les responsables de l'organisation peuvent inviter des membres d'équipe dans des organisations depuis la page Inviter
des membres d'équipe. Lorsque vous ajoutez de nouveaux membres d'équipe, le rôle Auditeur leur est affecté automatiquement. Vous pouvez changer les rôles
ultérieurement dans la page Répertoire d'équipe. Pour inviter un membre d'équipe, procédez comme suit : 

<ol>
<li>Cliquez sur l'icône **Compte et support** ![Icône Compte et support](../admin/images/account_support.svg) &gt;
**Compte** &gt; *nom_de_votre_compte* &gt; **Inviter des membres d'équipe**.</li>
<li>Sélectionnez l'organisation dans laquelle inviter les membres d'équipe. </li>
<li>Cliquez sur **Suivant**.</li>
<li>Sélectionnez les espaces auxquels vos membre d'équipe doivent pouvoir accéder. </li>
<li>Sélectionnez le rôle à affecter pour les espaces sélectionnés dans l'organisation. </li>
<li>Sélectionnez l'option permettant de confirmer que vous prenez en charge tous les frais liés au compte. </li>
<li>Entrez l'adresse électronique d'un membre d'équipe ou les adresses électroniques de plusieurs membres d'équipe :
<ul>
<li>Pour ajouter un seul membre d'équipe, entrez l'adresse électronique et cliquez sur **Envoyer**.</li>
<li>Pour ajouter plusieurs membres d'équipe, cliquez sur **Invitez toute le monde d'un coup**. Entrez les adresses électroniques dans
une liste en les séparant par une virgule, un espace ou un retour à la ligne. Ensuite, cliquez sur **Suivant** afin de vérifier les
adresses électroniques auxquelles envoyer les invitations, puis cliquez sur **Envoyer**.</li>
</ul>
</li>
</ol>

Cliquez sur **Afficher les éléments en attente** pour déterminer si les invitations sont en attente ou ont été acceptées. Vous
pouvez choisir de renvoyer le courrier électronique d'invitation ou d'annuler l'invitation pour une invitation en attente à tout moment.


## Edition des rôles 
{: #editinguserroles}

Les propriétaires de compte et les responsables de l'organisation peuvent éditer les rôles d'organisation et d'espace pour
les membres d'équipe existants dans la page **Répertoire d'équipe**.
 

1. Cliquez sur l'icône **Compte et support** ![Icône Compte et support](../admin/images/account_support.svg)
&gt; **Compte** &gt; *nom_de_votre_compte* &gt; **Répertoire d'équipe**. 
2. Localisez le membre d'équipe dont vous voulez éditer les rôles. 
3. Cliquez sur **Afficher les rôles**.
4. Sélectionnez ou désélectionner les rôles d'organisation afin de modifier l'accès du membre d'équipe aux organisations. 
5. Cliquez sur **Afficher les espaces** pour ajouter ou retirer des rôles d'espace. 
6. Sélectionnez ou désélectionner les rôles d'espace afin de modifier l'accès du membre d'équipe aux espaces. 
7. Cliquez sur **Fermer les espaces**.
8. Cliquez sur **Sauvegarder** au bas de la page. 

Un gestionnaire de l'espace peut éditer les rôles des membres d'équipe dans son espace dans la page **Gérer les organisations**. 

1. Cliquez sur l'icône **Compte et support** ![Icône Compte et support](../admin/images/account_support.svg)
&gt; **Compte** &gt; *nom_de_votre_compte* &gt; **Gérer les organisations**. 
2. Localisez l'organisation dans laquelle se trouve votre espace. 
3. Cliquez sur **Afficher les détails**.
4. Localisez votre espace et cliquez sur l'option d'**édition de l'espace**.
5. Sélectionnez l'onglet **Utilisateurs**. 
6. Sélectionnez ou désélectionnez l'option de rôle d'espace pour le rôle à ajouter ou retirer pour le membre d'équipe. 
7. Cliquez sur **Sauvegarder**.
