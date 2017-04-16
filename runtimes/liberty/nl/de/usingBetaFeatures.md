---

copyright:
  years: 2015, 2016
lastupdated: "2016-06-10"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Beta-Features verwenden
{: #using_beta_features}

Die Beta-Features von Liberty ermöglichen den vorzeitigen Zugriff auf die neuen Funktionen und Programmiermodelle, die in einem zukünftigen Liberty-Release enthalten sein können. Die meisten Beta-Features können auch in Anwendungen verwendet werden, die in Bluemix implementiert sind.

**Wichtig**: Die Beta-Features dienen nur zu Entwicklungs- und Testzwecken und dürfen in Produktionsumgebungen nicht verwendet werden. Umfassende Nutzungsbedingungen finden Sie in der
[ Lizenzvereinbarung für Betaversionen](http://public.dhe.ibm.com/ibmdl/export/pub/software/websphere/wasdev/downloads/wlp/beta/lafiles/en.html).

In Bluemix verfügbare Liberty-Beta-Features
<table>
<tr>
<th align="left">Feature</th>
<th align="left">Feature</th>
<th align="left">Feature</th>
<th align="left">Feature</th>
</tr>

<tr>
<td>bluemixLogCollector-1.1</td>
<td>httpWhiteboard-1.0</td>
<td>logstashCollector-1.1</td>
<td>osgiBundle-1.0</td>
</tr>
</table>

Führen Sie die folgenden Schritte aus, um die Liberty-Beta-Features in Bluemix verwenden zu können:

1. [Implementieren Sie ein Serververzeichnis oder einen paketierten Server](optionsForPushing.html) mit mindestens einem in der Datei 'server.xml' aktivierten Beta-Feature, wie im folgenden Beispiel gezeigt:
```
    <server>
        <featureManager>
            <feature>jsp-2.3</feature>
            <feature>bluemixLogCollector-1.1</feature>
        </featureManager>
    </server>
```
{: #codeblock}

2.  Setzen Sie die Umgebungsvariable **IBM_LIBERTY_BETA** auf **true**. Diese Variable weist das
Liberty-Buildpack an, die Beta-Features zu installieren und für Ihre Anwendung zu aktivieren.  Beispiel:
  * Verwendung des Befehlszeilentools 'cf':
```
       $ cf set-env <yourappname> IBM_LIBERTY_BETA true
```
{: #codeblock}

  * Alternativ Verwendung der Datei 'manifest.yml':
```
      env:
          IBM_LIBERTY_BETA: "true"
```

3. Setzen Sie die Umgebungsvariable **JBP_CONFIG_LIBERTY** auf **"version: +"**. Diese Variable aktiviert die [monatliche Liberty-Laufzeit](buildpackDefaults.html#liberty_versions), die Beta-Features unterstützt. Beispiel:
  * Verwendung des Befehlszeilentools 'cf':
```
       $ cf set-env <yourappname> JBP_CONFIG_LIBERTY "version: +"
```
{: #codeblock}

  * Alternativ Verwendung der Datei 'manifest.yml':
```
      env:
          JBP_CONFIG_LIBERTY: "version: +"
```

Wenn Sie die Beta-Features für eine bestehende Anwendung aktivieren, müssen Sie für Ihre Anwendung nach dem Einstellen der Umgebungsvariablen ein erneutes Staging durchführen.

{: #codeblock}

# Zugehörige Links
{: #rellinks}
## Allgemein
{: #general}
* [Liberty-Laufzeit](index.html)
* [Übersicht über das Liberty-Profil](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
