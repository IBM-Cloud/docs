---

Titel: Benutzerbasierte Push-Benachrichtigungen aktivieren

Schlüsselwörter: Benutzerbasierte Push-Benachrichtigungen, userId, Benutzer-ID
copyright:
 years: 2015, 2016

---

# Benutzerbasierte Benachrichtigungen aktivieren
{: #user_based_notifications}
Letzte Aktualisierung: 16. August 2016
{: .last-updated}

Auf Benutzer-ID basierte Push-Benachrichtigungen zielen mit angepassten Nachrichten auf Benutzer mobiler Apps ab. Benutzerbasierte Benachrichtigungen können dabei helfen, bestimmte Einzelpersonen durch Ausschöpfen ihrer persönlichen Vorgaben und Auswahloptionen zu beteiligen.   

## Gerät mit Benutzer-ID registrieren
Um Push-Benachrichtigungen zu aktivieren, die auf einer Benutzer-ID basieren, müssen Sie sicherstellen, dass Sie das Gerät mit einer Benutzer-ID registrieren und außerdem den geheimen Clientschlüssel ('clientSecret') übergeben, der bei der Bereitstellung der {{site.data.keyword.mobilepushshort}}-Services zugeordnet wird. Ohne einen gültigen geheimen Clientschlüssel ('clientSecret') schlägt die Geräteregistrierung fehl.   

Die Benutzer-ID kann eine beliebige Zeichenfolge sein, die die Anwendung gegenüber der API für die Geräteregistrierung bereitstellt. Normalerweise führt eine mobile Anwendung zuerst einen Authentifizierungszyklus aus, in dessen Verlauf der Benutzer mobiler Anwendungen bei einem Authentifizierungsservice wie [{{site.data.keyword.amafull}}](https://console.ng.bluemix.net/docs/services/mobileaccess/index.html) authentifiziert wird. Nach der erfolgreichen Authentifizierung wird die ID des authentifizierten Benutzers dann zusammen mit einem geheimen Clientschlüssel ('clientSecret') an die API für Push-Geräteregistrierungen übergeben. Das Vorhandensein eines geheimen Clientschlüssels setzt die Zuordnung nur von autorisierten Benutzer-IDs bei der Registrierung mobiler Geräte um. 

Behandeln Sie den geheimen Clientschlüssel 'clientSecret' stets vertraulich und codieren Sie ihn zu keinem Zeitpunkt fest in die mobile App. Es gibt verschiedene Muster für die Anwendungsinitialisierung, mit denen 'clientSecret' zur Anwendungslaufzeit dynamisch extrahiert werden kann. Das Ablaufdiagramm stellt dieses Muster dar. 

![Push-Aktivierung](images/init_client_secret.jpg) 

Sie können ein Gerät auch für die Zuordnung zu einem anonymen Benutzer ('anonymous') registrieren. Hierbei müssen Sie eine Variante der API für die Geräteregistrierung verwenden, bei der die Angabe der Argumente mit der Benutzer-ID und dem geheimen Clientschlüssel 'clientSecret' nicht erforderlich ist.    

## Benutzeranmeldung/-abmeldung synchronisieren und Push-Benachrichtigungen aktivieren 

Sie können festlegen, dass Benachrichtigungen nur gesendet werden, wenn der Benutzer angemeldet ist.  

Dies kann zum Beispiel zutreffen, wenn ein Gerät von einer Familie oder einem Team bei der Arbeit gemeinsam genutzt wird und bestimmte Benutzer in der Familie oder im Team angesprochen werden sollen. In einem derartigen Anwendungsfall würde die Anwendung mithilfe einer entsprechenden Benutzeranmelde- und -abmeldesequenz so überwacht, dass die Identität des aktuellen Anwendungsbenutzers verfolgt wird. Um sicherzustellen, dass Benachrichtigungen, die einen bestimmten Benutzer zum Ziel haben, auch stets nur von diesem Benutzer empfangen werden, müssen Sie nach der erfolgreichen Anmeldung die API für die Geräteregistrierung aufrufen, mit der die Benutzer-ID des angemeldeten Benutzers übergeben wird. Ebenso müssen Sie vor dem Abmelden die API für die Rücknahme der Registrierung aufrufen. Durch die Ablaufplanung dieser Push-APIs in Verbindung mit der An- und der Abmeldung wird sichergestellt, dass Push-Benachrichtigungen, die für einen bestimmten Benutzer bestimmt sind, auch nur an diesen Benutzer gesendet werden. 
