---

copyright:
  years: 2016
lastupdated: "2016-06-21"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Utilisation de l'environnement JRE Oracle
{: #using_oraacle_jre}

Vous pouvez exécuter votre application Liberty sur Bluemix avec l'environnement JRE Oracle, si vous le voulez.  Pour ce faire, vous devez :
* héberger l'environnement JRE dans un emplacement à partir duquel le pack de construction peut le télécharger,
* héberger un fichier index.yml qui fournit l'emplacement de l'environnement d'exécution hôte, et
* configurer votre application pour utiliser cet environnement JRE.

## Hébergement de l'environnement JRE et du fichier index.yml
{: #hosting_jre}

Le fichier JRE Oracle doit être hébergé sur un serveur Web et le pack de construction Liberty doit être en mesure de le télécharger depuis ce serveur. Vous pouvez l'héberger directement sur Bluemix à l'aide des fonctions disponibles sur le serveur, ou vous pouvez l'héberger sur un emplacement disponible publiquement.  Le serveur doit être configuré avec un fichier index.yml qui spécifie les détails relatifs au fichier JRE. Procédez comme suit pour héberger l'environnement JRE et le fichier index.yml :
  1. Procurez-vous l'environnement JRE Oracle.  Notez que ce dernier doit être la version à utiliser sur un système d'exploitation Unix 64 bits, et être un fichier tar.gz.
  2. Hébergez le fichier JRE dans un emplacement à partir duquel le pack de construction Liberty peut le télécharger. 
  3. Prenez soin de fournir un fichier index.yml à l'emplacement d'hébergement. Le fichier index.yml doit contenir une entrée composée de l'ID de version de l'environnement JRE Oracle suivi d'un signe deux-points et de l'URL complète de l'emplacement de ce fichier JRE. Le format du fichier index.yml est :
```
   ---
   jre_version: https://hostingLocation/jreName.tar.gz
```
{: codeblock}

    * Par exemple :
    ```
       ---
       1.8.0_91: https://myHostingApp.ng.bluemix.net/jre-8u91-fcs-bin-b14-linux-x64-01_apr_2016.tar.gz
    ```

## Configuration de l'application
{: #configure_app}

Deux variables d'environnement doivent être définies sur l'application Liberty. La variable *JBP_CONFIG_OPENJDK* doit être définie pour spécifier l'emplacement du fichier index.yml et la variable d'environnement *JVM* doit être définie sur *openjdk* pour configurer le pack de construction afin qu'il se serve d'un environnement JRE alternatif.

Pour la variable JBP_CONFIG_OPENJDK, la valeur est
```
   'repository_root: "https://locationToIndexYml"'
```
{: codeblock}

Pour définir ceci, vous pouvez émettre une commande comme celle-ci :
```
   $ cf se myApp JBP_CONFIG_OPENJDK 'repository_root: https://myHostingApp.ng.bluemix.net'
```
{: codeblock}

Notez que l'URL *repository_root* n'inclut pas index.yml, mais s'arrête juste avant son emplacement.

Pour définir la variable d'environnement JVM, émettez une commande comme celle-ci :
```
   $ cf se myApp JVM 'openjdk'
```
{: codeblock}

**Remarque** : vous devez reconstituer votre application après avoir défini les variables d'environnement.

## Confirmation
{: #confirmation}

Pour confirmer que l'environnement JRE est utilisé, cherchez dans staging_task.log un message similaire à celui ci-dessous :
```
   -----> Downloading OpenJdk 1.8.0_91 from https://myHostingApp.ng.bluemix.net/jre-8u91-fcs-bin-b14-linux-x64-01_apr_2016.tar.gz (6.2s)
```
{: codeblock}

# rellinks
{: #rellinks}
## general
{: #general}
* [Environnement d'exécution Liberty](index.html)
* [Présentation de Liberty Profile](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
