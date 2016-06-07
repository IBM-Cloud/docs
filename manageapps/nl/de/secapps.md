---

copyright:
  years: 2015, 2016

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#Apps schützen
{: #securingapps}

*Letzte Aktualisierung: 9. Mai 2016*

Sie können Ihre Anwendungen schützen, indem Sie SSL-Zertifikate hochladen und den Zugriff auf die Anwendungen beschränken.
{:shortdesc}

##Zertifikatssignieranforderungen erstellen
{: #ssl_csr}

Bevor Sie die SSL-Zertifikate hochladen können, für die Sie in {{site.data.keyword.Bluemix}} berechtigt sind, müssen Sie auf
Ihrem Server eine Zertifikatssignieranforderung (CSR) erstellen.

Bei einer CSR handelt es sich um eine Nachricht, die an eine Zertifizierungsstelle
gesendet wird, um die Signierung eines öffentlichen Schlüssels und der zugehörigen Informationen
anzufordern. Am häufigsten haben CSRs das Format des PKCS-Standards #10. Die CSR umfasst einen öffentlichen Schlüssel
sowie einen allgemeinen Namen, eine Organisation, eine Stadt, ein Bundesland, ein Land sowie eine E-Mail-Adresse. SSL-Zertifikatsanforderungen
werden nur mit einer CSR-Schlüssellänge von 2048 Bits akzeptiert.

Damit die CSR gültig ist, müssen bei ihrer Generierung die folgenden Angaben gemacht werden:

**Landesname**
  
  Ein zweistelliger Code, der für das Land oder die Region steht. Die Abkürzung 'US' steht z. B. für die Vereinigten Staaten. Ziehen Sie für
weitere Länder oder Regionen vor der Erstellung der CSR die [Liste der
ISO-Landescodes](https://www.iso.org/obp/ui/#search){:new_window} zurate.
  
**Bundesland oder Kanton**

  Der vollständige und ungekürzte Name des Bundeslands oder des Kantons.

**Standort**

  Der vollständige Name der Stadt.
  
**Organisation**

  Der vollständige Name des Geschäfts oder des Unternehmens, das an Ihrem Standort rechtsgültig registriert ist,
oder ein persönlicher Name. Bei Unternehmen müssen Sie sicherstellen, dass das Registrierungssuffix mit angegeben wird, z. B. Ltd., Inc. oder NV.
  
**Organisationseinheit**

  Der Name der Abteilung Ihres Unternehmens, die das Zertifikat anfordert, z. B.
Buchhaltung oder Marketing.
  
**Allgemeiner Name**

  Der vollständig qualifizierte Domänenname (FQDN), für den Sie das SSL-Zertifikat anfordern.
  
Die Methoden für die Erstellung einer CSR variieren in Abhängigkeit von Ihrem Betriebssystem. Das folgende Beispiel zeigt, wie eine CSR mithilfe des [OpenSSL-Befehlszeilentools](http://www.openssl.org/){:new_window} erstellt wird:

```
openssl req -out CSR.csr -new -newkey rsa:2048 -nodes -keyout
    privatekey.key
```

**Hinweis:** Die OpenSSL-Implementierung SHA-512 ist von der Compilerunterstützung für den ganzzahligen 64-Bit-Typ abhängig. Sie können die SHA-1-Option für Anwendungen verwenden, die Kompatibilitätsprobleme mit dem SHA-256-Zertifikat haben.

Ein Zertifikat wird von einer Zertifizierungsstelle ausgegeben und von dieser Zertifizierungsstelle digital signiert. Nach dem Erstellen der Zertifikatssignieranforderung (Certificate Signing Request, CSR) können Sie Ihr SSL-Zertifikat bei einer öffentlichen Zertifizierungsstelle generieren. 

##SSL-Zertifikate hochladen
{: #ssl_certificate}

Sie können ein Sicherheitsprotokoll anwenden, um die Kommunikation für Ihre Anwendung zu schützen und so ein Ausspionieren, Manipulationen und das
Fälschen von Nachrichten zu verhindern.

Für jede Organisation in {{site.data.keyword.Bluemix_notm}} mit einem Kontoeigner, der einen Plan mit
nutzungsabhängiger Zahlung oder einen Abonnementplan besitzt, dürfen Sie vier Zertifikate kostenlos hochladen. Für jede Organisation mit einem
Kontoeigner, der ein Konto für eine kostenlose Testversion besitzt, dürfen Sie ein Zertifikat kostenlos hochladen.

Bevor Sie Zertifikate hochladen können,
müssen Sie eine Zertifikatssignieranforderung erstellen. Siehe [Zertifikatssignieranforderungen erstellen](#ssl_csr).

^Wenn Sie eine angepasste Domäne verwenden, um das SSL-Zertifikat ordnungsgemäß bereitzustellen, müssen Sie die folgenden Regionsendpunkte verwenden, um die URL-Route zur Verfügung zu stellen, die Ihrer Organisation in Bluemix zugeordnet ist. 

  * US-South: secure.us-south.bluemix.net 
  * EU-GB: secure.eu-gb.bluemix.net
  * AU-SYD: secure.au-syd.bluemix.net 


Um ein Zertifikat für Ihre Anwendung hochzuladen, gehen Sie wie folgt vor:

1. Erstellen Sie eine Route oder bearbeiten Sie eine vorhandene Route, indem Sie **Routen und App-Zugriff bearbeiten** im Anwendungsmenü auswählen.

2. Klicken Sie im Dialogfenster 'Routen und App-Zugriff bearbeiten' auf **Domänen verwalten**.

3. Klicken Sie für Ihre angepasste Domäne auf **Zertifikat hochladen**.

4. Navigieren Sie in der Liste, um ein Zertifikat, einen privaten Schlüssel und optional ein Zwischenzertifikat hochzuladen. Sie können auch das Kontrollkästchen auswählen, um Anforderungen eines Clientzertifikats zu aktivieren. Wenn Sie die Option zum Anfordern eines Clientzertifikats aktivieren, müssen Sie die Truststore-Datei eines Clientzertifikats hochladen, die den zulässigen Benutzerzugriff für Ihre angepasste Domäne definiert.

  **Zertifikat**
    
    Ein digitales Dokument, das einen öffentlichen Schlüssel an die Identität des Zertifikatsinhabers bindet, sodass der Zertifikatsinhaber authentifiziert werden kann. Ein Zertifikat wird von einer Zertifizierungsstelle ausgegeben und von dieser Zertifizierungsstelle digital signiert.
    
    Ein Zertifikat wird in der Regel ausgegeben und von einer Zertifizierungsstelle signiert. Für Test- und Entwicklungszwecke können Sie ein selbst signiertes Zertifikat verwenden. 
    
    Die folgenden Zertifikatstypen werden in {{site.data.keyword.Bluemix_notm}} unterstützt:

	* PEM (pem, .crt, .cer und .cert)
	* DER (.der oder .cer )
	* PKCS #7 (p7b, p7r, spc)
	  
  **Privater Schlüssel**
  
    Ein algorithmisches Muster, das verwendet wird, um Nachrichten zu verschlüsseln, die nur der zugehörige öffentliche
Schlüssel entschlüsseln kann. Mit dem privaten Schlüssel werden auch Nachrichten entschlüsselt, die vom entsprechenden öffentlichen Schlüssel
verschlüsselt wurden. Der private Schlüssel wird im System des Benutzers gespeichert und durch ein Kennwort geschützt.
    
    Die folgenden Typen von
privaten Schlüsseln werden in
{{site.data.keyword.Bluemix_notm}} unterstützt:
    
    * PEM (pem, .key)
    * PKCS #8 (p8, pk8)
    
    **Einschränkung:** Private Schlüssel, die durch eine Kennphrase geschützt sind, können nicht hochgeladen werden.
    
  **Zwischenzertifikat**
  
    Ein untergeordnetes Zertifikat, das von der Zertifizierungsstelle
für Trusted Roots speziell dafür ausgegeben wird, Serverzertifikate für End-Entitäten auszugeben. Im Ergebnis erhält man eine Zertifikatskette, die mit der
Zertifizierungsstelle für Trusted Roots beginnt und über das Zwischenzertifikat zum SSL-Zertifikat gelangt, das für die Organisation ausgegeben wird.
    
    Sie
sollten ein Zwischenzertifikat verwenden, um die Authentizität des Hauptzertifikats zu prüfen. Zwischenzertifikate werden normalerweise von einem vertrauenswürdigen
Dritten angefordert. Möglicherweise benötigen Sie kein Zwischenzertifikat, wenn Sie Ihre Anwendung vor der Bereitstellung für die Produktion
testen.
  
  **Anforderung eines Clientzertifikats aktivieren**
  
    Wenn Sie diese Option aktivieren, wird ein Benutzer bei dem Versuch, auf eine durch SSL geschützte Domäne zuzugreifen, aufgefordert, ein clientseitiges Zertifikat anzugeben. Beispiel:
Wenn in einem Web-Browser ein Benutzer versucht, auf eine SSL-geschützte Domäne zuzugreifen, wird der
Benutzer im Web-Browser dazu aufgefordert, für die Domäne ein Clientzertifikat bereitzustellen. Verwenden Sie die Option **Truststore für Clientzertifikate** zum Hochladen der Datei, um die clientseitigen Zertifikate zu definieren, die Sie für den Zugriff auf Ihre angepasste Domäne zulassen.
  
  **Hinweis:** Die Funktion für angepasste Zertifikate in der {{site.data.keyword.Bluemix_notm}}-Domänenverwaltung hängt von der SNI (Server Name Indication)-Erweiterung des TLS-Protokolls (Transport Layer Security) ab. Deshalb muss der Client-Code, der auf {{site.data.keyword.Bluemix_notm}}-Anwendungen zugreift, die durch angepasste Zertifikate geschützt sind, die SNI-Erweiterung in der TLS-Implementierung unterstützen. Weitere Informationen hierzu finden Sie im [Abschnitt 7.4.2 von RFC 4346](http://tools.ietf.org/html/rfc4346#section-7.4.2){:new_window}.

  **Truststore für Clientzertifikate**
  
  Der Truststore für Clientzertifikate ist eine Datei, in der die Clientzertifikate für die Benutzer enthalten sind, denen Sie Zugriff auf Ihre Anwendung gewähren möchten. Wenn Sie die Option zum Anfordern eines Clientzertifikats aktivieren, müssen Sie eine Truststore-Datei für Clientzertifikate hochladen. 
  
   Die folgenden Zertifikatstypen werden in {{site.data.keyword.Bluemix_notm}} unterstützt:
    
      * PEM (pem, .crt, .cer und .cert)
	  * DER (.der oder .cer )
      * PKCS #7 (p7b, p7r, spc)

Um ein Zertifikat zu löschen oder ein vorhandenes Zertifikat durch ein neues zu ersetzen, wechseln Sie zu
**Organisationen verwalten** > **Domänen** > **Zertifikat anzeigen**,
um Ihre Zertifikate zu verwalten.
