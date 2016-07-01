---

copyright:
  années : 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

#Accès au système
{: #system_access}
Ces rubriques présentent les méthodes de création et de gestion d'une instance de service en même temps que les différentes méthodes d'accès et de configuration de l'accès à vos systèmes.
{: shortdesc}

*Dernière mise à jour : 08 juin 2016*
{: .last-updated}

## Utilisation de l'API REST dans WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}
{: #restapi_usage}

Des instances dans WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} sont créées, provisionnées, gérées et supprimées de l'une des façons suivantes :

* Depuis {{site.data.keyword.Bluemix_notm}} Catalog et Service Dashboard dans l'interface utilisateur {{site.data.keyword.Bluemix_notm}}.
* A partir de la création d'une application ou d'un script utilisant les API RESTful.

En utilisant les API REST compatibles Swagger 2.0, les clients ont accès à la même fonction que celle fournie via le portail et le tableau de bord. Pour plus d'informations sur les ressources et API REST prises en charge, voir la [documentation d'API REST](https://new-console.{DomainName}/apidocs/212){: new_window} de WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} 

**Remarque :** après création d'une instance de service, selon la taille Tee-Shirt créée, votre service risque de ne pas être immédiatement prêt à être utilisé. Il est recommandé de faire une requête sur la zone **Statut** de l'élément JSON retourné pour déterminer l'état actuel de l'instance de service.

**Remarque :** par défaut, l'URL BASE API pointe sur un noeud final de la région [US South Region](https://wasaas-broker.ng.bluemix.net/wasaas-broker/api/v1){: new_window}. Si vous utilisez la région UK ou Sydney, assurez-vous que votre application se sert de l'un des noeuds finaux suivants :

* [UK Region](https://wasaas-broker.eu-gb.bluemix.net/wasaas-broker/api/v1){: new_window}
* [Sydney Region](https://wasaas-broker.au-syd.bluemix.net/wasaas-broker/api/v1){: new_window}


## Tableau de bord du service
{: #service_dashboard}

Une fois votre instance de service créée, revenez au tableau de bord du service. Vous pouvez revenir au tableau de bord du service à tout moment en
cliquant sur l'icône du service dans le tableau de bord de votre organisation.
Depuis le tableau de bord du service, vous pouvez accéder aux éléments suivants :

*  Un lien vers cette documentation.
*  Un lien permettant de télécharger le fichier de configuration OpenVPN.
*  La possibilité de démarrer et d'arrêter la machine virtuelle. La machine virtuelle est démarrée initialement.
*  Le nom d'hôte.
*  Le nom et le mot de passe de l'administrateur.
*  Une clé SSH privée.
*  Le nom et le mot de passe de d'administrateur WebSphere®.
*  Les URL du centre d'administration et de la console d'administration.

**Remarque** : du fait d'un volume spécifique de ressources de calcul, de mémoire et d'entrée/sortie, les clients sont facturés pour les les machines virtuelles accumulées dans l'état STOPPED à un taux réduit de 5%.  Les clients sont gérés par rapport à un nombre fixe d'instances STOPPED ne comportant pas plus de 10 adresses IP ou 64 Go de mémoire.


## Configuration d'openVPN pour les instances WebSphere Application Server for Bluemix
{: #setup_openvpn}

OpenVPN est requis pour accéder à un serveur WebSphere Application Server sur une machine virtuelle Bluemix. Il doit être
installé et s'exécuter avec des privilèges d'administrateur.  

### Pour ouvrir openVPN sous Windows, procédez comme suit :

1. Suivez le lien de téléchargement d'[openVPN Windows](http://swupdate.openvpn.org/community/releases/) et téléchargez le module
suivant :
  * [openvpn-install-2.3.4-I001-x86_64.exe](https://swupdate.openvpn.org/community/releases/openvpn-install-2.3.4-I001-x86_64.exe){: new_window}
pour environnement 64 bits, ou
  * [openvpn-install-2.3.4-I001-i686.exe](https://swupdate.openvpn.org/community/releases/openvpn-install-2.3.4-I001-i686.exe){: new_window}
pour environnement 32 bits
2. Prenez soin de sélectionner [Exécuter en tant qu'administrateur
Windows](https://technet.microsoft.com/en-us/magazine/ff431742.aspx){: new_window} et installez openVPN.
3. Téléchargez les fichiers de configuration de réseau privé virtuel depuis le lien de téléchargement OpenVPN de l'instance WebSphere Application
Server for Bluemix dans le tableau de bord des services. Décompressez les quatre fichiers vers le répertoire **{répertoire_OpenVPN}\config**.   Par exemple :

  <pre>  
    C:\Program Files\OpenVPN\Config
  </pre>
  {: codeblock}

4. Lancez le programme client openVPN "OpenVPN GUI". Prenez soin de sélectionner
[Exécuter en tant qu'administrateur
Windows](https://technet.microsoft.com/en-us/magazine/ff431742.aspx){: new_window} lorsque vous lancez le programme. Sinon, il se peut que vous ne puissiez pas vous connecter.

### Procédez comme suit pour ouvrir openVPN sous Linux :
1. Pour installer openVPN, suivez ces
[instructions](https://openvpn.net/index.php/access-server/docs/admin-guides/182-how-to-connect-to-access-server-with-linux-clients.html){: new_window}.
  * Si vous devez télécharger et installer manuellement le gestionnaire de packages RPM, accédez à la
[page de téléchargement d'openVPN
unix/linux](https://openvpn.net/index.php/access-server/download-openvpn-as-sw.html){: new_window}. Vous aurez peut-être besoin de l'aide de votre administrateur Linux.
3. Téléchargez les fichiers de configuration réseau privé virtuel depuis le lien de téléchargement OpenVPN de l'instance WebSphere Application Server for Bluemix dans le
tableau de bord des services. Procédez à l'extraction des fichiers dans le
répertoire à partir duquel vous prévoyez de démarrer le client openVPN. Les quatre fichiers doivent se trouver dans le même répertoire.
3. Démarrez le programme client openVPN.  Ouvrez une fenêtre de terminal et accédez au répertoire contenant les fichiers de configuration. Exécutez la
commande suivante en tant que root :

  <pre>
      $ openvpn --config vt-wasaas-wasaas.ovpn
  </pre>
  {: codeblock}  

### Pour configurer openVPN sous Mac, procédez comme suit :
1. Une méthode consiste à installer le logiciel open source [Tunnelblick](https://tunnelblick.net/){: new_window}.
2. Procédez à l'extraction des fichiers de configuration du réseau privé virtuel depuis le service WebSphere. Tunnelblick vous invite à entrer le mot de passe de l'administrateur pour Mac et ajoute la configuration à l'ensemble de réseaux privés virtuels que
vous pouvez utiliser pour vous connecter.
3. Connectez-vous au réseau privé virtuel pour pouvoir accéder à votre machine virtuelle. Après votre premier accès, Tunnelblick met en cache la configuration pour que vous puissiez vous connecter depuis [Tunnelblick](https://tunnelblick.net/){: new_window}. Vous pouvez placer une icône dans la barre de menus supérieure pour un accès facile.


## Utilisation de SSH pour accéder aux machines virtuelles WebSphere Application Server for Bluemix
{: #using_ssh}

Ces instructions supposent que vous utilisez OpenSSH comme client. OpenSSH est généralement disponible sur Linux ou dans Cygwin s'exécutant sous
Windows. Il peut aussi être installé en vue de son exécution depuis une invite de commande Windows.

Pour vérifier l'installation d'OpenSSH, entrez la commande suivante :
  ```
      $ ssh -V
  ```
  {: codeblock}

Votre réponse devrait être similaire à ceci :
  ```
      OpenSSH_6.6p1, OpenSSL 1.0.1g 7 Apr 2014
  ```
  {: codeblock}

Procédez comme suit pour configurer l'accès SSH aux machines virtuelles de votre serveur WebSphere
Application Server for Bluemix :

1. Examinez le message d'avertissement qui s'affiche la première fois que vous vous connectez :
"L'authenticité de l'hôte x.x.x.x n'a pas pu être établie". Ce comportement est
normal. A l'invite, sélectionnez Oui. La clé publique est à présent installée sur votre machine virtuelle pour l'utilisateur
"virtuser".
2. Connectez-vous à virtuser à l'aide de la clé privée. Pour de meilleurs résultats, utilisez la méthode d'authentification par clé privée.
3. Copiez le contenu de la clé privée dans un fichier.
4. Exécutez la commande suivante :

  <pre>
    $ ssh virtuser@169.53.246.xxx -i /chemin/nom_fichier_clé_privée
  </pre>
  {: codeblock}

5. Obtenez les droits d'accès sysadmin complets en basculant de l'utilisateur virtuser à l'utilisateur root à l'aide de la commande suivante :

  <pre>
    $ sudo su root
  </pre>
  {: codeblock}

6. Si vous rencontrez des problèmes lors de l'accès au système avec la clé SSH privée, utilisez le mot de passe root fourni. Connectez-vous en tant que
root en exécutant la commande suivante et soumettez le mot de passe :

 <pre>
    $ ssh root@169.53.246.x
  </pre>
  {: codeblock}

7. Que vous accédiez au système avec la clé ssh privée ou le mot de passe root, changez immédiatement le mot de passe root.
8. Pour simplifier vos commandes SSH, créez un fichier nommé "config" dans le répertoire %HOME%/.ssh. Par exemple :

  <pre>
   Host VM1
      Hostname 169.53.246.xxx
      User virtuser
      IdentityFile /chemin/nom_fichier_clé_privée
  </pre>
  {: codeblock}

9. Exécutez "ssh VM1" pour vous connecter en tant que virtuser.

## Chemins système
{: #system_paths}

* Les commandes du profil Liberty peuvent être émises depuis */opt/IBM/WebSphere/Liberty/bin*.
* L'emplacement du profil de serveur Liberty est */opt/IBM/WebSphere/Profiles/Liberty/servers/server1*.
* Les commandes WebSphere Application Server Traditional peuvent être émises depuis */opt/IBM/WebSphere/AppServer/bin*.
* L'emplacement du profil de serveur Traditional WebSphere Application Server est */opt/IBM/WebSphere/Profiles/DefaultAppSrv01/servers/server1*.

## Utilisation des liens vers le centre d'administration et vers la console d'administration
{: #console_links}

Lorsque vous cliquez sur le lien vers le centre d'administration ou la console d'administration, il se peut qu'un avertissement indiquant que la connexion n'est pas sécurisée s'affiche. Le message exact varie selon le navigateur, tout comme les étapes permettant de contourner ou d'éliminer l'avertissement.

Etant donné que vous utilisez des liens fournis par {{site.data.keyword.IBM}}, vous pouvez ignorer l'avertissement et vous connecter sans crainte. Votre navigateur peut proposer de stocker une exception de sécurité ; c'est la façon la plus facile d'éviter l'avertissement à l'avenir.

Vous pouvez aussi exporter le certificat de signataire entrant, puis l'importer dans votre navigateur en tant que certificat racine accrédité. Cette option
nécessite que vous ajoutiez une entrée dans votre fichier *hosts* pour mapper l'adresse IP de la machine virtuelle au nom
usuel de l'émetteur du certificat. Le format de ce nom est le suivant : wl<pureapplication.ibmcloud.com. Si vous utilisez le nom d'hôte à la place de
l'adresse IP dans l'adresse URL, vous devriez pouvoir vous connecter correctement. Vous devez ensuite accéder au centre d'administration ou à la console d'administration avec ce nom d'hôte, au lieu de l'adresse IP dans l'adresse URL.

Enfin, les clients installent souvent leurs propres certificats racine pour les applications externes. Pour plus d'informations, reportez-vous au Knowledge
Center de
[WebSphere
Application Server](http://www.ibm.com/support/knowledgecenter/SSEQTP_8.5.5/com.ibm.websphere.base.doc/ae/tsec_securecomm.html?cp=SSEQTP_8.5.5%2F1-11-2-6&lang=en){: new_window} ou de
[Liberty Core](http://www.ibm.com/support/knowledgecenter/SSD28V_8.5.5/com.ibm.websphere.wlp.core.doc/ae/twlp_sec_comm.html?lang=en){: new_window}.

## Ports de pare-feu
{: #firewall_ports}

Il peut être nécessaire d'ouvrir des ports sur le pare-feu afin d'autoriser l'accès à des applications et des bases de données.
  * Sur chaque noeud WebSphere Application Server for Bluemix, un script openFirewallPorts.sh est présent dans le répertoire REP_WAS/virtual/bin.
  * Sur chaque hôte de la collectivité Liberty, un script openFirewallPorts.sh est présent dans le répertoire REP_WAS/virtual/bin.

Syntaxe :
  ```
      $ openFirewallPorts.sh -ports <PORT>:<PROTOCOLE>,... -persist true|false
  ```
  {: codeblock}

* Remplacez PORT par numéro de port
* Remplacez PROTOCOLE par TCP ou par UDP
* -persist doit recevoir la valeur true ou false

Vous pouvez spécifier plusieurs ports en les séparant par une virgule (",").

**Remarque **: Le port source (sport) et le port de destination (dport) du port ouvert sont tous deux ouverts dans les sections
INPUT et OUTPUT du pare-feu. Vous devez exécuter ce script en tant que root en utilisant sudo. Vous pouvez aussi
modifier iptables directement.
