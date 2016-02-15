{:shortdesc: .shortdesc}

# bx-Befehle zum Interagieren mit {{site.data.keyword.Bluemix_notm}}
{: #bluemix_cli}

*Letzte Aktualisierung:* 5. Januar 2016

Von der {{site.data.keyword.Bluemix}}-Befehlszeilenschnittstelle (CLI) werden Befehle bereitgestellt, die nach Namensbereich für Benutzer zur Interaktion mit {{site.data.keyword.Bluemix_notm}} zusammengefasst sind. Manche {{site.data.keyword.Bluemix_notm}}-CLI-Befehle, die auch als bx-Befehle bezeichnet werden, sind umschließende Elemente (Wrapper) für vorhandene cf-Befehle, andere sind in {{site.data.keyword.Bluemix_notm}} eindeutig. In der nachfolgenden Liste werden alle von der {{site.data.keyword.Bluemix_notm}}-CLI unterstützten Befehle mit Namen, Optionen, Verwendungen, Voraussetzungen, Beschreibungen und Beispielen aufgeführt.
{:shortdesc}
 
**Hinweis:** Unter *Voraussetzungen* wird aufgelistet, welche Aktionen vor der Verwendung des Befehls ausgeführt werden müssen. Für Befehle, für die keine Voraussetzungen erfüllt sein müssen, ist **Keine** angegeben. Andernfalls kann mindestens eine der folgenden Aktionen eine Voraussetzung sein:
<dl>
<dt>Endpunkt</dt>
<dd>Vor dem Verwenden des Befehls muss ein API-Endpunkt durch Absetzen des Befehls <code>bluemix api</code> definiert werden.</dd>
<dt>Anmeldung</dt>
<dd>Vor dem Verwenden des Befehls muss eine Anmeldung mithilfe des Befehls <code>bluemix login</code> durchgeführt werden.</dd>
<dt>Ziel</dt>
<dd>Vor dem Verwenden des Befehls muss der Befehl <code>bluemix target</code> zum Definieren einer Organisation und eines Bereichs ausgeführt werden.</dd>
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

`MyOrg` als aktuelle Organisation und `MySpace` als aktuellen Bereich definieren:

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





## bluemix regions
Zeigt die Informationen für alle Regionen in {{site.data.keyword.Bluemix_notm}} an.

```
bluemix regions
```

**Voraussetzungen**: Endpunkt


## bluemix region-set
Wechselt zur angegebenen Region. Von diesem Befehl wird automatisch auf dieselbe Organisation und denselben Bereich in der neuen Region zurückverwiesen (sofern möglich). Andernfalls wird der Benutzer durch den Befehl aufgefordert, eine neue Organisation und einen neuen Bereich auszuwählen, wenn der Benutzer bereits angemeldet ist. Der API-Endpunkt wird entsprechend geändert.

```
bluemix region-set REGION_NAME
```

**Voraussetzungen**: Endpunkt

**Befehlsoptionen**:

*REGION_NAME* (erforderlich): Der Name der Region, zu der Sie wechseln möchten. Mit dem Befehl `bluemix regions` können Sie alle Regionsnamen anzeigen.

**Beispiele**:

Als aktuelle Region `eu-gb` festlegen:

```
bluemix region-set eu-gb
```



## bluemix config
Schreibt Standardwerte in die Konfigurationsdatei. 

```
bluemix config --http-timeout TIMEOUT_IN_SECONDS | --trace (true|false|path/to/file) | --color (true|false) | --locale (LOCALE|CLEAR)
```

**Voraussetzungen**: Keine

**Befehlsoptionen**:

--http-timeout *TIMEOUT_IN_SECONDS*: Der Zeitlimitwert für HTTP-Anforderungen. Der Standardwert ist 60 Sekunden. 

--trace true|false|*path/to/file*: Trace für HTTP-Anforderungen mit Ausgabe auf Terminal oder in angegebener Datei aktivieren.

--color true|false: Farbausgabe aktivieren oder inaktivieren. Die Farbausgabe ist standardmäßig aktiviert.

--locale *LOCALE*: Eine Standardländereinstellung festlegen. Wenn LOCALE den Wert *CLEAR* hat, wird die vorherige Ländereinstellung gelöscht.

Nur eine dieser Optionen kann gleichzeitig angegeben werden.

**Beispiele**:

HTTP-Anforderungszeitlimit auf 30 Sekunden setzen:

```
bluemix config --http-timeout 30
```

Traceausgabe für HTTP-Anforderungen aktivieren:

```
bluemix config --trace true
```

Traceausgabe für HTTP-Anforderungen in eine angegebene Datei */home/usera/my_trace* schreiben:

```
bluemix config --trace /home/usera/my_trace
```

Farbausgabe inaktivieren:

```
bluemix config --color false
```

Ländereinstellung auf 'zh_Hans' setzen:

```
bluemix config --locale zh_Hans
```

Ländereinstellungen löschen:

```
bluemix config --locale CLEAR
```










## bluemix list
Alle cf-Anwendungen, -Container, -Containergruppen und -VM-Gruppen im aktuellen Bereich anzeigen.

```
bluemix list [apps|containers|container-groups|vm-groups]
```

**Voraussetzungen**: Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**:

apps (optional): Nur die Anwendungsinformationen anzeigen.

containers (optional): Nur die Containerinformationen anzeigen.

container-groups (optional): Nur die Containergruppeninformationen anzeigen.

vm-groups (optional): Nur die VM-Gruppeninformationen anzeigen.

Nur eine der Optionen `apps`, `containers`, `container-groups` oder `vm-groups` kann gleichzeitig angegeben werden. Wenn keine der Optionen angegeben wird, werden alle cf-Anwendungen, -Container, Containergruppen und -VM-Gruppen aufgelistet.

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
bluemix scale CF_APP_NAME|CONTAINER_GROUP_NAME [-i INSTANCE_COUNT][-k DISK_QUOTA] [-m MEMORY_SIZE]
```

**Voraussetzungen**:  Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**:

*CF_APP_NAME*|*CONTAINER_GROUP_NAME* (erforderlich): Der Name der cf-Anwendung oder -Containergruppe, die skaliert werden soll.

-i *INSTANCE_COUNT* (optional): Die neue Anzahl der Instanzen für die cf-Anwendung oder -Containergruppe, die skaliert werden soll. Diese Option ist die einzige gültige Option für eine Containergruppe, die skaliert werden soll.

-k *DISK_QUOTA* (optional): Das neue Festplattenkontingent der cf-Anwendung. Nicht gültig für die Skalierung einer Containergruppe.

-m *MEMORY_SIZE* (optional): Die neue Hauptspeichergröße für die cf-Anwendung. Nicht gültig für die Skalierung einer Containergruppe.

**Beispiele**:

Aktuelle Anzahl der Instanzen für `my-container-group` anzeigen:

```
bluemix scale my-container-group
```

`my-container-group` auf 2 Instanzen skalieren:

```
bluemix scale my-container-group -i 2
```

`my-java-app` auf 3 Instanzen, 8 GB Festplattenkontingent und 1024 MB Hauptspeichergröße skalieren:

```
bluemix scale my-java-app -i 3 -k 8G -m 1024M
```


## bluemix curl
Ausführung einer unformatierten HTTP-Anforderung für {{site.data.keyword.Bluemix_notm}}. *Content-Type* ist standardmäßig auf *application/json* eingestellt. Vom Befehl wird eine Anforderung an den {{site.data.keyword.Bluemix_notm}}-Konsolenserver (zum Beispiel https://console.ng.bluemix.net) anstatt an den cf-API-Endpunkt (zum Beispiel https://api.ng.bluemix.net) gesendet.

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
Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf orgs`, jedoch mit dem Unterschied, dass auch Regionen, in denen Organisationen vorhanden sind, angezeigt werden.


## bluemix iam org
Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf org`, jedoch mit dem Unterschied, dass auch Regionen, in denen die Organisation vorhanden ist, angezeigt werden.


## bluemix iam org-create
Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf create-org`.





## bluemix iam org-replicate
Repliziert eine Organisation aus der aktuellen Region in eine andere Region.

```
bluemix iam org-replicate ORG_NAME REGION_NAME
```

**Voraussetzungen**: Endpunkt, Anmeldung

**Befehlsoptionen**:

*ORG_NAME* (erforderlich): Der Name der vorhandenen Organisation, die repliziert werden soll.

*REGION_NAME* (erforderlich): Der Name der Region, die die replizierte Organisation hostet.

**Beispiele**:

Die Organisation `OE_Runtimes_Scaling` in die Region `eu-gb` replizieren:

```
bluemix iam org-replicate OE_Runtimes_Scaling eu-gb
```














## bluemix iam org-rename
Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf rename-org`.


## bluemix iam org-delete
Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf delete-org`.


## bluemix iam spaces
Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf spaces`.


## bluemix iam space
Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf space`.


## bluemix iam space-create
Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf create-space`.


## bluemix iam space-rename
Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf rename-space`.


## bluemix iam space-delete
Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf delete-space`.


## bluemix iam user-create
Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf create-user`.


## bluemix iam user-delete
Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf delete-user`.


## bluemix iam org-users
Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf org-users`.


## bluemix iam org-role-set
Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf set-org-role`.


## bluemix iam org-role-unset
Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf unset-org-role`.


## bluemix iam space-users
Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf space-users`.


## bluemix iam space-role-set
Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf set-space-role`.


## bluemix iam space-role-unset
Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf unset-space-role`.


## bluemix catalog templates
Zeigt die Boilerplate-Vorlagen in Bluemix an.

```
bluemix catalog templates [-d]
```

**Voraussetzungen**: Endpunkt, Anmeldung

**Befehlsoptionen**:

-d (optional): Wenn die Option `-d` angegeben wird, wird auch die Beschreibung jeder Vorlage angezeigt. Andernfalls werden nur die ID und der Name jeder Vorlage angezeigt.


## bluemix catalog template-run
Erstellt eine cf-Anwendung, die auf der angegebenen Vorlage mit der angegebenen URL und Beschreibung basiert. Die neue App wird standardmäßig automatisch gestartet.

```
bluemix catalog template-run TEMPLATE_ID CF_APP_NAME [-u URL] [-d DESCRIPTION] [--no-start]
```

**Voraussetzungen**: Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**:

*TEMPLATE_ID* (erforderlich): Die Vorlage, auf der die Anwendung bei ihrer Erstellung basiert. Verwenden Sie `bluemix templates`, um die IDs aller Vorlagen anzuzeigen.

*CF_APP_NAME* (erforderlich): Der Name der Anwendung, die erstellt werden soll.

-u *URL* (optional): Die Route der Anwendung. Wenn Sie nicht angegeben ist, wird die Route von {{site.data.keyword.Bluemix_notm}} automatisch auf der Grundlage des Anwendungsnamens und der Standarddomäne festgelegt.

-d *DESCRIPTION* (optional): Die Beschreibung der Anwendung.

--no-start (optional): Startet die Anwendung nach ihrer Erstellung nicht automatisch. Wenn diese Option nicht angegeben wird, wird die Anwendung nach ihrer Erstellung automatisch gestartet.

**Beispiele**:

cf-Anwendung `my-app` auf der Basis der Vorlage `javaHelloWorld` erstellen:

```
bluemix catalog template-run javaHelloWorld my-app
```

Anwendung `my-ruby-app` auf der Basis der Vorlage `rubyHelloWorld` mit der Route `myrubyapp.ng.bluemix.net` und der Beschreibung `My first ruby app on {{site.data.keyword.Bluemix_notm}}.` erstellen:

```
bluemix catalog template-run rubyHelloWorld my-ruby-app -u myrubyapp.ng.bluemix.net -d "My first ruby app on {{site.data.keyword.Bluemix_notm}}."
```

Anwendung `my-python-app` auf Basis der Vorlage `pythonHelloWorld` ohne automatischen Start erstellen:

```
bluemix catalog template-run pythonHelloWorld my-python-app --no-start
```




## bluemix catalog template-register

Registriert eine neue Boilerplate-Vorlage für {{site.data.keyword.Bluemix_notm}}.

```
bluemix catalog template-register TEMPLATE_ID TEMPLATE_URL
```

**Voraussetzungen**: Endpunkt, Anmeldung

**Befehlsoptionen**:

*TEMPLATE_ID* (erforderlich): Die ID der neuen registrierten Vorlage.

*TEMPLATE_URL* (erforderlich): Die URL, die die Metadaten der neuen Vorlage bereitstellt.

**Beispiele**:

Vorlage mit dem Namen `javaHelloWorld` erstellen:

```
bluemix catalog template-register javaHelloWorld http://javaHelloWorld.ng.bluemix.net/info
```

## bluemix catalog template-deregister

Nimmt die Registrierung einer vorhandenen Boilerplate-Vorlage zurück.

```
bluemix catalog template-deregister TEMPLATE_ID [-f]
```

**Voraussetzungen**: Endpunkt, Anmeldung

**Befehlsoptionen**:

*TEMPLATE_ID* (erforderlich): Verwenden Sie den Befehl `bluemix catalog templates`, um alle Vorlagen-IDs anzuzeigen.

-f  (optional): Deregistrierung ohne Bestätigung erzwingen.

**Beispiele**:

Registrierung der Vorlage `javaHelloWorld` ohne Bestätigung zurücknehmen:

```
bluemix catalog template-deregister javaHelloWorld -f
```


## bluemix catalog template-registry
Zeigt die {{site.data.keyword.Bluemix_notm}}-Vorlagenregistry an.

```
bluemix catalog template-registry
```

**Voraussetzungen**: Endpunkt









## bluemix catalog service-broker

Zeigt die Informationen zum angegeben Service-Broker an.

```
bluemix catalog service-broker SERVICE_BROKER_NAME
```

**Voraussetzungen**: Endpunkt, Anmeldung

**Befehlsoptionen**:

*SERVICE_BROKER_NAME* (erforderlich): Der Name des zu besuchenden Service-Brokers.


## bluemix catalog service-broker-create
{: #bluemix_catalog_service_broker_create}
Erstellt einen Service-Broker. 

```
bluemix catalog service-broker-create SERVICE_BROKER_JSON_TEXT|SERVICE_BROKER_JSON_FILE [--no-billing]
```

**Voraussetzungen**: Endpunkt, Anmeldung

**Befehlsoptionen**:

*SERVICE_BROKER_JSON_TEXT*|*SERVICE_BROKER_JSON_FILE* (erforderlich): Das JSON-Element, das den neuen zu erstellenden Service-Broker beschreibt. Sie können entweder den JSON-Dateinamen verwenden oder den JSON-Text direkt verwenden. 

--no-billing (optional): Wenn diese Option angegeben wird, wird die Abrechnungsfunktion für den Service-Broker inaktiviert. 

**Beispiele**:

Service-Broker mit einer JSON-Datei erstellen:

```
bluemix catalog service-broker-create ./broker.json
```

Neuen Service-Broker mit einem JSON-Text und ohne Abrechnung erstellen:

```
bluemix catalog service-broker-create '{"name":"test_broker", ...}' --no-billing
```

Das folgende Beispiel zeigt ein Service-Broker-JSON-Objekt mit allen erforderlichen Feldern:

```
{
    "name": "my_broker",  // Der Name des Service-Broker
    "broker_url": "http://my_broker.ng.bluemix.net"  // Die URL der Metadaten des Service-Brokers
    "auth_username": "username",
	"auth_password": "password",  // Der Benutzername und das Kennwort zum Aufruf der Service-Broker-URL. Benutzername und Kennwort sollten mit HTTP-Basisauthentifizierung gesendet werden.
    "visibilities": [
        {"organization_name": "OE_Runtimes_Scaling"}
    ]
}
```


## bluemix catalog service-broker-update
Aktualisiert einen vorhandenen Service-Broker. 

```
bluemix catalog service-broker-update ORIGINAL_BROKER_NAME SERVICE_BROKER_JSON_TEXT|SERVICE_BROKER_JSON_FILE
```

**Voraussetzungen**: Endpunkt, Anmeldung

**Befehlsoptionen**:

*ORIGINAL_BROKER_NAME* (erforderlich): Der Name des zu aktualisierenden Service-Brokers.

*SERVICE_BROKER_JSON_TEXT*|*SERVICE_BROKER_JSON_FILE* (erforderlich): Das neue JSON-Element, das den Service-Broker beschreibt. Sie können entweder den JSON-Dateinamen verwenden oder den JSON-Text direkt verwenden. 

**Beispiele**:

Vorhandenen Service-Broker `auto-scaling` aktualisieren:

```
bluemix catalog service-broker-update auto-scaling ./auto-scaling.json
```

Weitere Details zum JSON-Format für Service-Broker finden Sie unter [bluemix catalog service-broker-create](#bluemix_catalog_service_broker_create).


## bluemix catalog service-broker-delete

Löscht einen angegebenen Service-Broker.

```
bluemix catalog service-broker-delete SERVICE_BROKER_NAME [-f]
```

**Voraussetzungen**: Endpunkt, Anmeldung

**Befehlsoptionen**:

*SERVICE_BROKER_NAME* (erforderlich): Der Name des zu löschenden Service-Brokers. 

-f  (optional): Löschung ohne Bestätigung erzwingen. 

**Beispiele**:

Service-Broker `auto-scaling` ohne Bestätigung löschen:

```
bluemix catalog service-broker-delete auto-scaling -f
```














## bluemix network routes
Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf routes`.


## bluemix network route-check
Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf check-route`.


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

Route zu `my-app` mit angegebener Domäne zuordnen:

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

**Voraussetzungen**:  Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**:

*CF_APP_NAME*|*CONTAINER_GROUP_NAME* (erforderlich): Der Name der cf-Anwendung oder der -Containergruppe.

*DOMAIN* (erforderlich): Die Domäne der Route (Beispiele: 'mybluemix.net' oder 'ng.bluemix.net'). 

-n *HOST_NAME* (optional): Der Hostname der Route. Wenn der Hostname nicht angegeben wird, wird standardmäßig der Anwendungsname oder der Containergruppenname festgelegt.

**Beispiele**:

Zuordnung von `my-app.mybluemix.net` aus `my-app` entfernen:

```
bluemix network route-unmap my-app mybluemix.net
```

Zuordnung von `abc.ng.bluexmix.net` aus `my-container-group` entfernen:

```
bluemix network route-unmap my-container-group ng.bluemix.net -n abc
```


## bluemix network route-create
Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf create-route`.


## bluemix network route-delete
Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf delete-route`.


## bluemix network orphaned-routes-delete
Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf delete-orphaned-routes`.


## bluemix network domains
Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf domains`.


## bluemix network domain-create
Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf create-domain`.


## bluemix network domain-delete
Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf delete-domain`.


## bluemix network shared-domain-create
Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf create-shared-domain`.


## bluemix network shared-domain-delete
Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf delete-shared-domain`.




## bluemix security cert

Listet Zertifikatsinformationen für den angegebenen Host auf.

```
bluemix security cert HOST_NAME
```

**Voraussetzungen**: Endpunkt, Anmeldung

**Befehlsoptionen**:

*HOST_NAME* (erforderlich): Der Name des Servers, der das Zertifikat bereitstellt. 

**Beispiele**:

Zertifikat auf dem Host `ibmcxo-eventconnect.com` anzeigen:

```
bluemix security cert ibmcxo-eventconnect.com
```


## bluemix security cert-add

Fügt der angegebenen Domäne in der aktuellen Organisation ein Zertifikat hinzu.

```
bluemix security cert-add DOMAIN -k PRIVATE_KEY_FILE -c CERT_FILE [-p PASSWORD][-i INTERMEDIATE_CERT_FILE] [--verify-client]
```

**Voraussetzungen**: Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**:

*DOMAIN* (erforderlich): Die Domäne, der das Zertifikat hinzugefügt wird.

-k *PRIVATE_KEY_FILE* (erforderlich): Der Pfad der Datei mit dem privaten Schlüssel.

-c *CERT_FILE* (erforderlich): Der Pfad der Zertifikatsdatei.

-p *PASSWORD* (optional): Das Kennwort für das Zertifikat.

-i *INTERMEDIATE_CERT_FILE* (optional): Der Pfad für die Zwischenzertifikatsdatei.

--verify-client (optional): Gibt an, ob die Clientzertifikatsprüfung aktiviert werden soll.

**Beispiele**:

Zertifikat der Domäne `ibmcxo-eventconnect.com` hinzufügen:

```
bluemix security cert-add ibmcxo-eventconnect.com -k key_file.key -c cert_file.crt -p 123 -i inter_cert.cert
```


## bluemix security cert-remove
Entfernt ein Zertifikat aus der angegebenen Domäne in der aktuellen Organisation.

```
bluemix security cert-remove DOMAIN [-f]
```

**Voraussetzungen**: Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**:

*DOMAIN* (erforderlich): Die Domäne, aus der das Zertifikat entfernt werden soll.

-f  (optional): Löschung ohne Bestätigung erzwingen. 








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

Offizielles Plug-in-Repository der Bluemix-Befehlszeilenschnittstelle als `bluemix-repo` hinzufügen:

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

Repository `bluemix-repo` aus der Befehlszeilenschnittstelle von {{site.data.keyword.Bluemix_notm}} entfernen:

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

Alle Plug-ins im Repositorys `bluemix-repo` auflisten:

```
bluemix plugin repo-plugin-list -r bluemix-repo
```


## bluemix plugin list
Listet alle in der Befehlszeilenschnittstelle von {{site.data.keyword.Bluemix_notm}} installierten Plug-ins auf.

```
bluemix plugin list
```

**Voraussetzungen**: Keine


## bluemix plugin install
Installiert die angegebene Version des Plug-ins in der {{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle aus dem angegebenen Pfad oder Repository.

```
bluemix plugin install PLUGIN_PATH|PLUGIN_NAME [-r REPO_NAME][-v VERSION]
```

**Voraussetzungen**: Keine

**Befehlsoptionen**:

*PLUGIN_PATH*|*PLUGIN_NAME* (erforderlich): Wenn `-r *REPO_NAME*` nicht angegeben wird, wird das Plug-in vom angegebenen lokalen Pfad oder der fernen URL installiert.

-r *REPO_NAME* (optional): Der Name des Repositorys, in dem sich die Binärdatei des Plug-ins befindet.
-v *VERSION* (optional): Die Version des Plug-ins, die installiert werden soll. Bei keiner Angabe wird die letzte Version des Plug-ins installiert. Diese Option ist nur gültig, wenn Sie das Plug-in aus dem Repository installieren.

**Beispiele**:

Plug-in von einer lokalen Datei installieren:

```
bluemix plugin install /downloads/new_plugin
```

Plug-in von ferner URL installieren:

```
bluemix plugin install http://plugins.ng.bluemix.net/downloads/new_plugin
```

Plug-in `IBM-Containers` der letzten Version aus dem Repository `bluemix-repo` installieren:

```
bluemix plugin install IBM-Containers -r bluemix-repo
```
Plug-in `IBM-Containers` mit der Version `0.5.800` aus dem Repository `bluemix-repo` installieren:

```
bluemix plugin install IBM-Containers -r bluemix-repo -v 0.5.800
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

Plug-in `IBM-Containers` deinstallieren, das vorher installiert wurde:

```
bluemix plugin uninstall IBM-Containers
```
