---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-03-17"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# IBM Cloud Identity and Access Management (IAM)
{: #iam_overview}

IBM Cloud IAM stellt ein sicheres Verfahren zur Verwaltung von Benutzer- und Serviceidentitäten und des Zugriffs auf Ressourcen für diese Identitäten bereit. Sie können Benutzer im Konto oder in der Organisation abhängig von den Zugriffsoptionen anzeigen, zu deren Verwaltung Sie berechtigt sind. Sie können alle Operationen für Benutzer ausführen, wie zum Beispiel Benutzer einladen und deren zugewiesene Rollen verwalten sowie Konten und/oder Organisationen verwalten, auf die diese Benutzer Zugriff haben. Als Kontoeigner können Sie die Zugriffsoptionen, deren Mitglieder sowohl Sie als auch die Benutzer sind, unabhängig von der Rolle im aktuellen Konto verwalten. 

Das Identity-Management umfasst die folgenden Tasks: 
 * Benutzermanagement 
   * Benutzerinformationen erstellen, löschen und aktualisieren
   * API-Key-Management
   * Token erstellen, aktualisieren und austauschen
   * Identitätsauthentifizierung von Benutzern
 * Service-ID-Management
   * Benutzerinformationen erstellen, löschen und aktualisieren
   * API-Key-Management
   * Token erstellen, aktualisieren und austauschen
   * Identitätsauthentifizierung für Services
   
   
Das Zugriffsmanagement umfasst die folgenden Tasks: 
 * Richtlinienmanagement
   * Richtlinien erstellen, löschen, aktualisieren
 * Entscheidungen zum Zugriff auf Ressourcen
 
## Identity - Übersicht
{: #identity}

Der Cloud IAM-Token-Service ist der Authentifizierungsservice für IBM Cloud und baut auf den offenen Standards auf, die in [OAuth 2.0]( https://tools.ietf.org/html/rfc6749), [JWT](https://tools.ietf.org/html/rfc7519), [JWT Profile](https://tools.ietf.org/html/rfc7523) und [JWKS](https://tools.ietf.org/html/rfc7517) spezifiziert werden. 

Ein Hauptzweck des Token-Service ist die Authentifizierung von Entwicklern, Operatoren und Administratoren für die IBM Cloud-Plattform. Für diese Authentifizierung wird der Token-Service mit dem IBMid-System verbunden, um Benutzer zu authentifizieren. In dedizierten und lokalen Umgebungen kann er auch mit einem vom Kunden ausgewählten Authentifizierungssystem wie LDAP verbunden werden.  

Zum Abrufen eines IAM-Tokens können Sie die OAuth 2.0-Bewilligungstypen ('grant_type') wie `password` (Kennwort) verwenden. Beispiel: 
```
curl
    -u "<Client-ID>:<geheimer_Clientschlüssel>"
    –H "Content-Type: application/x-www-form-urlencoded"
    –d "grant_type=password&username=<IBMid>&password=<IBMid-Kennwort>
       [&ims_account=<IMS-Konto>][&bss_account=<BSS-Konto>]
       [&response_type=cloud_iam,uaa,ims_portal]"
    "https://iam.ng.bluemix.net/oidc/token[?pretty=true]"
```
{: codeblock}

Als Erweiterung zu OAuth 2.0 müssen Sie Kontoinformationen angeben, um das Token-Konto spezifisch zu machen. Sie können außerdem verschiedene Antworttypen ('response_type') auflisten, um `UAA`- oder `IMS`-Tokens für Interaktionen mit Cloud Foundry-APIs oder IMS-APIs abzurufen. 

Über den Cloud-Token-Service können Sie API-Schlüssel für Benutzer erstellen, aktualisieren, löschen und verwenden. Diese API-Schlüssel können entweder durch API-Aufrufe oder über die Bluemix-Konsole erstellt werden. Zur Nutzung eines API-Schlüssels kann ein entsprechender Benutzer (Adopter) den folgenden erweiterten Bewilligungstyp verwenden: 
```
curl
    -u "<Client-ID>:<geheimer_Clientschlüssel>"
    –H "Content-Type: application/x-www-form-urlencoded"
    –d "grant_type=urn:ibm:params:oauth:grant-type:apikey&
       apikey=<API-Schlüsselwert>[&response_type=cloud_iam,uaa,ims_portal]"
    "https://iam.ng.bluemix.net/oidc/token[?pretty=true]"
```
{: codeblock}

Das resultierende Token kann wie ein durch eine Kennwortbewilligung oder eine UI-Anmeldung abgerufenes Token verwendet werden. 

Als weitere Variation bietet Ihnen der Cloud-IAM-Token-Service die Möglichkeit, sich interaktiv über die Benutzerschnittstelle anzumelden. Diese Möglichkeit wurde mithilfe des OAuth 2.0-Bewilligungstyps `authorization_code` implementiert, der auch als `OAuth Dance` bezeichnet wird, weil er mehrere Web-Browser-Umleitungen während der Authentifizierungsphase verursacht. 

Der andere Hauptzweck des Token-Service ist die Möglichkeit, Service-IDs und API-Schlüssel für Service-IDs zu erstellen. Eine Service-ID ist einer "Funktions-ID" oder einer "Anwendungs-ID" ähnlich und wird zur Authentifizierung bei Services, jedoch nicht zum Darstellen eines Benutzers verwendet. 

Benutzer können Service-IDs erstellen und an Bereiche binden, wie zum Beispiel an ein Bluemix-Konto, eine Cloud Foundry-Organisation oder einen Cloud Foundry-Bereich. Diese Bindung hat den Zweck, der Service-ID einen Container zu Verwaltungszwecken zuzuordnen. Darüber hinaus definiert dieser Container, wer die Service-ID aktualisieren und löschen kann und wer API-Schlüssel, die dieser Service-ID zugeordnet sind, erstellen, aktualisieren, lesen und löschen kann. Eine Service-ID gehört NICHT zu einem Benutzer. 

Wenn Sie sich mit der Verwendung von Service-IDs näher vertraut machen möchten, können Sie die [Demo-Anwendung](https://iam.ng.bluemix.net/demo) ausprobieren, die die APIs demonstriert. 

## Zugriffsmanagement - Übersicht
{: #access_management}

IAM ist ein attributbasiertes Zugriffssteuerungssystem (ABAC - Attribute Based Access Control) mit Bedingungen, die durch die [NIST](http://nvlpubs.nist.gov/nistpubs/specialpublications/NIST.sp.800-162.pdf)-Veröffentlichung motiviert wurden.  

IAM arbeitet mit einer Kombination aus Attributen, um den Zugriff auf Ressourcen zu bestimmen. IAM-Richtlinien haben Regeln, die auf die Rollen, die Attribute für Benutzer und Service-IDs, Ressourcenattribute und Bedingungen angewendet werden. Dies bietet flexible und leistungsfähige Möglichkeiten zum Definieren des Zugriffs für Benutzer und Service-IDs. 

Eine virtuelle Maschine VM123 kann zum Beispiel die folgenden Attribute haben:  
```
    resource: {
      'serviceName': 'virtual-machine',
      'region': 'us-south',
      'resourceType': 'vm',
      'resource': 'vm123'
    }
```
{: codeblock}
  
Eine beliebige Kombination dieser Ressourcenattribute kann zum Erstellen einer Richtlinie verwendet werden.

Detailliertere Beispiele finden Sie unter [Beispiele für IAM-Richtlinien](https://console.stage1.ng.bluemix.net/docs/developing/Access-Management/policy_examples.html#iam_policy_examples).

Die attributbasierte Zugriffssteuerung (ABAC) unterscheidet sich von der rollenbasierten Zugriffssteuerung (RBAC), bei der Benutzern vordefinierte Rollen zugewiesen werden. Diese vordefinierten Rollen haben bestimmte Berechtigungen und Benutzer mit einer bestimmten Rolle haben alle Berechtigungen, die durch diese Rolle definiert werden.  
 
Beispiel: Eine Rolle `Administrator` für eine virtuelle Maschine. Diese Rolle impliziert alle Berechtigungen vom Typ 'Administrator' auf einer beliebigen Ressource für virtuelle Maschine.  

Eine attributbasierte Zugriffssteuerung lässt sich im Grunde wie folgt verstehen: 

1. Es gibt Benutzer, Ressourcen, Kontexte und Aktionen. 
1. Jede Instanz eines Benutzers, einer Ressource, eines Kontexts und einer Aktion hat eine eindeutige ID. 
1. Jeder Instanz werden Attribute zugeordnet.
   Dadurch wird eigentlich Folgendes definiert: "Was ist gilt für die Instanz aus Berechtigungsperspektive?".
   Beispiele: 
   1. Der Benutzer hat das Sternbild Fische und wurde in den 1960ern geboren. 
   1. Die Ressource ist eine Baseball-Teamliste. 
   1. Der Kontext ist 9:00 AM bis 5:00 PM Eastern Time. 
   1. Die Aktion ist "kann aktualisieren". 
1. Richtlinien werden erstellt, um festzulegen, welche Gruppe von Attributen dem Benutzer die Berechtigung gibt, die Aktion für die Ressource auszuführen. 
1. Wenn eine Anforderung von einem Benutzer eingeht, eine Aktion an einer Ressource auszuführen, werden die Richtlinien abgefragt, um zu prüfen, ob die Anforderung zugelassen wird. 

Die folgende Abbildung zeigt eine detaillierte Ansicht der Berechtigungssequenz. 

![Berechtigungssequenz](auth_sequence.png)

## Zugriffssteuerung für einen Service einrichten
{: #setup_access_mgmt}

Das Onboarding eines Service für {{site.data.keyword.Bluemix_notm}} besteht aus einer anderen Gruppe von Operationen als das Onboarding eines Service für Cloud-IAM. Technisch können Sie das Onboarding für {{site.data.keyword.Bluemix_notm}} und das Onboarding für Cloud-IAM unabhängig voneinander und in beliebiger Reihenfolge durchführen. Das Cloud-IAM-Team arbeitet mit dem Onboarding-Team für {{site.data.keyword.Bluemix_notm}}-Services zusammen, sodass der Onboarding-Prozess für {{site.data.keyword.Bluemix_notm}}-Services auch das Cloud-IAM-Onboarding umfasst.

Zur Einrichtung der Zugriffssteuerung für Ihren Service müssen Sie die folgenden Schritte im Rahmen Ihres Onboarding-Prozesses ausführen: 

### Schritt 1: Erstellen Sie eine Service-ID, indem Sie die folgende HTTP-Anforderung ausführen: 
```
  POST https://iam.ng.bluemix.net/serviceids
  Authorization: <Bluemix-Token>
  Content-Type: application/json

  {
    "name": "<Name_für_Service-ID>",
    "description": "<Beschreibung_für_Service-ID>",
    "boundTo": "<CRN>"
  }
```
{: codeblock}

Curl-Befehl:
```  
curl -X POST -H 'Authorization: <Bluemix-Token>' -H 'Content-Type: application/json' -d '{"name": "<Name_für_Service>", "description": "<Beschreibung_für_Service-ID>", "boundTo": "<CRN>"}' 'https://iam.ng.bluemix.net/serviceids'
```
{: codeblock}

Im Folgenden werden die Werte für `Service-ID` und `Service-CRN` ausführlicher beschrieben, die in dem `curl`-Befehl verwendet werden: 
  
#### Feld für die Service-ID 
  
Der Name der Service-ID kann derselbe wie der Servicename sein, der in den CRN-Feldern für Ihren Service enthalten ist. 
  
Ihre Service-ID muss an ein Konto, eine Organisation oder einen Bereich gebunden sein. Diese Bindung bestimmt, wer Ihre Service-ID verwalten kann. Beispiel: Der Administrator, an den Ihre Service-ID gebunden ist, kann sie aktualisieren oder löschen. Ihr {{site.data.keyword.Bluemix_notm}}-Token muss Zugriff auf das Element (Konto, Organisation und Bereich) haben, an das Sie die ID binden. Zum Binden an ein Konto muss das CRN-Feld `boundTo` wie folgt aussehen:  

`crn:v1:::<Servicename>::a/<Konto-ID>:::` 
  
Für eine Organisation muss es wie folgt aussehen:
`crn:v1:<CNAME>:<ctype>:<Servicename>:<Region>:o/<Organisations-ID>:::` 
  
Für einen Bereich muss es wie folgt aussehen:
`crn:v1:<CNAME>:<ctype>:<Servicename>:<Region>:s/<Bereichs-ID>:::`  
  
Der Wert `boundTo`, der angegeben wird, hat keine Auswirkung darauf, auf welche Ressourcen Ihre Service-ID zugreifen kann.  
  
IAM-Zugriffsrichtlinien steuern, auf welche Ressourcen Ihre Service-ID zugreifen kann. Auch wenn Ihre Service-ID an eine IBM Organisation gebunden ist, können IAM-Richtlinien erstellt werden, die Ihrer Service-ID den Zugriff auf Ressourcen außerhalb dieser Organisation erlauben. Wenn Sie ein Onboarding mit IAM durchführen, ermöglicht die erste Zugriffsrichtlinie, die durch das IAM-Team erstellt wird, der Service-ID das Erstellen von Richtlinien für beliebige Ressourcen, deren Eigner Ihr Service ist. 

Weitere Informationen zu dieser API und zugehörigen APIs finden Sie unter [createServiceid](https://iam.stage1.ng.bluemix.net/ibm/api/explorer/). 

#### CRN-Feld für den Service

Der Servicename im CRN-Feld `boundTo` muss mit dem Servicenamen übereinstimmen, der im CRN-Feld für Ihren Service enthalten ist. 
  
Hilfeinformationen zum Ausfüllen dieser Felder finden Sie unter [CRN-Spezifikation](https://github.ibm.com/ibmcloud/builders-guide/blob/master/specifications/crn/CRN.md). 

Speichern Sie aus der Antwort die Werte 'metadata->uuid' und 'metadata->crn', bei denen es sich um Ihre Service-ID und den CRN-Wert für Ihre Service-ID handelt.


### Schritt 2: Nehmen Sie Kontakt mit der 'AccessControl Squad' unter [#iam-adopters](https://ibm-cloudplatform.slack.com/messages/iam-adopters) auf.  
Ihrer Service-ID wird die Rolle 'Administrator' der Richtlinien für die Ressourcen Ihres Service erteilt. 

Verwenden Sie das folgende Format:
```
IAM adopter service info

service id: UUID aus Schritt 1
service name: Ihr Servicename wie in den CRN-Feldern für Ihren Service
```
{: codeblock}

### Schritt 3: Sie müssen einen API-Schlüssel aus Ihrer Service-ID erstellen. Verwenden Sie die folgende HTTP-Anforderung: 
```
  POST https://iam.ng.bluemix.net/apikeys
  Authorization: <Bluemix-Token>
  Content-Type: application/json

  {
    "boundTo": "<CRN für Service-ID>",
    "name": "<Name des API-Schlüssels>",
    "description": "<Beschreibung des API-Schlüssels>"
  }
```
{: codeblock}

Curl-Befehl: 
```
  curl -X POST -H 'Authorization: <Bluemix-Token>' -H 'Content-Type: application/json' -d '{"boundTo": "<CRN für Service-ID>", "name": "<Name des API-Schlüssels>", "description": "<Beschreibung des API-Schlüssels>"}' https://iam.ng.bluemix.net/apikeys
```
{: codeblock}

Der Wert in `boundTo` muss der CRN-Wert Ihrer Service-ID sein (Feld 'metadata->crn' das aus der Antwort von Schritt 1 gespeichert wurde). Der Name und die Beschreibung können beliebig gewählt werden. 

Speichern Sie aus der Antwort den Wert 'entity->apiKey'. 

Weitere Informationen zu dieser API und zugehörigen APIs finden Sie unter [createAPIKey](https://iam.stage1.ng.bluemix.net/ibm/api/explorer/#!/Cloud_IAM_Service_Id_and_Api_Key_MVP/createAPIKey). 

### Schritt 4: Rufen Sie ein Zugriffstoken für den API-Schlüssel Ihrer Service-ID ab.  

Wenn die Berechtigung eingerichtet ist, kann Ihr Service PAP- und PDP-Anforderungen für die Ressourcen Ihres Service ausführen. 

Verwenden Sie das Entity-Feld **apiKey** aus Schritt 3, bei dem es sich um Ihren API-Schlüsselwert (apikey_value) handelt. 

  * Rufen Sie dann das Token mit dem API-Schlüsselwert ab (stellen Sie sicher, dass Sie Escapezeichen verwenden): 

    Curl-Command:
```
    curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -H "Accept: application/json" -d "grant_type=urn%3Aibm%3Aparams%3Aoauth%3Agrant-type%3Aapikey&apikey=<apikey_value>" "https://iam.ng.bluemix.net/oidc/token"
```
{: codeblock}

Verwenden Sie das Feld **access_token** im Ergebnis, bei dem es sich um Ihr API-Schlüsseltoken (für Ihre Service-ID) handelt. Das Zugriffstoken (**access_token**) muss URL-codiert sein, wenn es in dem curl-Befehl verwendet wird, der zuvor gezeigt wurde. 


### Schritt 5: Registrieren Sie die Liste der möglichen Serviceaktionen für den Servicenamen. 

  a. Ordnen Sie Rollen, die im IAM-System definiert sind, Serviceaktionen zu. Diese Zuordnung wird später bei der Serviceregistrierung verwendet. 

  * Eine Liste der im IAM-System definierten Rollen (IAM System Defined Roles) können Sie durch die folgende Anforderung abrufen: 
  
Curl-Befehl:
```
curl -X GET --header 'Accept: application/json' --header 'Authorization: <API-Schlüsseltoken>' 'https://iampap.ng.bluemix.net/acms/v1/roles'
```
{: codeblock}

**Hinweis:** Verwenden Sie die *CRN-Version* der im IAM-System definierten Rollen in den Nutzdaten Ihrer Serviceregistrierung. 

Das folgende Beispiel zeigt eine Zuordnung von Serviceaktionen zu Rollen. 

  <table>
    <tr>
      <th>API-Endpunkt</th>
      <th>Serviceaktion</th>
      <th>Im IAM-System definierte Rollen</th>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}</td>
      <td>key-protect.keys.create</td>
      <td>Administrator</td>
    </tr>
    <tr>
      <td>GET /api/keys/{key_id}</td>
      <td>key-protect.keys.read</td>
      <td>Viewer, Editor, Administrator</td>
    </tr>
    <tr>
      <td>PUT /api/keys/{key_id}</td>
      <td>key-protect.keys.update</td>
      <td>Editor, Administrator</td>
    </tr>
    <tr>
      <td>DELETE /api/keys/{key_id}</td>
      <td>key-protect.keys.delete</td>
      <td>Administrator</td>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}/encode</td>
      <td>key-protect.keys.encode</td>
      <td>Editor, Administrator</td>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}/decode</td>
      <td>key-protect.keys.decode</td>
      <td>Editor, Administrator</td>
    </tr>
  </table>

  b. Verwenden Sie die folgende Befehlszeile, um Ihren Service beim Richtlinienverwaltungspunkt (`PAP` - Policy Administration Point) zu registrieren: 
```
  curl -X PUT -H 'Content-Type: application/json' -H 'Accept: application/json' -H 'Authorization: <API-Schlüsseltoken>' -d '{
    "displayName": {
      "default": <Serviceanzeigename>
    },
    "actions": [{
      "id": <Serviceaktion>,
      "displayName": {
        "default": <Anzeigename der Serviceaktion>
      },
      "roles": [<system_defined_role_crn>]
    }]
  }' 'https://iampap.ng.bluemix.net/acms/v1/services/<Servicename>'
  ```
{: codeblock}
  
Aktionen müssen wie im [Serviceaktionformat](https://console.stage1.ng.bluemix.net/docs/developing/Access-Management/index.html#action_format) spezifiziert definiert werden. 
  
Das Standardformat sieht zum Beispiel wie folgt aus: 

  `<Servicename>.<Komponente>.<Verb>`
  
  Mit der Aktion `key-protect.keys.decode` aus dem obigen Beispiel:  
  * Servicename = key-protect
  * Komponente = keys
  * Verb = decode
  

### Schritt 6: Überprüfen Sie den registrierten Service entsprechend den Details in Schritt 5. 

```
curl -H "Authorization: <API-Schlüsseltoken>" "https://iampap.ng.bluemix.net/acms/v1/services/<Servicename>"
```

### Schritt 7 (Optional): Löschen Sie den Service, den Sie in Schritt 5 registriert haben. 

```
curl -X DELETE -H "Authorization: <API-Schlüsseltoken>" "https://iampap.ng.bluemix.net/acms/v1/services/<Servicename>"
```

### Schritt 8: Konfigurieren Sie den Service zur Verwendung des PEP-SDK, um Berechtigungen mit dem PDP zu überprüfen. Wählen Sie die entsprechende SDK-Sprache aus. 

  * [PEP-SDK für Java](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Java)
  * [PEP-SDK für Nodejs](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Node)
  * [PEP-SDK für Python](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Python)
 

## Terminologie
{: #terminology}

### Identity-Terminologie

* IBMid - Eine Identität, die von IBM für den Zugriff auf IBM Cloud, IBM Anwendungen, Communitys und Support bereitgestellt und gehostet wird. 
* Benutzer-ID - Eine Kennung, die eine reale Person darstellt. 
* Service-ID - Eine Kennung, die einen technischen Benutzer, eine Maschine, eine Anwendung oder Services darstellt. Diese Kennung ist "Funktions-IDs" oder "Anwendungs-IDs" ähnlich, die ebenfalls einen technischen Benutzer darstellen, jedoch wird für diese Kennung der Entitätstyp "Benutzer-ID" verwendet. 
* OAuth 2.0 - Ein offener Standard für die Autorisierung von Zugriff auf Anwendungen und APIs ohne Angabe von Berechtigungsnachweisen für den Zielservice. OAuth wird auch zur Aufbewahrung von Authentifizierungsdaten verwendet.
* OpenID Connect - Ein offener Standard, der auf OAuth 2.0 aufsetzt und in erster Linie auf das Bereitstellen von Informationen zu dem authentifizierten Benutzer ausgerichtet ist.
* Client-ID - Anwendungen, die mit OAuth 2.0-konformen Endpunkten interagieren, benötigen zur Authentifizierung ein geheimes Wertpaar aus Client-ID und geheimem Schlüssel. Eine Anwendung muss bei einem Token-Service registriert werden, um eine Client-ID abzurufen. 
* Tokenendpunkt - Wird vom Client zum Abrufen eines oder mehrerer Tokens verwendet, indem er Identitätsinformationen wie einen Benutzernamen oder ein Kennwort, eine Berechtigungsbewilligung oder ein Aktualisierungstoken einreicht.
* Berechtigungsendpunkt - Wird vom Client für die Authentifizierung eines Benutzers über die Benutzerschnittstelle (UI) beim Token-Service verwendet.
* Token - Eine nicht transparente Zeichenfolge, die es einer Anwendung ermöglicht, die Authentifizierung und/oder Berechtigung einer Identität abzurufen.
* Zugriffstoken - Dieses Token wird als Form von Identitätsinformationen für APIs herumgesendet. Es enthält Identitätsinformationen und gilt nur für eine kurze Zeit.
* Aktualisierungstoken - Dieses Token wird auf dem Client gespeichert, der nur eine Authentifizierung angefordert hat. Es wird zum Abrufen eines neuen Zugriffstokens (d. h. zur Aktualisierung des Zugriffstokens) verwendet, wenn das Zugriffstoken abläuft. Da das Aktualisierungstoken eine lange Gültigkeit besitzt, darf es das Clientsystem nur für den Zweck der Aktualisierung des eigentlichen Zugriffstokens verlassen.
* Identitätscookie - Nach der Anmeldung beim IBM Cloud-Token-Service wird ein Cookie mit Ihrer Identität an Ihren Browser ausgegeben. Sie werden nicht zur erneuten Anmeldung aufgefordert, solange dieses Cookie vorhanden und gültig ist. Es läuft nach 24 Stunden ab, wenn Sie sich vom IBM Cloud-Token-Service abmelden oder Ihren Browser schließen. 
* JSON Web Token - Ein JSON-basierter Standard (RFC 7519) zur Darstellung von Zugriffstokens. Der Inhalt dieses Zugriffstokens ist transparent (d. h. er ist leicht lesbar). Ein JWT-basiertes Token ist in der Regel signiert, um den Herkunftsnachweis dieses Tokens überprüfbar zu machen.
* Öffentlicher Schlüssel - Kann zum Prüfen einer Signatur eines JSON Web Tokens verwendet werden. Bei asymmetrischer Verschlüsselung kann der öffentliche Schlüssel gefahrlos zur Verwendung durch Clients veröffentlicht werden.
* Privater Schlüssel - Kann zum Prüfen einer Signatur für ein JSON Web Token verwendet werden. Dieser Schlüssel muss geheimgehalten werden, da andernfalls andere Personen gültige Zugriffstoken erstellen könnten.
* Realm-ID (realmid) - Eine Kennung zur Unterscheidung von Benutzern aus verschiedenen Benutzerregistrys. Gegenwärtig werden der Wert "IBMid" für Benutzer, die durch das IBMid-System authentifiziert werden, und der Wert "iam" für Service-IDs, die durch den Token-Service authentifiziert werden, verwendet.
* Kennung (ID) - Eine Kennung, die sich nie ändert und einen Benutzer innerhalb einer Benutzerregistry (durch den Parameter `realmid` angegeben) eindeutig identifiziert. Die Kombination aus Realm-ID und Kennung (<realmid>-<kennung>) muss immer einen eindeutig identifizierbaren Benutzer bezeichnen. Im Fall von IBMid wird die eindeutige IBM Kennung 'IUI' verwendet.             
* Subjekt - Der Benutzername der Identität. Häufig in der gleichen Form wie eine E-Mail-Adresse. Im Fall von IBMid ist dies die IBMid der Identität.
* Angepasste Anforderungen (Custom Claims) - Zusätzliche, vom Standard abweichende Informationen in einem JSON Web Token.

### Zugriffsmanagementterminologie

* (PAP) Policy Administration Point - Richtlinienverwaltungspunkt, über den Zugriffsberechtigungsrichtlinien verwaltet werden. 
* (PDP) Policy Decision Point - Richtlinienentscheidungspunkt, der Zugriffsanforderungen mithilfe von Berechtigungsrichtlinien auswertet, bevor er Zugriffsentscheidungen ausgibt. 
* (PEP) Policy Enforcement Point - Richtliniendurchsetzungspunkt, der die Zugriffsanforderung eines Benutzers für eine Ressource abfängt und eine Entscheidungsanforderung an den PDP sendet, um die Zugriffsentscheidung abzurufen (d. h., der Zugriff auf die Ressource wird genehmigt oder abgelehnt), und anschließend der empfangenen Entscheidung entsprechend verfährt. 
* (PIP) Policy Information Point - Richtlinieninformationspunkt, der als Quelle für Attributwerte (d. h. für Ressource, Subjekt, Umgebung) fungiert.
* (PRP) Policy Retrieval Point - Richtlinienabrufpunkt, an dem die XACML-Zugriffsberechtigungsrichtlinien gespeichert werden, in der Regel eine Datenbank oder das Dateisystem. 
* Subjekt (Subject) - Das "Wer" in einem Autorisierungspaar aus Ressource und Subjekt, wie zum Beispiel ein Benutzer oder eine Gruppe. Die Ressource ist die Ressource, auf die das Subjekt zugreifen kann.
* Rolle - Eine Gruppe von Berechtigungen, die einem Benutzer, einer Gruppe von Benutzern, einem System, einem Service oder einer Anwendung zugewiesen werden kann, um die Ausführung bestimmter Tasks zuzulassen. 
* Ressource - Ein physisches oder logisches Objekt, für das Aktionen ausgeführt werden können, wie zum Beispiel eine Organisation, ein Bereich, eine Datenbank oder eine Tabelle.
* Bedingungen - Funktionen, deren Auswertung den Wert "True" (Wahr), "False" (Falsch) oder “Indeterminate” (Unbestimmt) ergibt.
* Aktion - Eine definierte Task, die eine Anwendung an einem Objekt oder einer Ressource infolge eines Ereignisses ausführt.
* Richtlinie - Ein Satz von Regeln, eine Kennung für den Algorithmus zur Kombination von Regeln und (optional) eine Gruppe von Verpflichtungen oder Ratschlägen. Kann Komponente eines Richtliniensatzes sein. 

## Systemdefinierte Rollen
{: #system_defined_roles}

IBM Cloud-Rollen stellen eine Sammlung von Aktionen dar, die durch IAM aktivierte Services bereitgestellt werden. 

Die Gruppierung von Aktionen in Rollen bietet Flexibilität für die Unterstützung von Aktionen für Services und Ressourcen unter Verwendung eines minimalen Satzes an systemdefinierten Rollen. Wenn Sie zum Beispiel einen `Administrator` für VMs, Speicher und Vernetzung benötigen, können Sie die Rolle `Administrator` für alle drei Zwecke verwenden und einfach jeweils das Ziel der Richtlinie ändern. `Administrator` für VMs, `Administrator` für Storage (Speicher) und `Administrator` für Networking (Vernetzung). 

*Was IBM Cloud IAM nicht tut:* Eine Alternative, die von anderen Zugriffsmanagementsystemen verwendet wird, besteht darin, Ressourcen in die Rolle einzubeziehen. Dieses Konzept hat jedoch implizit einen neuen Rollennamen für jeden Typ von Ressource zur Folge, der in das System eingeführt wird. Bei diesem Verfahren wären zum Beispiel eine Rolle `VMAdministrator`, eine Rolle `StorageAdministrator` und eine Rolle `NetworkAdministrator` erforderlich, um die Verwaltung für VM-, Speicher- und Netzressourcen abzudecken. 


In der folgenden Tabelle sind die durch das IAM-System definierten Rollen und Beispiele für Aktionen, die ihnen zugeordnet sind, aufgeführt. 

|IBM Cloud-Rollenname| Beschreibung | Beispielaktionen|
|:-----------------|:-----------------|:-----------------|
|Viewer (Anzeigeberechtigter)|Aktionen, die den Status nicht ändern (z. B. Lesezugriff)| <ul><li>Geräte auflisten</li><li>Speicherobjekt lesen</li><li>Abfrage ausführen</li><li>Suche ausführen</li></ul>|
|Editor (Bearbeiter)|Aktionen, die den Status ändern und Unterressourcen erstellen/löschen können|<ul><li>VM erstellen</li><li>VM löschen</li><li>Speicher anhängen</li><li>Neu starten</li><li>Starten/stoppen</li><li>Umbenennen</li></ul>|
|Operator (Bediener)|Aktionen, die zum Konfigurieren und Betreiben von Ressourcen erforderlich sind|<ul><li>Konfiguration aktualisieren</li><li>VM starten/stoppen</li><li>Protokolle anzeigen</li><li>Backup/Restore durchführen</li></ul>|
|Administrator|Alle Aktionen, einschließlich der Möglichkeit, die Zugriffssteuerung zu verwalten|<ul><li>Benutzer einladen</li><li>VM erstellen</li>Benutzerzugriffsrichtlinien aktualisieren</li><li>Geräte auflisten</li><li>VM erstellen</li><li>VM löschen</li><li>Speicher anhängen</li><li>Neu starten</li><li>Starten/stoppen</li><li>Umbenennen</li><li>Backup/Restore durchführen</li></ul>|
|Abrechnungsadministrator|Aktionen in Bezug auf die Verwaltung der Rechnungsstellung|<ul><li>Kreditkarte aktualisieren</li><li>Rechnungen auflisten</li><li>Rechnungen herunterladen</li></ul>|

Die aktuellste Liste der systemdefinierten Rollen kann über den PAP-Microservice abgerufen werden. 

Curl-Befehl: 

`curl -X GET --header 'Accept: application/json' --header 'Authorization: <API-Schlüsseltoken>' 'https://iampap.ng.bluemix.net/acms/v1/roles'`
    
    
## Serviceaktionsformat
{: #action_format}

Aktionen müssen in einem von zwei Formaten definiert werden: 
  
* Standard:

    `<Servicename>.<Komponente>.<Verb>`
* Zugriffssteuerungsabfangpunkt (Access Control Intercept Point): 

    `<METHODE> /<API-Route>`
  
### Standard
Die meisten Services rufen den IAM-Richtlinienentscheidungspunkt (PDP - Policy Decision Point) direkt auf und können Quellcode ändern, um das Standardaktionsformat zu unterstützen.   
 
 Dieses Format muss alle drei Teile enthalten und alphanumerisch sein, ohne Leerzeichen oder Sonderzeichen mit Ausnahme von '-'. 

`<Servicename>.<Komponente>.<Verb>`

Dabei gilt: 
* Servicename - Der Servicename, der im CRN-Feld für den Servicenamen definiert ist. 
* Komponente - Die Ressource oder Unterressource des Service. 
* Verb - Das Verb, das die unterstützte Aktion für die Servicenamenkomponente definiert.  
  
Beispiel: `key-protect.keys.decode` 
* Servicename = key-protect
* Komponente = keys
* Verb = decode

### Zugriffssteuerungsabfangpunkt für die REST-API
{: intercept_point}

In einigen Fällen werden REST-API-Anforderungen durch ein Gateway geleitet, das als Abfangpunkt für die Zugriffssteuerung (Access Control Intercept Point) fungiert. Der IAM-Richtlinienentscheidungspunkt (PDP) wird direkt von dem Abfangpunkt aufgerufen, bevor der tatsächliche REST-API-Service aufgerufen wird. Der Service, der die REST-API-Anforderung verarbeitet, ruft den IAM-Richtlinienentscheidungspunkt nie auf. 

Dem Abfangpunkt sind nur die REST-API-Route und der Endpunkt bekannt, an den die Anforderungen zu senden ist. Weitere Informationen finden Sie unter [Informationen zu Abfangpunkten für die Zugriffssteuerung](https://console.stage1.ng.bluemix.net/docs/developing/Access-Management/intercept_point.html#intercept_point_overview). 


 Dieses Format muss alle beide Teile enthalten und unterstützt sichere Zeichen für URLs wie in [RFC 1738](https://www.ietf.org/rfc/rfc1738.txt) spezifiziert. 
 
 
`<METHODE> /<API-Route>`
  
Dabei gilt:
* METHODE - Die Methode der REST-API.  
* API-Route - Der URI für die REST-API. 

Beispiel: `GET /v1/things/thing123`
* METHODE = GET
* API-Route = /v1/things/thing123

<!---
# Setting up access control for your service
{: #setup_access_mgmt}

Onboarding a service to {{site.data.keyword.Bluemix_notm}} is a different set of operations than onboarding a service with Cloud IAM. Technically you can onboard with {{site.data.keyword.Bluemix_notm}} and Cloud IAM independently and in any order. The Cloud IAM team is working with the {{site.data.keyword.Bluemix_notm}} service onboarding team so that the {{site.data.keyword.Bluemix_notm}} service on boarding process will also include Cloud IAM onboarding.

To setup access control for your service you must use the following steps.

#### Step 1: Create a service id by making this http request:
  ```
  POST https://iam.ng.bluemix.net/serviceids
  Authorization: <bluemix token>
  Content-Type: application/json

  {
    "name": "<service id name>",
    "description": "<service id description>",
    "boundTo": "<crn>"
  }
  ```
Curl command:
  ```  
  curl -X POST -H 'Authorization: <bluemix token>' -H 'Content-Type: application/json' -d '{"name": "<service id name>", "description": "<service id description>", "boundTo": "<crn>"}' 'https://iam.ng.bluemix.net/serviceids'
  ```
  
### Service id 
  
The service id name can be the same as the service name that appears in the crns for your service.
  
Your service id must be bound to an account, organization, or space. This binding determines who can manage your service id. For example, the administrator where your service id is bound are able to update or delete. Your {{site.data.keyword.Bluemix_notm}} token needs to have access to the account, organization, and space you are binding the id to. To bind to an account, the `boundTo` crn must look like the following: 

`crn:v1:::<service name>::a/<account id>:::` 
  
For an organization it must look like the following:
`crn:v1:<cname>:<ctype>:<service name>:<region>:o/<organization id>:::` 
  
For a space it must look like the following:
`crn:v1:<cname>:<ctype>:<service name>:<region>:s/<space id>:::`  
  
The `boundTo` value specified has no affect on which resources your service id can access. 
  
IAM access policies control which resources your service id can access. Even though your service id is bound to an IBM organization, IAM policies can be created that allow your service id to access resources outside of that organization.  When on boarding with IAM the first access policy that is created by the IAM team allows the service id to create policies for any resources owned by your service.

See [createServiceid](https://iam.stage1.ng.bluemix.net/ibm/api/explorer/#!/Cloud_IAM_Service_Id_and_Api_Key_MVP/createServiceid) for more information on this api and related apis.

###Service crn

The service-name in the `boundTo` crn must match the service name that appears in the crn for your service.
  
See the [CRN spec](https://github.ibm.com/ibmcloud/builders-guide/blob/master/specifications/crn/CRN.md) for help filling in these fields.

From the response, save metadata&ndash>uuid and metadata&ndash>crn, which are your service id and service id crn.


#### Step 2: Contact the AccessControl Squad at [#iam-adopters](https://ibm-cloudplatform.slack.com/messages/iam-adopters). 
Your service id will be given the role of Administrator of policies for your service's resources.

Use this format:
```
IAM adopter service info

service id: uuid from step #1
service name: your service name as it will appear in the crns for your service
```

#### Step 3: You must create an api key from your service id. Use the following http request:
```
  POST https://iam.ng.bluemix.net/apikeys
  Authorization: <bluemix token>
  Content-Type: application/json

  {
    "boundTo": "<service id crn>",
    "name": "<api key name>",
    "description": "<api key description>"
  }
```
Curl command: 
```
  curl -X POST -H 'Authorization: <bluemix token>' -H 'Content-Type: application/json' -d '{"boundTo": "<service id crn>", "name": "<api key name>", "description": "<api key description>"}' https://iam.ng.bluemix.net/apikeys
```
`boundTo` needs to be the crn of your service id (field metadata&ndash>crn saved from step 1’s response). The name and description can be anything.

From the response, save entity&ndash>apiKey.

See [createAPIKey](https://iam.stage1.ng.bluemix.net/ibm/api/explorer/#!/Cloud_IAM_Service_Id_and_Api_Key_MVP/createAPIKey) for more information on this api and related apis.

#### Step 4: Get an access token for your service id's API key. 

When the permission is established, your service can make PAP and PDP requests for your service's resources.

Use the entity **apiKey** field from step #3, this is your API key value (apikey_value).

  * Then get the token with the API key value (make sure you use escape characters):

    Curl Command: 
    ```
    curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -H "Accept: application/json" -d "grant_type=urn%3Aibm%3Aparams%3Aoauth%3Agrant-type%3Aapikey&apikey=<apikey_value>" "https://iam.ng.bluemix.net/oidc/token"
    ```

Use the **access_token** field in the result, this is your api key token(for your service id).


#### Step 5: Register the list of possible service actions for the service name.

  a. Map service actions to IAM System Defined Roles. This mapping is used later during the service registration.

  * A list of IAM System Defined Roles can be found by performing the following request:
Curl command:
```
curl -X GET &ndash&ndashheader 'Accept: application/json' &ndash&ndashheader 'Authorization: <api key token>' 'https://iampap.ng.bluemix.net/acms/v1/roles'
```

**Note:** Use the _crn version_ of the IAM System Defined Roles in your service registration payload.

The following is an example of mapping service actions to roles.

  <table>
    <tr>
      <th>API Endpoint</th>
      <th>Service Action</th>
      <th>IAM System Defined Roles</th>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}</td>
      <td>key-protect.keys.create</td>
      <td>Administrator</td>
    </tr>
    <tr>
      <td>GET /api/keys/{key_id}</td>
      <td>key-protect.keys.read</td>
      <td>Viewer, Editor, Administrator</td>
    </tr>
    <tr>
      <td>PUT /api/keys/{key_id}</td>
      <td>key-protect.keys.update</td>
      <td>Editor, Administrator</td>
    </tr>
    <tr>
      <td>DELETE /api/keys/{key_id}</td>
      <td>key-protect.keys.delete</td>
      <td>Administrator</td>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}/encode</td>
      <td>key-protect.keys.encode</td>
      <td>Editor, Administrator</td>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}/decode</td>
      <td>key-protect.keys.decode</td>
      <td>Editor, Administrator</td>
    </tr>
  </table>

  b. Use the following command line to register your service with the `PAP`:
```
  curl -X PUT -H 'Content-Type: application/json' -H 'Accept: application/json' -H 'Authorization: <api key token>' -d '{
    "displayName": {
      "default": <service display name>
    },
    "actions": [{
      "id": <service_action>,
      "displayName": {
        "default": <service action display name>
      },
      "roles": [<system_defined_role_crn>]
    }]
  }' 'https://iampap.ng.bluemix.net/acms/v1/services/<service_name>'
  ```
  
Actions must be defined as specified in the 
[Service Action Format](https://console.stage1.ng.bluemix.net/docs/developing/Access-Management/index.html#action_format).
  
For example, using the standard format:

  `<service-name>.<component>.<verb>`
  
  Using action `key-protect.keys.decode` from the previous example 
  * service-name = key-protect
  * component = keys
  * verb = decode
  
  [TODO: Also support REST like action format, yet to be approved]: <>

#### Step 6: Configure the service to use the PEP SDK in order to check permissions with the PDP. Pick the corresponding SDK language.

  * [PEP SDK for Java](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Java)
  * [PEP SDK for Nodejs](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Node)
  * [PEP SDK for Python](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Python)


<!---
# Identity and Access Management Adopter Guidelines
{: #iam_guidelines}

Onboarding a service to {{site.data.keyword.Bluemix_notm}} is a different set of operations than onboarding a service with Cloud IAM. Technically you can onboard with {{site.data.keyword.Bluemix_notm}} and Cloud IAM independently and in any order. The Cloud IAM team is working with the {{site.data.keyword.Bluemix_notm}} service onboarding team so that the {{site.data.keyword.Bluemix_notm}} service on boarding process will also include Cloud IAM onboarding. Until that work is complete please use the following onboarding steps.

- Users are identified with their IBMid.
  - Users authenticate with their IBMid and password.
  - Authentication returns a UAA/OAuth token which is used to access services within the IBM Cloud.
  
- Services are identified by their ServiceIDs.
  - Services authenticate with their ServiceID and APIkey.
  - Authentication returns an OAuth token which is used to access other services within the IBM Cloud.
  
- Services grant access to their resources by creating *Access Policies*.
  - *Roles* can be viewed and *Access Policies* can be managed through the 
  *Policy Administration Point (PAP)*.
  - Actions are permitted or denied through the *Policy Enforcement Point (PEP)* and *Policy Decision Point (PDP)*. 
  

## Creating a ServiceID
{: #create_serviceid}

To create a ServiceID you must use one of the following steps:

Make a one-time request for your ServiceID/APIkey.

 * Create a ServiceID with [swagger](https://iam.ng.bluemix.net/docs).
```
POST /serviceids
```
 * Create a ServiceID using `curl`.
```
curl -X POST -H "Authorization: $CF_TOKEN" -H 'Content-Type: application/json' -d '{"name": "IAMdemo", "description": "IAM demo of adopting service", "boundTo": "crn:v1:staging:public:docker-registry:us-south:o/57666a74-e136-4eb0-a085-220345fac266:::"}' 'https://iam.ng.bluemix.net/serviceids’
```
**Note**
The `boundTo` is the {{site.data.keyword.Bluemix_notm}} Org that is owned by you or your admin.

## Creating a ServiceID metadata response
{: #create_serviceid_metadata}

The following is a ServiceID metadata response using `curl`. Your service ID is expressed with a UUID and CRN format.

```
{"metadata":{\
"uuid":"ServiceId-3ec0dd02-7a10-40bf-92e7-b9a329547c07",\
"crn":"crn:v1:staging:public:iam:us-south:o/57666a74-e136-4eb0-a085-220345fac266::\
serviceid:ServiceId-3ec0dd02-7a10-40bf-92e7-b9a329547c07",\
"version":"1-4d9b1b10ce893f750a2d7e0d6ee34fd7"},"entity":{"boundTo":"crn:v1:staging:public:docker-registry:\
us-south:o/57666a74-e136-4eb0-a085-220345fac266:::","name":"IAMdemo","descripti\
on":"IAM demo of adopting service"}}
```

## Creating an APIkey for your ServiceID
{: #create_apikey_serviceid}

Create an APIkey
```
POST /apikeys
```

The following is a `curl` example of creating an APIkey
```
curl -X POST -H 'Authorization: $CF_TOKEN' -H 'Content-Type: application/json' -d '{"boundTo": "crn:v1:staging:public:iam:us-south:o/57666a74-e136-4eb0-a085-220345fac266::serviceid:ServiceId-3ec0dd02-7a10-40bf-92e7-b9a329547c07", "name": "IAMdemo", "description": "IAM deom of adopting service"}' https://iam.ng.bluemix.net/apikeys
```

## Authenticating with an APIkey
{: #auth_apikey}

The following is a `curl` example of authenticating with an APIkey
```
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -H \
"Accept: application/json" -d "grant_type=urn%3Aibm%3Aparams%3Aoauth%3Agrant-ty\
pe%3Aapikey&apikey=DuE2s….bfRKc=" "https://iam.s\tage1.ng.bluemix.net/oidc/token”
{"access_token":"eyJraWQiOiIyMDE2MTAyNC0wMDowMDowMCIsImFsZyI6IlJTMjU2In0.eyJpZG\
VudGlmaWVyIjoiU2VydmljZUlkLTNlYzBkZDAyLTdhMTAtNDBiZi05MmU3LWI5YTMyOTU0N2MwNyIsI\
nN1YiI6IlNlcnZpY2VJZC0zZWMwZGQwMi03YTEwLTQwYmYtOTJlNy1iOWEzMjk1NDdjMDciLCJzdWJf\
dHlwZSI6IlNlcnZpY2VJZCIsImFjY291bnQiOnsiYnNzIjoiMDY0Zjg3NTZlMzZlODk5MDAyYjliM2M\
wNzZiZTM3OGIifSwibWZhIjp7fSwiaWF0IjoxNDc5Mzk3MTYwLCJleHAiOjE0Nzk0MDA3NjAsImlzcy\
I6Imh0dHBzOi8vaWFtLnN0YWdlMS5uZy5ibHVlbWl4Lm5ldC9vaWRjL3Rva2VuIiwiZ3JhbnRfdHlwZ\
SI6InVybjppYm06cGFyYW1zOm9hdXRoOmdyYW50LXR5cGU6YXBpa2V5Iiwic2NvcGUiOiJvcGVuaWQi\
LCJjbGllbnRfaWQiOiJkZWZhdWx0In0.APRVqQmfUwn6K4Kg2sicT_kGpqSGQXr4Vua8Q5p4B0_dfGE\
tbbe10JqHeE4ovud6u8xjclAIcqCcbjIH4RijnUNGReVse49gS6JlXxmiNGA8OVlNGjiL68ygIpYsj-\
crx8kVuTrXAFqx9lhLEBhAzDneldu-gjSz7wrQKqISikcMXPXQkmLDuoT-OGNq8rG4fCiENBiweUrGf\
_Yw9W5NSiWyQGdWmczS70Krc_hx1iXskmt8pz5_0_vPXY6_tG5rY6KPw-bHO1wux91Q7aTZwCmaL0zI\
F2d3cIuFe1XywJ_926MfwWy65MxC3xv7-_rsZMFoprrLtBsuEnshNWUDhg",
"token_type":"Bearer","expires_in":3600,"expiration":1479400760}
```

## Registering your ServiceID with IAM
{: #register_serviceid}

To complete the on boarding process, contact the AccessControl Squad at
[#iam-adopters](https://ibm-cloudplatform.slack.com/messages/iam-adopters). 

Your service id will be given the role of Administrator of policies for your 
service's resources.

Call the `PAP` and `GET` the existing policies
```
curl -X GET -H 'Authorization:<APIkeyToken>' \
'https://iampap.ng.bluemix.net/acms/v1/scopes/global/service_ids/\
ServiceId-3ec0dd02-7a10-40bf-92e7-b9a329547c07/policies'

Response:
{"policies":[]}  <-- no policies yet
```

## Creating access policies
{: #creating_policies}

Now that you are fully on boarded, you can begin creating access policies 
for resources owned by your service.
-->

# Lab-Service-IDs und API-Schlüssel

interconnect-service1:
  * ServiceId-2bc4561c-615f-4ba3-ab50-eba3b70a69d3
  * 7DRDYlbFM8Mpt7cOKS7clQisOItOfFcvItkd4MQsd20M

interconnect-service2:
  * ServiceId-089f58e9-f0a0-4b47-b3db-a2d9036080aa
  * rOB0ZqGR1pbiWxNMbn_OfFDmuJcULhqnYW_G0hNnJj0w

interconnect-service3:
  * ServiceId-9a57c3ed-2a8d-45ff-8b34-a7feb80e81bd
  * 6qZoPsd_V47hQQHHVFR1Z8PeGwTZKmNxHgGlURH7OIPf

interconnect-service4;
  * ServiceId-df633c5f-dee3-4e7b-87c3-7a3ed57d6509
  * 3yICAhsR55nlXJLjPA2nLBcAM1SX7LrXpOabjivVeteQ

interconnect-service5:
  * ServiceId-e3703b76-4f91-4323-9b6d-db3122952a72
  * 1ZD8qf_jqHC7JVOzrrvbuI3Dcr153hkGsr4Ll7EvsXKW

interconnect-service6:
  * ServiceId-2a31b14e-6cad-4597-82cf-04f2cb16c26d
  * XFROeDFVyBnJfecSjNhZngPDOniX-5qXl9QWZrsuNjYY

interconnect-service7:
  * ServiceId-56b98026-bb1c-4166-8128-c4841d10373c
  * cBponeC40MEgPy4mW55kb26XbMFAVmF0y2T3T1fYXJuL

interconnect-service8:
  * ServiceId-7a9cf953-044e-474a-9ffb-e66a1b68f437
  * OEGprDQNk7TLxFNrCbKfvLGxQRrbGS-PvhKSCUYJYn1a

interconnect-service9:
  * ServiceId-147203b6-0156-41c6-a28c-7306f047eebb
  * 2OiRisDKDXYA0_0BtlA7OyBk-7II9NUa709HgbF-D_kY

interconnect-service10:
  * ServiceId-87909073-acb8-403c-ab32-91d632e6c5a6
  * 93eWV_Ns2UrjNGENaaau1yOQmGDvTO2FxEivThGIZUOV

interconnect-service11:
  * ServiceId-0e2ec208-926e-4db7-aab4-c0d3bf44865f
  * gEa6bECSMAVF68cS5AbckIKp47_OX3_q63JNWI6-Q5Y0

interconnect-service12:
  * ServiceId-c793ae24-5f43-4c55-815a-830b8c79d1ee
  * WRSnr-FJZ_mI2DbG-8MNqPdAZHq3IkVZU-WbWL7l7uNC

interconnect-service13:
  * ServiceId-b426e816-6975-47df-ac69-01c08560ef3e
  * MkFJJ_zJDg5MiIRUo78dzCC-Mmw3r9DSzZVMvHZ7A63Z

interconnect-service14:
  * ServiceId-d97a9df4-6dbe-43ab-8b10-a70bb3ff9085
  * N63GX1wfo6UDc5kNrEWYHcPT27bD9V0JLmoB-iKsPfEb

interconnect-service15:
  * ServiceId-c6090a5b-569d-40cc-84f5-12480a9ede60
  * xLuJdPmW5npQMuHs4hyJOWZMaYY7i_DwZOSjWlZjnjjK

interconnect-service16:
  * ServiceId-c1d34878-cac3-43a3-bad6-a5b4992d9ed9
  * UZjSMGF8Aw42lzbHtkgDH14FyJxe0s0aN0O4Qk9uBe8T

interconnect-service17:
  * ServiceId-9ccaba36-6b07-4e9b-8b97-fbe1111f4908
  * CJb3qUI3cQWUiMMSt2RuL3ti9yE-F2-i2-1yIfowOM30

interconnect-service18:
  * ServiceId-84a01c41-8330-49e3-842f-b45eaa368d3d
  * 8-qw4_k5Sbjd1sxAiKksHubfPIlkjK2C9S0DnK-WpPDo

interconnect-service19:
  * ServiceId-2ef5d7ea-7ce0-453d-aa70-fbc5f4b781ef
  * Cz4QHZR_qd_WUZsScF-dVcu31J08dPuF_gszMd4oCLJj

interconnect-service20:
  * ServiceId-9e85525e-fe29-45e1-81b5-0681cd0b7f22
  * -OeamgjtKqnGUmdKFAVOWjKhYJMYP8HstCcPrRKfy4V9

interconnect-service21:
  * ServiceId-62c49423-3205-446e-a4aa-e24deb9b158e
  * N2XQ6MpKTvRJX_2IuDQoOiMK5AIhICUFj2wMVyg8O6Pn

interconnect-service22:
  * ServiceId-2de4c08b-f2cc-4e93-bb8b-eebf2222f93e
  * lEOzJvJJV0EgDjQQa8g5kr_D-PawYqIN-QE1QTNpoD5S

interconnect-service23:
  * ServiceId-49e6dc57-70f2-4a69-aac9-311394454475
  * G7epLqdbohZ8tVs8Jcx4qSjlMzlzrw2piNEnPiP4RZ7A

interconnect-service24:
  * ServiceId-7a4ac3ec-bd69-4dbf-8439-f8f5a2ffb88a
  * I7d2KnqbyeQG1rk1AcKeVXgNT1iqCwhSAhan9g-pWucx

interconnect-service25:
  * ServiceId-542a018b-9248-4bb3-bfc1-e0c9d1e70b46
  * WUl0OMnGkLP1BF3bdkqOJeT3niuwD2p1kWd8In05jpho

interconnect-service26:
  * ServiceId-c94f5b5e-0d43-4843-8153-d402fae7e1b5
  * dBtmioisFz_7gTYBPL1IArA_E9F4HYnYYAKVZJfxIcv3

interconnect-service27:
  * ServiceId-37986f6b-325c-42c3-8973-c88c7d365c0c
  * SY1kOsSpSPSLOocmBMwuPWO7u-60aglBliO2Qa4tu4dv

interconnect-service28:
  * ServiceId-08a48402-a02c-4fe6-9260-635188202aad
  * QFaQPoJaYAcVsVlmnVIlkO1haVY_xg8ZZEt-AkmAzAIn

interconnect-service29:
  * ServiceId-e9414ce2-c8d5-44d6-be68-f6c5176f4482
  * FKiafH2hr8eooB0nS6N-3vDrYkIbltzBZb688U8JxpvD

interconnect-service30:
  * ServiceId-e5caa06b-4087-4f55-b51c-bbbad4d78d84
  * 2hcjXXt2G7hmyqAhWlqhXHL9OwFlNdr2_3NZ3tVkBMF2

interconnect-service31:
  * ServiceId-e71b84e8-fe53-4e40-af46-af26f9e59db3
  * 0vwL6DjNl8ATJJ_mvHrEfuzYt9dyeZulA1nKj_q3zUjf

interconnect-service32:
  * ServiceId-fc200643-5788-4af9-a1a5-847d373331b3
  * gM919kowr90lDhuRNbvc-kt3WOKW0YQLRGYNqLVbwC-B

interconnect-service33:
  * ServiceId-df0898a2-8b19-49fc-a88b-f4868c6d2b18
  * KjDoJ5z2WGv2hIG9PRJuylkh0SPLnvAYLY7mVRkmCGGf

interconnect-service34:
  * ServiceId-1eaa9835-fb15-49a6-b19c-74970795a33f
  * wUXkKrKqJmZO8S4io1QoryPlZml9_G6A4L-6WHftl7Ny

interconnect-service35:
  * ServiceId-14f7e5fc-5be8-49b5-9843-4b338cc0c34e
  * Fi7nwbNHJVU7CXAba-MJR2jiCSG524zQVb5CIFWwAM1D

interconnect-service36:
  * ServiceId-fdfe7ec7-1ec7-4798-bb1d-1815b0d31b57
  * wEj7KGnheNnadxzLTOjOe1TlSqgOB75pEzEV5tz6xxl9

interconnect-service37:
  * ServiceId-4488b45e-992f-4479-8cc1-c7160dafb067
  * weXbJ6CkIgcY0K6Aly3yNmjVb6a7cFWhlphaiD27XMdY

interconnect-service38:
  * ServiceId-5830536e-b38e-47a4-9b2b-d3c996a545dd
  * ElMOFJEGKh6qbq1CLoImqK8gvSP0KQLyxmPlY8bZecbw

interconnect-service39:
  * ServiceId-a03d5d46-d064-41c3-b330-35dfc149333b
  * qR0PIg9jT-cPWbj8ShWmha42qXP5Qijoin8l0TfxBH8w

interconnect-service40:
  * ServiceId-8b7e2cdc-b1c6-4707-8554-7c42c7ff1276
  * VZofAdNllinmi7jQMfQlmvbbJcbpAguunzKKeanweF8c

interconnect-service41:
  * ServiceId-cda9707c-8fee-497d-a514-e593b4e01002
  * Eoj46Od3qp381LaEc5nhYj-CIGZmrJKt4Gc9oRfB1naD

interconnect-service42:
  * ServiceId-c743b5f8-5ba6-464e-86ed-83e8dd3ee1b5
  * nespdN1a1I_TQ7pwgBD2gCgtjWpHJrUigUk_69GJTCDC

interconnect-service43:
  * ServiceId-40513e4d-53e6-4dde-8baf-f3a5c82ba234
  * lYCUBuwNSyW9DNOXcBXfof4znnrZihALfdbTRvytni48

interconnect-service44:
  * ServiceId-afee12ac-c58a-433c-be98-416acbb670e2
  * 2SBqJdVgwwuBBV8k3eDg6_4NVeDBaLynQgImqct4DfFv

interconnect-service45:
  * ServiceId-65a3733a-eb0a-402b-ae91-5a412dc9725f
  * to5dKzNvpNLearwdg0KeJc-zftazx-xlu0yt1uk1Q0VP

interconnect-service46:
  * ServiceId-10413fbe-10aa-4bb5-b641-65a9bbeb9d53
  * kKyrLaYCqbhNxH-Axcv7ABcX0aGdPw-MR2nYjkVORVhY

interconnect-service47:
  * ServiceId-82ead5c9-195a-4780-bbec-b3655a475896
  * -uTIzbpCJSIn45vYZP86YtrKzpgwyQZThibltlL2rRgu

interconnect-service48:
  * ServiceId-c06741b5-0ec8-4131-8b2b-276a4f72c0a1
  * 6FpfmxrQpdD00X4_m8Jhk-r4Bwg4x47BZRnLfA-qVe67

interconnect-service49:
  * ServiceId-ee93887b-11d1-49b9-be63-2764a42beb57
  * 46ZqlkPk_n3QjTbweHa3X4HLQc4N-_O0ODYSfDHu_vui

interconnect-service50:
  * ServiceId-71dd52eb-7bbc-4ff0-aaf3-70816830660e
  * vDhkWd9DzUf7V_5cWaMhmz8IPmyshCJlZcu_tf39EyNm


