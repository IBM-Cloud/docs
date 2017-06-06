---

copyright:

  years: 2015, 2017
lastupdated: "2017-05-10"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Gestion des clés d'API
{: #manapikey}

Une clé d'interface de programmation (clé d'API) est un code transmis par des programmes informatiques qui appellent une interface de programmation (API) afin d'identifier le programme appelant, son développeur ou son utilisateur sur le site Web. Les clés d'API permettent de suivre et de contrôler l'utilisation de l'API, par exemple pour empêcher toute utilisation malveillante ou abusive de l'API (telle qu'elle peut être définie dans les conditions du service). Le clé d'API sert souvent d'identificateur unique et de jeton de valeur confidentielle pour l'authentification. En général, elle dispose d'un ensemble de droits d'accès à l'API qui lui est associée. Les clés d'API peuvent reposer sur le système d'identificateurs uniques universels (UUID) afin de garantir que chacune d'entre elles est unique pour chaque utilisateur. 

En tant qu'utilisateur {{site.data.keyword.Bluemix_notm}}, vous pouvez choisir d'utiliser une clé d'API lorsque vous activez un programme ou un script sans fournir votre mot de passe au script. L'utilisation d'une clé d'API présente l'avantage suivant : un utilisateur ou une organisation peut créer plusieurs clés d'API pour divers programmes et les clés d'API peuvent être supprimées indépendamment si elles sont compromises sans interférence avec d'autres clés d'API, ou l'utilisateur. De plus, en tant qu'[utilisateur fédéré](/docs/admin/adminpublic.html#federatedid), vous pouvez utiliser une clé d'API pour vous connecter. Pour plus d'informations sur l'utilisation d'une clé d'API pour la connexion, voir la documentation relative à la [commande `bluemix login` de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}](/docs/cli/reference/bluemix_cli/bx_cli.html#bluemix_login) et à la [commande `cf login` de l'interface de ligne de commande cf](/docs/cli/reference/cfcommands/index.html#cf_login).

Vous pouvez gérer vos clés d'API {{site.data.keyword.Bluemix_notm}} depuis la fenêtre Clés d'API Bluemix. Sélectionnez **Gérer** &gt; **Sécurité** &gt; **Clés d'API Bluemix** pour afficher la liste de vos clés avec des descriptions et des dates. Vous pouvez créer, éditer ou supprimer des clés d'API depuis cette page. 

Pour créer une clé d'API : 

1. Sélectionnez **Gérer** &gt; **Sécurité** &gt; **Clés d'API Bluemix**.
2. Cliquez sur **Créer une clé d'API**.
3. Entrez un nom et une description pour votre clé d'API. 
4. Cliquez sur **Créer une clé d'API**.
5. Ensuite, cliquez sur **Afficher** afin d'afficher la clé d'API pour la copier et la sauvegarder en vue d'une utilisation ultérieure, ou cliquez sur **Télécharger une clé d'API**.

**Remarque ** : la clé d'API ne peut être affichée ou téléchargée qu'au moment de sa création. Si la clé d'API est perdue, vous devez en créer une autre. 

Pour éditer une clé d'API : 

1. Sélectionnez **Gérer** &gt; **Sécurité** &gt; **Clés d'API Bluemix**.
2. Dans le menu **Actions** d'une clé d'API répertoriée dans la table, cliquez sur **Editer un nom & et une description**.  
3. Mettez à jour les informations relatives à votre clé d'API. 
4. Cliquez sur **Mettre à jour une clé d'API**.

Pour supprimer une clé d'API :  

1. Sélectionnez **Gérer** &gt; **Sécurité** &gt; **Clés d'API Bluemix**.
2. Dans le menu **Actions** d'une clé d'API répertoriée dans la table, cliquez sur **Supprimer**.
3. Ensuite, confirmez la suppression en cliquant sur **Supprimer la clé**.

Vous pouvez aussi utiliser l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}} pour gérer vos clés d'API en répertoriant vos clés, en créant des clés, ou mettant à jour des clés ou en supprimant des clés. Voir la section relative à la commande [`bluemix iam api-keys`](/docs/cli/reference/bluemix_cli/bx_cli.html#bluemix_iam) pour plus d'informations. 

