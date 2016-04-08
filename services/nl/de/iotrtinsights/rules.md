---

copyright:
  years: 2015,2016

---

{:shortdesc: .shortdesc}

# Regeln erstellen und auf Alerts antworten{: #rules}

Verwenden Sie Analyseregeln, um Alerts und Benachrichtigungen für Ihre Geräte einzurichten. Sie können zum Beispiel eine Regel erstellen, die einen Alert zum Gerätedashboard hinzufügt und eine E-Mail an einen Administrator sendet, wenn der Temperatursensor des Geräts eine ungewöhnlich hohe Temperatur registriert.
{: shortdesc}

Sie können Regeln mit Bedingungen verwenden, die Datenpunkte oder Kontextparameter vergleichen, wie zum Beispiel Assetzuordnungen zu statischen Werten, anderen Datenpunkten oder Kontextparametern. 

>**Hinweis:** Wenn Sie Instanzen eines kostenlosen Plans von {{site.data.keyword.iotrtinsights_short}} verwenden, werden alle Regeln nach einer Stunde automatisch inaktiviert. Sie können die Regeln manuell wieder reaktivieren. Für eine kontinuierliche Verfügbarkeit der Regeln können Sie ein Upgrade auf einen kostenpflichtigen Plan durchführen.
Gehen Sie wie folgt vor, um eine Regel für ein Gerät zu erstellen: 
1. Gehen Sie in der {{site.data.keyword.iotrtinsights_short}}-Konsole zu **Analytics > Regeln**.
2. Klicken Sie auf **Neue Regel hinzufügen**, benennen Sie die Regel, geben Sie eine Beschreibung an und wählen Sie ein Nachrichtenschema für die Regel aus. Klicken Sie anschließend auf **Weiter**.  
3. Klicken Sie auf **OK**, um die neue Regel zu erstellen. 
3. **Optional:** Wählen Sie eine Alertpriorität für die Regel aus.
Mithilfe der Priorität werden die Alerts klassifiziert, die in der Alertsanzeige aufgelistet werden. Die Standardpriorität ist "Niedrig". 
3. Zum Einrichten der Regellogik fügen Sie eine oder mehrere IF-Bedingungen hinzu, die als Auslöser für die Regel verwendet werden.
Sie können Bedingungen in parallelen Zeilen hinzufügen, um diese als OR-Bedingungen anzuwenden. Sie können Bedingungen aber auch in sequenziellen Spalten hinzufügen, um sie als AND-Bedingungen anzuwenden.
**Tipp:** Damit Sie eine Vorstellung der typischen Werte bekommen, die von Ihren Geräten zurückgegeben werden, gehen Sie zu **Geräte > Geräte durchsuchen** und klicken Sie auf Ihr Gerät, damit die Echtzeitdaten angezeigt werden.
**Wichtig:** Zum Auslösen einer Bedingung, die zwei Datenpunkte vergleicht, oder zum Auslösen von mindestens zwei Datenpunktbedingungen, die sequenziell miteinander kombiniert sind, müssen die auslösenden Daten in derselben Nachricht enthalten sein. Wenn die Daten in mehreren Nachrichten empfangen werden, werden die Bedingung oder die sequenziellen Bedingungen nicht ausgelöst.   
> **Beispiele:**   
Eine einfache Regel könnte einen Alert auslösen, wenn ein Parameterwert größer als ein angegebener Wert ist.   
Beispiel: Bedingung = `ax>5`  
Eine komplexere Regel könnte einen Alert auslösen, wenn ein Parameterwert für ein Gerät, das einem bestimmten Asset zugeordnet ist, einen bestimmten Wert überschreitet.   
Beispiel: Bedingung = `ax>5 AND asset.assetnum==5001`   
Detaillierte Schritte sind im Thema [Beispiel: Komplexe Regel mithilfe von Nachrichtenschema und Kontextparameterbedingungen erstellen](#complex "Beispiel: Komplexe Regel mithilfe von Nachrichtenschema und Kontextparameterbedingungen erstellen") beschrieben.   
4. Konfigurieren Sie die Voraussetzungen für bedingte Auslöser für Ihre Regel.
Um zu steuern, wie viele Alerts für eine Regel innerhalb eines bestimmten Zeitraums ausgelöst werden, können Sie Voraussetzungen für bedingte Auslöser für Ihre Regel konfigurieren.
**Wichtig:** Die bedingten Auslöser werden auf alle Bedingungen in der Regel angewendet. Beispiel: Wenn für eine Regel fünf unterschiedliche parallele (OR) Bedingungen festgelegt sind, wird jede Bedingung, die zutrifft, auf den Zähler für bedingte Auslöser angerechnet.
Gehen Sie wie folgt vor, um bedingte Auslöser für eine Regel einzurichten: 
 1. Klicken Sie im Regeleditor auf den Link **Jedes Mal auslösen, wenn Bedingungen erfüllt sind**, um den Bedingungsdialog zu öffnen. 
 2. Wählen Sie den bedingten Auslöser, der mit der Regel verwendet werden soll, aus und konfigurieren Sie ihn. 
 <ul>
 <li>Jedes Mal auslösen, wenn Bedingungen erfüllt sind</li>
 <li>Auslösen, wenn Bedingungen N Mal in M *Zeiteinheit* erfüllt sind</li>
 </ul>  
Eine detailliertere Beschreibung bedingter Auslöser finden Sie im Abschnitt [Bedingte Auslöser](#conditional "Bedingte Auslöser - Übersicht").
5. Erstellen Sie eine oder mehrere Aktionen oder wählen Sie diese aus, die auftreten, wenn die Regelbedingungen erfüllt sind.
Weitere Informationen zu Aktionen finden Sie im Abschnitt [Aktionen erstellen](actions.html#shared "Aktionen erstellen").    
 > Beispiel: Eine Aktion kann darin bestehen, eine E-Mail zu senden. Weitere Informationen zu den unterschiedlichen Aktionstypen finden Sie im Abschnitt [Aktionstypen](actions.html "Aktionstypen").
6. Wenn die Regel Ihren Anforderungen entspricht, klicken Sie auf **Speichern**. 
7. Klicken Sie auf der Seite "Regeln" auf ![Symbol 'Konfigurieren'](images/gear.png "Symbol 'Konfigurieren'") und wählen Sie **Aktivieren** aus, um die Regel zu aktivieren. 

Ihre Regel ist aktiv. Wenn die Bedingungen der Regel erfüllt sind, wird ein Alert zum Dashboard **Dashboards > Überblick** hinzugefügt und alle Regelaktionen werden ausgeführt. 

## Bedingte Auslöser{: #conditional}

Um zu steuern, wie viele Alerts für eine Regel innerhalb eines bestimmten Zeitraums ausgelöst werden, können Sie Voraussetzungen für bedingte Auslöser für Ihre Regel konfigurieren.


Abhängig von der Nachrichtenfrequenz und den Regelbedingungen wird eine Regel möglicherweise sehr häufig ausgelöst, wenn eine Auslöserbedingung erfüllt ist. Beispiel: Wenn die Bedingung `temp >= 90` lautet und die Temperatur steigt und sich bei 91 Grad stabilisiert, wird die Regel mit jeder ankommenden Nachricht ausgelöst. Abhängig von der Frequenz der Gerätenachrichten und den Aktionen, die von der Regel ausgeführt werden sollen, kann dies zum Beispiel schnell Ihren Maileingang füllen oder einen Twitter-Feed mit Nachrichten überfüllen, die keinen zusätzlichen Wert außer dem der ersten Nachricht enthalten. 

**Wichtig:** Die bedingten Auslöser werden auf alle Bedingungen in der Regel angewendet. Beispiel: Wenn für eine Regel fünf unterschiedliche parallele (OR) Bedingungen festgelegt sind, wird jede Bedingung, die zutrifft, auf den Zähler für bedingte Auslöser angerechnet.


Bedingung | Beschreibung
------------- | -------------
Jedes Mal auslösen, wenn Bedingungen erfüllt sind | Die Regel wird jedes Mal ausgelöst, wenn die Regelbedingungen erfüllt sind.
Auslösen, wenn Bedingungen N Mal in M *Tagen/Stunden/Minuten/Benutzerdefiniert* erfüllt sind | Die Regel wird ausgelöst, wenn die Bedingungen M Mal im ausgewählten Zeitintervall erfüllt wurden, und sie wird erst dann wieder ausgelöst, wenn die konfigurierte Zeitspanne vorbei ist. </br>Beispiel: Voraussetzung für bedingten Auslöser =`Nur einmal auslösen, wenn Bedingungen 4 Mal in 30 Minuten erfüllt werden`. Das Gerät sendet alle fünf Minuten eine neue Nachricht. Mittags überschreitet die Temperatur erstmals 90 Grad, womit die Bedingung erfüllt ist. Der Zähler für bedingte Auslöser wird gestartet, die Regel wird aber noch nicht ausgelöst. Nach 15 Minuten und drei weiteren Nachrichten, die angeben, dass `temp > 90` empfangen wurde, wird die Regel ausgelöst. Danach wird die Regel unabhängig von der Temperatur 15 Minuten lang nicht ausgelöst.
## Beispiel: Komplexe Regel mithilfe von Nachrichtenschema und Kontextparameterbedingungen erstellen{: #complex}
Führen Sie die folgenden Schritte aus, um eine komplexere Regel zu erstellen, die einen Alert im Alerts-Dashboard erstellt, wenn der Parameter "ax" den Wert "5" für ein beliebiges IoT-Telefongerät überschreitet, das Assetnummer 5001 zugeordnet ist: 
1. Gehen Sie zu **Geräte > Assetzuordnungen verwalten** und ordnen Sie mindestens ein IoT-Telefongerät einem Asset mit der Assetnummer 5001 zu.
Detaillierte Schritte sind im Abschnitt [Assets verwalten](assets.html "Assets verwalten") beschrieben. 
2. Gehen Sie zu **Analytics** und klicken Sie auf **Neue Regel hinzufügen**. 
3. Geben Sie einen beschreibenden Namen und eine Beschreibung für die Regel an. Geben Sie außerdem den Gerätetyp an, auf den die Regel angewendet wird, indem Sie das für Ihren IoT-Telefongerätetyp erstellte Nachrichtenschema auswählen. 
4. Klicken Sie auf **OK**, um die neue Regel zu erstellen. 
<!-- 5. Click ![Add icon.](images/rules_plus.png "Add icon") to add an initial condition. -->
6. Klicken Sie auf die Kachel für die neue Bedingung und bearbeiten Sie die erste Bedingung. 
 1. Wählen Sie **Datenpunkt** als Operand aus, der verglichen werden soll. 
 2. Wählen Sie den Datenpunkt **ax** aus. 
 3. Wählen Sie den Operator **>** aus, sodass die Bedingung zutrifft, wenn der Wert des ersten Operanden größer ist als der Wert des zweiten Operanden. 
 3. Wählen Sie **Statischer Wert** als den Operanden aus, mit dem der Vergleich ausgeführt werden soll. 
 4. Geben Sie den Wert `5` ein, mit dem der Datenpunkt "ax" verglichen werden soll. 
 5.  Klicken Sie auf **OK**, um die Bedingung hinzuzufügen. 
5. Zum Hinzufügen der AND-Bedingung klicken Sie auf ![Symbol 'Hinzufügen'](images/rules_plus.png "Symbol 'Hinzufügen'") rechts neben der ersten Bedingung. 
6. Klicken Sie auf die Kachel für die neue Bedingung und bearbeiten Sie die Bedingung. 
  1. Wählen Sie **Kontext** als Operand aus, der verglichen werden soll. 
  2. Klicken Sie im Kontextparametermenü auf das Dreieck vor dem Kontextschema **Assets**, um die Liste der Assetkontextparameter zu erweitern. 
  3. Wählen Sie den Kontextschemaparameter **ASSETNUM** aus. 
  3. Wählen Sie den Operator **==** aus, sodass die Bedingung zutrifft, wenn die Werte des ersten und des zweiten Operanden gleich sind. 
  3. Wählen Sie **Statischer Wert** als den Operanden aus, mit dem der Vergleich ausgeführt werden soll. 
  4. Geben Sie `5001` als den Wert ein, mit dem der Kontextschemaparameter **ASSETNUM** verglichen werden soll. 
  5.  Klicken Sie auf **OK**, um die Bedingung zu erstellen. 
7. Verwenden Sie den standardmäßigen bedingten Auslöser `Jedes Mal auslösen, wenn Bedingungen erfüllt sind`. 
7. Erstellen Sie eine oder mehrere Aktionen oder wählen Sie diese aus. 
7. Speichern Sie die neue Regel. 
7. Klicken Sie auf der Seite "Regeln" der Kachel für die neue Regel auf ![Symbol 'Konfigurieren'](images/gear.png "Symbol 'Konfigurieren'") und wählen Sie **Aktivieren** aus, um die Regel zu aktivieren. 

## Beispiel: Assetbasierte Regeln erstellen{: #asset_rules}

Nachdem Sie Ihre Geräte erfolgreich Assets zugeordnet haben, können Sie Regeln erstellen, die die Assetdetails verwenden. Das Zuordnen von Geräten zu Assets und das Erstellen von Regeln, die Datenpunkte und Assetinformationen umfassen, sind leistungsfähige Funktionen. 

In den nachfolgenden Beispielen werden Assets verwendet, um die Mobiltelefone des Unternehmens zu verfolgen. Zwei Assets wurden erstellt und Mobiltelefonen zugeordnet. Asset 5001 ist Telefonen mit EINKAUFSPREIS (PURCHASEPRICE) < 100 und Asset 5002 Telefonen mit EINKAUFSPREIS (PURCHASEPRICE) >=100 zugeordnet. Die Gerätedatenauslöserbedingung für jedes Beispiel ist `d.ax>5`, was in diesem vereinfachten Beispiel einer plötzlichen Beschleunigung des Telefons entspricht, wenn es zum Beispiel hinfällt. 

Sie können nun zwei einfache Regeln einrichten, die angeben, wenn ein Telefon, das Asset 5001 zugeordnet ist, fallen gelassen wurde. Genauso einfach können Sie eine Regel einrichten, die verfolgt, wenn ein Telefon, das nicht Asset 5001 zugeordnet ist, hinfällt. Dabei kann es sich um alle Telefone von Asset 5002 handeln oder um Telefone, die keinem Asset zugeordnet sind. 

Beispiel | Regel
------------- | -------------
Regel nur auslösen, wenn das Gerät Asset 5001 zugeordnet ist | IF `d.ax>5` AND `asset.assetnum==5001` THEN ...
Regel nur auslösen, wenn das Gerät NICHT Asset 5001 zugeordnet ist | IF `d.ax>5` AND `asset.assetnum!=5001` THEN ...

Sie können auch Regeln einrichten, die für Telefone mit einem bestimmten EINKAUFSPREIS (PURCHASEPRICE) ausgelöst werden.   

Beispiel | Regel
------------- | -------------
Regel nur auslösen, wenn das Telefon weniger als 100 kostet | IF `d.ax>5` AND `asset.purchaseprice<100` THEN ...
Regel nur auslösen wenn das Telefon mehr als 100 kostet | IF `d.ax>5` AND `asset.purchaseprice>=100` THEN ...

Sie können diese Regeln für ein komplexeres Verhalten auch kombinieren. 

Beispiel | Regel
------------- | -------------
Regel nur auslösen, wenn das Telefon Asset 5001 zugeordnet ist (weniger als 100 kostet), aber mehr als 75 kostet | IF `d.ax>5` AND `asset.assetnum==5001` AND `asset.purchaseprice>75` THEN ...
Regel nur auslösen, wenn das Telefon Asset 5002 zugeordnet ist (mehr als 100 kostet), aber weniger als 200 kostet | IF `d.ax>5` AND `asset.assetnum==5002` AND `asset.purchaseprice<200` THEN ...
