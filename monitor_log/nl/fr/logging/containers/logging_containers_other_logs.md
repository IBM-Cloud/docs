---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Collecte de données de journal autres que par défaut depuis un conteneur
{: #logging_containers_collect_data}

Pour capturer des données depuis des emplacements de journal autres que ceux par défaut dans un conteneur, définissez la variable d'environnement **LOG_LOCATIONS** lorsque vous créez un conteneur.
{:shortdesc}

* Ajoutez la variable d'environnement **LOG_LOCATIONS** en spécifiant le chemin du fichier journal lorsque vous créez le conteneur. 
* Vous pouvez ajouter plusieurs fichiers journaux en les séparant par des virgules. 

## Collecte de données de journal autres que celles par défaut via la console Bluemix
{: #logging_containers_collect_data_ui}

Pour collecter des données autres que celles par défaut via la console, procédez comme suit :

1. Dans le catalogue, sélectionnez **Conteneurs** et choisissez une image. 

    La liste des images qui est affichée inclut les images fournies par {{site.data.keyword.IBM}} et celles stockées dans votre registre {{site.data.keyword.Bluemix_notm}} privé. 

2. Définissez votre conteneur. Choisissez un type, entrez un nom pour le conteneur, sélectionnez sa taille et définissez d'autres attributs comme les informations d'adresse IP et les ports. Pour plus d'informations, voir [création et déploiement d'un conteneur unique via l'interface utilisateur de {{site.data.keyword.Bluemix_notm}}](/docs/containers/container_single_ui.html). 

3. Développez la section **Options avancées** et sélectionnez **Ajouter une nouvelle variable d'environnement**.

4. Ajoutez la variable **LOG_LOCATIONS** et définissez sa valeur sur le journal que vous désirez analyser.

    Par exemple, lorsque vous ajoutez un conteneur basé sur l'image Liberty la plus récente, pour analyser le fichier journal *dpkg.log*, définissez la variable d'environnement sur la valeur suivante :
    
    <table>
      <tbody>
        <tr>
          <th align="center">Nom de la variable</th>
          <th align="center">Valeur</th>
        </tr>
        <tr>
          <td align="left">LOG_LOCATIONS</td>
          <td align="left">/var/log/dpkg.log</td>
        </tr>
      </tbody>
    </table>

4. Cliquez sur **Créer**.

Le tableau de bord de conteneur s'ouvre. Vérifiez que le statut du conteneur indique bien *En cours d'exécution*, puis vérifiez les journaux dans l'onglet **Surveillance et journaux**.


## Collecte de données de journal autres que celles par défaut via l'interface CLI
{: #logging_containers_collect_data_cli}

Pour collecter des données de journal autres que celles par défaut via l'interface CLI, procédez comme suit :

1. Configurez un terminal afin d'utiliser l'interface CLI {{site.data.keyword.containershort}}. Pour plus d'informations, voir [Configuration de l'interface CLI d'IBM Bluemix Container Service](/docs/containers/container_cli_cfic_install.html).

2. Connectez-vous à l'interface CLI de Cloud Foundry via la commande suivante : `cf login`. A l'invite, entrez votre ID {{site.data.keyword.Bluemix_notm}}, votre mot de passe, votre organisation et votre
espace. 

    Par défaut, vous être connecté à la région Sud des Etats-Unis ou à la dernière région à laquelle vous
étiez
connecté. 
    
    Vous pouvez inclure l'option **–a** si vous désirez vous connecter à une région spécifique dans {{site.data.keyword.Bluemix_notm}}. Par exemple, le tableau suivant liste les commandes par région :

    <table>
      <tbody>
        <tr>
          <th align="center">Région</th>
          <th align="center">Commande</th>
        </tr>
        <tr>
          <td align="left">Sud des États-Unis</td>
          <td align="left"> cf login -a api.ng.bluemix.net</td>
        </tr>
        <tr>
          <td align="left">Royaume-Uni</td>
          <td align="left">cf login -a api.eu-gb.bluemix.net</td>
        </tr>
        <tr>
          <td align="left">Sydney</td>
          <td align="left">cf login -a api.au-syd.bluemix.net</td>
        </tr>
      </tbody>
    </table>
    

3. Connectez-vous à {{site.data.keyword.containershort}} à l'aide de la commande suivante : `cf ic login`

4. Créez un conteneur unique depuis une image. Incluez la variable d'environnement LOG_LOCATIONS afin d'inclure des emplacements de journal autres que ceux par défaut.  

    Pour ajouter un emplacement personnalisé afin d'examiner ces informations de journal dans Kibana, ajoutez la variable d'environnement **LOG_LOCATIONS** lorsque vous créez le conteneur. Entrez la commande suivante :
    
    `docker run -p numéro_port -e "LOG_LOCATIONS=log1,log2" --name nom_conteneur registry.nom_domaine/nom_image:étiquette_image`
    
    où 
    
     <table>
      <tbody>
        <tr>
          <th align="center">Option</th>
          <th align="center">Description</th>
        </tr>
        <tr>
          <td align="left">-p</td>
          <td align="left"> Si vous désirez rendre votre application accessible depuis Internet, vous devez exposer un port public. Incluez tous les ports spécifiés dans le fichier Dockerfile pour l'image que vous utilisez. <br> Vous pouvez choisir comme protocole IP à utiliser soit UDP, soit TCP. Si vous ne spécifiez pas de protocole, votre port est automatiquement exposé pour le trafic TCP. <br> Lorsque vous exposez un port public, vous créez pour votre conteneur un Groupe de sécurité de réseau public vous permettant d'envoyer et de recevoir des données publiques uniquement sur le port exposé. Tous les autres ports publics sont fermés et ne peuvent pas être utilisés pour accéder à votre application depuis Internet. <br> Vous pouvez inclure plusieurs ports en spécifiant plusieurs options -p. </td>
        </tr>
        <tr>
          <td align="left">-e</td>
          <td align="left">Configurez une variable d'environnement. <br> Vous pouvez mentionner plusieurs clés séparément. Encadrez le nom de la variable d''environnement, tout comme sa valeur, par des guillemets. <br> Pour ajouter un fichier journal à surveiller dans le conteneur, incluez la variable d'environnement LOG_LOCATIONS avec le chemin d'accès du fichier journal.</td>
        </tr>
        <tr>
          <td align="left">--name</td>
          <td align="left">Définit le nom du conteneur.</td>
        </tr>
	<tr>
          <td align="left">registry.nom_domaine</td>
          <td align="left">Registre dans la région publique. Par exemple, pour la région Sud des Etats-Unis, le nom de domaine par défaut est : `ng.bluemix.net` et pour le Royaume-Uni : `eu-gb.bluemix.net` </td>
        </tr>
        <tr>
          <td align="left">nom_image</td>
          <td align="left">Nom de l'image que vous désirez ajouter.</td>
        </tr>
	<tr>
          <td align="left">étiquette_image</td>
          <td align="left">Etiquette de l'image que vous désirez ajouter.</td>
        </tr>
      </tbody>
    </table>
    
    Par exemple, pour créer un conteneur basé sur l'image Liberty la plus récente et inclure le fichier journal `/var/log/dpkg.log`, utilisez la commande suivante : 
    
    `docker run -p 9080 -e "LOG_LOCATIONS=/var/log/dpkg.log" --name MyContainer registry.ng.bluemix.net/ibmliberty:latest`
    
    Le fichier dpkg.log est un fichier journal Ubuntu standard généré habituellement lors de la création d'un conteneur, mais qui n'est pas envoyé automatiquement à Kibana.

Pour vérifier le statut d'un conteneur, exécutez la commande `docker ps`. Si ce statut indique *En cours d'exécution*, vérifiez les journaux dans la console {{site.data.keyword.Bluemix_notm}}, via la ligne de commande, ou via Kibana.



