---



copyright:

  years: 2015, 2017
lastupdated: "2017-05-03"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix_notm}}-Befehle (bx)
{: #bluemix_cli}

Version: 0.5.2

Von der {{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle (CLI) werden Befehle bereitgestellt, die nach Namensbereich für Benutzer zur Interaktion mit {{site.data.keyword.Bluemix_notm}} zusammengefasst sind. Bei einigen {{site.data.keyword.Bluemix_notm}}-Befehlen handelt es sich um Wrapper bereits vorhandener cf-Befehle, während andere Befehle die Funktionalität für {{site.data.keyword.Bluemix_notm}}-Benutzer erweitern. In der nachfolgenden Liste werden alle von der {{site.data.keyword.Bluemix_notm}}-CLI unterstützten Befehle mit Namen, Optionen, Nutzungen, Voraussetzungen, Beschreibungen und Beispielen aufgeführt.
{:shortdesc}

**Hinweis:** Unter *Voraussetzungen* wird aufgelistet, welche Aktionen vor der Verwendung des Befehls ausgeführt werden müssen. Für Befehle, für die keine Voraussetzungen erfüllt sein müssen, ist **Keine** angegeben. Andernfalls kann mindestens eine der folgenden Aktionen eine Voraussetzung sein:

<dl>
<dt>Endpunkt</dt>
<dd>Vor dem Verwenden des Befehls muss ein API-Endpunkt durch Absetzen des Befehls <code>bluemix api</code> definiert werden.</dd>
<dt>Anmeldung</dt>
<dd>Vor der Verwendung des Befehls ist die Anmeldung über den Befehl <code>bluemix login</code> erforderlich.
Verwenden Sie beim Anmelden mit einer eingebundenen ID die Option '--sso' für die Anmeldung mit einmaligem Kenncode oder verwenden Sie die Option '--apikey' für die Authentifizierung mit einem API-Schlüssel. Wechseln Sie in der {{site.data.keyword.Bluemix_notm}}-Konsole zum Erstellen von API-Schlüsseln zu **Verwalten** &gt; **Sicherheit** &gt; **Bluemix-API-Schlüssel**.
</dd>
<dt>Ziel</dt>
<dd>Vor dem Verwenden des Befehls muss der Befehl <code>bluemix target</code> zum Definieren einer Organisation und eines Bereichs ausgeführt werden.</dd>
<dt>Docker</dt>
<dd>Die Docker-CLI (docker) muss installiert werden, um diesen Befehl auszuführen.</dd>
</dl>

## Index für Bluemix-Befehle
{: #bx_commands_index}

Verwenden Sie die Indizes in den folgenden Tabellen als Referenz für die häufig verwendeten Bluemix-Befehle.

**Hinweis:** Sie können das Kurzformat für Bluemix-Befehle verwenden. Beispiel: `bx api` ist die Kurzform von `bluemix api`.



<table summary="Allgemeine Bluemix-Befehle">
<caption>Tabelle 1. Allgemeine Bluemix-Befehle</caption>
 <thead>
 <th colspan="5">Allgemeine Bluemix-Befehle</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix help](bx_cli.html#bluemix_help)</td>
 <td>[bluemix api](bx_cli.html#bluemix_api)</td>
 <td>[bluemix login](bx_cli.html#bluemix_login)</td>
 <td>[bluemix logout](bx_cli.html#bluemix_logout)</td>
 <td>[bluemix target](bx_cli.html#bluemix_target)</td>
 </tr>
 <tr>
 <td>[bluemix info](bx_cli.html#bluemix_info) </td>
 <td>[bluemix regions](bx_cli.html#bluemix_regions) </td>
 <td>[bluemix config](bx_cli.html#bluemix_config)</td>
 <td>[bluemix curl](bx_cli.html#bluemix_curl)</td>
 <td>[bluemix update](bx_cli.html#bluemix_update)</td>
 </tr>
 </tbody>
 </table>

<table summary="Bluemix-Befehle zur Verwaltung von Konten, Organisationen, Bereichen, Rollen und API-Schlüsseln.">
<caption>Tabelle 2. Befehle zur Verwaltung von Konten, Organisationen, Bereichen, Rollen und API-Schlüsseln</caption>
 <thead>
 <th colspan="5">Befehle zur Verwaltung von Konten, Organisationen, Bereichen, Rollen und API-Schlüsseln</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix iam orgs](bx_cli.html#bluemix_iam_orgs)</td>
 <td>[bluemix iam org](bx_cli.html#bluemix_iam_org)</td>
 <td>[bluemix iam org-create](bx_cli.html#bluemix_iam_org_create)</td>
 <td>[bluemix iam org-replicate](bx_cli.html#bluemix_iam_org_replicate)</td>
 <td>[bluemix iam org-rename](bx_cli.html#bluemix_iam_org_rename)</td>
 </tr>
 <tr>
 <td>[bluemix iam org-delete](bx_cli.html#bluemix_iam_org_delete)</td>
 <td>[bluemix iam spaces](bx_cli.html#bluemix_iam_spaces)</td>
 <td>[bluemix iam space](bx_cli.html#bluemix_iam_space)</td>
 <td>[bluemix iam space-create](bx_cli.html#bluemix_iam_space_create)</td>
 <td>[bluemix iam space-rename](bx_cli.html#bluemix_iam_space_rename)</td>
 </tr>
 <tr>
 <td>[bluemix iam space-delete](bx_cli.html#bluemix_iam_space_delete)</td>
 <td>[bluemix iam org-users](bx_cli.html#bluemix_iam_org_users)</td>
 <td>[bluemix iam org-user-add](bx_cli.html#bluemix_iam_org_user_add)</td>
 <td>[bluemix iam org-user-remove](bx_cli.html#bluemix_iam_org_user_remove)</td>
 <td>[bluemix iam org-roles](bx_cli.html#bluemix_iam_org_roles)</td>
 </tr>
 <tr>
 <td>[bluemix iam org-role-set](bx_cli.html#bluemix_iam_org_role_set)</td>
 <td>[bluemix iam org-role-unset](bx_cli.html#bluemix_iam_org_role_unset)</td>
 <td>[bluemix iam space-users](bx_cli.html#bluemix_iam_space_users)</td>
 <td>[bluemix iam space-roles](bx_cli.html#bluemix_iam_space_roles)</td>
 <td>[bluemix iam space-role-set](bx_cli.html#bluemix_iam_space_role_set)</td>
</tr>
 <tr>
 <td>[bluemix iam space-role-unset](bx_cli.html#bluemix_iam_space_role_unset)</td>
 <td>[bluemix iam accounts](bx_cli.html#bluemix_iam_accounts)</td>
 <td>[bluemix iam org-account](bx_cli.html#bluemix_iam_org_account)</td>
 <td>[bluemix iam account-users](bx_cli.html#bluemix_iam_account_users)</td>
 <td>[bluemix iam account-users-delete](bx_cli.html#bluemix_iam_account_users_delete)</td>
 </tr>
 <tr>
  <td>[bluemix iam account-user-invite](bx_cli.html#bluemix_iam_account_user_invite)</td>
  <td>[bluemix iam account-user-reinvite](bx_cli.html#bluemix_iam_account_user_reinvite)</td>
  <td>[bluemix iam api-keys](bx_cli.html#bluemix_iam_api_keys)</td>
  <td>[bluemix iam api-key-create](bx_cli.html#bluemix_iam_api_key_create)</td>
  <td>[bluemix iam api-key-delete](bx_cli.html#bluemix_iam_api_key_delete)</td>
 </tr>
 <tr>
  <td>[bluemix iam api-key-update](bx_cli.html#bluemix_iam_api_key_update)</td>
  <td></td>
  <td></td>
  <td></td>
  <td></td>
 </tr>
 </tbody>
 </table>

<table summary="Bluemix-Befehle zur Verwaltung von CF-Apps und von Domänen, Routen und Zertifikaten für Apps.">
<caption>Table 3. Befehle zur Verwaltung von CF-Apps und von Domänen, Routen und Zertifikaten für Apps</caption>
 <thead>
 <th colspan="5">Befehle zur Verwaltung von CF-Apps und von Domänen, Routen und Zertifikaten für Apps</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix app push](bx_cli.html#bluemix_app_push)</td>
 <td>[bluemix app list](bx_cli.html#bluemix_app_list)</td>
 <td>[bluemix app show](bx_cli.html#bluemix_app_show)</td>
 <td>[bluemix app delete](bx_cli.html#bluemix_app_delete)</td>
 <td>[bluemix app rename](bx_cli.html#bluemix_app_rename)</td>
 </tr>
 <tr>
 <td>[bluemix app start](bx_cli.html#bluemix_app_start)</td>
 <td>[bluemix app stop](bx_cli.html#bluemix_app_stop)</td>
 <td>[bluemix app restart](bx_cli.html#bluemix_app_restart)</td>
 <td>[bluemix app restage](bx_cli.html#bluemix_app_restage)</td>
 <td>[bluemix app instance-restart](bx_cli.html#bluemix_app_instance_restart)</td>
 </tr>
 <tr>
 <td>[bluemix app events](bx_cli.html#bluemix_app_events)</td>
 <td>[bluemix app files](bx_cli.html#bluemix_app_files)</td>
 <td>[bluemix app logs](bx_cli.html#bluemix_app_logs)</td>
 <td>[bluemix app env](bx_cli.html#bluemix_app_env)</td>
 <td>[bluemix app env-set](bx_cli.html#bluemix_app_env_set)</td>
 </tr>
 <tr>
 <td>[bluemix app env-unset](bx_cli.html#bluemix_app_env_unset)</td>
 <td>[bluemix app stacks](bx_cli.html#bluemix_app_stacks)</td>
 <td>[bluemix app stack-show](bx_cli.html#bluemix_app_stack_show)</td>
 <td>[bluemix app manifest-create](bx_cli.html#bluemix_app_manifest_create)</td>
 <td>[bluemix app domain-cert](bx_cli.html#bluemix_app_domain_cert)</td>
 </tr>
 <tr>
  <td>[bluemix app domain-cert-add](bx_cli.html#bluemix_app_domain_cert_add)</td>
  <td>[bluemix app domain-cert-remove](bx_cli.html#bluemix_app_domain_cert_remove)</td>
  <td>[bluemix app domains](bx_cli.html#bluemix_app_domains)</td>
  <td>[bluemix app domain-create](bx_cli.html#bluemix_app_domain_create)</td>
  <td>[bluemix app domain-delete](bx_cli.html#bluemix_app_domain_delete)</td>
 </tr>
 <tr>
  <td>[bluemix app shared-domain-create](bx_cli.html#bluemix_app_shared_domain_create)</td>
  <td>[bluemix app shared-domain-delete](bx_cli.html#bluemix_app_shared_domain_delete)</td>
  <td>[bluemix app routes](bx_cli.html#bluemix_app_routes)</td>
  <td>[bluemix app route-check](bx_cli.html#bluemix_app_route_check)</td>
  <td>[bluemix app route-map](bx_cli.html#bluemix_app_route_map)</td>
 </tr>
 <tr>
  <td>[bluemix app route-unmap](bx_cli.html#bluemix_app_route_unmap)</td>
  <td>[bluemix app route-create](bx_cli.html#bluemix_app_route_create)</td>
  <td>[bluemix app route-delete](bx_cli.html#bluemix_app_route_delete)</td>
  <td>[bluemix app orphaned-routes-delete](bx_cli.html#bluemix_app_orphaned_routes_delete)</td>
  <td></td>
 </tr>
  </tbody>
 </table>

<table summary="Bluemix-Befehle zur Verwaltung von Bluemix-Services">
<caption>Tabelle 4. Befehle zur Verwaltung von Bluemix-Services</caption>
 <thead>
 <th colspan="5">Befehle zur Verwaltung von Bluemix-Services</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix service offerings](bx_cli.html#bluemix_service_offerings)</td>
 <td>[bluemix service list](bx_cli.html#bluemix_service_list)</td>
 <td>[bluemix service show](bx_cli.html#bluemix_service_show)</td>
 <td>[bluemix service create](bx_cli.html#bluemix_service_create)</td>
 <td>[bluemix service update](bx_cli.html#bluemix_service_update)</td>
 </tr>
 <tr>
 <td>[bluemix service delete](bx_cli.html#bluemix_service_delete)</td>
 <td>[bluemix service rename](bx_cli.html#bluemix_service_rename)</td>
 <td>[bluemix service bind](bx_cli.html#bluemix_service_bind)</td>
 <td>[bluemix service unbind](bx_cli.html#bluemix_service_unbind)</td>
 <td>[bluemix service key-create](bx_cli.html#bluemix_service_key_create)</td>
 </tr>
 <tr>
 <td>[bluemix service key-delete](bx_cli.html#bluemix_service_key_delete)</td>
 <td>[bluemix service keys](bx_cli.html#bluemix_service_keys)</td>
 <td>[bluemix service key-show](bx_cli.html#bluemix_service_key_show)</td>
 <td>[bluemix service user-provided-create](bx_cli.html#bluemix_service_user_provided_create)</td>
 <td>[bluemix service user-provided-update](bx_cli.html#bluemix_service_user_provided_update)</td>
 </tr>
  </tbody>
 </table>

<table summary="Bluemix-Befehle zur Verwaltung der Bluemix-Einstellungen für Kataloge, Plug-ins, Abrechnungen und Sicherheit.">
<caption>Tabelle 5. Befehle zur Verwaltung der Bluemix-Einstellungen für Kataloge, Plug-ins, Abrechnungen und Sicherheit</caption>
 <thead>
 <th colspan="5">Befehle zur Verwaltung der Bluemix-Einstellungen für Kataloge, Plug-ins, Abrechnungen und Sicherheit</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix catalog templates](bx_cli.html#bluemix_catalog_templates)</td>
 <td>[bluemix catalog template](bx_cli.html#bluemix_catalog_template)</td>
 <td>[bluemix catalog template-run](bx_cli.html#bluemix_catalog_template_run)</td>
 <td>[bluemix plugin repos](bx_cli.html#bluemix_plugin_repos)</td>
 <td>[bluemix plugin repo-add](bx_cli.html#bluemix_plugin_repo_add)</td>
 </tr>
 <tr>
 <td>[bluemix plugin repo-remove](bx_cli.html#bluemix_plugin_repo_remove)</td>
 <td>[bluemix plugin repo-plugins](bx_cli.html#bluemix_plugin_repo_plugins)</td>
 <td>[bluemix plugin list](bx_cli.html#bluemix_plugin_list)</td>
 <td>[bluemix plugin install](bx_cli.html#bluemix_plugin_install)</td>
 <td>[bluemix plugin uninstall](bx_cli.html#bluemix_plugin_uninstall)</td>
 </tr>
 <tr>
 <td>[bluemix plugin update](bx_cli.html#bluemix_plugin_update)</td>
 <td>[bluemix billing account-usage](bx_cli.html#bluemix_billing_account_usage)</td>
 <td>[bluemix billing org-usage](bx_cli.html#bluemix_billing_org_usage)</td>
 <td>[bluemix billing orgs-usage-summary](bx_cli.html#bluemix_billing_orgs_usage_summary)</td>
 <td></td>
 </tr>
 </tbody>
 </table>
 
## bluemix help
{: #bluemix_help}
Zeigt die erweiterte Hilfe für integrierte Befehle und unterstützte Namensbereiche der obersten Ebene in der {{site.data.keyword.Bluemix_notm}}-CLI oder die Hilfe für einen bestimmten integrierten Befehl oder Namensbereich an.

```
bluemix help [COMMAND|NAMESPACE]
```

<strong>Voraussetzungen</strong>: Keine

<strong>Befehlsoptionen:</strong>

   <dl>
   <dt>COMMAND|NAMESPACE (optional)</dt>
   <dd>Der Befehl oder Namensbereich, für den die Hilfe angezeigt wird. Wenn nichts angegeben ist, wird die erweiterte Hilfe für die {{site.data.keyword.Bluemix_notm}}-CLI angezeigt.</dd>
   </dl>



<strong>Beispiele</strong>:

Erweiterte Hilfe für die {{site.data.keyword.Bluemix_notm}}-CLI anzeigen:

```
bluemix help
```

Hilfe für den Befehl `info` anzeigen:

```
bluemix help info
```



## bluemix api
{: #bluemix_api}
{{site.data.keyword.Bluemix_notm}}-API-Endpunkt festlegen oder anzeigen.

```
bluemix api [API_ENDPOINT] [--unset] [--skip-ssl-validation]
```

<strong>Voraussetzungen</strong>: Keine

<strong>Befehlsoptionen:</strong>
   <dl>
   <dt>API_ENDPOINT (optional)</dt>
   <dd>Der API-Endpunkt, der als Ziel verwendet wird, zum Beispiel `https://api.chinabluemix.net`. Wenn weder die Option *API_ENDPOINT* noch die Option `--unset` angegeben wird, wird der aktuelle API-Endpunkt angezeigt.</dd>
   <dt>--unset (optional)</dt>
   <dd>Entfernt die Einstellung für den API-Endpunkt.</dd>
   <dt>--skip-ssl-validation (optional)</dt>
   <dd>Umgeht die SSL-Validierung von HTTP-Anforderungen.</dd>
   </dl>
<strong>Beispiele</strong>:

Für den API-Endpunkt api.chinabluemix.net festlegen:

```
bluemix api api.chinabluemix.net
```

```
bluemix api https://api.chinabluemix.net --skip-ssl-validation
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

Benutzer anmelden. 

```
bluemix login [OPTIONS...]
```

<strong>Voraussetzungen</strong>: Keine

<strong>Befehlsoptionen:</strong>
<dl>
  <dt>-a <i>API_ENDPOINT</i> (optional)</dt>
  <dd> API-Endpunkt (z. B.: api.ng.bluemix.net)</dd>
  <dt> --apikey <i>API_KEY oder @API_KEY_FILE_PATH</i>
  <dd> API-Schlüsselinhalt oder der Pfad einer API-Schlüsseldatei, die durch @ angegeben wird.</dd>
  <dt> --sso (optional) </dt>
  <dd> Einmaligen Kenncode zum Anmelden verwenden. </dd>
  <dt> -u <i>USERNAME</i> (optional)</dt>
  <dd> Der Benutzername.</dd>
  <dt> -p <i>PASSWORD</i> (optional)</dt>
  <dd> Das Kennwort.</dd>
  <dt> -c <i>ACCOUNT_ID</i> (optional) </dt>
  <dd> Die ID des Zielkontos.</dd>
  <dt> -o <i>ORG_NAME</i> (optional) </dt>
  <dd> Der Name der Zielorganisation. </dd>
  <dt> -s <i>SPACE_NAME</i> (optional) </dt>
  <dd> Der Name des Zielbereichs.</dd>
  <dt> --skip-ssl-validation (optional) </dt>
  <dd> Umgeht die SSL-Validierung von HTTP-Anforderungen. Diese Option wird nicht empfohlen.</dd>
</dl>

<strong>Beispiele</strong>:

Interaktive Anmeldung:

```
bluemix login
```

Anmeldung mit einem Benutzernamen und einem Kennwort und Festlegen des Kontos, der Organisation und des Bereichs:

```
bluemix login -u Benutzername -p Kennwort -c MyAccountID -o MyOrg -s MySpace
```

Anmeldung mit einmaligem Kenncode und Festlegen eines Zielkontos, einer Organisation und eines Bereichs:

```
bluemix login --sso -c MyAccountID -o MyOrg -s MySpace
```

Anmeldung mit API-Schlüssel und Festlegen von Zielen:

* API-Schlüssel hat zugeordnetes Konto.

```
bluemix login --apikey api-key-string -o MyOrg -s MySpace
```

```
bluemix login --apikey @Dateiname -o MyOrg -s MySpace
```

* API-Schlüssel hat kein zugeordnetes Konto.

```
bluemix login --apikey api-key-string -c MyAccountID -o MyOrg -s MySpace
```

```
bluemix login --apikey @Dateiname -c MyAccountID -o MyOrg -s MySpace
```

<strong>Hinweis:</strong> Wenn der API-Schlüssel ein zugeordnetes Konto hat, ist ein Wechsel zu einem anderen Konto nicht zulässig.


## bluemix logout
{: #bluemix_logout}

Benutzer abmelden.

```
bluemix logout
```

<strong>Voraussetzungen</strong>: Keine


## bluemix target
{: #bluemix_target}


Zielkonto, Region, Organisation oder Bereich festlegen oder anzeigen.

```
bluemix target [-c ACCOUNT_ID] [-r REGION] [-o ORG_NAME] [-s SPACE_NAME]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen:</strong>
   <dl>
   <dt>-c <i>ACCOUNT_ID</i> (optional)</dt>
   <dd>Die ID des Zielkontos.</dd>
   <dt>-r <i>REGION</i> (optional)</dt>
   <dd>Die Region, zu der gewechselt werden soll.</dd>
   <dt>-o <i>ORG_NAME</i> (optional)</dt>
   <dd>Der Name der Zielorganisation.</dd>
   <dt>-s <i>SPACE_NAME</i> (optional)</dt>
   <dd>Der Name des Zielbereichs.</dd>
   </dl>
Wenn keine der Optionen angegeben wird, werden das aktuelle Konto, die aktuelle Region, die aktuelle Organisation und der aktuelle Bereich angezeigt.

<strong>Beispiele</strong>:

Festlegen des aktuellen Kontos, der aktuellen Organisation und des aktuellen Bereichs:

```
bluemix target -c MyAccountID -o MyOrg -s MySpace
```

Zu einer neuen Region wechseln:

```
bluemix target -r eu-gb
```

Anzeigen des aktuellen Kontos, der aktuellen Region, der aktuellen Organisation und des aktuellen Bereichs:

```
bluemix target
```


## bluemix info
{: #bluemix_info}

{{site.data.keyword.Bluemix_notm}}-Basisinformationen einschließlich aktueller Region, Cloud-Controller-Version und einigen nützlichen Endpunkten (zum Beispiel zum Anmelden und Austauschen von Zugriffstoken) anzeigen.

```
bluemix info
```

<strong>Voraussetzungen</strong>: Endpunkt


## bluemix config
{: #bluemix_config}


Schreibt Standardwerte in die Konfigurationsdatei.

```
bluemix config --http-timeout TIMEOUT_IN_SECONDS | --trace (true|false|path/to/file) | --color (true|false) | --locale (LOCALE|CLEAR) | --check-version (true|false)
```

<strong>Voraussetzungen</strong>: Keine

<strong>Befehlsoptionen:</strong>
   <dl>
   <dt>--http-timeout <i>TIMEOUT_IN_SECONDS</i></dt>
   <dd>Der Zeitlimitwert für HTTP-Anforderungen. Der Standardwert ist 60 Sekunden.</dd>
   <dt>--trace true|false|<i>path-to-file</i></dt>
   <dd>Trace für HTTP-Anforderungen mit Ausgabe auf Terminal oder in angegebener Datei aktivieren.</dd>
   <dt>--color true|false</dt>
   <dd>Farbausgabe aktivieren oder inaktivieren. Die Farbausgabe ist standardmäßig aktiviert.</dd>
   <dt>--locale <i>LOCALE|CLEAR</i></dt>
   <dd>Eine Standardländereinstellung festlegen. Wenn LOCALE den Wert <i>CLEAR</i> hat, wird die vorherige Ländereinstellung gelöscht.</dd>
   <dt>--check-version true|false</dt>
   <dd>CLI-Versionsprüfung aktivieren oder inaktivieren.</dd>
   </dl>

Es kann jeweils nur eine dieser Optionen gleichzeitig angegeben werden.

<strong>Beispiele</strong>:

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


## bluemix curl
{: #bluemix_curl}

Ausführung einer unformatierten HTTP-Anforderung für {{site.data.keyword.Bluemix_notm}}. *Content-Type* ist standardmäßig auf *application/json* eingestellt. Dieser Befehl sendet die Anforderung an {{site.data.keyword.Bluemix_notm}} Multi-Cloud Control Proxy. Informationen zu den unterstützten Pfaden finden Sie in den API-Pfaddefinitionen im [CloudFoundry-API-Dokument ](http://apidocs.cloudfoundry.org/){: new_window} ![Symbol für externen Link](../../../icons/launch-glyph.svg).

```
bluemix curl PATH [OPTIONS...]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen:</strong>
   <dl>
   <dt><i>PATH</i> (erforderlich)</dt>
   <dd>Der URL-Pfad der Ressource. Beispiel: /v2/apps.</dd>
   <dt><i>OPTIONS</i> (optional)</dt>
   <dd>Die Optionen, die vom Befehl `bluemix curl` unterstützt werden, sind mit den Optionen identisch, die vom Befehl `cf curl` unterstützt werden.</dd>
   </dl>

<strong>Beispiele</strong>:

Informationen für alle Organisationen des aktuellen Kontos anzeigen:

```
bluemix curl /v2/organizations
```

## bluemix update
{: #bluemix_update}

Die Befehlszeilenschnittstelle auf die neueste Version aktualisieren.

```
bluemix update
```

<strong>Voraussetzungen</strong>: Keine

## bluemix regions
{: #bluemix_regions}

Zeigt die Informationen für alle Regionen in {{site.data.keyword.Bluemix_notm}} an.

```
bluemix regions
```

<strong>Voraussetzungen</strong>: Endpunkt


## bluemix iam orgs
{: #bluemix_iam_orgs}

Alle Organisationen auflisten

```
bluemix iam orgs [-r REGION] [--guid]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen:</strong>
   <dl>
   <dt>-r <i>REGION</i> (optional)</dt>
   <dd>Für welche Region die Organisationsinformationen angezeigt werden sollen. Wenn 'all' angegeben ist, werden alle Organisationen in allen Regionen aufgelistet.</dd>
   <dt>--guid (optional)</dt>
   <dd>GUID der Organisationen anzeigen.</dd>
   </dl>

<strong>Beispiele</strong>:

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

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen:</strong>
   <dl>
   <dt>ORG_NAME (erforderlich)</dt>
   <dd>Der Name der Organisation.</dd>
   <dt>--guid (optional)</dt>
   <dd>GUID der Organisationen anzeigen.</dd>
   </dl>

<strong>Beispiele</strong>:

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

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen:</strong>
   <dl>
   <dt>ORG_NAME (erforderlich)</dt>
   <dd>Der Name der Organisation, die erstellt wird.</dd>
   </dl>

<strong>Beispiele</strong>:

Organisation mit dem Namen `IBM` erstellen:

```
bluemix iam org-create IBM
```

## bluemix iam org-replicate
{: #bluemix_iam_org_replicate}

Repliziert eine Organisation aus der aktuellen Region in eine andere Region.

```
bluemix iam org-replicate ORG_NAME REGION_NAME
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen:</strong>
   <dl>
   <dt>ORG_NAME (erforderlich)</dt>
   <dd>Der Name der vorhandenen Organisation, die repliziert werden soll.</dd>
   <dt>REGION_NAME (erforderlich)</dt>
   <dd>Der Name der Region, die die replizierte Organisation hostet.</dd>
   </dl>

<strong>Beispiele</strong>:

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

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen:</strong>
   <dl>
   <dt>OLD_ORG_NAME (erforderlich)</dt>
   <dd>Der bisherige Name der Organisation, die umbenannt werden soll.</dd>
   <dt>NEW_ORG_NAME (erforderlich)</dt>
   <dd>Der neue Name für die Organisation, die umbenannt werden soll.</dd>
   </dl>

## bluemix iam org-delete
{: #bluemix_iam_org_delete}

Die angegebene Organisation in der aktuellen Region löschen.

```
bluemix iam org-delete ORG_NAME [-f --all]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen:</strong>
   <dl>
   <dt>ORG_NAME (erforderlich)</dt>
   <dd>Der Name der vorhandenen Organisation, die gelöscht werden soll.</dd>
   <dt>-f (optional)</dt>
   <dd>Löschung ohne Bestätigung erzwingen.</dd>
   <dt>--all (optional)</dt>
   <dd>Die Organisation in allen Regionen löschen.</dd>
   </dl>


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

## bluemix iam org-users
{: #bluemix_iam_org_users}

Benutzer in der angegebenen Organisation nach Rolle anzeigen

```
bluemix iam org-users ORG_NAME [-a]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen:</strong>
<dl>
<dt>ORG_NAME (erforderlich)</dt>
<dd>Der Name der Organisation.</dd>
<dt>-a (optional)</dt>
<dd>Alle Benutzer in der angegebenen Organisation auflisten (nicht nach Rolle gruppiert).</dd>
</dl>

## bluemix iam org-user-add
{: #bluemix_iam_org_user_add}

Benutzer zur Organisation hinzufügen (Organisationsmanager erforderlich).

```
 bluemix iam org-user-add USER_NAME ORG
```

## bluemix iam org-user-remove
{: #bluemix_iam_org_user_remove}

Benutzer aus Organisation entfernen (Organisationsmanager oder nur Benutzer selbst)

```
   bluemix iam org-user-remove USER_NAME ORG [-f, --force]
```

<strong>Befehlsoptionen:</strong>
<dl>
<dt>--force, -f</dt>
<dd>Löschung ohne Bestätigung erzwingen.</dd>
</dl>

## bluemix iam org-roles
{: #bluemix_iam_org_roles}

Alle Organisationsrollen des aktuellen Benutzers abrufen.

```
bluemix iam org-roles
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

## bluemix iam org-role-set
{: #bluemix_iam_org_role_set}

Einem Benutzer eine Organisationsrolle zuweisen. Diese Operation kann nur von einem Organisationsmanager ausgeführt werden.

```
bluemix iam org-role-set USER_NAME ORG_NAME ORG_ROLE
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen:</strong>
  <dl>
   <dt>USER_NAME (erforderlich)</dt>
   <dd>Der Name des Benutzers, der zugeordnet wird.</dd>
   <dt>ORG_NAME (erforderlich)</dt>
   <dd>Der Name der Organisation, der dieser Benutzer zugeordnet wird.</dd>
   <dt>ORG_ROLE (erforderlich)</dt>
   <dd>Der Name der Organisationsrolle, der dieser Benutzer zugeordnet wird. Beispiel:
   <ul>
   <li>OrgManager: Diese Rolle kann Benutzer einladen und verwalten, Pläne auswählen und ändern sowie Ausgabenlimits festlegen.</li>
   <li>BillingManager: Diese Rolle kann die Abrechnungskonto- und Zahlungsinformationen erstellen und verwalten.</li>
   <li>OrgAuditor: Diese Rolle verfügt über Lesezugriff auf die Organisationsinformationen und -berichte.</li>
   </ul>
   </dd>
  </dl>

<strong>Beispiele</strong>:

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

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen:</strong>
   <dl>
   <dt>USER_NAME (erforderlich)</dt>
   <dd>Der Name des Benutzers, der entfernt wird.</dd>
   <dt>ORG_NAME (erforderlich)</dt>
   <dd>Der Name der Organisation, aus der dieser Benutzer entfernt wird.</dd>
   <dt>ORG_ROLE (erforderlich)</dt>
   <dd>Der Name der Organisationsrolle, aus der dieser Benutzer entfernt wird. Beispiel:
   <ul>
   <li>OrgManager: Diese Rolle kann Benutzer einladen und verwalten, Pläne auswählen und ändern sowie Ausgabenlimits festlegen.</li>
   <li>BillingManager: Diese Rolle kann die Abrechnungskonto- und Zahlungsinformationen erstellen und verwalten.</li>
   <li>OrgAuditor: Diese Rolle verfügt über Lesezugriff auf die Organisationsinformationen und -berichte.</li>
   </ul>
   </dd>
    </dl>

<strong>Beispiele</strong>:

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

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen:</strong>
   <dl>
   <dt>ORG_NAME (erforderlich)</dt>
   <dd>Der Name der Organisation.</dd>
   <dt>SPACE_NAME (erforderlich)</dt>
   <dd>Der Name des Bereichs.</dd>
   </dl>


## bluemix iam space-role-set
{: #bluemix_iam_space_role_set}

Einem Benutzer eine Bereichsrolle zuweisen. Diese Operation kann nur von einem Bereichsmanager ausgeführt werden.

```
bluemix iam space-role-set USER_NAME ORG_NAME SPACE_NAME SPACE_ROLE
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen:</strong>

   <dl>
   <dt>USER_NAME (erforderlich)</dt>
   <dd>Der Name des Benutzers, der zugeordnet wird.</dd>
   <dt>ORG_NAME (erforderlich)</dt>
   <dd>Der Name der Organisation, der dieser Benutzer zugeordnet wird.</dd>
   <dt>SPACE_NAME (erforderlich)</dt>
   <dd>Der Name des Bereichs, dem dieser Benutzer zugeordnet wird.</dd>
   <dt>SPACE_ROLE (erforderlich)</dt>
   <dd>Der Name der Bereichsrolle, die diesem Benutzer zugeordnet wird. Beispiel:
   <ul>
   <li>SpaceManager: Diese Rolle kann Benutzer einladen und verwalten sowie Funktionen für einen angegebenen Bereich aktivieren.</li>
   <li>SpaceDeveloper: Diese Rolle kann Apps und Services erstellen und verwalten sowie Protokolle und Berichte anzeigen.</li>
   <li>SpaceAuditor: Diese Rolle kann Protokolle, Berichte und Einstellungen für den Bereich anzeigen.</li>
   </ul></dd>
    </dl>

<strong>Beispiele</strong>:

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

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen:</strong>

   <dl>
   <dt>USER_NAME (erforderlich)</dt>
   <dd>Der Name des Benutzers, der entfernt wird.</dd>
   <dt>ORG_NAME (erforderlich)</dt>
   <dd>Der Name der Organisation, aus der dieser Benutzer entfernt wird.</dd>
   <dt>SPACE_NAME (erforderlich)</dt>
   <dd>Der Name des Bereichs, aus dem dieser Benutzer entfernt wird.</dd>
   <dt>SPACE_ROLE (erforderlich)</dt>
   <dd>Der Name der Bereichsrolle, aus der dieser Benutzer entfernt wird. Beispiel:
   <ul>
   <li>SpaceManager: Diese Rolle kann Benutzer einladen und verwalten sowie Funktionen für einen angegebenen Bereich aktivieren.</li>
   <li>SpaceDeveloper: Diese Rolle kann Apps und Services erstellen und verwalten sowie Protokolle und Berichte anzeigen.</li>
   <li>SpaceAuditor: Diese Rolle kann Protokolle, Berichte und Einstellungen für den Bereich anzeigen.</li>
   </ul></dd>
    </dl>


<strong>Beispiele</strong>:

Die Benutzerin `Mary` aus der Organisation `IBM` und dem Bereich `Cloud` mit der Rolle `SpaceManager` entfernen:

```
bluemix iam space-role-unset Mary IBM Cloud SpaceManager
```

## bluemix iam accounts
{: #bluemix_iam_accounts}

Alle Konten des aktuellen Benutzers auflisten.

```
bluemix iam accounts
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung


## bluemix iam org-account
{: #bluemix_iam_org_account}

Das Konto der angegebenen Organisation anzeigen (Organisationsbenutzer erforderlich).

```
bluemix iam org-account ORG_NAME [--guid]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen:</strong>
<dl>
  <dt>--guid (optional)</dt>
  <dd>Nur die Konto-ID anzeigen.</dd>
</dl>


## bluemix iam account-users
{: #bluemix_iam_account_users}

Dem Konto zugeordnete Benutzer anzeigen. Diese Operation kann nur vom Kontoeigner ausgeführt werden.

```
bluemix iam account-users
```

## bluemix iam account-user-delete
{: #bluemix_iam_account_user_delete}

Benutzer aus dem aktuellen Konto löschen (nur Kontoeigner).

```
bluemix iam account-user-delete USERNAME [-f]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen:</strong>
<dl>
<dt>USERNAME (erforderlich)</dt>
<dd>Der Benutzername.</dd>
<dt>--force, -f (optional)</dt>
<dd>Löschung ohne Bestätigung erzwingen.</dd>
</dl>

## bluemix iam account-user-invite
{: #bluemix_iam_account_user_invite}

Lädt den Benutzer zu dem Konto mit bereits festgelegter Organisation und Bereichsrolle ein. Diese Operation kann nur vom Kontoeigner ausgeführt werden.

```
bluemix iam account-user-invite USER_NAME ORG_NAME ORG_ROLE SPACE_NAME SPACE_ROLE
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen:</strong>
<dl>
   <dt>USER_NAME (erforderlich)</dt>
   <dd>Der Name des Benutzers, der eingeladen wird.</dd>
   <dt>ORG_NAME (erforderlich)</dt>
   <dd>Der Name der Organisation, zu der dieser Benutzer eingeladen wird.</dd>
   <dt>ORG_ROLE (erforderlich)</dt>
   <dd>Der Name der Organisationsrolle, zu der dieser Benutzer eingeladen wird. Beispiel:
   <ul>
  <li>OrgManager: Diese Rolle kann Benutzer einladen und verwalten, Pläne auswählen und ändern sowie Ausgabenlimits festlegen.</li>
  <li>BillingManager: Diese Rolle kann die Abrechnungskonto- und Zahlungsinformationen erstellen und verwalten.</li>
  <li>OrgAuditor: Diese Rolle verfügt über Lesezugriff auf die Organisationsinformationen und -berichte.</li>
  </ul> </dd>
   <dt>SPACE_NAME (erforderlich)</dt>
   <dd>Der Name des Bereichs, zu dem dieser Benutzer eingeladen wird.</dd>
   <dt>SPACE_ROLE (erforderlich)</dt>
   <dd>Der Name des Bereichs, zu dem dieser Benutzer eingeladen wird. Der Name der Bereichsrolle, zu der dieser Benutzer eingeladen wird. Beispiel:
   <ul>
<li>SpaceManager: Diese Rolle kann Benutzer einladen und verwalten sowie Funktionen für einen angegebenen Bereich aktivieren.</li>
<li>SpaceDeveloper: Diese Rolle kann Apps und Services erstellen und verwalten sowie Protokolle und Berichte anzeigen.</li>
<li>SpaceAuditor: Diese Rolle kann Protokolle, Berichte und Einstellungen für den Bereich anzeigen.</li>
</ul>
</dd>
</dl>

<strong>Beispiele</strong>:

Die Benutzerin `Mary` zur Organisation `IBM` einladen und die Rolle `OrgManager` sowie den Bereich `Cloud` mit der Rolle `SpaceAuditor` zuweisen:

```
bluemix iam account-user-invite Mary IBM OrgManager Cloud SpaceAuditor
```

## bluemix iam account-user-reinvite
{: #bluemix_iam_account_user_reinvite}

Einladung erneut an einen Benutzer senden (Organisationsmanager oder Kontoeigner erforderlich)

```
 bluemix iam account-user-reinvite USER_EMAIL ORG_NAME
```

## bluemix iam api-keys
{: #bluemix_iam api_keys}

Alle API-Schlüssel der Bluemix-Plattform auflisten.

```
bluemix iam api-keys
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

## bluemix iam api-key-create
{: #bluemix_iam_api_key_create}

Neuen API-Schlüssel für Bluemix-Plattform erstellen.

```
bluemix iam api-key-create NAME [-d DESCRIPTION] [-f, --file FILE]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen:</strong>
<dl>
<dt>NAME (erforderlich)</dt>
<dd>Der Name des zu erstellenden API-Schlüssels.</dd>
<dt>-d <i>DESCRIPTION</i> (optional)</dt>
<dd>Die Beschreibung des API-Schlüssels.</dd>
<dt>-f, -- file <i>FILE</i></dt>
<dd>Informationen zu API-Schlüssel in angegebener Datei speichern. Wenn nicht festgelegt, wird der JSON-Inhalt angezeigt.</dd>
</dl>

<strong>Beispiele</strong>:

API-Schlüssel erstellen und in einer Datei speichern:

```
bluemix iam api-key-create MyKey -d "this is my API key" -f key_file
```

## bluemix iam api-key-update
{: #bluemix_iam_api_key_update}

API-Schlüssel der Bluemix-Plattform aktualisieren.

```
bluemix iam api-key-update NAME [-n NAME] [-d DESCRIPTION]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen:</strong>
<dl>
<dt>NAME (erforderlich)</dt>
<dd>Der alte Name des zu aktualisierenden API-Schlüssels.</dd>
<dt>-n <i>NAME</i> (optional)</dt>
<dd>Der neue Name des API-Schlüssels.</dd>
<dt>-d <i>DESCRIPTION</i> (optional)</dt>
<dd>Die neue Beschreibung des API-Schlüssels.</dd>
</dl>

<strong>Beispiele</strong>:

Beschreibung eines API-Schlüssels aktualisieren:

```
bluemix iam api-key-update MyKey -d "the new description of my key"
```

## bluemix api-key-delete
{: #bluemix_api_key_delete}

API-Schlüssel der Bluemix-Plattform löschen.

```
bluemix iam api-key-delete NAME [-f]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen:</strong>
<dl>
<dt>NAME (erforderlich)</dt>
<dd>Der Name des zu löschenden API-Schlüssels.</dd>
<dt>-f  (optional)</dt>
<dd>Löschung ohne Bestätigung erzwingen.</dd>
</dl>


## bluemix app push
{: #bluemix_app_push}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf push`.


## bluemix app list
{: #bluemix_app_list}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf apps`.


## bluemix app show
{: #bluemix_app_show}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf app`.


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


## bluemix app stack-show
{: #bluemix_app_stack_show}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf stack`.


## bluemix app manifest-create
{: #bluemix_app_manifest_create}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf create-app-manifest`.

## bluemix app domain-cert 
{: #bluemix_app_domain_cert}

Die Zertifikatsinformationen für eine Domäne auflisten

```
bluemix app domain-cert DOMAIN_NAME
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen:</strong>
<dl>
<dt>DOMAIN_NAME (erforderlich)</dt>
<dd>Die Domäne, in der das Zertifikat gehostet wird.</dd>
</dl>


<strong>Beispiele</strong>:

Die Zertifikatsinformationen für die Domäne `ibmcxo-eventconnect.com` anzeigen:

```
bluemix app domain-cert ibmcxo-eventconnect.com
```

## bluemix app domain-cert-add
{: #bluemix_app_domain_cert_add}

Fügt der angegebenen Domäne in der aktuellen Organisation ein Zertifikat hinzu.

```
bluemix app domain-cert-add DOMAIN -k PRIVATE_KEY_FILE -c CERT_FILE [-p PASSWORD] [-i INTERMEDIATE_CERT_FILE] [-t TRUST_STORE_FILE]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel

<strong>Befehlsoptionen:</strong>
   <dl>
   <dt>DOMAIN (erforderlich)</dt>
   <dd>Die Domäne, der das Zertifikat hinzugefügt wird.</dd>
   <dt>-k <i>PRIVATE_KEY_FILE</i> (erforderlich)</dt>
   <dd>Der Pfad der Datei mit dem privaten Schlüssel.</dd>
   <dt>-c <i>CERT_FILE</i> (erforderlich)</dt>
   <dd>Der Pfad der Zertifikatsdatei.</dd>
   <dt>-p <i>PASSWORD</i> (optional)</dt>
   <dd>Das Kennwort für das Zertifikat.</dd>
   <dt>-i <i>INTERMEDIATE_CERT_FILE</i> (optional)</dt>
   <dd>Der Pfad für die Zwischenzertifikatsdatei.</dd>
   <dt>-t <i>TRUST_STORE_FILE</i> (optional)</dt>
   <dd>Die Truststore-Datei.</dd>
   </dl>


<strong>Beispiele</strong>:

Zertifikat der Domäne `ibmcxo-eventconnect.com` hinzufügen:

```
bluemix app domain-cert-add ibmcxo-eventconnect.com -k key_file.key -c cert_file.crt -p 123 -i inter_cert.cert
```

## bluemix app domain-cert-remove
{: #bluemix_app_domain_cert_remove}

Entfernt ein Zertifikat aus der angegebenen Domäne in der aktuellen Organisation.

```
bluemix app domain-cert-remove DOMAIN [-f]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel

<strong>Befehlsoptionen:</strong>

   <dl>
   <dt>DOMAIN (erforderlich)</dt>
   <dd>Die Domäne, aus der das Zertifikat entfernt werden soll.</dd>
   <dt>-f  (optional)</dt>
   <dd>Löschung ohne Bestätigung erzwingen.</dd>
   </dl>

## bluemix app domains
{: #bluemix_app_domains}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf domains`.


## bluemix app domain-create
{: #bluemix_app_domain_create}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf create-domain`.


## bluemix app domain-delete
{: #bluemix_app_domain_delete}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf delete-domain`.


## bluemix app shared-domain-create
{: #bluemix_app_shared_domain_create}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf create-shared-domain`.


## bluemix app shared-domain-delete
{: #bluemix_app_shared_domain_delete}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf delete-shared-domain`.

## bluemix app routes
{: #bluemix_app_routes}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf routes`.


## bluemix app route-check
{: #bluemix_app_route_check}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf check-route`.


## bluemix app route-map
{: #bluemix_app_route_map}

Ordnet eine Route einer vorhandenen cf-Anwendung oder -Containergruppe zu, die über die angegebene Domäne oder den angegebenen Hostnamen verfügt.

```
bluemix app route-map CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel

<strong>Befehlsoptionen:</strong>

   <dl>
   <dt>CF_APP_NAME|CONTAINER_GROUP_NAME (erforderlich)</dt>
   <dd>Der Name der cf-Anwendung oder -Containergruppe für die Zuordnung der Route.</dd>
   <dt>DOMAIN (erforderlich)</dt>
   <dd>Die Domäne der Route. Beispiele: mychinabluemix.net oder chinabluemix.net. </dd>
   <dt>-n <i>HOST_NAME</i> (optional)</dt>
   <dd>Der Hostname der Route. Wenn der Hostname nicht angegeben wird, wird standardmäßig der Anwendungsname oder der Containergruppenname festgelegt.</dd>
   </dl>

<strong>Beispiele</strong>:

Route zu `my-app` mit angegebener Domäne zuordnen:

```
bluemix app route-map my-app mychinabluemix.net
```

Route zu 'my-container-group' mit angegebener Domäne und angegebenem Hostnamen zuordnen:

```
bluemix app route-map my-container-group chinabluemix.net -n abc
```


## bluemix app route-unmap
{: #bluemix_app_route_unmap}

Entfernt die Zuordnung der angegebenen Route von einer vorhandene cf-Anwendung oder -Containergruppe.

```
bluemix app route-unmap CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel

<strong>Befehlsoptionen:</strong>

   <dl>
   <dt>CF_APP_NAME|CONTAINER_GROUP_NAME (erforderlich)</dt>
   <dd>Der Name der cf-Anwendung oder -Containergruppe.</dd>
   <dt>DOMAIN (erforderlich)</dt>
   <dd>Die Domäne der Route (Beispiele: mychinabluemix.net oder chinabluemix.net).</dd>
   <dt>-n <i>HOST_NAME</i> (optional)</dt>
   <dd>Der Hostname der Route. Wenn der Hostname nicht angegeben wird, wird standardmäßig der Anwendungsname oder der Containergruppenname festgelegt.</dd>
   </dl>

<strong>Beispiele</strong>:

Zuordnung von `my-app.mychinabluemix.net` zu `my-app` aufheben:

```
bluemix app route-unmap my-app mychianbluemix.net
```

Zuordnung von `abc.chinabluexmix.net` zu `my-container-group` aufheben:

```
bluemix app route-unmap my-container-group chinabluemix.net -n abc
```


## bluemix app route-create
{: #bluemix_app_route_create}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf create-route`.


## bluemix app route-delete
{: #bluemix_app_route_delete}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf delete-route`.


## bluemix app orphaned-routes-delete
{: #bluemix_app_orphaned_routes_delete}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf delete-orphaned-routes`.


## bluemix app domains
{: #bluemix_app_domains}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf domains`.


## bluemix app domain-create
{: #bluemix_app_domain_create}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf create-domain`.


## bluemix app domain-delete
{: #bluemix_app_domain_delete}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf delete-domain`.


## bluemix app shared-domain-create
{: #bluemix_app_shared_domain_create}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf create-shared-domain`.


## bluemix app shared-domain-delete
{: #bluemix_app_shared_domain_delete}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf delete-shared-domain`.


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

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen:</strong>

   <dl>
   <dt>-d (optional)</dt>
   <dd>Wenn die Option <i>-d</i> angegeben wird, wird auch die Beschreibung jeder Vorlage angezeigt. Andernfalls werden nur die ID und der Name jeder Vorlage angezeigt.</dd>
   </dl>


## bluemix catalog template
{: #bluemix_catalog_template}

Zeigt die detaillierten Informationen einer angegebenen Boilerplate-Vorlage an.

```
bluemix catalog template TEMPLATE_ID
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen:</strong>
   <dl>
   <dt>TEMPLATE_ID (erforderlich)</dt>
   <dd>Die ID der Boilerplate-Vorlage. Verwenden Sie <i>bluemix templates</i>, um die IDs aller Vorlagen anzuzeigen.</dd>
   </dl>


<strong>Beispiele</strong>:

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

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel

<strong>Befehlsoptionen:</strong>
   <dl>
   <dt>TEMPLATE_ID (erforderlich)</dt>
   <dd>Die Vorlage, auf der die Anwendung bei ihrer Erstellung basiert. Verwenden Sie <i>bluemix templates</i>, um die IDs aller Vorlagen anzuzeigen.</dd>
   <dt>CF_APP_NAME (erforderlich)</dt>
   <dd>Der Name der cf-Anwendung, die erstellt werden soll.</dd>
   <dt>-u <i>URL</i> (optional)</dt>
   <dd>Die Route der Anwendung. Wenn sie nicht angegeben ist, wird die Route von Bluemix automatisch auf der Grundlage des Anwendungsnamens und der Standarddomäne festgelegt.</dd>
   <dt>-d <i>DESCRIPTION</i> (optional)</dt>
   <dd>Die Beschreibung für die Anwendung.</dd>
   <dt>--no-start (optional)</dt>
   <dd>Startet die Anwendung nach ihrer Erstellung nicht automatisch. Wenn diese Option nicht angegeben wird, wird die Anwendung nach ihrer Erstellung automatisch gestartet.</dd>
   </dl>


<strong>Beispiele</strong>:

cf-Anwendung `my-app` auf der Basis der Vorlage `javaHelloWorld` erstellen:

```
bluemix catalog template-run javaHelloWorld my-app
```

Anwendung `my-ruby-app` auf der Basis der Vorlage `rubyHelloWorld` mit der Route `myrubyapp.chinabluemix.net` und der Beschreibung `My first ruby app on {{site.data.keyword.Bluemix_notm}}.` erstellen:

```
bluemix catalog template-run rubyHelloWorld my-ruby-app -u myrubyapp.chinabluemix.net -d "My first ruby app on {{site.data.keyword.Bluemix_notm}}."
```

Anwendung `my-python-app` auf Basis der Vorlage `pythonHelloWorld` ohne automatischen Start erstellen:

```
bluemix catalog template-run pythonHelloWorld my-python-app --no-start
```

## bluemix billing account-usage
{: #bluemix_billing_account_usage}

Monatliche Nutzung und Kosten des Kontos anzeigen.

```
bluemix billing account-usage [-d YYYY-MM] [--json]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen:</strong>

<dl>
  <dt>-d MONTH_DATE (optional)</dt>
  <dd>Daten für Monat und Datum durch Angeben des Formats JJJJ-MM anzeigen. Bei keiner Angabe wird die Nutzung des aktuellen Monats angezeigt.</dd>
  <dt>--json (optional)</dt>
  <dd>Nutzungsergebnis im JSON-Format anzeigen.</dd>
</dl>

<strong>Beispiele</strong>:

Nutzungs- und Kostenbericht des Kontos für 06/2016 anzeigen:

```
bluemix billing account-usage -d 2016-06
```

## bluemix billing org-usage
{: #bluemix_billing_org_usage}

Monatliche Nutzungsdetails einer Organisation anzeigen. Diese Operation kann nur von einem Abrechnungsmanager der Organisation ausgeführt werden.

```
bluemix billing org-usage ORG_NAME [-d YYYY-MM] [-r REGION_NAME] [--json]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen:</strong>

<dl>
  <dt>ORG_NAME (erforderlich)</dt>
  <dd>Name der Organisation.</dd>
  <dt>-d MONTH_DATE (optional)</dt>
  <dd>Daten für Monat und Datum durch Angeben des Formats JJJJ-MM anzeigen. Bei keiner Angabe wird die Nutzung des aktuellen Monats angezeigt.</dd>
  <dt>-r REGION_NAME</dt>
  <dd>Name der Region, in der die Organisation gehostet wird. Wenn 'Alle' eingestellt ist, wird die Organisationsnutzung in allen Regionen angezeigt.</dd>
  <dt>--json (optional)</dt>
  <dd>Nutzungsergebnis im JSON-Format anzeigen.</dd>
</dl>



## bluemix billing orgs-usage-summary
{: #bluemix_billing_orgs_usage_summary}

Zusammenfassung der monatlichen Nutzung für die Organisationen im eigenen Konto anzeigen.

```
bluemix billing orgs-usage-summary [-d YYYY-MM] [-r REGION_NAME] [--json]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen:</strong>

<dl>
  <dt>-d MONTH_DATE (optional)</dt>
  <dd>Daten für Monat und Datum durch Angeben des Formats JJJJ-MM anzeigen. Bei keiner Angabe wird die Nutzung des aktuellen Monats angezeigt.</dd>
  <dt>-r REGION_NAME</dt>
  <dd>Name der Region, in der die Organisationen gehostet werden. Wenn 'Alle' eingestellt ist, wird eine Nutzungszusammenfassung der Organisationen in allen Regionen angezeigt.</dd>
  <dt>--json (optional)</dt>
  <dd>Nutzungsergebnis im JSON-Format anzeigen.</dd>
</dl>


## bluemix plugin repos
{: #bluemix_plugin_repos}

Listet alle Plug-in-Repositorys auf, die in der Befehlszeilenschnittstelle von {{site.data.keyword.Bluemix_notm}} registriert sind.

```
bluemix plugin repos
```

<strong>Voraussetzungen</strong>: Keine


## bluemix plugin repo-add
{: #bluemix_plugin_repo_add}

Fügt ein neues Plug-in-Repository zur Befehlszeilenschnittstelle von {{site.data.keyword.Bluemix_notm}} hinzu.

```
bluemix plugin repo-add REPO_NAME REPO_URL
```

<strong>Voraussetzungen</strong>: Keine

<strong>Befehlsoptionen:</strong>

   <dl>
   <dt>REPO_NAME (erforderlich)</dt>
   <dd>Der Name des Repositorys, das hinzugefügt werden soll. Sie können einen eigenen Namen für jedes Repository definieren.</dd>
   <dt>REPO_URL (erforderlich)</dt>
   <dd>Die URL des Repositorys, das hinzugefügt werden soll. Die URL des Repositorys muss das Protokoll (zum Beispiel 'http://plugins.ng.bluemix.net' anstatt 'plugins.ng.bluemix.net') enthalten. 'http://plugins.ng.bluemix.net' ist das offizielle Plug-in-Repository der Bluemix-CLI.</dd>
    </dl>


<strong>Beispiele</strong>:

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

<strong>Voraussetzungen</strong>: Keine

<strong>Befehlsoptionen:</strong>
   <dl>
   <dt>REPO_NAME (erforderlich)</dt>
   <dd>Der Name des Repositorys, das entfernt werden soll.</dd>
   </dl>

<strong>Beispiele</strong>:

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

<strong>Voraussetzungen</strong>: Keine

<strong>Befehlsoptionen:</strong>

   <dl>
   <dt>-r <i>REPO_NAME</i> (optional)</dt>
   <dd>Listet nur die Plug-ins im angegebenen Repository auf.</dd>
   </dl>

<strong>Beispiele</strong>:

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

<strong>Voraussetzungen</strong>: Keine


## bluemix plugin install
{: #bluemix_plugin_install}

Installiert die angegebene Version des Plug-ins in der {{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle aus dem angegebenen Pfad oder Repository.

```
bluemix plugin install PLUGIN_PATH|PLUGIN_NAME [-r REPO_NAME] [-v VERSION]
```

<strong>Voraussetzungen</strong>: Keine

<strong>Befehlsoptionen:</strong>

   <dl>
   <dt>PLUGIN_PATH|PLUGIN_NAME (erforderlich)</dt>
   <dd>Wenn -r <i>REPO_NAME</i> nicht angegeben wird, wird das Plug-in vom angegebenen lokalen Pfad oder der Remote URL installiert.</dd>
   <dt>-r <i>REPO_NAME</i> (optional)</dt>
   <dd>Der Name des Repositorys, in dem sich die Binärdatei des Plug-ins befindet.</dd>
   <dt>-v <i>VERSION</i> (optional)</dt>
   <dd>Die Version des Plug-ins, die installiert werden soll. Bei keiner Angabe wird die letzte Version des Plug-ins installiert. Diese Option ist nur gültig, wenn Sie das Plug-in aus dem Repository installieren.</dd>
    </dl>

<strong>Beispiele</strong>:

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

## bluemix plugin update
{: #bluemix_plugin_update}

Plug-in aus einem Repository aktualisieren.

```
bluemix plugin update -r REPO_NAME [PLUGIN NAME [-v VERSION]]
```

<strong>Voraussetzungen</strong>: Keine

<strong>Befehlsoptionen:</strong>
<dl>
 <dt>-r REPO_NAME (erforderlich)</dt>
 <dd>Der Name des Repositorys, in dem sich die Binärdatei des Plug-ins befindet.</dd>
 <dt><i>PLUGIN_NAME</i> (optional)</dt>
 <dd>Wenn nicht angegeben, werden alle Plug-ins, die in dem jeweiligen Repository zur Aktualisierung verfügbar sind, zur Auswahl aufgelistet.</dd>
 <dt>-v <i>VERSION</i> (optional)</dt>
 <dd>Die Version des Plug-ins, auf die aktualisiert werden soll. Wenn nicht angegeben, wird das Plug-in auf die neueste verfügbare Version aktualisiert.</dd>
</dl>

<strong>Beispiele</strong>:

Auf alle verfügbaren Upgrades im Plug-in-Repository "My-Repo" prüfen:

```
bluemix plugin update -r My-Repo
```

Upgrade für Plug-in "plugin-echo" im Repository "My-Repo" auf die neueste Version durchführen:

```
bluemix plugin update -r My-Repo plugin-echo
```

Plug-in "plugin-echo" im Repository "My-Repo" auf Version "1.0.1" aktualisieren:

```
bluemix plugin update -r My-Repo plugin-echo -v 1.0.1
```

## bluemix plugin uninstall
{: #bluemix_plugin_uninstall}

Deinstalliert das angegebene Plug-in in der Befehlszeilenschnittstelle von {{site.data.keyword.Bluemix_notm}}.

```
bluemix plugin uninstall PLUGIN_NAME
```

<strong>Voraussetzungen</strong>: Keine

<strong>Befehlsoptionen:</strong>

   <dl>
   <dt>PLUGIN_NAME (erforderlich)</dt>
   <dd>Der Name des Plug-ins, das deinstalliert werden soll.</dd>
    </dl>

<strong>Beispiele</strong>:

Plug-in `IBM-Containers` deinstallieren, das zuvor installiert wurde:

```
bluemix plugin uninstall IBM-Containers
```
