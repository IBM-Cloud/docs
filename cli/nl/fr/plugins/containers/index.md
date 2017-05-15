---



copyright:

  years: 2015, 2017

lastupdated: "2017-01-12"


---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Interface de ligne de commande IBM Containers
{: #containercli}

*Version :* 1.0.0

L'interface de ligne de commande d'IBM Containers  est un plug-in
d'interface de ligne de commande {{site.data.keyword.Bluemix_notm}} qui
permet de gérer les conteneurs et les groupes de conteneurs sur Bluemix.
{: shortdesc}

**Remarque :** la zone *Prérequis* répertorie les actions qui sont requises avant l'utilisation de la commande. Les commandes pour lesquelles aucune action n'est requise indiquent **Aucun**. Sinon, les prérequis peuvent inclure une ou plusieurs des actions suivantes :
<dl>
<dt>Noeud final</dt>
<dd>Un noeud final d'API doit être défini via <code>bluemix api</code> avant l'utilisation de la commande.</dd>
<dt>Connexion</dt>
<dd>La connexion avec la commande <code>bluemix login</code> est requise avant l'utilisation de cette commande. Si vous vous connectez à l'aide d'un ID fédéré, utilisez l'option '--sso' pour vous authentifier avec un code d'accès unique.</dd>
<dt>Cible</dt>
<dd>La commande <code>bluemix target</code> doit être utilisée pour définir une organisation et un espace avant l'utilisation de cette commande.</dd>
<dt>Docker</dt>
<dd>L'interface de ligne de commande Docker (docker) est requise pour
l'exécution des commandes dans le plug-in d'interface de ligne de commande
d'IBM Containers.</dd>
</dl>

<table summary="Commandes Bluemix que vous pouvez utiliser pour gérer des conteneurs dans Bluemix.">
<caption>Tableau 1. Commandes pour la gestion de conteneurs dans Bluemix</caption>
 <thead>
 <th colspan="5">Commandes pour la gestion de conteneurs dans Bluemix</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix ic attach](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_attach)</td>
 <td>[bluemix ic build](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_build)</td>
 <td>[bluemix ic cp](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_cp)</td>
 <td>[bluemix ic cpi](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_cpi)</td>
 <td>[bluemix ic exec](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_exec)</td>
 </tr>
 <tr>
 <td>[bluemix ic group-create](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_group_create)</td>
 <td>[bluemix ic group-inspect](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_group_inspect)</td>
 <td>[bluemix ic group-instances](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_group_instances)</td>
 <td>[bluemix ic group-remove](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_group_remove)</td>
 <td>[bluemix ic group-update](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_group_update)</td>
 </tr>
 <tr>
  <td>[bluemix ic groups](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_groups)</td>
  <td>[bluemix ic info](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_info)</td>
  <td>[bluemix ic init](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_init)</td>
  <td>[ bluemix ic images](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_images)</td>
  <td>[bluemix ic inspect](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_inspect)</td>
 </tr>
 <tr>
 <td>[bluemix ic ip-bind](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_ip_bind)</td>
 <td>[bluemix ic ip-release](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_ip_release)</td>
 <td>[bluemix ic ip-request](/docs/cli/reference/bluemix_cli/index.html#ip_request)</td>
 <td>[bluemix ic ip-unbind](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_ip_unbind)</td>
 <td>[bluemix ic ips](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_ips)</td>
 </tr>
 <tr>
 <td>[bluemix ic kill](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_kill)</td>
 <td>[bluemix ic logs](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_logs)</td>
 <td>[bluemix ic namespace-get](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_namespace_get)</td>
 <td>[bluemix ic namespace-set](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_namespace_set)</td>
 <td>[bluemix ic pause](/docs/cli/reference/bluemix_cli/index.html#pause)</td>
 </tr>
 <tr>
 <td>[bluemix ic port](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_port)</td>
 <td>[bluemix ic ps](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_ps)</td>
 <td>[bluemix ic rename](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_rename)</td>
 <td>[bluemix ic reprovision](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_reprovision)</td>
 <td>[bluemix ic restart](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_restart)</td>
 </tr>
 <tr>
 <td>[bluemix ic rm](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_rm)</td>
 <td>[bluemix ic rmi](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_rmi)</td>
 <td>[bluemix ic route-map](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_route_map)</td>
 <td>[bluemix ic route-unmap](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_route_unmap)</td>
 <td>[bluemix ic run](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_run)</td>
 </tr>
 <tr>
 <td>[bluemix ic service-bind](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_service_bind)</td>
 <td>[bluemix ic service-unbind](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_service_unbind)</td>
 <td>[bluemix ic start](/docs/cli/reference/bluemix_cli/index.html#ic_start)</td>
 <td>[bluemix ic stats](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_stats)</td>
 <td>[bluemix ic stop](/docs/cli/reference/bluemix_cli/index.html#ic_stop)</td>
 </tr>
 <tr>
 <td>[bluemix ic top](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_top)</td>
 <td>[bluemix ic unpause](/docs/cli/reference/bluemix_cli/index.html#unpause)</td>
 <td>[bluemix ic unprovision](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_unprovision)</td>
 <td>[bluemix ic volume-inspect](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_inspect)</td>
 <td>[bluemix ic volume-create](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_create)</td>
 </tr>
 <tr>
 <td>[bluemix ic volume-fs](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_fs)</td>
 <td>[bluemix ic volume-fs-create](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_fs_create)</td>
 <td>[bluemix ic volume-fs-remove](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_fs_remove)</td>
 <td>[bluemix ic volume-fs-inspect](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_fs_inspect)</td>
 <td>[bluemix ic volume-fs-flavors](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_fs_flavors)</td>
 </tr>
 <tr>
 <td>[bluemix ic volume-remove](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_remove)</td>
 <td>[bluemix ic volumes](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volumes)</td>
 <td>[bluemix ic wait](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_wait)</td>
 <td>[bluemix ic wait-status](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_wait_status)</td>
 <td>[bluemix ic version](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_version)</td>
 </tr>
  </tbody>
 </table>


## bluemix ic attach
{: #bluemix_ic_attach}

Contrôlez un conteneur en cours d'exécution ou affichez sa sortie. Utilisez `CTRL+C` pour quitter et arrêter le conteneur. Cette commande appelle l'interface de ligne de commande Docker. Pour plus d'informations, voir la commande [attach ![icône de lien externe](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/attach/){: new_window} dans l'aide de Docker.

```
bluemix ic attach [--no-stdin] [--sig-proxy] CONTENEUR
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible, Docker

<strong>Options de commande</strong> :

   <dl>
   <dt>--no-stdin (facultatif)</dt>
   <dd>Indique de ne pas inclure l'entrée standard.</dd>
   <dt>--sig-proxy (facultatif)</dt>
   <dd>Indique d'envoyer par proxy tous les signaux reçus au processus. La valeur
par défaut est <i>true</i>.</dd>
   <dt><i>CONTENEUR</i> (requis)</dt>
   <dd>Nom ou ID du conteneur.</dd>
    </dl>

<strong>Exemples</strong> :

L'exemple suivant est une demande d'association au conteneur `mon_conteneur` :
```
bluemix ic attach mon_conteneur
```



## bluemix ic build
{: #bluemix_ic_build}

Appelez le service de génération IBM Containers afin de générer une image Docker localement ou dans votre référentiel {{site.data.keyword.Bluemix_notm}} privé. Cette commande appelle l'interface de ligne de commande Docker. Pour plus d'informations, voir la commande [build ![icône de lien externe](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/build/){: new_window} dans l'aide de Docker.

```
bluemix ic build -t ETIQUETTE|--tag ETIQUETTE [--no-cache] [-p|--pull] [-q|--quiet] EMPLACEMENT_DOCKERFILE
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible, Docker

<strong>Options de commande</strong> :
   <dl>
   <dt>-t <i>ETIQUETTE</i>|--tag <i>ETIQUETTE</i> (requis)</dt>
   <dd>Nom de référentiel à appliquer à l'image créée.</dd>
   <dt>--no-cache (facultatif)</dt>
   <dd>Indique de ne pas utiliser le cache lorsque l'image est générée. La valeur par défaut est <i>false</i>.</dd>
   <dt>--pull (facultatif)</dt>
   <dd>Indique d'essayer d'extraire l'image de base depuis le registre même si elle est en cache.</dd>
   <dt>-q|--quiet (facultatif)</dt>
   <dd>Supprime la sortie détaillée générée par les conteneurs. La valeur par défaut est <i>false</i>.</dd>
   <dt><i>EMPLACEMENT_DOCKERFILE</i> (requis)</dt>
   <dd>Chemin du fichier Dockerfile et du contexte sur l'hôte local.</dd>
    </dl>

<strong>Exemples</strong> :

L'exemple suivant illustre une demande de génération d'une image nommée *monimage*. Le document Dockerfile et les autres artefacts à utiliser dans la génération se trouvent dans le répertoire depuis lequel la commande est exécutée. Etant donné que le registre et l'espace de nom sont inclus dans le nom de l'image, l'image est générée dans le référentiel {{site.data.keyword.Bluemix_notm}} privé de votre organisation.
```
bluemix ic build -t registry.ng.bluemix.net/monespacenom/monimage
```


## bluemix ic cp
{: #bluemix_ic_cp}
Copie des fichiers ou des dossiers entre un conteneur et le système de fichiers local. Cette commande appelle l'interface de ligne de commande Docker. Pour plus d'informations, voir la commande [cp ![icône de lien externe](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/cp/){: new_window} dans l'aide de Docker.


## bluemix ic cpi
{: #bluemix_ic_cpi}

Accédez à une image Docker Hub ou à une image de votre registre local et copiez-la dans votre référentiel {{site.data.keyword.Bluemix_notm}} privé.

```
bluemix ic cpi IMAGE_SOURCE IMAGE_DESTINATION
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :
   <dl>
   <dt><i>IMAGE_SOURCE</i> (requis)</dt>
   <dd>Référentiel source et nom de l'image.</dd>
   <dt><i>IMAGE_DESTINATION</i> (requis)</dt>
   <dd>URL du référentiel {{site.data.keyword.Bluemix_notm}} privé, incluant l'espace de nom et le nom de l'image de destination. L'étiquette pour l'image est facultative.</dd>
   </dl>

<strong>Exemples</strong> :

Copiez une image depuis le référentiel source dans votre référentiel privé et ajoutez une étiquette pour l'image :

```
bluemix ic cpi référentiel_source/nom_image_source URL_registre_privé/nom_image_destination:étiquette
```

Copiez l'image `sinatra` depuis le référentiel `training` dans votre référentiel privé `registry.ng.bluemix.net/monespacenom` et nommez l'image `monimagesinatra`. Ajoutez une étiquette `v1` pour l'image `monimagesinatra`.

```
bluemix ic cpi training/sinatra registry.ng.bluemix.net/monespacenom/monimagesinatra:v1
```


## bluemix ic exec
{: #bluemix_ic_exec}

Exécutez une commande dans un conteneur. Pour plus d'informations, voir la commande [exec ![icône de lien externe](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/exec/){: new_window} dans l'aide de Docker.

```
bluemix ic exec [-d|--detach] [-it] [-u UTILISATEUR|--user UTILISATEUR] CONTENEUR [CMD]
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible, Docker

<strong>Options de commande</strong> :

   <dl>
   <dt>-d|--detach (facultatif)</dt>
   <dd>Indique d'exécuter en arrière-plan la commande spécifiée.</dd>
   <dt>-it (facultatif)</dt>
   <dd>Mode interactif. L'entrée standard continue d'être affichée. Entrez <i>exit</i> pour quitter.</dd>
   <dt>-u <i>UTILISATEUR</i>|--user <i>UTILISATEUR</i> (facultatif)</dt>
   <dd>Nom de l'utilisateur.</dd>
   <dt><i>CONTENEUR</i> (requis)</dt>
   <dd>Nom ou ID du conteneur.</dd>
   <dt><i>CMD</i> (facultatif)</dt>
   <dd>Commande à exécuter dans le(s) conteneur(s) spécifié(s).</dd>
   </dl>

<strong>Exemples</strong> :

Exécutez la commande `bash` dans le conteneur `mon_conteneur` en mode interactif :

```
bluemix ic exec -it mon_conteneur bash
```

Exécutez la commande `date` dans le conteneur `mon_conteneur` :

```
bluemix ic exec mon_conteneur date
```


## bluemix ic group-create
{: #bluemix_ic_group_create}

Créez un groupe de conteneurs évolutif.

```
bluemix ic group-create [--publish,-p PORT] --name NOM_GROUPE [--memory,-m TAILLE_MEMOIRE] [-n,--hostname NOM_HOTE] [-d,--domain DOMAINE] [--env,-e CLE_ENV=VAL_ENV] [--env-file
FICHIER_VARIABLE_ENVIRONNEMENT] [-P false|true] [--volume] [--min NOMBRE_MIN_INSTANCES] [--max NOMBRE_MAX_INSTANCES] [--desired NOMBRE_INSTANCES_SOUHAITE] [--anti false|true] [--auto false|true] NOM_IMAGE [CMD [CMD ...]]
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :
   <dl>
    <dt><i>NOM_IMAGE</i> (requis)</dt>
   <dd>Image à inclure dans chaque instance de conteneur dans le groupe de conteneurs. Vous pouvez spécifier des commandes après l'image, mais n'indiquez pas d'options. Incluez toutes les options avant de spécifier une image. <br><br>Si vous utilisez une image qui se trouve dans le référentiel {{site.data.keyword.Bluemix_notm}} privé de votre organisation, spécifiez l'image au format <i>registry.ng.bluemix.net/ESPACE_NOM/IMAGE</i>. <br><br>Si vous utilisez une image fournie par IBM Containers, n'incluez pas l'espace de nom de votre organisation. Spécifiez l'image au format <i>registry.ng.bluemix.net/IMAGE</i>. </dd>
   <dt>--name <i>NOM_GROUPE</i> (requis)</dt>
   <dd>Attribue un nom au groupe. <i>-n</i> est obsolète.<br>
   <strong>Astuce :</strong> le nom de conteneur doit commencer par une lettre. Il peut inclure des lettres majuscules, des
lettres minuscules, des chiffres, des points, des traits de soulignement (_) ou des traits d'union (-).</dd>
   <dt>-m <i>TAILLE_MEMOIRE</i>|--memory <i>TAILLE_MEMOIRE</i> (facultatif)</dt>
   <dd>Affecte une limite de mémoire, en Mo, au groupe. Lorsque vous créez un groupe de conteneurs depuis l'interface de ligne de commande, la valeur par défaut pour chaque instance de conteneur est <i>64</i> Mo. Lorsque vous créez un groupe de conteneurs depuis le tableau de bord {{site.data.keyword.Bluemix_notm}}, la valeur par défaut pour chaque instance de conteneur est <i>256</i> Mo. Les valeurs admises sont <i>64</i>, <i>256</i>, <i>512</i>, <i>1024</i> et <i>2048</i>. Une fois que vous avez affecté une limite de mémoire, vous ne pouvez plus la modifier.</dd>
   <dt>-n <i>NOM_HOTE</i>|--hostname <i>NOM_HOTE</i> (facultatif)</dt>
   <dd>Nom d'hôte, tel que <i>monhôteconteneur</i>. L'hôte et le domaine sont combinés pour former l'adresse URL de route publique complète, par exemple <i>http://monhôteconteneur.mybluemix.net</i>. Lorsque vous passez en revue les détails d'un groupe de conteneurs avec la commande <i>bluemix ic group-inspect</i>, l'hôte et le domaine sont affichés ensemble et constituent la route.</dd>
   <dt>-d <i>DOMAINE</i>|--domain <i>DOMAINE</i> (facultatif)</dt>
   <dd>Généralement, le domaine est <i>.mybluemix.net</i>. L'hôte et le domaine sont combinés pour former l'adresse URL de route publique complète, par exemple <i>http://monhôteconteneur.mybluemix.net</i>. Lorsque vous passez en revue les détails d'un groupe de conteneurs avec la commande <i>bluemix ic group-inspect</i>, l'hôte et le domaine sont affichés ensemble et constituent la route.</dd>
   <dt>-e <i>CLE_ENV=VAL_ENV</i>|--env <i>CLE_ENV=VAL_ENV</i> (facultatif)</dt>
   <dd>Définissez la variable d'environnement. Répertoriez plusieurs clés séparément. Si vous incluez des guillemets, placez-les autour du nom et de la valeur de la variable d'environnement. Par exemple : `-e "clé1=valeur1" -e "clé2=valeur2" -e "clé3=valeur3"`.  Le tableau suivant répertorie certaines variables d'environnement couramment utilisées que vous pouvez spécifier :</dd>
    </dl>


|  Variable d'environnement                              |     Description                            |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;nom_app&gt;*       | Liez un service à un conteneur. Utilisez la variable d'environnement `CCS_BIND_APP` pour lier
une application au conteneur. L'application est liée au service cible et sert de pont qui permet à {{site.data.keyword.Bluemix_notm}} de fournir les informations contenues dans la variable `VCAP_SERVICES` de votre application pont à votre instance de conteneur en cours d'exécution. Pour plus d'informations sur la création d'une application pont, voir
[Liaison d'un service à un conteneur](../../../containers/container_integrations_binding.html){: new_window}. |
| CCS_BIND_SRV=*&lt;nom_instance_service1&gt;*,*&lt;nom_instance_service2&gt;* | Pour lier un service Bluemix directement à un
conteneur sans utiliser d'application de pont, utilisez CCS_BIND_SRV. Cette liaison permet à Bluemix d'injecter les informations VCAP_SERVICES dans
l'instance de conteneur en cours d'exécution. Pour répertorier plusieurs services Bluemix, incluez-les dans la même variable d'environnement. |
| LOG_LOCATIONS=*&lt;chemin_fichier&gt;* | Ajoutez un fichier journal à surveiller dans le conteneur. Incluez la variable d'environnement `LOG_LOCATIONS` avec un chemin d'accès au fichier journal. |
{: caption="Tableau 2. Variables d'environnement couramment utilisées" caption-side="top"}

 <dl>
   <dt>--env-file <i>FICHIER_VARIABLE_ENVIRONNEMENT</i> (facultatif)</dt>
   <dd> Importe les variables d'environnement d'un fichier, env-file étant le chemin d'accès au fichier sur le répertoire local. Chaque ligne du fichier représente une paire clé=valeur. </dd>
   <dt>--volume <i>VOLUME</i>:<i>CHEMIN_CONTENEUR</i>[:ro] (facultatif)</dt>
   <dd>Rattache un volume à un conteneur en spécifiant ses détails sous le format <i>ID_volume:Chemin_conteneur[:ro]</i>.
   <ul>
   <li><i>VOLUME</i> : ID ou nom du volume.</li>
   <li><i>CHEMIN_CONTENEUR</i> : Chemin absolu du volume dans le conteneur.</li>
   <li>ro (facultatif) : La spécification de <i>ro</i> rend le volume accessible en lecture seule, au lieu de le laisser accessible par défaut en lecture/écriture.</li></ul>
   </dd>
   <dt>-p <i>PORT</i>|--publish <i>PORT</i> (facultatif)</dt>
   <dd>Expose le port pour le trafic HTTP. Les conteneurs qui se trouvent dans votre groupe doivent être à l'écoute sur le port HTTP. Il n'est pas possible d'envoyer des demandes HTTPS. Vous ne pouvez pas inclure plusieurs ports pour les groupes de conteneurs. <br><br>Lorsque vous spécifiez un port, vous mettez l'application à disposition dans l'équilibreur de charge {{site.data.keyword.Bluemix_notm}} ou dans les conteneurs qui tentent d'accéder à l'hôte dans le même espace {{site.data.keyword.Bluemix_notm}}. L'équilibreur de charge ou les conteneurs {{site.data.keyword.Bluemix_notm}} peuvent alors utiliser le port pour joindre l'hôte et l'application dans le même espace {{site.data.keyword.Bluemix_notm}}. Si un port est spécifié dans le document Dockerfile pour l'image que vous utilisez, incluez ce port. <br>
   <strong>Conseils </strong>: <ul>
   <li>Pour l'image Liberty Server certifiée IBM, ou une version modifiée de cette image, entrez le port 9080.</li>
   <li>Pour l'image Node.js certifiée IBM, ou une version modifiée de cette image, entrez le port 8000.</li>
   </ul>
   </dd>
   <dt>-P (facultatif)</dt>
   <dd>Publie tous les ports</dd>
   <dt>--min <i>NOMBRE_MIN_INSTANCES</i> (facultatif)</dt>
   <dd>Nombre minimal d'instances. La valeur par défaut est 1. Si vous définissez un nombre minimum d'instances, cette valeur ne peut plus être modifiée après la création du groupe de conteneurs.</dd>
   <dt>--max <i>NOMBRE_MAX_INSTANCES</i> (facultatif)</dt>
   <dd>Nombre maximal d'instances. La valeur par défaut est 2. Si vous définissez un nombre maximum d'instances, cette valeur ne peut plus être modifiée après la création du groupe de conteneurs.</dd>
   <dt>--desired <i>NOMBRE_INSTANCES_SOUHAITE</i> (facultatif)</dt>
   <dd>Nombre d'instances dont vous avez besoin. La valeur par défaut est 2.</dd>
   <dt>--auto (facultatif)</dt>
   <dd>Lorsque le groupe de conteneurs est créé et que la reprise automatique est activée, IBM Containers vérifie la santé de chaque instance en envoyant une demande HTTP au port affecté.<br>
   Si aucune réponse n'est reçue d'une instance de conteneur aux cours de deux intervalles consécutifs de 90 secondes, l'instance est supprimée et remplacée par une nouvelle instance. Aucune action n'est effectuée si le conteneur répond. Ce processus est répété en permanence. Au cours d'une fenêtre de 30 minutes, si le nombre total de conteneurs différents qui sont membres du groupe est égal ou supérieur à trois fois la taille maximale observée pour le groupe, la reprise automatique est désactivée définitivement pour le groupe de conteneurs. Pour l'activer à nouveau, vous devez recréer le groupe de conteneurs.</dd>
  <dt>--anti (facultatif)</dt>
  <dd> Utilisez l'anti-affinité pour élever le niveau de haute disponibilité de votre groupe de conteneurs. L'option --anti force chaque instance de conteneur de votre groupe à être placée sur un noeud de traitement physique distinct, ce qui réduit les chances que tous les conteneurs d'un groupe tombent en panne en même temps en cas de défaillance matérielle. Il se peut que vous ne puissiez pas utiliser cette option avec des tailles de groupe plus importantes car chaque région et organisation Bluemix possède un ensemble limité de noeuds de traitement disponibles pour déploiement. Si votre déploiement échoue, vous pouvez soit réduire le nombre d'instances de conteneur dans le groupe, soit retirer l'option --anti. </dd>
   <dt><i>CMD</i> (facultatif)</dt>
   <dd>Commande et arguments transmis au groupe de conteneurs pour exécution. Cette commande doit être une commande à exécution longue. N'utilisez pas de commande à exécution courte, c'est-à-dire qui ne s'exécute pas très longtemps, comme <i>/bin/date</i>, car elle pourrait entraîner la panne du conteneur.  <br> <strong>Remarques :</strong> <ul>
   <li>La commande et les arguments doivent être spécifiés à la fin de la ligne de commande <i>bluemix ic run</i>.</li>
   <li>Si les arguments de commande incluent un trait d'union (-), comme dans <i>-c</i> dans l'exemple de commande précédent, la commande doit être précédée par deux traits d'union (--).</li>
   </ul></dd>
   </dl>


<strong>Exemples</strong> :

Créez un groupe de conteneurs `mon_groupe_conteneurs` en utilisant l'image `registry.ng.bluemix.net/ibmnode` fournie par IBM Containers, puis exécutez la commande à exécution longue `ping localhost` sur ce groupe de conteneurs :

```
bluemix ic group-create --name mon_groupe_conteneurs registry.ng.bluemix.net/ibmnode ping localhost
```

Créez un groupe de conteneurs `mon_groupe_conteneurs` en utilisant l'image `registry.ng.bluemix.net/ibmnode` fournie par IBM Containers, puis exécutez la commande à exécution longue `tail -f /dev/null` sur ce groupe de conteneurs :

```
bluemix ic group-create --name mon_groupe_conteneurs registry.ng.bluemix.net/ibmnode -- tail -f /dev/null
```

Créez un groupe évolutif `mongroupe` pour lequel la reprise automatique est activée en utilisant l'image `registry.ng.bluemix.net/ibmliberty`. Le port est `9080`, le nom d'hôte est `monhôteconteneur` et le nom de domaine est `mybluemix.net`.
```
bluemix ic group-create -p 9080 --auto -n monhôteconteneur -d mybluemix.net --name mongroupe registry.ng.bluemix.net/ibmliberty
```


## bluemix ic group-inspect
{: #bluemix_ic_group_inspect}

Affichez les informations détaillées, comme les variables d'environnement, les ports ou la mémoire, qui sont spécifiées pour un groupe de conteneurs lors de sa création.

```
bluemix ic group-inspect GROUPE_CONTENEURS
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :

   <dl>
   <dt><i>GROUPE_CONTENEURS</i> (requis)</dt>
   <dd>ID ou nom du groupe de conteneurs.</dd>
   </dl>

<strong>Exemples</strong> :

L'exemple suivant est une demande d'inspection du groupe de conteneurs `mon_groupe` :
```
bluemix ic group-inspect mon_groupe
```


## bluemix ic group-instances
{: #bluemix_ic_group_instances}

Répertoriez les instances d'un groupe de conteneurs spécifié.

```
bluemix ic group-instances GROUPE_CONTENEURS
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :

   <dl>
   <dt><i>GROUPE_CONTENEURS</i> (requis)</dt>
   <dd>ID ou nom du groupe de conteneurs.</dd>
   </dl>

<strong>Exemples</strong> :

Répertoriez toutes les instances du groupe de conteneurs `mon_groupe` :
```
bluemix ic group-instances mon_groupe
```


## bluemix ic group-remove
{: #bluemix_ic_group_remove}

Retirez un groupe de conteneurs d'un espace.

```
bluemix ic group-remove [-f|--force] NOM_GROUPE [GROUP_NAME2 [...]]
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :

   <dl>
   <dt>-f|--force (facultatif)</dt>
   <dd>Force le retrait d'un conteneur en exécution ou défaillant.</dd>
   <dt><i>NOM_GROUPE</i> (requis)</dt>
   <dd>ID ou nom du groupe de conteneurs.</dd>
   </dl>


<strong>Exemples</strong> :

L'exemple suivant est une demande de retrait d'un groupe de conteneurs dont le nom est `mon_groupe` :
```
bluemix ic group-remove mon_groupe
```


## bluemix ic group-update
{: #bluemix_ic_group_update}

Mettez à jour un groupe de conteneurs.


```
bluemix ic group-update [--anti] [--desired NOMBRE_INSTANCES_SOUHAITE] [-e ENV_KEY=VAL_ENV] NOM_GROUPE
```

**Astuce :** afin de mettre à jour le nom d'hôte ou le domaine pour un groupe de conteneurs, utilisez `bluemix ic route-map [-n HOTE][-d DOMAIN] GROUPE_CONTENEURS`.

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :
 <dl>
   <dt>--anti (facultatif)</dt>
   <dd>Utilisez l'anti-affinité pour élever le niveau de haute disponibilité de votre groupe de conteneurs. L'option --anti force chaque instance de conteneur de votre groupe à être placée sur un noeud de traitement physique distinct, ce qui réduit les probabilités que tous les conteneurs d'un groupe tombent en panne en même temps en cas de défaillance matérielle. Il se peut que vous ne puissiez pas utiliser cette option avec des tailles de groupe plus importantes car chaque région et organisation Bluemix possède un ensemble limité de noeuds de traitement disponibles pour déploiement. Si votre déploiement échoue, vous pouvez soit réduire le nombre d'instances de conteneur dans le groupe, soit retirer l'option --anti.</dd>
   <dt>--desired <i>NOMBRE_INSTANCES_SOUHAITE</i> (facultatif)</dt>
   <dd>Nombre d'instances dont vous avez besoin. La valeur par défaut est <i>2</i>.</dd>
   <dt>-e <i>CLE_ENV=VAL_ENV</i>(facultatif)</dt>
   <dd>Définissez la variable d'environnement. Répertoriez plusieurs clés séparément. Si vous incluez des guillemets, placez-les autour du nom et de la valeur de la variable d'environnement. Par exemple : `-e "clé1=valeur1" -e "clé2=valeur2" -e "clé3=valeur3"`.</dd>
   <dt><i>NOM_GROUPE</i> (requis)</dt>
   <dd>ID ou nom du groupe de conteneurs.</dd>
   </dl>

<strong>Exemples</strong> :

L'exemple suivant est une demande de mise à jour du groupe de conteneurs `mon_groupe` :
```
bluemix ic group-update --desired 5 mon_groupe
```


## bluemix ic groups
{: #bluemix_ic_groups}

Répertoriez les groupes de conteneurs qui existent dans le référentiel {{site.data.keyword.Bluemix_notm}} privé de l'organisation.

```
bluemix ic groups [-q]
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :
	<dl>
	<dt>-q (facultatif)</dt>
   	<dd>Affiche uniquement les ID groupe</dd>
	</dl>


## bluemix ic images
{: #bluemix_ic_images}

Affichez la liste de toutes les images disponibles dans le référentiel {{site.data.keyword.Bluemix_notm}} privé de l'organisation. Pour plus d'informations, voir la commande [images ![icône de lien externe](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/images){: new_window} dans l'aide de Docker. La liste inclut l'ID de l'image, la date de création et le nom de l'image.

```
bluemix ic images [-a|--all] [-f CONDITION] [--no-trunc] [-q|--quiet]
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible, Docker

<strong>Options de commande</strong> :

   <dl>
   <dt>-a|--all (facultatif)</dt>
   <dd>Indique d'inclure toutes les couches d'image pour chaque image dans le référentiel de votre organisation, et non pas seulement la couche la plus récente.</dd>
   <dt>-f (facultatif)</dt>
   <dd>Filtre la liste des images en fonction de la condition fournie.</dd>
   <dt>--no-trunc (facultatif)</dt>
   <dd>Indique de ne pas tronquer la sortie.</dd>
   <dt>-q|--quiet (facultatif)</dt>
   <dd>Indique d'afficher uniquement les ID numériques.</dd>
   </dl>

<strong>Exemples</strong> :

L'exemple suivant est une demande de réception de la liste des images disponibles pour l'organisation :
```
bluemix ic images
```


## bluemix ic info
{: #bluemix_ic_info}

Affichez un ensemble d'informations décrivant l'état de l'instance de service cloud de conteneur. Les informations incluent la limite relative aux conteneurs, l'utilisation des conteneurs, les conteneurs en cours d'exécution, la limite de mémoire, l'utilisation de la mémoire, la limite relative aux adresses IP flottantes, l'utilisation des adresses IP flottantes, l'adresse URL de l'hôte CCS, l'adresse URL de l'hôte du registre et le statut du mode débogage.

```
bluemix ic info
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible


## bluemix ic init
{: #bluemix_ic_init}

Initialisez l'environnement des conteneurs sur votre machine locale afin d'utiliser l'ensemble des capacités du service IBM Containers.

```
bluemix ic init
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

**Remarque :** avant l'initialisation, assurez-vous que l'interface de ligne de commande Docker (docker) est installée et configurée dans votre variable d'environnement PATH. Pour passer dans une autre région, utilisez la commande `bluemix region-set`.

<strong>Exemples</strong> :

Passez dans la région `us-south` :

```
bluemix region-set us-south
```


## bluemix ic inspect
{: #bluemix_ic_inspect}

Affichez les informations sur un conteneur. Pour plus d'informations, voir la commande [inspect ![icône de lien externe](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/inspect){: new_window} dans l'aide de Docker.

```
bluemix ic inspect [IMAGE|images|CONTENEUR]
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible, Docker

<strong>Options de commande</strong> :

   <dl>
   <dt><i>IMAGE</i> (requis)</dt>
   <dd>Affiche des informations détaillées sur une image spécifique en indiquant son nom ou son ID.</dd>
   <dt>images (requis)</dt>
   <dd>Affiche des informations détaillées sur toutes les images de votre référentiel.</dd>
   <dt><i>CONTENEUR</i> (requis)</dt>
   <dd>Affiche des informations détaillées sur un conteneur spécifique en indiquant son nom ou son ID.</dd>
   </dl>

**Remarque :** vous ne pouvez spécifier qu'un seul des arguments suivants à la fois : *IMAGE*, *images* ou *CONTENEUR*.

<strong>Exemples</strong> :

L'exemple suivant est une demande d'inspection d'un conteneur dont le nom est `proxy` :
```
bluemix ic inspect proxy
```


## bluemix ic ip-bind
{: #bluemix_ic_ip_bind}

Liez une adresse IP flottante disponible à un conteneur.

```
bluemix ic ip-bind ADRESSE_IP CONTENEUR
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :

   <dl>
   <dt><i>ADRESSE_IP</i> (requis)</dt>
   <dd>Adresse IP à lier.</dd>
   <dt><i>CONTENEUR</i> (requis)</dt>
   <dd>Nom ou ID du conteneur à lier.</dd>
   </dl>

<strong>Exemples</strong> :

L'exemple suivant est une demande de liaison de l'adresse IP `192.123.12.12` au conteneur `proxy` :
```
bluemix ic ip-bind 192.123.12.12 proxy
```


## bluemix ic ip-release
{: #bluemix_ic_ip_release}

Libérez une adresse IP flottante de l'instance de service cloud de conteneur.

```
bluemix ic ip-release ADRESSE_IP [ADRESSE2_IP [...]]
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :

   <dl>
   <dt><i>ADRESSE_IP</i> (requis)</dt>
   <dd>Adresse IP à libérer.</dd>
   </dl>


## bluemix ic ip-request
{: #ip_request}
Demandez une nouvelle adresse IP flottante.

```
bluemix ic ip-request [-q]
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :

   <dl>
   <dt>-q (facultatif)</dt>
   <dd>Répertorie uniquement les adresses IP, sans les ID des conteneurs qui sont liés à ces adresses IP.</dd>
   </dl>


## bluemix ic ip-unbind
{: #bluemix_ic_ip_unbind}

Annulez la liaison d'une adresse IP flottante à son conteneur.

Les adresses IP publiques constituent une ressource limitée dans IBM Containers. Par conséquent, les adresses IP publiques qui sont allouées à un espace et qui ne sont pas liées à un conteneur sont régulièrement récupérées auprès des utilisateurs de l'essai gratuit, environ toutes les semaines. Les adresses IP publiques non liées ne sont jamais récupérées auprès des utilisateurs facturés ponctuellement ou disposant d'un abonnement.

```
bluemix ic ip-unbind ADRESSE_IP CONTENEUR
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :

   <dl>
   <dt><i>ADRESSE_IP</i> (requis)</dt>
   <dd>Adresse IP pour laquelle annuler la liaison.</dd>
   <dt><i>CONTENEUR</i> (requis)</dt>
   <dd>ID ou nom du conteneur pour lequel annuler la liaison.</dd>
   </dl>

<strong>Exemples</strong> :

L'exemple suivant est une demande d'annulation de la liaison de l'adresse IP `192.123.12.12` au conteneur `proxy` :
```
bluemix ic ip-unbind 192.123.12.12 proxy
```


## bluemix ic ips
{: #bluemix_ic_ips}

Répertoriez les adresses IP flottantes disponibles pour l'utilisateur connecté. La liste répertorie les adresses IP et l'ID de conteneur auquel les adresses IP sont liées. Si l'adresse IP n'est pas utilisée, aucun ID de conteneur n'est affiché.

```
bluemix ic ips [-q]
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :

   <dl>
   <dt>-q (facultatif)</dt>
   <dd>Répertorie uniquement les adresses IP, sans les ID des conteneurs qui sont liés à ces adresses IP.</dd>
   </dl>


<strong>Exemples</strong> :

L'exemple suivant illustre une demande de réception de la liste de toutes les adresses IP disponibles pour l'organisation :
```
bluemix ic ips -q
```


## bluemix ic kill
{: #bluemix_ic_kill}

Arrêtez un processus en cours dans un conteneur sans arrêter le conteneur. Pour plus d'informations, voir la commande [kill ![icône de lien externe](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/kill/){: new_window} dans l'aide de Docker.

```
bluemix ic kill [-s CMD|--signal CMD] CONTENEUR
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible, Docker

<strong>Options de commande</strong> :

   <dl>
   <dt>-s <i>CMD</i>|--signal <i>CMD</i> (facultatif)</dt>
   <dd>Envoie une commande au processus s'exécutant dans le conteneur.</dd>
   <dt><i>CONTENEUR</i> (requis)</dt>
   <dd>ID ou nom du conteneur.</dd>
   </dl>


<strong>Exemples</strong> :

L'exemple suivant est une demande d'arrêt du processus dans un conteneur dont le nom est `proxy` :
```
bluemix ic kill proxy
```


## bluemix ic logs
{: #bluemix_ic_logs}

Affiche les journaux de sortie ou d'erreur d'un conteneur en cours d'exécution. Pour plus d'informations, voir la commande [logs ![icône de lien externe](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/logs/){: new_window} dans l'aide de Docker.
```
bluemix ic logs [OPTIONS] CONTENEUR
```


## bluemix ic namespace-get
{: #bluemix_ic_namespace_get}

Affichez le nom du référentiel d'images {{site.data.keyword.Bluemix_notm}} privé pour l'organisation à laquelle vous êtes connecté.

```
bluemix ic namespace-get
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible


## bluemix ic namespace-set
{: #bluemix_ic_namespace_set}

Définissez le nom du référentiel d'images {{site.data.keyword.Bluemix_notm}} privé pour l'organisation à laquelle vous êtes connecté.

*Restriction* : vous ne pouvez pas utiliser de trait d'union (`-`) dans le nom d'espace de nom de votre référentiel.

```
bluemix ic namespace-set NOM
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :

   <dl>
   <dt><i>NOM</i> (requis)</dt>
   <dd>Fonction exécutée une seule fois pour définir l'espace de nom du référentiel de votre organisation, si ce n'est déjà fait. Une fois l'espace de nom défini, réinitialisez IBM Containers avec la commande `bluemix ic init` avant de continuer.</dd>
   </dl>


## bluemix ic pause
{: #pause}

Interrompez tous les processus d'un conteneur en cours d'exécution. Pour plus d'informations, voir la commande [pause ![icône de lien externe](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/pause/){: new_window} dans l'aide de Docker. Pour arrêter un conteneur, voir la commande [bluemix ic unpause](#unpause).

```
bluemix ic pause CONTENEUR
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible, Docker

<strong>Options de commande</strong> :
   <dl>
   <dt><i>CONTENEUR</i> (requis)</dt>
   <dd>Nom ou ID du conteneur.</dd>
   </dl>

<strong>Réponses</strong> :

- Paused container successfully.

- Command failed with container cloud service

 `{message}`

 Où `{message}` est l'erreur connexe.

- Command failed - Could not connect to container cloud service

<strong>Exemples</strong> :

L'exemple suivant est une demande d'interruption d'un conteneur dont le nom est `proxy` :
```
bluemix ic pause proxy
```


## bluemix ic port
{: #bluemix_ic_port}

Répertoriez les mappages de port ou un mappage spécifique pour le conteneur. Cette commande encapsule la commande `docker port`. Pour plus d'informations, voir la commande [port ![icône de lien externe](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/port/){: new_window} dans l'aide de Docker.


## bluemix ic ps
{: #bluemix_ic_ps}
Affichez la liste des conteneurs en cours d'exécution dans l'espace de nom de l'utilisateur connecté. Par défaut, cette commande affiche seulement les conteneurs en cours d'exécution. Pour plus d'informations, voir la commande [ps ![icône de lien externe](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/ps/){: new_window} dans l'aide de Docker.

```
bluemix ic ps [-a|--all] [--filter env=CRITERES_RECHERCHE] [-s|--size] [-l NOMBRE|--limit NOMBRE] [-q|--quiet]
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible, Docker

<strong>Options de commande</strong> :

   <dl>
   <dt>-a|--all (facultatif)</dt>
   <dd>Affiche tous les conteneurs, qu'ils soient en exécution ou arrêtés.</dd>
   <dt>--filter env=<i>CRITERES_RECHERCHE</i> (facultatif)</dt>
   <dd>Recherche les conteneurs possédant une valeur de variable d'environnement spécifique. Vous pouvez filtrer vos conteneurs en fonction d'une clé de variable d'environnement ou d'une valeur répertoriée dans la section Env de votre réponse d'interface de ligne de commande lorsque vous inspectez un conteneur. Remplacez CRITERES_RECHERCHE par la clé ou la valeur recherchée. Vos critères de recherche n'ont pas besoin de renvoyer une correspondance exacte. </dd>
   <dt>-s|--size (facultatif)</dt>
   <dd>Répertorie les tailles des conteneurs.</dd>
   <dt>-l <i>NOMBRE</i>|--limit <i>NOMBRE</i> (facultatif)</dt>
   <dd>Répertorie les conteneurs les plus récemment créés, où <i>NOMBRE</i> est le nombre de ces conteneurs que vous désirez renvoyer. <br><br> Par exemple, si vous
avez créé séquentiellement les conteneurs <i>node1</i> à <i>node5</i>, la commande <i>bluemix ic ps --limit 2</i> renvoie node4 et node5 puisqu'il s'agit des
deux derniers conteneurs créés. </dd>
   <dt>-q|--quiet (facultatif)</dt>
   <dd>Indique d'afficher uniquement les ID des conteneurs.</dd>
   </dl>


<strong>Exemples</strong> :

L'exemple suivant est une demande d'affichage de tous les conteneurs en cours d'exécution et arrêtés :
```
bluemix ic ps -a
```


## bluemix ic rename
{: #bluemix_ic_rename}
Renomme un conteneur. Pour plus d'informations, voir la commande [rename ![icône de lien externe](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/rename/){: new_window} dans l'aide de Docker.

```
bluemix ic rename ANCIEN_NOM NOUVEAU_NOM
```
<strong>Prérequis</strong> : Noeud final, Connexion, Cible, Docker

<strong>Options de commande</strong> :

<dl>
   <dt><i>ANCIEN_NOM</i> (requis)</dt>
   <dd>Ancien nom du conteneur.</dd>
   <dt><i>NOUVEAU_NOM</i> (requis)</dt>
   <dd>Nouveau nom du conteneur.</dd>
   </dl>


## bluemix ic reprovision
{: #bluemix_ic_reprovision}

Recrée le service IBM Containers dans l'espace Bluemix auquel vous êtes connecté. Le quota d'origine pour l'espace est conservé.

<strong>Important</strong> : lorsque vous exécutez cette commande, aucun de vos conteneurs et groupes de conteneurs contenus dans cet espace ne sera
migrés vers l'espace qui est remis à disposition et vos conteneurs et groupes seront retirés lors du processus de migration.

```
bluemix ic reprovision [--force|-f] [ZONE_DISPONIBILITE]
```
<strong>Options de commande</strong> :

<dl>
   <dt>--force|-f (facultatif)</dt>
   <dd>Force la recréation du service IBM Containers dans l'espace Bluemix.</dd>
   <dt><i>ZONE_DISPONIBILITE</i> (facultatif)</dt>
   <dd>Nom de la zone de disponibilité IBM Containers dans laquelle vos conteneurs sont déployés. Si aucune zone de disponibilité n'est spécifiée, la zone de disponibilité par défaut définie pour la région est utilisée.</dd>
   </dl>


## bluemix ic restart
{: #bluemix_ic_restart}

Redémarrer un conteneur. Pour plus d'informations, voir la commande [restart ![icône de lien externe](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/restart/){: new_window} dans l'aide de Docker.

```
bluemix ic restart CONTENEUR [-t SECS|--time SECS]
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible, Docker

<strong>Options de commande</strong> :

   <dl>
   <dt><i>CONTENEUR</i> (requis)</dt>
   <dd>Nom ou ID du conteneur.</dd>
   <dt>-t <i>SECS</i>|--time <i>SECS</i> (facultatif)</dt>
   <dd>Nombre de secondes pendant lesquelles patienter avant le redémarrage du conteneur.</dd>
   </dl>


<strong>Réponses</strong> :

- Restarted container successfully.

- Command failed with container cloud service

 `{message}`

 Où `{message}` est l'erreur connexe.

- Command failed - Could not connect to container cloud service

<strong>Exemples</strong> :

L'exemple suivant est une demande de redémarrage d'un conteneur dont le nom est `proxy` :
```
bluemix ic restart proxy
```


## bluemix ic rm
{: #bluemix_ic_rm}

Supprimez un conteneur. Pour plus d'informations, voir la commande [rm ![icône de lien externe](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/rm/){: new_window} dans l'aide de Docker.

```
bluemix ic rm [-f|--force] CONTENEUR
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible, Docker

<strong>Options de commande</strong> :

   <dl>
   <dt>-f|--force (facultatif)</dt>
   <dd>Force le retrait d'un conteneur en exécution ou défaillant.</dd>
   <dt><i>CONTENEUR</i> (requis)</dt>
   <dd>Nom ou ID du conteneur.</dd>
   </dl>

<strong>Réponses</strong> :

- Removed container successfully.

- Command failed with container cloud service

 `{message}`

 Où `{message}` est l'erreur connexe.

- Command failed - Could not connect to container cloud service.

<strong>Exemples</strong> :

L'exemple suivant est une demande de retrait d'un conteneur dont le nom est `proxy` :
```
bluemix ic rm proxy
```


## bluemix ic rmi
{: #bluemix_ic_rmi}

Supprimez une image de l'espace de nom de l'utilisateur connecté. Pour plus d'informations, voir la commande [rmi ![icône de lien externe](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/rmi/){: new_window} dans l'aide de Docker.

```
bluemix ic rmi [-R REGISTRE|--registry REGISTRE] IMAGE
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible, Docker

<strong>Options de commande</strong> :

   <dl>
   <dt>-R <i>REGISTRE</i>|--registry <i>REGISTRE</i> (facultatif)</dt>
   <dd>Changer l'hôte de registre. Par défaut, le registre que vous spécifiez dans la commande <i>bluemix ic init</i> est utilisé.</dd>
   <dt><i>IMAGE</i> (requis)</dt>
   <dd>Nom de l'image à supprimer. Si aucune étiquette n'est spécifiée dans le nom de l'image, l'image associée à l'étiquette <i>latest</i> est supprimée par défaut.</dd>
   </dl>

<strong>Réponses</strong> :

- Removed: `{IMAGE}`

 Où `{IMAGE}` est le nom de l'image qui a été supprimée.

- Error! No registry host specified.

- Image remove failed - Could not connect to container cloud registry

- Command failed with container cloud service

 `{message}`

 Où `{message}` est l'erreur connexe.

<strong>Exemples</strong> :

L'exemple suivant est une demande de retrait de l'image `monespacenom/monimage:latest` :
```
bluemix ic rmi registry.ng.bluemix.net/monespacenom/monimage:latest
```


## bluemix ic route-map
{: #bluemix_ic_route_map}

Etablissez la route pour le trafic Internet à utiliser pour accéder au groupe de conteneurs. Vous pouvez utiliser cette commande pour établir une nouvelle route ou mettre à jour une route existante.

```
bluemix ic route-map [-n HOTE|--hostname HOTE] [-d DOMAINE|--domain DOMAINE] GROUPE_CONTENEURS
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :

   <dl>
   <dt>-n <i>HOTE</i>|--hostname <i>HOTE</i> (facultatif)</dt>
   <dd>Nom d'hôte de la route. Il s'agit de la première partie de l'adresse URL de route publique complète, par exemple <i>monhôteconteneur</i> dans l'adresse URL <i>monhôteconteneur.mybluemix.net</i>.</dd>
   <dt>-d <i>DOMAINE</i>|--domain <i>DOMAINE</i> (facultatif)</dt>
   <dd>Nom de domaine pour la route, qui constitue la seconde partie de l'URL complète de route publique. Dans la plupart des cas, le domaine est
<i>mybluemix.net</i>. Vous pouvez aussi utiliser ce paramètre pour spécifier un domaine privé.</dd>
   <dt><i>GROUPE_CONTENEURS</i> (requis)</dt>
   <dd>ID ou nom du groupe de conteneurs.</dd>
   </dl>

<strong>Exemples</strong> :

L'exemple ci-dessous illustre une demande de mappage de la route du groupe appelé `GROUPE1`, où `mon_hôte` est le
nom de l'hôte et `mybluemix.net` est le domaine.
```
bluemix ic route-map -n mon_hôte -d mybluemix.net GROUPE1
```


## bluemix ic route-unmap
{: #bluemix_ic_route_unmap}

Etablissez la route pour le trafic Internet à utiliser pour accéder au groupe de conteneurs. Vous pouvez utiliser cette commande pour établir une nouvelle route ou mettre à jour une route existante.

```
bluemix ic route-unmap [-n HOTE|--hostname HOTE] [-d DOMAINE|--domain DOMAINE] GROUPE_CONTENEURS
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :

   <dl>
   <dt>-n <i>HOTE</i>|--hostname <i>HOTE</i> (facultatif)</dt>
   <dd>Nom d'hôte de la route.</dd>
   <dt>-d <i>DOMAINE</i>|--domain <i>DOMAINE</i> (facultatif)</dt>
   <dd>Nom de domaine de la route.</dd>
   <dt><i>GROUPE_CONTENEURS</i> (requis)</dt>
   <dd>ID ou nom du groupe de conteneurs.</dd>
   </dl>

<strong>Exemples</strong> :

L'exemple suivant illustre une demande d'annulation du mappage de la route du groupe intitulé `GROUPE1`, où `mon_hôte` est le
nom de  l'hôte et `organization.com`, le domaine.
```
bluemix ic route-unmap -n mon_hôte -d organisation.com GROUPE1
```


## bluemix ic run
{: #bluemix_ic_run}

Démarrez un nouveau conteneur dans le service cloud de conteneur depuis un nom d'image. Pour plus d'informations, voir la commande [run ![icône de lien externe](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/run/){: new_window} dans l'aide de Docker.


```
bluemix ic run [-p PORT|--publish PORT] [-P] [-m MEMOIRE|--memory MEMOIRE] [-e ENV|--env ENV] [-volume VOLUME:CHEMIN_CONTENEUR] -n NOM|--name NOM [--link NOM:ALIAS] [-it] IMAGE [CMD [CMD ...]]
```
**Remarque :** vérifiez que l'outil de commandes Cloud Foundry est installé et que vous disposez d'un jeton Cloud Foundry. L'aboutissement
d'une connexion à l'aide de `bluemix login` et de `bluemix ic init` génère le jeton et les certificats requis.


<strong>Prérequis</strong> : Noeud final, Connexion, Cible, Docker

<strong>Options de commande</strong> :

   <dl>
   <dt>-p <i>PORT</i>|--publish <i>PORT</i> (facultatif)</dt>
   <dd>Expose le port pour le trafic HTTP. Incluez tous les ports spécifiés dans le document Dockerfile pour l'image que vous utilisez. Vous pouvez inclure plusieurs ports avec plusieurs options <i>-p</i>. L'exposition d'un port lie automatiquement une adresse IP publique au conteneur si une telle adresse est disponible. <br><br>Si une adresse IP existe dans l'espace à lier au conteneur, vous pouvez la spécifier plutôt que de procéder à la liaison ultérieurement. L'adresse IP doit être spécifiée au format &lt;adresse_ip&gt;:&lt;port_conteneur&gt;:&lt;port_conteneur&gt; <br><br>Pour plus d'informations sur la demande d'adresses IP pour un espace, voir la commande <a href="index.html#ip_request" target="_blank">bluemix ic ip-request</a>. <br><br>Lorsque vous spécifiez un port, vous rendez l'application disponible dans l'équilibreur de charge {{site.data.keyword.Bluemix_notm}} ou dans les conteneurs du même espace {{site.data.keyword.Bluemix_notm}} qui tentent d'accéder à l'hôte. Si un port est spécifié dans le document Dockerfile pour l'image que vous utilisez, incluez ce port. <br><br><strong>Conseils :</strong><ul><li>Pour l'image Liberty Server certifiée IBM, ou une version modifiée de cette image, entrez le port 9080.</li><li>Pour l'image Node.js certifiée IBM, ou une version modifiée de cette image, entrez le port 8000.</li></ul></dd>
   <dt>-P (facultatif)</dt>
   <dd>Expose automatiquement au trafic HTTP les ports spécifiés dans le fichier Dockerfile de l'image.</dd>
   <dt>-m <i>MEMOIRE</i>|--memory <i>MEMOIRE </i> (facultatif)</dt>
   <dd>Affecte une limite de mémoire, en Mo, au groupe. Lorsque vous créez un groupe de conteneurs depuis l'interface de ligne de commande, la valeur par défaut pour chaque instance de conteneur est 64 Mo.  Lorsque vous créez un groupe de conteneurs depuis le tableau de bord {{site.data.keyword.Bluemix_notm}}, la valeur par défaut est 256 Mo. Les valeurs admises sont : 64, 256, 512, 1024 et 2048 Mo. Une fois que vous avez affecté une limite de mémoire, vous ne pouvez plus la modifier.</dd>
   <dt>-e <i>ENV</i>|--env <i>ENV</i> (facultatif)</dt>
   <dd>Définit la variable d'environnement, où <i>ENV</i> représente une paire clé=valeur. Répertoriez plusieurs clés séparément. Si vous incluez des guillemets, placez-les autour du nom et de la valeur de la variable d'environnement. Par exemple : -e "clé1=valeur1" -e "clé2=valeur2" -e "clé3=valeur3". Le tableau suivant répertorie certaines variables d'environnement couramment utilisées que vous pouvez spécifier :</dd>
   </dl>


|      Variable d'environnement                          |   Description                              |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;nom_app&gt;*       | Liez un service à un conteneur. Utilisez la variable d'environnement `CCS_BIND_APP` pour lier
une application au conteneur. L'application est liée au service cible et sert de pont qui permet à {{site.data.keyword.Bluemix_notm}} de fournir les informations contenues dans la variable `VCAP_SERVICES` de votre application pont dans votre instance de conteneur en cours d'exécution. Pour plus d'informations sur la création d'une application pont, voir
[Liaison d'un service à un conteneur](../../../containers/container_integrations_binding.html){: new_window}. |
| CCS_BIND_SRV=*&lt;nom_instance_service1&gt;*,*&lt;nom_instance_service2&gt;* | Pour lier un service Bluemix directement à un
conteneur sans utiliser d'application de pont, utilisez CCS_BIND_SRV. Cette liaison permet à Bluemix d'injecter les informations VCAP_SERVICES dans
l'instance de conteneur en cours d'exécution. Pour répertorier plusieurs services Bluemix, incluez-les dans la même variable d'environnement. |
| LOG_LOCATIONS=*&lt;chemin_fichier&gt;* | Ajoutez un fichier journal à surveiller dans le conteneur. Incluez la variable d'environnement `LOG_LOCATIONS` avec un chemin d'accès au fichier journal. |
{: caption="Tableau 3. Variables d'environnement couramment utilisées" caption-side="top"}


   <dl>
   <dt>--volume <i>VOLUME</i>:<i>CHEMIN_CONTENEUR</i>[:ro] (facultatif)</dt>
   <dd>Rattache un volume à un conteneur en spécifiant ses détails sous le format <i>ID_volume:Chemin_conteneur[:ro]</i>.
   <ul>
   <li><i>VOLUME</i> : ID ou nom du volume.</li>
   <li><i>CHEMIN_CONTENEUR</i> : Chemin absolu du volume dans le conteneur.</li>
   <li>ro (facultatif) : La spécification de <i>ro</i> rend le volume accessible en lecture seule, au lieu de le laisser accessible par défaut en lecture/écriture.</li></ul>
   </dd>
   <dt>-n <i>NOM</i>|--name <i>NOM</i> (requis)</dt>
   <dd>Attribue un nom au conteneur. <br> <strong>Astuce :</strong> le nom de conteneur doit commencer par une lettre. Il peut inclure des lettres majuscules, des lettres minuscules, des chiffres, des points, des traits de soulignement (_) ou des traits d'union (-).</dd>
   <dt>--link <i>NOM</i>:<i>ALIAS</i> (facultatif)</dt>
   <dd>Chaque fois que vous désirez qu'un conteneur communique avec un autre en exécution, vous pouvez le désigner en utilisant un alias pour le nom d'hôte.</dd>
   <dt>-it (facultatif)</dt>
   <dd>Indique d'exécuter le conteneur en mode interactif. Une fois le conteneur créé, l'entrée standard continue d'être affichée. Entrez <i>exit</i> pour quitter.</dd>
   <dt><i>IMAGE</i> (requis)</dt>
   <dd>Image à inclure dans le conteneur. Vous pouvez spécifier des commandes après l'image, mais n'indiquez pas d'options. Incluez toutes les options avant de spécifier une image. Incluez toutes les options avant de spécifier une image. <br><br>Si vous utilisez une image qui se trouve dans le référentiel {{site.data.keyword.Bluemix_notm}} privé de votre organisation, spécifiez l'image au format <i>registry.ng.bluemix.net/ESPACE_NOM/IMAGE</i>. <br><br>Si vous utilisez une image fournie par IBM Containers, spécifiez-la sous le format : <i>registry.ng.bluemix.net/IMAGE</i>. </dd>
   <dt><i>CMD</i> (facultatif)</dt>
   <dd>Commande et arguments transmis au groupe de conteneurs pour exécution. Cette commande doit être une commande à exécution longue. N'utilisez pas de commande à exécution courte, c'est-à-dire qui ne s'exécute pas très longtemps, comme <i>/bin/date</i>, car elle pourrait entraîner la panne du conteneur.</dd>
   </dl>


<strong>Exemples</strong> :

Exécutez la commande à exécution longue `sh -c "while true; do date; sleep 20; done"` sur le conteneur `mon_conteneur` construit sur l'image `registry.ng.bluemix.net/ibmnode`.
```
bluemix ic run --name mon_conteneur registry.ng.bluemix.net/ibmnode -- sh -c "while true; do date; sleep 20; done"
```


Créez et démarrez un conteneur `proxy` avec une limite de mémoire de `1024` Mo en utilisant l'image `mon_espace_nom/nginx`, où `mon_espace_nom` est l'espace de nom associé aux utilisateurs connectés.
```
bluemix ic run -n proxy -m 1024 registry.ng.bluemix.net/mon_espace_nom/nginx
```

Créez et démarrez un conteneur en utilisant l'image `mon_espace_nom/blog` et transmettez les données d'identification sous forme de variables d'environnement. `mon_espace_nom` est l'espace de nom associé aux utilisateurs connectés.
```
bluemix ic run -n mon_conteneur -e USER=johnsmith -e PASS=password registry.ng.bluemix.net/mon_espace_nom/blog
```

Ajoutez un volume au conteneur en utilisant l'image `mon_espace_nom/blog`, où `mon_espace_nom` est l'espace de nom associé aux utilisateurs connectés.
```
bluemix ic run -n mon_conteneur -v IDVol1:/premier/chemin -v IDVol2:/deuxième/chemin registry.ng.bluemix.net/mon_espace_nom/blog
```


## bluemix ic service-bind
{: #bluemix_ic_service-bind}

Ajoutez un service à un groupe de conteneurs en cours d'exécution. Cette commande est disponible uniquement pour les groupes de conteneurs. Les conteneurs doivent être liés à un service via la commande bluemix ic run.

```
bluemix ic service-bind NOM_GROUPE INSTANCE_SERVICE
```
<strong>Options de commande</strong> :

   <dl>
   <dt><i>NOM_GROUPE</i> (requis)</dt>
   <dd>ID ou nom du groupe.</dd>
   <dt><i>INSTANCE_SERVICE</i> (requis)</dt>
   <dd>Nom de l'instance de service qui doit être ajouté au groupe de conteneurs.</dd>
   </dl>


## bluemix ic service-unbind
{: #bluemix_ic_service-unbind}

Suppression d'un service dans un groupe de conteneurs en exécution. Cette commande est disponible uniquement pour les groupes de conteneurs. Pour les conteneurs
uniques, vous devez supprimer le conteneur et en créer un nouveau sans le service.

```
bluemix ic service-unbind NOM_GROUPE INSTANCE_SERVICE
```
<strong>Options de commande</strong> :

   <dl>
   <dt><i>NOM_GROUPE</i> (requis)</dt>
   <dd>ID ou nom du groupe.</dd>
   <dt><i>INSTANCE_SERVICE</i> (requis)</dt>
   <dd>Nom de l'instance de service qui doit être ajouté au groupe de conteneurs.</dd>
   </dl>


## bluemix ic start
{: #ic_start}
Démarrez un conteneur arrêté. Pour plus d'informations, voir la commande [start ![icône de lien externe](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/start/){: new_window} dans l'aide de Docker. Pour arrêter un conteneur, voir la commande [bluemix ic stop](#ic_stop).

```
bluemix ic start CONTENEUR
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible, Docker

<strong>Options de commande</strong> :

   <dl>
   <dt><i>CONTENEUR</i> (requis)</dt>
   <dd>Nom ou ID du conteneur.</dd>
   </dl>


<strong>Réponses</strong> :

- Started container successfully.

- Command failed with container cloud service

 `{message}`

 Où `{message}` est l'erreur connexe.

- Command failed - Could not connect to container cloud service

<strong>Exemples</strong> :

L'exemple suivant est une demande de démarrage d'un conteneur dont le nom est `proxy` :
```
bluemix ic start proxy
```


## bluemix ic stats
{: #bluemix_ic_stats}

Affichez les statistiques d'utilisation actuelles d'un ou de plusieurs conteneurs. Utilisez `CTRL+C` pour quitter. Pour plus d'informations, voir la commande [stats ![icône de lien externe](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/stats/){: new_window} dans l'aide de Docker.

```
bluemix ic stats [--no-stream] CONTENEUR [CONTENEUR]
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible, Docker

<strong>Options de commande</strong> :

   <dl>
   <dt><i>CONTENEUR</i> (requis)</dt>
   <dd>Nom ou ID du conteneur.</dd>
   <dt>--no-stream (facultatif)</dt>
   <dd>Indique d'afficher uniquement le dernier résultat, sans inclure les informations qui le précédent.</dd>
   </dl>

<strong>Exemples</strong> :

L'exemple suivant est une demande d'affichage des statistiques les plus récentes sur un conteneur :
```
bluemix ic stats --no-stream mon_conteneur
```


## bluemix ic stop
{: #ic_stop}
Arrêtez un conteneur en cours d'exécution. Pour plus d'informations, voir la commande [stop ![icône de lien externe](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/stop/){: new_window} dans l'aide de Docker. Pour démarrer un conteneur, voir la commande [bluemix ic start](#ic_start).

```
bluemix ic stop CONTENEUR [-t SECS|--time SECS]
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible, Docker

<strong>Options de commande</strong> :

   <dl>
   <dt><i>CONTENEUR</i> (requis)</dt>
   <dd>Nom ou ID du conteneur.</dd>
   <dt>-t <i>SECS</i>|--time <i>SECS</i> (facultatif)</dt>
   <dd>Nombre de secondes avant l'arrêt du conteneur.</dd>
   </dl>

<strong>Réponses</strong> :

- Stopped container successfully.

- Command failed with container cloud service

 `{message}`

 Où `{message}` est l'erreur connexe.

- Command failed - Could not connect to container cloud service

<strong>Exemples</strong> :

L'exemple suivant est une demande d'arrêt d'un conteneur dont le nom est `proxy` :
```
bluemix ic stop proxy
```


## bluemix ic top
{: #bluemix_ic_top}

Affichez les processus en cours d'exécution dans le conteneur. Pour plus d'informations, voir la commande [top ![icône de lien externe](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/top/){: new_window} dans l'aide de Docker.

```
bluemix ic top CONTENEUR [CONTENEUR]
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible, Docker

<strong>Options de commande</strong> :

   <dl>
   <dt><i>CONTENEUR</i> (requis)</dt>
   <dd>Nom ou ID du conteneur.</dd>
   </dl>

<strong>Exemples</strong> :

L'exemple suivant est une demande d'affichage des processus d'un conteneur dont le nom est `mon_conteneur`.
```
bluemix ic top mon_conteneur
```


## bluemix ic unpause
{: #unpause}

Reprenez l'exécution de tous les processus dans un conteneur en cours d'exécution. Pour plus d'informations, voir la commande [unpause ![icône de lien externe](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/unpause/){: new_window} dans l'aide de Docker. Pour interrompre un conteneur, voir la commande [bluemix ic pause](#pause).

```
bluemix ic unpause CONTENEUR
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible, Docker

<strong>Options de commande</strong> :

   <dl>
   <dt><i>CONTENEUR</i> (requis)</dt>
   <dd>Nom ou ID du conteneur.</dd>
   </dl>

<strong>Réponses</strong> :

- Unpaused container successfully.

- Command failed with container cloud service

 `{message}`

 Où `{message}` est l'erreur connexe.

- Command failed - Could not connect to container cloud service

<strong>Exemples</strong> :

L'exemple suivant est une demande de reprise d'un conteneur dont le nom est `proxy` :
```
bluemix ic unpause proxy
```


## bluemix ic unprovision
{: #bluemix_ic_unprovision}

Supprime le service IBM Containers de l'espace Bluemix auquel vous êtes connecté.

<strong>Attention</strong> : lorsque vous exécutez cette commande, tous vos conteneurs et groupes de conteneurs sont perdus. Votre espace est toujours disponible dans Bluemix. Pour recommencer à utiliser le service IBM Containers, vous devez exécuter `bluemix ic reprovision` pour remettre le service IBM
Containers à disposition.

```
bluemix ic reprovision [--force|-f]
```
<strong>Options de commande</strong> :

<dl>
   <dt>--force|-f (facultatif)</dt>
   <dd>Force la suppression de Bluemix dans l'espace Bluemix.</dd>
 </dl>


## bluemix ic version
{: #bluemix_ic_version}

Affichez la version de Docker et de l'API IBM Containers.

```
bluemix ic version
```

<strong>Prérequis</strong> : Docker

Pour identifier la version d'IBM Containers, exécutez la commande `bluemix ic info`. Pour plus d'informations, reportez-vous à la commande [version ![Icône de lien externe](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/version/){: new_window} dans l'aide de Docker.


## bluemix ic volume-create
{: #bluemix_ic_volume_create}

Créez un volume.

```
bluemix ic volume-create NOM_VOLUME NOM_PF
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :

   <dl>
   <dt><i>NOM_PF</i> (facultatif)</dt>
   <dd>Nom du partage de fichiers. Si aucun partage de fichiers n'est disponible ou indiqué, le volume sera généré sur le partage de fichiers par défaut
de l'espace.</dd>
   <dt><i>NOM_VOLUME</i> (requis)</dt>
   <dd>Nom du volume. Ce nom peut comporter des lettres en minuscules, des chiffres, des traits de soulignement (_) et des traits d'union (-).</dd>
   </dl>


<strong>Exemples</strong> :

L'exemple suivant est une demande de création d'un volume :
```
bluemix ic volume-create nom_volume nom_partage_fichiers
```


## bluemix ic volume-fs
{: #bluemix_ic_volume_fs}

Répertoriez les partages de fichiers.

```
bluemix ic volume-fs
```


## bluemix ic volume-fs-create
{: #bluemix_ic_volume_fs_create}

Crée un partage de fichiers.

```
bluemix ic volume-fs-create NOM_PARTAGE_FICHIERS
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :

   <dl>
   <dt><i>NOM_PARTAGE_FICHIERS</i> (requis)</dt>
   <dd>Nom du partage de fichiers. Ce nom peut comporter des lettres en minuscules, des chiffres, des traits de soulignement (_) et des traits d'union (-).</dd>
   </dl>

<strong>Exemples</strong> :

L'exemple suivant illustre une demande de création d'un partage de fichiers.
```
bluemix ic volume-fs-create mon_partage_fichiers
```


## bluemix ic volume-fs-flavors
{: #bluemix_ic_volume_fs_flavors}

Répertorie toutes les versions de partage de fichiers.

```
bluemix ic volume-fs-flavors
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible


## bluemix ic volume-fs-inspect
{: #bluemix_ic_volume_fs_inspect}

Inspectez un partage de fichiers.

```
bluemix ic volume-fs-inspect NOM_PARTAGE_FICHIERS
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :

  <dl>
  <dt><i>NOM_PARTAGE_FICHIERS</i> (requis)</dt>
   <dd>Nom du partage de fichiers.</dd>
   </dl>

<strong>Exemples</strong> :

L'exemple ci-dessous illustre une demande d'inspection d'un partage de fichiers, où `mon_partage_fichiers` est le nom du partage de
fichiers.
```
bluemix ic volume-fs-inspect mon_partage_fichiers
```


## bluemix ic volume-fs-remove
{: #bluemix_ic_volume_fs_remove}

Supprime un partage de fichiers.

```
bluemix ic volume-fs-remove NOM_PARTAGE_FICHIERS
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :

   <dl>
   <dt><i>NOM_PARTAGE_FICHIERS</i> (requis)</dt>
   <dd>Nom du partage de fichiers.</dd>
   </dl>

<strong>Exemples</strong> :

L'exemple ci-dessous illustre une demande de retrait d'un partage de fichiers, où `mon_partage_fichiers` est le nom du partage
de
fichiers.
```
bluemix ic volume-fs-remove mon_partage_fichiers
```


## bluemix ic volume-inspect
{: #bluemix_ic_volume_inspect}

Inspectez un volume.

```
bluemix ic volume-inspect NOM_VOLUME
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :

   <dl>
   <dt><i>NOM_VOLUME</i> (requis)</dt>
   <dd>Nom du volume.</dd>
   </dl>

<strong>Exemples</strong> :

L'exemple suivant est une demande d'inspection d'un volume, où `nom_volume` est le nom du volume :
```
bluemix ic volume-inspect nom_volume
```


## bluemix ic volume-remove
{: #bluemix_ic_volume_remove}

Retirez un volume.

```
bluemix ic volume-remove NOM_VOLUME
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :

   <dl>
   <dt><i>NOM_VOLUME</i> (requis)</dt>
   <dd>Nom du volume.</dd>
    </dl>

<strong>Exemples</strong> :

L'exemple suivant est une demande de retrait d'un volume, où `nom_volume` est le nom du volume :
```
bluemix ic volume-remove nom_volume
```


## bluemix ic volumes
{: #bluemix_ic_volumes}

Répertoriez les volumes.

```
bluemix ic volumes
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible


## bluemix ic wait
{: #bluemix_ic_wait}

Quittez un conteneur et affichez le code de sortie comme confirmation. Pour plus d'informations, voir la commande [wait ![icône de lien externe](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/wait/){: new_window} dans l'aide de Docker.

```
bluemix ic wait CONTENEUR [CONTENEUR]
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible, Docker

<strong>Options de commande</strong> :

   <dl>
   <dt><i>CONTENEUR</i> (requis)</dt>
   <dd>Nom ou ID du conteneur.</dd>
   </dl>

<strong>Exemples</strong> :

L'exemple suivant est une demande de sortie d'un conteneur dont le nom est `mon_conteneur` :
```
bluemix ic wait mon_conteneur
```


## bluemix ic wait-status
{: #bluemix_ic_wait_status}

Indique d'attendre qu'un conteneur unique ou un groupe de conteneurs passe à un état non transitoire. Pendant cette attente, la ligne de commande ne renvoie pas de résultat et vous ne pouvez pas entrer de
commandes. Dès que le conteneur passe à un état non transitoire, un message OK s'affiche. Pour les conteneurs uniques, les états non transitoires sont notamment les suivants : En cours d'exécution, Arrêt, En panne, En pause ou Suspendu. Pour les groupes de conteneurs, les états non transitoires sont notamment les suivants : CREATE_COMPLETE, UPDATE_COMPLETE ou FAILED

```
bluemix ic wait-status CONTENEUR
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible, Docker

<strong>Options de commande</strong> :

   <dl>
   <dt><i>CONTENEUR</i> (requis)</dt>
   <dd>Nom ou ID du conteneur.</dd>
   </dl>

<strong>Exemples</strong> :

L'exemple suivant est une demande de sortie d'un conteneur dont le nom est `mon_conteneur` :
```
bluemix ic wait mon_conteneur
```
