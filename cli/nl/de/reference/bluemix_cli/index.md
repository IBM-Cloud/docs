---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix_notm}}-Befehle (bx)
{: #bluemix_cli}

*Letzte Aktualisierung: 15. April 2016*

Von der {{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle (CLI) werden Befehle bereitgestellt, die nach Namensbereich für Benutzer zur Interaktion mit {{site.data.keyword.Bluemix_notm}} zusammengefasst sind. Bei einigen {{site.data.keyword.Bluemix_notm}}-Befehlen handelt es sich um Wrapper bereits vorhandener cf-Befehle, während andere Befehle die Funktionalität für {{site.data.keyword.Bluemix_notm}}-Benutzer erweitern. In der nachfolgenden Liste werden alle von der {{site.data.keyword.Bluemix_notm}}-CLI unterstützten Befehle mit Namen, Optionen, Verwendungen, Voraussetzungen, Beschreibungen und Beispielen aufgeführt.
{:shortdesc}
 
**Hinweis:** Unter *Voraussetzungen* wird aufgelistet, welche Aktionen vor der Verwendung des Befehls ausgeführt werden müssen. Für Befehle, für die keine Voraussetzungen erfüllt sein müssen, ist **Keine** angegeben. Andernfalls kann mindestens eine der folgenden Aktionen eine Voraussetzung sein:
<dl>
<dt>Endpunkt</dt>
<dd>Vor dem Verwenden des Befehls muss ein API-Endpunkt durch Absetzen des Befehls <code>bluemix api</code> definiert werden.</dd>
<dt>Anmeldung</dt>
<dd>Vor dem Verwenden des Befehls muss eine Anmeldung mithilfe des Befehls <code>bluemix login</code> durchgeführt werden.</dd>
<dt>Ziel</dt>
<dd>Vor dem Verwenden des Befehls muss der Befehl <code>bluemix target</code> zum Definieren einer Organisation und eines Bereichs ausgeführt werden.</dd>
<dt>Docker</dt>
<dd>Die Docker-CLI (docker) muss installiert werden, um diesen Befehl auszuführen.</dd>
</dl>

Sie können die folgenden {{site.data.keyword.Bluemix_notm}}-Befehle verwenden:

 <table role="presentation"> 
 <tbody> 
 <tr> 
 <td>[bluemix help](index.html#bluemix_help)</td> 
 <td>[bluemix api](index.html#bluemix_api)</td> 
 <td>[bluemix login](index.html#bluemix_login)</td>
 <td>[bluemix logout](index.html#bluemix_logout)</td>
 <td>[bluemix target](index.html#bluemix_target)</td>
 </tr> 
 <tr> 
 <td> 
 [bluemix info](index.html#bluemix_info) </td> 
 <td>[bluemix config](index.html#bluemix_config)</td> 
 <td>[bluemix list](index.html#bluemix_list)</td>
 <td>[bluemix scale](index.html#bluemix_scale)</td>
 <td>[bluemix curl](index.html#bluemix_curl)</td>
 </tr>
 
 <tr> 
 <td>[bluemix iam orgs](index.html#bluemix_iam_orgs) </td> 
 <td>[bluemix iam org](index.html#bluemix_iam_org)</td> 
 <td>[bluemix iam org-create](index.html#bluemix_iam_org_create)</td>
 <td>[bluemix iam org-replicate](index.html#bluemix_iam_org_replicate)</td>
 <td>[bluemix iam org-rename](index.html#bluemix_iam_org_rename)</td>
 </tr>
 
 <tr> 
 <td>[bluemix iam org-delete](index.html#bluemix_iam_org_delete) </td> 
 <td>[bluemix iam spaces](index.html#bluemix_iam_spaces)</td> 
 <td>[bluemix iam space](index.html#bluemix_iam_space)</td>
 <td>[bluemix iam space-create](index.html#bluemix_iam_space_create)</td>
 <td>[bluemix iam space-rename](index.html#bluemix_iam_space_rename)</td>
 </tr>
 
 <tr> 
 <td>[bluemix iam space-delete](index.html#bluemix_iam_space_delete) </td> 
 <td>[bluemix iam account-users](index.html#bluemix_iam_account-users)</td> 
 <td>[bluemix iam account-user-invite](index.html#bluemix_iam_account-user-invite)</td>
 <td>[bluemix iam org-users](index.html#bluemix_iam_org_users)</td>
 <td>[bluemix iam org-role-set](index.html#bluemix_iam_org_role_set)</td>
 </tr>
 
 <tr> 
 <td>[bluemix iam org-role-unset](index.html#bluemix_iam_org_role_unset) </td> 
 <td>[bluemix iam space-users](index.html#bluemix_iam_space_users)</td> 
 <td>[bluemix iam space-role-set](index.html#bluemix_iam_space_role_set)</td>
 <td>[bluemix iam space-role-unset](index.html#bluemix_iam_space_role_unset)</td>
 <td>[bluemix app push](index.html#bluemix_app_push)</td>
 </tr>
 
 <tr> 
 <td>[bluemix app list](index.html#bluemix_app_list) </td> 
 <td>[bluemix app show](index.html#bluemix_app_show)</td> 
 <td>[bluemix app scale](index.html#bluemix_app_scale)</td>
 <td>[bluemix app delete](index.html#bluemix_app_delete)</td>
 <td>[bluemix app rename](index.html#bluemix_app_rename)</td>
 </tr>
 
 <tr> 
 <td>[bluemix app start](index.html#bluemix_app_start) </td> 
 <td>[bluemix app stop](index.html#bluemix_app_stop)</td> 
 <td>[bluemix app restart](index.html#bluemix_app_restart)</td>
 <td>[bluemix app restage](index.html#bluemix_app_restage)</td>
 <td>[bluemix app instance-restart](index.html#bluemix_app_instance_restart)</td>
 </tr>
 
 <tr> 
 <td>[bluemix app events](index.html#bluemix_app_events) </td> 
 <td>[bluemix app files](index.html#bluemix_app_files)</td> 
 <td>[bluemix app logs](index.html#bluemix_app_logs)</td>
 <td>[bluemix app env](index.html#bluemix_app_env)</td>
 <td>[bluemix app env-set](index.html#bluemix_app_env_set)</td>
 </tr>
 
 <tr> 
 <td>[bluemix app env-unset](index.html#bluemix_app_env_unset) </td> 
 <td>[bluemix app stacks](index.html#bluemix_app_stacks)</td> 
 <td>[bluemix app stack](index.html#bluemix_app_stack)</td>
 <td>[bluemix app manifest-create](index.html#bluemix_app_manifest_create)</td>
 <td>[bluemix service offerings](index.html#bluemix_service_offerings)</td>
 </tr>
 
 <tr> 
 <td>[bluemix service list](index.html#bluemix_service_list) </td> 
 <td>[bluemix service show](index.html#bluemix_service_show)</td> 
 <td>[bluemix service create](index.html#bluemix_service_create)</td>
 <td>[bluemix service update](index.html#bluemix_service_update)</td>
 <td>[bluemix service delete](index.html#bluemix_service_delete)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix service rename](index.html#bluemix_service_rename) </td> 
 <td>[bluemix service bind](index.html#bluemix_service_bind)</td> 
 <td>[bluemix service unbind](index.html#bluemix_service_unbind)</td>
 <td>[bluemix service key-create](index.html#bluemix_service_key_create)</td>
 <td>[bluemix service key-delete](index.html#bluemix_service_key_delete)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix service keys](index.html#bluemix_service_keys) </td> 
 <td>[bluemix service key-show](index.html#bluemix_service_key_show)</td> 
 <td>[bluemix service user-provided-create](index.html#bluemix_service_user_provided_create)</td>
 <td>[bluemix service user-provided-update](index.html#bluemix_service_user_provided_update)</td>
 <td>[bluemix catalog templates](index.html#bluemix_catalog_templates)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix catalog template](index.html#bluemix_catalog_template) </td> 
 <td>[bluemix catalog template-run](index.html#bluemix_catalog_template_run)</td> 
 <td>[bluemix network regions](index.html#bluemix_network_regions)</td>
 <td>[bluemix network region-set](index.html#bluemix_network_region_set)</td>
 <td>[bluemix network routes](index.html#bluemix_network_routes)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix network route-check](index.html#bluemix_network_route_check)</td> 
 <td>[bluemix network route-map](index.html#bluemix_network_route_map)</td> 
 <td>[bluemix network route-unmap](index.html#bluemix_network_route_unmap)</td>
 <td>[bluemix network route-create](index.html#bluemix_network_route_create)</td>
 <td>[bluemix network route-delete](index.html#bluemix_network_route_delete)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix network orphaned-routes-delete](index.html#bluemix_network_orphaned_routes_delete)</td> 
 <td>[bluemix network domains](index.html#bluemix_network_domains)</td> 
 <td>[bluemix network domain-create](index.html#bluemix_network_domain_create)</td>
 <td>[bluemix network domain-delete](index.html#bluemix_network_domain_delete)</td>
 <td>[bluemix network shared-domain-create](index.html#bluemix_network_shared_domain_create)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix network shared-domain-delete](index.html#bluemix_network_shared_domain_delete)</td> 
 <td>[bluemix security cert](index.html#bluemix_security_cert)</td> 
 <td>[bluemix security cert-add](index.html#bluemix_security_cert_add)</td>
 <td>[bluemix security cert-remove](index.html#bluemix_security_cert_remove)</td>
 <td>[bluemix plugin repos](index.html#bluemix_plugin_repos)</td>
 </tr>
 
 <tr> 
 <td>[bluemix plugin repo-add](index.html#bluemix_plugin_repo_add)</td> 
 <td>[bluemix plugin repo-remove](index.html#bluemix_plugin_repo_remove)</td> 
 <td>[bluemix plugin repo-plugins](index.html#bluemix_plugin_repo_plugins)</td>
 <td>[bluemix plugin list](index.html#bluemix_plugin_list)</td>
 <td>[bluemix plugin install](index.html#bluemix_plugin_install)</td>
 </tr>
 
 <tr> 
 <td>[bluemix plugin uninstall](index.html#bluemix_plugin_uninstall)</td> 
 <td>[bluemix ic init](index.html#bluemix_ic_init)</td> 
 <td>[bluemix ic attach](index.html#bluemix_ic_attach)</td>
 <td>[bluemix ic build](index.html#bluemix_ic_build)</td>
 <td>[bluemix ic create](index.html#bluemix_ic_create)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix ic cpi](index.html#bluemix_ic_cpi)</td> 
 <td>[bluemix ic exec](index.html#bluemix_ic_exec)</td> 
 <td>[bluemix ic groups](index.html#bluemix_ic_groups)</td>
 <td>[bluemix ic group-inspect](index.html#bluemix_ic_group_inspect)</td>
 <td>[bluemix ic group-instances](index.html#bluemix_ic_group_instances)</td>
 </tr>
 
 <tr> 
 <td>[bluemix ic group-create](index.html#bluemix_ic_group_create)</td> 
 <td>[bluemix ic group-update](index.html#bluemix_ic_group_update)</td> 
 <td>[bluemix ic group-remove](index.html#bluemix_ic_group_remove)</td>
 <td>[bluemix ic images](index.html#bluemix_ic_images)</td>
 <td>[bluemix ic inspect](index.html#bluemix_ic_inspect)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix ic info](index.html#bluemix_ic_info)</td> 
 <td>[bluemix ic ips](index.html#bluemix_ic_ips)</td> 
 <td>[bluemix ic ip-request](index.html#ip_request)</td>
 <td>[bluemix ic ip-release](index.html#bluemix_ic_ip_release)</td>
 <td>[bluemix ic ip-bind](index.html#bluemix_ic_ip_bind)</td>
 </tr>
 
 <tr> 
 <td>[bluemix ic ip-unbind](index.html#bluemix_ic_ip_unbind)</td> 
 <td>[bluemix ic kill](index.html#bluemix_ic_kill)</td> 
 <td>[bluemix ic namespace-get](index.html#bluemix_ic_namespace_get)</td>
 <td>[bluemix ic namespace-set](index.html#bluemix_ic_namespace_set)</td>
 <td>[bluemix ic pause](index.html#pause)</td>
 </tr>
 
 <tr> 
 <td>[bluemix ic unpause](index.html#unpause)</td> 
 <td>[bluemix ic port](index.html#bluemix_ic_port)</td> 
 <td>[bluemix ic ps](index.html#bluemix_ic_ps)</td>
 <td>[bluemix ic restart](index.html#bluemix_ic_restart)</td>
 <td>[bluemix ic rm](index.html#bluemix_ic_rm)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix ic rmi](index.html#bluemix_ic_rmi)</td> 
 <td>[bluemix ic run](index.html#bluemix_ic_run)</td> 
 <td>[bluemix ic route-map](index.html#bluemix_ic_route_map)</td>
 <td>[bluemix ic route-unmap](index.html#bluemix_ic_route_unmap)</td>
 <td>[bluemix ic start](index.html#ic_start)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix ic stop](index.html#ic_stop)</td> 
 <td>[bluemix ic stats](index.html#bluemix_ic_stats)</td> 
 <td>[bluemix ic top](index.html#bluemix_ic_top)</td>
 <td>[bluemix ic volumes](index.html#bluemix_ic_volumes)</td>
 <td>[bluemix ic volume-inspect](index.html#bluemix_ic_volume_inspect)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix ic volume-create](index.html#bluemix_ic_volume_create)</td> 
 <td>[bluemix ic volume-remove](index.html#bluemix_ic_volume_remove)</td> 
 <td>[bluemix ic volume-fs](index.html#bluemix_ic_volume_fs)</td> 
 <td>[bluemix ic volume-fs-create](index.html#bluemix_ic_volume_fs_create)</td> 
 <td>[bluemix ic volume-fs-remove](index.html#bluemix_ic_volume_fs_remove)</td> 
 </tr>
 
 <tr>
 <td>[bluemix ic volume-fs-inspect](index.html#bluemix_ic_volume_fs_inspect)</td>
 <td>[bluemix ic volume-fs-flavors](index.html#bluemix_ic_volume_fs_flavors)</td> 
 <td>[bluemix ic wait](index.html#bluemix_ic_wait)</td>
 <td>[bluemix ic version](index.html#bluemix_ic_version)</td>
 </tr>
 
 
 </tbody> 
 </table> 

  

## bluemix help
{: #bluemix_help}
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

Hilfe für Befehl `info` anzeigen:

```
bluemix help info
```

Hilfe für den Namensbereich `ic` anzeigen:

```
bluemix help ic
```

oder 

```
bluemix ic help
```

Hilfe für Befehl `group-create` unter Namensbereich `ic` anzeigen:

```
bluemix ic help group-create
```


## bluemix api
{: #bluemix_api}
{{site.data.keyword.Bluemix_notm}}-API-Endpunkt festlegen oder anzeigen. Dieser Befehl schließt den Befehl `cf api` ein.

```
bluemix api [API_ENDPOINT][--unset]
```

**Voraussetzungen**: Keine

**Befehlsoptionen**:

*API_ENDPOINT* (optional): Der API-Endpunkt, der als Ziel verwendet wird, zum Beispiel 'https://api.ng.bluemix.net'.  Wenn weder die Option *API_ENDPOINT* noch die Option `--unset` angegeben wird, wird der aktuelle API-Endpunkt angezeigt.

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
{: #bluemix_login}

Anmeldung des Benutzers. Dieser Befehl schließt den Befehl `cf login` ein. Die Befehlsoption sind dieselben wie die für den Befehl `cf login`.

```
bluemix login [OPTIONS...]
```

**Voraussetzungen**: Endpunkt

**Befehlsoptionen**: Informationen zu den Optionen, die vom Befehl `login` unterstützt werden, finden Sie in den Informationen zur Verwendung des Befehls `cf login` für cf-Befehle zur Verwaltung von Anwendungen.


## bluemix logout
{: #bluemix_logout}

Abmeldung des Benutzers. Dieser Befehl schließt den Befehl `cf logout` ein.

```
bluemix logout
```

**Voraussetzungen**: Keine


## bluemix target
{: #bluemix_target}


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
{: #bluemix_info}

{{site.data.keyword.Bluemix_notm}}-Basisinformationen einschließlich aktueller Region, Cloud-Controller-Version und einigen nützlichen Endpunkten (zum Beispiel zum Anmelden und Austauschen von Zugriffstoken) anzeigen.

```
bluemix info
```

**Voraussetzungen**: Endpunkt


## bluemix config
{: #bluemix_config}


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
{: #bluemix_list}

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

Es kann immer nur eine der Befehlsoptionen `apps`, `containers`, `container-groups` bzw. `vm-groups` gleichzeitig angegeben werden. Wenn keine der Optionen angegeben wird, werden alle cf-Anwendungen, -Container, Containergruppen und -VM-Gruppen aufgelistet.

**Beispiele**:

Alle cf-Anwendungen auflisten:

```
bluemix list apps
```

Alle Containerinstanzen auflisten:

```
bluemix list containers
```

Alle Anwendungen, Container, Containergruppen und VM-Gruppen auflisten:

```
bluemix list
```


## bluemix scale
{: #bluemix_scale}

Scale-in oder Scale-out der cf-Anwendung oder -Containergruppe für eine bestimmte Instanzenanzahl, ein bestimmtes Festplattenkontingent und eine bestimmte Speichergröße durchführen.

**Hinweis:** Zum Skalieren einer Containergruppe kann nur eine Instanzenanzahl angegeben werden. Wenn keine Option angegeben wird, werden durch diesen Befehl die aktuelle Instanzenanzahl für die Containergruppe sowie das Plattenkontingent und die Hauptspeichergröße für die cf-Anwendung aufgelistet.

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
{: #bluemix_curl}

Ausführung einer unformatierten HTTP-Anforderung für {{site.data.keyword.Bluemix_notm}}. *Content-Type* ist standardmäßig auf *application/json* eingestellt. Dieser Befehl sendet die Anforderung an {{site.data.keyword.Bluemix_notm}} Multi-Cloud Control Proxy. Informationen zu den unterstützten Pfaden finden Sie in den API-Pfaddefinitionen im [CloudFoundry-API-Dokument](http://apidocs.cloudfoundry.org/){: new_window}.

```
bluemix curl PATH [OPTIONS...]
```

**Voraussetzungen**: Endpunkt, Anmeldung

**Befehlsoptionen**:

*PATH* (erforderlich): Der URL-Pfad der Ressource. Beispiel: /v2/apps.

*OPTIONS* (optional): Die Optionen, die vom Befehl `bluemix curl` unterstützt werden, sind mit den Optionen identisch, die vom Befehl `cf curl` unterstützt werden.

**Beispiele**:

Informationen für alle Organisationen des aktuellen Kontos anzeigen:

```
bluemix curl /v2/organizations
```


## bluemix iam orgs
{: #bluemix_iam_orgs}

Alle Organisationen auflisten

```
bluemix iam orgs [-r REGION --guid]
```

**Voraussetzungen**: Endpunkt, Anmeldung

**Befehlsoptionen**:

*-r REGION*  (optional): Für welche Region die Organisationsinformationen angezeigt werden sollen. Wenn 'all' angegeben ist, werden alle Organisationen in allen Regionen aufgelistet.

*--guid* (optional): GUID der Organisationen anzeigen.

**Beispiele**:
Alle Organisationen in der angegebenen Region `us-south` auflisten und die GUID anzeigen

```
bluemix iam orgs -r us-south --guid
```

## bluemix iam org
{: #bluemix_iam_org}

Die Informationen für die angegebene Organisation anzeigen

```
bluemix iam org ORG_NAME [--guid]
```

**Voraussetzungen**: Endpunkt, Anmeldung

**Befehlsoptionen**:

*ORG_NAME* (erforderlich): Der Name der Organisation.

*--guid* (optional): GUID der Organisation anzeigen.


**Beispiele**:
Informationen für die Organisation `IBM` mit der GUID anzeigen

```
bluemix iam org IBM --guid
```

## bluemix iam org-create
{: #bluemix_iam_org_create}

Eine neue Organisation erstellen. Diese Operation kann nur vom Kontoeigner ausgeführt werden.

```
bluemix iam org-create ORG_NAME
```

**Voraussetzungen**: Endpunkt, Anmeldung

**Befehlsoptionen**:

*ORG_NAME* (erforderlich): Der Name der Organisation, die erstellt wird.

**Beispiele**:
Organisation mit dem Namen `IBM` erstellen

```
bluemix iam org-create IBM
```


## bluemix iam org-replicate
{: #bluemix_iam_org_replicate}

Repliziert eine Organisation aus der aktuellen Region in eine andere Region.

```
bluemix iam org-replicate ORG_NAME REGION_NAME
```

**Voraussetzungen**: Endpunkt, Anmeldung

**Befehlsoptionen**:

*ORG_NAME* (erforderlich): Der Name der vorhandenen Organisation, die repliziert werden soll.

*REGION_NAME* (erforderlich): Der Name der Region, die die replizierte Organisation hostet.

**Beispiele**:

Die Organisation `myorg` in die Region `eu-gb` replizieren:

```
bluemix iam org-replicate myorg eu-gb
```


## bluemix iam org-rename
{: #bluemix_iam_org_rename}

Eine Organisation umbenennen. Diese Operation kann nur von einem Organisationsmanager ausgeführt werden.

```
bluemix iam org-rename OLD_ORG_NAME NEW_ORG_NAME
```

**Voraussetzungen**: Endpunkt, Anmeldung

**Befehlsoptionen**:

*OLD_ORG_NAME* (erforderlich): Der bisherige Name der Organisation, die umbenannt werden soll.

*NEW_ORG_NAME*  (erforderlich): Der neue Name für die Organisation, die umbenannt werden soll.


## bluemix iam org-delete
{: #bluemix_iam_org_delete}

Die angegebene Organisation in der aktuellen Region löschen.

```
bluemix iam org-delete ORG_NAME [-f --all]
```

**Voraussetzungen**: Endpunkt, Anmeldung

**Befehlsoptionen**:

*ORG_NAME* (erforderlich): Der Name der vorhandenen Organisation, die gelöscht werden soll.

*-f* (optional): Löschen ohne Bestätigung erzwingen.

*--all* (optional): Die Organisation in allen Regionen löschen.


## bluemix iam spaces
{: #bluemix_iam_spaces}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf spaces`.


## bluemix iam space
{: #bluemix_iam_space}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf space`.


## bluemix iam space-create
{: #bluemix_iam_space_create}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf create-space`.


## bluemix iam space-rename
{: #bluemix_iam_space_rename}


Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf rename-space`.


## bluemix iam space-delete
{: #bluemix_iam_space_delete}


Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf delete-space`.


## bluemix iam account-users
{: #bluemix_iam_account_users}

Dem Konto zugeordnete Benutzer anzeigen. Diese Operation kann nur vom Kontoeigner ausgeführt werden.

```
bluemix iam account-users
```

## bluemix iam account-user-invite
{: #bluemix_iam_account-user_inviate}


Lädt den Benutzer zu dem Konto mit bereits festgelegter Organisation und Bereichsrolle ein. Diese Operation kann nur vom Kontoeigner ausgeführt werden.

```
bluemix iam account-user-invite USER_NAME ORG_NAME ORG_ROLE SPACE_NAME SPACE_ROLE
```

**Voraussetzungen**: Endpunkt, Anmeldung


**Befehlsoptionen**:

*USER_NAME* (erforderlich): Der Name des Benutzers, der eingeladen wird.

*ORG_NAME* (erforderlich): Der Name der Organisation, zu der dieser Benutzer eingeladen wird.

*ORG_ROLE* (erforderlich): Der Name der Organisationsrolle, zu der dieser Benutzer eingeladen wird. Beispiel:

<dl>
<dt>OrgManager</dt>
<dd>Diese Rolle kann Benutzer einladen und verwalten, Pläne auswählen und ändern sowie Ausgabenlimits festlegen.</dd>
<dt>BillingManager</dt>
<dd>Diese Rolle kann die Abrechnungskonto- und Zahlungsinformationen erstellen und verwalten.</dd>
<dt>OrgAuditor</dt>
<dd>Diese Rolle verfügt über Lesezugriff auf die Organisationsinformationen und -berichte. </dd>
</dl> 

*SPACE_NAME* (erforderlich): Der Name des Bereichs, zu dem dieser Benutzer eingeladen wird.

*SPACE_ROLE* (erforderlich): Der Name der Bereichsrolle, zu der dieser Benutzer eingeladen wird. Beispiel:

<dl>
<dt>SpaceManager</dt>
<dd>Diese Rolle kann Benutzer einladen und verwalten sowie Funktionen für einen angegebenen Bereich aktivieren.</dd>
<dt>SpaceDeveloper</dt>
<dd>Diese Rolle kann Apps und Services erstellen und verwalten sowie Protokolle und Berichte anzeigen.</dd>
<dt>SpaceAuditor</dt>
<dd>Diese Rolle kann Protokolle, Berichte und Einstellungen für den Bereich anzeigen.</dd>
</dl> 

**Beispiele**:

Die Benutzerin `Mary` zur Organisation `IBM` einladen und die Rolle `OrgManager` sowie den Bereich `Cloud` mit der Rolle `SpaceAuditor` zuweisen:

```
bluemix iam account-user-inviate Mary IBM OrgManager Cloud SpaceAuditor
```

## bluemix iam org-users
{: #bluemix_iam_org_users}

Benutzer in der angegebenen Organisation nach Rolle anzeigen

```
bluemix iam org-users ORG_NAME [-a]
```

**Voraussetzungen**: Endpunkt, Anmeldung

**Befehlsoptionen**:

*ORG_NAME* (erforderlich): Der Name der Organisation.

*-a* (optional): Alle Benutzer in der angegebenen Organisation auflisten (nicht nach Rolle gruppiert).


## bluemix iam org-role-set
{: #bluemix_iam_org_role_set}

Einem Benutzer eine Organisationsrolle zuweisen. Diese Operation kann nur von einem Organisationsmanager ausgeführt werden.

```
bluemix iam org-role-set USER_NAME ORG_NAME ORG_ROLE
```

**Voraussetzungen**: Endpunkt, Anmeldung

**Befehlsoptionen**:

*USER_NAME* (erforderlich): Der Name des Benutzers, der zugeordnet wird.

*ORG_NAME* (erforderlich): Der Name der Organisation, der dieser Benutzer zugeordnet wird.

*ORG_ROLE* (erforderlich): Der Name der Organisationsrolle, der dieser Benutzer zugeordnet wird. Beispiel:

<dl>
<dt>OrgManager</dt>
<dd>Diese Rolle kann Benutzer einladen und verwalten, Pläne auswählen und ändern sowie Ausgabenlimits festlegen.</dd>
<dt>BillingManager</dt>
<dd>Diese Rolle kann die Abrechnungskonto- und Zahlungsinformationen erstellen und verwalten.</dd>
<dt>OrgAuditor</dt>
<dd>Diese Rolle verfügt über Lesezugriff auf die Organisationsinformationen und -berichte. </dd>
</dl> 

**Beispiele**:

Die Benutzerin `Mary` der Organisation `IBM` mit der Rolle `OrgManager` zuweisen:

```
bluemix iam org-role-set Mary IBM OrgManager
```


## bluemix iam org-role-unset
{: #bluemix_iam_org_role_unset}

Eine Organisationsrolle für einen Benutzer entfernen (widerrufen). Diese Operation kann nur von einem Organisationsmanager ausgeführt werden.

```
bluemix iam org-role-unset USER_NAME ORG_NAME ORG_ROLE
```

**Voraussetzungen**: Endpunkt, Anmeldung

**Befehlsoptionen**:

*USER_NAME* (erforderlich): Der Name des Benutzers, der entfernt wird.

*ORG_NAME* (erforderlich): Der Name der Organisation, aus der dieser Benutzer entfernt wird.

*ORG_ROLE* (erforderlich): Der Name der Organisationsrolle, aus der dieser Benutzer entfernt wird. Beispiel:

<dl>
<dt>OrgManager</dt>
<dd>Diese Rolle kann Benutzer einladen und verwalten, Pläne auswählen und ändern sowie Ausgabenlimits festlegen.</dd>
<dt>BillingManager</dt>
<dd>Diese Rolle kann die Abrechnungskonto- und Zahlungsinformationen erstellen und verwalten.</dd>
<dt>OrgAuditor</dt>
<dd>Diese Rolle verfügt über Lesezugriff auf die Organisationsinformationen und -berichte. </dd>
</dl> 

**Beispiele**:

Die Benutzerin `Mary` aus der Organisation `IBM` und der Rolle `OrgManager` entfernen:

```
bluemix iam org-role-unset Mary IBM OrgManager
```


## bluemix iam space-users
{: #bluemix_iam_space_users}

Benutzer in dem angegebenen Bereich nach Rolle anzeigen

```
bluemix iam space-users ORG_NAME SPACE_NAME
```

**Voraussetzungen**: Endpunkt, Anmeldung

**Befehlsoptionen**:

*ORG_NAME* (erforderlich): Der Name der Organisation.

*SPACE_NAME* (erforderlich): Der Name des Bereichs.


## bluemix iam space-role-set
{: #bluemix_iam_space_role_set}

Einem Benutzer eine Bereichsrolle zuweisen. Diese Operation kann nur von einem Bereichsmanager ausgeführt werden.

```
bluemix iam space-role-set USER_NAME ORG_NAME SPACE_NAME SPACE_ROLE
```

**Voraussetzungen**: Endpunkt, Anmeldung

**Befehlsoptionen**:

*USER_NAME* (erforderlich): Der Name des Benutzers, der zugeordnet wird.

*ORG_NAME* (erforderlich): Der Name der Organisation, der dieser Benutzer zugeordnet wird.

*SPACE_NAME* (erforderlich): Der Name des Bereichs, dem dieser Benutzer zugeordnet wird.

*SPACE_ROLE* (erforderlich): Der Name der Bereichsrolle, die diesem Benutzer zugeordnet wird. Beispiel:

<dl>
<dt>SpaceManager</dt>
<dd>Diese Rolle kann Benutzer einladen und verwalten sowie Funktionen für einen angegebenen Bereich aktivieren.</dd>
<dt>SpaceDeveloper</dt>
<dd>Diese Rolle kann Apps und Services erstellen und verwalten sowie Protokolle und Berichte anzeigen.</dd>
<dt>SpaceAuditor</dt>
<dd>Diese Rolle kann Protokolle, Berichte und Einstellungen für den Bereich anzeigen.</dd>
</dl> 


**Beispiele**:

Die Benutzerin `Mary` der Organisation `IBM` und dem Bereich `Cloud` mit der Rolle `SpaceManager` zuweisen:

```
bluemix iam space-role-set Mary IBM Cloud SpaceManager
```

## bluemix iam space-role-unset
{: #bluemix_iam_space_role_unset}

Eine Bereichsrolle für einen Benutzer entfernen (widerrufen). Diese Operation kann nur von einem Bereichsmanager ausgeführt werden.

```
bluemix iam space-role-unset USER_NAME ORG_NAME SPACE_NAME SPACE_ROLE
```

**Voraussetzungen**: Endpunkt, Anmeldung

**Befehlsoptionen**:

*USER_NAME* (erforderlich): Der Name des Benutzers, der entfernt wird.

*ORG_NAME* (erforderlich): Der Name der Organisation, aus der dieser Benutzer entfernt wird.

*SPACE_NAME* (erforderlich): Der Name des Bereichs, aus dem dieser Benutzer entfernt wird.

*SPACE_ROLE* (erforderlich): Der Name der Bereichsrolle, aus der dieser Benutzer entfernt wird. Beispiel:

<dl>
<dt>SpaceManager</dt>
<dd>Diese Rolle kann Benutzer einladen und verwalten sowie Funktionen für einen angegebenen Bereich aktivieren.</dd>
<dt>SpaceDeveloper</dt>
<dd>Diese Rolle kann Apps und Services erstellen und verwalten sowie Protokolle und Berichte anzeigen.</dd>
<dt>SpaceAuditor</dt>
<dd>Diese Rolle kann Protokolle, Berichte und Einstellungen für den Bereich anzeigen.</dd>
</dl> 

**Beispiele**:

Die Benutzerin `Mary` aus der Organisation `IBM` und dem Bereich `Cloud` mit der Rolle `SpaceManager` entfernen:

```
bluemix iam space-role-unset Mary IBM Cloud SpaceManager
```


## bluemix app push
{: #bluemix_app_push}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf push`.


## bluemix app list
{: #bluemix_app_list}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf apps`.


## bluemix app show
{: #bluemix_app_show}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf app`.


## bluemix app scale
{: #bluemix_app_scale}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf scale`.


## bluemix app delete
{: #bluemix_app_delete}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf delete`.


## bluemix app rename
{: #bluemix_app_rename}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf rename`.


## bluemix app start
{: #bluemix_app_start}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf start`.


## bluemix app stop
{: #bluemix_app_stop}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf stop`.


## bluemix app restart
{: #bluemix_app_restart}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf restart`.


## bluemix app restage
{: #bluemix_app_restage}


Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf restage`.


## bluemix app instance-restart
{: #bluemix_app_instance_restart}


Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf restart-app-instance`.


## bluemix app events
{: #bluemix_app_events}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf events`.


## bluemix app files
{: #bluemix_app_files}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf files`.


## bluemix app logs
{: #bluemix_app_logs}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf logs`.


## bluemix app env
{: #bluemix_app_env}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf env`.


## bluemix app env-set
{: #bluemix_app_env_set}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf set-env`.


## bluemix app env-unset
{: #bluemix_app_env_unset}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf unset-env`.


## bluemix app stacks
{: #bluemix_app_stacks}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf stacks`.


## bluemix app stack
{: #bluemix_app_stack}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf stack`.


## bluemix app manifest-create
{: #bluemix_app_manifest_create}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf create-app-manifest`.


## bluemix service offerings
{: #bluemix_service_offerings}


Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf marketplace`.


## bluemix service list
{: #bluemix_service_list}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf services`.


## bluemix service show
{: #bluemix_service_show}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf service`.


## bluemix service create
{: #bluemix_service_create}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf create-service`.


## bluemix service update
{: #bluemix_service_update}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf update-service`.


## bluemix service delete
{: #bluemix_service_delete}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf delete-service`.


## bluemix service rename
{: #bluemix_service_rename}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf rename-service`.


## bluemix service bind
{: #bluemix_service_bind}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf bind-service`.


## bluemix service unbind
{: #bluemix_service_unbind}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf unbind-service`.


## bluemix service key-create
{: #bluemix_service_key_create}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf create-service-key`.


## bluemix service key-delete
{: #bluemix_service_key_delete}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf delete-service-key`.


## bluemix service keys
{: #bluemix_service_keys}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf service-keys`.


## bluemix service key-show
{: #bluemix_service_key_show}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf service-key`.


## bluemix service user-provided-create
{: #bluemix_service_user_provided_create}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf create-user-provided-service`.


## bluemix service user-provided-update
{: #bluemix_service_user_provided_update}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf update-user-provided-service`.


## bluemix catalog templates
{: #bluemix_catalog_templates}

Zeigt die Boilerplate-Vorlagen in Bluemix an.

```
bluemix catalog templates [-d]
```

**Voraussetzungen**: Endpunkt, Anmeldung

**Befehlsoptionen**:

-d (optional): Wenn die Option `-d` angegeben wird, wird auch die Beschreibung jeder Vorlage angezeigt. Andernfalls werden nur die ID und der Name jeder Vorlage angezeigt.


## bluemix catalog template
{: #bluemix_catalog_template}

Zeigt die detaillierten Informationen einer angegebenen Boilerplate-Vorlage an.

```
bluemix catalog template TEMPLATE_ID
```

**Voraussetzungen**: Endpunkt, Anmeldung

**Befehlsoptionen**:

*TEMPLATE_ID* (erforderlich): Die ID der Boilerplate-Vorlage. Verwenden Sie den Befehl 'bluemix templates', um die IDs aller Vorlagen anzuzeigen.

**Beispiele**:

Details der Vorlage `mobileBackendStarter` anzeigen:

```
bluemix catalog template mobileBackendStarter
```


## bluemix catalog template-run
{: #bluemix_catalog_template_run}

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


## bluemix network regions
{: #bluemix_network_regions}

Zeigt die Informationen für alle Regionen in {{site.data.keyword.Bluemix_notm}} an.

```
bluemix network regions
```

**Voraussetzungen**: Endpunkt


## bluemix network region-set
{: #bluemix_network_region_set}

Wechselt zur angegebenen Region. Von diesem Befehl wird automatisch auf dieselbe Organisation und denselben Bereich in der neuen Region zurückverwiesen (sofern möglich). Andernfalls wird der Benutzer durch den Befehl aufgefordert, eine neue Organisation und einen neuen Bereich auszuwählen, wenn der Benutzer bereits angemeldet ist. Der API-Endpunkt wird entsprechend geändert.

```
bluemix network region-set REGION_NAME
```

**Voraussetzungen**: Endpunkt

**Befehlsoptionen**:

*REGION_NAME* (erforderlich): Der Name der Region, zu der Sie wechseln möchten. Mit dem Befehl `bluemix network regions` können Sie alle Regionsnamen anzeigen.

**Beispiele**:

Als aktuelle Region `eu-gb` festlegen:

```
bluemix network region-set eu-gb
```


## bluemix network routes
{: #bluemix_network_routes}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf routes`.


## bluemix network route-check
{: #bluemix_network_route_check}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf check-route`.


## bluemix network route-map
{: #bluemix_network_route_map}

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
{: #bluemix_network_route_unmap}

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
{: #bluemix_network_route_create}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf create-route`.


## bluemix network route-delete
{: #bluemix_network_route_delete}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf delete-route`.


## bluemix network orphaned-routes-delete
{: #bluemix_network_orphaned_routes_delete}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf delete-orphaned-routes`.


## bluemix network domains
{: #bluemix_network_domains}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf domains`.


## bluemix network domain-create
{: #bluemix_network_domain_create}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf create-domain`.


## bluemix network domain-delete
{: #bluemix_network_domain_delete}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf delete-domain`.


## bluemix network shared-domain-create
{: #bluemix_network_shared_domain_create}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf create-shared-domain`.


## bluemix network shared-domain-delete
{: #bluemix_network_shared_domain_delete}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf delete-shared-domain`.


## bluemix security cert
{: #bluemix_security_cert}

Die Zertifikatsinformationen für eine Domäne auflisten

```
bluemix security cert DOMAIN_NAME
```

**Voraussetzungen**: Endpunkt, Anmeldung

**Befehlsoptionen**:

*DOMAIN_NAME* (erforderlich): Die Domäne, in der das Zertifikat gehostet wird.

**Beispiele**:

Die Zertifikatsinformationen für die Domäne `ibmcxo-eventconnect.com` anzeigen:

```
bluemix security cert ibmcxo-eventconnect.com
```


## bluemix security cert-add
{: #bluemix_security_cert_add}

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
{: #bluemix_security_cert_remove}

Entfernt ein Zertifikat aus der angegebenen Domäne in der aktuellen Organisation.

```
bluemix security cert-remove DOMAIN [-f]
```

**Voraussetzungen**: Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**:

*DOMAIN* (erforderlich): Die Domäne, aus der das Zertifikat entfernt werden soll.

-f  (optional): Löschung ohne Bestätigung erzwingen.







## bluemix plugin repos
{: #bluemix_plugin_repos}

Listet alle Plug-in-Repositorys auf, die in der Befehlszeilenschnittstelle von {{site.data.keyword.Bluemix_notm}} registriert sind.

```
bluemix plugin repos
```

**Voraussetzungen**: Keine


## bluemix plugin repo-add
{: #bluemix_plugin_repo_add}

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
{: #bluemix_plugin_repo_remove}

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


## bluemix plugin repo-plugins
{: #bluemix_plugin_repo_plugins}

Listet alle verfügbaren Plug-ins in allen hinzugefügten Repositorys oder einem bestimmten Repository auf.

```
bluemix plugin repo-plugins [-r REPO_NAME]
```

**Voraussetzungen**: Keine

**Befehlsoptionen**:

-r *REPO_NAME* (optional): Listet nur die Plug-ins im angegebenen Repository auf.

**Beispiele**:

Alle Plug-ins in allen hinzugefügten Repositorys auflisten:

```
bluemix plugin repo-plugins
```

Alle Plug-ins im Repositorys `bluemix-repo` auflisten:

```
bluemix plugin repo-plugins -r bluemix-repo
```


## bluemix plugin list
{: #bluemix_plugin_list}

Listet alle in der Befehlszeilenschnittstelle von {{site.data.keyword.Bluemix_notm}} installierten Plug-ins auf.

```
bluemix plugin list
```

**Voraussetzungen**: Keine


## bluemix plugin install
{: #bluemix_plugin_install}

Installiert die angegebene Version des Plug-ins in der {{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle aus dem angegebenen Pfad oder Repository.

```
bluemix plugin install PLUGIN_PATH|PLUGIN_NAME [-r REPO_NAME][-v VERSION]
```

**Voraussetzungen**: Keine

**Befehlsoptionen**:

*PLUGIN_PATH*|*PLUGIN_NAME* (erforderlich): Wenn `-r *REPO_NAME*` nicht angegeben wird, wird das Plug-in vom angegebenen lokalen Pfad oder der Remote URL installiert.

-r *REPO_NAME* (optional): Der Name des Repositorys, in dem sich die Binärdatei des Plug-ins befindet.
-v *VERSION* (optional): Die Version des Plug-ins, die installiert werden soll. Bei keiner Angabe wird die letzte Version des Plug-ins installiert. Diese Option ist nur gültig, wenn Sie das Plug-in aus dem Repository installieren.

**Beispiele**:

Plug-in von einer lokalen Datei installieren:

```
bluemix plugin install /downloads/new_plugin
```

Plug-in von der Remote URL installieren:

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
{: #bluemix_plugin_uninstall}

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


## bluemix ic init
{: #bluemix_ic_init}

Initialisiert die Containerumgebung auf Ihrer lokalen Maschine, um den vollen Funktionsumfang des IBM Containers-Service verwenden zu können.

```
bluemix ic init
```

**Voraussetzungen**: Endpunkt, Anmeldung, Ziel

**Hinweis:** Stellen Sie vor der Initialisierung sicher, dass die Docker-CLI (docker) installiert und in Ihrer Umgebungsvariablen PATH konfiguriert ist. Wenn Sie zu einer anderen Region wechseln wollen, verwenden Sie den Befehl `bluemix region-set`. 

**Beispiele**:

Wechselt zur Region `us-south`:

```
bluemix region-set us-south
```


## bluemix ic attach
{: #bluemix_ic_attach}

Dient zum Steuern eines aktiven Containers oder zum Anzeigen der Ausgabe des Containers. Verwenden Sie die Tastenkombination `STRG+C`, um die Verarbeitung zu beenden und den Container zu stoppen. Dieser Befehl ruft die Docker-CLI auf. Weitere Informationen finden Sie unter dem Befehl [attach](https://docs.docker.com/reference/commandline/attach/){: new_window} in der Docker-Hilfe. 

```
bluemix ic attach [--no-stdin][--sig-proxy] CONTAINER
```

**Voraussetzungen**: Endpunkt, Anmeldung, Ziel, Docker

**Befehlsoptionen**:

--no-stdin (optional): Standardeingabe nicht einschließen.

--sig-proxy (optional): Alle empfangenen Signale an den Prozess weiterleiten. Standardwert: **true**.

*CONTAINER* (erforderlich): Der Name oder die ID des Containers.

**Beispiele**:

Das folgende Beispiel zeigt eine Anforderung für die Zuordnung zum Container `my_container`:
```
bluemix ic attach my_container
```


## bluemix ic build
{: #bluemix_ic_build}

Ruft den Build-Service für IBM Containers auf, um ein Docker-Image lokal oder in Ihrem privaten {{site.data.keyword.Bluemix_notm}}-Repository zu erstellen. Dieser Befehl ruft die Docker-CLI auf. Weitere Informationen finden Sie unter dem Befehl [build](https://docs.docker.com/reference/commandline/build/){: new_window} in der Docker-Hilfe. 

```
bluemix ic build -t TAG|--tag TAG [--no-cache][-p|--pull] [-q|--quiet] DOCKERFILE_LOCATION
```

**Voraussetzungen**: Endpunkt, Anmeldung, Ziel, Docker

**Befehlsoptionen**:

-t *TAG*|--tag *TAG* (erforderlich): Der Repository-Name, der auf das erstellte Image anzuwenden ist.

--no-cache (optional): Den Cache nicht verwenden, wenn das Image erstellt wird. Der Standardwert ist **false**.

-p|--pull (optional): Versuchen, das Basisimage mit Pull-Operation aus der Registry zu extrahieren, auch wenn es im Cache gespeichert ist.

-q|--quiet (optional): Die von den Containern generierte ausführliche Ausgabe unterdrücken. Der Standardwert ist **false**.

*DOCKERFILE_LOCATION* (erforderlich): Der Pfad zur Dockerfile und zum Kontext auf dem lokalen Host.

**Beispiele**:

Das folgende Beispiel zeigt eine Anforderung zum Erstellen eines Image mit dem Namen *myimage*. Die Dockerfile und andere im Build zu verwendende Artefakte befinden sich in dem Verzeichnis, in dem der Befehl ausgeführt wird. Da die Registry und der Namensbereich im Imagenamen enthalten sind, wird das Image im privaten {{site.data.keyword.Bluemix_notm}}-Repository Ihrer Organisation erstellt.
```
bluemix ic build -t registry.ng.bluemix.net/mynamespace/myimage .
```


## bluemix ic create
{: #bluemix_ic_create}

Erstellt einen neuen Container in Ihrem {{site.data.keyword.Bluemix_notm}}-Repository. Dieser Befehl schließt den Befehl `docker create` ein. Weitere Informationen finden Sie unter dem Befehl [create](https://docs.docker.com/reference/commandline/create/){: new_window} in der Docker-Hilfe.


## bluemix ic cpi
{: #bluemix_ic_cpi}

Greift auf ein Docker Hub-Image oder auf ein Image in Ihrer lokalen Registry zu und kopiert das Image in Ihr privates {{site.data.keyword.Bluemix_notm}}-Repository.

```
bluemix ic cpi SOURCE_IMAGE DESTINATION_IMAGE
```

**Voraussetzungen**: Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**:

*SOURCE_IMAGE* (erforderlich): Der Name des Quellenrepositorys und des Quellenimage.

*DESTINATION_IMAGE* (erforderlich): Die URL des privaten {{site.data.keyword.Bluemix_notm}}-Repositorys, die den Namensbereich und den Namen des Zielimage einschließt. Ein Tag für das Image ist optional.

**Beispiele**:

Image aus dem Quellenrepository in Ihr privates Repository kopieren und einen Tag für das Image hinzufügen:

```
bluemix ic cpi source_repository/source_image_name private_registry_URL/destination_image_name:tag
```

Das Image `sinatra` aus dem Repository `training` in Ihr privates Repository `registry.ng.bluemix.net/mynamespace` kopieren und das Image mit dem Namen `mysinatra` benennen. Den Tag `v1` für das Image `mysinatra` hinzufügen. 

```
bluemix ic cpi training/sinatra registry.ng.bluemix.net/mynamespace/mysinatra:v1
```


## bluemix ic exec
{: #bluemix_ic_exec}


Führt einen Befehl in einem Container aus. Weitere Informationen finden Sie unter dem Befehl [exec](https://docs.docker.com/reference/commandline/exec/){: new_window} in der Docker-Hilfe.

```
bluemix ic exec [-d|--detach][-it] [-u USER|--user USER] CONTAINER [CMD]
```

**Voraussetzungen**: Endpunkt, Anmeldung, Ziel, Docker

**Befehlsoptionen**:

-d|--detach (optional): Angegebenen Befehl im Hintergrund ausführen.

-it (optional): Interaktiver Modus. Anzeige der Standardeingabe beibehalten. Geben Sie `exit` zum Beenden ein.

-u *USER*|--user *USER* (optional): Der Benutzername.

*CONTAINER* (erforderlich): Der Name oder die ID des Containers.

*CMD* (optional): Der in dem angegebenen Container bzw. den angegebenen Containern auszuführende Befehl.

**Beispiele**:

Befehl `bash` im Container `my_container` im interaktiven Modus ausführen:

```
bluemix ic exec -it my_container bash
```

Befehl `date` im Container `my_container` ausführen:

```
bluemix ic exec my_container date
```


## bluemix ic groups
{: #bluemix_ic_groups}

Listet Containergruppen im privaten {{site.data.keyword.Bluemix_notm}}-Repository der Organisation auf.

```
bluemix ic groups
```

**Voraussetzungen**: Endpunkt, Anmeldung, Ziel


## bluemix ic group-inspect
{: #bluemix_ic_group_inspect}

Zeigt detaillierte Informationen an, wie zum Beispiel Umgebungsvariablen, Ports oder Speicher, die für eine Containergruppe bei der Erstellung angegeben wurden.

```
bluemix ic group-inspect CONTAINER_GROUP
```

**Voraussetzungen**: Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**:

*CONTAINER_GROUP* (erforderlich): Die ID oder der Name der Containergruppe.

**Beispiele**:

Das folgende Beispiel zeigt eine Anforderung zum Überprüfen der Containergruppe `my_group`:
```
bluemix ic group-inspect my_group
```


## bluemix ic group-instances
{: #bluemix_ic_group_instances}

Listet Instanzen einer angegebenen Containergruppe auf.

```
bluemix ic group-instances CONTAINER_GROUP
```

**Voraussetzungen**: Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**:

*CONTAINER_GROUP* (erforderlich): Die ID oder der Name der Containergruppe.

**Beispiele**:

Alle Instanzen der Containergruppe `my_group` auflisten:
```
bluemix ic group-instances my_group
```


## bluemix ic group-create
{: #bluemix_ic_group_create}

Erstellt eine skalierbare Containergruppe.

```
bluemix ic group-create [-p PORT|--publish port][-m MEMORY|--memory MEMORY] [-e ENV|--env ENV][-v VOLUME:CONTAINER_PATH] [--min MIN][--max MAX] [--desired DESIRED][--auto] [-n HOST|--hostname HOST][-d DOMAIN|--domain DOMAIN] [--name NAME] IMAGE [CMD]
```

**Voraussetzungen**:  Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**:

-m *MEMORY*|--memory *MEMORY* (optional): Der Gruppe eine Speicherbegrenzung in MB zuweisen. Wenn Sie eine Containergruppe über die CLI erstellen, ist der Standardwert für jede Containerinstanz `64` MB. Wenn Sie eine Containergruppe über das {{site.data.keyword.Bluemix_notm}}-Dashboard erstellen, ist der Standardwert für jede Containerinstanz `256` MB. Gültige Werte: `64`, `256`, `512`, `1024` und `2048`. Nach der Zuweisung einer Speicherbegrenzung kann der Wert nicht mehr geändert werden.

-e *ENV*|--env *ENV* (optional): Die Umgebungsvariable festlegen, wobei **ENV** ein `schlüssel=wert`-Paar ist. Geben Sie mehrere Schlüssel separat an. Wenn Anführungszeichen angegeben werden, geben Sie sie so an, dass der Name und der Wert der Umgebungsvariablen eingeschlossen werden. Beispiel: `-e "schlüssel1=wert1" -e "schlüssel2=wert2" -e "schlüssel3=wert3"`.  In der folgenden Tabelle sind einige häufig verwendete Umgebungsvariablen aufgeführt, die Sie angeben können:

|  Umgebungsvariable                              |     Beschreibung                            |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;app-name&gt;*       | Bindet einen Service an einen Container. Mit der Umgebungsvariablen `CCS_BIND_APP` können Sie eine App an den Container binden. Die App wird an den Zielservice gebunden und fungiert als Bridge, über die {{site.data.keyword.Bluemix_notm}} die Informationen aus der Umgebungsvariablen `VCAP_SERVICES` Ihrer Bridge-App in die aktive Containerinstanz übertragen kann. Weitere Informationen zur Erstellung einer Bridge-App finden Sie unter [Service an einen Container binden](http://www.ng.bluemix.net/docs/containers/container_creating_ov.html#container_binding_ov){: new_window}. |
| CCS_SSH_KEY=*&lt;öffentlicher_ssh-schlüssel&gt;* | Fügt einem Container einen SSH-Schlüssel hinzu, wenn Sie den Container erstellen. Sie können den SSH-Schlüssel mithilfe der Umgebungsvariablen hinzufügen, wenn Sie den Container über das {{site.data.keyword.Bluemix_notm}}-Dashboard oder über die CLI erstellen. Weitere Informationen zu SSH-Schlüsseln finden Sie unter [Bei einem Container anmelden](http://www.ng.bluemix.net/docs/containers/container_creating_ov.html#container_cli_login_ssh){: new_window}. |
| LOG_LOCATIONS=*&lt;dateipfad&gt;* | Fügt eine Protokolldatei für die Überwachung im Container hinzu. Fügen Sie die Umgebungsvariable `LOG_LOCATIONS` mit einem Pfad zu der Protokolldatei ein. |
*Tabelle 1. Häufig verwendete Umgebungsvariablen*

-v VOLUME:CONTAINER_PATH[:ro]|--volume VOLUME:CONTAINER_PATH[:ro](optional): Datenträger einem Container durch Angabe der Details im Format `VolumeId:ContainerPath[:ro]` zuordnen.

- *VOLUME*: Die ID oder der Name des Datenträgers.
- *CONTAINER_PATH*: Der absolute Pfad zu dem Datenträger in dem Container.
- ro: Optional. Die Angabe `ro` aktiviert den Schreibschutz des Datenträgers anstelle des standardmäßigen Lese-/Schreibzugriffs.

-p *PORT*|--publish *PORT* (optional): Macht den Port für den HTTP-Datenverkehr verfügbar. Container in Ihrer Gruppe müssen über den HTTP-Port empfangsbereit sein. HTTPS-Anforderungen sind nicht möglich. Für Containergruppen können Sie nicht mehrere Ports einschließen.

Wenn Sie einen Port angeben, machen Sie die App für {{site.data.keyword.Bluemix_notm}} Load Balancer oder Container verfügbar. Anschließend können Bluemix Load Balancer oder die Container den Port verwenden, um den Host und die App in demselben {{site.data.keyword.Bluemix_notm}}-Bereich zu erreichen. Anschließend können die {{site.data.keyword.Bluemix_notm}}-Lastausgleichsfunktion oder -Container den Port verwenden, um den Host und die App im selben {{site.data.keyword.Bluemix_notm}}-Bereich zu erreichen. Wenn ein Port in der Dockerfile für das Image, das Sie verwenden, angegeben ist, schließen Sie diesen Port ein.

**Tipp:**

- Für das von IBM zertifizierte Liberty Server-Image oder für eine modifizierte Version dieses Image geben Sie Port 9080 ein.
- Für das von IBM zertifizierte Node.js-Image oder für eine modifizierte Version dieses Image geben Sie Port 8000 ein.

--min *MIN* (optional): Die minimale Anzahl von Instanzen. Der Standardwert ist **1**. Wenn Sie eine minimale Anzahl von Instanzen festlegen, kann der Wert nach der Erstellung der Containergruppe nicht mehr geändert werden.

--max *MAX* (optional): Die maximale Anzahl von Instanzen. Der Standardwert ist **2**. Wenn Sie eine maximale Anzahl von Instanzen festlegen, kann der Wert nach der Erstellung der Containergruppe nicht mehr geändert werden.

--desired *DESIRED* (optional): Die Anzahl der von Ihnen benötigten Instanzen. Der Standardwert ist **2**.

--auto (optional): Wenn die Containergruppe erstellt wurde und die automatische Wiederherstellung aktiviert ist, überprüft IBM Containers den Status jeder Instanz mit einer HTTP-Anforderung an den Port, der zugewiesen wurde.

Wenn in zwei aufeinander folgenden Intervallen von 90 Sekunden keine Antwort von einer Containerinstanz empfangen wird, wird die Instanz entfernt und durch eine neue Instanz ersetzt. Wenn der Container antwortet, wird keine Aktion ausgeführt. Dieser Prozess wird kontinuierlich wiederholt. Wenn die Gesamtzahl verschiedener Container, die Mitglieder der Gruppe sind, während eines 30-Minuten-Fensters drei oder mehrmal die maximale Größe der Gruppe überschreitet, wird die automatische Wiederherstellung für die Containergruppe permanent inaktiviert. Zur erneuten Aktivierung der automatischen Wiederherstellung müssen Sie die Containergruppe neu erstellen.

-n *HOST*|--hostname *HOST* (optional): Der Hostname, z. B. `mycontainerhost`. Der Hostname und der Domänenname werden zum vollständigen Wert der öffentlichen Routen-URL kombiniert. Beispiel: `http://mycontainerhost.mybluemix.net`. Wenn Sie die Details einer Containergruppe mit dem Befehl `bluemix ic group-inspect` untersuchen, werden der Host und die Domäne zusammen als Route aufgeführt.

-d *DOMAIN*|--domain *DOMAIN* (optional): In der Regel ist die Domäne `.mybluemix.net`. Der Hostname und der Domänenname werden zum vollständigen Wert der öffentlichen Routen-URL kombiniert. Beispiel: `http://mycontainerhost.mybluemix.net`. Wenn Sie die Details einer Containergruppe mit dem Befehl `bluemix ic group-inspect` untersuchen, werden der Host und die Domäne zusammen als Route aufgeführt.

--name *NAME* (erforderlich): Der Gruppe einen Namen zuweisen. `-n` ist veraltet.

**Tipp:** Der Containername muss mit einem Buchstaben beginnen. Der Name kann Großbuchstaben, Kleinbuchstaben, Ziffern, Punkte (`.`), Unterstreichungszeichen (`_`) oder Bindestriche (`-`) enthalten.

*IMAGE* (erforderlich): Das Image, das in jede Containerinstanz in der Containergruppe eingeschlossen werden soll. Sie können Befehle nach dem Image auflisten, fügen Sie jedoch keine Optionen nach dem Image ein. Fügen Sie alle Optionen ein, bevor Sie ein Image angeben.

Wenn Sie ein Image im privaten {{site.data.keyword.Bluemix_notm}}-Repository Ihrer Organisation verwenden, geben Sie das Image im folgenden Format an: `registry.ng.bluemix.net/NAMENSBEREICH/IMAGE`.

Wenn Sie ein Image verwenden, das durch IBM Containers bereitgestellt wird, geben Sie nicht den Namensbereich Ihrer Organisation an. Geben Sie das Image im folgenden Format an: `registry.ng.bluemix.net/IMAGE`.

*CMD*  (optional): Der Befehl und die Argumente, die an die Containergruppe zur Ausführung übergeben werden. Dieser Befehl muss ein Befehl mit langer Laufzeit sein. Verwenden Sie keinen Befehl mit kurzer Laufzeit, beispielsweise **/bin/date**, da ein Befehl mit kurzer Laufzeit dazu führen kann, dass der Container abstürzt.

**Hinweis:**
- Der Befehl und seine Argumente müssen am Ende der Befehlszeile von `bluemix ic run` kommen.
- Wenn die Befehlsargumente einen Bindestrich (`-`) enthalten, wie in `-c` im vorherigen Beispielbefehl, müssen dem Befehl zwei Bindestriche (`--`) vorangestellt werden.



**Beispiele**:

Containergruppe `my_container_group` unter Verwendung des Image `registry.ng.bluemix.net/ibmnode`, das von IBM Containers bereitgestellt wird, erstellen und anschließend den Befehl `ping localhost` mit langer Laufzeit für diese Containergruppe ausführen:

```
bluemix ic group-create --name my_container_group registry.ng.bluemix.net/ibmnode ping localhost
```

Containergruppe `my_container_group` unter Verwendung des Image `registry.ng.bluemix.net/ibmnode`, das von IBM Containers bereitgestellt wird, erstellen und anschließend den Befehl `tail -f /dev/null` mit langer Laufzeit für diese Containergruppe ausführen:

```
bluemix ic group-create --name my_container_group registry.ng.bluemix.net/ibmnode -- tail -f /dev/null
```

Skalierbare Gruppe `mygroup` mit aktivierter automatischer Wiederherstellung unter Verwendung des Image `registry.ng.bluemix.net/ibmliberty` erstellen. Der Port ist `9080`, der Hostname ist `mycontainerhost` und der Domänenname ist `.mybluemix.net`.
```
bluemix ic group-create -p 9080 --auto -n mycontainerhost -d .mybluemix.net --name mygroup registry.ng.bluemix.net/ibmliberty 
```


## bluemix ic group-update
{: #bluemix_ic_group_update}

Aktualisiert eine Containergruppe.


```
bluemix ic group-update [--min MIN][--max MAX] [--desired DESIRED][--auto] CONTAINER_GROUP
```

**Tipp:** Verwenden Sie zum Aktualisieren des Hostnamens oder der Domäne für eine Containergruppe den Befehl `bluemix ic route-map [-n HOST][-d DOMAIN] CONTAINER_GROUP`.

**Voraussetzungen**: Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**:

--min *MIN* (optional): Die minimale Anzahl von Instanzen. Der Standardwert ist **1**. Wenn eine minimale Anzahl von Instanzen festlegt ist, kann der Wert nicht geändert werden.

--max *MAX* (optional): Die maximale Anzahl von Instanzen. Der Standardwert ist **2**. Wenn eine maximale Anzahl von Instanzen festlegt ist, kann der Wert nicht geändert werden.

--desired *DESIRED* (optional): Die Anzahl der von Ihnen benötigten Instanzen. Der Standardwert ist **2**.

**Tipp:** Es kann nur eine der Optionen `--min MIN`, `--max MAX` oder `--desired DESIRED` gleichzeitig angegeben werden.

--auto (optional): Instanzen mit Fehlern durch Aktivierung der automatischen Wiederherstellung automatisch erneut starten.

*CONTAINER_GROUP* (erforderlich): Die ID oder der Name der Containergruppe.

**Beispiele**:

Das folgende Beispiel zeigt eine Anforderung zum Aktualisieren der Containergruppe `my_group`:
```
bluemix ic group-update --max 5 my_group
```


## bluemix ic group-remove
{: #bluemix_ic_group_remove}

Entfernt eine Containergruppe aus dem privaten {{site.data.keyword.Bluemix_notm}}-Repository der Organisation.

```
bluemix ic group-remove [-f|--force] CONTAINER_GROUP
```

**Voraussetzungen**:  Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**:

-f|--force (optional): Erzwingt das Entfernen eines aktiven oder fehlerhaften Containers.

*CONTAINER_GROUP* (erforderlich): Die ID oder der Name der Containergruppe.

**Beispiele**:

Das folgende Beispiel ist eine Anforderung zum Entfernen einer Containergruppe, wobei `my_group` der Name der Containergruppe ist.
```
bluemix ic group-remove my_group
```


## bluemix ic images
{: #bluemix_ic_images}

Zeigt eine Liste aller verfügbaren Images im privaten {{site.data.keyword.Bluemix_notm}}-Repository der Organisation an. Weitere Informationen finden Sie unter dem Befehl [images](https://docs.docker.com/reference/commandline/images){: new_window} in der Docker-Hilfe. Die Liste umfasst die Image-ID, das Erstellungsdatum und den Imagenamen.

```
bluemix ic images [-a|--all][--no-trunc] [-q|--quiet]
```

**Voraussetzungen**: Endpunkt, Anmeldung, Ziel, Docker

**Befehlsoptionen**:

-a|--all (optional): Alle Image-Layer für jede Image im Repository Ihrer Organisation einschließen, nicht nur der neueste Layer.

--no-trunc (optional): Ausgabe nicht abschneiden.

-q|--quiet (optional): Nur die numerischen IDs anzeigen.

**Beispiele**:

Das folgende Beispiel zeigt eine Anforderung zum Empfangen einer Liste der verfügbaren Images für die Organisation:
```
bluemix ic images
```


## bluemix ic inspect
{: #bluemix_ic_inspect}

Zeigt die Informationen zu einem Container an. Weitere Informationen finden Sie unter dem Befehl [inspect](https://docs.docker.com/reference/commandline/inspect){: new_window} in der Docker-Hilfe.

```
bluemix ic inspect [IMAGE|images|CONTAINER]
```

**Voraussetzungen**: Endpunkt, Anmeldung, Ziel, Docker

**Befehlsoptionen**:

*IMAGE* (erforderlich): Detaillierte Informationen zu einem bestimmten Image durch Angabe des Namens oder der ID des Image anzeigen.

images  (erforderlich): Detaillierte Informationen zu allen Images in Ihrem Repository anzeigen.

*CONTAINER* (erforderlich): Detaillierte Informationen zu einem bestimmten Container durch Angabe des Namens oder der ID des Containers anzeigen.

**Tipp:** Nur eine der Optionen *IMAGE*, images oder *CONTAINER* kann gleichzeitig angegeben werden. 

**Beispiele**:

Das folgende Beispiel zeigt eine Anforderung zum Überprüfen eines Containers mit dem Namen `proxy`: 
```
bluemix ic inspect proxy
```


## bluemix ic info
{: #bluemix_ic_info}

Zeigt eine Gruppe von Informationen an, die den Status der Instanz des Container-Cloud-Service beschreiben. Die Informationen umfassen die Containerbegrenzung, die Containernutzung, die aktiven Container, die Speicherbegrenzung, Speicherbelegung, die variabel verknüpfte IP-Begrenzung, die variabel verknüpfte IP-Nutzung, die CCS-Host-URL, die Registry-Host-URL und den Status des Debugmodus.

```
bluemix ic info
```

**Voraussetzungen**: Endpunkt, Anmeldung, Ziel


## bluemix ic ips
{: #bluemix_ic_ips}

Listet die verfügbaren, variabel verknüpften IP-Adressen für den angemeldeten Benutzer auf. Die Liste umfasst IP-Adressen und die Container-ID, mit der die IP-Adressen verbunden sind. Wenn die IP-Adresse nicht im Gebrauch ist, wird keine Container-ID angezeigt.

```
bluemix ic ips [-a|--all]
```

**Voraussetzungen**:  Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**:

-a|--all (optional): Alle IP-Adressen auflisten. Standardmäßig werden nur verfügbare IP-Adressen zurückgegeben.

**Beispiele**:

Das folgende Beispiel zeigt eine Anforderung zum Empfangen einer Liste aller IP-Adressen für die Organisation, unabhängig davon, ob sie verfügbar sind.
```
bluemix ic ips -a
```


## bluemix ic ip-request
{: #ip_request}
Fordert eine neue variabel verknüpfte IP-Adresse an.

```
bluemix ic ip-request
```

**Voraussetzungen**: Endpunkt, Anmeldung, Ziel


## bluemix ic ip-release
{: #bluemix_ic_ip_release}

Gibt eine variabel verknüpfte IP-Adresse von der Instanz des Container-Cloud-Service frei.

```
bluemix ic ip-release IP_ADDRESS
```

**Voraussetzungen**: Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**:

*IP_ADDRESS* (erforderlich): Die freizugebende IP-Adresse.


## bluemix ic ip-bind
{: #bluemix_ic_ip_bind}

Bindet eine verfügbare, variabel verknüpfte IP-Adresse an einen Container.

```
bluemix ic ip-bind IP_ADDRESS CONTAINER
```

**Voraussetzungen**: Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**:

*IP_ADDRESS* (erforderlich): Die zu bindende IP-Adresse.

*CONTAINER* (erforderlich): Die ID oder der Name des zu bindenden Containers.

**Beispiele**:

Das folgende Beispiel zeigt eine Anforderung zum Binden der IP-Adresse `192.123.12.12` an den Container `proxy`:
```
bluemix ic ip-bind 192.123.12.12 proxy
```


## bluemix ic ip-unbind
{: #bluemix_ic_ip_unbind}

Hebt die Bindung einer variabel verknüpften IP-Adresse an ihren Container auf.

Öffentliche IP-Adressen sind eine begrenzte Ressource in IBM Containers. Daher werden öffentliche IP-Adressen, die einem Bereich zugeorndet und nicht an einen Container gebunden sind, in regelmäßigen, d. h. ungefähr wöchentlichen, Intervallen von freien Testbenutzern zurückgefordert. Nicht gebundene öffentliche IP-Adressen werden nie von Kunden mit nutzungsabhängiger Zahlung oder von Abonnementbenutzern zurückgefordert.

```
bluemix ic ip-unbind IP_ADDRESS CONTAINER
```

**Voraussetzungen**: Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**:

*IP_ADDRESS* (erforderlich): Die IP-Adresse, deren Bindung aufzuheben ist.

*CONTAINER* (erforderlich): Die ID oder der Name des Containers, dessen Bindung aufzuheben ist.

**Beispiele**:

Das folgende Beispiel zeigt eine Anforderung zum Aufheben der Bindung der IP-Adresse `192.123.12.12` an den Container `proxy`:
```
bluemix ic ip-unbind 192.123.12.12 proxy
```


## bluemix ic kill
{: #bluemix_ic_kill}

Stoppt einen aktiven Prozess in einem Container, ohne den Container zu stoppen. Weitere Informationen finden Sie unter dem Befehl [kill](https://docs.docker.com/reference/commandline/kill/){: new_window} in der Docker-Hilfe.

```
bluemix ic kill [-s CMD|--signal CMD] CONTAINER
```

**Voraussetzungen**: Endpunkt, Anmeldung, Ziel, Docker

**Befehlsoptionen**:

-s *CMD*|--signal *CMD* (optional): Befehl an den Prozess senden, der im Container ausgeführt wird.

*CONTAINER* (erforderlich): Die ID oder der Name des Containers.

**Beispiele**:

Das folgende Beispiel zeigt eine Anforderung zum Beenden des Prozesses in einem Container mit dem Namen `proxy`:
```
bluemix ic kill proxy
```


## bluemix ic namespace-get
{: #bluemix_ic_namespace_get}

Zeigt den Namen des privaten {{site.data.keyword.Bluemix_notm}}-Image-Repositorys für die Organisation an, bei der Sie angemeldet sind.

```
bluemix ic namespace-get
```

**Voraussetzungen**: Endpunkt, Anmeldung, Ziel


## bluemix ic namespace-set
{: #bluemix_ic_namespace_set}

Legt den Namen des privaten {{site.data.keyword.Bluemix_notm}}-Image-Repositorys für die Organisation fest, bei der Sie angemeldet sind.

*Einschränkung:* Im Namen des Namensbereichs Ihres Repositorys kann kein Bindestrich (`-`) verwendet werden.

```
bluemix ic namespace-set NAME
```

**Voraussetzungen**: Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**:

*NAME* (erforderlich): Eine nur einmal ausführbare Funktkion zum Festlegen des Repository-Namensbereichs für Ihre Organisation, sofern dieser nicht bereits festgelegt ist. Reinitialisieren Sie IBM Containers nach dem Festlegen des Namensbereichs mit dem Befehl `bluemix ic init`, bevor Sie fortfahren.


## bluemix ic pause
{: #pause}

Hält alle Prozesse innerhalb eines aktiven Containers an. Weitere Informationen finden Sie unter dem Befehl [pause](https://docs.docker.com/reference/commandline/pause/){: new_window} in der Docker-Hilfe. Informationen zum Aufheben des Anhaltens eines Containers finden Sie unter dem Befehl [bluemix ic unpause](#unpause).

```
bluemix ic pause CONTAINER
```

**Voraussetzungen**: Endpunkt, Anmeldung, Ziel, Docker

**Befehlsoptionen**:

*CONTAINER* (erforderlich): Der Name oder die ID des Containers.

**Antworten:**

- Paused container successfully (Container erfolgreich angehalten)

- Command failed with container cloud service (Befehl für Container-Cloud-Service fehlgeschlagen)

 `{message}`
  
 Dabei ist `{message}` der zugehörige Fehler.
 
- Command failed - Could not connect to container cloud service (Befehl fehlgeschlagen - Verbindung zu Container-Cloud-Service konnte nicht hergestellt werden)

**Beispiele**:

Das folgende Beispiel zeigt eine Anforderung zum Anhalten eines Containers mit dem Namen `proxy`:
```
bluemix ic pause proxy
```


## bluemix ic unpause
{: #unpause}

Hebt das Anhalten aller Prozesse innerhalb eines aktiven Containers auf. Weitere Informationen finden Sie unter dem Befehl [unpause](https://docs.docker.com/reference/commandline/unpause/){: new_window} in der Docker-Hilfe. Informationen zum Anhalten eines Containers finden Sie unter dem Befehl [bluemix ic pause](#pause).

```
bluemix ic unpause CONTAINER
```

**Voraussetzungen**: Endpunkt, Anmeldung, Ziel, Docker

**Befehlsoptionen**:

*CONTAINER* (erforderlich): Der Name oder die ID des Containers.

**Antworten:**

- Unpaused container successfully (Anhalten des Containers erfolgreich aufgehoben)

- Command failed with container cloud service (Befehl für Container-Cloud-Service fehlgeschlagen) 

 `{message}` 
 
 Dabei ist `{message}` der zugehörige Fehler.
 
- Command failed - Could not connect to container cloud service (Befehl fehlgeschlagen - Verbindung zu Container-Cloud-Service konnte nicht hergestellt werden)

**Beispiele**:

Das folgende Beispiel zeigt eine Anforderung zum Aufheben des Anhaltens eines Containers mit dem Namen `proxy`:
```
bluemix ic unpause proxy
```


## bluemix ic port
{: #bluemix_ic_port}

Listet Portzuordnungen oder eine bestimmte Zuordnung für den Container auf. Dieser Befehl schließt den Befehl `docker port` ein. Weitere Informationen finden Sie unter dem Befehl [port](https://docs.docker.com/reference/commandline/port/){: new_window} in der Docker-Hilfe.


## bluemix ic ps
{: #bluemix_ic_ps}
Zeigt eine Liste der Container an, die im Namensbereich des angemeldeten Benutzers aktiv sind. Standardmäßig zeigt dieser Befehl nur Container an, die aktiv sind. Weitere Informationen finden Sie unter dem Befehl [ps](https://docs.docker.com/reference/commandline/ps/){: new_window} in der Docker-Hilfe.

```
bluemix ic ps [-a|--all][-s|--size] [-l NUM|--limit NUM][-q|--quiet]
```

**Voraussetzungen**: Endpunkt, Anmeldung, Ziel, Docker

**Befehlsoptionen**:

-a|--all (optional): Alle Container anzeigen, d. h. aktive und gestoppte Container.

-s|--size (optional): Die Größen der Container auflisten.

-l *NUM*|--limit *NUM* (optional): Die kürzlich erstellten Container auflisten, wobei *NUM* die Anzahl der kürzlich erstellten Container ist, die zurückgegeben werden sollen.

Beispiel: Wenn Sie nacheinander die Container `node1` bis `node5` erstellt haben, gibt der Befehl `bluemix ic ps --limit 2` die Container `node4` und `node5` zurück, da diese die beiden zuletzt erstellten Container sind.

-q|--quiet (optional): Nur Container-IDs anzeigen.

**Beispiele**:

Das folgende Beispiel zeigt eine Anforderung zum Anzeigen aller aktiven und gestoppten Container:
```
bluemix ic ps -a
```


## bluemix ic restart
{: #bluemix_ic_restart}

Startet einen Container erneut. Weitere Informationen finden Sie unter dem Befehl [restart](https://docs.docker.com/reference/commandline/restart/){: new_window} in der Docker-Hilfe.

```
bluemix ic restart CONTAINER [-t SECS|--time SECS]
```

**Voraussetzungen**: Endpunkt, Anmeldung, Ziel, Docker

**Befehlsoptionen**:

*CONTAINER* (erforderlich): Der Name oder die ID des Containers.

-t *SECS*|--time *SECS* (optional): Die Anzahl Sekunden, die vor dem Neustart des Containers abgewartet werden soll.

**Antworten:**

- Restarted container successfully (Container erfolgreich erneut gestartet)

- Command failed with container cloud service (Befehl für Container-Cloud-Service fehlgeschlagen) 

 `{message}` 
 
 Dabei ist `{message}` der zugehörige Fehler.
 
- Command failed - Could not connect to container cloud service (Befehl fehlgeschlagen - Verbindung zu Container-Cloud-Service konnte nicht hergestellt werden)

**Beispiele**:

Das folgende Beispiel zeigt eine Anforderung zum erneuten Starten eines Containers mit dem Namen `proxy`:
```
bluemix ic restart proxy
```


## bluemix ic rm
{: #bluemix_ic_rm}

Entfernt einen Container. Weitere Informationen finden Sie unter dem Befehl [rm](https://docs.docker.com/reference/commandline/rm/){: new_window} in der Docker-Hilfe.

```
bluemix ic rm [-f|--force] CONTAINER
```

**Voraussetzungen**: Endpunkt, Anmeldung, Ziel, Docker

**Befehlsoptionen**:

-f|--force (optional): Erzwingt das Entfernen eines aktiven oder fehlerhaften Containers.

*CONTAINER* (erforderlich): Der Name oder die ID des Containers.

**Antworten:**

- Removed container successfully (Container erfolgreich entfernt)

- Command failed with container cloud service (Befehl für Container-Cloud-Service fehlgeschlagen) 

 `{message}` 
 
 Dabei ist `{message}` der zugehörige Fehler.
 
- Command failed - Could not connect to container cloud service (Befehl fehlgeschlagen - Verbindung zu Container-Cloud-Service konnte nicht hergestellt werden)

**Beispiele**:

Das folgende Beispiel zeigt eine Anforderung zum Entfernen eines Containers mit dem Namen `proxy`:
```
bluemix ic rm proxy
```


## bluemix ic rmi
{: #bluemix_ic_rmi}

Entfernt ein Image aus dem Namensbereich des angemeldeten Benutzers. Weitere Informationen finden Sie unter dem Befehl [rmi](https://docs.docker.com/reference/commandline/rmi/){: new_window} in der Docker-Hilfe.

```
bluemix ic rmi [-R REGISTRY|--registry REGISTRY] IMAGE
```

**Voraussetzungen**: Endpunkt, Anmeldung, Ziel, Docker

**Befehlsoptionen**:

-R *REGISTRY*|--registry *REGISTRY* (optional): Den Registry-Host ändern. Standardmäßig wird die Registry verwendet, die im Befehl `bluemix ic init` angegeben wird.

*IMAGE* (erforderlich): Der Name des Image, das entfernt werden soll. Wenn der Imagename nicht mit Tags versehen wird, wird standardmäßig das Image mit dem Tag `latest` entfernt.

**Antworten:**

- Removed: `{IMAGE}` (Entfernt: IMAGE)

 Dabei ist `{IMAGE}` der Name des entfernten Image.
 
- Error! No registry host specified. (Fehler! Es wurde kein Registry-Host angegeben.)

- Image remove failed - Could not connect to container cloud registry (Entfernen des Image fehlgeschlagen - Verbindung zu Container-Cloud-Registry konnte nicht hergestellt werden)

- Command failed with container cloud service (Befehl für Container-Cloud-Service fehlgeschlagen) 

 `{message}`
 
 Dabei ist `{message}` der zugehörige Fehler.

**Beispiele**:

Das folgende Beispiel zeigt eine Anforderung zum Entfernen des Image `mynamespace/myimage:latest`:
```
bluemix ic rmi registry.ng.bluemix.net/mynamespace/myimage:latest
```


## bluemix ic run
{: #bluemix_ic_run}

Startet einen neuen Container im Container-Cloud-Service über einen Imagenamen. Weitere Informationen finden Sie unter dem Befehl [run](https://docs.docker.com/reference/commandline/run/){: new_window} in der Docker-Hilfe.



```
bluemix ic run [-p PORT|--publish PORT][-P] [-m MEMORY|--memory MEMORY][-e ENV|--env ENV] [-v VOLUME:CONTAINER_PATH] -n NAME|--name NAME [--link NAME:ALIAS][-it] IMAGE [CMD [CMD ...]]
```
**Hinweis:** Stellen Sie sicher, dass das Cloud Foundry-Befehlstool installiert ist und dass Sie über ein Cloud Foundry-Token verfügen. Durch eine erfolgreiche Anmeldung mit den Befehlen `bluemix login` und `bluemix ic init` werden das erforderliche Token und die erforderlichen Zertifikate generiert. 


**Voraussetzungen**: Endpunkt, Anmeldung, Ziel, Docker

**Befehlsoptionen**:

-p *PORT*|--publish *PORT* (optional): Macht den Port für den HTTP-Datenverkehr verfügbar. Schließen Sie die Ports ein, die in der Dockerfile für das Image, das Sie verwenden, angegeben sind. Sie können mehrere Ports mit mehreren Optionen `-p` einschließen. Durch das Verfügbarmachen eines Ports wird automatisch eine öffentliche IP-Adresse an den Container gebunden, wenn eine öffentliche IP-Adresse verfügbar ist.

Wenn Sie eine bestehende IP-Adresse im Bereich haben, die Sie an den Container binden wollen, können Sie die IP-Adresse angeben, anstatt Sie später zu binden. Die IP-Adresse muss im folgenden Format angegeben werden: *&lt;ip-adresse&gt;:&lt;container-port&gt;:&lt;container-port&gt;*

Weitere Informationen zum Anfordern von IP-Adressen für einen Bereich finden Sie unter dem Befehl [bluemix ic ip-request](#ip_request).

Wenn Sie einen Port angeben, machen Sie die App für {{site.data.keyword.Bluemix_notm}} Load Balancer oder Container in demselben {{site.data.keyword.Bluemix_notm}}-Bereich verfügbar. Anschließend können Bluemix Load Balancer oder die Container den Port verwenden, um den Host zu erreichen. Wenn ein Port in der Dockerfile für das Image, das Sie verwenden, angegeben ist, schließen Sie diesen Port ein.

**Tipp:**

- Für das von IBM zertifizierte Liberty Server-Image oder für eine modifizierte Version dieses Image geben Sie Port 9080 ein.
- Für das von IBM zertifizierte Node.js-Image oder für eine modifizierte Version dieses Image geben Sie Port 8000 ein.

-P (optional): Die in der Dockerfile für das Image angegebenen Ports automatisch für den HTTP-Datenverkehr verfügbar machen.

-m *MEMORY*|--memory *MEMORY* (optional): Der Gruppe eine Speicherbegrenzung in MB zuweisen. Wenn Sie eine Containergruppe über die CLI erstellen, ist der Standardwert für jede Containerinstanz `64` MB.  Wenn Sie eine Containergruppe über das {{site.data.keyword.Bluemix_notm}}-Dashboard erstellen, ist der Standardwert für jede `256` MB. Gültige Werte: `64`, `256`, `512`, `1024` und `2048`. Nach der Zuweisung einer Speicherbegrenzung kann der Wert nicht mehr geändert werden.

-e *ENV*|--env *ENV* (optional): Die Umgebungsvariable festlegen, wobei **ENV** ein `schlüssel=wert`-Paar ist. Geben Sie mehrere Schlüssel separat an. Wenn Sie Anführungszeichen angeben, geben Sie sie so an, dass der Name und der Wert der Umgebungsvariablen eingeschlossen werden. Beispiel: `-e "schlüssel1=wert1" -e "schlüssel2=wert2" -e "schlüssel3=wert3"`. In der folgenden Tabelle sind einige häufig verwendete Umgebungsvariablen aufgeführt, die Sie angeben können:

|      Umgebungsvariable                          |   Beschreibung                              |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;app-name&gt;*       | Bindet einen Service an einen Container. Mit der Umgebungsvariablen `CCS_BIND_APP` können Sie eine App an den Container binden. Die App wird an den Zielservice gebunden und fungiert als Bridge, über die {{site.data.keyword.Bluemix_notm}} die Informationen aus der Umgebungsvariablen `VCAP_SERVICES` Ihrer Bridge-App in die aktive Containerinstanz übertragen kann. Weitere Informationen zur Erstellung einer Bridge-App finden Sie unter [Service an einen Container binden](http://www.ng.bluemix.net/docs/containers/container_creating_ov.html#container_binding_ov){: new_window}. |
| CCS_SSH_KEY=*&lt;öffentlicher_ssh-schlüssel&gt;* | Fügt einem Container einen SSH-Schlüssel hinzu, wenn Sie den Container erstellen. Sie können den SSH-Schlüssel mithilfe der Umgebungsvariablen hinzufügen, wenn Sie einen Container über das {{site.data.keyword.Bluemix_notm}}-Dashboard oder über die CLI erstellen. Weitere Informationen zu SSH-Schlüsseln finden Sie unter [Bei einem Container anmelden](http://www.ng.bluemix.net/docs/containers/container_creating_ov.html#container_cli_login_ssh){: new_window}. |
| LOG_LOCATIONS=*&lt;dateipfad&gt;* | Fügt eine Protokolldatei für die Überwachung im Container hinzu. Fügen Sie die Umgebungsvariable `LOG_LOCATIONS` mit einem Pfad zu der Protokolldatei ein. |
*Tabelle 2. Häufig verwendete Umgebungsvariablen*

-v VOLUME:CONTAINER_PATH[:ro]|--volume VOLUME:CONTAINER_PATH[:ro](optional):  Datenträger einem Container durch Angabe der Details im folgenden Format zuordnen: `VolumeId:ContainerPath[:ro]`.

- *VOLUME*: Die ID oder der Name des Datenträgers.
- *CONTAINER_PATH*: Der absolute Pfad zu dem Datenträger in dem Container.
- ro: Optional. Die Angabe `ro` aktiviert den Schreibschutz des Datenträgers anstelle des standardmäßigen Lese-/Schreibzugriffs.

-n *NAME*|--name *NAME* (erforderlich): Dem Container einen Namen zuweisen.

*Tipp:* Der Containername muss mit einem Buchstaben beginnen. Der Name kann Großbuchstaben, Kleinbuchstaben, Ziffern, Punkte (`.`), Unterstreichungszeichen (`_`) oder Bindestriche (`-`) enthalten.

--link *NAME*:*ALIAS* (optional): Wenn ein Container mit einem anderen Container, der aktiv ist, kommunizieren soll, können Sie ihn durch einen Alias für den Hostnamen adressieren.

-it (optional): Container im interaktiven Modus ausführen. Nach dem Erstellen des Containers die Anzeige der Standardeingabe beibehalten. Geben Sie `exit` zum Beenden ein.

*IMAGE* (erforderlich): Das Image, das in den Container eingeschlossen werden soll. Sie können Befehle nach dem Image auflisten, fügen Sie jedoch keine Optionen nach dem Image ein. Fügen Sie alle Optionen vor der Angabe eines Image ein.

Wenn Sie ein Image im privaten {{site.data.keyword.Bluemix_notm}}-Repository Ihrer Organisation verwenden, geben Sie das Image im folgenden Format an: *registry.ng.bluemix.net/NAMENSBEREICH/IMAGE*.

Wenn Sie ein Image verwenden, das durch IBM Containers bereitgestellt wird, geben Sie das Image im folgenden Format an: *registry.ng.bluemix.net/IMAGE*.

*CMD* (optional): Der Befehl und die Argumente, die an den Container zur Ausführung übergeben werden. Dieser Befehl muss ein Befehl mit langer Laufzeit sein. Verwenden Sie keinen Befehl mit kurzer Laufzeit, beispielsweise `/bin/date`, da ein Befehl mit kurzer Laufzeit dazu führen kann, dass der Container abstürzt.



**Beispiele**:

Den Befehl `sh -c "while true; do date; sleep 20; done"` mit langer Laufzeit für den Container `my_container` ausführen, der auf dem Image `registry.ng.bluemix.net/ibmnode` erstellt wurde. 
```
bluemix ic run --name my_container registry.ng.bluemix.net/ibmnode -- sh -c "while true; do date; sleep 20; done"
```


Container `proxy` unter Verwendung des Image `my_namespace/nginx` erstellen und anschließend mit einer Speicherbegrenzung von `1024` MB starten, wobei `my_namespace` der Namensbereich ist, der den angemeldeten Benutzern zugeordnet ist.
```
bluemix ic run -n proxy -m 1024 registry.ng.bluemix.net/my_namespace/nginx
```

Container mit dem Image `my_namespace/blog` erstellen und starten und die Berechtigungsnachweise als Umgebungsvariablen übergeben. `my_namespace` ist der Namensbereich, der den angemeldeten Benutzern zugeordnet ist.
```
bluemix ic run -n my_container -e USER=johnsmith -e PASS=password registry.ng.bluemix.net/my_namespace/blog
```

Datenträger einem Container unter Verwendung des Image `my_namespace/blog` hinzufügen, wobei `my_namespace` der Namensbereich ist, der den angemeldeten Benutzern zugeordnet ist.
```
bluemix ic run -n my_container -v VolId1:/first/path -v VolId2:/second/path registry.ng.bluemix.net/my_namespace/blog
```


## bluemix ic route-map
{: #bluemix_ic_route_map}

Legt die Route für den Internetdatenverkehr fest, die für den Zugriff auf die Containergruppe verwendet werden soll. Mit diesem Befehl können Sie eine neue Route festlegen oder eine vorhandene Route aktualisieren.

```
bluemix ic route-map [-n HOST|--hostname HOST][-d DOMAIN|--domain DOMAIN] CONTAINER_GROUP
```

**Voraussetzungen**:  Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**:

-n *HOST*|--hostname *HOST* (optional): Der Hostname für die Route. Der Hostname ist der erste Teil der vollständigen öffentlichen Routen-URL, wie z. B. `mycontainerhost` in der URL `mycontainerhost.mybluemix.net`.

-d *DOMAIN*|--domain *DOMAIN* (optional): Der Domänenname für die Route, der den zweiten Teil der vollständigen öffentlichen Routen-URL darstellt. In den meisten Fällen ist die Domäne `mybluemix.net`. Sie können mit diesem Parameter auch eine private Domäne angeben.

*CONTAINER_GROUP* (erforderlich): Die ID oder der Name der Containergruppe.

**Beispiele**:

Das folgende Beispiel zeigt eine Anforderung zum Zuordnen der Route für die Gruppe mit dem Namen `GROUP1`. Dabei ist `my_host` der Hostname und `organization.com` die Domäne.
```
bluemix ic route-map -n my_host -d organization.com GROUP1
```


## bluemix ic route-unmap
{: #bluemix_ic_route_unmap}

Legt die Route für den Internetdatenverkehr fest, die für den Zugriff auf die Containergruppe verwendet werden soll. Mit diesem Befehl können Sie eine neue Route festlegen oder eine vorhandene Route aktualisieren.

```
bluemix ic route-unmap [-n HOST|--hostname HOST][-d DOMAIN|--domain DOMAIN] CONTAINER_GROUP
```

**Voraussetzungen**:  Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**:

-n *HOST*|--hostname *HOST* (optional): Der Hostname für die Route.

-d *DOMAIN*|--domain *DOMAIN* (optional): Der Domänenname für die Route.

*CONTAINER_GROUP* (erforderlich): Die ID oder der Name der Containergruppe.

**Beispiele**:

Das folgende Beispiel zeigt eine Anforderung zum Aufheben der Zuordnung der Route für die Gruppe mit dem Namen `GROUP1`. Dabei ist `my_host` der Hostname und `organization.com` die Domäne.
```
bluemix ic route-unmap -n my_host -d organization.com GROUP1
```


## bluemix ic start
{: #ic_start}
Startet einen gestoppten Container. Weitere Informationen finden Sie unter dem Befehl [start](https://docs.docker.com/reference/commandline/start/){: new_window} in der Docker-Hilfe. Informationen zum Stoppen eines Containers finden Sie unter dem Befehl [bluemix ic stop](#ic_stop).

```
bluemix ic start CONTAINER
```

**Voraussetzungen**: Endpunkt, Anmeldung, Ziel, Docker

**Befehlsoptionen**:

*CONTAINER* (erforderlich): Der Name oder die ID des Containers.

**Antworten:**

- Started container successfully (Container erfolgreich gestartet)

- Command failed with container cloud service (Befehl für Container-Cloud-Service fehlgeschlagen)

 `{message}`
  
 Dabei ist `{message}` der zugehörige Fehler.
 
- Command failed - Could not connect to container cloud service (Befehl fehlgeschlagen - Verbindung zu Container-Cloud-Service konnte nicht hergestellt werden)

**Beispiele**:

Das folgende Beispiel zeigt eine Anforderung zum Starten eines Containers mit dem Namen `proxy`.
```
bluemix ic start proxy
```


## bluemix ic stop  
{: #ic_stop}
Stoppt einen aktiven Container. Weitere Informationen finden Sie unter dem Befehl [stop](https://docs.docker.com/reference/commandline/stop/){: new_window} in der Docker-Hilfe. Informationen zum Starten eines Containers finden Sie unter dem Befehl [bluemix ic start](#ic_start).

```
bluemix ic stop CONTAINER [-t SECS|--time SECS]
```

**Voraussetzungen**: Endpunkt, Anmeldung, Ziel, Docker

**Befehlsoptionen**:

*CONTAINER* (erforderlich): Der Name oder die ID des Containers.

-t *SECS*|--time *SECS* (optional): Die Anzahl Sekunden, die vor dem Stoppen des Containers abgewartet werden soll.

**Antworten:**

- Stopped container successfully (Container erfolgreich gestoppt)

- Command failed with container cloud service (Befehl für Container-Cloud-Service fehlgeschlagen)

 `{message}`
  
 Dabei ist `{message}` der zugehörige Fehler.
 
- Command failed - Could not connect to container cloud service (Befehl fehlgeschlagen - Verbindung zu Container-Cloud-Service konnte nicht hergestellt werden)

**Beispiele**:

Das folgende Beispiel zeigt eine Anforderung zum Stoppen eines Containers mit dem Namen `proxy`.
```
bluemix ic stop proxy
```


## bluemix ic stats
{: #bluemix_ic_stats}

Zeigt Live-Nutzungsstatistiken für einen oder mehrere Container an. Verwenden Sie die Tastenkombination `STRG+C` zum Beenden. Weitere Informationen finden Sie unter dem Befehl [stats](https://docs.docker.com/reference/commandline/stats/){: new_window} in der Docker-Hilfe.

```
bluemix ic stats [--no-stream] CONTAINER [CONTAINER]
```

**Voraussetzungen**: Endpunkt, Anmeldung, Ziel, Docker

**Befehlsoptionen**:

*CONTAINER* (erforderlich): Der Name oder die ID des Containers.

--no-stream  (optional): Nur das letzte Ergebnis anzeigen und keine vorherigen Informationen einschließen.

**Beispiele**:

Das folgende Beispiel zeigt eine Anforderung zum Anzeigen der jüngsten Statistiken zu einem Container:
```
bluemix ic stats --no-stream my_container
```


## bluemix ic top
{: #bluemix_ic_top}

Zeigt die Prozesse an, die im Container ausgeführt werden. Weitere Informationen finden Sie unter dem Befehl [top](https://docs.docker.com/reference/commandline/top/){: new_window} in der Docker-Hilfe.

```
bluemix ic top CONTAINER [CONTAINER]
```

**Voraussetzungen**: Endpunkt, Anmeldung, Ziel, Docker

**Befehlsoptionen**:

*CONTAINER* (erforderlich): Der Name oder die ID des Containers.

**Beispiele**:

Das folgende Beispiel zeigt eine Anforderung zum Anzeigen der Prozesse in einem Container mit dem Namen `my_container`.
```
bluemix ic top my_container
```


## bluemix ic volumes
{: #bluemix_ic_volumes}

Listet Datenträger auf.

```
bluemix ic volumes
```

**Voraussetzungen**: Endpunkt, Anmeldung, Ziel


## bluemix ic volume-inspect
{: #bluemix_ic_volume_inspect}

Überprüft einen Datenträger.

```
bluemix ic volume-inspect VOLUME_NAME
```

**Voraussetzungen**: Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**:

*VOLUME_NAME* (erforderlich): Der Name des Datenträgers.

**Beispiele**:

Das folgende Beispiel zeigt eine Anforderung zum Überprüfen des Datenträgers. Dabei ist `volume_name` der Name des Datenträgers.
```
bluemix ic volume-inspect volume_name
```


## bluemix ic volume-create
{: #bluemix_ic_volume_create}

Erstellt einen Datenträger.

```
bluemix ic volume-create VOLUME_NAME
```

**Voraussetzungen**: Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**:

*VOLUME_NAME* (erforderlich): Der Name des Datenträgers. Der Name kann Kleinbuchstaben, Ziffern, Unterstreichungszeichen (`_`) und Bindestriche (`-`) enthalten.

**Beispiele**:

Das folgende Beispiel zeigt eine Anforderung zum Erstellen eines Datenträgers.
```
bluemix ic volume-create volume_name 
```


## bluemix ic volume-remove
{: #bluemix_ic_volume_remove}

Entfernt einen Datenträger.

```
bluemix ic volume-remove VOLUME_NAME
```

**Voraussetzungen**: Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**:

*VOLUME_NAME* (erforderlich): Der Name des Datenträgers.

**Beispiele**:

Das folgende Beispiel zeigt eine Anforderung zum Entfernen eines Datenträgers. Dabei ist `volume_name` der Name des Datenträgers.
```
bluemix ic volume-remove volume_name
```

## bluemix ic volume-fs
{: #bluemix_ic_volume_fs}

Dateisysteme auflisten

```
bluemix ic volume-fs
```

## bluemix ic volume-fs-create
{: #bluemix_ic_volume_fs_create}

Ein neues Dateisystem erstellen

```
bluemix ic volume-fs-create FILE_SYSTEM_NAME
```

**Voraussetzungen**: Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**:

*FILE_SYSTEM_NAME* (erforderlich): Der Name des Dateisystems. Der Name kann Kleinbuchstaben, Ziffern, Unterstreichungszeichen (`_`) und Bindestriche (`-`) enthalten.

**Beispiele**:

Das folgende Beispiel zeigt eine Anforderung zum Erstellen eines Dateisystems.
```
bluemix ic volume-fs-create my_file_system
```

## bluemix ic volume-fs-remove
{: #bluemix_ic_volume_fs_remove}

Ein Dateisystem entfernen

```
bluemix ic volume-fs-remove FILE_SYSTEM_NAME
```

**Voraussetzungen**: Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**:

*FILE_SYSTEM_NAME* (erforderlich): Der Name des Dateisystems.

**Beispiele**:

Das folgende Beispiel zeigt eine Anforderung zum Entfernen eines Dateisystems. Dabei ist `my_file_system` der Name des Dateisystems.
```
bluemix ic volume-fs-remove my_file_system
```

## bluemix ic volume-fs-inspect
{: #bluemix_ic_volume_fs_inspect}

Ein Dateisystem überprüfen

```
bluemix ic volume-fs-inspect FILE_SYSTEM_NAME
```

**Voraussetzungen**: Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**:

*FILE_SYSTEM_NAME* (erforderlich): Der Name des Dateisystems.

**Beispiele**:

Das folgende Beispiel zeigt eine Anforderung zum Überprüfen eines Dateisystems. Dabei ist `my_file_system` der Name des Dateisystems (Datenträgers).
```
bluemix ic volume-fs-inspect my_file_system
```
## bluemix ic volume-fs-flavors
{: #bluemix_ic_volume_fs_flavors}

Alle Dateisystemversionen auflisten

```
bluemix ic volume-fs-flavors
```

**Voraussetzungen**: Endpunkt, Anmeldung, Ziel

## bluemix ic wait
{: #bluemix_ic_wait}

Beendet einen Container und zeigt den Beendigungscode als Bestätigung an. Weitere Informationen finden Sie unter dem Befehl [wait](https://docs.docker.com/reference/commandline/wait/){: new_window} in der Docker-Hilfe.

```
bluemix ic wait CONTAINER [CONTAINER]
```

**Voraussetzungen**: Endpunkt, Anmeldung, Ziel, Docker

**Befehlsoptionen**:

*CONTAINER* (erforderlich): Der Name oder die ID des Containers.

**Beispiele**:

Das folgende Beispiel zeigt eine Anforderung zum Beenden eines Containers mit dem Namen `my_container`:
```
bluemix ic wait my_container
```


## bluemix ic version
{: #bluemix_ic_version}

Zeigt die Version von Docker an. 

```
bluemix ic version
```

**Voraussetzungen**: Docker

Zum Anzeigen der Version von IBM Containers führen Sie den Befehl `bluemix ic info` aus. Weitere Informationen finden Sie unter dem Befehl [version](https://docs.docker.com/reference/commandline/version/){: new_window} in der Docker-Hilfe.
