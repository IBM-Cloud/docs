---

copyright:
  years: 2015, 2016

---

<!-- Copyright info at top of file: REQUIRED
    The copyright info is YAML content that must occur at the top of the MD file, before attributes are listed.
    It must be surrounded by 3 dashes.
    The value "years" can contain just one year or a two years separated by a comma. (years: 2014, 2016)
    Indentation as per the previous template must be preserved.
-->

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Extension du service {{site.data.keyword.deliverypipeline}}
{: #deliverypipeline_extending}
Dernière mise à jour : 29 août 2016
{: .last-updated}

Vous pouvez étendre les fonctions du service {{site.data.keyword.deliverypipeline}} en configurant vos travaux pour qu'ils utilisent les services pris en charge. Par exemple, les travaux de test peuvent exécuter des analyses de code statique et les travaux de génération peuvent internationaliser des chaînes.
{:shortdesc}

<!-- Include a sentence to briefly introduce the steps/subtopics. Example: -->

Les tâches suivantes expliquent comment intégrer des outils sélectionnés à un service Delivery Pipeline.

## Exécution d'analyses de code statique à l'aide du pipeline

{: #deliverypipeline_scan}

Vous souhaitez rechercher des problèmes de sécurité dans votre code avant de le déployer ? Lorsque vous utilisez IBM® Static Analyzer for Bluemix™ dans le cadre de votre pipeline, vous pouvez exécuter des vérifications automatisées par rapport aux fichiers binaires de génération `.war`, `.ear`, `.jar` ou `.class` statique d'application Java.

Un pipeline qui utilise le service Static Analyzer inclut généralement les étapes suivantes :

+ Une étape de génération permettant de créer les fichiers source
+ Une étape de traitement incluant les travaux suivants :
  + Un travail de génération permettant d'exécuter le service Static Analyzer
  + Un travail de génération exécutant une génération de conteneur
+ Une étape de déploiement permettant de déployer le conteneur


### Création d'une analyse de code statique

Avant de commencer, [consultez les
conditions d'utilisation du service](http://www-03.ibm.com/software/sla/sladb.nsf/sla/bm-6814-01).

<!-- Use ordered list markup for the step section. Include code examples as needed. -->

1. Créez une étape de traitement.

  a. Cliquez sur **Ajouter une étape**.

  b. Donnez un nom à l'étape, par exemple, `Traitement en cours`.

  c. Pour le type d'entrée, sélectionnez **Artefacts de construction**.

  d. Pour l'étape et pour le travail, vérifiez les valeurs et mettez-les à jour si besoin.

2. Dans l'étape de traitement, ajoutez un travail de génération pour exécuter l'examen du code.

  a. Sur l'onglet **Travaux**, cliquez sur **Ajouter un travail**.

  b. Pour le type de travail, sélectionnez **Tester**.

  c. Pour le type de testeur, sélectionnez **IBM Security Static Analyzer**.

  d. Pour l'organisation et l'espace, vérifiez les valeurs et mettez-les à jour si besoin.

  e. Sélectionnez ou désélectionnez la case à cocher **Configurer un service et un espace pour moi** selon les besoins.

    * Si vous souhaitez que le pipeline vérifie dans votre espace Bluemix l'existence du service et d'une application qui établit une liaison entre le service et le conteneur, sélectionnez la case à cocher. Si le service ou l'application liée n'existe pas, il est créé par le pipeline pour ajouter le forfait gratuit du service à votre espace. L'application liée est créée avec le nom `pipeline_bridge_app`. Ensuite, le pipeline utilise les données d'identification de pipeline_bridge_app pour accéder aux services liés.

    * Si vous avez déjà configuré le service et l'application liée dans votre espace Bluemix ou si vous souhaitez [configurer manuellement ces exigences](https://www.ng.bluemix.net/docs/containers/container_group_pipeline_ov.html#container_binding_pipeline), laissez la case à cocher désélectionnée.

  f. Dans la zone **Minutes to wait for analysis to complete**, tapez une valeur comprise entre 0 et 59 minutes. La valeur par défaut est 5 minutes. Une URL vers le tableau de bord Static Analyzer figure dans les journaux de console à la fin du travail.

     Si l'analyse Static Analyzer n'est pas terminée avant l'heure que vous avez spécifiée, le travail échoue. Toutefois, l'analyse de l'examen continue de s'exécuter et vous pouvez l'afficher sur le tableau de bord Static Analyzer. Une fois l'examen Static Analyzer terminé, si vous relancez l'exécution du travail, la demande d'examen n'est pas soumise et le travail de pipeline peut être effectué. Sinon, vous pouvez configurer le pipeline pour qu'il ne soit pas bloqué si l'analyse aboutit. Pour obtenir des instructions, voir l'étape suivante.

  g. Sélectionnez ou désélectionnez la case à cocher **Arrêter d'exécuter cette étape si ce travail échoue** selon ce qui doit se produire si ce travail échoue ou dépasse le délai d'attente prévu. Les travaux peuvent échouer lorsque les vulnérabilités sont élevées.

    * Si vous sélectionnez la case à cocher et que le travail échoue, les travaux ultérieurs dans l'étape et les étapes ultérieures ne s'exécutent pas.

    * Si vous désélectionnez la case à cocher et que le travail échoue, l'étape se poursuit sans bloquer les travaux et les étapes ultérieurs. Par exemple, si vous savez que le rapport inclut de nombreux problèmes à traiter, vous souhaiterez peut-être configurer la poursuite de l'étape car l'examen peut durer un certain temps. Dans ce cas, il n'est pas souhaitable que le reste de vos travaux et de vos étapes s'arrêtent uniquement parce que l'examen
dure trop longtemps.

  h. Cliquez sur **Sauvegarder**.

3. Lorsque le travail est terminé, affichez les résultats en cliquant sur **Afficher les journaux et l'historique
**. En cas de réussite ou de dépassement de délai de l'analyse, une URL apparaît dans les résultats de l'examen. Si l'examen est en attente, attendez qu'il se termine pour afficher tous les résultats.

4. Vous pouvez, si nécessaire, exécuter à nouveau l'étape de traitement avant la fin de l'analyse. Toutefois, dans les situations suivantes, une nouvelle analyse n'est pas soumise à nouveau et les résultats précédents sont utilisés :
  * L'étape de traitement était toujours en cours d'exécution lorsque vous avez démarré une nouvelle analyse.
  * Un examen était déjà soumis pour la génération.
  * Une nouvelle génération de source n'a pas encore été exécutée.

5. Pour démarrer une nouvelle analyse, exécutez l'une des étapes suivantes :
  * Exécutez l'étape de génération qui entre dans l'étape de traitement, puis relancez l'exécution de l'étape de traitement.
  * Ouvrez l'URL des résultats de l'examen, puis cliquez sur l'icône **Corbeille**. Ensuite, relancez l'étape de traitement.

Exemples de sortie dans la console :

**Examen réussi**
![Exemple d'examen réussi](images/analyzer_success.png)

**Examen en attente**
![Exemple d'examen en attente](images/analyzer_pending.png)

Pour plus d'informations sur l'utilisation du service Static Analyzer, [voir les documents sur le service Static Analyzer](https://console.ng.bluemix.net/docs/services/ApplicationSecurityonCloud/index.html).

<!--

## Globalizing strings by using the pipeline
{: #deliverypipeline_globalize}

You can translate strings automatically into other languages when you use the IBM Globalization Pipeline service with your pipeline. IBM Globalization Pipeline uses machine translation to translate your source files as part of the pipeline's build and deployment process.

You can also update the machine-translated strings within the globalization project. A translator or native speaker of the language can then review the machine-translated strings to ensure that they are of a high quality.

To see an example of a typical pipeline that uses the Globalization Pipeline service, watch this video:

<iframe width="640" height="360" src="https://www.youtube.com/embed/UToj7FIomCg?feature=player_embedded" frameborder="0" allowfullscreen></iframe>

### Creating a globalization stage and job
Before you begin:

1. All English-translatable strings should be included in one or more `filename_en.properties` or `filename_en.json` files that all use the same name. For example: `messages_en.properties`.

2. If your messages are in `.json` files, remove the depth from the structure by removing any subkeys. To remove the subkeys, change instances of `{key: {subkey: value, subkey:value}}` to `{key:value, key:value}`.

To create the globalization stage and job:

1. Create a globalization stage.

  a. Click **ADD STAGE**.

  b. Name the stage; for example, `Globalization`.

  c. For the input type, select **SCM repository**.

2. In the globalization stage, add a job to translate the source files.

  a. On the **JOBS** tab, click **ADD JOB**.

  b. For the job type, select **Build**.

  c. For the builder type, select **IBM Globalization Pipeline**.

  d. For the organization and space, verify the values and update them if needed.

  e. In the **Source file name** field, type the name and extension of the `.properties` or `.json` input file. If you have files in different subdirectories, but they all have the same name, you need to type the file name once only. For example, if you have a `messages_en.properties` file in three directories, type `messages_en.properties` for the source file name, and all files with that name will be translated.

  f. Determine whether to select the **Set up service and space for me** check box.

    * If you want the pipeline to check your Bluemix space for the service and an app that binds the service to the container, select this check box. If the service or bound app does not exist, the pipeline adds the free plan of the service to your space for you. The bound app that is created is named `pipeline_bridge_app`. Then, the pipeline uses the credentials from pipeline_bridge_app to access the bound services.

    * If you configured the service and bound app in your Bluemix space already or if you want to [configure these requirements manually](https://www.ng.bluemix.net/docs/containers/container_group_pipeline_ov.html#container_binding_pipeline), leave this check box cleared.

  g. For the Globalization bundle prefix, enter a prefix for the bundle name, which is structured in this format: `<globalization_bundle_prefix>.path.to.source.file`. The pipeline job creates this Globalization bundle for you in the Globalization Pipeline service.

    **Tip:** Use the DevOps Services project name in the prefix so that the project can be identified easily in the Globalization Pipeline service.

  h. Click **SAVE**.

3. Create another stage to package your app. For the input of the job in this stage, use the IBM Globalization Pipeline job from the previous stage. Do not use the source as the input. The Globalization Pipeline job augments the source files with the machine-translated strings.

4. To ensure that the machine-translated content is included in the packaged app, create another stage to package the app in. For the input to that stage, include the Globalization Pipeline job.

The machine translated files are placed in the same directory as the source `.properties` or `.json` file. To view the files, click **Job > Artifacts**.

After the stage is completed, you can review the translated files from the console output. You can also direct translators to the files so that they can review the machine-translation output and provide revisions to improve quality. The revisions are stored in a Cloudant™ database and take precedence over any future machine translations of the same strings.

For more information about using the Globalization Pipeline service from the Bluemix Dashboard, [see the Globalization Pipeline service documentation](https://www.ng.bluemix.net/docs/services/GlobalizationPipeline/index.html).

-->

## Création de notifications Slack pour les générations dans le pipeline
{: #deliverypipeline_slack}

Vous pouvez envoyer des notifications sur les résultats de génération d'IBM Container Service, d'IBM Security Static Analyzer et d'IBM Globalization depuis votre service Delivery Pipeline vers vos canaux Slack.

Avant de commencer, créez une URL webhook Slack ou copiez-en une qui existe :

1. Ouvrez la page Slack Integration pour votre équipe : `https://_project_name_.slack.com/services`
2. Dans la liste des intégrations, localisez **Incoming WebHooks** et cliquez sur **Add**.
3. Sélectionnez un canal et cliquez sur **Add Incoming WebHooks Integration**.
4. Ajoutez une **URL webhook** ou copiez-en une qui existe.

Pour plus d'informations, [voir la rubrique Incoming WebHooks dans la documentation Slack](https://api.slack.com/incoming-webhooks).

Pour créer des notifications Slack :

1. Dans le pipeline, ouvrez la configuration pour une étape.
2. Dans l'onglet **Propriétés d'environnement**, cliquez sur **Ajouter une propriété**.
3. Sélectionnez **Propriété de texte**.
4. Entrez le nom et une valeur pour la propriété d'environnement. Répétez l'opération afin de créer plusieurs propriétés d'environnement.

  *Tableau 1. Propriétés d'environnement pour la configuration de notifications Slack*

  <table>
  <tr>
  <th>Nom</th>
  <th>Valeur</th>
  <th>Description</th>
  <tr/>
  <tr>
    <td><code>SLACK_WEBHOOK_PATH</code></td>
    <td>Adresse URL</td>
    <td>Requis. URL webhook qui est sauvegardée dans les paramètres de votre projet Slack.</td>
  </tr>
  <tr>
    <td><code>SLACK_COLOR</code></td>
    <td>Vous pouvez entrer l'une des valeurs suivantes :
      <ul><li><code>good</code></li>
      <li><code>warning</code></li>
      <li><code>danger</code></li>
      <li>N'importe quel code hexadécimal, par exemple, #439FEO</li></ul></td>
    <td>Facultatif. Couleur de la bordure qui s'affiche le long du message dans Slack. Les couleurs par défaut sont vert pour les messages de succès, rouge pour les messages d'erreur et gris pour les messages d'information.</td>
  </tr>
  <tr>
    <td><code>NOTIFY_FILTER</code></td>
    <td>Pour recevoir un sous-ensemble seulement des types de message, entrez l'une des valeurs suivantes :
      <ul>
      <li><code>good</code> : Pour afficher uniquement les messages d'information, de succès et inconnus. Les messages d'erreur ne sont pas envoyés.</li>
      <li><code>bad</code> : Pour afficher tous les messages.</li>
      <li><code>info</code> : Pour afficher uniquement les messages d'information. Les messages de succès, d'erreur et inconnus ne sont pas envoyés.</li>
      <li><code>unknown</code> : Pour afficher tous les messages.</li></ul>
      Exemple : Si vous définissez <code>NOTIFY_FILTER = bad</code>, des notifications d'erreur s'affichent uniquement dans le canal Slack.</td>
    <td>Facultatif. Décidez quel type de message pour lequel envoyer des notifications. Par défaut, les messages de succès et d'erreur
sont envoyés, mais pas les messages d'information.
      <ul><li><code>good</code> : résultats de génération positifs.</li>
      <li><code>bad</code> : résultats de génération négatifs.</li>
      <li><code>info</code> : messages d'information sur le processus de génération.</li>
      <li><code>unknown</code> : aucun type n'est associé aux messages inconnus.</li></ul></td>
   </table>

5. Cliquez sur **Sauvegarder**.

6. Répétez ces étapes afin d'envoyer des notifications Slack pour d'autres étapes incluant des travaux IBM Container Service, IBM Security Analyzer et IBM Globalization.

La notification de génération affichée dans Slack inclut un lien vers le projet des services DevOps et parfois vers le tableau de bord du projet. Pour qu'un utilisateur Slack puisse ouvrir ces liens, il doit être enregistré auprès des services DevOps et être membre du projet dans lequel le pipeline est configuré.

## Création de notifications HipChat pour les générations dans le pipeline
{: #deliverypipeline_hipchat}

Vous pouvez envoyer des notifications sur les résultats de génération d'IBM Container Service, d'IBM Security Static Analyzer et d'IBM Globalization depuis votre service Delivery Pipeline vers vos salles HipChat.

Avant de commencer, créez un jeton HipChat ou copiez-en un qui existe :

1. Accédez à la page HipChat Account pour votre compte : `https://_project_name_.hipchat.com/account/api`
2. Créez un jeton ou utilisez-en un qui existe.

Pour créer des notifications HipChat, procédez comme suit :

1. Dans le pipeline, ouvrez la configuration pour une étape.
2. Dans l'onglet **Propriétés d'environnement**, cliquez sur **Ajouter une propriété**.
3. Sélectionnez **Propriété de texte**.
4. Entrez le nom et une valeur pour la propriété d'environnement. Répétez l'opération afin de créer plusieurs propriétés d'environnement.

  *Tableau 2. Propriétés d'environnement pour la configuration de notifications HipChat*

  <table>
  <tr>
  <th>Nom</th>
  <th>Valeur</th>
  <th>Description</th>
  </tr>
  <tr>
    <td><code>HIP_CHAT_TOKEN</code></td>
    <td>Chaîne alphanumérique</td>
    <td>Requis. Voir la rubrique "Avant de commencer" pour savoir comment créer un jeton HipChat en en copier un qui existe.</td>
  </tr>
  <tr>
    <td><code>HIP_CHAT_ROOM_NAME</code></td>
    <td>Nom de la salle</td>
    <td>Requis.</td>
  </tr>
  <tr>
    <td><code>HIP_CHAT_COLOR</code></td>
    <td>Entrez l'une des valeurs suivantes :
      <ul><li><code>yellow</code></li>
      <li><code>red</code></li>
      <li><code>green</code></li>
      <li><code>purple</code></li>
      <li><code>gray</code></li>
      <li><code>random</code></li></ul>
    </td>
    <td>Facultatif : Spécifiez la couleur d'arrière-plan et la couleur de bordure des notifications HipChat. Si vous définissez <code>HIP_CHAT_COLOR</code>, vous n'avez pas besoin de spécifier la couleur lorsque vous appelez le script.
     <p><code>-l notification_level</code></p> </td>
  </tr>
  <tr>
    <td><code>NOTIFICATION_COLOR</code></td>
    <td>Entrez l'une des valeurs suivantes :
      <ul><li><code>good</code></li>
      <li><code>danger</code></li>
      <li><code>info</code></li></ul>
    Cette variable s'applique aux couleurs de notification HipChat et Slack. Si vous spécifiez
<code>NOTIFICATION_COLOR</code>, vous n'avez pas besoin de spécifier <code>HIP_CHAT_COLOR</code> ou
<code>SLACK_COLOR</code>.</td>
    <td>Facultatif : Spécifiez la couleur d'arrière-plan et la couleur de bordure des notifications HipChat et Slack. Si vous définissez <code>NOTIFICATION_COLOR</code>, vous n'avez pas besoin de spécifier la couleur lorsque vous appelez le script.
     <p><code>-l notification_level</code></p> </td>
  </tr>
  <tr>
    <td><code>NOTIFICATION_LEVEL</code></td>
    <td>Entrez l'une des valeurs suivantes :
      <ul><li><code>good</code></li>
      <li><code>info</code></li>
      <li><code>bad</code></li></ul></td>
    <td>Facultatif : spécifiez le niveau de notification. Pour plus de détails sur les éléments déclenchant la notification, voir <code>NOTIFICATION_FILTER</code>.</td>
  </tr>
  <tr>
    <td><code>NOTIFICATION_FILTER</code></td>
    <td>Entrez l'une des valeurs suivantes :
      <ul><li><code>good</code></li>
      <li><code>info</code></li>
      <li><code>bad</code></li></ul>
    <td>Facultatif : spécifiez le niveau de filtre de notification. Des notifications sont envoyées lorsque
les paramètres suivants sont remplis :
      <ul><li><code>NOTIFICATION_FILTER = good</code> et <code>NOTIFICATION_LEVEL = bad</code>, <code>good</code> ou <code>unknown</code></li>
      <li><code>NOTIFICATION_FILTER = info</code> et <code>NOTIFICATION_LEVEL = bad</code>, <code>good</code>, <code>info</code> ou <code>unknown</code></li>
      <li><code>NOTIFICATION_FILTER = bad</code> et <code>NOTIFICATION_LEVEL = bad</code> ou <code>unknown</code></li>
      <li><code>NOTIFICATION_FILTER = unknown</code> et <code>NOTIFICATION_LEVEL = bad</code>, <code>good</code> ou <code>unknown</code></li></ul></td>
    </tr>
  </table>

5. Cliquez sur **Sauvegarder**.

6. Répétez ces étapes afin d'envoyer des notifications HipChat pour d'autres étapes incluant des travaux IBM Container Service, IBM Security Static Analyzer et IBM Globalization.

## Utilisation d'Active Deploy pour un déploiement sans durée d'immobilisation dans le pipeline
{: #deliverypipeline_activedeploy}

Vous pouvez automatiser le déploiement en continu de vos applications ou de vos groupes de conteneurs à l'aide du service IBM Active Deploy dans le service Bluemix DevOps Services Delivery Pipeline. Pour plus d'informations sur la mise en route, [voir la documentation Active Deploy](https://new-console.ng.bluemix.net/docs/services/ActiveDeploy/updatingapps.html#adpipeline).

## Génération et déploiement d'images de conteneur à l'aide du pipeline
{: #deliverypipeline_containers}

Vous pouvez automatiser vos générations d'application et vos déploiements de conteneur dans Bluemix à l'aide du service IBM Continuous Delivery Pipeline for Bluemix. Le service Delivery Pipeline dans DevOps prend en charge :
  - La génération d'images Docker
  - Le déploiement d'images de conteneurs sur Bluemix

Pour plus d'informations sur la mise en route, voir [la présentation de Delivery Pipeline et des conteneurs](https://new-console.ng.bluemix.net/docs/containers/container_pipeline_ov.html#container_pipeline_ov).
