---

 

copyright:

  2015，2016

 

---

{:shortdesc: .shortdesc} 
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#Hébergement d'applications dans {{site.data.keyword.Bluemix_notm}}

*Dernière mise à jour : 9 mai 2016*

<!--The whole topic is staging only -->

Avec {{site.data.keyword.Bluemix}}, vous pouvez créer des applications et héberger vos
applications existantes. Vous pouvez migrer vos applications dans {{site.data.keyword.Bluemix_notm}} à condition
qu'elles soient prêtes pour le cloud. {{site.data.keyword.Bluemix_notm}} vous propose plusieurs manières d'exécuter vos applications, par exemple avec Cloud Foundry, IBM Containers et
Virtual Machines.

##Rendre vos applications prêtes pour le cloud
{: #cloud-readyapps}

Pour qu'une application soit prête pour le cloud, vous devez respecter les principes de la plateforme de cloud lors de la conception et de la
construction de l'application. Une application prête pour le cloud peut utiliser les capacités mises à disposition par la plateforme de cloud.

Si tous les principes ci-après sont respectés dans votre application, l'application est prête pour le cloud et peut être migrée dans
{{site.data.keyword.Bluemix_notm}}. Si un principe n'est pas appliqué dans votre application, vous pouvez généralement modifier votre application pour qu'elle le respecte.

* Ne codez pas votre application directement dans une topologie spécifique.

  Dans un environnement autre qu'un environnement de cloud, l'application
peut utiliser une topologie de déploiement particulière. Cependant, la topologie de l'application peut changer dans les applications en cloud, car les
applications et les services prêts pour le cloud autorisent des modifications immédiates à des fins d'évolutivité. Ces modifications incluent la mise à l'échelle dynamique et le redimensionnement manuel du nombre d'instances d'une application.

  Construisez votre application de sorte qu'elle soit aussi générique et sans état que possible pour éviter qu'elle ne soit affectée par les
modifications à des fins d'évolutivité.

* Ne partez pas du principe que le système de fichiers est permanent.

  Etant donné qu'une application peut être déplacée, supprimée ou dupliquée à tout
moment dans le cloud, ne vous appuyez pas sur les fichiers qui se trouvent dans le système de fichiers. Si une application utilise le système de fichiers local comme cache pour les informations utilisées fréquemment, notamment les journaux d'application, les
informations sont perdues lorsque l'instance est arrêtée et redémarrée à un autre emplacement ou sur une machine virtuelle différente.

  Vous pouvez stocker les informations dans un service, par exemple une base de données SQL ou NoSQL, au lieu de les stocker dans le système de
fichiers local. Dans un environnement de cloud dynamique, il est également essentiel que vos journaux soient disponibles dans un service qui survit aux
instances d'application dans lesquelles les journaux sont générés.

* Ne stockez pas l'état de session dans votre application.

  L'état de votre système est défini par vos bases de données et votre espace de stockage
partagé, et non par chaque instance d'application en cours d'exécution. L'état, quel qu'il soit, limite l'évolutivité d'une application. Essayez de réduire l'impact de l'état de session en le stockant à un emplacement centralisé
sur le serveur.

  Si vous ne pouvez pas éliminer l'état de session entièrement, envoyez-le dans un magasin hautement disponible externe à votre serveur
d'applications, par exemple IBM WebSphere Extreme Scale, Redis ou Memcached, ou une base de données externe.

* N'utilisez pas de dépendance d'infrastructure spécifique.

  Il s'agit d'un principe général qui se traduit sous différentes formes. Par exemple, ne partez pas du
principe que les services que votre application utilise sont associés à des noms d'hôte ou des adresses IP spécifiques. Etant donné que l'emplacement des services peut changer ou que les services peuvent être régénérés dans votre environnement de cloud, les noms d'hôte
et les
adresses IP peuvent également changer.

  L'extraction de dépendances propres à l'environnement dans un ensemble de fichiers de propriétés
constitue une amélioration, mais reste inadaptée. Il est préférable d'utiliser un registre de services externe pour résoudre les noeuds finaux des services
ou de déléguer la fonction de routage complète à un bus de services ou à un équilibreur de charge avec un nom virtuel.

* N'utilisez pas d'API d'infrastructure dans votre application.

  Si vous vous appuyez sur une API d'infrastructure spécifique dans votre application, il
est plus complexe de changer l'infrastructure, car une API d'infrastructure peut faire référence à de nombreuses couches différentes dans votre pile de
logiciels.

  A la place, vous pouvez vous appuyer sur des produits commerciaux ou open source existants, et laisser les solutions PaaS (plateforme sous forme de
services) dans la couche PaaS afin de ne pas les intégrer à votre code d'application.

* N'utilisez pas de protocoles opaques.

  N'utilisez pas de protocoles opaques requérant des étapes de configuration supplémentaires afin d'assurer la
résilience.

  Les applications reposant sur des protocoles standard sont plus résilientes avec les éléments de configuration délégués à la plateforme. Les protocoles standard sont HTTP, SSL, la base de données standard, la mise en file d'attente et les connexions de service Web.

* Ne vous appuyez pas sur des fonctions propres au système d'exploitation.

  Si vous avez déjà utilisé des fonctions propres au système
d'exploitation, vous pouvez résoudre le problème en utilisant des bibliothèques de compatibilité, par exemple Cygwin et Mono. Cygwin est une bibliothèque
de compatibilité qui fournit un ensemble d'outils Linux dans un environnement Windows. Mono est une bibliothèque de compatibilité qui fournit des capacités Windows .NET dans Linux.

  Evitez les dépendances propres au
système d'exploitation ; à la place, utilisez des services mis à disposition par l'infrastructure de middleware ou les fournisseurs de services.

* N'installez pas manuellement votre application.

  Votre application doit être installée fréquemment à la demande dans l'environnement de cloud
dynamique. Le processus d'installation doit être scripté et fiable, et les données de configuration doivent être externalisées à partir des scripts.

  Au minimum, capturez votre installation d'application sous forme d'ensemble uniforme de scripts indépendants du système d'exploitation. Veillez à ce que l'installation d'application reste petite et portable pour qu'elle puisse s'adapter à différentes techniques d'automatisation. De plus, limitez les dépendances requises par l'installation d'application.

Pour plus d'informations sur les applications prêtes pour le cloud, voir [The
Twelve-Factor App](http://12factor.net/){:new_window}.

##Migration de vos applications
{: #ht_hostapp}

Vous pouvez migrer vos applications dans {{site.data.keyword.Bluemix_notm}} de manière incrémentielle
au lieu de les envoyer intégralement dans l'environnement de cloud. Vous pouvez d'abord migrer une partie de votre application, puis vous connecter aux
données ou au système d'enregistrement qui existent à l'aide du service Cloud Integration.

Dans vos applications en cloud, il peut être nécessaire d'accéder aux données ou aux services de back end, par exemple un système d'enregistrement. Dans {{site.data.keyword.Bluemix_notm}}, vous pouvez utiliser le service Secure Gateway afin d'établir un tunnel
sécurisé entre une organisation {{site.data.keyword.Bluemix_notm}} et le réseau de back end de l'entreprise. Le service permet aux applications dans {{site.data.keyword.Bluemix_notm}} d'accéder aux données et aux services
du réseau de back end. Pour des détails, voir [Reaching enterprise backend with Bluemix Secure Gateway via console](https://developer.ibm.com/bluemix/2015/04/01/reaching-enterprise-backend-bluemix-secure-gateway/){:new_window}.

Pour déployer votre application dans {{site.data.keyword.Bluemix_notm}} en tant qu'application Cloud Foundry,
sélectionnez un contexte d'exécution dans le catalogue {{site.data.keyword.Bluemix_notm}}. Le contexte d'exécution contient une application Hello
World de démarrage que vous pouvez remplacer par votre propre application. Si vous ne trouvez pas de module de démarrage fournissant le contexte
d'exécution que vous recherchez, vous pouvez apporter un pack de construction personnalisé compatible avec Cloud Foundry dans {{site.data.keyword.Bluemix_notm}} en spécifiant l'option -b
dans la commande cf push. Pour des détails, voir [Utilisation de packs de construction de communauté](../cfapps/byob.html).

Vous pouvez utiliser les outils et les services suivants mis à disposition par
{{site.data.keyword.Bluemix_notm}} :

*Tableau 1. Outils {{site.data.keyword.Bluemix_notm}}*

| Outil	| Méthode |
|:------|:--------|
|Interface de ligne de commande Cloud Foundry (cf cli)	|Gérez votre code sur le client local et utilisez l'interface de ligne de commande Cloud Foundry pour envoyer votre application par
commande push dans {{site.data.keyword.Bluemix_notm}} manuellement. Pour plus d'informations, voir [Téléchargement de votre application](../starters/upload_app.html).|
|Eclipse	|Gérez votre code dans Eclipse et utilisez IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} pour envoyer votre application par commande push.|
|intégration Git	|Gérez votre code sur GitHub et intégrez Git dans {{site.data.keyword.Bluemix_notm}}. Vous pouvez collaborer avec d'autres développeurs. Votre application est déployée dans
{{site.data.keyword.Bluemix_notm}} automatiquement lorsque vous validez les modifications dans le code. Il n'est
pas nécessaire d'envoyer manuellement l'application par commande push.|
|{{site.data.keyword.Bluemix_notm}} DevOps
Delivery Pipeline	|Gérez votre code dans le référentiel DevOps GitHub et déployez votre application dans
{{site.data.keyword.Bluemix_notm}} à l'aide de DevOps Delivery Pipeline.|


Si la plateforme Cloud Foundry ne prend pas en charge les exigences relatives à votre application, vous pouvez utiliser un conteneur ou une machine
virtuelle où le contexte d'exécution est défini, configuré et géré avec des options personnalisées supplémentaires.

##Téléchargement de votre applications avec cf cli
{: #ht_cfcli}

Vous pouvez gérer votre code sur le client local et utiliser l'interface de ligne de commande Cloud
Foundry afin de télécharger votre application dans {{site.data.keyword.Bluemix_notm}} manuellement. Si vous
changez votre code, vous devez à nouveau envoyer votre application par commande push dans
{{site.data.keyword.Bluemix_notm}} afin d'exécuter le code mis à jour.

Procédez comme suit pour migrer votre application :

<ol>
<li>Installez l'interface de ligne de commande Cloud Foundry. Veillez à utiliser la version la plus récente de l'interface de ligne de commande cf.
<ol>
<li>Téléchargez le programme d'installation pour votre système d'exploitation.</li>
<li>Suivez l'assistant de l'outil pour installer la ligne de commande.</li>
<li>Utilisez la commande suivante pour vérifier la version de l'interface de ligne de commande cf :
<pre>cf -v</pre></li>
</ol>
</li>

<li>Facultatif : si vous voulez spécifier et sauvegarder les détails du déploiement avant d'envoyer une application par commande push dans
{{site.data.keyword.Bluemix_notm}}, vous pouvez ajouter le manifeste d'application en procédant comme suit :
<ol>
<li>Accédez au répertoire de travail de votre application et créez un fichier dont le nom est manifest.yml par défaut.</li>
<li>Spécifiez les détails du déploiement dans le fichier manifeste. L'exemple ci-dessous est une illustration d'un fichier manifeste pour une application
Java..
<pre class="pre codeblock"><code>applications:
- disk_quota: 1024M
  host: myjavatest
  name: MyJavaTest
  path: webStarterApp.war
  domain: mybluemix.net
  instances: 1
  memory: 512M</code></pre>
<p>Pour plus d'informations sur les options prises en charge que vous pouvez utiliser dans ce fichier, voir [Manifeste d'application](../manageapps/depapps.html#appmanifest).

</p></li></ol>
</li>

<li>Envoyez votre application par commande push. Vous pouvez télécharger votre application avec la commande cf push.
<ol>
<li>Connectez-vous à {{site.data.keyword.Bluemix_notm}} avec la commande ci-après. Sélectionnez
votre organisation et votre espace lorsque vous y êtes invité.
<pre>cf login -a https://api.ng.bluemix.net</pre></li>
<li>Depuis le répertoire de votre application, entrez la commande cf push avec le nom de l'application. Le nom de l'application doit être unique dans
l'environnement {{site.data.keyword.Bluemix_notm}}.
<pre>cf push nom_app</pre></li>
<li>Facultatif : si vous utilisez un pack de construction externe, vous devez utiliser l'option -b avec la commande cf push. Exemple :
<pre>cf push nom_app -b URL_pack_construction</pre>
<p>Voir Utilisation de packs de construction de communauté pour des détails.</p>
</li></ol>
</li>

<li>Facultatif : si vous modifiez votre application, vous devez télécharger les modifications en entrant à nouveau la commande cf push. L'interface de ligne de
commande cf utilise vos options précédentes et vos réponses aux invites pour mettre à jour n'importe quelle instance en cours d'exécution de votre application avec
les nouvelles parties de code.</li>
</ol>

**Remarques :**

* Lorsque vous utilisez la commande cf push, l'interface de ligne de commande cf copie tous les fichiers et tous les répertoires du répertoire de
travail dans {{site.data.keyword.Bluemix_notm}}. Assurez-vous que votre répertoire de travail contient uniquement les fichiers requis.
* Assurez-vous que votre organisation dispose de suffisamment de mémoire pour toutes les instances de votre application. Afin d'afficher le quota de
mémoire de votre organisation, utilisez cf org nom_organisation.
* Pour plus d'informations sur cf push, voir [Commandes cf](../cli/reference/cfcommands/index.html).

##Migration de vos données et utilisation des services
{: #ht_service}

Après avoir téléchargé votre application dans
{{site.data.keyword.Bluemix_notm}}, sélectionnez le service auquel votre application est connectée dans le
catalogue {{site.data.keyword.Bluemix_notm}}, créez une instance de service, liez l'instance à votre
application, puis redémarrez votre application.

La variable d'environnement VCAP_SERVICES de votre application est un objet JSON qui contient des informations sur la façon d'interagir avec une
instance de service dans {{site.data.keyword.Bluemix_notm}}. Les informations incluent le nom de l'instance de service, les données d'identification et l'adresse URL de connexion à l'instance de service.

Pour exécuter votre code dans {{site.data.keyword.Bluemix_notm}}, vous devez ajouter la logique de code pour
l'analyse syntaxique de la variable VCAP_SERVICES afin d'obtenir des informations sur la connexion au service. Modifiez votre application pour obtenir
l'hôte et le port affectés dynamiquement de l'instance de service par le biais des variables d'environnement. L'exemple suivant montre comment obtenir les
données d'identification d'une instance de service Postgre SQL dans une application Ruby :

```
services = JSON.parse(ENV['VCAP_SERVICES'], :symbolize_names => true)
        url = services.values.map do |srvs|
          srvs.map do |srv|
            if srv[:credentials][:uri] =~ /^postgres/
              srv[:credentials][:uri]
            else
              []
            end
          end
        end.flatten!.first
```		
{:codeblock}

Pour garantir l'exécution de votre application dans un environnement local après sa modification pour
{{site.data.keyword.Bluemix_notm}}, vérifiez la présence de la variable d'environnement
VCAP_SERVICES, qui est définie pour toutes les applications {{site.data.keyword.Bluemix_notm}} Cloud
Foundry.


# Liens connexes
{: #rellinks}

## Liens connexes
{: #general}

* [IBM Containers](../containers/container_cli_ov.html)
* [Virtual Machines](../virtualmachines/vm_index.html)
* [Initiation à Delivery Pipeline](../services/DeliveryPipeline/index.html)
* [Déploiement d'applications avec IBM Eclipse Tools for Bluemix](../manageapps/eclipsetools/eclipsetools.html)
* [The Twelve-Factor App](http://12factor.net/){:new_window}
* [Reaching enterprise backend with Bluemix Secure Gateway via console](https://developer.ibm.com/bluemix/2015/04/01/reaching-enterprise-backend-bluemix-secure-gateway/){:new_window}
