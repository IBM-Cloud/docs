# bl-Befehle

*Letzte Aktualisierung:* 13. November 2015

Wenn Sie eine Node.js-Anwendung erstellen, können Sie Bluemix™ Live Sync dazu verwenden, die Anwendungsinstanz ohne großen Zeitaufwand in Bluemix zu aktualisieren
und Entwicklungsprozesse wie auf dem Desktop durchzuführen, ohne dass eine erneute Bereitstellung erforderlich ist. Wenn Sie eine Änderung vornehmen, ist diese Änderung sofort in der aktiven Bluemix-Anwendung sichtbar. Die Bluemix Live Sync-Befehlszeilenschnittstelle heißt *bl*. 

Mithilfe der Befehle der **bl**-Befehlszeilenschnittstelle können Sie die folgenden Aufgaben ausführen:


* Eine in Bluemix ausgeführte Anwendung starten und stoppen. 
* Ein neues cloudbasiertes Projekt über den Desktop erstellen.

* Änderungen auf Ihrem Desktop mit dem cloudbasierten Projektarbeitsbereich und der aktiven Anwendung in Bluemix synchronisieren. 
* Die Liste der Projekte anzeigen, die für die Synchronisation verfügbar sind. 
* Den Status von aktiven Anwendungen anzeigen. 

Weitere Informationen zum Herunterladen und Verwenden des Befehls 'bl' finden Sie in der Veröffentlichung [Bluemix Live Sync](https://www.ng.bluemix.net/docs/manageapps/bluemixlive.html#bluemixlive). 

## bl-Befehle

Die Bluemix Live Sync-Befehlszeile **bl** weist die folgende Syntax auf: 

``` bl command [arguments][options] [--help]```

### Befehle
<dl>
<dt>login, l</dt>
<dd>Anmeldung an Bluemix. </dd>
<dt>logout, lo</dt>
<dd>Abmeldung des Benutzers.</dd>
<dt>sync, s</dt>
<dd>Synchronisationsprozess zwischen Desktop und Server starten. </dd>
<dt>create, c</dt>
<dd>Privates Projekt erstellen, mit dem Git-Repository in diesem Verzeichnis verknüpfen und den Inhalt in Bluemix bereitstellen. </dd>
<dt>projects, p</dt>
<dd>Alle für die Synchronisation verfügbaren Projekte auflisten.</dd>
<dt>start, st</dt>
<dd>Anwendungsinstanz in Bluemix starten. </dd>
<dt>stop, sp</dt>
<dd>Anwendungsinstanz in Bluemix stoppen.</dd>
<dt>status, ss</dt>
<dd>Status der aktiven Anwendungsinstanz in Bluemix auflisten. </dd>
</dl>

### Argumente
<dl>
<dd>Argumente für den Befehl.</dd>
</dl>

### Optionen
<dl>
<dd>Optionen für den Befehl.</dd>
</dl>

### Globale Optionen
<dl>
<dt>--help</dt>
<dd>Hilfetextseite für den angegebenen Befehl anzeigen. </dd>
<dt>--verbose</dt>
<dd>Ausführliche Protokollierung aktivieren.</dd>
</dl>

**Hinweis:** Wenn ein Argument oder eine Option ein Leerzeichen enthält, schließen Sie den Wert in doppelte Anführungszeichen ein. 
