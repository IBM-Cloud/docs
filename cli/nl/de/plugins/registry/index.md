---



copyright:

  years: 2017

lastupdated: "2017-03-20"


---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.registrylong_notm}}-Befehlszeilenschnittstelle (CLI)
{: #containerregcli}

Die Befehlszeilenschnittstelle (CLI) von {{site.data.keyword.registrylong}} ist ein Plug-in, über das Sie Ihre Registry-Ressourcen wie Namensbereiche und Images in Ihrer Organisation verwalten können.
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
 <td>[bx cr api](#bx-cr-api)</td>
 <td>[bx cr info](#bx-cr-info)</td>
 <td>[bx cr image-inspect](#bx-cr-image-inspect)</td>
 <td>[bx cr image-list](#bx-cr-image-list)</td>
 <td>[bx cr image-rm](#bx-cr-image-rm)</td>
 </tr>
 <tr>
 <td>[bx cr login](#bx-cr-login)</td>
 <td>[bx cr namespace-add](#bx-cr-namespace-add)</td>
 <td>[bx cr namespace-list](#bx-cr-namespace-list)</td>
 <td>[bx cr namespace-rm](#bx-cr-namespace-rm)</td>
 </tr></tbody></table>


## bx cr api
Gibt die Details zu dem Registry-API-Endpunkt zurück, an dem die Befehle ausgeführt werden. 

```
bx cr api
```
{: codeblock}


## bx cr info
Zeigt den Namen und die Organisation (org) der Registry an, bei der Sie angemeldet sind. 

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
<dd>(Optional) Formatiert die Ausgabeelemente unter Verwendung einer Go-Vorlage. </dd>
<dt>IMAGE</dt>
<dd>Der vollständige {{site.data.keyword.Bluemix_short}}-Registry-Pfad zu dem Image, das Sie untersuchen wollen. Wenn in dem Image-Pfad kein Tag angegeben wird, wird das Image mit dem Tag `latest` untersucht. Sie können mehrere Images untersuchen, indem Sie die einzelnen privaten {{site.data.keyword.Bluemix_short}}-Registry-Pfade in dem Befehl jeweils durch ein Leerzeichen getrennt auflisten. </dd>
</dl>


## bx cr image-list
Zeigt alle Images in Ihrer {{site.data.keyword.Bluemix_short}}-Organisation an. 

```
 bx cr image-list [--no-trunc] [-q, --quiet] [--include-ibm] [--format FORMAT]
```
{: codeblock}

**Parameter**
<dl>
<dt>--no-trunc</dt>
<dd>(Optional) Gibt an, die Ausgabe nicht abzuschneiden. </dd>
<dt>-q, --quiet</dt>
<dd>(Optional) Zeigt eine eindeutige Kennung für das Image im folgenden Format an: 'repository:tag'. </dd>
<dt>--include-ibm</dt>
<dd>(Optional) Schließt von IBM bereitgestellte öffentliche Images in die Ausgabe ein. Ohne diese Option werden nur private Images aufgelistet. </dd>
<dt>--format FORMAT</dt>
<dd>(Optional) Formatiert die Ausgabeelemente unter Verwendung einer Go-Vorlage. </dd>
</dl>


## bx cr image-rm
Löscht ein angegebenes Image aus Ihrer Registry. 

```
bx cr image-rm IMAGE [IMAGE]
```
{: codeblock}

**Parameter**
<dl>
<dt>IMAGE</dt>
<dd>Der vollständige {{site.data.keyword.Bluemix_short}}-Registry-Pfad zu dem Image, das Sie entfernen wollen. Wenn der Image-Pfad nicht mit einem Tag versehen wird, wird standardmäßig das Image mit dem Tag `latest` entfernt. Sie können mehrere Images entfernen, indem Sie die einzelnen privaten {{site.data.keyword.Bluemix_short}}-Registry-Pfade in dem Befehl jeweils durch ein Leerzeichen getrennt auflisten. </dd>
</dl>


## bx cr login
Wenn Docker installiert ist, führt dieser Befehl den Befehl `docker login` für die Registry aus. Der Befehl `docker login` ist erforderlich, um die Befehle `docker push` und `docker pull` für die Registry ausführen zu können. Dieser Befehl ist nicht erforderlich, um andere `bx cr`-Befehle auszuführen. Wenn Docker nicht installiert ist, gibt dieser Befehl eine Fehlernachricht zurück. 

```
bx cr login
```
{: codeblock}


## bx cr namespace-add
Fügt einen Namensbereich in Ihrer Bluemix-Organisation hinzu.  

```
bx cr namespace-add NAMESPACE
```
{: codeblock}

**Parameter**
<dl>
<dt>NAMESPACE</dt>
<dd>Der Namensbereich, den Sie hinzufügen wollen. Der Namensbereich muss über alle {{site.data.keyword.Bluemix_short}}-Organisationen hinweg eindeutig sein. </dd>
</dl>


## bx cr namespace-list
Zeigt alle Namensbereiche Ihrer {{site.data.keyword.Bluemix_short}}-Organisation an. 

```
bx cr namespace-list
```
{: codeblock}


## bx cr namespace-rm
Entfernt einen Namensbereich aus Ihrer {{site.data.keyword.Bluemix_short}}-Organisation. Images in diesem Namensbereich werden gelöscht, wenn der Namensbereich entfernt wird. 

```
bx cr namespace-rm NAMESPACE
```
{: codeblock}

**Parameter**
<dl>
<dt>NAMESPACE</dt>
<dd>Der Namensbereich, den Sie entfernen wollen. </dd>
</dl>
