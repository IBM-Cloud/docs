---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Beta-Features verwenden
{: #using_beta_features}

*Letzte Aktualisierung: 23. März 2016*

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
<td>cloudant-1.0</td>
<td>httpWhiteboard-1.0</td>
<td>osgiBundle-1.0</td>
<td>passwordUtilities-1.0</td>
</tr>
</table>

Führen Sie einen der folgenden Schritte aus, um die Liberty-Beta-Features in Bluemix verwenden zu können:

1. [Implementieren Sie ein Serververzeichnis oder einen paketierten Server](optionsForPushing.html) mit mindestens einem in der Datei 'server.xml' aktivierten Beta-Feature, wie im folgenden Beispiel gezeigt:
```
    <server>
        <featureManager>
            <feature>jsp-2.3</feature>
            <feature>passwordUtilities-1.0</feature>
        </featureManager>
    </server>
```
{: #codeblock}

2.  Setzen Sie die Umgebungsvariable IBM_LIBERTY_BETA auf **true**. Diese Variable weist das
Liberty-Buildpack an, die Beta-Features zu installieren und für Ihre Anwendung zu aktivieren.  Lesen Sie folgende Beispiele:
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
{: #codeblock}

# Zugehörige Links
## Allgemein
* [Liberty-Laufzeit](index.html)
* [Übersicht über das Liberty-Profil](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
