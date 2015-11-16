{:shortdesc: .shortdesc}

# bluemix-Befehle
{: #bluemix_cli}

*Letzte Aktualisierung:* 19. Oktober 2015

Die Befehlszeilenschnittstelle von Bluemix stellt eine Reihe von Befehlen zur Verfügung, die nach Namensbereich gruppiert sind und mit deren Hilfe Benutzer mit Bluemix interagieren können. Bei einigen Bluemix-CLI-Befehlen handelt es sich um Wrapper bereits vorhandener cf-Befehle, andere Befehle sind für Bluemix spezifisch. In den folgenden Informationen werden alle Befehle aufgeführt, die von der Befehlszeilenschnittstelle von Bluemix unterstützt werden; diese Informationen umfassen auch Namen, Optionen, Syntax, Voraussetzungen, Beschreibungen und Beispiele zu den Befehlen.
{:shortdesc}
 
**Anmerkung:** Unter *Voraussetzungen* finden Sie Aktionen, die vor der Verwendung des jeweiligen Befehls erforderlich sind. Befehle, für die keine vorausgesetzten Aktionen erforderlich sind, sind mit **Keine** markiert. In allen anderen Fällen kann für die Voraussetzungen mindestens eine der folgenden Aktionen erforderlich sein:
<dl>
<dt>**Endpunkt**</dt>
<dd>Vor der Verwendung des Befehls muss mittels `bluemix api` ein API-Endpunkt festgelegt werden.</dd>
<dt>**Anmeldung**</dt>
<dd>Vor der Verwendung des Befehls ist die Anmeldung über den Befehl `bluemix login` erforderlich.</dd>
<dt>**Ziel**</dt>
<dd>Vor der Verwendung dieses Befehls muss der Befehl `bluemix target` zum Festlegen einer Organisation oder eines Bereichs verwendet werden.</dd>
</dl>

## bluemix help
Es wird die erweiterte Hilfe für integrierte Befehle der ersten Ebene und unterstützte Namensbereiche der Bluemix-CLI bzw. Hilfe für einen bestimmten integrierten Befehl oder Namensbereich angezeigt.

```
bluemix help [COMMAND|NAMESPACE]
```

**Voraussetzungen**:  Keine

**Befehlsoptionen**:

*COMMAND*|*NAMESPACE*  (optional):  Der Befehl oder Namensbereich, für den Hilfe angezeigt wird. Ohne Angabe wird die erweiterte Hilfe für die Bluemix-CLI angezeigt.

**Beispiele**:

Anzeigen der erweiterten Hilfe für die Bluemix-CLI:

```
bluemix help
```

Anzeigen der Hilfe für den Namensbereich `catalog`:

```
bluemix help catalog
```

```
bluemix catalog help
```

Anzeigen der Hilfe für den Befehl `info`:

```
bluemix help info
```

Anzeigen der Hilfe für den Befehl `templates` unter dem Namensbereich `catalog`:

```
bluemix catalog help templates
```


## bluemix api
Es wird der Bluemix-API-Endpunkt festgelegt oder angezeigt. Dieser Befehl umschließt den Befehl `cf api`.

```
bluemix api [API_ENDPOINT][--unset]
```

**Voraussetzungen**:  Keine

**Befehlsoptionen**:

*API_ENDPOINT*  (optional):  Der anvisierte API-Endpunkt, z. B. https://api.ng.bluemix.net. Wenn sowohl die Option *API_ENDPOINT* als auch die Option `–unset` nicht angegeben ist, wird der aktuelle API-Endpunkt angezeigt.

`--unset`  (optional):  Die Einstellung für den API-Endpunkt wird entfernt.

**Beispiele**:

Festlegen des API-Endpunkts auf api.ng.bluemix.net:

```
bluemix api api.ng.bluemix.net
```

Anzeigen des aktuellen API-Endpunkts:

```
bluemix api
```

Den API-Endpunkt aufheben:

```
bluemix api --unset
```


## bluemix login
Der Benutzer wird angemeldet. Dieser Befehl umschließt den Befehl `cf login`. Die Befehlsoptionen sind mit den Befehlsoptionen des Typs `cf login` identisch.

```
bluemix login [OPTIONS...]
```

**Voraussetzungen**:  Endpunkt

**Befehlsoptionen**:
Informationen zu den Optionen, die der Befehl `login` unterstützt, finden Sie bei den Informationen zur Syntax des Befehls `cf login` für cf-Befehle zur Verwaltung von Anwendungen.


## bluemix logout
Der Benutzer wird abgemeldet. Dieser Befehl umschließt den Befehl `cf logout`. 

```
bluemix logout
```

**Voraussetzungen**:  Keine


## bluemix target
Es wird die Zielorganisation oder der Zielbereich festgelegt oder angezeigt. Dieser Befehl umschließt den Befehl `cf target`. 

```
bluemix target [-o ORG_NAME] [-s SPACE_NAME]
```

**Voraussetzungen**:  Endpunkt, Anmeldung

**Befehlsoptionen**:

-o *ORG_NAME*  (optional):  Der Name der Organisation, die anvisiert werden soll.

-s *SPACE_NAME*  (optional):  Der Name des Bereichs, der anvisiert werden soll. 

Wird weder -o *ORG_NAME* noch -s *SPACE_NAME* angegeben, werden die aktuelle Organisation und der aktuelle Bereich angezeigt.

**Beispiele**:

Festlegen der aktuellen Organisation auf 'MyOrg' und des aktuellen Bereichs auf 'MySpace':

```
bluemix target -o MyOrg -s MySpace
```

Anzeigen der aktuellen Organisation und des aktuellen Bereichs:

```
bluemix target
```


## bluemix info
Es werden die grundlegenden Informationen zu Bluemix angezeigt, einschließlich der aktuellen Region, der Version des Cloud-Controllers sowie einige nützliche Endpunkte, z. B. Endpunkte für Anmeldung und Austausch von Zugriffstokens.

```
bluemix info
```

**Voraussetzungen**:  Endpunkt


## bluemix list
Es werden alle cf-Anwendungen, Container, Containergruppen und VM-Gruppen im aktuellen Bereich aufgeführt.

```
bluemix list [apps|containers|container-groups|vm-groups]
```

**Voraussetzungen**:  Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**:

apps  (optional):  Es werden nur die Anwendungsinformationen angezeigt.

containers  (optional):  Es werden nur die Containerinformationen angezeigt.

container-groups  (optional):  Es werden nur die Containergruppeninformationen angezeigt.

vm-groups  (optional):  Es werden nur die VM-Gruppeninformationen angezeigt.

Es kann immer nur eine der Befehlsoptionen `apps`, `containers`, `container-groups` bzw. `vm-groups` gleichzeitig angegeben werden. Wird keine dieser Befehlsoptionen angegeben, werden alle cf-Anwendungen, Container, Containergruppen und VM-Gruppen aufgeführt.

**Beispiele**:

Auflisten aller cf-Anwendungen:

```
bluemix list apps
```

Auflisten aller Containerinstanzen:

```
bluemix list containers
```

Auflisten aller Apps, Container, Containergruppen und VM-Gruppen:

```
bluemix list
```


## bluemix scale
Es wird für die cf-Anwendung oder die Containergruppe ein Scale-in bzw. ein Scale-out für eine angegebene Instanzzahl, das Plattenkontingent und die Hauptspeichergröße durchgeführt. 

**Anmerkung:** Für die Skalierung einer Containergruppe kann nur eine Instanzzahl angegeben werden. Ist keine Option angegeben, wird durch diesen Befehl die aktuelle Instanzzahl für die Containergruppe sowie das Plattenkontingent und die Hauptspeichergröße für die cf-Anwendung aufgeführt.

```
bluemix scale CF_APP_NAME|CONTAINER_GROUP_NAME [-i INSTANCE_COUNT] [-k DISK_QUOTA] [-m MEMORY_SIZE]
```

**Voraussetzungen**:  Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**:

*CF_APP_NAME*|*CONTAINER_GROUP_NAME*  (erforderlich):  Der Name der zu skalierenden cf-Anwendung bzw. Containergruppe.

-i *INSTANCE_COUNT*  (optional):  Die neue Instanzzahl für die zu skalierende cf-Anwendung oder die Containergruppe. Diese Option ist die einzige gültige Option für die zu skalierende Containergruppe.

-k *DISK_QUOTA*  (optional):  Das neue Plattenkontingent der cf-Anwendung. Nicht gültig für die Skalierung einer Containergruppe.

-m *MEMORY_SIZE*  (optional):  Die neue Hauptspeichergröße für die cf-Anwendung. Nicht gültig für die Skalierung einer Containergruppe.

**Beispiele**:

Anzeigen der aktuellen Instanzzahl für 'my-container-group':

```
bluemix scale my-container-group
```

Skalieren von 'my-container-group' auf 2 Instanzen:

```
bluemix scale my-container-group -i 2
```

Skalieren von 'my-java-app' auf 3 Instanzen, 8 G Plattenkontingent und 1024 M Hauptspeichergröße:

```
bluemix scale my-java-app -i 3 -k 8G -m 1024M
```


## bluemix curl
Es wird eine unbearbeitete HTTP-Anforderung an Bluemix durchgeführt. "Content-Type" ist standardmäßig auf "application/json" gesetzt. Mit diesem Befehl wird eine Anforderung an den Bluemix-Konsolenserver (z. B. https://console.ng.bluemix.net) und nicht an den cf-API-Endpunkt (z. B. https://api.ng.bluemix.net) gesendet.

```
bluemix curl PATH [OPTIONS...]
```

**Voraussetzungen**:  Endpunkt, Anmeldung

**Befehlsoptionen**:

*PATH*  (erforderlich):  Der URL-Pfad der Ressource. Beispiel: /rest/v2/apps.

*OPTIONS*  (optional):  Die Optionen, die der Befehl `bluemix curl` unterstützt, sind mit den Optionen für den Befehl `cf curl` identisch.

**Beispiele**:

Abrufen der Informationen für alle Boilerplate-Vorlagen:

```
bluemix curl /rest/templates
```


## bluemix iam orgs
Dieser Befehl erfüllt dieselbe Funktion und hat dieselben Optionen wie der Befehl `cf orgs`.


## bluemix iam org
Dieser Befehl erfüllt dieselbe Funktion und hat dieselben Optionen wie der Befehl `cf org`.


## bluemix iam org-create
Dieser Befehl erfüllt dieselbe Funktion und hat dieselben Optionen wie der Befehl `cf create-org`.


## bluemix iam org-rename
Dieser Befehl erfüllt dieselbe Funktion und hat dieselben Optionen wie der Befehl `cf rename-org`.


## bluemix iam org-delete
Dieser Befehl erfüllt dieselbe Funktion und hat dieselben Optionen wie der Befehl `cf delete-org`.


## bluemix iam spaces
Dieser Befehl erfüllt dieselbe Funktion und hat dieselben Optionen wie der Befehl `cf spaces`.


## bluemix iam space
Dieser Befehl erfüllt dieselbe Funktion und hat dieselben Optionen wie der Befehl `cf space`.


## bluemix iam space-create
Dieser Befehl erfüllt dieselbe Funktion und hat dieselben Optionen wie der Befehl `cf create-space`.


## bluemix iam space-rename
Dieser Befehl erfüllt dieselbe Funktion und hat dieselben Optionen wie der Befehl `cf rename-space`.


## bluemix iam space-delete
Dieser Befehl erfüllt dieselbe Funktion und hat dieselben Optionen wie der Befehl `cf delete-space`.


## bluemix iam user-create
Dieser Befehl erfüllt dieselbe Funktion und hat dieselben Optionen wie der Befehl `cf create-user`.


## bluemix iam user-delete
Dieser Befehl erfüllt dieselbe Funktion und hat dieselben Optionen wie der Befehl `cf delete-user`.


## bluemix iam org-users
Dieser Befehl erfüllt dieselbe Funktion und hat dieselben Optionen wie der Befehl `cf org-users`.


## bluemix iam org-role-set
Dieser Befehl erfüllt dieselbe Funktion und hat dieselben Optionen wie der Befehl `cf set-org-role`.


## bluemix iam org-role-unset
Dieser Befehl erfüllt dieselbe Funktion und hat dieselben Optionen wie der Befehl `cf unset-org-role`.


## bluemix iam space-users
Dieser Befehl erfüllt dieselbe Funktion und hat dieselben Optionen wie der Befehl `cf space-users`.


## bluemix iam space-role-set
Dieser Befehl erfüllt dieselbe Funktion und hat dieselben Optionen wie der Befehl `cf set-space-role`.


## bluemix iam space-role-unset
Dieser Befehl erfüllt dieselbe Funktion und hat dieselben Optionen wie der Befehl `cf unset-space-role`.


## bluemix catalog templates
Es werden die Boilerplate-Vorlagen in Bluemix angezeigt.

```
bluemix catalog templates [-d]
```

**Voraussetzungen**:  Endpunkt, Anmeldung

**Befehlsoptionen**:

-d  (optional):  Bei Angabe der Option '-d' wird außerdem zu jeder Vorlage die Beschreibung angezeigt. Andernfalls werden nur die ID und der Name der einzelnen Vorlagen angezeigt.


## bluemix catalog template-run
Es wird eine cf-Anwendung auf der Basis der angegebenen Vorlage mit der angegebenen URL und der entsprechenden Beschreibung erstellt. Die neue App wird standardmäßig automatisch gestartet.

```
bluemix catalog template-run TEMPLATE_ID CF_APP_NAME [-u URL] [-d DESCRIPTION] [--no-start]
```

**Voraussetzungen**:  Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**:

*TEMPLATE_ID*  (erforderlich):  Die Vorlage, auf der die Anwendung bei ihrer Erstellung basiert. Verwenden Sie den Befehl 'bluemix templates', um die ID aller Vorlagen anzuzeigen.

*CF_APP_NAME*  (erforderlich):  Der Name der zu erstellenden cf-Anwendung.

-u *URL*  (optional):  Die Route der Anwendung. Ohne Angabe wird die Route von Bluemix automatisch auf der Grundlage Ihres App-Namens und der Standarddomäne festgelegt.

-d *DESCRIPTION*  (optional):  Beschreibung der Anwendung.

--no-start  (optional):  Die Anwendung soll nach der Erstellung nicht automatisch gestartet werden. Ohne Angabe wird die Anwendung nach ihrer Erstellung automatisch gestartet.

**Beispiele**:

Erstellen der cf-Anwendung 'my-app' auf Basis der Vorlage 'javaHelloWorld':

```
bluemix catalog template-run javaHelloWorld my-app
```

Erstellen der Anwendung 'my-ruby-app' auf der Basis der Vorlage 'rubyHelloWorld' mit der Route 'myrubyapp.ng.bluemix.net' und der Beschreibung 'My first ruby app on Bluemix.':

```
bluemix catalog template-run rubyHelloWorld my-ruby-app -u myrubyapp.ng.bluemix.net -d "My first ruby app on Bluemix."
```

Erstellen der Anwendung 'my-python-app' auf Basis der Vorlage 'pythonHelloWorld' ohne automatischen Start:

```
bluemix catalog template-run pythonHelloWorld my-python-app --no-start
```


## bluemix network regions
Es werden Informationen zu allen Regionen in Bluemix angezeigt.

```
bluemix network regions
```

**Voraussetzungen**:  Endpunkt


## bluemix network region-set
Es wird zur angegebenen Region gewechselt. Dieser Befehl visiert automatisch dieselbe Organisation und denselben Bereich in der neuen Region erneut an, falls dies möglich ist, oder fordert den Benutzer zur Auswahl einer neuen Organisation und eines neuen Bereichs auf, falls der Benutzer bereits angemeldet ist. Der API-Endpunkt wird entsprechend geändert.

```
bluemix network region-set REGION_NAME
```

**Voraussetzungen**:  Endpunkt

**Befehlsoptionen**:

*REGION_NAME*  (erforderlich):  Der Name der Region, zu der Sie wechseln möchten. Wenn Sie den Befehl `bluemix regions` verwenden, werden alle Regionsnamen angezeigt.

**Beispiele**:

Festlegen der aktuellen Region auf'eu-gb':

```
bluemix network region-set eu-gb
```


## bluemix network routes
Dieser Befehl erfüllt dieselbe Funktion und hat dieselben Optionen wie der Befehl `cf routes`.


## bluemix network route-check
Dieser Befehl erfüllt dieselbe Funktion und hat dieselben Optionen wie der Befehl `cf check-route`.


## bluemix network route-map
Es wird eine Route zu einer vorhandenen cf-Anwendung oder Containergruppe zugeordnet, die über die angegebene Domäne und den angegebenen Hostnamen verfügt.

```
bluemix network route-map CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

**Voraussetzungen**:  Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**:

*CF_APP_NAME*|*CONTAINER_GROUP_NAME*  (erforderlich):  Der Name der cf-Anwendung bzw. der Containergruppe, der eine Route zugeordnet werden soll.

*DOMAIN*  (erforderlich):  Die Domäne der Route. Beispiel: mybluemix.net oder ng.bluemix.net. 

-n *HOST_NAME*  (optional):  Der Hostname der Route. Ohne Angabe wird der Hostname standardmäßig auf den App-Namen bzw. den Containergruppennamen festgelegt.

**Beispiele**:

Zuordnen einer Route zu 'my-app' mit der angegebenen Domäne:

```
bluemix network route-map my-app mybluemix.net
```

Zuordnen einer Route zu 'my-container-group' mit der angegebenen Domäne und dem angegebenen Hostnamen:

```
bluemix network route-map my-container-group ng.bluemix.net -n abc
```


## bluemix network route-unmap
Die Zuordnung einer Route zu einer vorhandenen cf-Anwendung oder Containergruppe wird aufgehoben.

```
bluemix network route-unmap CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

**Voraussetzungen**:  Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**:

*CF_APP_NAME*|*CONTAINER_GROUP_NAME*  (erforderlich):  Der Name der cf-Anwendung bzw. der Containergruppe.

*DOMAIN*  (erforderlich):  Die Domäne der Route (z. B. mybluemix.net oder ng.bluemix.net). 

-n *HOST_NAME*  (optional):  Der Hostname der Route. Ohne Angabe wird der Hostname standardmäßig auf den App-Namen bzw. den Containergruppennamen festgelegt.

**Beispiele**:

Aufheben der Zuordnung von 'my-app.mybluemix.net' von 'my-app':

```
bluemix network route-unmap my-app mybluemix.net
```

Aufheben der Zuordnung von 'abc.ng.bluexmix.net' von 'my-container-group':

```
bluemix network route-unmap my-container-group ng.bluemix.net -n abc
```


## bluemix network route-create
Dieser Befehl erfüllt dieselbe Funktion und hat dieselben Optionen wie der Befehl `cf create-route`.


## bluemix network route-delete
Dieser Befehl erfüllt dieselbe Funktion und hat dieselben Optionen wie der Befehl `cf delete-route`.


## bluemix network orphaned-routes-delete
Dieser Befehl erfüllt dieselbe Funktion und hat dieselben Optionen wie der Befehl `cf delete-orphaned-routes`.


## bluemix network domains
Dieser Befehl erfüllt dieselbe Funktion und hat dieselben Optionen wie der Befehl `cf domains`.


## bluemix network domain-create
Dieser Befehl erfüllt dieselbe Funktion und hat dieselben Optionen wie der Befehl `cf create-domain`.


## bluemix network domain-delete
Dieser Befehl erfüllt dieselbe Funktion und hat dieselben Optionen wie der Befehl `cf delete-domain`.


## bluemix network shared-domain-create
Dieser Befehl erfüllt dieselbe Funktion und hat dieselben Optionen wie der Befehl `cf create-shared-domain`.


## bluemix network shared-domain-delete
Dieser Befehl erfüllt dieselbe Funktion und hat dieselben Optionen wie der Befehl `cf delete-shared-domain`.


## bluemix plugin repos
Es werden alle Plug-in-Repositorys aufgeführt, die in der Befehlszeilenschnittstelle von Bluemix registriert sind.

```
bluemix plugin repos
```

**Voraussetzungen**:  Keine


## bluemix plugin repo-add
Es wird ein neues Plug-in-Repository zur Befehlszeilenschnittstelle von Bluemix hinzugefügt.

```
bluemix plugin repo-add REPO_NAME REPO_URL
```

**Voraussetzungen**:  Keine

**Befehlsoptionen**:

*REPO_NAME*  (erforderlich):  Der Name des hinzuzufügenden Repositorys. Sie können für jedes Repository Ihren eigenen Namen definieren.

*REPO_URL*  (erforderlich):  Die URL des hinzuzufügenden Repositorys. Die Repository-URL muss das Protokoll enthalten (z. B. http://plugins.ng.bluemix.net und nicht plugins.ng.bluemix.net). http://plugins.ng.bluemix.net ist das offizielle Plug-in-Repository der Befehlszeilenschnittstelle von Bluemix.

**Beispiele**:

Hinzufügen des offiziellen Plug-in-Repositorys zur Befehlszeilenschnittstelle von Bluemix als 'bluemix-repo':

```
bluemix plugin repo-add bluemix-repo http://plugins.ng.bluemix.net
```


## bluemix plugin repo-remove
Es wird ein Plug-in-Repository aus der Befehlszeilenschnittstelle von Bluemix entfernt.

```
bluemix plugin repo-remove REPO_NAME
```

**Voraussetzungen**:  Keine

**Befehlsoptionen**:

*REPO_NAME*  (erforderlich):  Der Name des zu entfernenden Repositorys. 

**Beispiele**:

Entfernen des Repositorys 'bluemix-repo' aus der Befehlszeilenschnittstelle von Bluemix:

```
bluemix plugin repo-remove bluemix-repo
```


## bluemix plugin repo-plugin-list
Es werden alle verfügbaren Plug-ins in allen hinzugefügten Repositorys oder einem bestimmten Repository aufgeführt.

```
bluemix plugin repo-plugin-list [-r REPO_NAME]
```

**Voraussetzungen**:  Keine

**Befehlsoptionen**:

-r *REPO_NAME*  (optional):  Es werden nur die Plug-ins im angegebenen Repository aufgeführt.

**Beispiele**:

Auflisten aller Plug-ins in allen hinzugefügten Repositorys:

```
bluemix plugin repo-plugin-list
```

Auflisten aller Plug-ins im Repository 'bluemix-repo':

```
bluemix plugin repo-plugin-list -r bluemix-repo
```


## bluemix plugin list
Es werden alle installierten Plug-ins in der Befehlszeilenschnittstelle von Bluemix aufgeführt.

```
bluemix plugin list
```

**Voraussetzungen**:  Keine


## bluemix plugin install
Das Plug-in wird aus dem angegebenen Pfad oder dem angegebenen Repository in der Befehlszeilenschnittstelle von Bluemix installiert.

```
bluemix plugin install PLUGIN_PATH|PLUGIN_NAME [-r REPO_NAME]
```

**Voraussetzungen**:  Keine

**Befehlsoptionen**:

*PLUGIN_PATH*|*PLUGIN_NAME*  (erforderlich):  Wenn '-r *REPO_NAME*' nicht angegeben ist, wird das Plug-in aus dem angegebenen lokalen Pfad oder über die ferne URL installiert.

-r *REPO_NAME*  (optional):  Der Name des Repositorys, in dem sich die Plug-in-Binärdatei befindet.

**Beispiele**:

Installieren eines Plug-ins aus der lokalen Datei:

```
bluemix plugin install /downloads/new_plugin
```

Installieren eines Plug-ins über die ferne URL:

```
bluemix plugin install http://plugins.ng.bluemix.net/downloads/new_plugin
```

Installieren des Plug-ins 'IBM-Containers' aus dem Repository 'bluemix-repo':

```
bluemix plugin install IBM-Containers -r bluemix-repo
```


## bluemix plugin uninstall
Das angegebene Plug-in wird aus der Befehlszeilenschnittstelle von Bluemix deinstalliert.

```
bluemix plugin uninstall PLUGIN_NAME
```

**Voraussetzungen**:  Keine

**Befehlsoptionen**:

*PLUGIN_NAME*  (erforderlich):  Der Name des zu deinstallierenden Plug-ins.

**Beispiele**:

Deinstallieren des zuvor installierten Plug-ins 'IBM-Containers':

```
bluemix plugin uninstall IBM-Containers
```
