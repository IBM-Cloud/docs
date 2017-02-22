---

copyright:
  years: 2014, 2017
lastupdated: "2017-01-17"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Configuration de l'interface de ligne de commande pour utiliser les commandes Swift et Cloud Foundry

Pour interagir avec le service {{site.data.keyword.objectstorageshort}} en utilisant les commandes Swift ou Cloud Foundry, vous devez installer les logiciels prérequis.
{: shortdesc}


## Installation du client Swift {: #install-swift-client}

Si ce n'est déjà fait, installez les logiciels prérequis suivants.
* Python 2.7 ou ultérieur
* Package setuptools
* Package pip
* Interface de ligne de commande Cloud Foundry


Pour installer le client Python Swift, exécutez la commande suivante :
```
pip install python-swiftclient
```
{: pre}

Pour installer le client Python Keystone, exécutez la commande suivante :
```
pip install python-keystoneclient
```
{: pre}

Pour plus d'informations sur les prérequis, voir la [documentation Openstack](http://docs.openstack.org/user-guide/common/cli_install_openstack_command_line_clients.html#install-the-prerequisite-software){: new_window}.


## Configuration du client {: #setup-swift-client}

Pour configurer le client Swift, vous devez `exporter` vos informations d'authentification. Vous pouvez [générer les données d'identification](/docs/services/ObjectStorage/os_credentials.html) via l'interface de ligne de commande en utilisant les commandes Cloud Foundry ou cURL ou en vous servant de l'interface utilisateur {{site.data.keyword.Bluemix_notm}}. Le client prend les informations dans les variables d'environnement du tableau ci-après.

<table>
<caption> Tableau 1. Variables d'environnement et descriptions </caption>
  <tr>
    <th> Variable d'environnement </th>
    <th> Description </th>
  </tr>
  <tr>
    <td> <code>OS_USER_ID</code> </td>
    <td> Votre ID utilisateur {{site.data.keyword.objectstorageshort}}. </td>
  </tr>
  <tr>
    <td> <code>OS_PASSWORD</code> </td>
    <td> Mot de passe pour votre instance {{site.data.keyword.objectstorageshort}}. </td>
  </tr>
  <tr>
    <td> <code>OS_PROJECT_ID</code> </td>
    <td> Votre ID projet. </td>
  </tr>
  <tr>
    <td> <code>OS_REGION_NAME</code> </td>
    <td> Région dans laquelle vos objets sont stockés. {{site.data.keyword.objectstorageshort}} est disponible dans les régions Dallas et Londres. </td>
  </tr>
  <tr>
    <td> <code>OS_AUTH_URL</code> </td>
    <td> URL du noeud final. Assurez-vous que <code>/v3</code> est ajouté à la fin de l'URL. </td>
  </tr>
</table>



Pour exporter vos informations d'authentification, entrez vos données d'identification et exécutez les commandes suivantes :
```
export OS_USER_ID=
export OS_PASSWORD=
export OS_PROJECT_ID=
export OS_AUTH_URL=
export OS_REGION_NAME=
export OS_IDENTITY_API_VERSION=
export OS_AUTH_VERSION=

swift auth
```
{: codeblock}


Exemple :
```
export OS_USER_ID=24a20b8e4e724f5fa9e7bfdc79ca7e85
  export OS_PASSWORD=*******
  export OS_PROJECT_ID=383ec90b22ff4ba4a78636f4e989d5b1
  export OS_AUTH_URL=https://identity.open.softlayer.com/v3
  export OS_REGION_NAME=dallas
  export OS_IDENTITY_API_VERSION=3
  export OS_AUTH_VERSION=3

swift auth
```
{: screen}
