---

Copyright :
  Années : 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Utilisation des fonctions bêta
{: #using_beta_features}

*Dernière mise à jour : 23 mars 2016*

Les fonctions bêta de Liberty sont destinées à faciliter l'accès aux nouvelles fonctionnalités et aux nouveaux modèles de programmation pouvant être intégrés dans une édition future de Liberty. La plupart des fonctions bêta peuvent également être utilisées dans des applications déployées sur Bluemix.

**Important** : Les fonctions bêta sont destinées à des fins de développement et de test et ne doivent pas être utilisées en
production. Pour connaître les conditions d'utilisation complètes de ces fonctions, voir le document relatif au [contrat de licence des versions bêta](http://public.dhe.ibm.com/ibmdl/export/pub/software/websphere/wasdev/downloads/wlp/beta/lafiles/en.html).

Fonctions bêta de Liberty disponibles dans Bluemix
<table>
<tr>
<th align="left">Fonction</th>
<th align="left">Fonction</th>
<th align="left">Fonction</th>
<th align="left">Fonction</th>
</tr>

<tr>
<td>cloudant-1.0</td>
<td>httpWhiteboard-1.0</td>
<td>osgiBundle-1.0</td>
<td>passwordUtilities-1.0</td>
</tr>
</table>

Pour utiliser les fonctions bêta de Liberty dans Bluemix, procédez de l'une des façons suivantes :

1. [Déployez un répertoire de serveur ou un package de serveur](optionsForPushing.html) avec une ou plusieurs fonctions bêta activées dans le fichier server.xml, comme dans l'exemple suivant :
```
    <server>
        <featureManager>
            <feature>jsp-2.3</feature>
            <feature>passwordUtilities-1.0</feature>
        </featureManager>
    </server>
```
{: #codeblock}

2.  Affectez à la variable d'environnement IBM_LIBERTY_BETA la valeur **true**. Cette variable indique au pack de construction Liberty qu'il doit installer et activer les fonctions bêta pour votre application.  Voir les exemples suivants :
  * Utilisation de l'outil de ligne de commande cf :
```
       $ cf set-env <yourappname> IBM_LIBERTY_BETA true
```
{: #codeblock}

  * Ou, utilisation du fichier manifest.yml :
```
      env:
          IBM_LIBERTY_BETA: "true"
```
{: #codeblock}

# rellinks
## general
* [Environnement d'exécution Liberty](index.html)
* [Présentation de Liberty Profile](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
