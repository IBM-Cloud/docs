---

 

copyright:

  2015，2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Utilisation des packs de construction intégrés de la communauté
*Dernière mise à jour : 15 mars 2016*

Si vous ne trouvez pas de module de démarrage qui offre le contexte d'exécution dont vous avez besoin dans le catalogue {{site.data.keyword.Bluemix}}, vous pouvez fournir un
pack de construction externe dans {{site.data.keyword.Bluemix_notm}}. Vous pouvez spécifier un pack de construction personnalisé et compatible avec Cloud Foundry lorsque vous déployez votre application avec la commande cf
push.
{:shortdesc}

Des packs de construction externes qui sont fournis par la communauté Cloud Foundry sont à votre disposition. Avant de déployer votre application dans {{site.data.keyword.Bluemix_notm}}, assurez-vous d'avoir installé
l'interface de ligne de commande cf.

**Remarque :** les packs de construction externes ne sont pas fournis par IBM ; par conséquent, si vous avez besoin d'aide, prenez
contact avec la
communauté Cloud Foundry.

## Packs de construction intégrés de la communauté

Dans {{site.data.keyword.Bluemix_notm}}, vous pouvez utiliser des packs de construction
intégrés fournis par la communauté Cloud Foundry. Pour afficher la liste des packs de construction intégrés de la communauté, exécutez la commande cf
buildpacks :

```
cf buildpacks
Getting buildpacks...

buildpack      position   enabled   locked   filename
...
java_buildpack     7      true      false    buildpack_java_v2.0.2.zip
ruby_buildpack     8      true      false    buildpack_ruby_v46-245-g2fc4ad8.zip
nodejs_buildpack   9      true      false    buildpack_nodejs_v8-177-g2b0a5cf.zip
```
{:screen}

<ul>

<li>
Dans le cas d'un contexte d'exécution ou d'une infrastructure identique, les packs de construction créés par IBM sont prioritaires sur ceux de la
communauté. Si vous voulez utiliser le pack de construction de la communauté à la place de celui créé par IBM, vous devez le spécifier à l'aide de l'option
-b de la commande cf push.
<p>Par exemple, vous pouvez utiliser le pack de construction de la communauté pour les applications Web Java. :</p>
<pre class="pre"><code>cf push nom_app -b pack_construction_java -p chemin_app</code></pre>
<p>Vous pouvez également utiliser le pack de construction de la communauté pour les applications Node.js :</p>
<pre class="pre"><code>cf push nom_app -b pack_construction_nodejs -p chemin_app</code></pre>
</li>

<li>
<p>Dans le cas d'un contexte d'exécution ou d'une infrastructure non pris en charge par les packs de construction créés par IBM, mais pris en charge par
les packs de construction intégrés de la communauté, il n'est pas nécessaire d'utiliser l'option -b avec la commande cf push.</p><p>Par exemple, pour des
applications Ruby, il n'existe aucun pack de construction créé par IBM. Pour utiliser le pack de construction intégré de la communauté, saisissez la commande suivante :</p>
<pre class="pre"><code>cf push nom_app -p chemin_app</code></pre>
</li>
</ul>

## Packs de construction externes

Vous pouvez utiliser des packs de construction externes ou personnalisés dans {{site.data.keyword.Bluemix_notm}}. Vous devez spécifier
l'adresse URL du pack de construction avec l'option -b et la pile avec l'option ```-s``` dans la commande **cf push**. Par exemple, pour utiliser un pack de construction de communauté externe pour des fichiers statiques, exécutez la commande suivante :

```
cf push nom_app -p chemin_app -b https://github.com/cloudfoundry-incubator/staticfile-buildpack.git -s cflinuxfs2
```
{:pre}

Ou bien, si vous ne souhaitez pas
utiliser ce pack de construction pour les applications Ruby, vous pouvez employer le pack de construction externe en entrant la commande suivante :

```
cf push nom_app -p chemin_app -b https://github.com/cloudfoundry/heroku-buildpack-ruby -s cflinuxfs2
```
{:pre}

Vous pouvez aussi utiliser un pack de
construction personnalisé pour votre application. Par exemple, pour utiliser un pack de construction PHP open source fourni par la communauté Cloud
Foundry, entrez la commande suivante lors du déploiement de l'application PHP dans Bluemix pour spécifier l'adresse URL du référentiel Git du pack de
construction :

```
cf push nom_app -p chemin_app -b https://github.com/dmikusa-pivotal/cf-php-build-pack -s cflinuxfs2
```
{:pre}

## Spécification de la version de pack de construction Java

<ul>
<li>
Utilisez la commande <strong>cf set-env</strong>. Par exemple, entrez la commande suivante pour définir la version Java 1.7.0 :
<pre class="pre"><code>cf set-env nom_app JBP_CONFIG_OPEN_JDK_JRE &#39;{jre: { version: 1.7.0_+ }}&#39;</code></pre>
<p>Ensuite, reconstituez votre application pour appliquer
la modification :</p>
<pre class="pre"><code>cf restage nom_app</code></pre>
</li>
<li>
Utilisez le fichier <code>manifest.yml</code>. Vous pouvez ajouter la variable d'environnement et la valeur que vous voulez spécifier
directement dans le fichier. Pour des informations détaillées, voir
la rubrique relative aux <a href="https://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html#env-block">variables
d'environnement</a>.</li></ul>
  

