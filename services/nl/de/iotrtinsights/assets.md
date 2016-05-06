---

copyright:
  years: 2015,2016

---

{:shortdesc: .shortdesc}

# Assets verwalten{: #manage-assets}

Eine der Stärken von {{site.data.keyword.iotrtinsights_full}} liegt darin, dass Sie Ihre Geräte Ihren verwalteten Assets zuordnen können und Regeln erstellen können, die auf alle Geräte angewendet werden, die einem Asset zugeordnet sind.
{: shortdesc}

Ein einzelnes Asset, das Sie überwachen wollen, könnte zum Beispiel mehrere Geräte und eine große Anzahl an Sensoren umfassen. 

>**Tipp:** Sie können die Zuordnungsprozedur wiederholen, wenn Ihre Assets aktualisiert oder geändert werden. Über den Parameter `action` in den Kontext- und Zuordnungsdateien können Sie Assets und Geräte hinzufügen und entfernen.
Gehen Sie wie folgt vor, um Ihre Geräten Ihren Assets zuzuordnen: 
1. Erstellen Sie eine Liste mit Assets und speichern Sie diese als CSV-Datei.
Diese Datei umfasst Assetdaten von Ihrer Asset-Management-Software.
Beispieldateiformat:
```
ASSETNUM,ASSETTYPE,AS_DESCRIPTION,AS_DESCRIPTION_LD,INSTALLDATE,AS_ITEMNUM,AS_ITEMSETID,AS_LOCATION,PRIORITY,PURCHASEPRICE,REPLACECOST,SERIALNUM,AS_SITEID,AS_STATUS,ACTION  
5001,FACILITIES,New Asset 1,,2015-03-16,1001,ITEMSET,CONFRMA1,1,1000,1200,123451,MYSITE,OPERATING,+    
5002,FACILITIES2,New Asset 2,,2015-03-16,1001,ITEMSET,CONFRMA1,1,1000,1200,123452,MYSITE,OPERATING,+
```
{: codeblock}

  Dabei gilt Folgendes:  
  - ASSETNUM - **Erforderlich:** Die Asset-ID-Nummer in Ihrem System. (12)
  - ASSETTYPE - Der Typ des Assets. (15)
  - AS_DESCRIPTION - Eine Kurzbeschreibung des Assets. (100)
  - AS_DESCRIPTION_LD - Eine komplette Beschreibung des Assets. (32.000)
  - INSTALLDATE - (Datum im Format jjjj-MM-tt) Das Datum, an dem das Asset installiert wurde. 
  - AS_ITEMNUM - Die Nummer eines zugehörigen Elements für das Asset. (30)
  - AS_ITEMSETID - Die Nummer der Elementgruppe für das Asset. (8)
  - AS_LOCATION - Die Position des Assets. (12)
  - PRIORITY - (Ganze Zahl) DIe Assetpriorität. (12)
  - PURCHASEPRICE - (Dezimalzahl) Der Kaufpreis des Assets. (10,2)
  - REPLACECOST - (Dezimalzahl) Die Kosten für den Ersatz des Assets. (10,2)
  - SERIALNUM - Die Seriennummer des Assets. (64)
  - AS_SITEID - Die ID des Standorts, an dem das Asset installiert ist. (8)
  - AS_STATUS - Der Status des Assets. (20)
  - ACTION - Ein Plussymbol (`+`) bedeutet, dass das Asset hinzugefügt wurde, und ein Minussymbol (`-`) bedeutet, dass das Asset entfernt wurde.   
  >**Tipp:** Die Zahl in Klammern gibt die maximale Länge der Zeichenfolge an. Sofern nicht anders angegeben, werden die Parameter als alphanumerische Zeichen in Groß-/Kleinschreibung eingegeben.
5. Erstellen Sie eine Zuordnungsliste für Assets und Geräte und speichern Sie diese als CSV-Datei. Mithilfe dieser Datei werden die importierten Assets in der Assetliste Ihren {{site.data.keyword.iot_short}}-Geräten zugeordnet. Beispieldateiformat:
```
  sourceType,sourceId,targetType,targetId,action  
  d:orgid:iot-device-type,device001,asset,5001,+  
  d:orgid:iot-device-type,device002,asset,5002,+  
  d:orgid:iot-device-type,device003,asset,5002,+  
  ```
  {: screen}   

  Dabei gilt Folgendes:
    - sourceType - Besteht aus den folgenden {{site.data.keyword.iot_short}}-Daten für Ihr Gerät: 
      - orgid - Ihre {{site.data.keyword.iot_short}}-Organisations-ID
      - iot-device-type - Ihr {{site.data.keyword.iot_short}}-Gerätetyp  
    - sourceID - Ihre {{site.data.keyword.iot_short}}-Geräte-ID  
    - targetType - Verwenden Sie das Wort `asset`, um eine Assetzuordnung zu erstellen 
    - targetID - Der Eintrag ASSETNUM für das Asset aus der Kontextdatei, die Sie erstellt haben
    - action - Ein Plussymbol (`+`) bedeutet, dass das Assest zugeordnet wurde, und ein Minussymbol (`-`) bedeutet, dass das Asset aus der Zuordnung entfernt wurde. 
2. Melden Sie sich bei der {{site.data.keyword.iotrtinsights_short}}-Konsole als Benutzer mit Administratorberechtigung an. 
2. Gehen Sie zu **Geräte > Gerätegruppen verwalten** und klicken Sie auf **Asset importieren**.  
3. Suchen Sie nach der erstellten Assetdatei und wählen Sie diese aus. 
4. Klicken Sie auf ![Symbol 'Erstellen'](images/create.png "Symbol 'Erstellen'"), um die Assetliste zu erstellen. 
3. Suchen Sie nach den Assets und wählen Sie die Assets und die Gerätezuordnungsdatei aus, die Sie erstellt haben. 
4. Klicken Sie auf ![Symbol 'Erstellen'](images/create.png "Symbol 'Erstellen'"), um die Assetliste zu erstellen. 
5. Gehen Sie zu **Geräte > Gerätegruppen verwalten** und klicken Sie auf eines Ihrer Assets, um eine Liste der Geräte anzuzeigen, die Sie dem Asset zugeordnet haben. 
