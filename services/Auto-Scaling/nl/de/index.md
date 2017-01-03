---

 

copyright:

  years: 2015，2016
lastupdated: "2016-11-02"  
 

---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.autoscaling}}-Service - Einführung
{: #autoscaling}
Letzte Aktualiserung: 02. November 2016
{: .last-updated}

In {{site.data.keyword.Bluemix_notm}} kann die Anwendungskapazität automatisch verwaltet werden. Mithilfe des {{site.data.keyword.autoscaling}}-Service kann die Verarbeitungsleistung der Anwendung automatisch erhöht oder reduziert werden. Die Anzahl der Anwendungsinstanzen wird auf der Basis der von Ihnen definierten {{site.data.keyword.autoscaling}}-Richtlinie dynamisch angepasst.
{:shortdesc} 

## Inhalte
  * [{{site.data.keyword.autoscaling}}-Service in {{site.data.keyword.Bluemix_notm}}](#as-service) verwenden
  * [Node.js-Apps mit dem {{site.data.keyword.autoscaling}}-Service konfigurieren](#node-asagent)
  * [{{site.data.keyword.autoscaling}}-Service über RESTful-API verwalten](#RESTAPI)
  * [{{site.data.keyword.autoscaling}}-Service über {{site.data.keyword.autoscaling}}-CLI verwalten](#CLI)
  * [Richtlinienfelder für den {{site.data.keyword.autoscaling}}-Service](#policy_fields)
  * [Fehlernachrichten](#err_msg)

## Verwendung des {{site.data.keyword.autoscaling}}-Service in {{site.data.keyword.Bluemix_notm}}
{: #as-service}

Um den {{site.data.keyword.autoscaling}}-Service verwenden zu können, müssen Sie die folgenden Schritte ausführen:

1. Klicken Sie im {{site.data.keyword.Bluemix_notm}}-Dashboard auf die Option *Service oder API hinzufügen* und wählen Sie anschließend im Abschnitt 'DevOps ' des Servicekatalogs den {{site.data.keyword.autoscaling}}-Service aus. Es wird ein neues Fenster für eine Übersicht des {{site.data.keyword.autoscaling}}-Service angezeigt.
2. Wählen Sie die Anwendung aus, an die Sie den {{site.data.keyword.autoscaling}}-Service binden möchten, und klicken Sie auf *Erstellen*. <br/>
*Hinweis:* Sie können nur einen einzigen {{site.data.keyword.autoscaling}}-Service an eine Anwendung binden. Wählen Sie die Anwendung in diesem Schritt nicht aus, wenn sie bereits mit einem anderen {{site.data.keyword.autoscaling}}-Service verbunden ist. Andernfalls wird der Fehler CWSCV2004E ausgegeben.<br/>Das Fenster 'Erneutes Staging für Anwendung' wird angezeigt.
3. Klicken Sie im Fenster 'Erneutes Staging für Anwendung' auf *Erneutes Staging*, um für Ihre Anwendung ein erneutes Staging durchzuführen, bevor Sie den neuen {{site.data.keyword.autoscaling}}-Service verwenden, den Sie soeben hinzugefügt haben. <br/><ul><li>Für Liberty-Anwendungen ist {{site.data.keyword.autoscaling}} nach einem erneuten Staging für Anwendungen automatisch konfiguriert und betriebsbereit.</li> <li>Für Node.js-Anwendungen müssen Sie Ihren Anwendungscode aktualisieren, um den {{site.data.keyword.autoscaling}}-Service zu aktivieren, bevor Sie die Anwendung per Push-Operation auf {{site.data.keyword.Bluemix_notm}} übertragen. Weitere Details finden Sie unter [Node.js-Apps mit dem {{site.data.keyword.autoscaling}}-Service konfigurieren](index.html#node_asagent).</ul><br/>
Nachdem das erneute Staging der Anwendung abgeschlossen ist, können Sie mit der Konfiguration des {{site.data.keyword.autoscaling}}-Service für Ihre Anwendung beginnen.
4. Für die Konfiguration von {{site.data.keyword.autoscaling}} für eine Anwendung müssen Sie in der {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle auf Ihre Anwendung klicken, an die der {{site.data.keyword.autoscaling}}-Service gebunden ist.
5. Klicken Sie im Serviceabschnitt des Dashboards auf das Symbol für *Auto-Scaling*.
6. Falls Sie die {{site.data.keyword.autoscaling}}-Richtlinie für die Anwendung noch nicht definiert haben, definieren Sie sie durch Klicken auf die Option *Richtlinie für {{site.data.keyword.autoscaling}} erstellen*.

Nun können Sie die {{site.data.keyword.autoscaling}}-Richtlinie konfigurieren, die Metrikstatistiken anzeigen oder den Skalierungsverlauf für die Anwendung anzeigen.
<dl>
<dt>Richtlinienkonfiguration</dt>
<dd>Dieser Abschnitt enthält Informationen zur Erstellung oder Bearbeitung der Skalierungsregeln für die Angabe der Bedingungen, unter denen bestimmte Skalierungsaktivitäten ausgelöst werden sollen.<ul>
<li> Bei Liberty for Java™-Anwendungen können Sie Skalierungsregeln für Heapspeicher, Hauptspeicher, Antwortzeit und Durchsatz definieren.  
<li> Bei Node.js-Anwendungen können Sie Skalierungsregeln für Heapspeicher, Hauptspeicher und Durchsatz definieren.
<li> Bei Ruby-Anwendungen können Sie Skalierungsregeln für den Hauptspeicher definieren.</ul>
*Hinweis:* Sie können mehrere Skalierungsregeln für mehr als einen Metriktyp definieren. Der {{site.data.keyword.autoscaling}}-Service ermittelt jedoch keine Konflikte zwischen den Skalierungsrichtlinien. Wenn Sie die Skalierungsrichtlinie definieren, müssen Sie sicherstellen, dass die verschiedenen Skalierungsrichtlinien nicht miteinander in Konflikt geraten. Andernfalls schwankt die Gesamtzahl der Instanzen möglicherweise, da für die Anwendung in rascher Folge Scale-in- und Scale-out-Aktionen durchgeführt werden.<br/><br/>
Wenn die Workload Ihrer Anwendung sich zur Spitzenzeit und zur Zeit ohne Nutzung drastisch verändert, können Sie einen Skalierungszeitplan erstellen, um die unterschiedlichen Skalierungsanforderungen für unterschiedliche Zeiträume abzuwickeln. Verwenden Sie für die Definition der Referenzversion der Anzahl der Anwendungsinstanzen den in einem Zeitplan angegebenen Parameter 'Anzahl der Instanzen - Minimum'; gleichzeitig gelten die dynamischen Skalierungsregeln für den Zeitplan zur Auslösung der Scale-in- und Scale-out-Aktionen weiterhin.</dd>
<dt>Statistiken zu Metriken</dt>
<dd>Es werden für die Instanzen Ihrer Anwendung die Statistiken zu den Metriken angezeigt. Sie können die Durchschnittsstatistik sehen und eine bestimmte Instanz auswählen,
um deren Statistikdaten anzuzeigen.</dd>
<dt>Skalierungsverlauf</dt>
<dd>Es wird der Skalierungsverlauf für Ihre Anwendungen angezeigt.<ul>
<li> Vergangene Woche:
Es wird der Skalierungsverlauf für die vergangene Woche angezeigt.
<li> Vergangener Monat:
Es wird der Skalierungsverlauf für den vergangenen Monat angezeigt.
<li> Benutzerdefinierter Bereich:
Sie können einen Zeitraum festlegen.</ul>
*Hinweis:* Durch die Auswahl von Skalierungsstatus bzw. der Option zum Skalieren (Anzahl reduzieren/erhöhen) können Sie den Protokollsatz filtern.</dd>
</dl>


## Node.js-Apps mit dem {{site.data.keyword.autoscaling}}-Service konfigurieren
{: #node-asagent}

Um den {{site.data.keyword.autoscaling}}-Service mit Ihren Node.js-Apps zu aktivieren, müssen Sie, abgesehen von den Schritten zur Servicebereitstellung und zur Bindung, auch die folgenden Schritte ausführen, bevor Sie die App per Push-Operation an {{site.data.keyword.Bluemix_notm}} übertragen.

1. Aktualisieren Sie die Datei 'package.json' mit den folgenden Schritten: <ol><li>Erstellen Sie einen Abhängigkeitseintrag für `blumix-autoscaling-agent`, zum Beispiel `"bluemix-autoscaling-agent": "*"`.<br/><li>(Optional) Legen Sie ein Limit für den Heapspeicher im Abschnitt `scripts` auf Grundlage des Speichers fest, der Ihrer App zugeordnet ist. Zum Beispiel: `"start": "node --max-old-space-size=600 app.js"`. .<br/>*Hinweis:* Legen Sie einen Wert für `max-old-space-size` fest, wenn Sie das Skalieren auf Grundlage der Heapspeichernutzung auslösen möchten. Wenn der Wert beim Starten Ihrer Anwendung nicht festgelegt ist, wird das Standardlimit für den Heapspeicher von Node.js verwendet. Das Standardlimit beträgt 1,4 GB und wird unabhängig davon verwendet, wie viel Speicher Ihrer App zugewiesen wurde. Dies kann zu falschen Entscheidungen beim automatischen Skalieren führen.<br/>
```
{
	"name": "NodejsStarterApp",
	"version": "0.0.1",
	"description": "A sample nodejs app for Bluemix",
	"scripts": {
		"start": "node --max-old-space-size=600 app.js"
	},
	"dependencies": {
		"bluemix-autoscaling-agent": "*"
	},
	"repository": {},
	"engines": {
		"node": "0.12.x"
	} 
}
```
</ol>
2. Aktualisieren Sie Ihre Hauptdatei, um die Agentendeklaration `var as_agent = require('bluemix-autoscaling-agent');` hinzuzufügen. Das folgende Code-Snippet zeigt eine vollständige js-Einstiegsdatei mit der Auto-Scaling-Agentendeklaration.<br/>
```
var agent = require('bluemix-autoscaling-agent');
var http = require('http');
var server = http.createServer(function handler(req, res) {
	console.log("Hello!");
	
	}).listen(process.env.PORT || 3000);
console.log('App is listening on port 3000');
```

## {{site.data.keyword.autoscaling}}-Service über RESTful-API verwalten 
{: #RESTAPI}

Die {{site.data.keyword.autoscaling}}-RESTful-API bietet neben der Bluemix-Benutzerschnittstelle eine alternative Möglichkeit zur Verwaltung des {{site.data.keyword.autoscaling}}-Service und unterstützt ferner den Abruf und die Analyse von Skalierungsdaten. Sie bietet ähnliche Funktionen wie beispielsweise die Erstellung einer Richtlinie und das Abrufen eines Skalierungsverlaufs wie in der {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle mit API.

Für die Verwendung der {{site.data.keyword.autoscaling}}-RESTful-API zur Verwaltung des {{site.data.keyword.autoscaling}}-Service führen Sie folgende Schritte aus, um die Voraussetzungen zu erfüllen: Binden Sie den {{site.data.keyword.autoscaling}}-Service mit Ihrer Anwendung wie im vorigen Abschnitt angegeben, fordern Sie `AccessToken`, die URL des {{site.data.keyword.autoscaling}}-API-Servers und die `app_id` der Anwendung an, für die Sie ein Scale-in oder Scale-out durchführen möchten.

1. Aus Sicherheitsgründen muss in jedem Anforderungsheader der {{site.data.keyword.autoscaling}}-RESTful-API ein ordnungsgemäßes `AccessToken`, das über die Prozedur CloudFoundry UAA abgerufen wurde, im `Authorization`-Header zur Verfügung gestellt werden, um die erforderliche Validierung der Anforderung anzugeben. Werden diese `AccessToken`-Ergebnisse nicht eingehalten, führt dies zu einer Antwort mit dem Fehler 401 wegen fehlender Berechtigung. Es gibt zwei Möglichkeiten, dieses `AccessToken` abzurufen, nachdem Sie das Cloud Foundry-Befehlszeilentool installiert und sich bei {{site.data.keyword.Bluemix_notm}} angemeldet haben:<ul><li>Sie können dieses Token über den Befehl `cf oauth-token` erhalten:
   ```
   > cf oauth-token
   Getting OAuth token...
   OK

     bearer eyJhbGciOiJIUzI1NiJ9.eyJqdGkiOiJhNjIzMGE1YS1mNzE3LTQ0YjItOWM3Yi1kNGJkYThhZGU0NjkiLCJzdWIiOiI4OGViNjM2My1hMjkzLTRlZTItYWQ1MS0yOGVkMTZmZjMwNzQiLCJzY29wZSI6WyJjbG91ZF9jb250cm9sbGVyLnJlYWQiLCJwYXNzd29yZC53cml0ZSIsImNsb3VkX2NvbnRyb2xsZXIud3JpdGUiLCJvcGVuaWQiXSwiY2xpZW50X2lkIjoiY2YiLCJjaWQiOiJjZiIsImF6cCI6ImNmIiwiZ3JhbnRfdHlwZSI6InBhc3N3b3JkIiwidXNlcl9pZCI6Ijg4ZWI2MzYzLWEyOTMtNGVlMi1hZDUxLTI4ZWQxNmZmMzA3NCIsIm9yaWdpbiI6InVhYSIsInVzZXJfbmFtZSI6Imtqa29uZ2tqQGNuLmlibS5jb20iLCJlbWFpbCI6Imtqa29uZ2tqQGNuLmlibS5jb20iLCJyZXZfc2lnIjoiZDhlNGY0MDIiLCJpYXQiOjE0NTU2MDc1NDUsImV4cCI6MTQ1NTY1MDc0NSwiaXNzIjoiaHR0cHM6Ly91YWEuc3RhZ2UxLm5nLmJsdWVtaXgubmV0L29hdXRoL3Rva2VuIiwiemlkIjoidWFhIiwiYXVkIjpbImNsb3VkX2NvbnRyb2xsZXIiLCJwYXNzd29yZCIsImNmIiwib3BlbmlkIl19.nrzsEAZmGXNOWjX8r5Xf7U8Hj5-CE1rtHg8_C-jZKSk
   ```
 Die zurückgegebene lange Zeichenfolge beginnt mit "bearer" (Träger) und ist das AccessToken (Zugriffstoken), das in der Anforderung der {{site.data.keyword.autoscaling}}-RESTful-API verwendet werden kann. Wenn Fehler wie "Command not found" (Befehl nicht gefunden) auftreten, können Sie Ihr Cloud Foundry-Befehlszeilentool auf eine neuere Version aktualisieren.</li><li>Sie finden dieses AccessToken (Zugriffstoken) auch im Ausgangsverzeichnis. Nach der Anmeldung bei {{site.data.keyword.Bluemix_notm}} über eine Befehlszeilenschnittstelle, wird ein `.cf`-Ordner in Ihrem Ausgangsordner erstellt, in dem Sie eine JSON-Datei mit dem Namen `config.json` finden, die eine Liste der Information zur Umgebung Ihrer aktuellen Anmeldung wie Organisation, Bereich, Authentifizierungsendpunkt und Version enthält. Sie können den Eintrag `AccessToken` in der Datei wie folgt lokalisieren: 
    ```
   >cat ~/.cf/config.json
 {
  "ConfigVersion": 3,
  "Target": "https://api.ng.bluemix.net",
  "ApiVersion": "2.40.0",
  "AuthorizationEndpoint": "https://login.ng.bluemix.net/UAALoginServerWAR",
  "LoggregatorEndPoint": "wss://loggregator.ng.bluemix.net:443",
  "DopplerEndPoint": "wss://doppler.ng.bluemix.net:443",
  "UaaEndpoint": "https://uaa.ng.bluemix.net",
  "RoutingApiEndpoint": "https://api.ng.bluemix.net/routing",
  "AccessToken": "bearer eyJhbGciOiJIUzI1NiJ9.eyJqdGkiOiJhNjIzMGE1YS1mNzE3LTQ0YjItOWM3Yi1kNGJkYThhZGU0NjkiLCJzdWIiOiI4OGViNjM2My1hMjkzLTRlZTItYWQ1MS0yOGVkMTZmZjMwNzQiLCJzY29wZSI6WyJjbG91ZF9jb250cm9sbGVyLnJlYWQiLCJwYXNzd29yZC53cml0ZSIsImNsb3VkX2NvbnRyb2xsZXIud3JpdGUiLCJvcGVuaWQiXSwiY2xpZW50X2lkIjoiY2YiLCJjaWQiOiJjZiIsImF6cCI6ImNmIiwiZ3JhbnRfdHlwZSI6InBhc3N3b3JkIiwidXNlcl9pZCI6Ijg4ZWI2MzYzLWEyOTMtNGVlMi1hZDUxLTI4ZWQxNmZmMzA3NCIsIm9yaWdpbiI6InVhYSIsInVzZXJfbmFtZSI6Imtqa29uZ2tqQGNuLmlibS5jb20iLCJlbWFpbCI6Imtqa29uZ2tqQGNuLmlibS5jb20iLCJyZXZfc2lnIjoiZDhlNGY0MDIiLCJpYXQiOjE0NTU2MDc1NDUsImV4cCI6MTQ1NTY1MDc0NSwiaXNzIjoiaHR0cHM6Ly91YWEuc3RhZ2UxLm5nLmJsdWVtaXgubmV0L29hdXRoL3Rva2VuIiwiemlkIjoidWFhIiwiYXVkIjpbImNsb3VkX2NvbnRyb2xsZXIiLCJwYXNzd29yZCIsImNmIiwib3BlbmlkIl19.nrzsEAZmGXNOWjX8r5Xf7U8Hj5-CE1rtHg8_C-jZKSk",
  "SSHOAuthClient": "ssh-proxy",
 .....
 }
   ```
Das `AccessToken` in der Datei `config.json` ist nur für einen bestimmten Zeitraum gültig. Wenn Sie den Fehler 401 wegen unberechtigtem Zugriff für eine REST-API-Anforderung erhalten, müssen Sie sich möglicherweise erneut von der Befehlszeilenschnittstelle aus anmelden, um die Datei zu aktualisieren und das neue `AcessToken` abzurufen. </li></ul>
 
2.  Sie können die URL vom {{site.data.keyword.autoscaling}}-API-Server abrufen, indem Sie die Umgebungsvariable `VCAP_SERVICE` überprüfen, nachdem Sie Ihre Anwendung an den {{site.data.keyword.autoscaling}}-Service gebunden haben. In `VCAP_SERVICE` können Sie den {{site.data.keyword.autoscaling}}-Serviceabschnitt finden und die `api_url` ist die URL des API-Servers, an den Sie Ihre Anwendung gebunden haben. Sie benötigen die URL des API-Servers, um eine Verbindung zum {{site.data.keyword.autoscaling}}-RESTful-API-Service herzustellen:
   ```
    {
      "Auto-Scaling": [
      {
         "name": "Auto-Scaling-iw",
         "label": "Auto-Scaling",
         "plan": "free",
         "credentials": {
            "agentUsername": "agent",
            "api_url": "https://ScalingAPI.ng.bluemix.net",
            "service_id": "3f42b7ff-d939-4ff2-9a55-cb09cef9ab9e",
            "app_id": "2287f442-a7f3-4799-8919-d3908c386fa3",
            "url": "https://Scaling3.ng.bluemix.net",
            "agentPassword": "0cddf80b-37e1-4cfd-b648-83a6c8wee69f"
         }
      }
     ]
   }
   ``` 
  Beachten Sie, dass diese URL auch über den Befehl `cf env APPNAME` gefunden werden kann:
   ```
   > cf env Hello
   Getting env variables for app Hello in org OE_Runtimes_SVT / space RT_SVT as Alice...
   OK

   System-Provided:
   {
     "VCAP_SERVICES": {
     "Auto-Scaling": [
     {
      "credentials": {
       "agentPassword": "b626b064-7d26-417a-b954-41c6d3cb5200",
       "agentUsername": "agent",
       "api_url": "https://ScalingAPI.ng.bluemix.net",
       "app_id": "aa8d19b6-eceb-4b6e-b034-926a87e98a51",
       "service_id": "8f482f78-58d8-493c-829b-635e4cbfd817",
       "url": "https://Scaling.ng.bluemix.net"
      },
      "label": "Auto-Scaling",
      "name": "ScalingService",
      "plan": "free",
      "tags": [
       "bluemix_extensions",
       "ibm_created",
       "dev_ops"
      ]
     }
   ...
   ```  
3.  Sie können die `app_id` von der Umgebungsvariable `VCAP_SERVICES` abrufen oder einfach den Befehl `cf app APPNAME --guid` ausführen:

   ```
   > cf app Hello --guid
   aa8d19b6-eceb-4b6e-b034-926a87e98a51
   > 
   ```

Mit den oben genannten Voraussetzungen können Sie REST-API-Anforderungen erstellen, indem Sie das REST-Client-Add-on oder einfach ein Tool wie `curl` verwenden. 

Mit einem REST-Client-Add-on wie beispielsweise denen für Firefox oder Chrome können Sie REST-Anforderungen an {{site.data.keyword.autoscaling}}-API-Server auslösen, um Ihren Befehl auszuführen. Sie müssen diesen Add-ons die URL der REST-API, Methoden und Header bereitstellen, die diese REST-API benötigt, sowie die Parameter im Hauptteil. Weitere Details zu jeder API finden Sie unter [REST API of IBM {{site.data.keyword.autoscaling}} for {{site.data.keyword.Bluemix_notm}}](https://new-console.ng.bluemix.net/apidocs/48){:new_window}.

Mit Tools wie `curl` können Sie den {{site.data.keyword.autoscaling}}-Service innerhalb eines Scripts wie folgt betreiben:    
```
    cf login -a http://api.ng.bluemix.net -u Alice -p pa55w0rd --skip-ssl-validation
    accessToken=$(cf oauth-token | grep bearer | sed -e s/bearer/Bearer/g)
    API_url=$(cf env Hello | grep "api_url" | awk '{print $2}' | cut -d "," -f1 | cut -d "\"" -f2 )
    policyJson="./policy.json"
    appId=$(cf app Hello --guid)

    echo  -e "\nCreate scaling policy using API :"
    createPolicyUrl="${API_url}/v1/autoscaler/apps/${appId}/policy"
    curl_cmd="curl $createPolicyUrl -X 'PUT' -H 'Content-Type:application/json'  -H 'Accept:application/json' -H 'Authorization:$accessToken' --data-binary @${policyJson} -s -o response.txt -w '%{http_code}\n'"
    eval status_code=$($curl_cmd)
    if [[ $status_code -eq 201 ]]; then
         echo "looks good"
    else
         echo "error happens"
         exit 255
    fi
  ```

## {{site.data.keyword.autoscaling}}-Service über die {{site.data.keyword.autoscaling}}-CLI betreiben 
{: #CLI}

Die {{site.data.keyword.autoscaling}}-CLI bietet ähnliche Funktionen wie die {{site.data.keyword.autoscaling}}-RESTful-API, ist aber bei der Konfiguration des {{site.data.keyword.autoscaling}}-Service benutzerfreundlicher. Mit der {{site.data.keyword.autoscaling}}-CLI brauchen Sie sich nicht um die Details wie `AccessToken` und URL des API-Servers in der {{site.data.keyword.autoscaling}}-RESTful-API kümmern. Sie brauchen nur die Anweisungen Schritt für Schritt zu befolgen, die die CLI angibt. Weitere Details dazu, wie die {{site.data.keyword.autoscaling}}-CLI installiert und verwendet wird, finden Sie unter [{{site.data.keyword.autoscaling}}-CLI](../../cli/plugins/auto-scaling/index.html){:new_window}



## Richtlinienfelder für den {{site.data.keyword.autoscaling}}-Service
{: #policy_fields}

| Feldname  | Beschreibung |
|-------------|----------------------|
|*Zulässige maximale Instanzanzahl* |	Die maximale Anzahl an Anwendungsinstanzen, die
gestartet werden können. Wenn die momentane Anzahl der Anwendungsinstanzen diesem Wert entspricht,
führt der {{site.data.keyword.autoscaling}}-Service keine weiteren Scale-out-Aktionen für die Anwendung durch. Standardmäßige minimale Instanzanzahl - Die minimale Anzahl an Anwendungsinstanzen, die gestartet werden können. Wenn die Anzahl der Instanzen diesem Wert entspricht,
führt der {{site.data.keyword.autoscaling}}-Service keine weiteren Scale-in-Aktionen für die Anwendung durch. |
| *Metriktyp*	| 	Die unterstützten Metriktypen, die überwacht werden
können. Weitere Informationen finden Sie in Tabelle 2. |
| *Skalieren (Anzahl erhöhen)* | 	Gibt
den Schwellenwert an, durch den eine Scale-out-Aktion ausgelöst wird, und gibt
an, wie viele Instanzen hinzukommen, wenn die Scale-out-Aktion ausgelöst wird. |
| *Skalieren (Anzahl reduzieren)* |	Gibt
einen Schwellenwert an, durch den eine Scale-in-Aktion ausgelöst wird, und gibt
an, wie viele Instanzen reduziert werden, wenn die Scale-in-Aktion ausgelöst wird. |
| *Statistikfenster* |	Die Länge des vergangenen Zeitraums, in dem empfangene Metrikwerte
als gültig erkannt wurden. Metrikwerte sind nur gültig, wenn
die Zeitmarken in diesem Zeitraum liegen. Die Einheit für den Parameter 'Statistikfenster' ist Sekunden. |
| *Überschreitungsdauer*	| Die Länge des vergangenen Zeitraums, in dem möglicherweise eine
Skalierungsaktion ausgelöst wird. Eine Skalierungsaktion wird ausgelöst, sobald
gesammelte Metrikwerte entweder über dem oberen Schwellenwert oder unter dem
unteren Schwellenwert liegen, und zwar länger als angegeben. Die Einheit für den Parameter 'Überschreitungsdauer' ist Sekunden. |
| *Cooldown-Zeitraum für Herunterskalierung* | Nach dem Auftreten einer Scale-in-Aktion werden während der Länge des durch die Option 'Cooldown-Zeitraum für Herunterskalierung' angegebenen Zeitraums weitere Skalierungsanforderungen ignoriert. Die Einheit für diesen Parameter ist Sekunden. |
| *Cooldown-Zeitraum für Hochskalierung*	| Nach dem Auftreten einer Scale-out-Aktion werden während der Länge des durch die Option 'Cooldown-Zeitraum für Hochskalierung' angegebenen Zeitraums weitere Skalierungsanforderungen ignoriert. Die Einheit für diesen Parameter ist Sekunden. |
| *Zeitzone*	| Die Zeitzone, in der der Zeitplan gültig ist. |
| *Startzeit*  |	Die Startzeit eines sich wiederholenden Zeitplans. |
| *Endzeit*    |	Die Endzeit eines sich wiederholenden Zeitplans.	|
| *Wiederholungszeitpunkt*	|	Der Tag der Woche, für den ein sich wiederholender Zeitplan gültig ist. |
| *Anzahl der Instanzen - Minimum* |	Die minimale Anzahl an Instanzen, die für die Anwendung während des im Zeitplan angegebenen Zeitraums
gestartet werden können. |
| *Startdatum & -zeit* |	Startdatum und -zeit des Zeitplans, der für ein bestimmtes Datum eingerichtet ist. |
| *Enddatum & und -zeit* |	Enddatum und -zeit des Zeitplans, der für ein bestimmtes Datum eingerichtet
ist.	|

Tabelle 1. Richtlinienfelder in der Skalierungsrichtlinie

| Metrikname | Beschreibung | Unterstützter Anwendungstyp |
|-------------|----------------------| ------------------- |
| *Heapspeicher* |	Prozentsatz der Heapspeicherbelegung.	| Liberty for Java, Node.js SDK |
| *Hauptspeicher*   |	Prozentsatz der Hauptspeicherbelegung.	|  Alle |
| *Durchsatz* | Anzahl der verarbeiteten Anforderungen pro Sekunde.| Liberty for Java, Node.js SDK |
| *Antwortzeit* |	Die Antwortzeit
für die verarbeiteten Anforderungen.	| Liberty for Java |

Tabelle 2. Unterstützte Metriknamen

*Anmerkung:* Zur Erfassung von Auto-Scaling-Metrikdaten muss Ihre Anwendung als Liberty-Web-App bereitgestellt werden, damit HTTP/HTTPS-Anforderungen zur Messung über den Liberty-Web-Container verarbeitet werden.
Beispiel: Wenn Sie eine Spring Boot-Anwendung als App des Typs "Main-Classs" ausführen, stellt das Liberty-Buildpack nur eine Java-Umgebung für Sie bereit und die App wird tatsächlich im in Spring integrierten Tomcat-Container ausgeführt; daher werden vom Auto-Scaling-Service keine Metrikdaten erfasst. Sie müssen Ihre App als Liberty-WAR ausführen, damit sie mit dem Auto-Scaling-Service funktioniert.

## Fehlernachrichten
{: #err_msg}
In diesem Abschnitt werden die Warnungen und Fehlernachrichten aufgeführt, die vom
{{site.data.keyword.autoscaling}}-Service generiert werden.
 
### CWSCV2004E Es ist bereits ein anderer
{{site.data.keyword.autoscaling}}-Service an die Anwendung gebunden.
**Sie können nur einen {{site.data.keyword.autoscaling}}-Service an eine Anwendung binden. Dieser Fehler tritt auf, wenn Sie den {{site.data.keyword.autoscaling}}-Service an eine Anwendung binden möchten, die bereits an einen anderen {{site.data.keyword.autoscaling}}-Service gebunden ist.**

Wählen Sie eine andere Anwendung aus, an die kein weiterer {{site.data.keyword.autoscaling}}-Service gebunden ist, und binden Sie den {{site.data.keyword.autoscaling}}-Zielservice an diese Anwendung.
Wenn dieser Fehler auch in allen anderen Fällen auftritt, wenden Sie sich an den IBM Support.

### CWSCV6001E Der API-Server kann die JSON-Eingabezeichenfolgen für die folgende API nicht parsen: {0}.
**Das Problem tritt beim Parsen von JSON-Ausgabezeichenfolgen auf.**

Prüfen Sie die JSON-Eingabe im API-Dokument und beheben Sie darin den Fehler.

### CWSCV6002E Der API-Server kann die JSON-Ausgabezeichenfolgen für die folgende API nicht parsen: {0}.
**Das Problem tritt beim Parsen von JSON-Ausgabezeichenfolgen auf.**

Wenden Sie sich für weitere Informationen an den Cloudadministrator.

### CWSCV6003E Formatfehler {0} für JSON-Eingabezeichenfolgen in JSON-Eingabe für folgende API: {1}.
**Beim Parsen von JSON-Eingabezeichenfolgen wurde ein Formatfehler entdeckt. **

Prüfen Sie die JSON-Eingabe im API-Dokument und beheben Sie darin den Fehler.

### CWSCV6004E Formatfehler {0} für JSON-Ausgabezeichenfolgen für folgende API: {1}.
**Beim Parsen von JSON-Ausgabezeichenfolgen wurde ein Formatfehler entdeckt. **

Wenden Sie sich für weitere Informationen an den Cloudadministrator.

### CWSCV6005E Interner Serverfehler während {0}.
**Beim Verarbeiten der Anforderung tritt ein interner Serverfehler auf. **

Wenden Sie sich für weitere Informationen an den Cloudadministrator.

### CWSCV6006E Aufrufen von CloudFoundry-APIs schlug fehl: {0}
**Beim Aufrufen von CloudFoundry-APIs ist ein Fehler aufgetreten.**

Wenden Sie sich für weitere Informationen an den Cloudadministrator.

### CWSCV6007E Die folgende Anwendung wurde nicht gefunden: {0}
**Die Anwendung wurde nicht gefunden.**

Prüfen Sie die Anwendungsinformationen, um weitere Informationen zu erhalten.

### CWSCV6008E Beim Abrufen von Informationen für Anwendung {0} ist folgender Fehler aufgetreten: {1}
**Das Abrufen von Anwendungsinformationen ist mit Fehlern fehlgeschlagen. **

Prüfen Sie die Anwendungsinformationen, um weitere Informationen zu erhalten.

### CWSCV6009E Service {0} für App {1} wurde nicht gefunden.
**Der Service für diese Anwendung konnte nicht gefunden werden. **

Prüfen Sie die Servicebindung für diese Anwendung, um weitere Informationen zu erhalten.

### CWSCV6010E Richtlinie für App {0} wurde nicht gefunden
**Die Richtlinie für diese Anwendung konnte nicht gefunden werden.**

Prüfen Sie die Anwendungskonfiguration, um weitere Informationen zu erhalten.

### CWSCV6011E Interne Authentifizierung fehlgeschlagen während {0}
**Die interne Authentifizierung ist fehlgeschlagen. **

Wenden Sie sich für weitere Informationen an den Cloudadministrator.


# rellinks
{: #rellinks}

## Beispiele
{: #samples}

* [Lernprogramm: Machen Sie Ihre Anwendung in {{site.data.keyword.Bluemix_notm}}](http://www.ibm.com/developerworks/cloud/library/cl-autoscale-app/index.html){:new_window} elastisch
* [Cloud Foundry Architecture Labs](https://developer.ibm.com/bluemix/docs/category/cloud-foundry-docs/){:new_window}

## sdk
{: #sdk}

* [Rest-API von IBM {{site.data.keyword.autoscaling}} for {{site.data.keyword.Bluemix_notm}}](https://new-console.{DomainName}/apidocs/48){:new_window}

## Allgemein
{: #general}

* [Container skalieren](https://www.{DomainName}/docs/containers/container_creating_ov.html#container_group_ov){:new_window}
* [Virtuelle Server skalieren](https://www.{DomainName}/docs/virtualmachines/vm_index.html#vm_manage_instances){:new_window}
* [{{site.data.keyword.autoscaling}}-CLI](../../cli/plugins/auto-scaling/index.html){:new_window}
* [{{site.data.keyword.autoscaling}}-Agent für Node.js](https://www.npmjs.com/package/bluemix-autoscaling-agent){:new_window}

