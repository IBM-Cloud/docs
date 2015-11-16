{:shortdesc: .shortdesc}

# Commandes Bluemix
{: #bluemix_cli}

*Dernière mise à jour :* 19 octobre 2015

L'interface de ligne de commande (CLI) Bluemix fournit un ensemble de commandes regroupées par espace-noms pour permettre aux utilisateurs d'interagir avec Bluemix. Certaines commandes CLI Bluemix sont des encapsuleurs de commandes cf existantes et d'autres sont propres à Bluemix. Les informations ci-après répertorient toutes les commandes prises en charge par l'interface CLI de Bluemix et incluent leurs noms, options, syntaxe, prérequis, descriptions, ainsi que des exemples.
{:shortdesc}
 
**Remarque :** *Prérequis* recense les actions requises avant d'utiliser la commande. Les commandes sans actions prérequises indiquent **Aucun**. Dans les autres cas, les prérequis peuvent inclure une ou plusieurs des actions suivantes :
<dl>
<dt>**Noeud final**</dt>
<dd>Un noeud final d'API doit être défini via la commande `bluemix api` avant d'utiliser cette commande.</dd>
<dt>**Connexion**</dt>
<dd>Une connexion à l'aide de la commande `bluemix login` est requise avant d'utiliser cette commande.</dd>
<dt>**Cible**</dt>
<dd>La commande `bluemix target` doit être utilisée pour définir une organisation et un espace avant d'utiliser cette commande.</dd>
</dl>

## bluemix help
Affiche l'aide générale pour les commandes intégrées de premier niveau et les espaces-noms pris en charge par l'interface CLI de Bluemix, ou l'aide sur une commande intégrée ou un espace-nom spécifique.

```
bluemix help [COMMANDE|ESPACE-NOMS]
```

**Prérequis** : aucun

**Options de la commande**:

*COMMANDE*|*ESPACE-NOMS*  (facultatif) : commande ou espace-noms pour lesquels l'aide est affichée. Si cette option n'est pas spécifiée, l'aide générale de l'interface CLI Bluemix est affichée.

**Exemples**:

Affichage de l'aide générale de l'interface CLI Bluemix :

```
bluemix help
```

Affichage de l'aide pour l'espace-noms `catalog` :

```
bluemix help catalog
```

```
bluemix catalog help
```

Affichage de l'aide pour la commande `info` :

```
bluemix help info
```

Affichage de l'aide pour la commande `templates` sous l'espace-noms `catalog` :

```
bluemix catalog help templates
```


## bluemix api
Définit ou affiche le noeud final d'API. Cette commande encapsule la commande `cf api`.

```
bluemix api [NOEUD_FINAL_API][--unset]
```

**Prérequis** : aucun

**Options de la commande**:

*NOEUD_FINAL_API*  (facultatif) : noeud final d'API ciblé, par exemple : https://api.ng.bluemix.net. Si ni l'option *NOEUD_FINAL_API*, ni l'option `–unset`, ne sont spécifiées, le noeud final d'API actuel est affiché.

`--unset` (facultatif) : annule le noeud final d'API.

**Exemples**:

Définition du noeud final d'API à api.ng.bluemix.net :

```
bluemix api api.ng.bluemix.net
```

Affichage du noeud final d'API actuel :

```
bluemix api
```

Annulation du noeud final d'API :

```
bluemix api --unset
```


## bluemix login
Connecte l'utilisateur. Cette commande encapsule la commande `cf login`.Les options de la commande sont les mêmes que pour la commande `cf login`.

```
bluemix login [OPTIONS...]
```

**Prérequis** : noeud final

**Options de la commande** :
Pour plus d'informations sur les options prises en charge par la commande `login`, voir `cf login`, informations de syntaxe des commandes cf pour gestion des applications.


## bluemix logout
Déconnecte l'utilisateur. Cette commande encapsule la commande `cf logout`.

```
bluemix logout
```

**Prérequis** : aucun


## bluemix target
Définit ou affiche l'organisation ou l'espace cible. Cette commande encapsule la commande `cf target`.

```
bluemix target [-o NOM_ORG] [-s NOM_ESPACE]
```

**Prérequis** : noeud final, connexion

**Options de la commande**:

-o *NOM_ORG* (facultatif) : nom de l'organisation à cibler.

-s *NOM_ESPACE* (facultatif) : nom de l'espace à cibler. 

Si ni -o *NOM_ORG* ni -s *NOM_ESPACE* ne sont spécifiés, l'organisation et l'espace actuels sont affichés.

**Exemples**:

Définition de l'organisation actuelle à to 'MyOrg' et de l'espace à 'MySpace':

```
bluemix target -o MyOrg -s MySpace
```

Affichage de l'organisation et de l'espace actuels :

```
bluemix target
```


## bluemix info
Affiche les informations Bluemix de base, notamment la région actuelle, la version de contrôleur de cloud et divers noeuds finaux utiles, comme ceux pour connexion et échange de jeton d'accès.

```
bluemix info
```

**Prérequis** : noeud final


## bluemix list
Répertorie toutes les applications, les conteneurs, les groupes de conteneurs et les groupes de machines virtuelles dans l'espace actuel.

```
bluemix list [apps|containers|container-groups|vm-groups]
```

**Prérequis** : noeud final, connexion, cible

**Options de la commande**:

apps (facultatif) : affiche uniquement les informations sur les applications.

containers (facultatif) : affiche uniquement les informations sur les conteneurs.

container-groups (facultatif) : affiche uniquement les informations sur les groupes de conteneurs.

vm-groups (facultatif) : affiche uniquement les informations sur les groupes de machines virtuelles.

Une seule option peut être spécifiée à la fois parmi `apps`, `containers`, `container-groups` ou `vm-groups`. Si aucune d'elles n'est spécifiée, toutes les applications cf, tous les conteneurs, groupes de conteneurs et groupes de machines virtuelles sont répertoriés.

**Exemples**:

Recensement de toutes les applications cf :

```
bluemix list apps
```

Recensement de toutes les instances de conteneurs :

```
bluemix list containers
```

Recensement de toutes les apps, tous les conteneurs, groupes de conteneurs et groupes de machines virtuelles :

```
bluemix list
```


## bluemix scale
Mise à l'échelle de l'application cf ou du groupe de conteneurs d'après le nombre d'instances, le quota de disque et la taille de mémoire spécifiés. 

*Remarque :** seul un nombre d'instances peut être spécifié pour la mise à l'échelle d'un groupe de conteneurs. Si aucune option n'est spécifiée, cette commande renvoie le nombre d'instances actuel pour le groupe de conteneurs, ainsi que le quota de disque et la taille de mémoire pour l'application cf.

```
bluemix scale NOM_APP_CF|NOM_GROUPE_CONTENEURS [-i NOMBRE_INSTANCES] -k QUOTA_DISQUE] [-m TAILLE_MEMOIRE]
```

**Prérequis** : noeud final, connexion, cible

**Options de la commande**:

*NOM_APP_CF*|*NOM_GROUPE_CONTENEURS*  (requis) : nom de l'application cf ou du groupe de conteneurs à mettre à l'échelle.

-i *NOMBRE_INSTANCES* (facultatif) : nouveau nombre d'instances pour l'application cf ou le groupe de conteneurs à mettre à l'échelle. Cette option est la seule valide pour le groupe de conteneurs à mettre à l'échelle.

-k *QUOTA_DISQUE* (facultatif) : nouveau quota de disque de l'application cf. Option non valide pour mise à l'échelle d'un groupe de conteneurs.

-m *TAILLE_MEMOIRE* (facultatif) : nouvelle taille de la mémoire pour l'application cf. Option non valide pour mise à l'échelle d'un groupe de conteneurs.

**Exemples**:

Affichage du nombre d'instances actuel pour 'my-container-group':

```
bluemix scale my-container-group
```

Dimensionnement de 'my-container-group' à 2 instances :

```
bluemix scale my-container-group -i 2
```

Dimensionnement de 'my-java-app' à 3 instances, avec 8 Go de quota disque et taille de mémoire de 1024 Mo :

```
bluemix scale my-java-app -i 3 -k 8G -m 1024M
```


## bluemix curl
Exécute une demande HTTP brute sur Bluemix. "Content-Type" est défini par défaut à "application/json". Cette commande envoie une demande au serveur de console Bluemix (par exemple, https://console.ng.bluemix.net) au lieu de l'envoyer au noeud final d'API cf (par exemple, https://api.ng.bluemix.net).

```
bluemix curl PATH [OPTIONS...]
```

**Prérequis** : noeud final, connexion

**Options de la commande**:

*PATH* (requis) : chemin d'URL de la ressource. Par exemple, /rest/v2/apps.

*OPTIONS* (facultatif) : les options prises en charge pour la commande `bluemix curl` sont les mêmes que celles pour la commande `cf curl`.

**Exemples**:

Extraction des informations sur tous les modèles de conteneur boilerplate :

```
bluemix curl /rest/templates
```


## bluemix iam orgs
Cette commande remplit la même fonction et accepte les mêmes options que la commande `cf orgs`.


## bluemix iam org
Cette commande remplit la même fonction et accepte les mêmes options que la commande `cf org`.


## bluemix iam org-create
Cette commande remplit la même fonction et accepte les mêmes options que la commande `cf create-org`.


## bluemix iam org-rename
Cette commande remplit la même fonction et accepte les mêmes options que la commande `cf rename-org`.


## bluemix iam org-delete
Cette commande remplit la même fonction et accepte les mêmes options que la commande `cf delete-org`.


## bluemix iam spaces
Cette commande remplit la même fonction et accepte les mêmes options que la commande `cf spaces`.


## bluemix iam space
Cette commande remplit la même fonction et accepte les mêmes options que la commande `cf space`.


## bluemix iam space-create
Cette commande remplit la même fonction et accepte les mêmes options que la commande `cf create-space`.


## bluemix iam space-rename
Cette commande remplit la même fonction et accepte les mêmes options que la commande `cf rename-space`.


## bluemix iam space-delete
Cette commande remplit la même fonction et accepte les mêmes options que la commande `cf delete-space`.


## bluemix iam user-create
Cette commande remplit la même fonction et accepte les mêmes options que la commande `cf create-user`.


## bluemix iam user-delete
Cette commande remplit la même fonction et accepte les mêmes options que la commande `cf delete-user`.


## bluemix iam org-users
Cette commande remplit la même fonction et accepte les mêmes options que la commande `cf org-users`.


## bluemix iam org-role-set
Cette commande remplit la même fonction et accepte les mêmes options que la commande `cf set-org-role`.


## bluemix iam org-role-unset
Cette commande remplit la même fonction et accepte les mêmes options que la commande `cf unset-org-role`.


## bluemix iam space-users
Cette commande remplit la même fonction et accepte les mêmes options que la commande `cf space-users`.


## bluemix iam space-role-set
Cette commande remplit la même fonction et accepte les mêmes options que la commande `cf set-space-role`.


## bluemix iam space-role-unset
Cette commande remplit la même fonction et accepte les mêmes options que la commande `cf unset-space-role`.


## bluemix catalog templates
Affiche les modèles de conteneur boilerplate sur Bluemix.

```
bluemix catalog templates [-d]
```

**Prérequis** : noeud final, connexion

**Options de la commande**:

-d (facultatif) : si l'option '-d' est spécifiée, la description de chaque modèle est également affichée. Sinon, seuls l'ID et le nom de chaque modèle sont indiqués.


## bluemix catalog template-run
Crée une application cf basée sur le modèle indiqué avec l'URL et la description spécifiées. Par défaut, la nouvelle application est lancée automatiquement.

```
bluemix catalog template-run ID_MODELE NOM_APP_CF [-u URL] [-d DESCRIPTION] [--no-start]
```

**Prérequis** : noeud final, connexion, cible

**Options de la commande**:

*ID_MODELE* (requis) : modèle sur lequel l'application sera basée lors de sa création. Utilisez 'bluemix templates' pour afficher tous les ID de modèles.

*NOM_APP_CF* (requis) : nom de l'application cf à créer.

-u *URL* (facultatif) : route de l'application. Si elle n'est pas spécifiée, la route est définie automatiquement par Bluemix d'après le nom de votre application et le domaine par défaut.

-d *DESCRIPTION* (facultatif) : description de l'application.

--no-start (facultatif) : indique de ne pas lancer automatiquement l'application après sa création. Si cette option n'est pas spécifiée, l'application est lancée automatiquement après sa création.

**Exemples**:

Création d'une application cf nommée 'my-app' basée sur le modèle 'javaHelloWorld' :

```
bluemix catalog template-run javaHelloWorld my-app
```

Création d'une application nommée 'my-ruby-app' basée sur le modèle 'rubyHelloWorld' avec comme route 'myrubyapp.ng.bluemix.net' et comme description 'Ma première application Ruby sur Bluemix.':

```
bluemix catalog template-run rubyHelloWorld my-ruby-app -u myrubyapp.ng.bluemix.net -d "Ma première application Ruby sur Bluemix."
```

Création d'une application nommée 'my-python-app' basée sur le modèle 'pythonHelloWorld' et sans démarrage automatique :

```
bluemix catalog template-run pythonHelloWorld my-python-app --no-start
```


## bluemix network regions
Affiche les informations de toutes les régions sur Bluemix.

```
bluemix network regions
```

**Prérequis** : noeud final


## bluemix network region-set
Bascule sur la région spécifiée. Cette commande cible automatiquement la même organisation et le même espace dans la nouvelle région (si ceci est possible), ou invite l'utilisateur à sélectionner une nouvelle organisation et un nouvel espace si l'utilisateur est déjà connecté. Le noeud final d'API est modifié en conséquence.

```
bluemix network region-set NOM_REGION
```

**Prérequis** : noeud final

**Options de la commande**:

*NOM_REGION* (requis) : nom de la région sur laquelle vous désirez basculer. Vous pouvez utiliser la commande `bluemix regions` pour afficher tous les noms de régions.

**Exemples**:

Définition de la région actuelle à 'eu-gb' :

```
bluemix network region-set eu-gb
```


## bluemix network routes
Cette commande remplit la même fonction et accepte les mêmes options que la commande `cf routes`.


## bluemix network route-check
Cette commande remplit la même fonction et accepte les mêmes options que la commande `cf check-route`.


## bluemix network route-map
Mappe une route à une application cf existante ou à un groupe de conteneurs avec le domaine et le nom d'hôte spécifiés.

```
bluemix network route-map NOM_APP_CF|NOM_GROUPE_CONTENEURS DOMAINE [-n NOM_HOTE]
```

**Prérequis** : noeud final, connexion, cible

**Options de la commande** :

*NOM_APP_CF*|*NOM_GROUPE_CONTENEURS* (requis) : nom de l'application cf ou du groupe de conteneurs à mapper à une route.

*DOMAINE* (requis) : domaine de la route. Par exemple, mybluemix.net ou ng.bluemix.net. 

-n *NOM_HOTE* (facultatif) : nom d'hôte de la route. S'il n'est pas indiqué, le nom d'hôte est défini sur le nom d'application ou le nom du groupe de conteneurs par défaut.

**Exemples**:

Mappage d'une route à 'my-app' avec le domaine spécifié :

```
bluemix network route-map my-app mybluemix.net
```

Mappage d'une route à 'my-container-group' avec le domaine et le nom d'hôte spécifiés :

```
bluemix network route-map my-container-group ng.bluemix.net -n abc
```


## bluemix network route-unmap
Annule le mappage à la route spécifiée d'une application cf existante ou d'un groupe de conteneurs.

```
bluemix network route-unmap NOM_APP_CF|NOM_GROUPE_CONTENEURS DOMAINE [-n NOM_HOTE]
```

**Prérequis** : noeud final, connexion, cible

**Options de la commande** :

*NOM_APP_CF*|*NOM_GROUPE_CONTENEURS* (requis) : nom de l'application cf ou du groupe de conteneurs.

*DOMAINE* (requis) : domaine de la route (par exemple, mybluemix.net ou ng.bluemix.net). 

-n *NOM_HOTE* (facultatif) : nom d'hôte de la route. S'il n'est pas indiqué, le nom d'hôte est défini sur le nom d'application ou le nom du groupe de conteneurs par défaut.

**Exemples**:

Unmap 'my-app.mybluemix.net' from 'my-app':

```
bluemix network route-unmap my-app mybluemix.net
```

Unmap 'abc.ng.bluexmix.net' from 'my-container-group':

```
bluemix network route-unmap my-container-group ng.bluemix.net -n abc
```


## bluemix network route-create
Cette commande remplit la même fonction et accepte les mêmes options que la commande `cf create-route`.


## bluemix network route-delete
Cette commande remplit la même fonction et accepte les mêmes options que la commande `cf delete-route`.


## bluemix network orphaned-routes-delete
Cette commande remplit la même fonction et accepte les mêmes options que la commande `cf delete-orphaned-routes`.


## bluemix network domains
Cette commande remplit la même fonction et accepte les mêmes options que la commande `cf domains`.


## bluemix network domain-create
Cette commande remplit la même fonction et accepte les mêmes options que la commande `cf create-domain`.


## bluemix network domain-delete
Cette commande remplit la même fonction et accepte les mêmes options que la commande `cf delete-domain`.


## bluemix network shared-domain-create
Cette commande remplit la même fonction et accepte les mêmes options que la commande `cf create-shared-domain`.


## bluemix network shared-domain-delete
Cette commande remplit la même fonction et accepte les mêmes options que la commande `cf delete-shared-domain`.


## bluemix plugin repos
Répertorie tous les référentiels de plug-in enregistrés dans l'interface de ligne de commande (CLI) Bluemix.

```
bluemix plugin repos
```

**Prérequis** : aucun


## bluemix plugin repo-add
Ajoute un nouveau référentiel de plug-in à l'interface de ligne de commande (CLI) Bluemix.

```
bluemix plugin repo-add NOM_REFERENTIEL URL_REFERENTIEL
```

**Prérequis** : aucun

**Options de la commande**:

*NOM_REFERENTIEL* (requis) : nom du référentiel à ajouter. Vous pouvez définir votre propre nom pour chaque référentiel.

*URL_REFERENTIEL* (requis) : URL du référentiel à ajouter. L'URL du référentiel doit inclure le protocole (par exemple, http://plugins.ng.bluemix.net au lieu de plugins.ng.bluemix.net). http://plugins.ng.bluemix.net est le référentiel de plug-in officiel de l'interface de ligne de commande (CLI) Bluemix.

**Exemples**:

Ajout du référentiel de plug-in officiel de l'interface de ligne de commande (CLI) Bluemix sous le nom 'bluemix-repo' :

```
bluemix plugin repo-add bluemix-repo http://plugins.ng.bluemix.net
```


## bluemix plugin repo-remove
Supprime un référentiel de plug-in de l'interface de ligne de commande (CLI) Bluemix.

```
bluemix plugin repo-remove NOM_REFERENTIEL
```

**Prérequis** : aucun

**Options de la commande**:

*NOM_REFERENTIEL* (requis) : nom du référentiel à supprimer. 

**Exemples**:

Suppression du référentiel 'bluemix-repo' de l'interface de ligne de commande (CLI) Bluemix :

```
bluemix plugin repo-remove bluemix-repo
```


## bluemix plugin repo-plugin-list
Liste tous les plug-ins disponibles dans tous les référentiels ajoutés ou dans un référentiel spécifique.

```
bluemix plugin repo-plugin-list [-r NOM_REFERENTIEL]
```

**Prérequis** : aucun

**Options de la commande**:

-r *NOM_REFERENTIEL* (facultatif) : ne liste que les plug-ins présents dans le référentiel spécifié.

**Exemples**:

Affichage de tous les plug-ins dans tous les référentiels ajoutés :

```
bluemix plugin repo-plugin-list
```

Affichage de tous les plug-ins dans le référentiel 'bluemix-repo' :

```
bluemix plugin repo-plugin-list -r bluemix-repo
```


## bluemix plugin list
Liste tous les plug-ins installés dans l'interface de ligne de commande (CLI) Bluemix.

```
bluemix plugin list
```

**Prérequis** : aucun


## bluemix plugin install
Installe dans l'interface de ligne de commande (CLI) Bluemix le plug-in depuis le chemin ou le référentiel spécifié.

```
bluemix plugin install CHEMIN_PLUG-IN|NOM PLUG-IN [-r NOM_REFERENTIEL]
```

**Prérequis** : aucun

**Options de la commande** :

*CHEMIN_PLUG-IN*|*NOM_PLUG-IN* (requis) : si '-r *NOM_REFERENTIEL*' n'est pas spécifié, le plug-in est installé depuis le chemin local spécifié ou l'URL distante.

-r *NOM_REFERENTIEL* (facultatif) : nom du référentiel où le plug-in binaire est situé.

**Exemples**:

Installation d'un plug-in depuis le fichier local :

```
bluemix plugin install /downloads/new_plugin
```

Installation d'un plug-in depuis l'URL distante :

```
bluemix plugin install http://plugins.ng.bluemix.net/downloads/new_plugin
```

Installation du plug-in BM-Containers' depuis le référentiel 'bluemix-repo' :

```
bluemix plugin install IBM-Containers -r bluemix-repo
```


## bluemix plugin uninstall
Désinstallation du plug-in spécifié de l'interface de ligne de commande (CLI) Bluemix.

```
bluemix plugin uninstall NOM_PLUG-IN
```

**Prérequis** : aucun

**Options de la commande**:

*NOM_PLUG-IN* (requis) : nom du plug-in à désinstaller.

**Exemples**:

Désinstallation du plug-in BM-Containers' installé auparavant :

```
bluemix plugin uninstall IBM-Containers
```
