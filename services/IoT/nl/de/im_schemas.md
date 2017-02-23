---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-03"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Schemas für Gerätetypen erstellen
{: #iotrtinsights_task}

Zum Verwenden von {{site.data.keyword.iot_short}}-Funktionen wie beispielsweise Regeln und Aktionen müssen Sie ein Schema erstellen, um Geräteeigenschaften benutzerfreundlichen Eigenschaftsnamen zuzuordnen, Dateneinheiten für die Eigenschaften festlegen und einen Nachrichtentyp angeben, der mit dem Schema verwendet werden soll.
{: shortdesc}

**Wichtig:** Zur Verwendung von Regeln und Aktionen sind Schemas erforderlich. Informationen finden Sie in [Cloud Analytics](cloud_analytics.html#rules).

**Wichtig:** Die Analysefunktionen stammen aus dem {{site.data.keyword.iotrtinsights_full}}-Service und werden zusammengeführt. Wenn Ihre {{site.data.keyword.iot_short_notm}}-Organisation als Datenquelle für eine vorhandene {{site.data.keyword.iotrtinsights_short}}-Instanz verwendet wird, sind Cloud Analytics und Edge Analytics erst aktiviert, wenn die vorhandenen {{site.data.keyword.iotrtinsights_short}}-Instanzen migriert wurden. Verwenden Sie weiterhin das {{site.data.keyword.iotrtinsights_short}}-Dashboard für Ihre Analysevorhaben, bis die Migration abgeschlossen ist. Weitere Informationen finden Sie im [Blog zu IBM Watson IoT Platform ![Symbol für externen Link](../../icons/launch-glyph.svg)](https://developer.ibm.com/iotplatform/2016/04/28/iot-real-time-insights-and-watson-iot-platform-a-match-made-in-heaven/){: new_window} in IBM developerWorks und in den Dashboards Ihrer bestehenden {{site.data.keyword.iotrtinsights_short}}-Instanz.  

## Geräteschema hinzufügen
{: #add_schema}

Gehen Sie wie folgt vor, um ein Schema hinzuzufügen:  
1. Wechseln Sie zu **Geräte > Schemas verwalten** und klicken Sie auf **Schema hinzufügen**.  
2. Wählen Sie einen Geräte-Typ aus, der diesem Nachrichtenschema zugeordnet werden soll. **Wichtig:** Für einen Gerätetyp kann nur ein einziges Schema festgelegt werden.

3. Fügen Sie mindestens eine Eigenschaft hinzu:  
    Sie können Eigenschaften aus einem verbundenen Gerät auswählen, virtuelle Eigenschaften erstellen, die vorhandene Eigenschaften ändern oder kombinieren, oder Sie können Eigenschaften manuell hinzufügen.  

    **Tipp:** Die verfügbaren Eigenschaften sind in den Nutzdaten der Nachrichten definiert, die von einem Gerät gesendet werden. Informationen zum {{site.data.keyword.iot_short}}-Nutzdatenformat finden Sie im Abschnitt [Nachrichtennutzdaten](reference/mqtt/index.html#message-payloadl "Nachrichtennutzdaten.").   
  <dl>
  <dt>Eigenschaft manuell hinzufügen</dt>
  <p><b>Tipp:</b> Zum Erstellen einer verschachtelten Eigenschaftsstruktur fügen Sie zuerst eine Eigenschaft hinzu, die den Datentyp 'parent' (übergeordnet) aufweist. Sie können in der Eigenschaftentabelle anschließend auf das ![Symbol zum Hinzufügen eines untergeordneten Elements](images/add_child.png "Untergeordnetes Element hinzufügen"), um mindestens eine untergeordnete Eigenschaft hinzuzufügen.</p>
  <dd>
  <ol>
    <li>Wählen Sie die Registerkarte **Manuell** aus.</li>
    <li>Definieren Sie folgende Eigenschaftsdetails:
    <ul>  
      <li>Name - Beschreibender Name der Eigenschaft, der in Dashboards, Menüs und Assistenten von {{site.data.keyword.iot_short}} verwendet wird.</li>
      <li>Datentyp - Der Datentyp der Eigenschaft:  
   `String`, `Integer`, `Float` oder `Parent`.</li>
   <!--<li>Event - A specific event to collect data for. Leave blank to collect for all events.</li>-->
   <li>Eigenschaft - Die Eigenschafts-ID, zum Beispiel:  
 `temp` oder `speed`  </br> Informationen dazu, wie Eigenschaften aus den Gerätenachrichten ermittelt werden, finden Sie in [Eigenschaften für Ihre Geräte angeben](#identify-datapoints "Eigenschaften angeben.").</li>
  <li>Dateneinheit - Optional: Die Einheit für die Daten der Eigenschaft. Beispiel:  
     `C` oder `Mph`  </li>
     <li> Dezimalstellen - Optional, nur Gleitkommawert: Die Anzahl der in die Gerätedaten einzuschließenden Dezimalstellen.</li>
    </ul>
    </li>
    <li>Klicken Sie auf **Fertigstellen**, um die Eigenschaft zu erstellen.</li>
  </ol>
  </dd>
  <dt>Virtuelle Eigenschaft erstellen</dt>
  <dd> Wenn die Geräteeigenschaft 'temp' beispielsweise einen Temperaturwert in Fahrenheit zurückgibt und Sie stattdessen Celsius verwenden möchten, können Sie die virtuelle Eigenschaft *temp_c* erstellen, die die Funktion *temp_c=(temp-32)/1,8* aufweist. Sie können in Ihren Regelbedingungen statt der echtzeitorientierten Eigenschaft *temp* anschließend die virtuelle Eigenschaft *temp_c* verwenden.  
  Gehen Sie wie folgt vor, um eine virtuelle Eigenschaft zu erstellen:
  <ol>
    <li>Wählen Sie die Registerkarte **Virtuelle Eigenschaft** aus.</li>  
    <li>Definieren Sie folgende Eigenschaftsdetails:
    <ul>
    <li>Name - Beschreibender Name der Eigenschaft, der in Dashboards, Menüs und Assistenten von {{site.data.keyword.iot_short}} verwendet wird.</li>
    <li>Datentyp - Der Datentyp der Eigenschaft:  
 `Float` oder `Integer`.</li>
 <li>Eigenschaft - Eigenschafts-ID für die virtuelle Eigenschaft. Beispiel:  
`temp_virt`</li>
    <li>Berechnung - Fügen Sie mindestens eine Komponente hinzu, um eine gültige Funktion zu definieren. Sie können Eigenschaften, numerische Werte und mathematische Operatoren wie +, -, \*, /, ( und ) verwenden.  
    Klicken Sie auf **Erweitert**, um eine Gruppe mit Formeln aufzurufen, die für Datenpunktreihen auf Edge-Geräten verwendet werden können. Weitere Informationen zu den erweiterten Formeln finden Sie in [Erweiterte Berechnungen für virtuelle Edge-Eigenschaften](im_vir_calculations.html).  
    **Wichtig:** Regelbedingungen zum Vergleichen virtueller Eigenschaften auf der Basis erweiterter Formeln werden nicht unterstützt.</li>
    <li>Dateneinheit - Optional: Die Einheit für die Daten der Eigenschaft. Beispiel: `C` oder `Mph`</li>
    <li> Dezimalstellen - Optional, nur Gleitkommawert: Die Anzahl der in die Gerätedaten einzuschließenden Dezimalstellen.</li>
   </ul>
   </li>
   <li>Klicken Sie auf **Fertigstellen**, um die Eigenschaft zu erstellen.</li>
  </ol>
  </dd>
  <dt>Eigenschaften von einem verbundenen Gerät auswählen</dt>
  <dd>
  <ol>
    <li>Wählen Sie die Registerkarte **Von verbundenen Geräten** aus.</li>  
    <li>Wählen Sie mindestens eine Eigenschaft aus, die dem Schema hinzugefügt werden soll. Diese Eigenschaften können später bearbeitet werden, um Attribute wie beispielsweise Name und Dateneinheit festzulegen.  
<!--**Important:** Each property must be unique for a schema. If you select multiple occurrences of the same property for different events, only one of the selected properties is added to the schema.</li>-->
  <li>Klicken Sie auf **OK**, um die Eigenschaften zu erstellen.</li>
  </ol>
  </dd>
    <dd>Die erstellten Eigenschaften werden hinzugefügt und als Beschreibung wird der Name der Eigenschaft ausgewählt. Klicken Sie zum Bearbeiten der Eigenschaft in der Liste auf die Eigenschaft und geben Sie zusätzliche Attribute an, wie beispielsweise Sensortyp, Datentyp und Anzahl der Dezimalstellen.</dd>
  </dl>
8. Klicken Sie auf **Fertigstellen**, um das Nachrichtenschema zu erstellen.

## Eigenschaften für Ihre Geräte angeben
{: #identify-datapoints}
   Die Eigenschaften für ein Gerät finden Sie im {{site.data.keyword.iot_short}}-Dashboard.

1. Wechseln Sie im {{site.data.keyword.iot_short}}-Dashboard zu **Geräte**.
2. Klicken Sie auf ein Gerät, um eine Seite zu öffnen, die Details zum Gerät anzeigt.
3. Blättern Sie abwärts zum Abschnitt **Sensorinformationen**, um eine Liste der verfügbaren Eigenschaften für ein verbundenes Gerät anzuzeigen.
