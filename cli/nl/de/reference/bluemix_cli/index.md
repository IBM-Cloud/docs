{:shortdesc: .shortdesc}

# bx-Befehle zum Interagieren mit {{site.data.keyword.Bluemix_notm}}
{: #bluemix_cli}

*Letzte Aktualisierung:* 19. Oktober 2015

Von der {{site.data.keyword.Bluemix}}-Befehlszeilenschnittstelle (CLI) werden Befehle bereitgestellt, die nach Namensbereich für Benutzer zur Interaktion mit {{site.data.keyword.Bluemix_notm}} zusammengefasst sind. Manche {{site.data.keyword.Bluemix_notm}}-CLI-Befehle, die auch als bx-Befehle bezeichnet werden, sind Oberflächen für vorhandene cf-Befehle, andere sind in {{site.data.keyword.Bluemix_notm}} eindeutig. In der nachfolgenden Liste werden alle von der {{site.data.keyword.Bluemix_notm}}-CLI unterstützten Befehle mit Namen, Optionen, Verwendungen, Voraussetzungen, Beschreibungen und Beispielen aufgeführt.
{:shortdesc}
 
**Hinweis:** Unter *Voraussetzungen* wird aufgelistet, welche Aktionen vor der Verwendung des Befehls ausgeführt werden müssen. Für Befehle, für die keine Voraussetzungen erfüllt sein müssen, ist **Keine** angegeben. Andernfalls kann mindestens eine der folgenden Aktionen eine Voraussetzung sein: 
<dl>
<dt>**Endpunkt**</dt>
<dd>Vor dem Verwenden des Befehls muss ein API-Endpunkt durch Absetzen des Befehls `bluemix api` definiert werden. </dd>
<dt>**Anmeldung**</dt>
<dd>Vor dem Verwenden des Befehls muss eine Anmeldung mithilfe des Befehls `bluemix login` durchgeführt werden. </dd>
<dt>**Ziel**</dt>
<dd>Vor dem Verwenden des Befehls muss der Befehl `bluemix target` zum Definieren einer Organisation und eines Bereichs ausgeführt werden. </dd>
</dl>

## bluemix help
Zeigt die erweiterte Hilfe für integrierte Befehle und unterstützte Namensbereiche der obersten Ebene in der {{site.data.keyword.Bluemix_notm}}-CLI oder die Hilfe für einen bestimmten integrierten Befehl oder Namensbereich an. 

```
bluemix help [COMMAND|NAMESPACE]
```

**Voraussetzungen**: Keine

**Befehlsoptionen**: 

*COMMAND*|*NAMESPACE* (optional): Der Befehl oder Namensbereich, für den die Hilfe angezeigt wird. Wenn nichts angegeben ist, wird die erweiterte Hilfe für die {{site.data.keyword.Bluemix_notm}}-CLI angezeigt. 

**Beispiele**: 

Erweiterte Hilfe für die {{site.data.keyword.Bluemix_notm}}-CLI anzeigen: 

```
bluemix help
```

Hilfe für den Namensbereich `catalog` anzeigen: 

```
bluemix help catalog
```

```
bluemix catalog help
```

Hilfe für Befehl `info` anzeigen: 

```
bluemix help info
```

Hilfe für Befehl `templates` unter Namensbereich `catalog` anzeigen: 

```
bluemix catalog help templates
```


## bluemix api
{{site.data.keyword.Bluemix_notm}}-API-Endpunkt festlegen oder anzeigen. Dieser Befehl schließt den Befehl `cf api` ein. 

```
bluemix api [API_ENDPOINT][--unset]
```

**Voraussetzungen**: Keine

**Befehlsoptionen**: 

*API_ENDPOINT* (optional): Der API-Endpunkt, der als Ziel verwendet wird, zum Beispiel 'https://api.ng.bluemix.net'. Wenn weder die Option *API_ENDPOINT* noch die Option `--unset` angegeben wird, wird der aktuelle API-Endpunkt angezeigt. 

`--unset` (optional): Entfernt die Einstellung für den API-Endpunkt. 

**Beispiele**: 

API-Endpunkt als api.ng.bluemix.net definieren: 

```
bluemix api api.ng.bluemix.net
```

Aktuellen API-Endpunkt anzeigen: 

```
bluemix api
```

Definition für den API-Endpunkt rückgängig machen: 

```
bluemix api --unset
```


## bluemix login
Anmeldung des Benutzers. Dieser Befehl schließt den Befehl `cf login` ein. Die Befehlsoption sind dieselben wie die für den Befehl `cf login`. 

```
bluemix login [OPTIONS...]
```

**Voraussetzungen**: Endpunkt

**Befehlsoptionen**: Informationen zu den Optionen, die vom Befehl `login` unterstützt werden, finden Sie in den Informationen zur Verwendung des Befehls `cf login` für cf-Befehle zur Verwaltung von Anwendungen. 


## bluemix logout
Abmeldung des Benutzers. Dieser Befehl schließt den Befehl `cf logout` ein. 

```
bluemix logout
```

**Voraussetzungen**: Keine


## bluemix target
Zielorganisation oder Zielbereich festlegen oder anzeigen. Dieser Befehl schließt den Befehl `cf target` ein. 

```
bluemix target [-o ORG_NAME] [-s SPACE_NAME]
```

**Voraussetzungen**: Endpunkt, Anmeldung

**Befehlsoptionen**: 

-o *ORG_NAME* (optional): Der Name der Zielorganisation. 

-s *SPACE_NAME* (optional): Der Name des Zielbereichs. 

Wenn weder -o *ORG_NAME* noch -s *SPACE_NAME* angegeben wird, werden die aktuelle Organisation und der aktuelle Bereich angezeigt. 

**Beispiele**: 

'MyOrg' als aktuelle Organisation und 'MySpace' als aktuellen Bereich definieren: 

```
bluemix target -o MyOrg -s MySpace
```

Aktuelle Organisation und aktuellen Bereich anzeigen: 

```
bluemix target
```


## bluemix info
{{site.data.keyword.Bluemix_notm}}-Basisinformationen einschließlich aktueller Region, Cloud-Controller-Version und einigen nützlichen Endpunkten (zum Beispiel zum Anmelden und Austauschen von Zugriffstoken) anzeigen. 

```
bluemix info
```

**Voraussetzungen**: Endpunkt


## bluemix list
Alle cf-Anwendungen, -Container, -Containergruppen und -VM-Gruppen im aktuellen Bereich anzeigen. 

```
bluemix list [apps|containers|container-groups|vm-groups]
```

**Voraussetzungen**:  Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**: 

apps (optional): Nur die Anwendungsinformationen anzeigen. 

containers (optional): Nur die Containerinformationen anzeigen. 

container-groups (optional): Nur die Containergruppeninformationen anzeigen. 

vm-groups (optional): Nur die VM-Gruppeninformationen anzeigen. 

Nur eine der Optionen 'apps', 'containers', 'container-groups' oder 'vm-groups' kann gleichzeitig angegeben werden. Wenn keine der Optionen angegeben wird, werden alle cf-Anwendungen, -Container, Containergruppen und -VM-Gruppen aufgelistet. 

**Beispiele**: 

Liste aller cf-Anwendungen: 

```
bluemix list apps
```

Liste aller Containerinstanzen: 

```
bluemix list containers
```

Alle Anwendungen, Container, Containergruppen und VM-Gruppen: 

```
bluemix list
```


## bluemix scale
Scale-in oder Scale-out der cf-Anwendung oder -Containergruppe für eine bestimmte Instanzenanzahl, ein bestimmtes Festplattenkontingent und eine bestimmte Speichergröße durchführen. 

**Hinweis:** Zum Skalieren einer Containergruppe kann nur eine Instanzenanzahl angegeben werden. Wenn keine Option angegeben wird, werden beim Absetzen dieses Befehls die aktuelle Instanzenanzahl für die Containergruppe sowie das Plattenkontingent und die Hauptspeichergröße für die cf-Anwendung aufgelistet. 

```
bluemix scale CF_APP_NAME|CONTAINER_GROUP_NAME [-i INSTANCE_COUNT] [-k DISK_QUOTA] [-m MEMORY_SIZE]
```

**Voraussetzungen**: Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**: 

*CF_APP_NAME*|*CONTAINER_GROUP_NAME* (erforderlich): Der Name der cf-Anwendung oder -Containergruppe, die skaliert werden soll. 

-i *INSTANCE_COUNT* (optional): Die neue Anzahl der Instanzen für die cf-Anwendung oder -Containergruppe, die skaliert werden soll. Diese Option ist die einzige gültige Option für eine Containergruppe, die skaliert werden soll. 

-k *DISK_QUOTA* (optional): Das neue Festplattenkontingent der cf-Anwendung. Nicht gültig für die Skalierung einer Containergruppe. 

-m *MEMORY_SIZE* (optional): Die neue Hauptspeichergröße für die cf-Anwendung. Nicht gültig für die Skalierung einer Containergruppe. 

**Beispiele**: 

Aktuelle Anzahl der Instanzen für 'my-container-group' anzeigen: 

```
bluemix scale my-container-group
```

'my-container-group' auf 2 Instanzen skalieren: 

```
bluemix scale my-container-group -i 2
```

'my-java-app' auf 3 Instanzen, 8 GB Festplattenkontingent und 1024 MB Hauptspeichergröße skalieren: 

```
bluemix scale my-java-app -i 3 -k 8G -m 1024M
```


## bluemix curl
Ausführung einer unformatierten HTTP-Anforderung für {{site.data.keyword.Bluemix_notm}}. Für den Inhaltstyp (Content-Type) ist standardmäßig 'application/json' eingestellt. Vom Befehl wird eine Anforderung an den {{site.data.keyword.Bluemix_notm}}-Konsolenserver (zum Beispiel https://console.ng.bluemix.net) anstatt an den cf-API-Endpunkt (zum Beispiel https://api.ng.bluemix.net) gesendet. 

```
bluemix curl PATH [OPTIONS...]
```

**Voraussetzungen**: Endpunkt, Anmeldung

**Befehlsoptionen**: 

*PATH* (erforderlich): Der URL-Pfad der Ressource. Beispiel: /rest/v2/apps. 

*OPTIONS* (optional): Die Optionen, die vom Befehl `bluemix curl` unterstützt werden, sind mit den Optionen identisch, die vom Befehl `cf curl` unterstützt werden. 

**Beispiele**: 

Informationen für alle Boilerplate-Vorlagen abrufen: 

```
bluemix curl /rest/templates
```


## bluemix iam orgs
Dieser Befehl weist dieselbe Funktion und dieselben Optionen wie der Befehl `cf orgs` auf. 


## bluemix iam org
Dieser Befehl weist dieselbe Funktion und dieselben Optionen wie der Befehl `cf org` auf. 


## bluemix iam org-create
Dieser Befehl weist dieselbe Funktion und dieselben Optionen wie der Befehl `cf create-org` auf. 


## bluemix iam org-rename
Dieser Befehl weist dieselbe Funktion und dieselben Optionen wie der Befehl `cf rename-org` auf. 


## bluemix iam org-delete
Dieser Befehl weist dieselbe Funktion und dieselben Optionen wie der Befehl `cf delete-org` auf. 


## bluemix iam spaces
Dieser Befehl weist dieselbe Funktion und dieselben Optionen wie der Befehl `cf spaces` auf. 


## bluemix iam space
Dieser Befehl weist dieselbe Funktion und dieselben Optionen wie der Befehl `cf space` auf. 


## bluemix iam space-create
Dieser Befehl weist dieselbe Funktion und dieselben Optionen wie der Befehl `cf create-space` auf. 


## bluemix iam space-rename
Dieser Befehl weist dieselbe Funktion und dieselben Optionen wie der Befehl `cf rename-space` auf. 


## bluemix iam space-delete
Dieser Befehl weist dieselbe Funktion und dieselben Optionen wie der Befehl `cf delete-space` auf. 


## bluemix iam user-create
Dieser Befehl weist dieselbe Funktion und dieselben Optionen wie der Befehl `cf create-user` auf. 


## bluemix iam user-delete
Dieser Befehl weist dieselbe Funktion und dieselben Optionen wie der Befehl `cf delete-user` auf. 


## bluemix iam org-users
Dieser Befehl weist dieselbe Funktion und dieselben Optionen wie der Befehl `cf org-users` auf. 


## bluemix iam org-role-set
Dieser Befehl weist dieselbe Funktion und dieselben Optionen wie der Befehl `cf set-org-role` auf. 


## bluemix iam org-role-unset
Dieser Befehl weist dieselbe Funktion und dieselben Optionen wie der Befehl `cf unset-org-role` auf. 


## bluemix iam space-users
Dieser Befehl weist dieselbe Funktion und dieselben Optionen wie der Befehl `cf space-users` auf. 


## bluemix iam space-role-set
Dieser Befehl weist dieselbe Funktion und dieselben Optionen wie der Befehl `cf set-space-role` auf. 


## bluemix iam space-role-unset
Dieser Befehl weist dieselbe Funktion und dieselben Optionen wie der Befehl `cf unset-space-role` auf. 


## bluemix catalog templates
Zeigt die Boilerplate-Vorlagen in Bluemix an. 

```
bluemix catalog templates [-d]
```

**Voraussetzungen**: Endpunkt, Anmeldung

**Befehlsoptionen**: 

-d (optional): Wenn die Option '-d' angegeben wird, wird auch die Beschreibung jeder Vorlage angezeigt. Andernfalls werden nur die ID und der Name jeder Vorlage angezeigt. 


## bluemix catalog template-run
Erstellt eine cf-Anwendung, die auf der angegebenen Vorlage mit der angegebenen URL und Beschreibung basiert. Die neue App wird standardmäßig automatisch gestartet. 

```
bluemix catalog template-run TEMPLATE_ID CF_APP_NAME [-u URL] [-d DESCRIPTION] [--no-start]
```

**Voraussetzungen**: Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**: 

*TEMPLATE_ID* (erforderlich): Die Vorlage, auf der die Anwendung bei ihrer Erstellung basiert. Verwenden Sie 'bluemix templates', um die IDs aller Vorlagen anzuzeigen. 

*CF_APP_NAME* (erforderlich): Der Name der Anwendung, die erstellt werden soll. 

-u *URL* (optional): Die Route der Anwendung. Wenn Sie nicht angegeben ist, wird die Route von {{site.data.keyword.Bluemix_notm}} automatisch auf der Grundlage des Anwendungsnamens und der Standarddomäne festgelegt. 

-d *DESCRIPTION* (optional): Die Beschreibung der Anwendung. 

--no-start (optional): Startet die Anwendung nach ihrer Erstellung nicht automatisch. Wenn diese Option nicht angegeben wird, wird die Anwendung nach ihrer Erstellung automatisch gestartet. 

**Beispiele**: 

cf-Anwendung 'my-app' auf der Basis der Vorlage 'javaHelloWorld' erstellen: 

```
bluemix catalog template-run javaHelloWorld my-app
```

Anwendung 'my-ruby-app' auf Basis der Vorlage 'rubyHelloWorld' mit Route 'myrubyapp.ng.bluemix.net' und Beschreibung 'My first ruby app on {{site.data.keyword.Bluemix_notm}}.' erstellen: 

```
bluemix catalog template-run rubyHelloWorld my-ruby-app -u myrubyapp.ng.bluemix.net -d "My first ruby app on {{site.data.keyword.Bluemix_notm}}."
```

Anwendung 'my-python-app' auf Basis der Vorlage 'pythonHelloWorld' ohne automatischen Start erstellen: 

```
bluemix catalog template-run pythonHelloWorld my-python-app --no-start
```


## bluemix network regions
Zeigt die Informationen für alle Regionen in {{site.data.keyword.Bluemix_notm}} an. 

```
bluemix network regions
```

**Voraussetzungen**: Endpunkt


## bluemix network region-set
Wechselt zur angegebenen Region. Von diesem Befehl wird automatisch auf dieselbe Organisation und denselben Bereich in der neuen Region zurückverwiesen (sofern möglich) oder der Benutzer aufgefordert, eine neue Organisation und einen neuen Bereich auszuwählen, wenn der Benutzer bereits angemeldet ist. Der API-Endpunkt wird entsprechend geändert. 

```
bluemix network region-set REGION_NAME
```

**Voraussetzungen**: Endpunkt

**Befehlsoptionen**: 

*REGION_NAME* (erforderlich): Der Name der Region, zu der Sie wechseln möchten. Mit dem Befehl `bluemix regions` können Sie alle Regionsnamen anzeigen. 

**Beispiele**: 

Als aktuelle Region 'eu-gb' festlegen: 

```
bluemix network region-set eu-gb
```


## bluemix network routes
Dieser Befehl weist dieselbe Funktion und dieselben Optionen wie der Befehl `cf routes` auf. 


## bluemix network route-check
Dieser Befehl weist dieselbe Funktion und dieselben Optionen wie der Befehl `cf check-route` auf. 


## bluemix network route-map
Ordnet eine Route einer vorhandenen cf-Anwendung oder -Containergruppe zu, die über die angegebene Domäne oder den angegebenen Hostnamen verfügt. 

```
bluemix network route-map CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

**Voraussetzungen**:  Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**: 

*CF_APP_NAME*|*CONTAINER_GROUP_NAME* (erforderlich): Der Name der cf-Anwendung oder der -Containergruppe für die Zuordnung der Route. 

*DOMAIN* (erforderlich): Die Domäne der Route. Beispiele: 'mybluemix.net' oder 'ng.bluemix.net'.  

-n *HOST_NAME* (optional): Der Hostname der Route. Wenn der Hostname nicht angegeben wird, wird standardmäßig der Anwendungsname oder der Containergruppenname festgelegt. 

**Beispiele**: 

Route zu 'my-app' mit angegebener Domäne zuordnen: 

```
bluemix network route-map my-app mybluemix.net
```

Route zu 'my-container-group' mit angegebener Domäne und angegebenem Hostnamen zuordnen: 

```
bluemix network route-map my-container-group ng.bluemix.net -n abc
```


## bluemix network route-unmap
Entfernt die Zuordnung der angegebenen Route von einer vorhandene cf-Anwendung oder -Containergruppe. 

```
bluemix network route-unmap CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

**Voraussetzungen**: Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**: 

*CF_APP_NAME*|*CONTAINER_GROUP_NAME* (erforderlich): Der Name der cf-Anwendung oder der -Containergruppe. 

*DOMAIN* (erforderlich): Die Domäne der Route (Beispiele: 'mybluemix.net' oder 'ng.bluemix.net').  

-n *HOST_NAME* (optional): Der Hostname der Route. Wenn der Hostname nicht angegeben wird, wird standardmäßig der Anwendungsname oder der Containergruppenname festgelegt. 

**Beispiele**: 

Zuordnung von 'my-app.mybluemix.net' zu 'my-app' rückgängig machen: 

```
bluemix network route-unmap my-app mybluemix.net
```

Zuordnung von 'abc.ng.bluexmix.net' zu 'my-container-group' rückgängig machen: 

```
bluemix network route-unmap my-container-group ng.bluemix.net -n abc
```


## bluemix network route-create
Dieser Befehl weist dieselbe Funktion und dieselben Optionen wie der Befehl `cf create-route` auf. 


## bluemix network route-delete
Dieser Befehl weist dieselbe Funktion und dieselben Optionen wie der Befehl `cf delete-route` auf. 


## bluemix network orphaned-routes-delete
Dieser Befehl weist dieselbe Funktion und dieselben Optionen wie der Befehl `cf delete-orphaned-routes` auf. 


## bluemix network domains
Dieser Befehl weist dieselbe Funktion und dieselben Optionen wie der Befehl `cf domains` auf. 


## bluemix network domain-create
Dieser Befehl weist dieselbe Funktion und dieselben Optionen wie der Befehl `cf create-domain` auf. 


## bluemix network domain-delete
Dieser Befehl weist dieselbe Funktion und dieselben Optionen wie der Befehl `cf delete-domain` auf. 


## bluemix network shared-domain-create
Dieser Befehl weist dieselbe Funktion und dieselben Optionen wie der Befehl `cf create-shared-domain` auf. 


## bluemix network shared-domain-delete
Dieser Befehl weist dieselbe Funktion und dieselben Optionen wie der Befehl `cf delete-shared-domain` auf. 


## bluemix plugin repos
Listet alle Plug-in-Repositorys auf, die in der Befehlszeilenschnittstelle von {{site.data.keyword.Bluemix_notm}} registriert sind. 

```
bluemix plugin repos
```

**Voraussetzungen**: Keine


## bluemix plugin repo-add
Fügt ein neues Plug-in-Repository zur Befehlszeilenschnittstelle von {{site.data.keyword.Bluemix_notm}} hinzu. 

```
bluemix plugin repo-add REPO_NAME REPO_URL
```

**Voraussetzungen**: Keine

**Befehlsoptionen**: 

*REPO_NAME* (erforderlich): Der Name des Repositorys, das hinzugefügt werden soll. Sie können einen eigenen Namen für jedes Repository definieren. 

*REPO_URL* (erforderlich): Die URL des Repositorys, das hinzugefügt werden soll. Die URL des Repositorys muss das Protokoll (zum Beispiel 'http://plugins.ng.bluemix.net' anstatt 'plugins.ng.bluemix.net') enthalten. 'http://plugins.ng.bluemix.net' ist das offizielle Plug-in-Repository der Benutzerschnittstelle von {{site.data.keyword.Bluemix_notm}}. 

**Beispiele**: 

Offizielles Plug-in-Repository der Bluemix-Benutzerschnittstelle als 'bluemix-repo' hinzufügen: 

```
bluemix plugin repo-add bluemix-repo http://plugins.ng.bluemix.net
```


## bluemix plugin repo-remove
Entfernt ein Plug-in-Repository aus der {{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle. 

```
bluemix plugin repo-remove REPO_NAME
```

**Voraussetzungen**: Keine

**Befehlsoptionen**: 

*REPO_NAME* (erforderlich): Der Name des Repositorys, das entfernt werden soll. 

**Beispiele**: 

Repository 'bluemix-repo' aus der Befehlszeilenschnittstelle von {{site.data.keyword.Bluemix_notm}} entfernen: 

```
bluemix plugin repo-remove bluemix-repo
```


## bluemix plugin repo-plugin-list
Listet alle verfügbaren Plug-ins in allen hinzugefügten Repositorys oder einem bestimmten Repository auf. 

```
bluemix plugin repo-plugin-list [-r REPO_NAME]
```

**Voraussetzungen**: Keine

**Befehlsoptionen**: 

-r *REPO_NAME* (optional): Listet nur die Plug-ins im angegebenen Repository auf. 

**Beispiele**: 

Alle Plug-ins in allen hinzugefügten Repositorys auflisten: 

```
bluemix plugin repo-plugin-list
```

Alle Plug-ins im Repositorys 'bluemix-repo' auflisten: 

```
bluemix plugin repo-plugin-list -r bluemix-repo
```


## bluemix plugin list
Listet alle in der Befehlszeilenschnittstelle von {{site.data.keyword.Bluemix_notm}} installierten Plug-ins auf. 

```
bluemix plugin list```

**Voraussetzungen**: Keine


## bluemix plugin install
Installiert das Plug-in in der {{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle aus dem angegebenen Pfad oder Repository. 

```
bluemix plugin install PLUGIN_PATH|PLUGIN_NAME [-r REPO_NAME]
```

**Voraussetzungen**: Keine

**Befehlsoptionen**: 

*PLUGIN_PATH*|*PLUGIN_NAME* (erforderlich): Wenn für '-r *REPO_NAME*' keine Angabe vorgenommen wurde, wird das Plug-in vom angegebenen lokalen Pfad oder der fernen URL installiert. 

-r *REPO_NAME* (optional): Der Name des Repositorys, in dem sich die Binärdatei des Plug-ins befindet. 

**Beispiele**: 

Plug-in von einer lokalen Datei installieren: 

```
bluemix plugin install /downloads/new_plugin
```

Plug-in von ferner URL installieren: 

```
bluemix plugin install http://plugins.ng.bluemix.net/downloads/new_plugin
```

Plug-in 'IBM-Containers' von Repository 'bluemix-repo' installieren: 

```
bluemix plugin install IBM-Containers -r bluemix-repo
```


## bluemix plugin uninstall
Deinstalliert das angegebene Plug-in in der Befehlszeilenschnittstelle von {{site.data.keyword.Bluemix_notm}}. 

```
bluemix plugin uninstall PLUGIN_NAME
```

**Voraussetzungen**: Keine

**Befehlsoptionen**: 

*PLUGIN_NAME* (erforderlich): Der Name des Plug-ins, das deinstalliert werden soll. 

**Beispiele**: 

Plug-in 'IBM-Containers' deinstallieren, das vorher installiert wurde: 

```
bluemix plugin uninstall IBM-Containers
```
