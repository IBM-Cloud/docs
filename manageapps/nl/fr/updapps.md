---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-25"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Mise à jour d'applications
{: #updatingapps}


Vous pouvez utiliser la commande cf push ou {{site.data.keyword.Bluemix}} DevOps Services pour mettre à jour les applications dans {{site.data.keyword.Bluemix_notm}}. Dans de nombreux cas, même pour les packs de construction intégrés tels que Node.js, vous devez également fournir un paramètre -c afin de spécifier la
commande à utiliser pour démarrer votre application.
{:shortdesc}

## Création et utilisation d'un domaine personnalisé
{: #domain}

Pour les applications CF et les groupes de conteneurs, vous pouvez utiliser un domaine personnalisé dans l'adresse URL de votre application au lieu
du domaine de système
{{site.data.keyword.Bluemix_notm}} par défaut, à savoir mybluemix.net.

Les domaines fournissent la route d'URL allouée à votre organisation dans {{site.data.keyword.Bluemix_notm}}. Pour utiliser un domaine personnalisé, vous devez enregistrer le domaine personnalisé sur un serveur DNS public, configurer ce domaine dans {{site.data.keyword.Bluemix_notm}}, puis mapper ce domaine au domaine de système {{site.data.keyword.Bluemix_notm}} sur le serveur DNS public. Une fois que votre domaine personnalisé est mappé au domaine de système {{site.data.keyword.Bluemix_notm}}, les requêtes de votre domaine personnalisé sont acheminées à votre application
dans {{site.data.keyword.Bluemix_notm}}.

Vous pouvez créer et utiliser un domaine personnalisé dans {{site.data.keyword.Bluemix_notm}} en utilisant
l'interface utilisateur {{site.data.keyword.Bluemix_notm}} ou l'interface de ligne de commande cf.

* Utilisez l'interface utilisateur {{site.data.keyword.Bluemix_notm}} :

  1. Créez un domaine personnalisé pour votre organisation.

	1. Accédez à **Gérer** &gt; **Compte** &gt; **Organisations** &gt; **Afficher les détails** pour votre organisation, puis cliquez sur **Editer l'organisation** &gt; **Domaines**.

	2. Sur l'onglet **Domaines**, cliquez sur **Ajouter un domaine**, entrez votre nom de domaine personnalisé, puis cliquez sur **Sauvegarder**.

	**Remarque** : Par exemple, vous pouvez utiliser `mon_entreprise.com` pour associer la route `www.mon_entreprise.com` à votre application.
Vous pouvez aussi utiliser `exemple.mon_entreprise.com` pour associer la route `www.exemple.mon_entreprise.com` à votre application.

  2. Ajoutez la route avec le domaine personnalisé à une application.

    1. Cliquez sur l'icône **Menu** ![Icône de menu](../icons/icon_hamburger.svg) &gt; **Tableau de bord**, puis cliquez sur la ligne de l'application à laquelle ajouter la route. La page **Vue d'ensemble** s'affiche.

	2. Dans le menu **Routes**, sélectionnez **Editer les routes**.

	3. Cliquez sur **Ajouter une route** et spécifiez la route à utiliser pour l'application.
	4. Cliquez sur **Sauvegarder**.

* Utilisez l'interface de ligne de commande cf :

  1. Créez un domaine personnalisé pour votre organisation en lançant la commande suivante :

    ```
    cf create-domain <nom_de_votre_organisation> mon_domaine
    ```

    *nom_de_votre_organisation*

        Nom de votre organisation.

    *mon_domaine*

        Nom de domaine personnalisé que vous désirez utiliser.

  2. Ajoutez la route avec le domaine personnalisé à une application. Pour les applications CF, entrez la commande suivante :

    ```
    cf map-route mon_app mon_domaine -n nom_hôte
    ```
    Pour les groupes de conteneurs, entrez la commande suivante :
     ```
     cf ic route map -n nom_hôte -d mon_domaine mon_groupe_de_conteneurs
     ```
    *mon_app*

    	Pour les applications CF, nom de votre application.

    *mon_domaine*

    	Nom de votre domaine personnalisé, par exemple, `www.mydomain.mybluemix.net`.

    *nom_hôte*

        Nom d'hôte sur la route que vous désirez utiliser pour votre application.

    *mon_groupe_de_conteneurs*

        Pour les groupes de conteneurs, nom du groupe de conteneurs.


Une fois le domaine personnalisé configuré dans {{site.data.keyword.Bluemix_notm}}, vous devez le mapper au domaine de système
{{site.data.keyword.Bluemix_notm}} sur votre serveur DNS enregistré :

  1. Configurez un enregistrement 'CNAME' pour le nom de domaine personnalisé sur votre serveur DNS. Les étapes de configuration de l'enregistrement
CNAME varient selon votre fournisseur DNS. Par exemple, si vous utilisez GoDaddy, vous suivez la procédure de la page [Domains Help ![icône de lien externe](../icons/launch-glyph.svg)](https://www.godaddy.com/help/add-a-cname-record-19236){: new_window} de GoDaddy.
  2. Mappez le nom de domaine personnalisé au noeud final sécurisé pour la région {{site.data.keyword.Bluemix_notm}} dans laquelle s'exécute
votre application. Utilisez les noeuds finaux de région suivants pour fournir la route d'URL allouée à votre organisation dans
{{site.data.keyword.Bluemix_notm}} :

    * SUD DES ETATS-UNIS : `secure.us-south.bluemix.net`
    * EUROPE-ROYAUME-UNI : `secure.eu-gb.bluemix.net`
    * AUSTRALIE-SYDNEY : `secure.au-syd.bluemix.net`
    * EUROPE-ALLEMAGNE : `secure.eu-de.bluemix.net`

Depuis un navigateur ou l'interface de ligne de commande, entrez l'adresse URL suivante pour accéder à l'application mon_app :

```
http://nom_hôte.mon_domaine
```

**Remarque :** pour supprimer une route orpheline, utilisez la commande suivante :

```
cf delete-route domaine -n nom_hôte -f
```

*domaine* est le nom de votre domaine et *nom_hôte* le nom d'hôte de la route pour votre application. Pour plus d'informations sur la commande
**cf delete-route**, entrez `cf delete-route -h`.

##Déploiements Blue-Green
{: #blue_green}

{{site.data.keyword.Bluemix_notm}} prend en charge la technique de déploiement Blue-Green pour
permettre une distribution continue et limiter les événements d'indisponibilité.

Le *déploiement Blue-Green* est une technique de déploiement à indisponibilité zéro qui compte deux environnements de
production identiques appelés Blue et Green. Leur différence tient aux artefacts que le développeur a délibérément modifiés, généralement selon la version de l'application. A tout moment, au moins l'un des environnements est actif. La technique de déploiement Blue-Green procure les avantages suivants :

* Passage rapide du logiciel de sa phase de test final vers l'environnement opérationnel de production.
* Déploiement d'une nouvelle version d'une application sans perturbation du trafic vers l'application.
* Basculement rapide. Si l'un de vos environnements connaît un problème, vous pouvez basculer rapidement vers l'autre environnement.

Si vous
avez déjà déployé une application dans {{site.data.keyword.Bluemix_notm}} et que vous souhaitez la mettre à niveau
vers une
nouvelle version, vous pouvez utiliser l'une des méthodes ci-dessous pour effectuer un déploiement Blue-Green.

### Exemple : Utilisation de la commande cf rename

Dans cet exemple, le nom de l'application est Blue. Cet exemple illustre la mise à jour de la version de *Blue* à l'aide de la commande **cf rename** sans
perturbation du trafic vers l'application. Vous pouvez, si vous le désirez, supprimer l'ancienne version de *Blue* une fois la nouvelle version en place.

1. Envoyez l'application *Blue* à {{site.data.keyword.Bluemix_notm}}.

  ```
  cf push Blue
  ```

  **Résultat :** l'application *Blue* s'exécute et répond à l'adresse URL `Blue.mybluemix.net`.

2. Utilisez la commande **cf rename** pour renommer
l'application *Blue* en *Green* :

  ```
  cf rename Blue Green
  ```

  Répertoriez les applications qui se trouvent dans l'espace en cours avec la commande **cf apps** :

  ```
  ...
  name             requested state   instances   memory   disk   urls
  Green            started           1/1         1G       1G	 Blue.mybluemix.net
  ...
  ```

  **Résultat :** l'application *Green* s'exécute et répond à l'adresse URL `Blue.mybluemix.net`.

3. Apportez les modifications nécessaires et préparez la version *Blue* mise à jour. Envoyez l'application *Blue*
mise à jour à {{site.data.keyword.Bluemix_notm}} :

  ```
  cf push Blue
  ```

  Répertoriez les applications qui se trouvent dans l'espace en cours avec la commande **cf apps** :

  ```
  ...
  name             requested state   instances   memory   disk   urls
  Green            started           1/1         1G       1G	 Blue.mybluemix.net
  Blue             started           1/1         1G       1G	 Blue.mybluemix.net
  ...
  ```

  **Résultats : **
    * Deux instances de l'application sont déployées, l'instance *Blue* et l'instance *Green*.
	* L'application *Green* s'exécute et répond à l'adresse URL `Blue.mybluemix.net`.

4. Facultatif : si vous voulez supprimer l'ancienne version (*Green*) de l'application, utilisez la commande **cf
delete**.

  ```
  cf delete Green -f
  ```

  Répertoriez les routes qui se trouvent dans votre espace avec la commande **cf route** :

  ```
  ...
  host             domain           apps
  Blue             mybluemix.net    Blue
  ...
  ```

  **Résultat :** l'application *Blue* répond à l'adresse URL `Blue.mybluemix.net`.

### Exemple : Utilisation de la commande cf map-route

Dans cet exemple, *Blue* est l'ancienne version déployée et
*Green* la version mise à jour. Cet exemple illustre la mise à jour de la version de *Blue* à l'aide de la commande **cf map-route** sans perturbation du trafic vers l'application. Vous pouvez, si vous le désirez, supprimer l'ancienne version de *Blue* une fois la nouvelle version en place.

1. Envoyez l'application *Blue* à {{site.data.keyword.Bluemix_notm}}.

  ```
  cf push Blue
  ```

  **Résultat :** l'application *Blue* s'exécute et répond à l'adresse URL `Blue.mybluemix.net`.

2. Apportez les modifications nécessaires et préparez la version *Green*. Envoyez l'application *Green* à
{{site.data.keyword.Bluemix_notm}} :

  ```
  cf push Green
  ```

  Répertoriez les applications qui se trouvent dans l'espace en cours avec la commande **cf route** :

  ```
  ...
  host             domain           apps
  Blue             mybluemix.net    Blue
  Green            mybluemix.net    Green
  ...
  ```

  **Résultats : **

    * Deux instances de l'application sont déployées, l'instance *Blue* et l'instance *Green*.
	* L'application *Blue* répond à l'adresse URL `Blue.mybluemix.net`. De plus, l'application *Green*
répond à l'adresse URL `Green.mybluemix.net`.

3. Mappez l'application *Blue* à l'application *Green* pour que tout le trafic vers `Blue.mybluemix.net`
soit routé vers l'application *Blue* et vers l'application *Green*.

  ```
  cf map-route Green mybluemix.net -n Blue
  ```

  Répertoriez les routes qui se trouvent dans votre espace avec la commande cf routes :

  ```
  ...
  host             domain           apps
  Blue             mybluemix.net    Blue, Green
  Green            mybluemix.net    Green
  ...
  ```

  **Résultat :**

    * Le routeur CF envoie désormais le trafic pour Blue.mybluemix.net. à l'application Blue et à l'application Green.
	* Le routeur CF continue à envoyer le trafic pour Green.mybluemix.net. à l'application Green.

4. Lorsque vous vérifiez que *Green* est en cours d'exécution comme prévu, supprimez la route `Blue.mybluemix.net` de
l'application *Blue* :

  ```
  cf unmap-route Blue mybluemix.net -n Blue
  ```

  Répertoriez les routes qui se trouvent dans votre espace avec la commande cf routes :

  ```
  ...
  host             domain           apps
  Blue             mybluemix.net    Green
  Green            mybluemix.net    Green
  ...
  ```

  **Résultat :** le routeur CF arrête d'envoyer le trafic à l'application *Blue*. L'application *Green*
répond aux deux adresses URL : `Green.mybluemix.net` et `Blue.mybluemix.net`.

5. Supprimez la route `Green.mybluemix.net` vers l'application *Green*.

  ```
  cf unmap-route Green mybluemix.net -n Green
  ```

  **Résultat :** le routeur CF arrête d'envoyer le trafic à l'application *Blue*. L'application *Green* répond à l'adresse URL `Blue.mybluemix.net`.

6. Facultatif : si vous voulez supprimer l'ancienne version (*Blue*) de l'application, utilisez la commande `cf
delete`.

  ```
  cf delete Blue -f
  ```

  Répertoriez les routes qui se trouvent dans votre espace avec la commande cf route :

  ```
  ...
  host             domain           apps
  Blue             mybluemix.net    Green
  ...
  ```

  **Résultat :** l'application *Green* répond à l'adresse URL `Blue.mybluemix.net`.


# Liens connexes
{: #rellinks notoc}

## Liens connexes
{: #general}

* [Blue-green deployments ![icône de lien externe](../icons/launch-glyph.svg)](http://martinfowler.com/bliki/BlueGreenDeployment.html){:new_window}
* [IBM {{site.data.keyword.Bluemix_notm}} DevOps Services ![icône de lien externe](../icons/launch-glyph.svg)](https://hub.jazz.net/){:new_window}
