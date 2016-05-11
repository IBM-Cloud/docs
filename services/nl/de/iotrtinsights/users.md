---

copyright:
  years: 2015,2016

---

{:shortdesc: .shortdesc}

# Benutzer verwalten{: #manage-users}

{{site.data.keyword.iotrtinsights_short}} wurde für die Teamarbeit konzipiert und ermöglicht es Administratoren, weitere Benutzer hinzuzufügen, die auf die {{site.data.keyword.iotrtinsights_short}}-Konsole zugreifen können.
{: shortdesc}

Rollenbeschreibungen:
- Operator
Operatoren melden sich direkt bei der {{site.data.keyword.iotrtinsights_short}}-Konsole an, um den Echtzeitdatenfluss Ihrer Geräte und Gerätegruppen zu überwachen. Operatoren können auch Regeln aktivieren und inaktivieren sowie bearbeitbare Dashboards ändern.   
- Administrator
Außer den Tasks, die ein Operator ausführen kann, können Administratoren Benutzer hinzufügen, Dashboard-Layouts verwalten, Datenquellen hinzufügen und Gerätetypen verwalten.   
- Eigentümer
Die Rolle des Eigentümers wird der IBM ID zugewiesen, die die {{site.data.keyword.iotrtinsights_short}}-Serviceinstanz in Bluemix bereitgestellt hat. Ein Eigentümer hat dieselben Berechtigungen wie ein Administrator, kann aber nicht gelöscht werden. 

Gehen Sie wie folgt vor, um einen neuen Benutzer hinzuzufügen: 
1. Fügen Sie den Benutzer zu {{site.data.keyword.iot_short}} hinzu.  
>**Wichtig:** Wenn Sie einen Benutzer mit Administratorrolle hinzufügen, müssen Sie diesen Benutzer auch zu {{site.data.keyword.iot_short}} hinzufügen.   

  1. Melden Sie sich beim Dashboard des {{site.data.keyword.iot_short}}-Service an, der als Datenquelle für Ihren {{site.data.keyword.iotrtinsights_short}}-Service dient.   
  2. Navigieren Sie zu **Zugriff > Mitglieder** und klicken Sie auf **Mitglieder hinzufügen**. 
  3. Geben Sie die IBM ID für den Benutzer ein, den Sie hinzufügen wollen, und klicken Sie auf **Mitglieder hinzufügen**. 
2. Fügen Sie den Benutzer zu {{site.data.keyword.iotrtinsights_short}} hinzu. 
  1. Melden Sie sich bei der {{site.data.keyword.iotrtinsights_short}}-Konsole als Benutzer mit Administratorrolle oder Eigentümerrolle an. 
  2. Gehen Sie zu **Einrichten > Benutzer verwalten**. 
  3. Klicken Sie auf **Neuen Benutzer hinzufügen**. 
  4. Geben Sie die E-Mail-Adresse des Benutzers ein, den Sie einladen wollen, wählen Sie eine Rolle für den Benutzer aus und klicken Sie auf ![Symbol 'Erstellen'](images/create.png "Symbol 'Erstellen'").
Es wird eine E-Mail mit dem Webkonsolenlink an den Benutzer gesendet. Wenn die E-Mail-Adresse bereits einer IBM ID zugeordnet ist, kann der Benutzer sich anmelden und direkt auf die Konsole zugreifen. Andernfalls wird der Benutzer vor dem Zugriff auf die Konsole aufgefordert, eine kostenlose IBM ID zu erstellen.   
>**Real-Time Insights-Instanz auswählen:** Benutzer, die als Operatoren oder Administratoren auf mehrere Instanzen von Real-Time Insights zugreifen können, können schnell zwischen diesen Instanzen wechseln. Sie können in der Real-Time Insights-Konsole auf ihren Benutzernamen klicken und die Instanz auswählen, auf die sie zugreifen wollen.   
