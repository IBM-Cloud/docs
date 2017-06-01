---



copyright:

  years: 2017

lastupdated: "2017-05-12"


---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.registrylong_notm}}-Befehlszeilenschnittstelle (CLI)
{: #containerregcli}

Die {{site.data.keyword.registrylong}}-Befehlszeilenschnittstelle (CLI) ist ein Plug-in für die Verwaltung der Registry und deren Ressourcen für Ihr Konto.
{: shortdesc}

**Voraussetzungen**
* Melden Sie sich vor der Ausführung von Registry-Befehlen bei {{site.data.keyword.Bluemix_short}} mit dem Befehl `bx login` an, um ein {{site.data.keyword.Bluemix_short}}-Zugriffstoken zu generieren und Ihre Sitzung zu authentifizieren.

<table summary="Container-Registry verwalten">
<caption>Tabelle 1. Befehle zur Verwaltung der {{site.data.keyword.registryshort}} in {{site.data.keyword.Bluemix_short}}
</caption>
 <thead>
 <th colspan="5">Befehle zur Verwaltung der Registry</th>
 </thead>
 <tbody>
 <tr>
 <td>[bx cr api](#bx_cr_api)</td>
 <td>[bx cr info](#bx-cr-info)</td>
 <td>[bx cr image-inspect](#bx-cr-image-inspect)</td>
 <td>[bx cr image-list (bx cr images)](#bx-cr-image-list)</td>
 <td>[bx cr image-rm](#bx-cr-image-rm)</td>
 </tr>
 <tr>
 <td>[bx cr login](#bx-cr-login)</td>
 <td>[bx cr namespace-add](#bx-cr-namespace-add)</td>
 <td>[bx cr namespace-list (bx cr namespaces)](#bx-cr-namespace-list)</td>
 <td>[bx cr namespace-rm](#bx-cr-namespace-rm)</td>
 <td>[bx cr token-add](#bx-cr-token-add)</td>
 </tr>
 <tr>
 <td>[bx cr token-get](#bx-cr-token-get)</td>
 <td>[bx cr token-list (bx cr tokens)](#bx-cr-token-list)</td>
 <td>[bx cr token-rm](#bx-cr-token-rm)</td>
 </tr>
 </tbody></table>



## bx cr api
{: #bx_cr_api}

Gibt die Details zu dem Registry-API-Endpunkt zurück, an dem die Befehle ausgeführt werden.

```
bx cr api
```
{: codeblock}


## bx cr info
Zeigt den Namen und das Konto der Registry an, bei der Sie angemeldet sind.

```
bx cr info
```
{: codeblock}


## bx cr image-inspect
Zeigt Details zu einem bestimmten Image an.

```
bx cr image-inspect [--format FORMAT] IMAGE [IMAGE]
```
{: codeblock}

**Parameter**


<dl>
<dt>--format FORMAT</dt>
<dd>(Optional) Formatiert die Ausgabeelemente unter Verwendung einer Go-Vorlage. 


</dd>
<dt>IMAGE</dt>
<dd>Der vollständige {{site.data.keyword.Bluemix_short}}-Registry-Pfad zu dem Image, das Sie untersuchen möchten (Format: `namespace/image:tag`). Wenn in dem Image-Pfad kein Tag angegeben wird, wird das Image mit dem Tag `latest` untersucht. Sie können mehrere Images untersuchen, indem Sie die einzelnen privaten {{site.data.keyword.Bluemix_short}}-Registry-Pfade in dem Befehl jeweils durch ein Leerzeichen getrennt auflisten.</dd>
</dl>


## bx cr image-list (bx cr images)
Zeigt alle Images in Ihrem {{site.data.keyword.Bluemix_short}}-Konto an.

```
 bx cr image-list [--no-trunc] [-q, --quiet] [--include-ibm] [--format FORMAT]
```
{: codeblock}

**Parameter**
<dl>
<dt>--no-trunc</dt>
<dd>(Optional) Gibt an, die Imageauszüge nicht abzuschneiden.</dd>
<dt>-q, --quiet</dt>
<dd>(Optional) Jedes Image ist in folgendem Format aufgelistet: `repository:tag`.</dd>
<dt>--include-ibm</dt>
<dd>(Optional) Schließt von IBM bereitgestellte öffentliche Images in die Ausgabe ein. Ohne diese Option werden standardmäßig nur private Images aufgelistet.</dd>
<dt>--format FORMAT</dt>
<dd>(Optional) Formatiert die Ausgabeelemente unter Verwendung einer Go-Vorlage. 


</dd>

</dl>


## bx cr image-rm
Löscht ein oder mehrere angegebene Images aus Ihrer Registry.

```
bx cr image-rm IMAGE [IMAGE]
```
{: codeblock}

**Parameter**
<dl>
<dt>IMAGE</dt>
<dd>Der vollständige {{site.data.keyword.Bluemix_short}}-Registry-Pfad zu dem Image, das Sie entfernen möchten (Format: `namespace/image:tag`). Wenn der Image-Pfad nicht mit einem Tag versehen wird, wird standardmäßig das Image mit dem Tag `latest` entfernt. Sie können mehrere Images entfernen, indem Sie die einzelnen privaten {{site.data.keyword.Bluemix_short}}-Registry-Pfade in dem Befehl jeweils durch ein Leerzeichen getrennt auflisten.</dd>
</dl>


## bx cr login
Führt den Befehl `docker login` für die Registry aus. Der Befehl `docker login` ist erforderlich, um die Befehle `docker push` und `docker pull` für die Registry ausführen zu können. Dieser Befehl ist nicht erforderlich, um andere `bx cr`-Befehle auszuführen. Wenn Docker nicht installiert ist, gibt dieser Befehl eine Fehlernachricht zurück.

```
bx cr login
```
{: codeblock}


## bx cr namespace-add
Fügt einen Namensbereich zu Ihrem {{site.data.keyword.Bluemix_short}}-Konto hinzu.

```
bx cr namespace-add NAMESPACE
```
{: codeblock}

**Parameter**
<dl>
<dt>NAMESPACE</dt>
<dd>Der Namensbereich, den Sie hinzufügen wollen. Der Namensbereich muss für alle {{site.data.keyword.Bluemix_short}}-Konten in derselben Region eindeutig sein.</dd>
</dl>


## bx cr namespace-list (bx cr namespaces)
Zeigt alle Namensbereiche an, die Ihrem {{site.data.keyword.Bluemix_short}}-Konto angehören.

```
bx cr namespace-list
```
{: codeblock}


## bx cr namespace-rm
Entfernt einen Namensbereich aus Ihrem {{site.data.keyword.Bluemix_short}}-Konto. Images in dieser Namensbereich werden gelöscht, wenn der Namensbereich entfernt wird.

```
bx cr namespace-rm NAMESPACE
```
{: codeblock}

**Parameter**
<dl>
<dt>NAMESPACE</dt>
<dd>Der Namensbereich, den Sie entfernen wollen.</dd>
</dl>


## bx cr token-add
Fügt ein Token hinzu, das Sie verwenden können, um den Zugriff auf eine Registry zu steuern.

```
bx cr token-add [--description VALUE] [-q, --quiet] [--non-expiring] [--readwrite]
```

{: codeblock}


**Parameter**
<dl>
<dt>--description VALUE</dt>
<dd>(Optional) Gibt den Wert als Beschreibung für das Token an, das beim Ausführen von `bx cr token-list` angezeigt wird. Wenn das Token automatisch vom IBM Bluemix Container-Service erstellt wird, wird als Beschreibung der Kubernetes-Clustername festgelegt. In diesem Fall wird das Token automatisch entfernt, wenn Ihr Cluster entfernt wird.</dd>
<dt>-q, --quiet</dt>
<dd>(Optional) Zeigt nur das Token ohne den umgebenden Text an.</dd>
<dt>--non-expiring</dt>
<dd>(Optional) Erstellt ein Token mit Zugriff, der nicht abläuft. Ist dieser Parameter nicht festgelegt, läuft der Zugriff über ein Token standardmäßig nach 24 Stunden ab.</dd>
<dt>--readwrite</dt>
<dd>(Optional) Erstellt ein Token, das Lese- und Schreibzugriff gewährt. Ohne diese Option ist der Zugriff standardmäßig schreibgeschützt.</dd>
</dl>


## bx cr token-get
Ruft das angegebene Token aus der Registry ab.

```
bx cr token-get TOKEN
```

{: codeblock}

**Parameter**
<dl>
<dt>TOKEN</dt>
<dd>(Optional) Die eindeutige ID des Tokens, das Sie abrufen möchten.</dd>
</dl>


## bx cr token-list (bx cr tokens)
Zeigt alle Token für Ihr {{site.data.keyword.Bluemix_short}}-Konto an.

```
bx cr token-list --format FORMAT
```
{: codeblock}

**Parameter**
<dl>
<dt>--format FORMAT</dt>
<dd>(Optional) Formatiert die Ausgabeelemente unter Verwendung einer Go-Vorlage. 


</dd>
</dl>


## bx cr token-rm
Entfernt einen oder mehrere angegebene Token.

```
bx cr token-rm TOKEN [TOKEN]
```
{: codeblock}

**Parameter**
<dl>
<dt>TOKEN</dt>
<dd>(Optional) TOKEN kann entweder das Token selbst sein oder die eindeutige ID des Tokens, wie in `bx cr token-list` dargestellt. Es können mehrere Token angegeben sein und sie müssen durch ein Leerzeichen getrennt werden.</dd>
</dl>


</dd>
</dl>


