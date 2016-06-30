---

copyright:
  years: 2015, 2016

---


{:shortdesc: .shortdesc} 
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#Surveillance et journalisation
{: #monitoringandlogging}

*Dernière mise à jour : 24 mai 2016*
{: .last-updated}

En surveillant vos applications et en consultant les journaux, vous pouvez suivre l'exécution des applications et le flux de données afin de mieux
comprendre votre déploiement. De plus, vous pouvez réduire le temps et l'effort qui sont requis pour identifier les problèmes et les résoudre.
{:shortdesc}

Les applications {{site.data.keyword.Bluemix}} peuvent être des applications à plusieurs instances distribuées à grande échelle et
l'exécution de votre application et de ses données peut être partagée entre plusieurs services. Dans cet environnement complexe, la surveillance de vos
applications et la consultation des journaux sont essentielles pour la gestion de vos applications.

##Surveillance et journalisation d'applications
{: #monitoring_logging_bluemix_apps}

{{site.data.keyword.Bluemix_notm}} intègre un mécanisme de journalisation qui génère des fichiers journaux pour vos applications, au cours de
leur exécution. Ces journaux comportent les erreurs, les avertissements et les messages d'information qui sont générés pour votre application. De plus,
vous pouvez également configurer votre application pour qu'elle écrive des messages de journal dans le fichier journal. Pour plus d'informations sur les formats des
journaux et sur leur affichage, voir [Journalisation pour les applications qui s'exécutent dans Cloud Foundry](#logging_for_bluemix_apps).

La surveillance de votre application vous permet d'afficher et de contrôler son déploiement. Elle permet d'effectuer les tâches
suivantes :

* Collecter et surveiller les informations sur les performances pour les instances d'application et vérifier si elles sont opérationnelles.
* En savoir plus sur le fonctionnement de l'application, par exemple détecter les goulots d'étranglement potentiels ou déterminer la
nécessité d'une mise à niveau.
* Estimer l'utilisation des ressources et les coûts.

Pour un fonctionnement stable de vos déploiements sur la plateforme {{site.data.keyword.Bluemix_notm}}, vous devez détecter les problèmes
rapidement et identifier les causes efficacement. Pour ce faire, gardez l'aspect traitement des incidents à l'esprit lorsque vous concevez vos applications
et utilisez des services ou des outils de surveillance et de journalisation lorsque votre application est déployée dans {{site.data.keyword.Bluemix_notm}}.

###Surveillance des applications qui s'exécutent dans Cloud Foundry
{: #monitoring_bluemix_apps}

Lorsque vous utilisez l'infrastructure Cloud Foundry pour exécuter vos applications dans {{site.data.keyword.Bluemix_notm}}, il est
souhaitable d'avoir connaissance des informations sur les performances, telles que l'état de santé, l'utilisation des ressources et les mesures du trafic. Elles
vous permettent de prendre des décisions ou des mesures en conséquence.

Pour surveiller des applications {{site.data.keyword.Bluemix_notm}}, appliquez l'une des méthodes suivantes :

* Services {{site.data.keyword.Bluemix_notm}}. Monitoring and Analytics propose un service que vous pouvez utiliser pour surveiller les
performances de votre application. De plus, ce service fournit également des fonctions d'analyse telles que l'analyse de journal. Pour plus d'informations, voir [Monitoring and Analytics](../services/monana/index.html).
* Options de tiers. Exemple : [New Relic](http://newrelic.com/){:new_window}.

###Journalisation pour les applications qui s'exécutent dans Cloud Foundry
{: #logging_for_bluemix_apps}

Des fichiers journaux sont créés automatiquement lorsque vous utilisez l'infrastructure Cloud
Foundry pour exécuter vos applications dans {{site.data.keyword.Bluemix_notm}}. Si vous rencontrez des erreurs au cours d'une étape entre le
déploiement et l'exécution, vous pouvez consulter les journaux pour déterminer comment résoudre le problème.

<!-- 2016.1.27: original shortdes: Log files are automatically created when you are using the Cloud Foundry infrastructure to run your apps on {{site.data.keyword.Bluemix_notm}}. You can view logs from the {{site.data.keyword.Bluemix_notm}} Dashboard, the cf command line interface, or external hosts. You can also filter the logs to see the parts that you are interested in. -->



###Format de journal
{: #log_format}

Les journaux pour les applications {{site.data.keyword.Bluemix_notm}} sont affichés dans un format fixe similaire au modèle suivant :

```
         1         2         3         4         5
12345678901234567890123456789012345678901234567890
--------------------------------------------------
aaaa-MM-jjTHH:mm:ss:SS-0500 [App/0]      OUT <message>
```
{:screen}

Chaque entrée de journal contient quatre zones. Reportez-vous à la liste suivante pour une description courte de chaque zone :

<dl>
<dt><strong>Horodatage</strong></dt>
<dd>
<pre class="pre screen"><code>aaaa-MM-jjTHH:mm:ss:SS-0500</code></pre>
<p>Colonnes : 1 à 27</p>
<p>Date et heure de l'instruction de journal. L'horodatage est défini à la milliseconde près.</p>
</dd>

<dt><strong>Composant</strong></dt>
<dd>
<pre class="pre screen"><code>[App/0]</code></pre>
<p>Colonnes : 29 à 40</p>
<p>Composant qui génère les journaux. La liste suivante donne la définition de tous les composants :</p>

<dl>
<dt><strong>APP</strong></dt>
<dd>Application. Le composant APP est suivi d'une barre oblique et d'un chiffre qui indique l'instance d'application. 0 est la première instance, 1 est la
deuxième instance, etc.</dd>

<dt><strong>interface API</strong></dt>
<dd>API Cloud Foundry.</dd>

<dt><strong>DEA</strong></dt>
<dd>Agent DEA (Droplet Execution Agent).</dd>

<dt><strong>LGR</strong></dt>
<dd>Loggregator.</dd>

<dt><strong>RTR</strong></dt>
<dd>Routeur.</dd>

<dt><strong>STG</strong></dt>
<dd>Constitution.</dd>
</dl>
</dd>

<dt><strong>Flux</strong></dt>
<dd>
<pre class="pre screen"><code>OUT</code></pre>
<p>Colonnes : 42 à 44</p>
<p>Flux dans lequel le message de journal est écrit. <samp class="ph codeph">OUT</samp> désigne le flux <samp class="ph codeph">stdout</samp> et
<samp class="ph codeph">ERR</samp> désigne le flux <samp class="ph codeph">stderr</samp>.</p>
</dd>

<dt><strong>Message</strong></dt>
<dd>
<pre class="pre screen"><code>&lt;<var class="keyword varname">Message</var>&gt;</code></pre>
<p>Colonnes : 46 à fin de ligne</p>
<p>Message émis par le composant. Il varie selon le contexte.</p>
</dd>

</dl>

###Affichage des journaux
{: #viewing_logs}

Vous pouvez afficher les journaux pour vos applications Cloud Foundry à trois endroits :

  * [Dans le tableau de bord {{site.data.keyword.Bluemix_notm}}](#viewing_logs_UI){:new_window}
  * [Dans l'interface de ligne de commande](#viewing_logs_cli){:new_window}
  * [Sur des hôtes de journaux externes](#thirdparty_logging){:new_window}

#### Affichage des journaux dans le tableau de bord {{site.data.keyword.Bluemix_notm}}
{: #viewing_logs_UI}

Pour afficher les journaux de déploiement ou d'exécution, procédez comme suit :
1. Connectez-vous à {{site.data.keyword.Bluemix_notm}}, puis cliquez sur la vignette de votre application dans le tableau de bord. La page des détails de l'application s'ouvre.
2. Dans la barre de navigation de gauche, cliquez sur **Journaux**.

Dans la console **Journaux**, vous pouvez afficher les journaux récents pour votre application ou afficher les dernières lignes des
journaux en temps réel. De plus, vous pouvez filtrer les journaux par type et canal.

**Remarque :** les journaux ne sont pas conservés en cas de panne ou après un déploiement d'application.



#### Affichage des journaux dans l'interface de ligne de commande
{: #viewing_logs_cli}

Choisissez l'une des options suivantes pour afficher les journaux depuis l'interface de ligne de commande :

<ul>
<li>Affichage des dernières lignes des journaux lorsque vous déployez des applications.
<p>Utilisez la commande **cf logs** pour afficher les journaux de votre application et des composants système qui interagissent
avec votre application lorsque vous déployez des applications dans {{site.data.keyword.Bluemix_notm}}. Vous pouvez entrer les commandes
ci-dessous dans l'interface de ligne de commande cf. Pour plus d'informations sur les journaux cf, voir
<a href="http://docs.cloudfoundry.org/devguide/deploy-apps/streaming-logs.html" target="_blank">Log Types and Their Messages dans la documentation Cloud
Foundry</a>. </p>
<dl>
<dt><strong>cf logs <var class="keyword varname">nom_app</var> --recent</strong></dt>
<dd>Affichez les journaux récents.</dd>

<dt><strong>cf logs <var class="keyword varname">nom_app</var></strong></dt>
<dd>Affichez les journaux qui sont générés à partir du moment ou vous exécutez cette commande.</dd>
</dl>
<div class="note tip"><span class="tiptitle">Astuce :</span> lorsque vous exécutez la commande <span class="keyword cmdname">cf push</span> ou
<span class="keyword cmdname">cf start</span> dans une seule fenêtre de ligne de commande, vous pouvez entrer <samp class="ph codeph">cf logs nom_app
--recent</samp> dans une autre fenêtre de ligne de commande pour afficher les journaux en temps réel. </div>
</li>

<li>Affichage des journaux après le déploiement des applications.

<p>Lorsque la journalisation des applications est activée, vous pouvez afficher les journaux d'application ci-après si vous rencontrez des problèmes liés
à votre application à l'exécution. Les journaux d'application peuvent permettre de déterminer la cause de l'erreur.</p>

<dl><strong>buildpack.log</strong></dt>
<dd>
<p>Ce fichier journal enregistre des événements d'information à granularité fine pour le débogage. Vous pouvez l'utiliser pour identifier les problèmes liés à l'exécution du pack de construction.</p>
<p>Pour générer des données dans le fichier <span class="ph filepath">buildpack.log</span>, vous devez activer la fonction de trace du pack de construction
avec la commande suivante :
   <pre class="pre">cf set-env <var class="keyword varname">nom_app</var> JBP_LOG_LEVEL DEBUG</pre>
<p>
<p>Pour afficher ce journal, entrez la commande suivante :
<pre class="pre">cf files <var class="keyword varname">nom_app</var> app/.buildpack-diagnostics/buildpack.log</pre>
</p>
</dd>

<dt><strong>staging_task.log</strong></dt>
<dd><p>Ce fichier journal enregistre des messages après les étapes principales de la tâche de constitution. Vous pouvez l'utiliser pour
identifier les problèmes liés à la constitution.</p>
<p>Pour afficher ce journal, entrez la commande suivante :
<pre class="pre">cf files <var class="keyword varname">nom_app</var> logs/staging_task.log</pre>
</p>
</dd>
</dl>
</li></ul>


**Remarque :** pour des informations sur l'activation de la journalisation des applications, voir [Débogage d'erreurs d'exécution](../debug/index.html#debugging-runtime-errors).




###Filtrage des journaux
{: #filtering_logs}

Pour afficher les journaux qui vous intéressent ou exclure le contenu que vous ne voulez pas afficher, vous pouvez utiliser la commande **cf
logs** avec des options de filtrage telles que **cut** et **grep** dans l'interface de ligne de commande
cf.

* Pour afficher une partie des journaux à la place des journaux prolixes complets, utilisez l'option **cut**. Par exemple, pour
afficher les informations de composant et de message, utilisez la commande suivante :
```
cf logs nom_app --recent | cut -c 29-40,46- 
```

Pour plus d'informations sur l'option **grep**, entrez cut --help.
* Pour afficher les entrées de journal qui contiennent certains mots clés, utilisez l'option **grep**. Par exemple, pour afficher
les entrées de journal contenant le mot clé [APP, vous pouvez utiliser la commande suivante :
```
cf logs nom_app --recent | grep '\[App'
```
Pour plus d'informations sur l'option **grep**, entrez `grep --help`.



### Configuration d'hôtes de journaux externes
{: #thirdparty_logging}

{{site.data.keyword.Bluemix_notm}} conserve une quantité limitée d'informations de
journal en mémoire. Lorsque des informations sont journalisées, les anciennes informations sont remplacées par les informations plus récentes. Pour
conserver toutes les informations de journal, vous pouvez sauvegarder vos journaux sur un hôte de journaux externe, par exemple dans un service de gestion des
journaux tiers ou sur un autre hôte.

Pour transférer les journaux de votre application et du système vers un hôte de journaux externe, procédez comme suit :

  1. Déterminez le noeud final de journalisation. 
     
	 Vous pouvez envoyer des journaux à un regroupeur de journaux tiers, comme Papertrail,
Splunk ou Sumologic. Vous pouvez aussi envoyer des journaux à un hôte syslog, un hôte syslog chiffré avec TLS (Transport Layer Security) ou un noeud final
HTTPS POST. Les méthodes d'obtention de noeuds finaux de journalisation varient selon l'hôte de journaux.

  2. Créez une instance de service fournie par l'utilisateur.
     
	 Utilisez la commande ```cf create-user-provided-service``` (ou la version courte de la commande, ```cups``) pour
créer une instance de service fournie par l'utilisateur : 
	 ```
	 cf create-user-provided-service <nom_service> -l <noeud_final_journalisation>
	 ```
	 **nom_service**
	 
	 Nom de l'instance de service fournie par l'utilisateur.
	 
	 **noeud_final_journalisation**
	 
	 Noeud final de journalisation auquel {{site.data.keyword.Bluemix_notm}} envoie des journaux. Reportez-vous au tableau suivant pour
remplacer *noeud_final_journalisation* par la valeur appropriée :
	 
	 <table>
     <thead>
     <tr>
     <th>Noeud final de journalisation</th>
     <th>Commande</th>
	 <th>Remarques</th>
     </tr>
     </thead>
     <tbody>
     <tr>
     <td>hôte syslog</td>
     <td>`cf cups my-logs -l syslog://HOTE:PORT`</td>
	 <td>Par exemple, pour activer la journalisation dans Papertrail, entrez `cf cups my-logs -l
syslog://<url_papertrail>`. Remplacez `<url_papertrail>` par l'adresse URL de votre noeud final de journalisation
pour Papertrail.</td>
     </tr>
	 <tr>
     <td>hôte syslog-tls</td>
     <td>`cf cups my-logs -l syslog-tls://HOTE:PORT`</td>
	 <td>Le certificat doit être considéré comme digne de confiance par une autorité de certification. N'utilisez pas de certificat autosigné.</td>
     </tr>
	 <tr>
     <td>HTTPS POST</td>
     <td>`cf cups my-logs -l https://HOTE:PORT`</td>
	 <td>Ce noeud final doit se trouver sur l'Internet public et {{site.data.keyword.Bluemix_notm}} doit pouvoir y accéder.</td>
     </tr>
     </tbody>
     </table>	
  3. Liez l'instance de service à votre application.

	 Utilisez la commande suivante pour lier l'instance de service à votre application : 
	
	 ```
	 cf bind-service nom_app <nom_service>
	 ```
	 **nom_app**
	 
	 Nom de votre application.
	 
	 **nom_service**
	 
	 Nom de l'instance de service fournie par l'utilisateur.
	 
  4. Reconstituez l'application. 
     Entrez ```cf restage nom_app``` pour que les modifications soient appliquées. 

#### Affichage des journaux à partir d'hôtes externes
{: #viewing_logs_external}

	 
Lorsque des journaux sont générés, vous pouvez consulter les messages après un bref délai sur votre hôte de journaux externe. Ceux-ci sont similaires
aux messages que vous pouvez afficher dans l'interface utilisateur de {{site.data.keyword.Bluemix_notm}} ou dans l'interface de ligne de commande
cf.  S'il existe plusieurs instances de votre application, les journaux sont regroupés et vous pouvez tous les afficher. De plus, ils sont conservés en cas
de panne et après un déploiement.

**Remarque :** les journaux que vous affichez dans l'interface de ligne de commande ne sont pas au format syslog et il se peut
qu'ils ne correspondent pas exactement aux messages qui sont affichés sur votre hôte de journaux externe. 

### Exemple : transmission des journaux d'application Cloud Foundry à Splunk 
{: #splunk}

Dans cet exemple, un développeur nommé Jane crée un serveur virtuel à l'aide d'IBM Virtual Servers Beta et de l'image Ubuntu. Jane tente de transmettre
les journaux d'application Cloud Foundry de {{site.data.keyword.Bluemix_notm}} à Splunk. 

  1. Pour commencer, Jane configure Splunk.

     a. Jane télécharge Splunk Light depuis le site [Download Splunk
Light](https://www.splunk.com/en_us/download/splunk-light.html){:new_window}, puis l'installe via la commande suivante. Le logiciel est installé sous /opt/splunk. 
       
	    ```
        dpkg -i  ~/splunklight-6.3.0-aa7d4b1ccb80-linux-2.6-amd64.deb
        ```
	   
     b. Jane installe et adjoint le module complémentaire RFC5424 de la technologie syslog pour son intégration avec
{{site.data.keyword.Bluemix_notm}}. Pour les instructions d'installation du module complémentaire, reportez-vous au document
[Cloud Foundry guideline](https://docs.cloudfoundry.org/devguide/services/integrate-splunk.html){:new_window}.  

	    Jane installe le module complémentaire via les commandes suivantes :
        
	    ```
        cd /opt/splunk/etc/apps
        tar xvfz ~/rfc5424-syslog_11.tgz
        ```
	   
        Jane associe le module complémentaire en remplaçant */opt/splunk/etc/apps/rfc5424/default/transforms.conf* par un nouveau
fichier *transforms.conf* contenant le texte suivant :
	   
	    ```
        [rfc5424_host]
        DEST_KEY = MetaData:Host
        REGEX = <\d+>\d{1}\s{1}\S+\s{1}(\S+)
        FORMAT = host::$1

        [rfc5424_header]
        REGEX = <(\d+)>\d{1}\s{1}\S+\s{1}\S+\s{1}(\S+)\s{1}(\S+)\s{1}(\S+)
        FORMAT = prival::$1 appname::$2 procid::$3 msgid::$4
        MV_ADD = true
        ```
        {:screen}	   

     c. Une fois Splunk configuré, Jane doit ouvrir certains ports sur la machine Ubuntu pour accepter le flux syslog entrant
(port 5140) et l'interface utilisateur Web de Splunk (port
8000) vu que, par défaut, le pare-feu est en place sur le serveur virtuel {{site.data.keyword.Bluemix_notm}}.
	   
	    **Remarque :** la configuration iptable est réalisée ici à des fins d'évaluation par Jane et n'est que temporaire. Pour configurer le
paramètre de pare-feu dans le serveur virtuel Bluemix en environnement de production, reportez-vous au document
[Network Security Groups](https://new-console.ng.bluemix.net/docs/services/networksecuritygroups/index.html){:new_window} pour plus
d'informations.
	 
	   ```
	   iptables -A INPUT -p tcp --dport 5140 -j ACCEPT
       iptables -A INPUT -p tcp --sport 5140 -j ACCEPT
       iptables -A INPUT -p tcp --dport 8000 -j ACCEPT
       iptables -A INPUT -p tcp --sport 8000 -j ACCEPT
	   ```
	   {:screen}	
	  
	   Jane lance ensuite Splunk à l'aide de la commande suivante :

       ```
	   /opt/splunk/bin/splunk start --accept-license
       ```
		
  2. Jane configure les paramètres Splunk afin d'accepter le flux syslog de {{site.data.keyword.Bluemix_notm}}. Elle doit créer une entrée de données
pour le flux syslog.

     a. Dans la partie gauche de l'interface Web de Splunk, Jane clique sur **Data > Data inputs**. Une liste des types d'entrées pris en
charge par Splunk s'affiche. 
	 
     b. Elle sélectionne **TCP** vu que le flux syslog utilise ce protocole.
	 
     c. Dans le panneau **TCP**, elle entre **5140** dans la zone **Port**, en laissant vides
les autres zones, puis clique sur **Next**.
	 
     d. Dans la liste **Source Type**, elle sélectionne **Uncategorized > rfc5424_syslog**.
	 
     e. Pour le type **Method**, elle sélectionne **IP**.
	 
     f. Dans la zone **Index**, Jane clique sur **Create a new index**. Elle nomme le nouvel index
"bluemix", puis clique sur **Save**.
	 
     g. Enfin, dans la fenêtre **Review**, Jane confirme que le paramètre est correct, puis clique sur
**Submit** pour activer cette entrée de données.

  3. Dans {{site.data.keyword.Bluemix_notm}}, Jane crée un service de flux syslog et le lie à une application.

     a. Jane crée un service de flux à l'aide de la commande suivante dans l'interface CLI cf :
	 
     ```
     cf cups splunk -l syslog://dummyhost:5140
     ```
        
     **Remarque :** *dummyhost* n'est pas le nom réel. Il est utilisé pour masquer le nom d'hôte véritable. 

     b. Jane lie le service de flux syslog à une application dans son espace, puis retransfère l'application.
	 
	 ```
     cf bind-service myapp splunk
     cf restage myapp
     ```
		

Jane teste son application, puis entre la chaîne de requête suivante dans l'interface Web de Splunk :

```
source="tcp:5140" index="bluemix" sourcetype="rfc5424_syslog"
```

Jane observe un flux de journaux dans son interface Web Splunk. Bien qu'elle ait installé la version Splunk Light, Jane dispose toujours d'une capacité
de 500 Mo par jour pour ses journaux. 




