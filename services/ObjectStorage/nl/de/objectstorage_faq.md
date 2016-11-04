---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# FAQ {: #faq}

*Letzte Aktualisierung: 19. Oktober 2016*
{: .last-updated}

Diese FAQ bieten Antworten auf häufig gestellte Fragen zum {{site.data.keyword.objectstorageshort}}-Service.
{: shortdesc}


## Welche Konten und Zahlungspläne können für {{site.data.keyword.objectstorageshort}} verwendet werden? {: #account-payment}

Der {{site.data.keyword.objectstorageshort}}-Service bietet zwei Planoptionen: Kostenlos und Standard. Die [Preisstruktur](https://console.ng.bluemix.net/pricing/) ist vom ausgewählten Plan abhängig.

<table>
  <tr>
    <th> Kostenloser Plan</th>
    <th> Standardplan</th>
  </tr>
  <tr>
    <td> Nur eine Serviceinstanz in einer {{site.data.keyword.Bluemix_notm}}-Organisation zu einer bestimmten Zeit zulässig</td>
    <td> Unbegrenzte Anzahl von Serviceinstanzen</td>
  </tr>
  <tr>
    <td> Für jeden verfügbar</td>
    <td> Verfügbar nur für kostenpflichtige {{site.data.keyword.Bluemix_notm}}-Konten und interne IBM Benutzer</td>
  </tr>
  <tr>
    <td> Kostenlos</td>
    <td> Nutzungsabhängige oder Subskriptions-Zahlungspläne</td>
  </tr>
  <tr>
    <td> Enthält eine Speichernutzungsbegrenzung von 5 GB für den Einstieg</td>
    <td> Unbegrenzter Speicherplatz</td>
  </tr>
</table>

*Tabelle 1: Vergleich des kostenlosen und des Standardplans*

**Achtung**: Benutzer, die mit einem {{site.data.keyword.Bluemix_notm}}-Testkonto arbeiten, können den kostenlosen Plan nutzen. Wenn der Zeitraum für den Test abläuft, wird die zugeordnete {{site.data.keyword.objectstorageshort}}-Serviceinstanz inaktiviert, d. h. Sie können nicht auf das Speicherkonto zugreifen. Nach 30 Tagen wird Ihr {{site.data.keyword.Bluemix_notm}}-Konto bereinigt und alle Daten werden gelöscht. Zur Vermeidung von Datenverlust aktualisieren Sie das [gebührenpflichtige {{site.data.keyword.Bluemix_notm}}-Konto ](https://new-console.ng.bluemix.net/docs/admin/account.html) so bald wie möglich.

## Wie ändere ich meinen Plan? {: #changeplan}  
Für Instanzen, die im Rahmen des Beta-Plans oder des kostenfreien Plans erstellt werden, kann ein Upgrade auf auf den Standardplan durchgeführt werden. Die zugeordnete Organisation muss ein gebührenpflichtiges {{site.data.keyword.Bluemix_notm}}-Konto sein. Testkonten mit Object Storage-Instanzen können nicht auf den Standardplan aktualisiert werden und Instanzen im Standardplan können nicht auf andere Pläne herabgestuft werden. Ihre Serviceinstanzen und Kundendaten werden bei einem Upgrade in den neuen Plan verschoben.

Zum Durchführen eines Upgrades gehen Sie folgendermaßen vor:
1.	Klicken Sie in der Benutzerschnittstelle von {{site.data.keyword.objectstorageshort}} auf **Plan**.
2.	Wählen **Standard** als neuen Plan aus und klicken Sie auf **Speichern**.

Sie können außerdem Ihren [Zahlungsplan ändern](../../pricing/index.html#changing), indem Sie die Befehlszeilenschnittstelle verwenden.

## Welche Gebühren werden für meine Nutzung von {{site.data.keyword.objectstorageshort}} fällig und wann werden sie in Rechnung gestellt? {: #charge-bill}

Für den Service {{site.data.keyword.objectstorageshort}} werden nur Gebühren für das, was Sie nutzen, fällig.  Um mit der Verwendung des Service zu beginnen, sind keine Einrichtungsgebühren oder Konfigurationsgebühren zu entrichten. Es fallen keine Gebühren für API-Anforderungen oder Netzverkehr mit ankommenden Daten an.

Die Rechnungsstellung für {{site.data.keyword.objectstorageshort}} erfolgt aufgrund Ihrer Speichernutzung innerhalb des Fakturierungszyklus. Dies schließt alle Objektdaten in Containern ein, die Sie innerhalb Ihres {{site.data.keyword.Bluemix_notm}}-Organisationskontos erstellt haben.

Gebühren für die Übertragung abgehender Daten werden fällig, sobald Daten aus einem Ihrer Objektcontainer über das öffentliche Netz gelesen werden. Die ganze Bandbreite, die während des Fakturierungszyklus verbraucht wird, wird als "Public Outbound Bandwidth" in Rechnung gestellt.

Am Ende des Fakturierungszyklus wird Ihnen die Nutzung von {{site.data.keyword.Bluemix_notm}} während dieses Fakturierungszeitraums automatisch in Rechnung gestellt. Sie können Ihre Gebühren für den momentanen Fakturierungszeitraum über die {{site.data.keyword.Bluemix_notm}}-Berichterstellungsfunktion einsehen.
