# Commandes bl

*Dernière mise à jour :* 13 novembre 2015

Si vous générez une application Node.js, vous pouvez utiliser Bluemix. Live Sync afin de mettre rapidement à jour l'instance d'application qui
s'exécute dans Bluemix et procéder au développement comme vous le feriez sur le bureau, sans redéploiement. Lorsque vous apportez une modification, vous
pouvez immédiatement voir cette modification dans votre application Bluemix en cours d'exécution. L'interface de ligne de commande Bluemix Live Sync
s'appelle *bl*.

Vous pouvez utiliser l'interface de ligne de commande **bl** pour effectuer les tâches suivantes :

* Démarrer et arrêter une application qui s'exécute dans Bluemix.
* Créer un projet reposant sur le cloud depuis votre bureau.
* Synchroniser les modifications apportées sur votre bureau dans l'espace de projet reposant sur le cloud et dans l'application en cours d'exécution
dans Bluemix.
* Afficher la liste des projets disponibles pour la synchronisation.
* Afficher le statut des applications en cours d'exécution.

Pour plus d'informations sur le téléchargement et l'utilisation de la commande bl, voir [Bluemix Live Sync](https://www.ng.bluemix.net/docs/manageapps/bluemixlive.html#bluemixlive).


## Commandes bl

La ligne de commande Bluemix Live Sync, **bl**, applique la syntaxe suivante :

``` commande bl [arguments][options] [--help]```

### Commandes
<dl>
<dt>login, l</dt>
<dd>Connecte à Bluemix. </dd>
<dt>logout, lo</dt>
<dd>Déconnecte l'utilisateur.</dd>
<dt>sync, s</dt>
<dd>Démarre le processus de synchronisation entre le bureau et le serveur.</dd>
<dt>create, c</dt>
<dd>Crée un projet privé, le lie au référentiel Git dans ce répertoire et déploie le contenu dans Bluemix.</dd>
<dt>projects, p</dt>
<dd>Répertorie tous les projets disponibles pour la synchronisation.</dd>
<dt>start, st</dt>
<dd>Démarre l'instance d'application dans Bluemix. </dd>
<dt>stop, sp</dt>
<dd>Arrête l'instance d'application dans Bluemix. </dd>
<dt>status, ss</dt>
<dd>Affiche le statut de l'instance d'application en cours d'exécution dans Bluemix. </dd>
</dl>

### Arguments
<dl>
<dd>Arguments de la commande.</dd>
</dl>

### Options
<dl>
<dd>Options de la commande.</dd>
</dl>

### Options globales
<dl>
<dt>--help</dt>
<dd>Affiche la page d'aide pour la commande spécifiée.</dd>
<dt>--verbose</dt>
<dd>Active la consignation prolixe.</dd>
</dl>

**Remarque :** si l'un de vos arguments ou l'une de vos options comporte un espace, placez la valeur entre guillemets.
