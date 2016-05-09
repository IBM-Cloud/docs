---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix_notm}}-Administrator-CLI
{: #bluemixadmincli}

*Letzte Aktualisierung: 3. März 2016*

Sie können Benutzer für Ihre {{site.data.keyword.Bluemix_notm}} Local- oder
{{site.data.keyword.Bluemix_notm}} Dedicated-Umgebung über die Cloud
Foundry-Befehlszeilenschnittstelle mit dem
{{site.data.keyword.Bluemix_notm}}-Administrator-CLI-Plug-in verwalten. Sie können Benutzer zum Beispiel aus einer LDAP-Registry
hinzufügen. Informationen zur Zuordnung Ihres {{site.data.keyword.Bluemix_notm}} Public-Kontos finden Sie unter [Verwalten](../../../admin/adminpublic.html#administer).

Vor dem Beginn müssen Sie die Befehlszeilenschnittstelle 'cf' installieren. Für das
{{site.data.keyword.Bluemix_notm}}-Administrator-CLI-Plug-in
ist cf Version 6.11.2 oder höher erforderlich. [Cloud Foundry-Befehlszeilenschnittstelle herunterladen](https://github.com/cloudfoundry/cli/releases){: new_window}

**Einschränkung:** Die
Cloud Foundry-Befehlszeilenschnittstelle wird nicht von Cygwin unterstützt. Verwenden Sie
die Cloud Foundry-Befehlszeilenschnittstelle in einem
Befehlszeilenfenster, das sich von dem Befehlszeilenfenster von Cygwin unterscheidet.

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
<dd class="pd">Die Unterdomäne der URL für Ihre {{site.data.keyword.Bluemix_notm}}-Instanz.</dd>
</dl>
</li>
<li>Führen Sie zum Installieren des {{site.data.keyword.Bluemix_notm}}-Administrator-CLI-Plug-ins den folgenden Befehl aus:<br/><br/> <code>
cf install-plugin bluemix-admin-cli -r BluemixAdmin
</code>
</li>
</ol>

## {{site.data.keyword.Bluemix_notm}}-Administrator-CLI-Plug-in verwenden

Mit dem {{site.data.keyword.Bluemix_notm}}-Administrator-CLI-Plug-in können Sie Benutzer hinzufügen oder entfernen, Benutzer aus Organisationen zuweisen oder die Zuweisung von Benutzern aufheben und andere Management-Tasks ausführen. Führen Sie den folgenden Befehl aus,
um eine Liste der Befehle anzuzeigen:

```
cf plugins
```
{: codeblock}

Wenn Sie weitere Hilfe zu einem Befehl benötigen, verwenden Sie die Option `-help`.

### Verbindung zu {{site.data.keyword.Bluemix_notm}} herstellen und anmelden

Bevor Sie das Administrator-CLI-Plug-in zum Verwalten von Benutzern verwenden können, müssen Sie eine Verbindung herstellen und sich anmelden, falls dies noch nicht erfolgt ist.

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

### Benutzer hinzufügen

Sie können Ihrer {{site.data.keyword.Bluemix_notm}}-Umgebung einen Benutzer aus einem LDAP-Registry hinzufügen. Geben Sie den folgenden Befehl ein:

```
cf ba add-user <user_name> <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">Der Name des Benutzers im LDAP-Registry.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">Der Name oder die GUID der {{site.data.keyword.Bluemix_notm}}-Organisation, der der Benutzer hinzugefügt werden soll.</dd>
</dl>

**Tipp:** Sie können auch **ba au** als Alias für den längeren
Befehlsnamen **ba add-user** verwenden.

<!-- staging-only commands start. Live for interconnect -->

### Nach einem Benutzer suchen

Sie können nach einem Benutzer suchen. Geben Sie den folgenden Befehl ein:

```
cf ba search-users <user_name>
```
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">Der Name des Benutzers in {{site.data.keyword.Bluemix_notm}}.</dd>

</dl>

**Tipp:** Sie können auch **ba su** als Alias für den längeren
Befehlsnamen **ba search-users** verwenden.

### Berechtigungen für einen Benutzer festlegen

Sie können Berechtigungen für einen angegebenen Benutzer festlegen. Geben Sie den folgenden Befehl ein:

```
cf ba set-permissions <user_name> <permission> <access>
```
{: codeblock}

**Hinweis:** Sie können jeweils nur eine Berechtigung gleichzeitig festlegen.

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">Der Name des Benutzers in {{site.data.keyword.Bluemix_notm}}.</dd>
<dt class="pt dlterm">&lt;permission&gt;</dt>
<dd class="pd">Legen Sie die Berechtigungen für den Benutzer fest: Admin (Administrator), Login (Anmelden), Catalog (Katalog: Zugriff 'read' oder 'write'), Reports
(Berichte: Zugriff 'read' oder 'write') oder Users (Benutzer: Zugriff 'read' oder 'write').</dd>
<dt class="pt dlterm">&lt;access&gt;</dt>
<dd class="pd">Für die Berechtigungen Catalog, Reports oder Users müssen Sie außerdem die Zugriffsebene mit <code>read</code> oder <code>write</code> angeben.</dd>
</dl>

**Tipp:** Sie können auch **ba sp** als Alias für den längeren
Befehlsnamen **ba set-permissions** verwenden.

<!-- staging-only commands end -->

### Benutzer entfernen

Sie können einen Benutzer aus Ihrer
{{site.data.keyword.Bluemix_notm}}-Umgebung
mit dem folgenden Befehl entfernen:

```
cf ba remove-user <user_name>
```
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">Der Name des Benutzers in {{site.data.keyword.Bluemix_notm}}.</dd>

</dl>

**Tipp:** Sie können auch **ba ru** als Alias für den längeren
Befehlsnamen **ba remove-user** verwenden.

### Organisation hinzufügen und löschen

Sie können eine Organisation hinzufügen und löschen.

* Geben Sie den folgenden Befehl ein, um eine Organisation hinzuzufügen:

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

* Geben Sie den folgenden Befehl ein, um eine Organisation zu löschen:

```
cf ba delete-organization <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">Der Name oder die GUID der zu löschenden {{site.data.keyword.Bluemix_notm}}-Organisation.</dd>
</dl>

**Tipp:** Sie können auch **ba do** als Alias für den längeren
Befehlsnamen **ba delete-organization** verwenden.

### Benutzer einer Organisation zuweisen

Sie können einen Benutzer in Ihrer
{{site.data.keyword.Bluemix_notm}}-Umgebung einer
bestimmten Organisation zuweisen. Geben Sie den folgenden Befehl ein:

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
finden Sie unter [Rollen](../../../admin/adminpublic.html#orgsandspaces).</dd>
</dl>

**Tipp:** Sie können auch **ba so** als Alias für den längeren
Befehlsnamen **ba set-org** verwenden.

### Zuweisung eines Benutzers zu einer Organisation aufheben

Sie können die Zuweisung eines Benutzers in Ihrer
{{site.data.keyword.Bluemix_notm}}-Umgebung zu einer
bestimmten Organisation aufheben. Geben Sie den folgenden Befehl ein:

```
cf ba unset-org <user_name> <organization> [<role>]
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">Der Name des Benutzers in {{site.data.keyword.Bluemix_notm}}.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">Der Name oder die GUID der {{site.data.keyword.Bluemix_notm}}-Organisation, der der Benutzer zugewiesen ist.</dd>
<dt class="pt dlterm">&lt;role&gt;</dt>
<dd class="pd">Informationen zu {{site.data.keyword.Bluemix_notm}}-Benutzerrollen und Beschreibungen
finden Sie unter [Rollen](../../../admin/adminpublic.html#orgsandspaces).</dd>
</dl>

**Tipp:** Sie können auch **ba uo** als Alias für den längeren
Befehlsnamen **ba unset-org** verwenden.

### Rollen

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

Sie können das Nutzungskontingent für eine bestimmte Organisation festlegen.

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

**Tipp:** Sie können auch **ba sq** als Alias für den längeren
Befehlsnamen **ba set-quota** verwenden.

### Berichte hinzufügen, löschen und abrufen

Sie können Sicherheitsberichte hinzufügen, löschen und abrufen.
* Geben Sie den folgenden Befehl ein, um einen Bericht hinzuzufügen:

```
cf ba add-report <category> <date> <PDF|TXT|LOG> <RTF>
```
{: codeblock}

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

**Tipp:** Sie können auch **ba ar** als Alias für den längeren
Befehlsnamen **ba add-report** verwenden.

* Geben Sie den folgenden Befehl ein, um einen Bericht zu löschen:

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

**Tipp:** Sie können auch **ba dr** als Alias für den längeren
Befehlsnamen **ba delete-report** verwenden.

* Geben Sie den folgenden Befehl ein, um einen Bericht abzurufen:

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

**Tipp:** Sie können auch **ba rr** als Alias für den längeren
Befehlsnamen **ba retrieve-report** verwenden.

### Services für alle Organisationen aktivieren und inaktivieren

Sie können die Anzeige eines Service im {{site.data.keyword.Bluemix_notm}}-Katalog für
alle Organisationen aktivieren oder inaktivieren.

* Geben Sie den folgenden Befehl ein, um die Sichtbarkeit eines Service im
{{site.data.keyword.Bluemix_notm}}-Katalog für alle Organisationen zu aktivieren:

```
cf ba enable-service-plan <plan_identifier>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">Der Name oder die GUID des Service, der aktiviert werden soll. Wenn der eingegebene Servicename nicht eindeutig ist, werden Sie mit Serviceplänen zur Auswahl eines Service aufgefordert.</dd>
</dl>

**Tipp:** Sie können auch **ba esp** als Alias für den längeren
Befehlsnamen **ba enable-service-plan** verwenden.

* Geben Sie den folgenden Befehl ein, um die Sichtbarkeit eines Service im
{{site.data.keyword.Bluemix_notm}}-Katalog für alle Organisationen zu inaktivieren:

```
cf ba disable-service-plan <plan_identifier>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">Der Name oder die GUID des Service, der inaktiviert werden soll. Wenn der eingegebene Servicename nicht eindeutig ist, werden Sie mit Serviceplänen zur Auswahl eines Service aufgefordert.</dd>
</dl>

**Tipp:** Sie können auch **ba dsp** als Alias für den längeren
Befehlsnamen **ba disable-service-plan** verwenden.

### Sichtbarkeit von Services für Organisationen hinzufügen, entfernen und bearbeiten

Sie können eine Organisation in der Liste der Organisationen, für die ein bestimmter Service im
{{site.data.keyword.Bluemix_notm}}-Katalog sichtbar ist, hinzufügen oder entfernen. Sie können
die Liste der Services, die für bestimmte Organisationen im {{site.data.keyword.Bluemix_notm}}-Katalog
sichtbar sind, auch bearbeiten und ersetzen.

* Geben Sie den folgenden Befehl ein, um einer Organisation zu gestatten, einen bestimmten Service
im {{site.data.keyword.Bluemix_notm}}-Katalog anzuzeigen:

```
cf ba add-service-plan-visibility <plan_identifier> <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">Der Name oder die GUID des Service, für den die Sichtbarkeit hinzugefügt werden soll. Wenn der eingegebene Servicename nicht eindeutig ist, werden Sie mit Serviceplänen zur Auswahl eines Service aufgefordert.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">Der Name oder die GUID der {{site.data.keyword.Bluemix_notm}}-Organisation, die der Sichtbarkeitsliste des Service hinzugefügt werden soll.</dd>
</dl>

**Tipp:** Sie können auch **ba aspv** als Alias für den längeren
Befehlsnamen **ba add-service-plan-visibility** verwenden.

* Geben Sie den folgenden Befehl ein, um die Sichtbarkeit eines Service im
{{site.data.keyword.Bluemix_notm}}-Katalog für eine Organisation zu entfernen:

```
cf ba remove-service-plan-visibility <plan_identifier> <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">Der Name oder die GUID des Service, für den die Sichtbarkeit entfernt werden soll. Wenn der eingegebene Servicename nicht eindeutig ist, werden Sie mit Serviceplänen zur Auswahl eines Service aufgefordert.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">Der Name oder die GUID der {{site.data.keyword.Bluemix_notm}}-Organisation, die aus der Sichtbarkeitsliste des Service entfernt werden soll.</dd>
</dl>

**Tipp:** Sie können auch **ba rspv** als Alias für den längeren
Befehlsnamen **ba remove-service-plan-visibility** verwenden.

* Verwenden Sie den folgenden Befehl, um alle vorhandenen sichtbaren Services für eine Organisation oder mehrere Organisationen zu ersetzen:

```
cf ba edit-service-plan-visibilities <plan_identifier> <organization_1> <optional_organization_2>
```
{: codeblock}

**Hinweis:** Dieser Befehl ersetzt vorhandene sichtbare Services für die angegebenen Organisationen
durch den Service, den Sie im Befehl angeben.

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">Der Name oder die GUID des Service, der sichtbar gemacht werden soll. Wenn der eingegebene Servicename nicht eindeutig ist, werden Sie mit Serviceplänen zur Auswahl eines Service aufgefordert.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">Der Name oder die GUID der {{site.data.keyword.Bluemix_notm}}-Organisation, für die die Sichtbarkeit hinzugefügt werden soll. Sie können
die Sichtbarkeit des Service für mehrere Organisationen aktivieren, indem Sie weitere Organisationsnamen oder GUIDs im Befehl angeben.</dd>
</dl>

**Tipp:** Sie können auch **ba espv** als Alias für den längeren
Befehlsnamen **ba edit-service-plan-visibility** verwenden.

### Mit Service-Brokern arbeiten

Mit den folgenden Befehlen können Sie alle Service-Broker auflisten, einen Service-Broker hinzufügen oder löschen oder einen Service-Broker aktualisieren.

* Sie können alle Servicebroker mit dem folgenden Befehl auflisten:

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

* Sie können einen Service-Broker hinzufügen, sodass Sie Ihrem
{{site.data.keyword.Bluemix_notm}}-Katalog einen angepassten Service hinzufügen können, indem Sie den folgenden Befehl eingeben:

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

* Sie können einen Service-Broker löschen, um den angepassten Service aus Ihrem
{{site.data.keyword.Bluemix_notm}}-Katalog zu entfernen, indem Sie den folgenden Befehl eingeben:

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

* Sie können einen Service-Broker aktualisieren, indem Sie den folgenden Befehl eingeben:

`cf ba update-service-broker <broker_name> <user_name> <password> <broker_url>`
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
