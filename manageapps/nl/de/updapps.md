---

copyright:
  years: 2015, 2016

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#Anwendungen aktualisieren
{: #updatingapps}

*Letzte Aktualisierung: 9. Mai 2016*


Sie können den Befehl 'cf push' oder {{site.data.keyword.Bluemix}} DevOps Services verwenden, um die Anwendungen in {{site.data.keyword.Bluemix_notm}} zu aktualisieren. In vielen Fällen müssen Sie (selbst für die integrierten Buildpacks wie beispielsweise 'Node.js') auch den Parameter '-c' verwenden, um anzugeben, welcher Befehl zum Starten Ihrer Anwendung verwendet wird.
{:shortdesc}

##Angepasste Domäne erstellen und verwenden
{: #domain}

Sie können in der URL Ihrer Anwendung eine angepasste Domäne anstelle der standardmäßigen
{{site.data.keyword.Bluemix_notm}}-Systemdomäne (mybluemix.net) verwenden.

Mithilfe von Domänen wird die URL-Route angegeben, die Ihrer Organisation in
{{site.data.keyword.Bluemix_notm}} zugeordnet ist. Um eine angepasste Domäne zu verwenden, müssen Sie die angepasste Domäne auf einem öffentlichen DNS-Server registrieren, die angepasste Domäne in {{site.data.keyword.Bluemix_notm}} konfigurieren und die angepasste Domäne der {{site.data.keyword.Bluemix_notm}}-Systemdomäne auf dem öffentlichen DNS-Server zuordnen. Nachdem Ihre angepasste Domäne der {{site.data.keyword.Bluemix_notm}}-Systemdomäne zugeordnet wurde, werden Anforderungen
für Ihre angepasste Domäne an Ihre Anwendung in {{site.data.keyword.Bluemix_notm}} weitergeleitet.

Sie können eine angepasste Domäne in {{site.data.keyword.Bluemix_notm}} erstellen und verwenden, indem Sie
entweder die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle oder die Befehlszeilenschnittstelle
'cf' verwenden.

* Verwendung der {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle:

  1. Erstellen Sie eine angepasste Domäne für Ihre Organisation.
    
	1. Klicken Sie in der Menüleiste des {{site.data.keyword.Bluemix_notm}}-**Dashboards** auf **Organisationen verwalten**.
	
	2. Klicken Sie auf der Registerkarte **Domänen** auf **Domäne hinzufügen**,
geben Sie den Namen Ihrer angepassten Domäne ein und klicken Sie auf **Speichern**.
    	
  2. Fügen Sie die Route mit der angepassten Domäne zu einer Anwendung hinzu.
  
    1. Klicken Sie in der Menüleiste des {{site.data.keyword.Bluemix_notm}}-**Dashboards** auf die Kachel der Anwendung, der Sie die Route hinzufügen wollen. Die Seite **Übersicht** wird angezeigt.
	
	2. Klicken Sie auf der Seite **Übersicht** auf die Option **Routen und
App-Zugriff bearbeiten**.
	
	3. Klicken Sie auf **Route hinzufügen** und geben Sie die Route an, die Sie für die Anwendung verwenden wollen.
	
* Verwendung der Befehlszeilenschnittstelle 'cf':
  
  1. Erstellen Sie eine angepasste Domäne für Ihre Organisation, indem Sie den folgenden Befehl eingeben:
    
    ```
    cf create-domain <Organisationsname> mydomain
    ```
    
    *Organisationsname*
  
        Der Name Ihrer Organisation.
	  
    *mydomain*
    
        Der Name, den Sie für die angepasste Domäne verwenden wollen.
	  
  2. Fügen Sie die Route mit der angepassten Domäne zu einer Anwendung hinzu, indem Sie den folgenden Befehl eingeben:
    
    ```
    cf map-route myapp mydomain -n host_name
    ```
    
    *myapp*
      
    	Der Name Ihrer Anwendung.
  	
    *mydomain*
      
    	Der Name Ihrer angepassten Domäne.
	
    *host_name*
    
        Der Hostname in der Route für Ihre Anwendung.
	
Nach der Konfiguration der angepassten Domäne in {{site.data.keyword.Bluemix_notm}} müssen Sie die angepasste Domäne der {{site.data.keyword.Bluemix_notm}}-Systemdomäne auf Ihrem registrierten DNS-Server zuordnen:

  1. Richten Sie einen Datensatz 'CNAME' für den Namen der angepassten Domäne auf Ihrem DNS-Server ein.
  2. Ordnen Sie den Namen der angepassten Domäne dem sicheren Endpunkt für die {{site.data.keyword.Bluemix_notm}}-Region zu, in der Ihre Anwendung ausgeführt wird. Verwenden Sie die folgenden Regionsendpunkte, um die URL-Route anzugeben, die Ihrer Organisation in {{site.data.keyword.Bluemix_notm}} zugeordnet ist:
  
    * US-SOUTH: `secure.us-south.bluemix.net`
    * EU-GB: `secure.eu-gb.bluemix.net`
    * AU-SYD: `secure.au-syd.bluemix.net`
  
Geben Sie die folgende URL in einen Browser oder eine Befehlszeilenschnittstelle ein, um auf die Anwendung 'myapp' zuzugreifen:

```
http://host_name.mydomain
```

**Hinweis:** Zum Entfernen einer verwaisten Route verwenden Sie den folgenden Befehl:

```
cf delete-route domain -n hostname -f
```

*domain* ist der Name Ihrer Domäne und *hostname* ist der Hostname der Route für Ihre Anwendung. Wenn Sie weitere Informationen zum Befehl **cf delete-route** benötigen, geben Sie `cf delete-route -h` ein.

##Blue-Green-Bereitstellungen
{: #blue_green}

{{site.data.keyword.Bluemix_notm}} unterstützt das
Blue-Green-Bereitstellungsverfahren, um Continuous Delivery
zu ermöglichen und Ausfallzeitereignisse zu minimieren.

Die *Blue-Green-Bereitstellung* ist ein Bereitstellungsverfahren ohne Ausfallzeiten
(Zero-Downtime-Deployment), das aus zwei nahezu identischen Produktionsumgebungen besteht: Blue und Green. Sie unterscheiden sich durch die Artefakte, die der Entwickler bewusst geändert hat; normalerweise ist dies die Version der Anwendung. Es ist zu jedem Zeitpunkt mindestens eine der Umgebungen aktiv. Durch die Verwendung des Blue-Green-Bereitstellungsverfahrens können Sie die folgenden Vorteile nutzen:

* Zeitnahe Überführung der Software aus der letzten Testphase in die Live-Produktion.
* Bereitstellung einer neuen Anwendungsversion ohne Unterbrechung des Datenverkehrs zu der betreffenden Anwendung.
* Rasche Durchführung von Rollback-Operationen. Beim Auftreten von Problemen in einer Ihrer Umgebungen können Sie schnell zu der jeweils anderen Umgebung
umschalten.

Wenn Sie bereits eine Anwendung
für {{site.data.keyword.Bluemix_notm}} bereitgestellt haben und
diese Anwendung auf eine neue Version aktualisieren wollen, können Sie eine der folgenden beiden Methoden verwenden,
um eine Blue-Green-Bereitstellung sicherzustellen.

###Beispiel: Befehl 'cf rename' verwenden

In diesem Beispiel lautet der Name der Anwendung 'Blue'. Das Beispiel veranschaulicht, wie die Version von *Blue* mithilfe des Befehls
**cf rename** aktualisiert wird, ohne den Datenverkehr zu der Anwendung zu unterbrechen. Optional kann die dann alte Version von
*Blue* gelöscht werden, wenn die aktualisierte Version vorhanden ist.

1. Stellen Sie die App *Blue* per Push-Operation in {{site.data.keyword.Bluemix_notm}} bereit.
  
  ```
  cf push Blue
  ```
  
  **Ergebnis:** Die App *Blue* wird ausgeführt und antwortet an die URL `Blue.mybluemix.net`.
  
2. Verwenden Sie den Befehl **cf rename**, um die App *Blue* in *Green* zu ändern:
  
  ```
  cf rename Blue Green
  ```
  
  Listen Sie die Anwendungen im aktuellen Bereich mit dem Befehl **cf apps** auf:
  
  ```
  ...
  name             requested state   instances   memory   disk   urls
  Green            started           1/1         1G       1G	 Blue.mybluemix.net
  ...
  ```
  
  **Ergebnis:** Die App *Green* wird ausgeführt und antwortet an die URL `Blue.mybluemix.net`.

3. Nehmen Sie die erforderlichen Änderungen vor und bereiten Sie die aktualisierte Version von
*Blue* vor. Stellen Sie die aktualisierte App *Blue* per Push-Operation in {{site.data.keyword.Bluemix_notm}} bereit:
  
  ```
  cf push Blue
  ```
  
  Listen Sie die Anwendungen im aktuellen Bereich mit dem Befehl **cf apps** auf:
  
  ```
  ...
  name             requested state   instances   memory   disk   urls
  Green            started           1/1         1G       1G	 Blue.mybluemix.net
  Blue             started           1/1         1G       1G	 Blue.mybluemix.net
  ...
  ```
  
  **Ergebnisse:**
    * Zwei Instanzen der Anwendung sind bereitgestellt: die Instanz *Blue* und die Instanz
*Green*.
	* Die App *Green* wird ausgeführt und antwortet an die URL `Blue.mybluemix.net`.
	
4. Optional: Wenn Sie die alte Version (*Green*) der App löschen wollen, verwenden Sie den Befehl **cf
delete**.
  
  ```
  cf delete Green -f
  ```
  
  Listen Sie die Routen in Ihrem Bereich mit dem Befehl
**cf route** auf:
  
  ```
  ...
  host             domain           apps
  Blue             mybluemix.net    Blue
  ...
  ```
  
  **Ergebnis:** Die App *Blue* antwortet an die URL `Blue.mybluemix.net`.
  
###Beispiel: Befehl 'cf map-route' verwenden

In diesem Beispiel ist *Blue* die zuvor bereitgestellte Anwendung, und
*Green* ist die aktualisierte Version. Dieses Beispiel veranschaulicht, wie die Version von *Blue* mithilfe des Befehls
**cf map-route** aktualisiert wird, ohne den Datenverkehr zu der Anwendung zu unterbrechen. Optional kann die dann alte Version von
*Blue* gelöscht werden, wenn die aktualisierte Version vorhanden ist.

1. Stellen Sie die App *Blue* per Push-Operation in {{site.data.keyword.Bluemix_notm}} bereit.
  
  ```
  cf push Blue
  ```
  
  **Ergebnis:** Die App *Blue* wird ausgeführt und antwortet an die URL `Blue.mybluemix.net`.
  
2. Nehmen Sie die erforderlichen Änderungen vor und bereiten Sie die Version *Green* vor. Stellen Sie die App *Green* per Push-Operation in {{site.data.keyword.Bluemix_notm}} bereit:
  
  ```
  cf push Green
  ```
  
  Listen Sie die Anwendungen im aktuellen Bereich mit dem Befehl **cf route** auf:
  
  ```
  ...
  host             domain           apps
  Blue             mybluemix.net    Blue
  Green            mybluemix.net    Green
  ...
  ```
  
  **Ergebnisse:**
  
    * Zwei Instanzen der App sind bereitgestellt: die Instanz *Blue* und die Instanz
*Green*.
	* Die App *Blue* antwortet an die URL `Blue.mybluemix.net`. Und die App *Green* antwortet an die URL `Green.mybluemix.net`.
	
3. Ordnen Sie die App *Blue* der App *Green* zu, sodass der gesamte Datenverkehr an `Blue.mybluemix.net` sowohl an die App *Blue* als auch an die App *Green* weitergeleitet wird.
  
  ```
  cf map-route Green mybluemix.net -n Blue
  ```
  
  Listen Sie die Routen in Ihrem Bereich mit dem Befehl 'cf routes' auf:
  
  ```
  ...
  host             domain           apps
  Blue             mybluemix.net    Blue, Green
  Green            mybluemix.net    Green
  ...
  ```
  
  **Ergebnis:**

    * Der CF-Router sendet nun den Datenverkehr für 'Blue.mybluemix.net' sowohl an die App 'Blue' als auch an die App 'Green'.
	* Der CF-Router sendet den Datenverkehr für 'Green.mybluemix.net' weiterhin an die App 'Green'.
	
4. Wenn Sie sich vergewissert haben, dass *Green* wie erwartet ausgeführt wird, entfernen Sie die Route
`Blue.mybluemix.net` aus
der App *Blue* :
  
  ```
  cf unmap-route Blue mybluemix.net -n Blue
  ```
  
  Listen Sie die Routen in Ihrem Bereich mit dem Befehl 'cf routes' auf:
  
  ```
  ...
  host             domain           apps
  Blue             mybluemix.net    Green
  Green            mybluemix.net    Green
  ...
  ```
  
  **Ergebnis:** Der CF-Router sendet keinen Datenverkehr mehr an die App
*Blue*. Die App *Green* antwortet an beide URLs: `Green.mybluemix.net` und `Blue.mybluemix.net`.
  
5. Entfernen Sie die Route `Green.mybluemix.net` zur App *Green*.
  
  ```
  cf unmap-route Green mybluemix.net -n Green
  ```
  
  **Ergebnis:** Der CF-Router sendet keinen Datenverkehr mehr an die App
*Blue*. Die App *Green* antwortet an die URL `Blue.mybluemix.net`.
  
6. Optional: Wenn Sie die alte Version (*Blue*) der Anwendung löschen wollen, verwenden Sie hierzu den Befehl `cf
delete`.
  
  ```
  cf delete Blue -f
  ```
  
  Listen Sie die Routen in Ihrem Bereich mit dem Befehl
'cf route' auf:
  
  ```
  ...
  host             domain           apps
  Blue             mybluemix.net    Green
  ...
  ```
  
  **Ergebnis:** Die App *Green* antwortet an die URL `Blue.mybluemix.net`.


# Zugehörige Links
{: #rellinks}

## Zugehörige Links
{: #general}

* [Blue-Green-Bereitstellungen](http://martinfowler.com/bliki/BlueGreenDeployment.html){:new_window}
* [IBM {{site.data.keyword.Bluemix_notm}} DevOps Services](https://hub.jazz.net/){:new_window}
