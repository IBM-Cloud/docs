---



copyright:

  years: 2015, 2017
lastupdated: "2017-02-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Einführung in die {{site.data.keyword.Bluemix_notm}}-CLI
{: #getting-started}

Die {{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle (CLI) stellt eine einheitliche Möglichkeit zur Interaktion mit Ihren Anwendungen, virtuellen Servern, Containern und weiteren Services über eine Befehlszeilenschnittstelle bereit. Mit der {{site.data.keyword.Bluemix_notm}}-CLI werden auch Community-Tools, wie die Cloud Foundry-CLI, die Docker-CLI und die OpenStack-CLI integriert und Umgebungseinstellungen initialisiert, mit denen Sie mit verschiedenen Berechnungstypen interagieren können.

**Einschränkung:** Die {{site.data.keyword.Bluemix_notm}}-CLI wird nicht von Cygwin unterstützt. Die {{site.data.keyword.Bluemix_notm}}-CLI darf daher nicht im Fenster mit der Cygwin-Befehlszeile verwendet werden.

**Hinweis:** Wenn sich in Ihrem Netz zwischen dem Host, auf dem die CLI ausgeführt wird, und {{site.data.keyword.Bluemix_notm}} ein HTTP-Proxy-Server befindet, müssen Sie den Hostnamen oder die IP-Adresse des Proxy-Servers in der Umgebungsvariablen HTTP_PROXY angeben.

## {{site.data.keyword.Bluemix_notm}}-CLI installieren
{: #install_bluemix_cli}

Installieren Sie vor der Installation der {{site.data.keyword.Bluemix_notm}}-CLI die [CF-CLI![Symbol für externen Link](../../../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli/releases){: new_window}.

Laden Sie unter Mac OS und Windows das [{{site.data.keyword.Bluemix_notm}}-CLI-Paket](/docs/cli/index.html#downloads) herunter und führen Sie anschließend das Installationsprogramm aus.

Führen Sie unter Linux die folgenden Schritte aus:

  1. Laden Sie das Paket herunter und extrahieren Sie es. Beispiel:

  ```
  ~$ tar -xvf Bluemix_CLI.tar.gz
  Bluemix_CLI/
  Bluemix_CLI/update_global_config
  Bluemix_CLI/install_bluemix_cli
  Bluemix_CLI/bx/
  Bluemix_CLI/bx/bash_autocomplete
  Bluemix_CLI/bx/zsh_autocomplete
  Bluemix_CLI/bin/
  Bluemix_CLI/bin/bluemix
  ~$
  ```

  2. Navigieren Sie in das Verzeichnis `Bluemix_CLI` und führen Sie den Befehl `./install_bluemix_cli` mit Rootberechtigung aus. Sie können den Befehl als Rootbenutzer ausführen oder den Befehl `sudo` verwenden, um die Rootberechtigung zu erhalten. Beispiel:

  ```
  ~# cd Bluemix_CLI
  ~/Bluemix_CLI# sudo ./install_bluemix_cli
  Superuser privileges are required to run this script.
  The Cloud Foundry CLI version 6.15 is already installed.
  Copying files...
  The Bluemix CLI installed successfully. To get started, open a new Linux terminal and enter "bluemix help", or enter "bx help" as short name.
  ~/Bluemix_CLI#
  ```

Sie können nun mit der Verwendung der {{site.data.keyword.Bluemix_notm}}-CLI beginnen oder weitere Plug-ins installieren.

## Plug-ins installieren
{: #install_plug-in}

Wie die Cloud Foundry-CLI unterstützt auch die {{site.data.keyword.Bluemix_notm}}-CLI ein Plug-in-Erweiterungsframework, mit dem über die bereits Befehle hinaus weitere Befehle integriert werden können.

Führen Sie die folgenden Schritte aus, um in Ihrer lokalen Umgebung ein Plug-in zu installieren:

  1. Laden Sie das Plug-in herunter. Beispiel:

  ```
  ~$ wget http://public.dhe.ibm.com/cloud/bluemix/cli/bluemix-plugins/auto-scaling-darwin-amd64.0.2.2--2016-02-18 14:02:12-- http://public.dhe.ibm.com/cloud/bluemix/cli/bluemix-plugins/auto-scaling-darwin-amd64.0.2.2
  Resolving public.dhe.ibm.com... 9.17.248.112
  Connection to public.dhe.ibm.com|9.17.248.112|:80... connected.
  HTTP request sent, awaiting response... 200 OK
  Length: 9857792 (9.4M) [text/plain]
  Saving to: 'auto-scaling-darwin-amd64-0.2.2'

  auto-scaling-darwin-0.2.2 100%[===================>] 9.40M 518KB/s in 22s

  2016-02-18 14:02:34 (443 KB/s) - `auto-scaling-darwin-amd64-0.2.2' saved [9857792/9857792]
  ```

  2. Auf UNIX-ähnlichen Systemen müssen Sie aus der heruntergeladenen Datei eine ausführbare Datei machen. Verwenden Sie hierfür den Befehl `chmod`. Beispiel:

  ```
  ~$ sudo chmod 755 auto-scaling-darwin-amd64-0.2.2
  Password:
  ~$
  ```

  3. Installieren Sie das Plug-in mit dem Befehl `bluemix plugin install`. Beispiel:

  ```
  ~$ bluemix plugin install ./auto-scaling-darwin-amd64-0.2.2
  Installing pluign './auto-scaling-darwin-amd64-0.2.2'...
  OK
  Plugin 'auto-scaling 0.2.2' was successfully installed.
  ~$
  ```

Führen Sie die folgenden Schritte aus, um die Installation von einem fernen Server aus durchzuführen:

  1. Installieren Sie das Plug-in über eine remote URL direkt mit dem Befehl `bluemix plugin install`. Beispiel:

  ```
  ~$ bluemix plugin install http://public.dhe.ibm.com/cloud/bluemix/cli/bluemix-plugins/auto-scaling-darwin-amd64-0.2.2
  Attempting to download the binary file...
  9857792 bytes downloaded
  Installing plugin '/var/folder/v7/l3hnkz0x0b9b5mf1fyxh7yw00000gn/T/BluemixFileDownload274645142/auto-scaling-darwin-adm64-0.2.2'...
  OK
  Plugin 'auto-scaling 0.2.2' was successfully installed.
  ~$
  ```

Sie können ein Plug-in auch über das Repository installieren. {{site.data.keyword.Bluemix_notm}} enthält Repositorys, in denen Plug-ins für die {{site.data.keyword.Bluemix_notm}}-CLI und die Cloud Foundry-CLI gehostet werden:

  * [Plug-in-Repository die für Cloud Foundry-CLI ](http://clis.ng.bluemix.net/ui/repository.html#cf-plugins){: new_window} ![Symbol für externen Link](../../../icons/launch-glyph.svg) - Diese Komponente hostet Plug-ins für die Cloud Foundry-CLI.
  * [Plug-in-Repository für die {{site.data.keyword.Bluemix_notm}}-CLI](http://clis.ng.bluemix.net/ui/repository.html#bluemix-plugins){: new_window} ![Symbol für externen Link](../../../icons/launch-glyph.svg) - Diese Komponente hostet Plug-ins speziell für die {{site.data.keyword.Bluemix_notm}}-CLI.

Führen Sie die folgenden Schritte aus, um die Installation vom Repository aus durchzuführen:

  1. Suchen Sie das Plug-in im Repository. Nach der Installation der {{site.data.keyword.Bluemix_notm}}-CLI wird standardmäßig das offizielle Repository `Bluemix` hinzugefügt. Sie können die Plug-ins im Repository `Bluemix` mit dem Befehl `bluemix plugin repo-plugins` auflisten. Beispiel:

  ```
  ~$ bluemix plugin repo-plugins -r Bluemix
  Getting plug-ins from repository 'Bluemix'...

  Repository: Bluemix
  Name           Description                                    Versions
  auto-scaling   Bluemix CLI plugin for Auto-Scaling service    0.2.1, 0.2.2
  nsg            Bluemix Network Security Group plugin          0.1.1

  ~$
  ```

  2. Installieren Sie das Plug-in über das `Bluemix`-Repository mit dem Befehl `bluemix plugin install`. Beispiel:

  ```
  ~$ bluemix plugin install auto-scaling -r Bluemix
  Looking up 'auto-scaling' from repository 'Bluemix'...
  9857792 bytes downloaded
  Installing plugin '/var/folder/v7/l3hnkz0x0b9b5mf1fyxh7yw00000gn/T/BluemixFileDownload062468676/auto-scaling-darwin-adm64-0.2.2'...
  OK
  Plugin 'auto-scaling 0.2.2' was successfully installed.
  ~$
  ```

## Bei der {{site.data.keyword.Bluemix_notm}}-CLI anmelden
{: #log_bmcli}

Nach der Installation der {{site.data.keyword.Bluemix_notm}}-CLI können Sie sich Ihrer IBMid und Ihrem Kennwort bei {{site.data.keyword.Bluemix_notm}} anmelden. Beispiel:

```
~$ bluemix login -a https://api.ng.bluemix.net
API endpoint: https://api.ng.bluemix.net

Email> demo_user@foo.com

Password>
Authenticating...
OK
```

Sie können nun die in {{site.data.keyword.Bluemix_notm}} integrierten Befehle verwenden. Beispiel: Führen Sie den Befehl `bluemix catalog templates` aus, um alle verfügbaren {{site.data.keyword.Bluemix_notm}}-Boilerplate-Vorlagen aufzulisten:

```
~$ bluemix catalog templates
Listing Bluemix boilerplate templates...

ID                      Name
pi-wdc-java-starter     Personality Insights Java Web Starter
xpages-starter          XPages Web Starter
mobileBackendStarter    Mobile Cloud
pi-wdc-nodejs-starter   Personality Insights Node.js Web Starter
mobileFirstPlatform     MobileFirst Services Starter
xspHelloWorld           IBM XPages
javacloudantbp          Java Cloudant Web Starter
```

# {{site.data.keyword.Bluemix_notm}}-Befehle (bx)
{: #bluemix_cli}

Version: 0.4.6

Von der {{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle (CLI) werden Befehle bereitgestellt, die nach Namensbereich für Benutzer zur Interaktion mit {{site.data.keyword.Bluemix_notm}} zusammengefasst sind. Bei einigen {{site.data.keyword.Bluemix_notm}}-Befehlen handelt es sich um Wrapper bereits vorhandener cf-Befehle, während andere Befehle die Funktionalität für {{site.data.keyword.Bluemix_notm}}-Benutzer erweitern. In der nachfolgenden Liste werden alle von der {{site.data.keyword.Bluemix_notm}}-CLI unterstützten Befehle mit Namen, Optionen, Nutzungen, Voraussetzungen, Beschreibungen und Beispielen aufgeführt.
{:shortdesc}

**Hinweis:** Unter *Voraussetzungen* wird aufgelistet, welche Aktionen vor der Verwendung des Befehls ausgeführt werden müssen. Für Befehle, für die keine Voraussetzungen erfüllt sein müssen, ist **Keine** angegeben. Andernfalls kann mindestens eine der folgenden Aktionen eine Voraussetzung sein:

<dl>
<dt>Endpunkt</dt>
<dd>Vor dem Verwenden des Befehls muss ein API-Endpunkt durch Absetzen des Befehls <code>bluemix api</code> definiert werden.</dd>
<dt>Anmeldung</dt>
<dd>Vor der Verwendung des Befehls ist die Anmeldung über den Befehl <code>bluemix login</code> erforderlich. Verwenden Sie beim Anmelden mit einer eingebundenen ID die Option '--sso' für die Anmeldung mit einmaligem Kenncode.</dd>
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
 <td>[bluemix help](index.html#bluemix_help)</td>
 <td>[bluemix api](index.html#bluemix_api)</td>
 <td>[bluemix_login](index.html#bluemix_login)</td>
 <td>[bluemix logout](index.html#bluemix_logout)</td>
 <td>[bluemix target](index.html#bluemix_target)</td>
 </tr>
 <tr>
 <td>[bluemix info](index.html#bluemix_info) </td>
 <td>[bluemix config](index.html#bluemix_config)</td>
 <td>[bluemix curl](index.html#bluemix_curl)</td>
 </tr>
  </tbody>
 </table>


<table summary="Bluemix-Befehle zur Verwaltung von Organisationen, Bereichen und Benutzern">
<caption>Tabelle 2. Befehle zur Verwaltung von Organisationen, Bereichen und Benutzern</caption>
 <thead>
 <th colspan="5">Befehle zur Verwaltung von Organisationen, Bereichen und Benutzern</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix iam orgs](index.html#bluemix_iam_orgs)</td>
 <td>[bluemix iam org](index.html#bluemix_iam_org)</td>
 <td>[bluemix iam org-create](index.html#bluemix_iam_org_create)</td>
 <td>[bluemix iam org-replicate](index.html#bluemix_iam_org_replicate)</td>
 <td>[bluemix iam org-rename](index.html#bluemix_iam_org_rename)</td>
 </tr>
 <tr>
 <td>[bluemix iam org-delete](index.html#bluemix_iam_org_delete)</td>
 <td>[bluemix iam spaces](index.html#bluemix_iam_spaces)</td>
 <td>[bluemix iam space](index.html#bluemix_iam_space)</td>
 <td>[bluemix iam space-create](index.html#bluemix_iam_space_create)</td>
 <td>[bluemix iam space-rename](index.html#bluemix_iam_space_rename)</td>
 </tr>
 <tr>
 <td>[bluemix iam space-delete](index.html#bluemix_iam_space_delete)</td>
 <td>[bluemix iam account-users](index.html#bluemix_iam_account_users)</td>
 <td>[bluemix iam account-users-delete](index.html#bluemix_iam_account_users_delete)</td>
 <td>[bluemix iam account-user-invite](index.html#bluemix_iam_account_user_invite)</td>
 <td>[bluemix iam account-user-reinvite](index.html#bluemix_iam_account_user_reinvite)</td>
 <td>[bluemix iam org-users](index.html#bluemix_iam_org_users)</td>
 </tr>
 <tr>
 <td>[bluemix iam org-user-add](index.html#bluemix_iam_org_user_add)</td>
 <td>[bluemix iam org-user-remove](index.html#bluemix_iam_org_user_remove)</td>
 <td>[bluemix iam org-role-set](index.html#bluemix_iam_org_role_set)</td>
 <td>[bluemix iam org-role-unset](index.html#bluemix_iam_org_role_unset)</td>
 <td>[bluemix iam space-users](index.html#bluemix_iam_space_users)</td>
 <td>[bluemix iam space-role-set](index.html#bluemix_iam_space_role_set)</td>
 </tr>
 <tr>
 <td>[bluemix iam space-role-unset](index.html#bluemix_iam_space_role_unset)</td>
 </tr>
 </tbody>
 </table>


<table summary="Bluemix-Befehle zur Verwaltung von Cloud Foundry-Apps">
<caption>Tabelle 3. Befehle zur Verwaltung von CF-Apps</caption>
 <thead>
 <th colspan="5">Befehle zur Verwaltung von CF-Apps</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix app push](index.html#bluemix_app_push)</td>
 <td>[bluemix app list](index.html#bluemix_app_list)</td>
 <td>[bluemix app show](index.html#bluemix_app_show)</td>
 <td>[bluemix app scale](index.html#bluemix_app_scale)</td>
 <td>[bluemix app delete](index.html#bluemix_app_delete)</td>
 </tr>
 <tr>
 <td>[bluemix app rename](index.html#bluemix_app_rename)</td>
 <td>[bluemix app start](index.html#bluemix_app_start)</td>
 <td>[bluemix app stop](index.html#bluemix_app_stop)</td>
 <td>[bluemix app restart](index.html#bluemix_app_restart)</td>
 <td>[bluemix app restage](index.html#bluemix_app_restage)</td>
 </tr>
 <tr>
 <td>[bluemix app instance-restart](index.html#bluemix_app_instance_restart)</td>
 <td>[bluemix app events](index.html#bluemix_app_events)</td>
 <td>[bluemix app files](index.html#bluemix_app_files)</td>
 <td>[bluemix app logs](index.html#bluemix_app_logs)</td>
 <td>[bluemix app env](index.html#bluemix_app_env)</td>
 </tr>
 <tr>
 <td>[bluemix app env-set](index.html#bluemix_app_env_set)</td>
 <td>[bluemix app env-unset](index.html#bluemix_app_env_unset)</td>
 <td>[bluemix app stacks](index.html#bluemix_app_stacks)</td>
 <td>[bluemix app stack](index.html#bluemix_app_stack)</td>
 <td>[bluemix app manifest-create](index.html#bluemix_app_manifest_create)</td>
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
 <td>[bluemix service offerings](index.html#bluemix_service_offerings)</td>
 <td>[bluemix service list](index.html#bluemix_service_list)</td>
 <td>[bluemix service show](index.html#bluemix_service_show)</td>
 <td>[bluemix service create](index.html#bluemix_service_create)</td>
 <td>[bluemix service update](index.html#bluemix_service_update)</td>
 </tr>
 <tr>
 <td>[bluemix service delete](index.html#bluemix_service_delete)</td>
 <td>[bluemix service rename](index.html#bluemix_service_rename)</td>
 <td>[bluemix service bind](index.html#bluemix_service_bind)</td>
 <td>[bluemix service unbind](index.html#bluemix_service_unbind)</td>
 <td>[bluemix service key-create](index.html#bluemix_service_key_create)</td>
 </tr>
 <tr>
 <td>[bluemix service key-delete](index.html#bluemix_service_key_delete)</td>
 <td>[bluemix service keys](index.html#bluemix_service_keys)</td>
 <td>[bluemix service key-show](index.html#bluemix_service_key_show)</td>
 <td>[bluemix service user-provided-create](index.html#bluemix_service_user_provided_create)</td>
 <td>[bluemix service user-provided-update](index.html#bluemix_service_user_provided_update)</td>
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
 <td>[bluemix catalog templates](index.html#bluemix_catalog_templates)</td>
 <td>[bluemix catalog template](index.html#bluemix_catalog_template)</td>
 <td>[bluemix catalog template-run](index.html#bluemix_catalog_template_run)</td>
 <td>[bluemix plugin repos](index.html#bluemix_plugin_repos)</td>
 <td>[bluemix plugin repo-add](index.html#bluemix_plugin_repo_add)</td>
 </tr>
 <tr>
 <td>[bluemix plugin repo-remove](index.html#bluemix_plugin_repo_remove)</td>
 <td>[bluemix plugin repo-plugins](index.html#bluemix_plugin_repo_plugins)</td>
 <td>[bluemix plugin list](index.html#bluemix_plugin_list)</td>
 <td>[bluemix plugin install](index.html#bluemix_plugin_install)</td>
 <td>[bluemix plugin uninstall](index.html#bluemix_plugin_uninstall)</td>
 </tr>
 <tr>
 <td>[bluemix bss account-usage](index.html#bluemix_bss_account_usage)</td>
 <td>[bluemix bss org-usage](index.html#bluemix_bss_org_usage)</td>
 <td>[bluemix bss orgs-usage-summary](index.html#bluemix_orgs_usage_summary)</td>
 <td>[bluemix security cert](index.html#bluemix_security_cert)</td>
 <td>[bluemix security cert-add](index.html#bluemix_security_cert_add)</td>
 </tr>
 <tr>
 <td>[bluemix security cert-remove](index.html#bluemix_security_cert_remove)</td>
 <td></td>
 <td></td>
 </tr>
  </tbody>
 </table>


<table summary="Bluemix-Befehle zur Verwaltung von Netzeinstellungen">
<caption>Tabelle 6. Befehle zur Verwaltung von Netzeinstellungen</caption>
 <thead>
 <th colspan="5">Befehle zur Verwaltung von Netzeinstellungen</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix network regions](index.html#bluemix_network_regions)</td>
 <td>[bluemix network region-set](index.html#bluemix_network_region_set)</td>
 <td>[bluemix network routes](index.html#bluemix_network_routes)</td>
 <td>[bluemix network route-check](index.html#bluemix_network_route_check)</td>
 <td>[bluemix network route-map](index.html#bluemix_network_route_map)</td>
 </tr>
 <tr>
 <td>[bluemix network route-unmap](index.html#bluemix_network_route_unmap)</td>
 <td>[bluemix network route-create](index.html#bluemix_network_route_create)</td>
 <td>[bluemix network route-delete](index.html#bluemix_network_route_delete)</td>
 <td>[bluemix network orphaned-routes-delete](index.html#bluemix_network_orphaned_routes_delete)</td>
 <td>[bluemix network domains](index.html#bluemix_network_domains)</td>
 </tr>
 <tr>
 <td>[bluemix network domain-create](index.html#bluemix_network_domain_create)</td>
 <td>[bluemix network domain-delete](index.html#bluemix_network_domain_delete)</td>
 <td>[bluemix network shared-domain-create](index.html#bluemix_network_shared_domain_create)</td>
 <td>[bluemix network shared-domain-delete](index.html#bluemix_network_shared_domain_delete)</td>
 <td></td>
 </tr>
  </tbody>
 </table>



### bluemix help
{: #bluemix_help}
Zeigt die erweiterte Hilfe für integrierte Befehle und unterstützte Namensbereiche der obersten Ebene in der {{site.data.keyword.Bluemix_notm}}-CLI oder die Hilfe für einen bestimmten integrierten Befehl oder Namensbereich an.

```
bluemix help [COMMAND|NAMESPACE]
```

<strong>Voraussetzungen</strong>: Keine

<strong>Befehlsoptionen</strong>:

   <dl>
   <dt>COMMAND|NAMESPACE (optional)</dt>
   <dd>Der Befehl oder Namensbereich, für den die Hilfe angezeigt wird. Wenn nichts angegeben ist, wird die erweiterte Hilfe für die {{site.data.keyword.Bluemix_notm}}-CLI angezeigt.</dd>
   </dl>



<strong>Beispiele</strong>:

Erweiterte Hilfe für die {{site.data.keyword.Bluemix_notm}}-CLI anzeigen:

```
bluemix help
```

Hilfe für Befehl `info` anzeigen:

```
bluemix help info
```



### bluemix api
{: #bluemix_api}
{{site.data.keyword.Bluemix_notm}}-API-Endpunkt festlegen oder anzeigen. Dieser Befehl schließt den Befehl `cf api` ein.

```
bluemix api [API_ENDPOINT] [--unset]
```

<strong>Voraussetzungen</strong>: Keine

<strong>Befehlsoptionen</strong>:
   <dl>
   <dt>API_ENDPOINT (optional)</dt>
   <dd>Der API-Endpunkt, der als Ziel verwendet wird, zum Beispiel `https://api.chinabluemix.net`. Wenn weder die Option *API_ENDPOINT* noch die Option `--unset` angegeben wird, wird der aktuelle API-Endpunkt angezeigt.</dd>
   <dt>--unset (optional)</dt>
   <dd>Entfernt die Einstellung für den API-Endpunkt.</dd>
    </dl>
<strong>Beispiele</strong>:

Für den API-Endpunkt api.chinabluemix.net festlegen:

```
bluemix api api.chinabluemix.net
```

Aktuellen API-Endpunkt anzeigen:

```
bluemix api
```

Definition für den API-Endpunkt rückgängig machen:

```
bluemix api --unset
```


### bluemix login
{: #bluemix_login}

Anmeldung des Benutzers. Dieser Befehl schließt den Befehl `cf login` ein. Die Befehlsoption sind dieselben wie die für den Befehl `cf login`.

```
bluemix login [OPTIONS...]
```

<strong>Voraussetzungen</strong>: Endpunkt

<!-- staging comment for Atlas 45: might need prereq for federated ID/SSO option unless we expect them to just view the details from the cf login command -->

<strong>Befehlsoptionen</strong>: Informationen zu den Optionen, die vom Befehl `login` unterstützt werden, finden Sie in den Informationen zur Verwendung des Befehls `cf login` für cf-Befehle zur Verwaltung von Anwendungen.

<strong>Hinweis:</strong> Verwenden Sie beim Anmelden mit einer eingebundenen ID die Option '--sso' für die Anmeldung mit einmaligem Kenncode.

### bluemix logout
{: #bluemix_logout}

Abmeldung des Benutzers. Dieser Befehl schließt den Befehl `cf logout` ein.

```
bluemix logout
```

<strong>Voraussetzungen</strong>: Keine


### bluemix target
{: #bluemix_target}


Zielorganisation oder Zielbereich festlegen oder anzeigen. Dieser Befehl schließt den Befehl `cf target` ein.

```
bluemix target [-o ORG_NAME] [-s SPACE_NAME]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen</strong>:
   <dl>
   <dt>-o <i>ORG_NAME</i> (optional)</dt>
   <dd>Der Name der Zielorganisation.</dd>
   <dt>-s <i>SPACE_NAME</i> (optional)</dt>
   <dd>Der Name des Zielbereichs.</dd>
   </dl>
Wenn weder -o *ORG_NAME* noch -s *SPACE_NAME* angegeben wird, werden die aktuelle Organisation und der aktuelle Bereich angezeigt.
<strong>Beispiele</strong>:

`MyOrg` als aktuelle Organisation und `MySpace` als aktuellen Bereich definieren:

```
bluemix target -o MyOrg -s MySpace
```

Aktuelle Organisation und aktuellen Bereich anzeigen:

```
bluemix target
```


### bluemix info
{: #bluemix_info}

{{site.data.keyword.Bluemix_notm}}-Basisinformationen einschließlich aktueller Region, Cloud-Controller-Version und einigen nützlichen Endpunkten (zum Beispiel zum Anmelden und Austauschen von Zugriffstoken) anzeigen.

```
bluemix info
```

<strong>Voraussetzungen</strong>: Endpunkt


### bluemix config
{: #bluemix_config}


Schreibt Standardwerte in die Konfigurationsdatei.

```
bluemix config --http-timeout TIMEOUT_IN_SECONDS | --trace (true|false|path/to/file) | --color (true|false) | --locale (LOCALE|CLEAR) | --check-version (true|false)
```

<strong>Voraussetzungen</strong>: Keine

<strong>Befehlsoptionen</strong>:
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

Nur eine dieser Optionen kann gleichzeitig angegeben werden.

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


### bluemix curl
{: #bluemix_curl}

Ausführung einer unformatierten HTTP-Anforderung für {{site.data.keyword.Bluemix_notm}}. *Content-Type* ist standardmäßig auf *application/json* eingestellt. Dieser Befehl sendet die Anforderung an {{site.data.keyword.Bluemix_notm}} Multi-Cloud Control Proxy. Informationen zu den unterstützten Pfaden finden Sie in den API-Pfaddefinitionen im [CloudFoundry-API-Dokument ](http://apidocs.cloudfoundry.org/){: new_window} ![Symbol für externen Link](../../../icons/launch-glyph.svg).

```
bluemix curl PATH [OPTIONS...]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen</strong>:
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


### bluemix iam orgs
{: #bluemix_iam_orgs}

Alle Organisationen auflisten

```
bluemix iam orgs [-r REGION --guid]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen</strong>:
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

### bluemix iam org
{: #bluemix_iam_org}

Die Informationen für die angegebene Organisation anzeigen

```
bluemix iam org ORG_NAME [--guid]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen</strong>:
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

### bluemix iam org-create
{: #bluemix_iam_org_create}

Eine neue Organisation erstellen. Diese Operation kann nur vom Kontoeigner ausgeführt werden.

```
bluemix iam org-create ORG_NAME
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen</strong>:
   <dl>
   <dt>ORG_NAME (erforderlich)</dt>
   <dd>Der Name der Organisation, die erstellt wird.</dd>
   </dl>

<strong>Beispiele</strong>:

Organisation mit dem Namen `IBM` erstellen

```
bluemix iam org-create IBM
```


### bluemix iam org-replicate
{: #bluemix_iam_org_replicate}

Repliziert eine Organisation aus der aktuellen Region in eine andere Region.

```
bluemix iam org-replicate ORG_NAME REGION_NAME
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen</strong>:
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


### bluemix iam org-rename
{: #bluemix_iam_org_rename}

Eine Organisation umbenennen. Diese Operation kann nur von einem Organisationsmanager ausgeführt werden.

```
bluemix iam org-rename OLD_ORG_NAME NEW_ORG_NAME
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen</strong>:
   <dl>
   <dt>OLD_ORG_NAME (erforderlich)</dt>
   <dd>Der bisherige Name der Organisation, die umbenannt werden soll.</dd>
   <dt>NEW_ORG_NAME (erforderlich)</dt>
   <dd>Der neue Name für die Organisation, die umbenannt werden soll.</dd>
   </dl>

### bluemix iam org-delete
{: #bluemix_iam_org_delete}

Die angegebene Organisation in der aktuellen Region löschen.

```
bluemix iam org-delete ORG_NAME [-f --all]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen</strong>:
   <dl>
   <dt>ORG_NAME (erforderlich)</dt>
   <dd>Der Name der vorhandenen Organisation, die gelöscht werden soll.</dd>
   <dt>-f (optional)</dt>
   <dd>Löschung ohne Bestätigung erzwingen.</dd>
   <dt>--all (optional)</dt>
   <dd>Die Organisation in allen Regionen löschen.</dd>
   </dl>


### bluemix iam spaces
{: #bluemix_iam_spaces}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf spaces`.


### bluemix iam space
{: #bluemix_iam_space}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf space`.


### bluemix iam space-create
{: #bluemix_iam_space_create}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf create-space`.


### bluemix iam space-rename
{: #bluemix_iam_space_rename}


Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf rename-space`.


### bluemix iam space-delete
{: #bluemix_iam_space_delete}


Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf delete-space`.


### bluemix iam account-users
{: #bluemix_iam_account_users}

Dem Konto zugeordnete Benutzer anzeigen. Diese Operation kann nur vom Kontoeigner ausgeführt werden.

```
bluemix iam account-users
```

### bluemix iam account-user-invite
{: #bluemix_iam_account_user_invite}


Lädt den Benutzer zu dem Konto mit bereits festgelegter Organisation und Bereichsrolle ein. Diese Operation kann nur vom Kontoeigner ausgeführt werden.

```
bluemix iam account-user-invite USER_NAME ORG_NAME ORG_ROLE SPACE_NAME SPACE_ROLE
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung


<strong>Befehlsoptionen</strong>:

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


### bluemix iam account-user-reinvite
{: #bluemix_iam_account_user_reinvite}

Einladung erneut an einen Benutzer senden (Organisationsmanager oder Kontoeigner erforderlich)
```
 bluemix iam account-user-reinvite USER_EMAIL ORG_NAME
```


### bluemix iam org-users
{: #bluemix_iam_org_users}

Benutzer in der angegebenen Organisation nach Rolle anzeigen

```
bluemix iam org-users ORG_NAME [-a]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen</strong>:
   <dl>
   <dt>ORG_NAME (erforderlich)</dt>
   <dd>Der Name der Organisation.</dd>
   <dt>-a (optional)</dt>
   <dd>Alle Benutzer in der angegebenen Organisation auflisten (nicht nach Rolle gruppiert).</dd>
    </dl>

### bluemix iam org-user-add
{: #bluemix_iam_org_user_add}

Benutzer zur Organisation hinzufügen (Organisationsmanager erforderlich).
```
 bluemix iam org-user-add USER_NAME ORG
```

### bluemix iam org-user-remove
{: #bluemix_iam_org_user_remove}

Benutzer aus Organisation entfernen (Organisationsmanager oder nur Benutzer selbst)
```
   bluemix iam org-user-remove USER_NAME ORG [-f, --force]
```

<strong>Befehlsoptionen</strong>:
  <dl>
   <dt>--force, -f</dt>
   <dd>Löschung ohne Bestätigung erzwingen.</dd>
 </dl>

### bluemix iam org-role-set
{: #bluemix_iam_org_role_set}

Einem Benutzer eine Organisationsrolle zuweisen. Diese Operation kann nur von einem Organisationsmanager ausgeführt werden.

```
bluemix iam org-role-set USER_NAME ORG_NAME ORG_ROLE
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen</strong>:
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


### bluemix iam org-role-unset
{: #bluemix_iam_org_role_unset}

Eine Organisationsrolle für einen Benutzer entfernen (widerrufen). Diese Operation kann nur von einem Organisationsmanager ausgeführt werden.

```
bluemix iam org-role-unset USER_NAME ORG_NAME ORG_ROLE
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen</strong>:
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


### bluemix iam space-users
{: #bluemix_iam_space_users}

Benutzer in dem angegebenen Bereich nach Rolle anzeigen

```
bluemix iam space-users ORG_NAME SPACE_NAME
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen</strong>:
   <dl>
   <dt>ORG_NAME (erforderlich)</dt>
   <dd>Der Name der Organisation.</dd>
   <dt>SPACE_NAME (erforderlich)</dt>
   <dd>Der Name des Bereichs.</dd>
   </dl>


### bluemix iam space-role-set
{: #bluemix_iam_space_role_set}

Einem Benutzer eine Bereichsrolle zuweisen. Diese Operation kann nur von einem Bereichsmanager ausgeführt werden.

```
bluemix iam space-role-set USER_NAME ORG_NAME SPACE_NAME SPACE_ROLE
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen</strong>:

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

### bluemix iam space-role-unset
{: #bluemix_iam_space_role_unset}

Eine Bereichsrolle für einen Benutzer entfernen (widerrufen). Diese Operation kann nur von einem Bereichsmanager ausgeführt werden.

```
bluemix iam space-role-unset USER_NAME ORG_NAME SPACE_NAME SPACE_ROLE
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen</strong>:

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


### bluemix app push
{: #bluemix_app_push}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf push`.


### bluemix app list
{: #bluemix_app_list}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf apps`.


### bluemix app show
{: #bluemix_app_show}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf app`.


### bluemix app scale
{: #bluemix_app_scale}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf scale`.


### bluemix app delete
{: #bluemix_app_delete}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf delete`.


### bluemix app rename
{: #bluemix_app_rename}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf rename`.


### bluemix app start
{: #bluemix_app_start}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf start`.


### bluemix app stop
{: #bluemix_app_stop}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf stop`.


### bluemix app restart
{: #bluemix_app_restart}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf restart`.


### bluemix app restage
{: #bluemix_app_restage}


Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf restage`.


### bluemix app instance-restart
{: #bluemix_app_instance_restart}


Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf restart-app-instance`.


### bluemix app events
{: #bluemix_app_events}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf events`.


### bluemix app files
{: #bluemix_app_files}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf files`.


### bluemix app logs
{: #bluemix_app_logs}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf logs`.


### bluemix app env
{: #bluemix_app_env}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf env`.


### bluemix app env-set
{: #bluemix_app_env_set}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf set-env`.


### bluemix app env-unset
{: #bluemix_app_env_unset}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf unset-env`.


### bluemix app stacks
{: #bluemix_app_stacks}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf stacks`.


### bluemix app stack
{: #bluemix_app_stack}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf stack`.


### bluemix app manifest-create
{: #bluemix_app_manifest_create}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf create-app-manifest`.


### bluemix service offerings
{: #bluemix_service_offerings}


Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf marketplace`.


### bluemix service list
{: #bluemix_service_list}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf services`.


### bluemix service show
{: #bluemix_service_show}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf service`.


### bluemix service create
{: #bluemix_service_create}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf create-service`.


### bluemix service update
{: #bluemix_service_update}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf update-service`.


### bluemix service delete
{: #bluemix_service_delete}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf delete-service`.


### bluemix service rename
{: #bluemix_service_rename}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf rename-service`.


### bluemix service bind
{: #bluemix_service_bind}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf bind-service`.


### bluemix service unbind
{: #bluemix_service_unbind}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf unbind-service`.


### bluemix service key-create
{: #bluemix_service_key_create}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf create-service-key`.


### bluemix service key-delete
{: #bluemix_service_key_delete}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf delete-service-key`.


### bluemix service keys
{: #bluemix_service_keys}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf service-keys`.


### bluemix service key-show
{: #bluemix_service_key_show}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf service-key`.


### bluemix service user-provided-create
{: #bluemix_service_user_provided_create}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf create-user-provided-service`.


### bluemix service user-provided-update
{: #bluemix_service_user_provided_update}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf update-user-provided-service`.


### bluemix catalog templates
{: #bluemix_catalog_templates}

Zeigt die Boilerplate-Vorlagen in Bluemix an.

```
bluemix catalog templates [-d]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen</strong>:

   <dl>
   <dt>-d (optional)</dt>
   <dd>Wenn die Option <i>-d</i> angegeben wird, wird auch die Beschreibung jeder Vorlage angezeigt. Andernfalls werden nur die ID und der Name jeder Vorlage angezeigt.</dd>
   </dl>


### bluemix catalog template
{: #bluemix_catalog_template}

Zeigt die detaillierten Informationen einer angegebenen Boilerplate-Vorlage an.

```
bluemix catalog template TEMPLATE_ID
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen</strong>:
   <dl>
   <dt>TEMPLATE_ID (erforderlich)</dt>
   <dd>Die ID der Boilerplate-Vorlage. Verwenden Sie <i>bluemix templates</i>, um die IDs aller Vorlagen anzuzeigen.</dd>
   </dl>


<strong>Beispiele</strong>:

Details der Vorlage `mobileBackendStarter` anzeigen:

```
bluemix catalog template mobileBackendStarter
```


### bluemix catalog template-run
{: #bluemix_catalog_template_run}

Erstellt eine cf-Anwendung, die auf der angegebenen Vorlage mit der angegebenen URL und Beschreibung basiert. Die neue App wird standardmäßig automatisch gestartet.

```
bluemix catalog template-run TEMPLATE_ID CF_APP_NAME [-u URL] [-d DESCRIPTION] [--no-start]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel

<strong>Befehlsoptionen</strong>:
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


### bluemix network regions
{: #bluemix_network_regions}

Zeigt die Informationen für alle Regionen in {{site.data.keyword.Bluemix_notm}} an.

```
bluemix network regions
```

<strong>Voraussetzungen</strong>: Endpunkt


### bluemix network region-set
{: #bluemix_network_region_set}

Wechselt zur angegebenen Region. Von diesem Befehl wird automatisch auf dieselbe Organisation und denselben Bereich in der neuen Region zurückverwiesen (sofern möglich). Andernfalls wird der Benutzer durch den Befehl aufgefordert, eine neue Organisation und einen neuen Bereich auszuwählen, wenn der Benutzer bereits angemeldet ist. Der API-Endpunkt wird entsprechend geändert.

```
bluemix network region-set REGION_NAME
```

<strong>Voraussetzungen</strong>: Endpunkt

<strong>Befehlsoptionen</strong>:

   <dl>
   <dt>REGION_NAME (erforderlich)</dt>
   <dd>Der Name der Region, zu der Sie wechseln möchten. Mit dem Befehl <i>bluemix network regions</i> können Sie alle Regionsnamen anzeigen.</dd>
    </dl>

<strong>Beispiele</strong>:

Als aktuelle Region `eu-gb` festlegen:

```
bluemix network region-set eu-gb
```


### bluemix network routes
{: #bluemix_network_routes}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf routes`.


### bluemix network route-check
{: #bluemix_network_route_check}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf check-route`.


### bluemix network route-map
{: #bluemix_network_route_map}

Ordnet eine Route einer vorhandenen cf-Anwendung oder -Containergruppe zu, die über die angegebene Domäne oder den angegebenen Hostnamen verfügt.

```
bluemix network route-map CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel

<strong>Befehlsoptionen</strong>:

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
bluemix network route-map my-app mychinabluemix.net
```

Route zu 'my-container-group' mit angegebener Domäne und angegebenem Hostnamen zuordnen:

```
bluemix network route-map my-container-group chinabluemix.net -n abc
```


### bluemix network route-unmap
{: #bluemix_network_route_unmap}

Entfernt die Zuordnung der angegebenen Route von einer vorhandene cf-Anwendung oder -Containergruppe.

```
bluemix network route-unmap CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel

<strong>Befehlsoptionen</strong>:

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
bluemix network route-unmap my-app mychianbluemix.net
```

Zuordnung von `abc.chinabluexmix.net` zu `my-container-group` aufheben:

```
bluemix network route-unmap my-container-group chinabluemix.net -n abc
```


### bluemix network route-create
{: #bluemix_network_route_create}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf create-route`.


### bluemix network route-delete
{: #bluemix_network_route_delete}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf delete-route`.


### bluemix network orphaned-routes-delete
{: #bluemix_network_orphaned_routes_delete}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf delete-orphaned-routes`.


### bluemix network domains
{: #bluemix_network_domains}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf domains`.


### bluemix network domain-create
{: #bluemix_network_domain_create}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf create-domain`.


### bluemix network domain-delete
{: #bluemix_network_domain_delete}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf delete-domain`.


### bluemix network shared-domain-create
{: #bluemix_network_shared_domain_create}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf create-shared-domain`.


### bluemix network shared-domain-delete
{: #bluemix_network_shared_domain_delete}

Dieser Befehl besitzt dieselbe Funktion und dieselben Optionen wie der Befehl `cf delete-shared-domain`.



### bluemix bss account-usage
{: #bluemix_bss_account_usage}

Monatliche Nutzung und Kosten des Kontos anzeigen.

```
bluemix bss account-usage [-d YYYY-MM] [--json]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen</strong>:

<dl>
  <dt>-d MONTH_DATE (optional)</dt>
  <dd>Daten für Monat und Datum durch Angeben des Formats JJJJ-MM anzeigen. Bei keiner Angabe wird die Nutzung des aktuellen Monats angezeigt.</dd>
  <dt>--json (optional)</dt>
  <dd>Nutzungsergebnis im JSON-Format anzeigen.</dd>
</dl>

<strong>Beispiele</strong>:

Nutzungs- und Kostenbericht des Kontos für 06/2016 anzeigen:

```
bluemix bss account-usage -d 2016-06
```

### bluemix bss org-usage
{: #bluemix_bss_org_usage}

Monatliche Nutzungsdetails einer Organisation anzeigen. Diese Operation kann nur von einem Abrechnungsmanager der Organisation ausgeführt werden.

```
bluemix bss org-usage ORG_NAME [-d YYYY-MM] [-r REGION_NAME] [--json]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen</strong>:

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



### bluemix bss orgs-usage-summary
{: #bluemix_bss_orgs_usage_summary}

Zusammenfassung der monatlichen Nutzung für die Organisationen im eigenen Konto anzeigen.

```
bluemix bss orgs-usage-summary [-d YYYY-MM] [-r REGION_NAME] [--json]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen</strong>:

<dl>
  <dt>-d MONTH_DATE (optional)</dt>
  <dd>Daten für Monat und Datum durch Angeben des Formats JJJJ-MM anzeigen. Bei keiner Angabe wird die Nutzung des aktuellen Monats angezeigt.</dd>
  <dt>-r REGION_NAME</dt>
  <dd>Name der Region, in der die Organisationen gehostet werden. Wenn 'Alle' eingestellt ist, wird eine Nutzungszusammenfassung der Organisationen in allen Regionen angezeigt.</dd>
  <dt>--json (optional)</dt>
  <dd>Nutzungsergebnis im JSON-Format anzeigen.</dd>
</dl>



### bluemix security cert
{: #bluemix_security_cert}

Die Zertifikatsinformationen für eine Domäne auflisten

```
bluemix security cert DOMAIN_NAME
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung

<strong>Befehlsoptionen</strong>:

   <dl>
   <dt>DOMAIN_NAME (erforderlich)</dt>
   <dd>Die Domäne, in der das Zertifikat gehostet wird.</dd>
   </dl>



<strong>Beispiele</strong>:

Die Zertifikatsinformationen für die Domäne `ibmcxo-eventconnect.com` anzeigen:

```
bluemix security cert ibmcxo-eventconnect.com
```


### bluemix security cert-add
{: #bluemix_security_cert_add}

Fügt der angegebenen Domäne in der aktuellen Organisation ein Zertifikat hinzu.

```
bluemix security cert-add DOMAIN -k PRIVATE_KEY_FILE -c CERT_FILE [-p PASSWORD] [-i INTERMEDIATE_CERT_FILE] [--verify-client]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel

<strong>Befehlsoptionen</strong>:
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
   <dt>--verify-client (optional)</dt>
   <dd>Gibt an, ob die Clientzertifikatsprüfung aktiviert werden soll.</dd>
   </dl>


<strong>Beispiele</strong>:

Zertifikat der Domäne `ibmcxo-eventconnect.com` hinzufügen:

```
bluemix security cert-add ibmcxo-eventconnect.com -k key_file.key -c cert_file.crt -p 123 -i inter_cert.cert
```


### bluemix security cert-remove
{: #bluemix_security_cert_remove}

Entfernt ein Zertifikat aus der angegebenen Domäne in der aktuellen Organisation.

```
bluemix security cert-remove DOMAIN [-f]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel

<strong>Befehlsoptionen</strong>:

   <dl>
   <dt>DOMAIN (erforderlich)</dt>
   <dd>Die Domäne, aus der das Zertifikat entfernt werden soll.</dd>
   <dt>-f  (optional)</dt>
   <dd>Löschung ohne Bestätigung erzwingen.</dd>
   </dl>



### bluemix plugin repos
{: #bluemix_plugin_repos}

Listet alle Plug-in-Repositorys auf, die in der Befehlszeilenschnittstelle von {{site.data.keyword.Bluemix_notm}} registriert sind.

```
bluemix plugin repos
```

<strong>Voraussetzungen</strong>: Keine


### bluemix plugin repo-add
{: #bluemix_plugin_repo_add}

Fügt ein neues Plug-in-Repository zur Befehlszeilenschnittstelle von {{site.data.keyword.Bluemix_notm}} hinzu.

```
bluemix plugin repo-add REPO_NAME REPO_URL
```

<strong>Voraussetzungen</strong>: Keine

<strong>Befehlsoptionen</strong>:

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


### bluemix plugin repo-remove
{: #bluemix_plugin_repo_remove}

Entfernt ein Plug-in-Repository aus der {{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle.

```
bluemix plugin repo-remove REPO_NAME
```

<strong>Voraussetzungen</strong>: Keine

<strong>Befehlsoptionen</strong>:
   <dl>
   <dt>REPO_NAME (erforderlich)</dt>
   <dd>Der Name des Repositorys, das entfernt werden soll.</dd>
   </dl>

<strong>Beispiele</strong>:

Repository `bluemix-repo` aus der Befehlszeilenschnittstelle von {{site.data.keyword.Bluemix_notm}} entfernen:

```
bluemix plugin repo-remove bluemix-repo
```


### bluemix plugin repo-plugins
{: #bluemix_plugin_repo_plugins}

Listet alle verfügbaren Plug-ins in allen hinzugefügten Repositorys oder einem bestimmten Repository auf.

```
bluemix plugin repo-plugins [-r REPO_NAME]
```

<strong>Voraussetzungen</strong>: Keine

<strong>Befehlsoptionen</strong>:

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


### bluemix plugin list
{: #bluemix_plugin_list}

Listet alle in der Befehlszeilenschnittstelle von {{site.data.keyword.Bluemix_notm}} installierten Plug-ins auf.

```
bluemix plugin list
```

<strong>Voraussetzungen</strong>: Keine


### bluemix plugin install
{: #bluemix_plugin_install}

Installiert die angegebene Version des Plug-ins in der {{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle aus dem angegebenen Pfad oder Repository.

```
bluemix plugin install PLUGIN_PATH|PLUGIN_NAME [-r REPO_NAME] [-v VERSION]
```

<strong>Voraussetzungen</strong>: Keine

<strong>Befehlsoptionen</strong>:

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

Plug-in `container-service` der letzten Version aus dem Repository `bluemix-repo` installieren: 

```
bluemix plugin install container-service -r bluemix-repo
```
Plug-in `container-service` mit der Version `0.5.800` aus dem Repository `bluemix-repo` installieren:

```
bluemix plugin install container-service -r bluemix-repo -v 0.1.217
```






### bluemix plugin uninstall
{: #bluemix_plugin_uninstall}

Deinstalliert das angegebene Plug-in in der Befehlszeilenschnittstelle von {{site.data.keyword.Bluemix_notm}}.

```
bluemix plugin uninstall PLUGIN_NAME
```

<strong>Voraussetzungen</strong>: Keine

<strong>Befehlsoptionen</strong>:

   <dl>
   <dt>PLUGIN_NAME (erforderlich)</dt>
   <dd>Der Name des Plug-ins, das deinstalliert werden soll.</dd>
    </dl>

<strong>Beispiele</strong>:

Plug-in `container-service` deinstallieren, das vorher installiert wurde: 

```
bluemix plugin uninstall container-service
```



# Zugehörige Links
{: #rellinks}

## Zugehörige Links
{: #general}

* [bx tool ](http://clis.ng.bluemix.net/ui/home.html){: new_window} ![Symbol für externen Link](../../../icons/launch-glyph.svg)
