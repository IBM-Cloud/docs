---

copyright:

  years: 2015, 2017

lastupdated: "2017-01-12"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix_notm}}-Administrator-CLI
{: #bluemixadmincli}


Sie können Ihre {{site.data.keyword.Bluemix_notm}} Local- oder {{site.data.keyword.Bluemix_notm}} Dedicated-Umgebung über die Cloud
Foundry-Befehlszeilenschnittstelle mit dem {{site.data.keyword.Bluemix_notm}}-Administrator-CLI-Plug-in verwalten. Sie können Benutzer zum Beispiel aus einer LDAP-Registry
hinzufügen. Informationen zur Zuordnung Ihres {{site.data.keyword.Bluemix_notm}} Public-Kontos finden Sie unter [Verwalten](/docs/admin/adminpublic.html#administer).

Vor dem Beginn müssen Sie die Befehlszeilenschnittstelle 'cf' installieren. Für das
{{site.data.keyword.Bluemix_notm}}-Administrator-CLI-Plug-in
ist cf Version 6.11.2 oder höher erforderlich. [Cloud Foundry-Befehlszeilenschnittstelle herunterladen![Symbol für externen Link](../../../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli/releases){: new_window}

**Einschränkung:** Die
Cloud Foundry-Befehlszeilenschnittstelle wird nicht von Cygwin unterstützt. Verwenden Sie
die Cloud Foundry-Befehlszeilenschnittstelle in einem
Befehlszeilenfenster, das sich von dem Befehlszeilenfenster von Cygwin unterscheidet.

**Hinweis:** Die {{site.data.keyword.Bluemix_notm}}-Administrator-CLI wird nur für die Umgebungen {{site.data.keyword.Bluemix_notm}} Local und {{site.data.keyword.Bluemix_notm}} Dedicated verwendet. Von {{site.data.keyword.Bluemix_notm}} Public wird sie nicht unterstützt.

## {{site.data.keyword.Bluemix_notm}}-Administrator-CLI-Plug-in hinzufügen

Nach der Installation der Befehlszeilenschnittstelle 'cf' können Sie das
{{site.data.keyword.Bluemix_notm}}-Administrator-CLI-Plug-in
hinzufügen.

**Hinweis:** Wenn Sie das {{site.data.keyword.Bluemix_notm}}-Administrator-Plug-in zuvor installiert haben, müssen Sie das Plug-in möglicherweise deinstallieren, das Repository löschen und anschließend das Plug-in erneut installieren, um die neuesten Aktualisierungen zu erhalten.

Führen Sie die folgenden Schritte aus, um das Repository hinzuzufügen und das Plug-in zu installieren:

<ol>
<li>Führen Sie zum Hinzufügen des {{site.data.keyword.Bluemix_notm}}-Administrator-Plug-in-Repositorys den folgenden Befehl aus:<br/><br/>
<code>
cf add-plugin-repo BluemixAdmin https://console.&lt;subdomain&gt;.bluemix.net/cli
</code><br/><br/>
<dl class="parml">
<dt class="pt dlterm">&lt;subdomain&gt;</dt>
<dd class="pd">Die Unterdomäne der URL für Ihre {{site.data.keyword.Bluemix_notm}}-Instanz. Beispiel: <code>https://console.mycompany.bluemix.net/cli</code></dd>
</dl>
</li>
<li>Führen Sie zum Installieren des {{site.data.keyword.Bluemix_notm}}-Administrator-CLI-Plug-ins den folgenden Befehl aus:<br/><br/>
<code>
cf install-plugin BluemixAdminCLI -r BluemixAdmin
</code>
</li>
</ol>

Wenn Sie das Plug-in deinstallieren müssen, können Sie die folgenden Befehle verwenden. Anschließend können Sie das aktualisierte Repository hinzufügen und das neueste Plug-in installieren.

* Plug-in deinstallieren: `cf uninstall-plugin BluemixAdminCLI`
* Plug-in-Repository entfernen: `cf remove-plugin-repo BluemixAdmin`


## {{site.data.keyword.Bluemix_notm}}-Administrator-CLI-Plug-in verwenden

Mit dem {{site.data.keyword.Bluemix_notm}}-Administrator-CLI-Plug-in können Sie Benutzer hinzufügen oder entfernen, Benutzer aus Organisationen zuweisen oder die Zuweisung von Benutzern aufheben und andere Management-Tasks ausführen.

Führen Sie den folgenden Befehl aus,
um eine Liste der Befehle anzuzeigen:

```
cf plugins
```
{: codeblock}

Wenn Sie weitere Hilfe zu einem Befehl benötigen, verwenden Sie die Option `-help`.

### Verbindung zu {{site.data.keyword.Bluemix_notm}} herstellen und anmelden

Bevor Sie das Administrator-CLI-Plug-in verwenden können, müssen Sie eine Verbindung herstellen und sich anmelden, falls dies noch nicht erfolgt ist.

<ol>
<li>Führen Sie zum Herstellen einer Verbindung zum {{site.data.keyword.Bluemix_notm}}-API-Endpunkt den folgenden Befehl aus:<br/><br/>
<code>
cf ba api https://console.&lt;subdomain&gt;.bluemix.net
</code>
<dl class="parml">
<dt class="pt dlterm">&lt;subdomain&gt;</dt>
<dd class="pd">Die Unterdomäne der URL für Ihre {{site.data.keyword.Bluemix_notm}}-Instanz.<br />
</dd>
</dl>
<p>Sie können die korrekte URL auf der Seite für Ressourcen und Informationen der Administratorkonsole
ermitteln. Die URL wird im Abschnitt 'API-Informationen' im Feld **API-URL** angezeigt.</p>
</li>
<li>Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} mit dem folgenden Befehl an:<br/><br/>
<code>
cf login
</code>
</li>
</ol>

## Benutzer verwalten
{: #admin_users}

### Benutzer hinzufügen
{: #admin_add_user}

Verwenden Sie den folgenden Befehl, um Ihrer {{site.data.keyword.Bluemix_notm}}-Umgebung einen Benutzer aus der Benutzerregistry Ihrer Umgebung hinzuzufügen:

```
cf ba add-user <user_name> <organization>
```
{: codeblock}

**Hinweis:** Zum Hinzufügen einer bestimmten Organisation müssen Sie ein **Administrator** mit der Berechtigung **users.write** (oder **Superuser**) sein. Wenn Sie ein Organisationsmanager sind, kann Ihnen auch die Funktion bereitgestellt werden, mit der Sie Ihrer Organisation Benutzer über einen Superuser hinzufügen können, der den Befehl **enable-managers-add-users** ausführt.  Weitere Informationen hierzu finden Sie unter [Managern die Möglichkeit geben, Benutzer hinzuzufügen](index.html#clius_emau).

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">Der Name des Benutzers im LDAP-Registry.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">Der Name oder die GUID der {{site.data.keyword.Bluemix_notm}}-Organisation, der der Benutzer hinzugefügt werden soll.</dd>
</dl>

**Tipp:** Sie können auch **ba au** als Alias für den längeren Befehlsnamen **ba add-user** verwenden.

<!-- staging-only commands start. Live for interconnect -->

### Nach einem Benutzer suchen
{: #admin_search_user}

Verwenden Sie den folgenden Befehl in Kombination mit den optionalen Suchfilterparametern (Name, Berechtigung, Organisation und Rolle), um nach einem Benutzer zu suchen:

```
cf ba search-users -name=<user_name_value> -permission=<permission_value> -organization=<organization_value> -role=<role_value>
```
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">&lt;user_name_value&gt;</dt>
<dd class="pd">Der Name des Benutzers in {{site.data.keyword.Bluemix_notm}}. </dd>
<dt class="pt dlterm">&lt;permission_value&gt;</dt>
<dd class="pd">Die Berechtigung, die dem Benutzer zugewiesen wurde. Beispiel: Superuser, Basic, Katalog, Benutzer und Berichte. Weitere Informationen zu den zugewiesenen Benutzerberechtigungen finden Sie im Abschnitt [Berechtigungen](/docs/admin/index.html#permissions). Dieser Parameter kann nicht in derselben Abfrage wie der Parameter 'organization' verwendet werden. </dd>
<dt class="pt dlterm">&lt;organization_value&gt;</dt>
<dd class="pd">Der Name der Organisation, zu der der Benutzer gehört. Dieser Parameter kann nicht in derselben Abfrage wie der Parameter 'permission' verwendet werden.</dd>
<dt class="pt dlterm">&lt;role_value&gt;</dt>
<dd class="pd">Die Organisationsrolle, die dem Benutzer zugewiesen wurde. Beispiel: Manager, Abrechnungsmanager oder Auditor für die Organisation. Sie müssen mit diesem Parameter die Organisation angeben. Weitere Informationen zu Rollen finden Sie im Abschnitt [Benutzerrollen](/docs/admin/users_roles.html#userrolesinfo).</dd>

</dl>

**Tipp:** Sie können auch **ba su** als Alias für den längeren Befehlsnamen **ba search-users** verwenden.

### Berechtigungen für einen Benutzer festlegen
{: #admin_setperm_user}

Verwenden Sie den folgenden Befehl, um die Berechtigungen für einen angegebenen Benutzer festzulegen:

```
cf ba set-permissions <user_name> <permission> <access>
```
{: codeblock}

**Hinweis:** Sie können jeweils nur eine Berechtigung gleichzeitig festlegen.

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">Der Name des Benutzers in {{site.data.keyword.Bluemix_notm}}.</dd>
<dt class="pt dlterm">&lt;permission&gt;</dt>
<dd class="pd">Legen Sie die Berechtigungen für den Benutzer fest: Admin (alternativ 'Superuser'), Login (alternativ 'Basic'), Catalog (Zugriff 'read' oder 'write'), Reports (Zugriff 'read' oder 'write') oder Users (Zugriff 'read' oder 'write').</dd>
<dt class="pt dlterm">&lt;access&gt;</dt>
<dd class="pd">Für die Berechtigungen Catalog, Reports oder Users müssen Sie außerdem die Zugriffsebene mit <code>read</code> oder <code>write</code> angeben.</dd>
</dl>

**Tipp:** Sie können auch **ba sp** als Alias für den längeren Befehlsnamen **ba set-permissions** verwenden.

<!-- staging-only commands end -->

### Benutzer entfernen
{: #admin_remov_user}

Verwenden Sie den folgenden Befehl, um einen Benutzer aus Ihrer {{site.data.keyword.Bluemix_notm}}-Umgebung zu entfernen:

```
cf ba remove-user <user_name>
```
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">Der Name des Benutzers in {{site.data.keyword.Bluemix_notm}}.</dd>

</dl>

**Tipp:** Sie können auch **ba ru** als Alias für den längeren Befehlsnamen **ba remove-user** verwenden.

### Managern die Möglichkeit geben, Benutzer hinzuzufügen
{: #clius_emau}

Wenn Sie in Ihrer {{site.data.keyword.Bluemix_notm}}-Umgebung über die **Superuser**-Berechtigung verfügen, können Sie Organisationsmanagern die Möglichkeit geben, den von ihnen verwalteten Organisationen Benutzer hinzuzufügen. Um Managern das Hinzufügen von Benutzern zu ermöglichen, verwenden Sie den folgenden Befehl:

```
cf ba enable-managers-add-users
```
{: codeblock}

**Tipp:** Sie können auch **ba emau** als Alias für den längeren Befehlsnamen **ba enable-managers-add-users** verwenden.

### Managern die Möglichkeit nehmen, Benutzer hinzuzufügen
{: #clius_dmau}

Wenn Organisationsmanager in Ihrer {{site.data.keyword.Bluemix_notm}}-Umgebung die Fähigkeit erhalten haben, den von ihnen verwalteten Organisationen Benutzer hinzuzufügen, indem sie den Befehl **enable-managers-add-users** verwenden, und wenn Sie über die **Superuser**-Berechtigung verfügen, können Sie diese Einstellung entfernen.  Um Managern die Möglichkeit zu nehmen, Benutzer hinzuzufügen, verwenden Sie den folgenden Befehl:

```
cf ba disable-managers-add-users
```
{: codeblock}

**Tipp:** Sie können auch **ba dmau** als Alias für den längeren Befehlsnamen **ba disable-managers-add-users** verwenden.

## Organisationen verwalten
{: #admin_orgs}

### Organisation hinzufügen
{: #admin_add_org}

Verwenden Sie den folgenden Befehl, um eine Organisation hinzuzufügen:

```
cf ba create-organization <organization> <manager>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">Der Name oder die GUID der hinzuzufügenden {{site.data.keyword.Bluemix_notm}}-Organisation.</dd>
<dt class="pt dlterm">&lt;manager&gt;</dt>
<dd class="pd">Der Benutzername des Managers der Organisation.</dd>
</dl>

**Tipp:** Sie können auch **ba co** als Alias für den längeren
Befehlsnamen **ba create-organization** verwenden.

### Organisation löschen
{: #admin_delete_org}

Verwenden Sie den folgenden Befehl, um eine Organisation zu löschen:

```
cf ba delete-organization <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">Der Name oder die GUID der zu löschenden {{site.data.keyword.Bluemix_notm}}-Organisation.</dd>
</dl>

**Tipp:** Sie können auch **ba do** als Alias für den längeren Befehlsnamen **ba delete-organization** verwenden.

### Benutzer einer Organisation zuweisen
{: #admin_ass_user_org}

Um einen Benutzer in Ihrer {{site.data.keyword.Bluemix_notm}}-Umgebung einer bestimmten Organisation zuzuweisen, verwenden Sie den folgenden Befehl:

```
cf ba set-org <user_name> <organization> [<role>]
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">Der Name des Benutzers in {{site.data.keyword.Bluemix_notm}}.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">Der Name oder die GUID der {{site.data.keyword.Bluemix_notm}}-Organisation, der der Benutzer zugewiesen werden soll.</dd>
<dt class="pt dlterm">&lt;role&gt;</dt>
<dd class="pd">Informationen zu {{site.data.keyword.Bluemix_notm}}-Benutzerrollen und Beschreibungen
finden Sie unter [Rollen](/docs/admin/users_roles.html).</dd>
</dl>

**Tipp:** Sie können auch **ba so** als Alias für den längeren Befehlsnamen **ba set-org** verwenden.

### Zuweisung eines Benutzers zu einer Organisation aufheben
{: #admin_unass_user_org}

Um die Zuweisung eines Benutzers in Ihrer {{site.data.keyword.Bluemix_notm}}-Umgebung zu einer bestimmten Organisation aufzuheben, verwenden Sie den folgenden Befehl:

```
cf ba unset-org <user_name> <organization> [<role>]
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">Der Name des Benutzers in {{site.data.keyword.Bluemix_notm}}.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">Der Name oder die GUID der {{site.data.keyword.Bluemix_notm}}-Organisation, der der Benutzer zugewiesen werden soll.</dd>
<dt class="pt dlterm">&lt;role&gt;</dt>
<dd class="pd">Informationen zu {{site.data.keyword.Bluemix_notm}}-Benutzerrollen und -Beschreibungen
finden Sie unter [Rollen zuweisen](/docs/admin/users_roles.html).</dd>
</dl>

**Tipp:** Sie können auch **ba uo** als Alias für den längeren Befehlsnamen **ba unset-org** verwenden.

#### Rollen zuweisen

<dl class="parml">
<dt class="pt dlterm">OrgManager</dt>
<dd class="pd">Organisationsmanager. Ein Organisationsmanager ist zu den folgenden Aktionen berechtigt:
<ul>
<li>Erstellen oder Löschen von Bereichen innerhalb der Organisation.</li>
<li>Einladen von Benutzern in die Organisation und Verwalten von Benutzern.</li>
<li>Verwalten von Domänen der Organisation.</li>
</ul>
</dd>
<dt class="pt dlterm">BillingManager</dt>
<dd class="pd">Abrechnungsmanager. Ein Abrechnungsmanager kann Informationen zur Laufzeit- und Servicenutzung
für die Organisation anzeigen.</dd>
<dt class="pt dlterm">OrgAuditor</dt>
<dd class="pd">Organisationsauditor. Ein Organisationsauditor kann Anwendungs- und Serviceinhalte im Bereich anzeigen.</dd>
</dl>

### Kontingent für eine Organisation festlegen
{: #admin_set_org_quota}

Verwenden Sie den folgenden Befehl, um für eine bestimmte Organisation ein Nutzungskontingent festzulegen:

```
cf ba set-quota <organization> <plan>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">Der Name oder die GUID der {{site.data.keyword.Bluemix_notm}}-Organisation, für die das Kontingent festgelegt werden soll.</dd>
<dt class="pt dlterm">&lt;plan&gt;</dt>
<dd class="pd">Der Kontingentplan für eine Organisation.</dd>
</dl>

**Tipp:** Sie können auch **ba sq** als Alias für den längeren Befehlsnamen **ba set-quota** verwenden.


### Containerkontingente für eine Organisation ermitteln
{: #admin_find_containquotas}

Verwenden Sie den folgenden Befehl, um das Kontingent für Container einer Organisation zu ermitteln:

```
cf bluemix-admin containers-quota <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">Der Name oder die ID der Organisation in Bluemix. Dieser Parameter ist erforderlich.</dd>
</dl>

**Tipp:** Sie können auch **ba cq** als Alias für den längeren Befehlsnamen **bluemix-admin containers-quota** verwenden.

### Containerkontingente für eine Organisation festlegen
{: #admin_set_containquotas}

Verwenden Sie den folgenden Befehl mit mindestens einer der Optionen, um das Kontingent für Container in einer Organisation festzulegen:

```
cf bluemix-admin set-containers-quota <organization> <options>
```
{: codeblock}

**Hinweis:** Sie können mehrere Optionen angeben. Es muss jedoch mindestens eine Option angegeben sein.

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">Der Name oder die ID der Organisation in Bluemix. Dieser Parameter ist erforderlich.</dd>
<dt class="pt dlterm">&lt;options&gt;</dt>
<dd class="pd">Geben Sie eine oder mehrere der folgenden Optionen an (der Wert muss jeweils eine ganze Zahl sein):
<ul>
<li>floating-ips-max &lt;Wert&gt;</li>
<li>floating-ips-space-default &lt;Wert&gt;</li>
<li>memory-max &lt;Wert&gt;</li>
<li>memory-space-default &lt;Wert&gt;</li>
<li>image-limit &lt;Wert&gt;</li>
</ul>
</dd>
</dl>

**Tipp:** Sie können auch die folgenden Kurznamen als Aliasnamen für die längeren Optionsnamen verwenden:
<dl class="parml">
<dt class="pt dlterm">floating-ips-max &lt;Wert&gt;</dt>
<dd class="pd"><strong>fim</strong></dd>
<dt class="pt dlterm">floating-ips-space-default &lt;Wert&gt;</dt>
<dd class="pd"><strong>fisd</strong></dd>
<dt class="pt dlterm">memory-max &lt;Wert&gt;</dt>
<dd class="pd"><strong>mm</strong></dd>
<dt class="pt dlterm">memory-space-default &lt;Wert&gt;</dt>
<dd class="pd"><strong>msd</strong></dd>
<dt class="pt dlterm">image-limit &lt;Wert&gt;</dt>
<dd class="pd"><strong>il</strong></dd>
</dl>

Optional können Sie eine Datei angeben, die bestimmte Konfigurationsparameter in einem gültigen JSON-Objekt enthält. Falls Sie die Option **-file** verwenden, hat diese Option Vorrang und die anderen Optionen werden ignoriert. Verwenden Sie den folgenden Befehl, um eine Datei bereitzustellen, anstatt die Optionen festzulegen:

```
cf bluemix-admin set-containers-quota <Organisation> <-Dateipfad zur JSON-Datei>
```
{: codeblock}

Das Format der JSON-Datei sollte dem folgenden Beispiel entsprechen:

```
{
  "floating_ips_max": 10,
  "floating_ips_space_default": 0,
  "ram_max": 4096,
  "ram_space_default": 0,
  "image_limit": 10
}
```
{: codeblock}

**Tipp:** Sie können auch **ba scq** als Alias für den längeren Befehlsnamen **bluemix-admin set-containers-quota** verwenden.

### Services für alle Organisationen aktivieren
{: #admin_ena_service_org}

Verwenden Sie den folgenden Befehl, um die Sichtbarkeit eines Service im
{{site.data.keyword.Bluemix_notm}}-Katalog für alle Organisationen zu aktivieren:

```
cf ba enable-service-plan <plan_identifier>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">Der Name oder die GUID des Serviceplans, der aktiviert werden soll. Wenn Sie einen nicht eindeutigen Serviceplannamen eingeben, wie zum Beispiel 'Standard' oder 'Basic', werden Sie dazu aufgefordert, eine Auswahl aus einer angezeigten Liste mit Serviceplänen zu treffen. Wählen Sie die Servicekategorie auf der Homepage aus, um einen Serviceplannamen anzugeben. Wählen Sie dann **Hinzufügen** aus, um die Services für diese Kategorie anzuzeigen. Klicken Sie auf den Servicenamen, um die Detailansicht zu öffnen; anschließend können Sie die Namen der für diesen Service verfügbaren Servicepläne anzeigen. </dd>
</dl>

**Tipp:** Sie können auch **ba esp** als Alias für den längeren Befehlsnamen **ba enable-service-plan** verwenden.

### Services für alle Organisationen inaktivieren
{: #admin_dis_service_org}

Verwenden Sie den folgenden Befehl, um die Sichtbarkeit eines Service im
{{site.data.keyword.Bluemix_notm}}-Katalog für alle Organisationen zu inaktivieren:

```
cf ba disable-service-plan <plan_identifier>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">Der Name oder die GUID des Serviceplans, der aktiviert werden soll. Wenn Sie einen nicht eindeutigen Serviceplannamen eingeben, wie zum Beispiel 'Standard' oder 'Basic', werden Sie dazu aufgefordert, eine Auswahl aus einer angezeigten Liste mit Serviceplänen zu treffen. Wählen Sie die Servicekategorie auf der Homepage aus, um einen Serviceplannamen anzugeben. Wählen Sie dann **Hinzufügen** aus, um die Services für diese Kategorie anzuzeigen. Klicken Sie auf den Servicenamen, um die Detailansicht zu öffnen; anschließend können Sie die Namen der für diesen Service verfügbaren Servicepläne anzeigen.</dd>
</dl>

**Tipp:** Sie können auch **ba dsp** als Alias für den längeren
Befehlsnamen **ba disable-service-plan** verwenden.

### Sichtbarkeit von Services für Organisationen hinzufügen
{: #admin_addvis_service_org}

Sie können eine Organisation aus der Liste der Organisationen, für die ein bestimmter Service im
{{site.data.keyword.Bluemix_notm}}-Katalog sichtbar ist, hinzufügen. Verwenden Sie den folgenden Befehl, um einer Organisation zu gestatten, einen bestimmten Service
im {{site.data.keyword.Bluemix_notm}}-Katalog anzuzeigen:

```
cf ba add-service-plan-visibility <plan_identifier> <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">Der Name oder die GUID des Serviceplans, der aktiviert werden soll. Wenn Sie einen nicht eindeutigen Serviceplannamen eingeben, wie zum Beispiel 'Standard' oder 'Basic', werden Sie dazu aufgefordert, eine Auswahl aus einer angezeigten Liste mit Serviceplänen zu treffen. Wählen Sie die Servicekategorie auf der Homepage aus, um einen Serviceplannamen anzugeben. Wählen Sie dann **Hinzufügen** aus, um die Services für diese Kategorie anzuzeigen. Klicken Sie auf den Servicenamen, um die Detailansicht zu öffnen; anschließend können Sie die Namen der für diesen Service verfügbaren Servicepläne anzeigen.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">Der Name oder die GUID der {{site.data.keyword.Bluemix_notm}}-Organisation, die der Sichtbarkeitsliste des Service hinzugefügt werden soll.</dd>
</dl>

**Tipp:** Sie können auch **ba aspv** als Alias für den längeren
Befehlsnamen **ba add-service-plan-visibility** verwenden.

### Sichtbarkeit von Services für Organisationen entfernen
{: #admin_remvis_service_org}

Sie können eine Organisation aus der Liste der Organisationen, für die ein bestimmter Service im
{{site.data.keyword.Bluemix_notm}}-Katalog sichtbar ist, entfernen. Verwenden Sie den folgenden Befehl, um die Sichtbarkeit eines Service im
{{site.data.keyword.Bluemix_notm}}-Katalog für eine Organisation zu entfernen:

```
cf ba remove-service-plan-visibility <plan_identifier> <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">Der Name oder die GUID des Serviceplans, der aktiviert werden soll. Wenn Sie einen nicht eindeutigen Serviceplannamen eingeben, wie zum Beispiel 'Standard' oder 'Basic', werden Sie dazu aufgefordert, eine Auswahl aus einer angezeigten Liste mit Serviceplänen zu treffen. Wählen Sie die Servicekategorie auf der Homepage aus, um einen Serviceplannamen anzugeben. Wählen Sie dann **Hinzufügen** aus, um die Services für diese Kategorie anzuzeigen. Klicken Sie auf den Servicenamen, um die Detailansicht zu öffnen; anschließend können Sie die Namen der für diesen Service verfügbaren Servicepläne anzeigen.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">Der Name oder die GUID der {{site.data.keyword.Bluemix_notm}}-Organisation, die aus der Sichtbarkeitsliste des Service entfernt werden soll.</dd>
</dl>

**Tipp:** Sie können auch **ba rspv** als Alias für den längeren
Befehlsnamen **ba remove-service-plan-visibility** verwenden.

### Sichtbarkeit von Services für Organisationen bearbeiten
{: #admin_editvis_service_org}

Sie können die Liste der Services, die für bestimmte Organisationen im {{site.data.keyword.Bluemix_notm}}-Katalog
sichtbar sind, bearbeiten und ersetzen. Verwenden Sie den folgenden Befehl, um alle vorhandenen sichtbaren Services für eine Organisation oder mehrere Organisationen zu ersetzen:

```
cf ba edit-service-plan-visibilities <plan_identifier> <organization_1> <optional_organization_2>
```
{: codeblock}

**Hinweis:** Dieser Befehl ersetzt vorhandene sichtbare Services für die angegebenen Organisationen
durch den Service, den Sie im Befehl angeben.

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">Der Name oder die GUID des Serviceplans, der aktiviert werden soll. Wenn Sie einen nicht eindeutigen Serviceplannamen eingeben, wie zum Beispiel 'Standard' oder 'Basic', werden Sie dazu aufgefordert, eine Auswahl aus einer angezeigten Liste mit Serviceplänen zu treffen. Wählen Sie die Servicekategorie auf der Homepage aus, um einen Serviceplannamen anzugeben. Wählen Sie dann **Hinzufügen** aus, um die Services für diese Kategorie anzuzeigen. Klicken Sie auf den Servicenamen, um die Detailansicht zu öffnen; anschließend können Sie die Namen der für diesen Service verfügbaren Servicepläne anzeigen.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">Der Name oder die GUID der {{site.data.keyword.Bluemix_notm}}-Organisation, für die die Sichtbarkeit hinzugefügt werden soll. Sie können
die Sichtbarkeit des Service für mehrere Organisationen aktivieren, indem Sie weitere Organisationsnamen oder GUIDs im Befehl angeben.</dd>
</dl>

**Tipp:** Sie können auch **ba espv** als Alias für den längeren
Befehlsnamen **ba edit-service-plan-visibility** verwenden.

## Berichte verwalten
{: #admin_add_report}

### Berichte hinzufügen
{: #admin_add_report}

Verwenden Sie den folgenden Befehl, um einen Sicherheitsbericht hinzuzufügen:

```
cf ba add-report <category> <date> <PDF|TXT|LOG> <RTF>
```
{: codeblock}

**Hinweis:** Wenn Sie für die Berichtsberechtigung über Schreibzugriff verfügen, können Sie eine neue Kategorie erstellen und für die Benutzer einen Bericht in einem zulässigen Format hinzufügen. Geben Sie den neuen Kategorienamen für den Parameter `category` ein oder fügen Sie den neuen Bericht einer vorhandenen Kategorie hinzu.

<dl class="parml">
<dt class="pt dlterm">&lt;category&gt;</dt>
<dd class="pd">Die Kategorie für den Bericht. Wenn ein Leerzeichen im Namen enthalten ist, setzen Sie den Namen in Anführungszeichen.</dd>
<dt class="pt dlterm">&lt;date&gt;</dt>
<dd class="pd">Das Berichtsdatum im Format <samp class="ph codeph">JJJJMMTT</samp>.</dd>
<dt class="pt dlterm">&lt;PDF|TXT|LOG&gt;</dt>
<dd class="pd">Der Pfad für die PDF-Datei, Textdatei oder Protokolldatei des Berichts, die hochgeladen werden soll.</dd>
<dt class="pt dlterm">&lt;RTF&gt;</dt>
<dd class="pd">Eine Option zum Einschluss einer RTF-Version (Rich Text Format) der PDF. Diese Option gilt nur,
wenn Sie einen Pfad zur PDF-Datei für den Bericht eingegeben haben. Die RTF-Version wird zum Indexieren und Suchen verwendet.</dd>
</dl>

**Tipp:** Sie können auch **ba ar** als Alias für den längeren Befehlsnamen **ba add-report** verwenden.

### Berichte löschen
{: #admin_del_report}

Verwenden Sie den folgenden Befehl, um einen Sicherheitsbericht zu löschen:

```
cf ba delete-report <category> <date> <name>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;category&gt;</dt>
<dd class="pd">Die Kategorie für den Bericht. Wenn ein Leerzeichen im Namen enthalten ist, setzen Sie den Namen in Anführungszeichen.</dd>
<dt class="pt dlterm">&lt;date&gt;</dt>
<dd class="pd">Das Berichtsdatum im Format <samp class="ph codeph">JJJJMMTT</samp>.</dd>
<dt class="pt dlterm">&lt;name&gt;</dt>
<dd class="pd">Der Name des Berichts.</dd>
</dl>

**Tipp:** Sie können auch **ba dr** als Alias für den längeren Befehlsnamen **ba delete-report** verwenden.

### Berichte abrufen
{: #admin_retr_report}

Verwenden Sie den folgenden Befehl, um einen Sicherheitsbericht abzurufen:

```
cf ba retrieve-report <category> <date> <name>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;category&gt;</dt>
<dd class="pd">Die Kategorie für den Bericht. Wenn ein Leerzeichen im Namen enthalten ist, setzen Sie den Namen in Anführungszeichen.</dd>
<dt class="pt dlterm">&lt;date&gt;</dt>
<dd class="pd">Das Berichtsdatum im Format <samp class="ph codeph">JJJJMMTT</samp>.</dd>
<dt class="pt dlterm">&lt;name&gt;</dt>
<dd class="pd">Der Name des Berichts.</dd>
</dl>

**Tipp:** Sie können auch **ba rr** als Alias für den längeren Befehlsnamen **ba retrieve-report** verwenden.

## Metrikinformationen zu Ressourcen anzeigen
{: #cliresourceusage}

Sie können Metrikinformationen zu Ressourcen anzeigen, beispielsweise Hauptspeicher- und Plattenbelegung oder CPU-Auslastung. Es wird eine Zusammenfassung der verfügbaren physischen und reservierten Ressourcen sowie der Nutzung dieser Ressourcen angezeigt. Zudem werden Nutzungsdaten, die vergangene Speichernutzung und die Plattenbelegung angezeigt. Die Daten zur vergangenen Speichernutzung und Plattenbelegung werden standardmäßig nach Wochen und in absteigender Reihenfolge angezeigt. Verwenden Sie den folgenden Befehl, um die Metrikinformationen zu Ressourcen anzuzeigen:

```
cf ba resource-metrics <monthly> <weekly>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;monthly&gt;</dt>
<dd class="pd">Anzeige der vergangenen Nutzungsdaten für Speicher und Plattenbelegung jeweils für einen Monat.</dd>
<dt class="pt dlterm">&lt;weekly&gt;</dt>
<dd class="pd">Anzeige der vergangenen Nutzungsdaten für Speicher und Plattenbelegung jeweils für eine Woche. Dies ist der Standardwert.</dd>
</dl>

**Tipp:** Sie können auch **ba rsm** als Alias für den längeren Befehlsnamen **ba resource-metrics** verwenden.


## Service-Broker verwalten
{: #admin_servbro}

### Service-Broker auflisten
{: #clilistservbro}

Verwenden Sie den folgenden Befehl, um alle Service-Broker aufzulisten:

```
cf ba service-brokers <broker_name>
```
{: codeblock}

**Hinweis:** Geben Sie zum Auflisten aller Service-Broker den Befehl ohne den Parameter `broker_name` ein.

<dl class="parml">
<dt class="pt dlterm">&lt;broker_name&gt;</dt>
<dd class="pd">Optional: Der Name des angepassten Service-Brokers. Verwenden Sie diesen Parameter, wenn Sie Informationen zu einem bestimmten Service-Broker abrufen wollen.</dd>
</dl>

**Tipp:** Sie können auch **ba sb** als Alias für den längeren
Befehlsnamen **ba service-brokers** verwenden.

### Service-Broker hinzufügen
{: #cliaddservbro}

Verwenden Sie den folgenden Befehl, um einen Service-Broker hinzuzufügen, sodass Sie einen angepassten Service zu Ihrem {{site.data.keyword.Bluemix_notm}}-Katalog hinzufügen können:

```
cf ba add-service-broker <broker_name> <user_name> <password> <broker_url>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;broker_name&gt;</dt>
<dd class="pd">Der Name des angepassten Service-Brokers.</dd>
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">Der Benutzername für das Konto, das Zugriff auf den Service-Broker hat.</dd>
<dt class="pt dlterm">&lt;password&gt;</dt>
<dd class="pd">Das Kennwort für das Konto, das Zugriff auf den Service-Broker hat.</dd>
<dt class="pt dlterm">&lt;broker_url&gt;</dt>
<dd class="pd">Die URL für den Service-Broker.</dd>
</dl>

**Tipp:** Sie können auch **ba asb** als Alias für den längeren
Befehlsnamen **ba add-service-broker** verwenden.

### Service-Broker löschen
{: #clidelservbro}

Verwenden Sie den folgenden Befehl, um einen Service-Broker zu löschen, sodass Sie einen angepassten Service aus Ihrem {{site.data.keyword.Bluemix_notm}}-Katalog entfernen können:

```
cf ba delete-service-broker <service_broker>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;service_broker&gt;</dt>
<dd class="pd">Der Name oder die GUID des angepassten Service-Brokers.</dd>
</dl>

**Tipp:** Sie können auch **ba dsb** als Alias für den längeren
Befehlsnamen **ba delete-service-broker** verwenden.

### Service-Broker aktualisieren
{: #cliupdservbro}

Verwenden Sie den folgenden Befehl, um einen Service-Broker zu aktualisieren:

```
cf ba update-service-broker <broker_name> <user_name> <password> <broker_url>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;broker_name&gt;</dt>
<dd class="pd">Der Name des angepassten Service-Brokers.</dd>
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">Der Benutzername für das Konto, das Zugriff auf den Service-Broker hat.</dd>
<dt class="pt dlterm">&lt;password&gt;</dt>
<dd class="pd">Das Kennwort für das Konto, das Zugriff auf den Service-Broker hat.</dd>
<dt class="pt dlterm">&lt;broker_url&gt;</dt>
<dd class="pd">Die URL für den Service-Broker.</dd>
</dl>

**Tipp:** Sie können auch **ba usb** als Alias für den längeren
Befehlsnamen **ba update-service-broker** verwenden.


## Anwendungssicherheitsgruppen verwalten
{: #admin_secgro}

Zum Arbeiten mit Anwendungssicherheitsgruppen (Application Security Groups, ASGs) müssen Sie ein Administrator mit voller Berechtigung für die lokale oder dedizierte Umgebung sein. Alle Benutzer in der Umgebung können die verfügbaren ASGs für die Organisation auflisten, die Ziel des Befehls ist. Zum Erstellen, Aktualisieren oder Binden von ASGs müssen Sie jedoch Administrator für die {{site.data.keyword.Bluemix_notm}}-Umgebung sein.

ASGs fungieren als virtuelle Firewalls, die den abgehenden Datenverkehr aus der Anwendung in die {{site.data.keyword.Bluemix_notm}}-Umgebung steuern. Jede ASG besteht aus einer Liste mit Regeln, die den Datenverkehr und die Kommunikation in das externe Netz oder aus diesem Netz definieren. Sie können eine oder mehrere ASGs an einen bestimmten Sicherheitsgruppensatz (z. B. an einen Gruppensatz, der für die Anwendung des globalen Zugriffs verwendet wird) oder an Bereiche innerhalb einer Organisation in der {{site.data.keyword.Bluemix_notm}}-Umgebung binden.

Bei der Erstinstallation von {{site.data.keyword.Bluemix_notm}} wird der gesamte Zugriff auf das externe Netz eingeschränkt. Zwei von IBM erstellte Sicherheitsgruppen (`public_networks` und `dns`) ermöglichen den globalen Zugriff auf das externe Netz, wenn Sie diese Gruppen an die Cloud Foundry-Standardsicherheitsgruppensätze binden. Die beiden Sicherheitsgruppensätze in Cloud Foundry zur Anwendung des globalen Zugriffs sind die Gruppensätze **Default Staging** und **Default Running**. Von diesen Gruppensätzen werden die Regeln für den Datenverkehr auf alle aktiven Apps bzw. alle Staging-Apps angewendet. Wenn Sie keine Bindung an diese beiden Sicherheitsgruppensätze herstellen möchten, können Sie die Bindung an die Cloud Foundry-Gruppensätze aufheben und die Sicherheitsgruppe anschließend an einen bestimmten Bereich binden. Weitere Informationen finden Sie in [Binding Application Security Groups ![Symbol für externen Link](../../../icons/launch-glyph.svg)](https://docs.cloudfoundry.org/adminguide/app-sec-groups.html#binding-groups){: new_window}.

**Hinweis:** Die folgenden Befehle, die Ihnen die Arbeit mit Sicherheitsgruppen ermöglichen, basieren auf Cloud Foundry Version 1.6. Weitere Informationen einschließlich der Angaben zu erforderlichen und optionalen Feldern finden Sie in den Cloud Foundry-Informationen zum Thema [Anwendungssicherheitsgruppen erstellen ![Symbol für externen Link](../../../icons/launch-glyph.svg)](https://docs.cloudfoundry.org/adminguide/app-sec-groups.html#creating-groups){: new_window}.

### Sicherheitsgruppen auflisten
{: #clilissecgro}

* Verwenden Sie den folgenden Befehl, um alle Sicherheitsgruppen aufzulisten:

```
cf ba security-groups
```
{: codeblock}

**Tipp:** Sie können auch **ba sgs** als Alias für den längeren Befehlsnamen **ba security-groups** verwenden.

* Verwenden Sie den folgenden Befehl, um die Details einer bestimmten Sicherheitsgruppe anzuzeigen:

```
cf ba security-groups <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;security-group&gt;</dt>
<dd class="pd">Der Name der Sicherheitsgruppe.</dd>
</dl>

**Tipp:** Sie können auch **ba sg** als Alias für den längeren Befehlsnamen **ba security-groups** mit dem Parameter `security-group` verwenden.


### Sicherheitsgruppe erstellen
{: #clicreasecgro}

Weitere Informationen zur Erstellung von Sicherheitsgruppen und Regeln, die den abgehenden Datenverkehr definieren, finden Sie in [Creating Application Security Groups ![Symbol für externen Link](../../../icons/launch-glyph.svg)](https://docs.cloudfoundry.org/adminguide/app-sec-groups.html#creating-groups){: new_window}.

Verwenden Sie den folgenden Befehl, um eine Sicherheitsgruppe zu erstellen:

```
cf ba create-security-group <security-group> <path-to-rules-file>
```
{: codeblock}

Den Namen erstellter Sicherheitsgruppen wird das Präfix `adminconsole_` vorangestellt, um sie von den Sicherheitsgruppen zu unterscheiden, die von IBM erstellt werden.

<dl class="parml">
<dt class="pt dlterm">&lt;security-group&gt;</dt>
<dd class="pd">Der Name der Sicherheitsgruppe.</dd>
<dt class="pt dlterm">&lt;path-to-rules-file&gt;</dt>
<dd class="pd">Der absolute oder relative Pfad zu einer Regeldatei.</dd>
</dl>

**Tipp:** Sie können auch **ba csg** als Alias für den längeren Befehlsnamen **ba create-security-group** verwenden.

### Sicherheitsgruppe aktualisieren
{: #cliupdsecgro}

Verwenden Sie den folgenden Befehl, um eine Sicherheitsgruppe zu aktualisieren:

```
cf ba update-security-group <security-group> <path-to-rules-file>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;security-group&gt;</dt>
<dd class="pd">Der Name der Sicherheitsgruppe.</dd>
<dt class="pt dlterm">&lt;path-to-rules-file&gt;</dt>
<dd class="pd">Der absolute oder relative Pfad zu einer Regeldatei.</dd>
</dl>

**Tipp:** Sie können auch **ba usg** als Alias für den längeren Befehlsnamen **ba update-security-group** verwenden.

### Sicherheitsgruppe löschen
{: #clidelsecgro}

Verwenden Sie den folgenden Befehl, um eine Sicherheitsgruppe zu löschen:

```
cf ba delete-security-group <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;security-group&gt;</dt>
<dd class="pd">Der Name der Sicherheitsgruppe.</dd>
</dl>

**Tipp:** Sie können auch **ba dsg** als Alias für den längeren Befehlsnamen **ba delete-security-group** verwenden.


### Sicherheitsgruppen binden
{: #clibindsecgro}

Weitere Informationen zum Binden von Sicherheitsgruppen finden Sie auf der Seite zum [Binden von Anwendungssicherheitsgruppen ![Symbol für externen Link](../../../icons/launch-glyph.svg)](https://docs.cloudfoundry.org/adminguide/app-sec-groups.html#binding-groups){: new_window}.

* Verwenden Sie den folgenden Befehl, um eine Bindung zum Sicherheitsgruppensatz 'Default Staging' herzustellen:

```
cf ba bind-staging-security-group <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;security-group&gt;</dt>
<dd class="pd">Der Name der Sicherheitsgruppe.</dd>
</dl>

**Tipp:** Sie können auch **ba bssg** als Alias für den längeren Befehlsnamen **ba bind-staging-security-group** verwenden.

* Verwenden Sie den folgenden Befehl, um eine Bindung zum Sicherheitsgruppensatz 'Default Running' herzustellen:

```
cf ba bind-running-security-group <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;security-group&gt;</dt>
<dd class="pd">Der Name der Sicherheitsgruppe.</dd>
</dl>

**Tipp:** Sie können auch **ba brsg** als Alias für den längeren Befehlsnamen **ba bind-running-security-group** verwenden.

* Verwenden Sie den folgenden Befehl, um eine Sicherheitsgruppe an einen Bereich zu binden:

```
cf ba bind-security-group <security-group> <org> <space>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;security-group&gt;</dt>
<dd class="pd">Der Name der Sicherheitsgruppe.</dd>
<dt class="pt dlterm">&lt;org&gt;</dt>
<dd class="pd">Der Name der Organisation, an die die Sicherheitsgruppe gebunden wird.</dd>
<dt class="pt dlterm">&lt;space&gt;</dt>
<dd class="pd">Der Name des Bereichs innerhalb der Organisation, an den die Sicherheitsgruppe gebunden wird.</dd>
</dl>

**Tipp:** Sie können auch **ba bsg** als Alias für den längeren Befehlsnamen **ba bind-security-group** verwenden.

### Bindung von Sicherheitsgruppen aufheben
{: #cliunbindsecgro}

Weitere Informationen zur Aufhebung der Bindung von Sicherheitsgruppen finden Sie auf der Seite zum [Aufheben von Bindungen von Anwendungssicherheitsgruppen ![Symbol für externen Link](../../../icons/launch-glyph.svg)](https://docs.cloudfoundry.org/adminguide/app-sec-groups.html#unbinding-groups){: new_window}.

* Verwenden Sie den folgenden Befehl, um die Bindung zu einem Sicherheitsgruppensatz 'Default Staging' aufzuheben:

```
cf ba unbind-staging-security-group <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;security-group&gt;</dt>
<dd class="pd">Der Name der Sicherheitsgruppe.</dd>
</dl>

**Tipp:** Sie können auch **ba ussg** als Alias für den längeren Befehlsnamen **ba unbind-staging-security-group** verwenden.

* Verwenden Sie den folgenden Befehl, um die Bindung zu einem Sicherheitsgruppensatz 'Default Running' aufzuheben:

```
cf ba unbind-running-security-group <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;security-group&gt;</dt>
<dd class="pd">Der Name der Sicherheitsgruppe.</dd>
</dl>

**Tipp:** Sie können auch **ba brsg** als Alias für den längeren Befehlsnamen **ba bind-running-security-group** verwenden.

* Verwenden Sie den folgenden Befehl, um die Bindung einer Sicherheitsgruppe zu einem Bereich aufzuheben:

```
cf ba unbind-security-group <security-group> <org> <space>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;security-group&gt;</dt>
<dd class="pd">Der Name der Sicherheitsgruppe.</dd>
<dt class="pt dlterm">&lt;org&gt;</dt>
<dd class="pd">Der Name der Organisation, an die die Sicherheitsgruppe gebunden wird.</dd>
<dt class="pt dlterm">&lt;space&gt;</dt>
<dd class="pd">Der Name des Bereichs innerhalb der Organisation, an den die Sicherheitsgruppe gebunden wird.</dd>
</dl>

**Tipp:** Sie können auch **ba usg** als Alias für den längeren Befehlsnamen **ba unbind-staging-security-group** verwenden.

## Buildpacks verwalten
{: #admin_buildpack}

### Buildpacks auflisten
{: #clilistbuildpack}

Wenn Sie über eine Schreibberechtigung für den App-Katalog verfügen, können Sie Buildpacks auflisten. Verwenden Sie den folgenden Befehl, um alle Buildpacks aufzulisten oder ein  bestimmtes Buildpack anzuzeigen:

```
cf ba buildpacks <buildpack_name>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;buildpack_name&gt;</dt>
<dd class="pd">Ein optionaler Parameter zur Angabe eines bestimmten Buildpacks, das angezeigt werden soll.</dd>
</dl>

**Tipp:** Sie können auch **ba lb** als Alias für den längeren Befehlsnamen **ba buildpacks** verwenden.

### Buildpack erstellen und hochladen
{: #clicreupbuildpack}

Wenn Sie über eine Schreibberechtigung für den App-Katalog verfügen, können Sie ein Buildpack erstellen und hochladen. Jede komprimierte Datei mit der Dateierweiterung .zip kann hochgeladen werden. Verwenden Sie den folgenden Befehl, um ein Buildpack hochzuladen:

```
cf ba create-buildpack <buildpack_name> <file_path> <position>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;buildpack_name&gt;</dt>
<dd class="pd">Der Name des hochzuladenden Buildpacks.</dd>
<dt class="pt dlterm">&lt;file_path&gt;</dt>
<dd class="pd">Der Pfad zur komprimierten Datei des Buildpacks.</dd>
<dt class="pt dlterm">&lt;position&gt;</dt>
<dd class="pd">Die Reihenfolge, in der die Buildpacks während der automatischen Buildpackerkennung geprüft werden.</dd>
</dl>

**Tipp:** Sie können auch **ba cb** als Alias für den längeren Befehlsnamen **ba create-buildpack** verwenden.

### Buildpack aktualisieren
{: #cliupdabuildpack}

Wenn Sie über eine Schreibberechtigung für den App-Katalog verfügen, können Sie ein vorhandenes Buildpack aktualisieren.  Verwenden Sie den folgenden Befehl, um ein Buildpack zu aktualisieren:

```
cf ba update-buildpack <buildpack_name> <position> <enabled> <locked>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;buildpack_name&gt;</dt>
<dd class="pd">Der Name des zu aktualisierenden Buildpacks.</dd>
<dt class="pt dlterm">&lt;position&gt;</dt>
<dd class="pd">Die Reihenfolge, in der die Buildpacks während der automatischen Buildpackerkennung geprüft werden.</dd>
<dt class="pt dlterm">&lt;enabled&gt;</dt>
<dd class="pd">Gibt an, ob das Buildpack für das Staging verwendet wird.</dd>
<dt class="pt dlterm">&lt;locked&gt;</dt>
<dd class="pd">Gibt an, ob das Buildpack gesperrt ist, um Aktualisierungen zu verhindern.</dd>
</dl>

**Tipp:** Sie können auch **ba ub** als Alias für den längeren Befehlsnamen **ba update-buildpack** verwenden.

### Buildpack löschen
{: #clidelbuildpack}

Wenn Sie über eine Schreibberechtigung für den App-Katalog verfügen, können Sie ein vorhandenes Buildpack löschen.  Verwenden Sie den folgenden Befehl, um ein Buildpack zu löschen:

```
cf ba delete-buildpack <buildpack_name>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;buildpack_name&gt;</dt>
<dd class="pd">Der Name des zu löschenden Buildpacks.</dd>
</dl>

**Tipp:** Sie können auch **ba db** als Alias für den längeren Befehlsnamen **ba delete-buildpack** verwenden.
