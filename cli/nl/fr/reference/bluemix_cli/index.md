{:shortdesc: .shortdesc}

# Commandes bx pour l'interaction avec {{site.data.keyword.Bluemix_notm}}
{: #bluemix_cli}

*Dernière mise à jour :* 5 janvier 2016

L'interface de ligne de commande {{site.data.keyword.Bluemix}} fournit un ensemble de commandes qui sont regroupées par espace de nom
pour que les utilisateurs puissent interagir avec {{site.data.keyword.Bluemix_notm}}. Certaines commandes de l'interface de ligne de commande
{{site.data.keyword.Bluemix_notm}}, appelées commandes bx, sont des encapsuleurs de commandes cf existantes, et d'autres sont uniques pour {{site.data.keyword.Bluemix_notm}}. Vous
trouverez ci-après la liste de toutes les commandes qui sont prises en charge par l'interface de ligne de commande
{{site.data.keyword.Bluemix_notm}}, ainsi que leurs noms, leurs options, leur syntaxe, les prérequis, leurs descriptions et des exemples.
{:shortdesc}
 
**Remarque :** la zone *Prérequis* répertorie les actions qui sont requises avant l'utilisation de la commande. Les
commandes pour lesquelles aucune action n'est requise indiquent **Aucun**. Sinon, les prérequis peuvent inclure une ou
plusieurs des actions suivantes :
<dl>
<dt>Noeud final</dt>
<dd>Un noeud final d'API doit être défini via <code>bluemix api</code> avant l'utilisation de la commande.</dd>
<dt>Connexion</dt>
<dd>La connexion avec la commande <code>bluemix login</code> est requise avant l'utilisation de cette commande.</dd>
<dt>Cible</dt>
<dd>La commande <code>bluemix target</code> doit être utilisée pour définir une organisation et un espace avant l'utilisation de cette commande.</dd>
</dl>

## bluemix help
Affichez l'aide générale pour les commandes intégrées de premier niveau et les espaces de nom pris en charge de
l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}, ou l'aide d'une commande intégrée ou d'un espace de nom spécifique.

```
bluemix help [COMMANDE|ESPACE DE NOM]
```

**Prérequis** : Aucun

**Options de commande** :

*COMMANDE*|*ESPACE DE NOM* (facultatif) : commande ou espace de nom pour laquelle ou lequel l'aide est affichée. Si la commande
ou l'espace de nom n'est pas spécifié, l'aide générale de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}} est affichée.

**Exemples** :

Affichez l'aide générale pour l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}} :

```
bluemix help
```

Affichez l'aide pour l'espace de nom `catalogue` :

```
bluemix help catalogue
```

```
bluemix catalog help
```

Affichez l'aide pour la commande `info` :

```
bluemix help info
```

Affichez l'aide pour la commande `templates` sous l'espace de nom `catalogue` :

```
bluemix catalogue help templates
```


## bluemix api
Définissez ou affichez le noeud final d'API {{site.data.keyword.Bluemix_notm}}. Cette commande encapsule la commande `cf api`.

```
bluemix api [NOEUD_FINAL_API][--unset]
```

**Prérequis** : Aucun

**Options de commande** :

*NOEUD_FINAL_API* (facultatif) : noeud final d'API ciblé, par exemple https://api.ng.bluemix.net.  Si
l'option *NOEUD_FINAL_API* et l'option `--unset` sont toutes les deux spécifiées, le noeud final d'API en cours est affiché.

`--unset` (facultatif) : retirez le paramètre de noeud final d'API.

**Exemples** :

Définissez le noeud final d'API api.ng.bluemix.net :

```
bluemix api api.ng.bluemix.net
```

Affichez le noeud final d'API en cours :

```
bluemix api
```

Annulez la définition du noeud final d'API :

```
bluemix api --unset
```


## bluemix login
Connectez l'utilisateur. Cette commande encapsule la commande `cf login`. Les options de commande sont les mêmes que pour `cf
login`.

```
bluemix login [OPTIONS...]
```

**Prérequis** : Noeud final

**Options de commande** : pour des informations sur les options prises en charge par la commande `login`, voir
les informations sur la syntaxe de la commande `cf login` pour les commandes cf de gestion des applications.


## bluemix logout
Déconnectez l'utilisateur. Cette commande encapsule la commande `cf logout`.

```
bluemix logout
```

**Prérequis** : Aucun


## bluemix target
Définissez ou affichez l'organisation ou l'espace cible. Cette commande encapsule la commande `cf target`.

```
bluemix target [-o NOM_ORG] [-s NOM_ESPACE]
```

**Prérequis** : Noeud final, Connexion

**Options de commande** :

-o *NOM_ORG* (facultatif) : nom de l'organisation à cibler.

-s *NOM_ESPACE* (facultatif) : nom de l'espace à cibler.

Si ni -o *NOM_ORG* ni -s *NOM_ESPACE* n'est spécifié, l'organisation et l'espace en cours sont affichés.

**Exemples** :

Définissez l'organisation en cours à `MonOrg` et l'espace à `MonEspace`:

```
bluemix target -o MonOrg -s MonEspace
```

Affichez l'organisation et l'espace en cours :

```
bluemix target
```


## bluemix info
Affichez les informations {{site.data.keyword.Bluemix_notm}} de base, notamment la région en cours, la version du contrôleur de cloud
et certains noeuds finaux utiles tels que les noeuds finaux pour la connexion et l'échange de jeton d'accès.

```
bluemix info
```

**Prérequis** : Noeud final





## bluemix regions
Affichez les informations pour toutes les régions dans {{site.data.keyword.Bluemix_notm}}.

```
bluemix regions
```

**Prérequis** : Noeud final


## bluemix region-set
Passez à la région spécifiée. Cette commande redirige automatiquement sur la même organisation et le même espace dans la nouvelle région, si possible. Autrement, l'utilisateur est invité à sélectionner une nouvelle organisation et un nouvel espace si l'utilisateur est déjà connecté. Le noeud final d'API est changé
en conséquence.

```
bluemix region-set NOM_REGION
```

**Prérequis** : Noeud final

**Options de commande** :

*NOM_REGION* (obligatoire) : nom de la région à laquelle vous voulez accéder. Vous pouvez utiliser la commande `bluemix
regions` pour afficher tous les noms de région.

**Exemples** :

Définissez la région en cours à `eu-gb`:

```
bluemix region-set eu-gb
```



## bluemix config
Ecrit les valeurs par défaut dans le fichier de configuration.

```
bluemix config --http-timeout DELAI_ATTENTE_EN_SECONDES | --trace (true|false|chemin/fichier) | --color (true|false) | --locale (ENVIRONNEMENT LOCAL|CLEAR)
```

**Prérequis** : Aucun

**Options de commande** :

--http-timeout *DELAI_ATTENTE_EN_SECONDES* : valeur du délai d'attente pour les demandes HTTP. La valeur par défaut est 60 secondes.

--trace true|false|*chemin/fichier* : tracer les demandes HTTP jusqu'au terminal ou au fichier spécifié.

--color true|false : activer ou désactiver la sortie couleur. La sortie couleur est activée par défaut.

--locale *ENVIRONNEMENT LOCAL* : définir un environnement local par défaut. Si ENVIRONNEMENT LOCAL correspond à *CLEAR*, l'environnement local précédent est supprimé.

Une seule de ces options peut être indiquée à la fois.

**Exemples** :

Définissez le délai d'attente des demandes HTTP à 30 secondes :

```
bluemix config --http-timeout 30
```

Activez la sortie de trace pour les demandes HTTP :

```
bluemix config --trace true
```

Tracez les demandes HTTP vers le fichier nommé */home/usera/my_trace* :

```
bluemix config --trace /home/usera/my_trace
```

Désactivez la sortie couleur :

```
bluemix config --color false
```

Définissez l'environnement local à zh_Hans :

```
bluemix config --locale zh_Hans
```

Effacez les paramètres d'environnement local :

```
bluemix config --locale CLEAR
```










## bluemix list
Répertoriez toutes les applications cf, les conteneurs, les groupes de conteneurs et les groupes de machines virtuelles dans l'espace en cours.

```
bluemix list [apps|containers|container-groups|vm-groups]
```

**Prérequis** :  Noeud final, Connexion, Cible

**Options de commande** :

apps (facultatif) : affichez uniquement les informations sur les applications.

containers (facultatif) : affichez uniquement les informations sur les conteneurs.

container-groups (facultatif) : affichez uniquement les informations sur les groupes de conteneurs.

vm-groups (facultatif) : affichez uniquement les informations sur les groupes de machines virtuelles.

Vous ne pouvez spécifier qu'une seule option `apps`, `containers`, `container-groups` ou `vm-groups` à la fois. Si vous ne spécifiez rien, toutes les
applications cf, tous les conteneurs, tous les groupes de conteneurs et tous les groupes de machines virtuelles sont répertoriés.

**Exemples** :

Répertoriez toutes les applications cf :

```
bluemix list apps
```

Répertoriez toutes les instances de conteneur :

```
bluemix list containers
```

Répertoriez toutes les applications, tous les conteneurs, tous les groupes de conteneurs et tous les groupes de machines virtuelles :

```
bluemix list
```


## bluemix scale
Réduisez ou augmentez le nombre d'instances, le quota de disque et la taille de mémoire spécifiés pour l'application cf ou le groupe de conteneurs.

**Remarque :** seul un nombre d'instances peut être indiqué pour la mise à l'échelle d'un groupe de conteneurs. Si aucune option n'est
spécifiée, cette commande répertorie le nombre d'instances en cours pour le groupe de conteneurs, ainsi que le quota de disque et la taille de mémoire pour
l'application cf.

```
bluemix scale NOM_APP_CF|NOM_GROUPE_CONTENEURS [-i NOMBRE_INSTANCES][-k DISK_QUOTA] [-m TAILLE_MEMOIRE]
```

**Prérequis** :  Noeud final, Connexion, Cible

**Options de commande** :

*NOM_APP_CF*|*NOM_GROUPE_CONTENEURS* (obligatoire) : nom de l'application cf ou du groupe de conteneurs à mettre à l'échelle.

-i *NOMBRE_INSTANCES*  (facultatif) : nouveau nombre d'instances pour l'application cf ou le groupe de conteneurs à mettre à l'échelle. Il s'agit de la seule option valide pour la mise à l'échelle d'un groupe de conteneurs.

-k *QUOTA_DISQUE* (facultatif) : nouveau quota de disque de l'application cf. Non valide pour la mise à l'échelle d'un groupe de conteneurs.

-m *TAILLE_MEMOIRE* (facultatif) : nouvelle taille de mémoire pour l'application cf. Non valide pour la mise à l'échelle d'un groupe de conteneurs.

**Exemples** :

Affichez le nombre d'instances actuel pour `mon-groupe-conteneurs` :

```
bluemix scale mon-groupe-conteneurs
```

Mettez à l'échelle `mon-groupe-conteneurs` à 2 instances :

```
bluemix scale mon-groupe-conteneurs -i 2
```

Mettez à l'échelle `mon-app-java` avec 3 instances, 8 Go de quota de disque et 1024 Mo de taille de mémoire :

```
bluemix scale mon-app-java -i 3 -k 8G -m 1024M
```


## bluemix curl
Exécutez une demande HTTP brute dans {{site.data.keyword.Bluemix_notm}}. *Content-Type* est défini avec *application/json* par défaut. Cette
commande envoie une demande au serveur de la console {{site.data.keyword.Bluemix_notm}} (par exemple https://console.ng.bluemix.net) au lieu de
l'envoyer au noeud final d'API cf (par exemple https://api.ng.bluemix.net).

```
bluemix curl CHEMIN [OPTIONS...]
```

**Prérequis** : Noeud final, Connexion

**Options de commande** :

*CHEMIN* (obligatoire) : chemin URL de la ressource. Exemple : /rest/v2/apps.

*OPTIONS* (facultatif) : les options prises en charge par la commande `bluemix
curl` sont les mêmes que pour la commande `cf curl`.

**Exemples** :

Procédez à l'extraction des informations pour tous les modèles de conteneur boilerplate :

```
bluemix curl /rest/templates
```


## bluemix iam orgs
Cette commande possède la même fonction et les mêmes options que la commande `cf orgs`, mais les régions dans lesquelles les organisations sont présentes s'affichent également.


## bluemix iam org
Cette commande possède la même fonction et les mêmes options que la commande `cf org`, mais les régions dans lesquelles l'organisation est présente s'affichent également.


## bluemix iam org-create
Cette commande possède la même fonction et les mêmes options que la commande `cf create-org`.





## bluemix iam org-replicate
Répliquez une organisation de la région en cours dans une autre région.

```
bluemix iam org-replicate NOM_ORG NOM_REGION
```

**Prérequis** : Noeud final, Connexion

**Options de commande** :

*NOM_ORG* (obligatoire) : nom de l'organisation existante à répliquer.

*NOM_REGION* (obligatoire) : nom de la région hébergeant l'organisation répliquée.

**Exemples** :

Répliquez l'organisation `OE_Runtimes_Scaling` dans la région `eu-gb` :

```
bluemix iam org-replicate OE_Runtimes_Scaling eu-gb
```














## bluemix iam org-rename
Cette commande possède la même fonction et les mêmes options que la commande `cf rename-org`.


## bluemix iam org-delete
Cette commande possède la même fonction et les mêmes options que la commande `cf delete-org`.


## bluemix iam spaces
Cette commande possède la même fonction et les mêmes options que la commande `cf spaces`.


## bluemix iam space
Cette commande possède la même fonction et les mêmes options que la commande `cf space`.


## bluemix iam space-create
Cette commande possède la même fonction et les mêmes options que la commande `cf create-space`.


## bluemix iam space-rename
Cette commande possède la même fonction et les mêmes options que la commande `cf rename-space`.


## bluemix iam space-delete
Cette commande possède la même fonction et les mêmes options que la commande `cf delete-space`.


## bluemix iam user-create
Cette commande possède la même fonction et les mêmes options que la commande `cf create-user`.


## bluemix iam user-delete
Cette commande possède la même fonction et les mêmes options que la commande `cf delete-user`.


## bluemix iam org-users
Cette commande possède la même fonction et les mêmes options que la commande `cf org-users`.


## bluemix iam org-role-set
Cette commande possède la même fonction et les mêmes options que la commande `cf set-org-role`.


## bluemix iam org-role-unset
Cette commande possède la même fonction et les mêmes options que la commande `cf unset-org-role`.


## bluemix iam space-users
Cette commande possède la même fonction et les mêmes options que la commande `cf space-users`.


## bluemix iam space-role-set
Cette commande possède la même fonction et les mêmes options que la commande `cf set-space-role`.


## bluemix iam space-role-unset
Cette commande possède la même fonction et les mêmes options que la commande `cf unset-space-role`.


## bluemix catalog templates
Affichez les modèles de conteneur boilerplate dans Bluemix.

```
bluemix catalog templates [-d]
```

**Prérequis** : Noeud final, Connexion

**Options de commande** :

-d (facultatif) : si l'option `-d` est spécifiée, la description de chaque modèle est également affichée. Sinon, seul l'ID et le nom des modèles sont affichés.


## bluemix catalog template-run
Créez une application cf reposant sur le modèle spécifié avec l'adresse URL et la description indiquées. Par défaut, la nouvelle application est
démarrée automatiquement.

```
bluemix catalog template-run ID_MODELE NOM_APP_CF [-u URL] [-d DESCRIPTION] [--no-start]
```

**Prérequis** : Noeud final, Connexion, Cible

**Options de commande** :

*ID_MODELE* (obligatoire) : modèle sur lequel doit s'appuyer l'application lorsqu'elle est créée. Utilisez `bluemix templates` pour voir tous les ID des modèles.

*NOM_APP_CF* (obligatoire) : nom de l'application cf à créer.

-u *URL* (facultatif) : route de l'application. Si elle n'est pas spécifiée, la route est définie par
{{site.data.keyword.Bluemix_notm}} automatiquement en fonction du nom de votre application et du domaine par défaut.

-d *DESCRIPTION* (facultatif) : description de l'application.

--no-start (facultatif) : permet de ne pas démarrer l'application automatiquement après sa création. Si cette option n'est pas spécifiée,
l'application est démarrée automatiquement après sa création.

**Exemples** :

Créez l'application cf `mon-app` d'après le modèle `javaHelloWorld` :

```
bluemix catalog template-run javaHelloWorld mon-app
```

Créez l'application `mon-app-ruby` d'après le modèle `rubyHelloWorld` avec la route `myrubyapp.ng.bluemix.net` et la description `Ma première application Ruby dans {{site.data.keyword.Bluemix_notm}}.` :

```
bluemix catalog template-run rubyHelloWorld mon-app-ruby -u myrubyapp.ng.bluemix.net -d "Ma première application Ruby dans {{site.data.keyword.Bluemix_notm}}."
```

Créez l'application `mon-app-python` d'après le modèle `pythonHelloWorld` sans démarrage automatique :

```
bluemix catalog template-run pythonHelloWorld mon-app-python --no-start
```




## bluemix catalog template-register

Enregistrez un nouveau modèle de conteneur boilerplate sur {{site.data.keyword.Bluemix_notm}}.

```
bluemix catalog template-register ID_MODELE URL_MODELE
```

**Prérequis** : Noeud final, Connexion

**Options de commande** :

*ID_MODELE* (obligatoire) : ID du nouveau modèle enregistré.

*URL_MODELE* (obligatoire) : URL d'hébergement des métadonnées du nouveau modèle.

**Exemples** :

Créez un modèle nommé `javaHelloWorld` :

```
bluemix catalog template-register javaHelloWorld http://javaHelloWorld.ng.bluemix.net/info
```

## bluemix catalog template-deregister

Annulez l'enregistrement d'un modèle de conteneur boilerplate existant.

```
bluemix catalog template-deregister ID_MODELE [-f]
```

**Prérequis** : Noeud final, Connexion

**Options de commande** :

*ID_MODELE* (obligatoire) : utilisez `bluemix catalog templates` pour afficher tous les ID des modèles.

-f  (facultatif) : forcer l'annulation d'enregistrement sans confirmation.

**Exemples** :

Annulez l'enregistrement du modèle `javaHelloWorld` sans confirmation :

```
bluemix catalog template-deregister javaHelloWorld -f
```


## bluemix catalog template-registry
Affichez le registre de modèles {{site.data.keyword.Bluemix_notm}}.

```
bluemix catalog template-registry
```

**Prérequis** : Noeud final









## bluemix catalog service-broker

Affichez les informations du courtier de services indiqué.

```
bluemix catalog service-broker NOM_COURTIER_SERVICES
```

**Prérequis** : Noeud final, Connexion

**Options de commande** :

*NOM_COURTIER_SERVICES* (obligatoire) : nom du courtier de services à consulter.


## bluemix catalog service-broker-create
{: #bluemix_catalog_service_broker_create}
Créez un courtier de services.

```
bluemix catalog service-broker-create TEXTE_JSON_COURTIER_SERVICES|FICHIER_JSON_COURTIER_SERVICES [--no-billing]
```

**Prérequis** : Noeud final, Connexion

**Options de commande** :

*TEXTE_JSON_COURTIER_SERVICES*|*FICHIER_JSON_COURTIER_SERVICES* (obligatoire) : code JSON décrivant le nouveau courtier de services à créer. Vous pouvez utiliser le nom du fichier JSON ou utiliser directement le texte JSON.

--no-billing (facultatif) : si cette option est spécifiée, la facturation du courtier de services est désactivée. 

**Exemples** :

Créez un courtier de services avec un fichier JSON :

```
bluemix catalog service-broker-create ./broker.json
```

Créez un nouveau courtier de services avec du texte JSON sans facturation :

```
bluemix catalog service-broker-create '{"name":"courtier_test", ...}' --no-billing
```

L'exemple suivant illustre un code JSON de courtier de services comportant tous les champs obligatoires :

```
{
    "name": "mon_courtier",  // nom du courtier de services
    "broker_url": "http://my_broker.ng.bluemix.net"  // URL qui pointe vers les métadonnées du courtier de services
    "auth_username": "nom d'utilisateur",
	"auth_password": "mot de passe",  // nom d'utilisateur et mot de passe nécessaires pour consulter l'URL du courtier de services. Le nom d'utilisateur et le mot de passe doivent être envoyés avec l'autorisation de base HTTP.
    "visibilities": [
        {"organization_name": "OE_Runtimes_Scaling"}
    ]
}
```


## bluemix catalog service-broker-update
Mise à jour d'un courtier de services existant.

```
bluemix catalog service-broker-update NOM_COURTIER_ORIGINE TEXTE_JSON_COURTIER_SERVICES|FICHIER_JSON_COURTIER_SERVICES
```

**Prérequis** : Noeud final, Connexion

**Options de commande** :

*NOM_COURTIER_ORIGINE* (obligatoire) : nom du courtier de services à mettre à jour.

*TEXTE_JSON_COURTIER_SERVICES*|*FICHIER_JSON_COURTIER_SERVICES* (obligatoire) : nouveau code JSON décrivant le courtier de services. Vous pouvez utiliser le nom du fichier JSON ou utiliser directement le texte JSON.

**Exemples** :

Mettez à jour le courtier de services `auto-scaling` existant :

```
bluemix catalog service-broker-update auto-scaling ./auto-scaling.json
```

Voir [bluemix catalog service-broker-create](#bluemix_catalog_service_broker_create) pour plus de détails sur le format JSON du courtier de services.


## bluemix catalog service-broker-delete

Supprimez le courtier de services indiqué.

```
bluemix catalog service-broker-delete NOM_COURTIER_SERVICES [-f]
```

**Prérequis** : Noeud final, Connexion

**Options de commande** :

*NOM_COURTIER_SERVICES* (obligatoire) : nom du courtier de services à supprimer.

-f  (facultatif) : forcer la suppression sans confirmation.

**Exemples** :

Supprimez le courtier de services `auto-scaling` sans confirmation :

```
bluemix catalog service-broker-delete auto-scaling -f
```














## bluemix network routes
Cette commande possède la même fonction et les mêmes options que la commande `cf routes`.


## bluemix network route-check
Cette commande possède la même fonction et les mêmes options que la commande `cf check-route`.


## bluemix network route-map
Mappez une route à une application cf ou un groupe de conteneurs existant associé au domaine et au nom d'hôte spécifiés.

```
bluemix network route-map NOM_APP_CF|NOM_GROUPE_CONTENEURS  DOMAINE  [-n NOM_HOTE]
```

**Prérequis** : Noeud final, Connexion, Cible

**Options de commande** :

*NOM_APP_CF*|*NOM_GROUPE_CONTENEURS* (obligatoire) : nom de l'application cf ou du groupe de conteneurs à mapper à une route.

*DOMAINE* (obligatoire) : domaine de la route. Exemple : mybluemix.net ou ng.bluemix.net. 

-n *NOM_HOTE* (facultatif) : nom d'hôte de la route. S'il n'est pas spécifié, le nom d'hôte est le nom de l'application ou le nom du
groupe de conteneurs par défaut.

**Exemples** :

Mappez une route à `mon-app` avec le domaine spécifié :

```
bluemix network route-map mon-app mybluemix.net
```

Mappez une route à 'mon-groupe-conteneurs' avec le domaine et le nom d'hôte spécifiés :

```
bluemix network route-map mon-groupe-conteneurs ng.bluemix.net -n abc
```


## bluemix network route-unmap
Supprimez le mappage de la route spécifiée à une application cf ou un groupe de conteneurs existant.

```
bluemix network route-unmap NOM_APP_CF|NOM_GROUPE_CONTENEURS  DOMAINE  [-n NOM_HOTE]
```

**Prérequis** : Noeud final, Connexion, Cible

**Options de commande** :

*NOM_APP_CF*|*NOM_GROUPE_CONTENEURS* (obligatoire) : nom de l'application cf ou du groupe de conteneurs.

*DOMAINE* (obligatoire) : domaine de la route (par exemple mybluemix.net ou ng.bluemix.net). 

-n *NOM_HOTE* (facultatif) : nom d'hôte de la route. S'il n'est pas spécifié, le nom d'hôte est le nom de l'application ou le nom du
groupe de conteneurs par défaut.

**Exemples** :

Supprimez le mappage de la route `mon-app.mybluemix.net` de `mon-app` :

```
bluemix network route-unmap mon-app mybluemix.net
```

Supprimez le mappage de la route `abc.ng.bluexmix.net` de `mon-groupe-conteneurs` :

```
bluemix network route-unmap mon-groupe-conteneurs ng.bluemix.net -n abc
```


## bluemix network route-create
Cette commande possède la même fonction et les mêmes options que la commande `cf create-route`.


## bluemix network route-delete
Cette commande possède la même fonction et les mêmes options que la commande `cf delete-route`.


## bluemix network orphaned-routes-delete
Cette commande possède la même fonction et les mêmes options que la commande `cf delete-orphaned-routes`.


## bluemix network domains
Cette commande possède la même fonction et les mêmes options que la commande `cf domains`.


## bluemix network domain-create
Cette commande possède la même fonction et les mêmes options que la commande `cf create-domain`.


## bluemix network domain-delete
Cette commande possède la même fonction et les mêmes options que la commande `cf delete-domain`.


## bluemix network shared-domain-create
Cette commande possède la même fonction et les mêmes options que la commande `cf create-shared-domain`.


## bluemix network shared-domain-delete
Cette commande possède la même fonction et les mêmes options que la commande `cf delete-shared-domain`.




## bluemix security cert

Affichez la liste des informations de certificat de l'hôte spécifié.

```
bluemix security cert NOM_HOTE
```

**Prérequis** : Noeud final, Connexion

**Options de commande** :

*NOM_HOTE* (obligatoire) : nom du serveur hébergeant le certificat.

**Exemples** :

Affichez le certificat de l'hôte `ibmcxo-eventconnect.com` :

```
bluemix security cert ibmcxo-eventconnect.com
```


## bluemix security cert-add

Ajoutez un certificat au domaine indiqué dans l'organisation en cours.

```
bluemix security cert-add DOMAINE -k FICHIER_CLE_PRIVEE -c FICHIER_CERT [-p MOT_DE_PASSE][-i INTERMEDIATE_CERT_FILE] [--verify-client]
```

**Prérequis** : Noeud final, Connexion, Cible

**Options de commande** :

*DOMAINE* (obligatoire) : domaine auquel est ajouté le certificat.

-k *FICHIER_CLE_PRIVEE* (obligatoire) : chemin d'accès au fichier de clé privée.

-c *FICHIER_CERT* (obligatoire) : chemin d'accès au fichier de certificat.

-p *MOT_DE_PASSE* (facultatif) : mot de passe du certificat.

-i *FICHIER_CERT_INTERMEDIAIRE* (facultatif) : chemin d'accès au fichier de certificat intermédiaire.

--verify-client (facultatif) : indique s'il faut activer la vérification du certificat client.

**Exemples** :

Ajoutez un certificat au domaine `ibmcxo-eventconnect.com` :

```
bluemix security cert-add ibmcxo-eventconnect.com -k key_file.key -c cert_file.crt -p 123 -i inter_cert.cert
```


## bluemix security cert-remove
Supprimez un certificat du domaine spécifié dans l'organisation en cours.

```
bluemix security cert-remove DOMAINE [-f]
```

**Prérequis** : Noeud final, Connexion, Cible

**Options de commande** :

*DOMAINE* (obligatoire) : domaine dont le certificat est à supprimer.

-f  (facultatif) : forcer la suppression sans confirmation.








## bluemix plugin repos
Répertoriez tous les référentiels de plug-in qui sont enregistrés dans l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}.

```
bluemix plugin repos
```

**Prérequis** : Aucun


## bluemix plugin repo-add
Ajoutez un nouveau référentiel de plug-in à l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}.

```
bluemix plugin repo-add NOM_REFERENTIEL URL_REFERENTIEL
```

**Prérequis** : Aucun

**Options de commande** :

*NOM_REFERENTIEL* (obligatoire) : nom du référentiel à ajouter. Vous pouvez définir votre propre nom pour chaque référentiel.

*URL_REFERENTIEL* (obligatoire) : adresse URL du référentiel à ajouter. Elle doit contenir le protocole (par exemple
http://plugins.ng.bluemix.net au lieu de plugins.ng.bluemix.net). http://plugins.ng.bluemix.net est le référentiel de plug-in officiel de l'interface de
ligne de commande {{site.data.keyword.Bluemix_notm}}.

**Exemples** :

Ajoutez le référentiel de plug-in officiel de l'interface de ligne de commande Bluemix sous la forme `référentiel-bluemix` :

```
bluemix plugin repo-add référentiel-bluemix http://plugins.ng.bluemix.net
```


## bluemix plugin repo-remove
Retirez un référentiel de plug-in de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}.

```
bluemix plugin repo-remove NOM_REFERENTIEL
```

**Prérequis** : Aucun

**Options de commande** :

*NOM_REFERENTIEL* (obligatoire) : nom du référentiel à retirer.

**Exemples** :

Supprimez `référentiel-bluemix` de l'interface de ligne de commande (CLI) {{site.data.keyword.Bluemix_notm}} :

```
bluemix plugin repo-remove référentiel-bluemix
```


## bluemix plugin repo-plugin-list
Répertoriez tous les plug-in disponibles dans tous les référentiels ajoutés ou dans un référentiel spécifique.

```
bluemix plugin repo-plugin-list [-r NOM_REFERENTIEL]
```

**Prérequis** : Aucun

**Options de commande** :

-r *NOM_REFERENTIEL* (facultatif) : répertoriez uniquement les plug-in dans le référentiel spécifié.

**Exemples** :

Répertoriez tous les plug-in dans tous les référentiels ajoutés :

```
bluemix plugin repo-plugin-list
```

Répertoriez tous les plug-in du référentiel `référentiel-bluemix` :

```
bluemix plugin repo-plugin-list -r référentiel-bluemix
```


## bluemix plugin list
Répertoriez tous les plug-in installés dans l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}.

```
bluemix plugin list
```

**Prérequis** : Aucun


## bluemix plugin install
Installez la version de plug-in spécifique dans l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}} à partir du chemin ou du référentiel spécifié.

```
bluemix plugin install CHEMIN_PLUG-IN|NOM_PLUG-IN [-r NOM_REFERENTIEL][-v VERSION]
```

**Prérequis** : Aucun

**Options de commande** :

*CHEMIN_PLUG-IN*|*NOM_PLUG-IN* (obligatoire) : si `-r *NOM_REFERENTIEL*` n'est pas indiqué, le plug-in est installé à partir de l'URL distante ou du chemin local indiqué.

-r *NOM_REFERENTIEL* (facultatif) : nom du référentiel dans lequel se trouve le fichier binaire du plug-in.
-v *VERSION*  (facultatif) : version de plug-in à installer. Si elle n'est pas fournie, la dernière version du plug-in est installée. Cette option n'est valide que si vous installez le plug-in à partir du référentiel.

**Exemples** :

Installez un plug-in depuis le fichier local :

```
bluemix plugin install /downloads/new_plugin
```

Installez un plug-in depuis l'adresse URL distante :

```
bluemix plugin install http://plugins.ng.bluemix.net/downloads/new_plugin
```

Installez la dernière version du plug-in `IBM-Containers` à partir du référentiel `référentiel-bluemix` :

```
bluemix plugin install IBM-Containers -r référentiel-bluemix
```
Installez le plug-in `IBM-Containers` avec la version `0.5.800` à partir du référentiel `référentiel-bluemix` :

```
bluemix plugin install IBM-Containers -r référentiel-bluemix -v 0.5.800
```






## bluemix plugin uninstall
Désinstallez le plug-in spécifié de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}.

```
bluemix plugin uninstall NOM_PLUG-IN
```

**Prérequis** : Aucun

**Options de commande** :

*NOM_PLUG-IN* (obligatoire) : nom du plug-in à désinstaller.

**Exemples** :

Désinstallez le plug-in `IBM-Containers` installé précédemment :

```
bluemix plugin uninstall IBM-Containers
```
