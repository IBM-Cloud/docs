---

copyright:
  years: 2015, 2017
lastupdated: "2017-4-7"

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

#Incorporation d'un flux de trame d'information Déployer dans {{site.data.keyword.Bluemix_notm}}
{: #embed-d2bm-iframe}


Vous pouvez incorporer le flux Déployer dans {{site.data.keyword.Bluemix_notm}}
en tant trame d'information dans divers types de contenu prenant en charge le balisage. Par exemple,
vous pouvez incorporer la trame d'information dans des fichiers Readme, des blogues, des articles et des pages Web.

{: shortdesc}

Le flux de trame d'information est utile si vous voulez gérer l'image de marque de votre entreprise. Lorsque des personnes cliquent sur votre trame d'information incorporée, elles restent dans votre contenu au lieu d'être redirigées vers le site Web bluemix.net. Si vous ne vous préoccupez pas de l'image de marque de votre entreprise, vous
pouvez insérer un bouton [Déployer
dans {{site.data.keyword.Bluemix_notm}}](/docs/develop/deploy_button.html) standard dans votre
contenu à la place de la trame d'information.

##Etapes du flux de trame d'information {: #iframe-steps}

1. Si vous ne disposez pas d'un compte {{site.data.keyword.Bluemix_notm}} actif,
créez un compte d'essai.

2. Vous pouvez sélectionner une région, une organisation (org), un espace et un nom d'application. Le nom d'application suggéré est construit à partir du
nom d'application précédent, de votre nom d'utilisateur et de l'heure.

3. La branche principale du référentiel Git public d'origine est clonée dans un nouveau projet
{{site.data.keyword.jazzhub_short}} privé avec un nouveau référentiel Git.

4. Si l'application requiert un fichier de génération, le fichier de génération est détecté automatiquement et l'application est générée.

5. L'application est déployée dans votre organisation {{site.data.keyword.Bluemix_notm}}.

##Exemple de flux de trame d'information {: #iframe-example}

<p>
L'<a class="xref" href="http://d2bm-iframe-sample.ng.bluemix.net/" target="_blank" title="(s'ouvre dans un nouvel onglet ou une nouvelle fenêtre)">exemple IBM Bluemix D2BM iFrame<img class="image" src="../icons/launch-glyph.svg" alt="External link icon"/></a> fournit un exemple de flux de trame d'information pour un référentiel Git public.<div class="image"><img class="image" src="images/d2bm_iframe_sample2.png" alt="Exemple de flux de trame d'information Déployer dans Bluemix" /></div>
</p>

<p>
Pour afficher la source de cet exempke, cliquez sur <a class="xref" href="https://hub.jazz.net/project/idsorg/d2bm-iframe-sample/overview" target="_blank" title="(s'ouvre dans un nouvel onglet ou une nouvelle fenêtre)">source<img class="image" src="../icons/launch-glyph.svg" alt="External link icon"/></a>.
</p>

##Incorporation du flux de trame d'information {: #embed-iframe}  

<ol>
<li>Chargez l'utilitaire JavaScript depuis <a class="xref" href="https://bluemix.net/deploy/embed.js" target="_blank" title="(s'ouvre dans un nouvel onglet ou une nouvelle fenêtre)">https://bluemix.net/deploy/embed.js<img class="image" src="../icons/launch-glyph.svg" alt="External link icon"/></a>. Cet utilitaire dépend de jQuery. Pour le charger, ajoutez la balise de script suivante à votre document :
<pre class="pre">
<code>&lt;script type="text/javascript" src="https://bluemix.net/deploy/embed.js"&gt;&lt;/script&gt;</code>
</pre>
</li>
<li> Instanciez le constructeur <code>DeployToBluemixIFrame</code> en utilisant les arguments suivants :

<dl class="parml">
<dt class="pt dlterm">domNodeId</dt>
<dd class="pd">ID du noeud domNode dans lequel insérer la trame d'information à votre contenu.</dd>

<dt class="pt dlterm">callback</dt>
<dd class="pd">Cet argument est appelé lorsque le flux de trame d'information est terminé ou si une erreur se produit. L'argument répond avec un résultat. Le fragment de code suivant indique un rappel de résultat ayant abouti :</dd>

<dt class="pt dlterm">args</dt>
<dd class="pd">Objet contenant les paramètres d'entrée au widget. Les paramètres suivants sont disponibles :

<dl class="parml">

<dt class="pt dlterm">repository</dt>
<dd class="pd">Référentiel Git à utiliser comme source pour le clonage et le déploiement. Cette valeur est obligatoire.</dd>

<dt class="pt dlterm">app_name</dt>
<dd class="pd">Nom d'application par défaut à utiliser comme valeur spécifiée dans la zone <strong>app_name</strong>
de la trame d'information. Cette valeur est facultative.</dd>


<dt class="pt dlterm">region_id</dt>
<dd class="pd">ID de la région cible par défaut. Par exemple : <code>ibm:yp:us-south</code>. Cette valeur est facultative.</dd>

<dt class="pt dlterm">organization_guid</dt>
<dd class="pd">Identificateur global unique de l'organisation cible par défaut. Pour trouver cette valeur, cliquez sur <strong>Gérer les organisations</strong> > <i>nom_organisation</i>. L'URL de l'organisation contient l'identificateur global unique de cette organisation. Cette valeur est facultative.</dd>

<dt class="pt dlterm">space_guid</dt>
<dd class="pd">Identificateur global unique de l'espace cible par défaut. Pour trouver cette valeur, cliquez sur <strong>Gérer les organisations</strong> >
<i>nom_espace</i>. L'adresse URL de l'espace contient l'identificateur global unique de cet espace. Cette valeur est facultative.</dd>

<dt class="pt dlterm">auto_login</dt>
<dd class="pd">Indique si la trame d'information connecte automatiquement l'utilisateur. La valeur
par défaut est <code>true</code>. Cette valeur est facultative.</dd>

<dt class="pt dlterm">width</dt>
<dd class="pd">Largeur de la trame d'information. Cette valeur est facultative. La valeur par défaut
est <code>620</code>.</dd>

<dt class="pt dlterm">height</dt>
<dd class="pd">Hauteur de la trame d'information. Cette valeur est facultative. La valeur par défaut
est <code>470</code>.</dd>
</dl>

</dd>
</dl>
</li>
</ol>  

**Astuce :** pour minimiser l'interaction avec la trame d'information, vous pouvez préremplir les zones **app_name**, **region_id**, **organization_guid**, **space_guid** et **auto_login**.
