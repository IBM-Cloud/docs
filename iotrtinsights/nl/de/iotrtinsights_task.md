---

copyright:
  years: 2015,2016

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Geräte verbinden und anzeigen
{: #iotrtinsights_task}
*Letzte Aktualisierung: 11. Februar 2016*

{{site.data.keyword.iotrtinsights_short}} verwendet {{site.data.keyword.iot_short}} für den Zugriff auf Geräte und den Datenabruf. Geräte, die Sie mit {{site.data.keyword.iot_short}} verbinden, sind automatisch mit {{site.data.keyword.iotrtinsights_short}} verbunden.
{: shortdesc}

Wenn Sie einen neuen Gerätetyp verbinden, müssen Sie auch das Nachrichtenschema konfigurieren, um die Gerätedatenpunkte zuzuordnen, die Einheiten festzulegen und den Gerätetyp zu benennen. Wenn Ihre Geräte einem bereits konfigurierten Gerätetyp entsprechen, werden ihre Daten automatisch im Dashboard angezeigt. 

## Neues Gerät hinzufügen
{: #iotrtinsights_subtask}

Gehen Sie wie folgt vor, um ein neues Gerät hinzuzufügen:   
Zum Hinzufügen eines neuen Geräts wird ein aus zwei Schritten bestehender Prozess ausgeführt. Zunächst fügen Sie das Gerät zu {{site.data.keyword.iot_short}} hinzu und anschließend konfigurieren Sie, wie {{site.data.keyword.iotrtinsights_short}} die Gerätedaten verarbeitet und anzeigt. 
1. Fügen Sie Geräte zu Ihrer {{site.data.keyword.iot_short}}-Instanz hinzu. 
> **Tipp:** Wenn Sie die IoT-Telefonanwendung bereitgestellt haben, wurde bereits ein IoT-Telefongerät zu dem {{site.data.keyword.iot_short}}-Service *iot-phone-iotf-service* hinzugefügt und Sie können diesen Schritt überspringen.   

  Weitere Informationen zum Hinzufügen neuer Geräte zu Ihrem {{site.data.keyword.iot_short}}-Service finden Sie in der [Dokumentation zu {{site.data.keyword.iot_full}}](https://www.ng.bluemix.net/docs/services/IoT/index.html) und im Thema mit den [Rezepten zur Verbindung von {{site.data.keyword.iot_short}}-Geräten](https://developer.ibm.com/recipes/?post_type=tutorials&s=IoTF). 
2. Konfigurieren Sie Ihr Gerät in {{site.data.keyword.iotrtinsights_short}}.   
  1. Melden Sie sich bei der {{site.data.keyword.iotrtinsights_short}}-Konsole als Benutzer mit Administratorberechtigung an. 
  9. Gehen Sie zu **Geräte > Geräte durchsuchen** und überprüfen Sie, ob Ihr neu hinzugefügtes Gerät aufgelistet wird. 
  > **Tipp:** Die Geräteliste wird einmal pro Minute mit den Daten aus Ihrer Datenquelle aktualisiert. Klicken Sie auf **Aktualisieren**, um die Geräteliste sofort zu aktualisieren.
  3. Gehen Sie zu **Geräte > Schemas verwalten** und klicken Sie auf **Neues Nachrichtenschema hinzufügen**.   
  4. Geben Sie einen Namen für das Nachrichtenschema ein. Beispiel:
  `Neues Nachrichtenschema`.
  5. Klicken Sie auf **Link zu neuer Datenquelle erstellen** und wählen Sie die Datenquelle und den Gerätetyp aus, die/der Ihrer {{site.data.keyword.iot_short}}-Instanz und Ihrem Gerät entspricht. Optional können Sie einen Ereignisnamen eingeben, um ausschließlich Daten für dieses Ereignis zu erfassen; oder Sie behalten den Platzhalter `+` bei, um alle Ereignisse zu erfassen. Für weitere Informationen zum Ermitteln des Ereignistyps für Ihr Gerät klicken Sie [hier](#identify-datapoints "Datenpunkte identifizieren").  
  >**Wichtig:** Jedes Nachrichtenschema muss aus einer eindeutigen Kombination von Datenquelle, Gerätetyp und Ereignisname bestehen. Wenn Sie mehrere Schemas für eine bestimmte Kombination aus Datenquelle und Gerätetyp erstellen wollen, geben Sie einen eindeutigen Namen für jedes Nachrichtenschema an, anstatt den Standardplatzhalter `+` zu verwenden.    
  6. Fügen Sie einen oder mehrere Datenpunkte hinzu, die Sie in die Gerätedashboards einbeziehen wollen. Sie können Datenpunkte von einem  verbundenem Gerät auswählen oder manuell Datenpunkte hinzufügen. Die verfügbaren Datenpunkte sind in den Nutzdaten der Nachrichten definiert, die von einem Gerät gesendet werden. Informationen zum {{site.data.keyword.iot_short}}-Nutzdatenformat finden Sie im Abschnitt zu [Nachrichtennutzdaten](https://docs.internetofthings.ibmcloud.com/messaging/payload.html "Nachrichtennutzdaten") in der {{site.data.keyword.iot_short}}-Dokumentation.    
    > **Tipp:** Sie können manuell virtuelle Datenpunkte erstellen, die vorhandene Datenpunkte des Typs "Ganze Zahl" oder "Gleitkommawert" ändern oder kombinieren. Wenn zum Beispiel der Gerätedatenpunkt "temp" einen Temperaturwert in Fahrenheit zurückgibt und Sie Celsius verwenden wollen, können Sie einen virtuellen Datenpunkt *temp_c* mit der Funktion *temp_c=(temp-32)/1,8* erstellen. Sie können dann den virtuellen Datenpunkt *temp_c* anstatt des Echtzeitdatenpunkts *temp* in Ihren Regelbedingungen verwenden. In den Dashboards sind die virtuellen Datenpunkte mit einer gestrichelten Linie unterstrichen.     

  <dl>
  <dt>Aus verbundenem Gerät auswählen</dt>
  <dd>
  <ol>
    <li>Klicken Sie auf **Aus verbundenem Gerät auswählen**. </li>  
    <li>Wählen Sie im Dialog "Datenpunkte hinzufügen" einen oder mehrere Datenpunkte zum Hinzufügen aus und klicken Sie anschließend auf **OK**. </li>   
    <li>Die ausgewählten Datenpunkte werden mit dem Beschreibungssatz zu dem Namen des Datenpunkts hinzugefügt. Klicken Sie auf den Datenpunkt in der Liste, um diesen zu bearbeiten, und fügen Sie zusätzliche Attribute wie Sensortyp, Datentyp und Anzahl der Dezimalstellen hinzu. </li>
  </ol>
  </dd>
  <dt>Manuell hinzufügen</dt>
  <p><b>Tipp:</b> Zum Erstellen einer [verschachtelten Datenpunktstruktur](schemas.html) fügen Sie zuerst einen Datenpunkt hinzu, der dem Datentyp "Übergeordnet" entspricht. Dann können Sie in der Datenpunkttabelle auf ![Symbol 'Untergeordnetes Element hinzufügen'](images/add_child.png "Untergeordnetes Element hinzufügen") klicken, um einen oder mehrere untergeordnete Datenpunkte hinzuzufügen. </p>
  <dd>
  <ol>
    <li>Klicken Sie auf **Manuell hinzufügen**. </li>
    <li>Wählen Sie **Echtzeitdatenpunkt** oder **Virtueller Datenpunkt** aus.</br></li>
    <li>Definieren Sie die folgenden Datenpunktinformationen:
    <ul>  
     <li> Datenpunkt - Die Datenpunkt-ID, die Sie im [{{site.data.keyword.iot_short}}-Dashboard lokalisiert haben](#identify-datapoints "Datenpunkte identifizieren"). Beispiel:   
   `id`, `ts`, `lat`  </li>
     <li>Beschreibung - Eine Kurzbeschreibung des Datenpunkts. Diese Beschreibung wird verwendet, wenn die Datenpunkte in Dashboards angezeigt werden. </li>
     <li>Funktion für virtuellen Datenpunkt - Fügen Sie eine oder mehrere Komponenten hinzu, um eine gültige Funktion zu definieren. Sie können Datenpunkte, numerische Werte und mathematische Operatoren wie +, -, \*, /, ( und ) verwenden, um Ihre Funktion zu erstellen. </li>
     <li>Datentyp - Der Datentyp des Datenpunkts:   
   `Zeichenfolge`, `Ganze Zahl`, `Gleitkommawert` oder `Übergeordnet`. </li>
     <li>Sensortyp - Optional können Sie auswählen, wie der Datenpunkt in den Dashboards interpretiert werden soll. Abhängig von der Kombination aus Typ und Sensortyp stehen möglicherweise zusätzliche Visualisierungsoptionen für Ihre Dashboard-Widgets zur Verfügung. Weitere Informationen zu Sensortypen und Visualisierungsoptionen finden Sie im Thema zu [Dashboard-Widgets](dashboards.html#dashboard-widget "Dashboard-Widgets"). </li>
     <li>Datenpunktsymbol - Sie können optional ein Symbol auswählen, um den Datenpunkt in den Dashboard-Widgets darzustellen. </li>
     <li>Mindestwert/Maximalwert - Optional, nur ganze Zahl und Gleitkommawert: Wenn ein Maximalwert und ein Mindestwert eingegeben werden, können Gerätedaten als Messanzeige in den Dashboards dargestellt werden. </li>
     <li>Dateneinheit - Optional: Die Einheit für die Daten des Datenpunkts. Beispiel:   
     `C`, `Mph`  </li>
     <li> Dezimalstellen - Optional, nur Gleitkommawert: Die Anzahl an Dezimalstellen, die bei den Gerätedaten angegeben werden soll. </li>
    </ul>
    </li>
  </ol>
  </dd>
  </dl>
   8. Klicken Sie auf **OK**, um das Nachrichtenschema zu erstellen. 
   9. Gehen Sie zu **Geräte > Geräte durchsuchen** und klicken Sie auf das neu hinzugefügte Gerät, um zu überprüfen, ob die Echtzeitgerätedaten angezeigt werden und die Datenpunkte korrekt zugeordnet sind. 

## Datenpunkte und Ereignisse im {{site.data.keyword.iot_short}}-Dashboard identifizieren
{: #identify-datapoints}
   Die Datenpunkte und Ereignistypen für ein Gerät können im {{site.data.keyword.iot_short}}-Dashboard ermittelt werden. 
   >**Tipp:** Wenn Sie die IoT-Telefonanwendung als IoT-Gerät verwenden, können Sie das Ereignis "sensorData" und die folgenden Datenpunkte für die Konfiguration des Nachrichtenschemas verwenden:
   >- d.id - Geräte-ID
   >- d.ts - Zeitmarke
   >- d.lat - Breitengrad
   >- d.lng - Längengrad
   >- d.ax - X-Beschleunigung
   >- d.ay - Y-Beschleunigung
   >- d.az - Z-Beschleunigung
   >- d.oa - Alpha-Bewegung
   >- d.ob - Beta-Bewegung
   >- d.og - Gamma-Bewegung
   >Dabei wird mit d.*datenpunkt* angegeben, dass der Datenpunkt in einem übergeordneten Datenpunkt d verschachtelt ist. 

   1. Klicken Sie im Bluemix-Dashboard auf die Internet of Things-Kachel.   
   >**Hinweis:** Wenn Sie die IoT-Telefonanwendung verwenden, klicken Sie auf die Kachel *iot-phone-iotf-service*.   
   2. Klicken Sie auf **Dashboard starten**, um das {{site.data.keyword.iot_short}}-Dashboard zu öffnen. 
   3. Rufen Sie die Seite **Geräte** auf. 
   4. Klicken Sie auf Ihr Gerät, um die Gerätedetailseite zu öffnen. Blättern Sie abwärts zum Abschnitt mit den **Sensorinformationen**, um eine Liste der verfügbaren Ereignisse und Datenpunkte für das Gerät anzuzeigen. Diese Informationen sind erforderlich, wenn Sie das Gerät in {{site.data.keyword.iotrtinsights_short}} konfigurieren. 
