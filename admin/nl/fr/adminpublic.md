---

 

copyright:

  2015, 2016

 

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Administration
{: #administer}
*Dernière mise à jour : 29 février 2016*

Gérez vos organisations, vos espaces et les utilisateurs affectés en cliquant sur l'icône **Compte et support** ![Compte et support](../support/images/account_support.svg), puis sélectionnez **Gérer les organisations**. Si vous êtes utilisateur d'un environnement {{site.data.keyword.Bluemix_notm}} local ou d'un environnement
{{site.data.keyword.Bluemix_notm}} dédié, voir [Gestion de l'environnement {{site.data.keyword.Bluemix_notm}}
local et de l'environnement {{site.data.keyword.Bluemix_notm}} dédié](../admin/index.html#mng) pour plus d'informations sur l'administration de votre instance locale
ou dédiée.
{:shortdesc}

## Gestion de l'environnement {{site.data.keyword.Bluemix_notm}} public
{: #mngacct}

Dans {{site.data.keyword.Bluemix}} Public, vous pouvez gérer l'ensemble des organisations et des espaces, y compris l'accès utilisateur à partir du tableau de bord figurant dans l'interface utilisateur. Vous pouvez également surveiller votre utilisation et votre facturation.
{:shortdesc}

### Organisations et espaces
{: #orgsandspaces}

En tant que responsable de l'organisation ou propriétaire de compte, vous pouvez utiliser la page Gérer les organisations pour afficher et gérer les
paramètres de l'organisation ou de l'espace, notamment l'accès utilisateur. Pour ouvrir la page Gérer les organisations, cliquez sur l'icône **Compte et support** ![Compte et support](../support/images/account_support.svg), puis sélectionnez **Gérer les organisations**.

#### Organisations

Une organisation est définie par les éléments suivants :

<dl>
<dt>Les utilisateurs</dt>
<dd>Rôle disposant du droit de base dans les organisations et les espaces. Vous devez être affecté à une organisation pour pouvoir obtenir d'autres
droits dans les espaces de l'organisation. Pour des informations détaillées, voir
[Utilisateurs et rôles](adminpublic.html#userroles).</dd>
<dt>Les domaines</dt>
<dd>Indiquez la route Internet allouée à l'organisation. Une route possède un sous-domaine et un domaine. En général, le sous-domaine est le nom de l'application. Le
domaine peut être un domaine de système ou un domaine personnalisé que vous avez enregistré pour votre application.<br/>
<p>**Remarque** : si vous ajoutez un domaine personnalisé, vous devez configurer votre serveur DNS afin de résoudre votre domaine
personnalisé de sorte qu'il désigne le domaine de système {{site.data.keyword.Bluemix_notm}}. Ainsi, lorsque
{{site.data.keyword.Bluemix_notm}} reçoit une demande pour votre domaine personnalisé, il peut l'acheminer correctement vers votre
application.</p></dd>
<dt>Le quota</dt>
<dd>Représente les limites des ressources pour l'organisation, notamment le nombre de services et la quantité de mémoire pouvant être alloués à
l'organisation. Les quotas sont affectés lorsque les organisations sont
créées. Toute application ou tout service dans un espace de l'organisation contribue à l'utilisation du quota. Avec les plans Paiement à la carte ou
Abonnement, vous pouvez ajuster votre quota pour les applications et les conteneurs Cloud Foundry au fur et à mesure que les besoins de votre organisation
changent.</dd>
</dl>

Dans {{site.data.keyword.Bluemix_notm}}, vous pouvez utiliser des organisations afin de permettre la collaboration entre les utilisateurs et
de faciliter le regroupement logique des ressources de projet comme suit :

<ul>
<li>Vous pouvez regrouper un ensemble d'espaces, d'applications, de services, de domaines, de routes et d'utilisateurs dans des organisations.</li>
<li>Vous pouvez gérer l'accès aux espaces et aux organisations pour chaque utilisateur.</li>
</ul>

Lorsque vous créez une organisation, le nom de l'organisation doit être unique dans {{site.data.keyword.Bluemix_notm}}. Une fois que vous
avez créé
l'organisation, le droit *Responsable de l'organisation*, qui vous permet d'éditer le nom de l'organisation, de supprimer l'organisation et de
créer des espaces dans l'organisation vous est attribué automatiquement.

Lorsque vous supprimez une organisation, tous les espaces, toutes les applications et tous les services dans l'organisation sont supprimés.

{{site.data.keyword.Bluemix_notm}} permet la collaboration dans les projets en affectant des utilisateurs dans une organisation et dans les
espaces de l'organisation. Vous pouvez vous servir de l'onglet **Utilisateurs** pour afficher et gérer les utilisateurs de
l'organisation. Vous pouvez aussi inviter des utilisateurs dans votre organisation en cliquant sur le lien **Inviter un nouvel utilisateur** dans
l'onglet **Utilisateurs**. Les droits suivants peuvent être attribués aux utilisateurs d'une organisation :

<ul>
<li>Utilisateur de l'organisation</li>
<li>Responsable de l'organisation</li>
<li>Responsable de la facturation de l'organisation</li>
<li>Auditeur de l'organisation</li>
</ul>

#### Espaces

Dans une organisation, vous pouvez utiliser des espaces pour regrouper un ensemble d'applications, de services et d'utilisateurs.

Une fois que vous avez ajouté des utilisateurs à une organisation, vous pouvez leur attribuer des droits pour les espaces dans l'organisation. A
l'instar des organisations, les espaces possèdent également un ensemble de droits pouvant être attribués aux utilisateurs :

<ul>
<li>Responsable de l'espace</li>
<li>Développeur de l'espace</li>
<li>Auditeur de l'espace</li>
</ul>

**Remarque** : un utilisateur doit disposer d'au moins l'un des droits dans l'espace.

L'onglet **Domaines** d'un espace est une liste en lecture seule des domaines qui sont affectés à l'espace. Le domaine de système est
toujours disponible dans un espace, et des domaines personnalisés peuvent également être alloués à l'espace. Les applications qui ont été créées
dans l'espace peuvent utiliser n'importe quel domaine répertorié pour l'espace.

### Utilisateurs et rôles
{: #userroles}

Les propriétaires de compte effectuent toutes les opérations sur les organisations et les espaces.

####Types d'utilisateur

Vous pouvez être membre ou collaborateur d'un compte.

<dl>
<dt>Membre</dt>
<dd>Vous êtes membre d'un compte {{site.data.keyword.Bluemix_notm}} si vous avez créé le compte ou avez été invité sur le compte, et si vous vous
êtes inscrit depuis l'invitation afin d'utiliser {{site.data.keyword.Bluemix_notm}} pour la première fois. </dd>
<dt>Collaborateur</dt>
<dd>Vous êtes collaborateur d'un compte {{site.data.keyword.Bluemix_notm}} si vous avez déjà utilisé {{site.data.keyword.Bluemix_notm}}
avec un compte différent, puis avez été invité sur ce compte et avez accepté l'invitation.</dd>
</dl>

#### Rôles utilisateur

Les droits suivants peuvent être accordés aux utilisateurs pour qu'ils aient différents rôles utilisateur dans une organisation ou un espace :

<dl>
<dt>Responsables de l'organisation</dt>
<dd>Les responsables de l'organisation possèdent les droits suivants :
<ul>
<li>Créer ou supprimer des espaces dans l'organisation.</li>
<li>Inviter des utilisateurs dans l'organisation si le responsable de l'organisation est aussi membre de l'organisation ou propriété du compte.</li>
<li>Gérer des utilisateurs existants qui se trouvent déjà dans l'organisation.</li>
<li>Gérer les domaines de l'organisation.</li>
</ul>
<p>**Remarque** : si vous êtes collaborateur et avez déjà utilisé {{site.data.keyword.Bluemix_notm}} avec un compte différent,
vous ne pouvez pas inviter d'utilisateur dans l'organisation même si vous possédez le rôle de responsable de l'organisation. Vous devez être membre pour
pouvoir inviter des utilisateurs. Voir <a href="../troubleshoot/index.html#ts_adduser">Impossible d'ajouter des utilisateurs à une organisation</a>
pour des informations sur le contournement de ce problème.</p>
</dd>
<dt>Responsables de la facturation</dt>
<dd>Les responsables de la facturation possèdent des droits qui leur permettent d'afficher les informations sur l'utilisation des contextes d'exécution et
des services pour l'organisation.</dd>
<dt>Auditeurs de l'organisation</dt>
<dd>Les auditeurs de l'organisation possèdent des droits qui leur permettent d'afficher le contenu des applications et des services dans l'espace.</dd>
<dt>Responsables de l'espace</dt>
<dd>Les responsables de l'espace possèdent les droits suivants :
<ul>
<li>Il ajoutent des utilisateurs dans l'espace et gèrent les utilisateurs.</li>
<li>Activer des fonctions pour l'espace.</li>
</ul>
</dd>
<dt>Développeurs de l'espace</dt>
<dd>Les développeurs de l'espace possèdent les droits suivants :
<ul>
<li>Créer, supprimer et gérer des applications et des services dans l'espace.</li>
<li>Accéder aux journaux dans l'espace.</li>
</ul>
</dd>
<dt>Auditeurs de l'espace</dt>
<dd>Les auditeurs de l'espace possèdent des droits qui leur permettent d'accéder en lecture seule à toutes les informations sur l'espace, par exemple aux
informations sur les applications et les services, aux paramètres, aux rapports et aux journaux.</dd>
</dl>

**Remarque** : les utilisateurs qui possèdent le rôle de responsable ou de développeur peuvent accéder à la variable
d'environnement VCAP_SERVICES. Toutefois, un utilisateur affecté au rôle auditeur ne peut pas accéder à VCAP_SERVICES.

### Gestion de vos organisations
{: #orgmng}

En tant que responsable de l'organisation ou propriétaire de compte, vous pouvez gérer vos organisations. Les tâches de gestion incluent la création
d'une organisation, le changement de nom d'une organisation, la création d'un espace, l'invitation d'utilisateurs dans un espace, la modification des rôles utilisateur et la suppression d'une organisation existante.

#### Création d'une organisation

Seuls les utilisateurs qui possèdent un compte payant peuvent créer une organisation. Avec un compte payant, vous pouvez créer une organisation en
procédant comme suit :

<ol>
<li>Accédez au tableau de bord {{site.data.keyword.Bluemix_notm}}, cliquez sur l'icône **Compte et support** ![Compte et support](../support/images/account_support.svg), puis sélectionnez **Gérer les organisations**.</li>
<li>Cliquez sur **Créer une organisation** et suivez les invites pour créer votre organisation.</li>
</ol>

#### Changement de nom d'une organisation

Procédez comme suit pour renommer votre organisation :

<ol>
<li>Accédez au tableau de bord {{site.data.keyword.Bluemix_notm}}, cliquez sur l'icône **Compte et support** ![Compte et support](images/account_support.svg), et sélectionnez **Gérer les organisations**.</li>
<li>Sélectionnez l'organisation à renommer.</li>
<li>Entrez un nouveau nom dans la zone **Organisation** et cliquez sur **Sauvegarder**.</li>
</ol>

#### Liste des membres 

Procédez comme suit pour répertorier les membres de votre organisation ou de votre espace :

<ol>
<li>Accédez au tableau de bord {{site.data.keyword.Bluemix_notm}}, cliquez sur l'icône **Compte et support** ![Compte et support](../support/images/account_support.svg), puis sélectionnez **Gérer les organisations**. Vous pouvez afficher les membres de votre organisation et leurs rôles dans l'onglet
**Utilisateurs**.</li>
<li>Cliquez sur le nom de l'espace dans votre organisation pour afficher les membres de cet espace et leurs rôles.</li>
</ol>

#### Création d'un espace

Vous pouvez créer des espaces dans votre organisation, par exemple un espace *dev* comme environnement de développement, un espace
*test* comme environnement de test et un espace *production* comme environnement de production. Ensuite, vous pouvez associer vos
applications à des espaces. Procédez comme suit pour créer un espace :

<ol>
<li>Accédez au tableau de bord {{site.data.keyword.Bluemix_notm}}, cliquez sur l'icône **Compte et support** ![Compte et support](images/account_support.svg), puis sélectionnez **Gérer les organisations**.</li>
<li>Cliquez sur **Créer un espace** indiqué à la suite du nom de votre organisation et suivez les invites afin de créer votre espace.</li>
</ol>

#### Invitation d'utilisateurs dans un espace

Vous pouvez inviter des utilisateurs dans vos organisations et vos espaces en fonction de leur adresse électronique. Les utilisateurs ne peuvent accéder qu'à l'espace auquel ils ont été ajoutés. 

Selon que l'invité possède un ID IBM ou non, il se voit attribuer un rôle de `membre` ou
de `collaborateur` pour le compte. Le tableau ci-dessous explique en détail l'affectation des rôles de compte en
fonction du type d'invitation.

*Tableau 1. Affectations de rôle de compte*

| **Type d'adresse électronique invitée** | **Rôle de compte affecté** | 
|----------------|------------------|
|L'utilisateur possède un ID IBM dont le compte est lié à l'adresse électronique invitée  | Membre  | 
|L'utilisateur ne possède pas d'ID IBM | Un ID IBM correspondant à l'adresse électronique soumise est créé et l'utilisateur est ajouté en tant que membre. | 
|Adresse électronique pour un utilisateur {{site.data.keyword.Bluemix_notm}} en cours | Collaborateur | 

Procédez comme suit pour ajouter des utilisateurs avec des rôles affectés à des espaces spécifiques pour l'organisation de votre choix :

<ol>
<li>Accédez à **Compte et support** &gt; **Compte** &gt; **Gérer les organisations**.</li>
<li>Sélectionnez **Inviter des utilisateurs**.</li>
<li>Entrez l'adresse électronique de la personne à inviter.</li>
<li>Sélectionnez le rôle pour l'organisation dans laquelle vous prévoyez d'inviter le nouvel utilisateur.</li>
<li>Sélectionnez le rôle pour l'espace dans lequel vous prévoyez d'inviter le nouvelle utilisateur.</li>
<li>Cliquez sur **Inviter**.</li>
<li>Affichez la confirmation de l'envoi de l'invitation dans la section **En attente**. Cliquez sur **Renvoyer le courrier électronique** ou **Annuler l'invitation** pour prendre une
décision
concernant une invitation en attente.</li>
</ol>

#### Modifications de rôles utilisateur

Procédez comme suit pour modifier les rôles utilisateur :

<ol>
<li>Dans l'interface utilisateur {{site.data.keyword.Bluemix_notm}}, cliquez sur l'icône **Compte et support** ![Compte et support](images/account_support.svg), puis sélectionnez **Gérer les organisations**.</li>
<li>Sélectionnez la case à cocher **RESPONSABLE**, **RESPONSABLE DE LA FACTURATION** ou **AUDITEUR** dans l'onglet **UTILISATEURS** pour changer les rôles des utilisateurs dans votre organisation. Vous pouvez également sélectionnez un espace dans le panneau de navigation, puis sélectionnez la case à cocher **RESPONSABLE**, **DEVELOPPEUR** ou **AUDITEUR** dans l'onglet **UTILISATEURS** pour changer les rôles des utilisateurs dans cet espace. </li>
<li>Cliquez sur **SAUVEGARDER**.</li>
</ol>

#### Suppression d'une organisation existante

Prenez contact avec le support en charge des ID et de l'enregistrement {{site.data.keyword.Bluemix_notm}} pour qu'il supprime votre
organisation.

**Remarque** : les opérations de suppression sont irréversibles. Vous perdez toutes vos applications et tous les services qui sont
associés à l'organisation.

