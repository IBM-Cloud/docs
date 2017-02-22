---

copyright:

  years: 2016, 2017

lastupdated: "2017-01-12"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Plug-in für privates Netzpeering für Bluemix CLI
{: #private_network_cli}

Sie können die Befehlszeilenschnittstelle (CLI) für privates Netzpeering zum Konfigurieren und Verwalten von privatem Netzpeering zwischen zwei {{site.data.keyword.Bluemix}}-Bereichen verwenden. Privates Netzpeering wird für IBM Containers (Docker-Containers) unterstützt. Die Bluemix-Bereiche können sich in unterschiedlichen Verfügbarkeitszonen derselben Region oder in verschiedenen Regionen befinden. Das CLI-Plug-in für privates Netzpeering steht für die Verwendung mit dem Bluemix CLI-Plug-in zur Verfügung.

Das CLI-Plug-in für privates Netzpeering steht für die Betriebssysteme Windows, MAC und Linux zur Verfügung. Stellen Sie sicher, dass Sie das für Sie geeignete Plug-in verwenden.

Bevor Sie beginnen, erstellen Sie Bluemix-Bereiche. Stellen Sie sicher, dass jeder Container eines Bereichs eine IP-Adresse aus einem anderen Netzwerk besitzt. Details hierzu finden Sie unter [Eigene private IP-Adresse verwenden](https://www.{DomainName}/docs/containers/container_security_network.html#container_cli_ips_byoip).

**Hinweis:** Wenn Sie das private Netzpeering mit einem Bluemix-Bereich verwendet haben und den Bereich löschen müssen, dann löschen Sie zuerst die Verbindungen für das private Netzpeering in diesem Bereich.

Zu Beginn installieren Sie IBM Bluemix CLI. Details hierzu finden Sie unter [Bluemix CLI](http://clis.ng.bluemix.net/ui/home.html).

## CLI-Plug-in für privates Netzpeering installieren

**Hinweis:** Wenn Sie eine Vorgängerversion des installierten Plug-ins besitzen, muss dieses deinstalliert werden. Zum Deinstallieren des Plug-ins verwenden Sie den folgenden Befehl:

```
bluemix plugin uninstall private-network-peering
```
### Lokal installieren
Laden Sie das Plug-in für privates Netzpeering für Ihre Plattform aus dem [Plug-in-Repository für die IBM Bluemix CLI](http://plugins.ng.bluemix.net/ui/repository.html#bluemix-plugins) herunter.

Installieren Sie das Plug-in für privates Netzpeering mit dem folgenden Befehl:

**Hinweis:** Wechseln Sie entweder zur Position des Plug-ins oder geben Sie sein Verzeichnis an.

* Für das Betriebssystem Microsoft Windows:

```
bluemix plugin install private-network-peering-windows-amd64.exe
```

* Für das Betriebssystem Apple MAC:

```
bluemix plugin install private-network-peering-darwin-amd64
```

* Für das Betriebssystem Linux:

```
bluemix plugin install private-network-peering-linux-amd64
```

**Hinweis:** Wenn während der Installation des Plug-ins für das Betriebssystem Linux eine Fehlernachricht angezeigt wird, dass die Genehmigung verweigert wird, dann führen Sie folgenden Befehl aus und ändern Sie die Berechtigungen:

```
chmod a+x ./private-network-peering-linux-amd64
```

### Installation aus dem Bluemix-Repository

Befolgen Sie diese Schritte, um das Plug-in aus dem Bluemix-Repository zu installieren:

1. Fügen Sie den Registry-Endpunkt für das Bluemix-Plug-in hinzu:
	```
	bluemix plugin repo-add bluemix-bx http://plugins.ng.bluemix.net
	```

2. Führen Sie den folgenden Befehl aus:

	```
	bluemix plugin install private-network-peering -r bluemix-bx
	```

## Liste der Befehle für das private Netzpeering
Folgende Befehle werden unterstützt. Verwenden Sie den Befehl `bluemix network`, um die Liste der verfügbaren Befehle anzuzeigen:

| Befehl     | Beschreibung                                    |
|-------------|------------------------------------------------|
| pnp-routers | Führt alle verfügbaren Router für das Peering auf.        |
| pnp-create  | Erstellt eine Verbindung für das private Netzpeering.   |
| pnp-delete  | Löscht eine Verbindung für das private Netzpeering.   |
| pnp-show    | Listet alle Verbindungen für das private Netzpeering auf.  |
{: caption="Table 1. Private network peering commands" caption-side="top"}


### Verwendung der Befehle
Zur Anzeige der Hilfeinformationen für die Befehle führen Sie folgenden Befehl aus: `bluemix network [command] -h`.

#### Auflisten aller verfügbaren Router für das Peering
```
bluemix network pnp-routers [--verbose (or -v)]
```

#####Optionale Parameter
{: #op1}

* **--verbose (or -v)** (Flag): Anzeigen ausführlicher Netzinformationen zu jedem Router.

######Beispiele für Befehle
{: #ex1}

Zum Anzeigen von Netzinformationen zu allen Routern:

	$ bluemix network pnp-routers
	Listing available routers ...
	OK

	IP              NAME            COMPUTE    REGION          ORGANIZATION    SPACE
	129.41.234.246  default-router  Container  US-South        ywu@us.ibm.com  demo1
	129.41.237.172  default-router  Container  US-South        ywu@us.ibm.com  demo2
	129.41.238.212  default-router  Container  United-Kingdom  ywu@us.ibm.com  demo3


Zum Anzeigen ausführlicher Netzinformationen zu allen Routern:


	$ bluemix network pnp-routers -v
	Listing available routers ...
	OK

	Router 'bce1aa25-bad0-4cf1-a831-d53c16463d06':
	FIELD          VALUE
	IP             129.41.234.246
	Name           default-router
	Compute        Container
	Region         US-South
	Organization   ywu@us.ibm.com
	Space          demo1
	Networks       172.31.0.0/16

	Router '9ea160f2-1a30-44cd-bd25-794d441b274b':
	FIELD          VALUE
	IP             129.41.237.172
	Name           default-router
	Compute        Container
	Region         US-South
	Organization   ywu@us.ibm.com
	Space          demo2
	Networks       172.25.0.0/16

	...


#### Erstellen eines privaten Netzpeerings unter Verwendung der IP-Adressen
```
bluemix network pnp-create <router_ip> <router_ip> <name>
```

#####Parameter
{: #p1}

* **router_ip**: IP-Adressen der zwei Router, die verbunden werden sollen. Sie können die IP-Adressen mit folgendem Befehl suchen: `bluemix network pnp-routers`
* **name**: Name der Verbindung des privaten Netzpeering.

######Beispiele für Befehle
{: #ex2}

	$ bluemix network pnp-create 129.41.234.246 129.41.237.172 demo
	Creating private network peering connection 'demo' ...
	Connecting 'default-router(129.41.234.246)' and 'default-router(129.41.237.172)' ...
	OK

	Private network peering connection 'demo' created.


####Erstellen eines privaten Netzpeerings unter Verwendung des Verbindungsnamens

```
bluemix network pnp-create -i <name>
```

#####Parameter
{: #p2}

* **--interactive (-i)** (Flag): Interaktiver Modus für die Router-Auswahl.
* **name**: Name der Verbindung des privaten Netzpeering.

######Beispiele für Befehle
{: #ex3}

	$ bluemix network pnp-create -i demo
	Creating private network peering connection 'demo' ...
	List of available routers (select TWO for peering):

	#  ROUTER                          COMPUTE    REGION          ORGANIZATION    SPACE
	1  default-router(129.41.234.246)  Container  US-South        ywu@us.ibm.com  demo1
	2  default-router(129.41.237.172)  Container  US-South        ywu@us.ibm.com  demo2
	3  default-router(129.41.238.212)  Container  United-Kingdom  ywu@us.ibm.com  demo3

	Select first router for peering> 1
	Select second router for peering> 2

	Connecting 'default-router(129.41.234.246)' and 'default-router(129.41.237.172)' ...
	OK

	Private network peering connection 'demo' created.


#### Auflisten aller Verbindungen für das private Netzpeering
```
bluemix network pnp-show [--verbose (or -v)]
```

#####Optionale Parameter
{: #op2}

* **--verbose (or -v)** (Flag): Anzeigen ausführlicher Netzinformationen zu jedem Router.

######Beispiele für Befehle
{: #ex4}

Anzeigen von Basisinformationen:

	$ bluemix network pnp-show
	Listing private network peering connections ...
	OK

	ID                                    NAME  STATUS  ROUTER1                         ROUTER2
	17b1c3c7-d614-4fc5-9afe-961e38ee79f8  demo  Active  default-router(129.41.234.246)  default-router(129.41.237.172)

Anzeigen ausführlicher Informationen:

	$ bluemix network pnp-show -v
	Listing private network peering connections ...
	OK

	Connection 'bedbc077-8040-41cc-a4aa-d9ce09a2e8ec':
	FIELD              VALUE
	Name               demo
	Status             Active
	Router1 Name       default-router
	Router1 IP         129.41.234.246
	Router1 Networks   172.31.0.0/16
	Router2 Name       default-router
	Router2 IP         129.41.237.172
	Router2 Networks   172.25.0.0/16


#### Löschen einer Verbindung für das private Netzpeering
```
bluemix network pnp-delete [--force (or -f)] <connection_id>
```
#####Parameter
{: #p3}
* **connection_id**: Eine oder mehrere Verbindungs-IDs, durch Kommas getrennt.

#####Optionale Parameter
{: #op3}

* **--force (or -f)** (Flag): Löscht die Verbindung ohne Aufforderung zur Bestätigung.

######Beispiel für einen Befehl:
{: #ex5}

Löschen einer Verbindung:

	$ bluemix network pnp-delete 17b1c3c7-d614-4fc5-9afe-961e38ee79f8
	Warning: deleted connections cannot be restored.
	Are you sure you want to delete the connection? (yes/no)> yes

	Deleting private network peering connection '17b1c3c7-d614-4fc5-9afe-961e38ee79f8' ...
	OK

	Private network peering connection '17b1c3c7-d614-4fc5-9afe-961e38ee79f8' deleted.


Löschen mehrerer Verbindungen:

```
bluemix network pnp-delete [-f] <connection_id>,<connection_id>,<connection_id>
```
