{:new_window: target="_blank"}

# FAQ {: #faq} 

*Letzte Aktualisierung: 18. Juli 2016*
{: .last-updated}


## Wie variieren die Preise je nach ausgewähltem Plan? {: #plan-price}
Die Preisgestaltung ist vom ausgewählten Plan abhängig. Weitere Informationen zu Preisen finden Sie in der [IBM Bluemix-Preisliste](https://console.ng.bluemix.net/pricing/){: new_window} oder verwenden Sie den [Preisrechner](https://console.ng.bluemix.net/?direct=classic/#/pricing/cloudOEPaneId=pricing&paneId=pricingSheet){: new_window}, um detailliertere Preisschätzungen zu ermitteln.


## Welche Konten und Zahlungspläne können für {{site.data.keyword.objectstorageshort}} verwendet werden? {: #account-payment}
Der {{site.data.keyword.objectstorageshort}}-Service wird mit mehreren Planoptionen bereitgestellt. Mit dem Release der allgemeinen Verfügbarkeit werden gegenwärtig zwei Pläne angeboten: Standard und Kostenlos. Der Standardplan ist nur für gebührenpflichtige {{site.data.keyword.Bluemix_notm}}-Konten verfügbar, entweder für 'Nutzungsabhängig' oder für 'Abonnement', sowie für interne IBM Benutzer. Der Standardplan umfasst zur Einführung eine Gratisleistung in Form von 5 GB kostenfreier Speichernutzung pro Konto.

Testkonten, die weiterhin aktiv sind, können den kostenlosen Plan nutzen, der nur das Vorhandensein einer Instanz in einer {{site.data.keyword.Bluemix_notm}}-Organisation zulässt. Wenn der Zeitraum für den {{site.data.keyword.Bluemix_notm}}-Test abläuft, wird die zugeordnete {{site.data.keyword.objectstorageshort}}-Serviceinstanz inaktiviert. Dies bedeutet, dass weder die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle noch die Befehlszeile auf das Speicherkonto zugreifen kann. Nach einer Frist von 30 Tagen wird Ihr {{site.data.keyword.Bluemix_notm}}-Konto bereinigt und alle Daten werden gelöscht. Zur Vermeidung von Datenverlust wird empfohlen, das gebührenpflichtige {{site.data.keyword.Bluemix_notm}}-Konto so bald wie möglich zu aktualisieren. Zum Aktualisieren Ihres Kontos klicken Sie auf das Benutzermanagementmenü und wählen **Konto** aus. Dadurch werden Anweisungen zum Aktualisierungsprozess bereitgestellt.

## Wie ändere ich meinen Plan? {: #changeplan}  
Für Instanzen, die im Rahmen des Beta-Plans oder des kostenfreien Plans erstellt werden, kann ein Upgrade auf auf den Standardplan durchgeführt werden. Die zugeordnete Organisation muss ein gebührenpflichtiges {{site.data.keyword.Bluemix_notm}}-Konto sein. Testkonten mit {{site.data.keyword.objectstorageshort}}-Instanzen können nicht auf den Standardplan aktualisiert werden und Instanzen im Standardplan können nicht auf andere Pläne herabgestuft werden. Ihre Serviceinstanzen und Kundendaten werden bei einem Upgrade in den neuen Plan verschoben.

Gehen Sie wie folgt vor, um für Ihren Plan ein Upgrade durchzuführen:
1.	Kicken Sie in der Benutzerschnittstelle von {{site.data.keyword.objectstorageshort}} auf **Plan**.
2.	Wählen **Standard** als neuen Plan aus und klicken Sie auf **Speichern**.

Sie können außerdem Ihren Zahlungsplan über die Befehlszeilenschnittstelle ändern. Weitere Informationen finden Sie in [Vorgehensweise zum Ändern des Plans](../../pricing/index.html#changing).


## Welche Gebühren werden für meine Nutzung von {{site.data.keyword.objectstorageshort}} fällig und wann werden sie in Rechnung gestellt? {: #charge-bill}

Für den Service {{site.data.keyword.objectstorageshort}} werden nur Gebühren für das, was Sie nutzen, fällig.  Um mit der Verwendung des Service zu beginnen, sind keine Mindestgebühren oder Konfigurationsgebühren zu entrichten und es sind auch keine sonstigen Verpflichtungen einzugehen. Es sind keine Gebühren für API-Anforderungen oder für Netzverkehr für eingehende Daten zu entrichten.

Die Kosten für Ihre Nutzung von {{site.data.keyword.objectstorageshort}} werden während des gesamten Fakturierungszyklus auf der Grundlage der Speichernutzung berechnet. Dies schließt alle Objektdaten in Containern ein, die Sie mit Ihrem {{site.data.keyword.Bluemix_notm}}-Organisationskonto erstellt haben. 

Gebühren für die Übertragung abgehender Daten werden fällig, sobald Daten aus einem Ihrer Objektcontainer über das öffentliche Netz gelesen werden. Bei der öffentlichen Bandbreite für abgehende Daten werden die Kosten für die gesamte verbrauchte Bandbreite im Fakturierungszyklus berechnet.

Die Metrikkomponenten für die Preisbestimmung von {{site.data.keyword.objectstorageshort}} sind folgende:
* Speichernutzung - $0.04 pro GB pro Monat
* Öffentliche Übertragung abgehender Daten - $0.09 pro GB pro Monat 

Am Ende des Fakturierungszyklus wird Ihnen die Nutzung während des momentanen Fakturierungszeitraums von {{site.data.keyword.Bluemix_notm}} automatisch in Rechnung gestellt. Sie können Ihre Gebühren für den momentanen Fakturierungszeitraum über die {{site.data.keyword.Bluemix_notm}}-Berichterstellungsfunktion einsehen.

Der für London und Dallas freigegebene Standardserviceplan unterliegt derselben Preisbestimmung.

## Wie funktioniert die Datenreplikation in {{site.data.keyword.objectstorageshort}}? {: #replication}
Der Service {{site.data.keyword.objectstorageshort}} pflegt drei Kopien Ihrer Daten, die in mehreren Speicherknoten repliziert werden. Weitere Informationen finden Sie in der Dokumentation [OpenStack Swift Replication](http://docs.openstack.org/developer/swift/overview_replication.html){: new_window}.

