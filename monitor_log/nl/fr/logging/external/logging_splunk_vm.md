---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Exemple : transmission des journaux d'application Cloud Foundry à Splunk
{: #splunk}

Dans cet exemple, un développeur nommé Jeanne crée un serveur virtuel à l'aide d'IBM Virtual Servers Beta et de l'image Ubuntu.  Jeanne tente de transmettre
les journaux d'application Cloud Foundry de {{site.data.keyword.Bluemix_notm}} à Splunk.
{:shortdesc}

  1. Pour commencer, Jeanne configure Splunk.

     a. Jeanne télécharge Splunk Light depuis le site [Download Splunk Light site ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://www.splunk.com/en_us/download/splunk-light.html){:new_window}, puis l'installe à l'aide de la commande suivante. Le logiciel est installé sous */opt/splunk*.

	    ```
        dpkg -i  ~/splunklight-6.3.0-aa7d4b1ccb80-linux-2.6-amd64.deb
        ```

     b. Jeanne installe et adjoint le module complémentaire RFC5424 de la technologie syslog pour son intégration avec
{{site.data.keyword.Bluemix_notm}}. Pour plus d'informations sur les instructions d'installation du module complémentaire, voir les [directives Cloud Foundry ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://docs.cloudfoundry.org/devguide/services/integrate-splunk.html){:new_window}.

	    Jeanne installe le module complémentaire via les commandes suivantes :

	    ```
        cd /opt/splunk/etc/apps
        tar xvfz ~/rfc5424-syslog_11.tgz
        ```

        Jeanne associe le module complémentaire en remplaçant */opt/splunk/etc/apps/rfc5424/default/transforms.conf* par un nouveau
fichier *transforms.conf* contenant le texte suivant :

	    ```
        [rfc5424_host]
        DEST_KEY = MetaData:Host
        REGEX = <\d+>\d{1}\s{1}\S+\s{1}(\S+)
        FORMAT = host::$1

        [rfc5424_header]
        REGEX = <(\d+)>\d{1}\s{1}\S+\s{1}\S+\s{1}(\S+)\s{1}(\S+)\s{1}(\S+)
        FORMAT = prival::$1 appname::$2 procid::$3 msgid::$4
        MV_ADD = true
        ```
        {:screen}

     c. Une fois Splunk configuré, Jeanne doit ouvrir certains ports sur la machine Ubuntu pour accepter le flux syslog entrant
(port 5140) et l'interface utilisateur Web de Splunk (port
8000) vu que, par défaut, le pare-feu est en place sur le serveur virtuel {{site.data.keyword.Bluemix_notm}}.

	    **Remarque :** la configuration iptable est réalisée ici à des fins d'évaluation par Jeanne et n'est que temporaire. Pour configurer le paramètre de pare-feu dans le serveur virtuel Bluemix en environnement de production, voir la documentation sur les [groupes de sécurité des réseaux ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://new-console.ng.bluemix.net/docs/services/networksecuritygroups/index.html){:new_window} pour plus d'informations. 

	   ```
	   iptables -A INPUT -p tcp --dport 5140 -j ACCEPT
       iptables -A INPUT -p tcp --sport 5140 -j ACCEPT
       iptables -A INPUT -p tcp --dport 8000 -j ACCEPT
       iptables -A INPUT -p tcp --sport 8000 -j ACCEPT
	   ```
	   {:screen}

	   Jeanne lance ensuite Splunk à l'aide de la commande suivante :

       ```
	   /opt/splunk/bin/splunk start --accept-license
       ```

  2. Jeanne configure les paramètres Splunk afin d'accepter le flux syslog de {{site.data.keyword.Bluemix_notm}}. Elle doit créer une entrée de données
pour le flux syslog.

     a. Depuis l'interface Web Splunk, Jeanne clique sur **Data > Data inputs**. Une liste des types d'entrées pris en
charge par Splunk s'affiche.

     b. Elle sélectionne **TCP** vu que le flux syslog utilise ce protocole.

     c. Dans le panneau **TCP**, elle entre **5140** dans la zone **Port**, en laissant vides
les autres zones, puis clique sur **Next**.

     d. Dans la liste **Source Type**, elle sélectionne **Uncategorized > rfc5424_syslog**.

     e. Pour le type **Method**, elle sélectionne **IP**.

     f. Dans la zone **Index**, Jeanne clique sur **Create a new index**. Elle nomme le nouvel index
"bluemix", puis clique sur **Save**.

     g. Enfin, dans la fenêtre **Review**, Jeanne confirme que le paramètre est correct, puis clique sur
**Submit** pour activer cette entrée de données.

  3. Dans {{site.data.keyword.Bluemix_notm}}, Jeanne crée un service de flux syslog et le lie à une application.

     a. Jeanne crée un service de flux à l'aide de la commande suivante dans l'interface de ligne de commande cf :

     ```
     cf cups splunk -l syslog://dummyhost:5140
     ```

     **Remarque :** *dummyhost* n'est pas le nom réel. Il est utilisé pour masquer le nom d'hôte véritable.

     b. Jeanne lie le service de flux syslog à une application dans son espace, puis retransfère l'application.

	 ```
     cf bind-service monapp splunk
     cf restage monapp
     ```


Jeanne teste son application, puis entre la chaîne de requête suivante dans l'interface Web de Splunk :

```
source="tcp:5140" index="bluemix" sourcetype="rfc5424_syslog"
```

Jeanne observe un flux de journaux dans son interface Web Splunk. Bien qu'elle ait installé la version Splunk Light, Jeanne dispose toujours d'une capacité
de 500 Mo par jour pour ses journaux.

