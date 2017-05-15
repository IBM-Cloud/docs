---

copyright:
  years: 2015, 2017
lastupdated: "2016-10-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Migration des données de ressources depuis la version bêta
{: #globalizationpipeline_betaresourcedatamigration}

La version bêta de {{site.data.keyword.GlobalizationPipeline_full}} prendra fin au terme d'un certain délai après la publication de la version GA. Les données utilisateur des instances bêta ne seront pas déplacées vers les instances de service GA. Pour conserver les données après la publication de la version GA, vous pouvez exporter les données de ressources dans des fichiers, puis les importer dans la nouvelle instance. Notez que vous ne pouvez pas effectuer cette opération à l'aide du tableau de bord de service. En outre, l'exportation des données de ressources dans l'un des formats de fichier de ressources ne préserve pas les autres métadonnées associées aux entrées de ressource.

Pour assurer la prise en charge de la migration de données depuis la version bêta vers la version GA, une fonction a été ajoutée à l'outil de ligne de commande Java de {{site.data.keyword.GlobalizationPipeline_short}}. La source de l'outil est hébergée à l'adresse https://github.com/IBM-Bluemix/gp-java-tools et son édition binaire sera également disponible dans le répertoire github. L'instantané de développement le plus récent est publié. [Téléchargez-le.](https://w3-connections.ibm.com/communities/service/html/communityview?communityUuid=589d87cf-d0c7-4e06-ab95-4108547f90aa#fullpageWidgetId=Wa22bb771e29b_4aa9_a114_cfe53fda2cc8&file=5cdaf089-ec7c-4881-b5a0-7ab651491237)

L'outil utilise une API REST développée après la version bêta pour le ***téléchargement des entrées de ressource***, par conséquent, l'instance de service de destination doit correspondre à la version GA. 
* Source : bêta ou GA
* Destination : GA uniquement

Pour copier toutes les données de bundle d'une instance de service de globalisation dans une autre instance, utilisez la commande ci-dessous :

```> java -jar gp-cli.jar copy-all-bundles -s <source-service-url> -i <source-instance-id> -u <source-user-id> -p <source-password> --dest-url <dest-service-url> --dest-instance-id <dest-instance-id> --dest-user-id <dest-user-id> --dest-password <dest-password>```


`source/target-service-url` et les autres valeurs de paramètre figurent dans les données d'identification du service source/de destination. Par exemple : 

```
{
  "gp-beta": [
    {
      "name": "Globalization Pipeline-7x",
      "label": "gp-beta",
      "plan": "gp-beta-plan",
      "credentials": {
 

      "url": "https://gp-beta-rest.ng.bluemix.net/translate/rest",
        "userId": "bd0b84362c6934d222c3a0a40fc1443b",
        "password": "OGxp6jDqCLCL1ui8kQSPTt1mZDi4EQwu",
        "instanceId": "bd0b84362c6934d222c3a0a40fc1233e"
      }
    }
  ]
}
```
De plus, toute l'interface CLI GP est mise à jour pour prendre en charge les données d'identification au format JSON en plus des options individuelles `(-s / -i / -u / -p)`. Vous pouvez créer un fichier JSON avec du contenu, tel que celui illustré ci-dessous : 

creds.json 
```
 {

        "url": "https://gp-rest.stage1.ng.bluemix.net/translate/rest",
        "userId": "36cad58b3a65dc9fe0183208305be137",
        "password": "43F9MRMu9Q8BWRXMLctunUsAe8LTdwq1",
        "instanceId": "b157e3fc63e62d76c50d9f689d7fc965"

} 
```
Ensuite, vous pouvez spécifier le fichier à l'aide de `-j <json-file>`. Dans la commande `copy/copy-all-bundles`, vous pouvez remplacer

```-s https://gp-rest.stage1.ng.bluemix.net/translate/rest -i b157e3fc63e62d76c50d9f689d7fc965 -u 36cad58b3a65dc9fe0183208305be137 -p 43F9MRMu9Q8BWRXMLctunUsAe8LTdwq1```

par

`-j creds.json `
 
Vous pouvez aussi copier bundle d'un emplacement à un autre à l'aide de la commande suivante : 

```> java -jar gp-cli.jar copy -s <source-service-url> -i <source-instance-id> -u <source-user-id> -p <source-password> -b <source-bundle-id> --dest-url <dest-service-url> --dest-instance-id <dest-instance-id> --dest-user-id <dest-user-id> --dest-password <dest-password> -d <dest-bundle-id>```


**Remarque :** Vous pouvez utiliser les paramètres `-b <source-bundle-id>` et `-d <dest-bundle-id>` en plus de ceux utilisés pour la commande copy-all-bundles. Cette commande peut être utilisée pour copier un bundle au sein d'une même instance. Dans ce cas, vous pouvez supprimer les paramètres de données d'identification de service de destination `(--dest-*)`.


Les commandes ci-dessus extraient des données de bundle et des données d'entrée de ressource existantes, puis les téléchargent vers le nouvel emplacement. Au cours du processus, certaines zones contrôlées par le serveur REST seront mises à jour (par exemple, la zone updatedBy/updatedAt). En outre, dans la mesure où ces commandes ne copient pas les données de configuration et de liaison de service, vous serez peut-être amené à configurer des services de traduction automatique dans l'instance de destination.


Ainsi, la version bêta prend en charge la traduction en langue arabe via Watson Language Translator. Dans la version GA, la traduction en langue arabe n'est plus proposée gratuitement. Lorsque vous portez des données bêta vers la nouvelle instance GA, le contenu en langue arabe déjà traduit est préservé. Aucune modification de la langue source ne déclenche automatiquement la traduction en langue arabe, sauf si vous configurez la liaison Watson de façon à activer la traduction en langue arabe. Cela est également vrai lorsque l'instance source est au niveau de la version GA. La liaison de service de traduction automatique externe est propre à une instance GP ; la configuration/liaison vers une autre instance n'est pas portée automatiquement. 

