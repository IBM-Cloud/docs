---

copyright:
  years: 2015, 2016

---


{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}

# Fehlerbehebung für SendGrid
{: #ts_sendgrid}

*Letzte Aktualisierung: 9. Dezember 2015*

Hier finden Sie die Antwort auf eine Frage zur Verwendung von SendGrid in {{site.data.keyword.Bluemix}}.
{:shortdesc}


## E-Mails können nicht mithilfe von SendGrid gesendet werden
{: #ts_sendgrid_email}

Wenn Sie E-Mails nicht mithilfe des Service SendGrid senden können, haben Sie möglicherweise den Grenzwert für die pro Serviceinstanz zu sendenden E-Mails erreicht.
{:shortdesc}


Nach dem Senden der maximal zulässigen Anzahl E-Mails können Sie den Service SendGrid nicht mehr zum Senden weiterer E-Mails verwenden.
{: tsSymptoms}


Wenn Sie E-Mails mithilfe des Service SendGrid senden, sind Sie auf den Versand von 25.000 E-Mails pro Serviceinstanz monatlich beschränkt. Nach dem Erreichen dieses Grenzwerts stoppt SendGrid den Versand von E-Mails und weitere Gebühren für das Aufrufen dieses Service werden nicht erhoben.
{: tsCauses}

Zum Überprüfen, wie hoch die Anzahl der noch für den Versand zulässigen E-Mails ist, klicken Sie im {{site.data.keyword.Bluemix_notm}}-Dashboard auf Ihre SendGrid-Serviceinstanz und klicken Sie anschließend auf die Option zum Öffnen des SendGrid-Dashboards. Im Feld für das verbleibende Guthaben wird die Anzahl angezeigt.


Wenn Sie nach dem Erreichen des Grenzwerts von 25.000 E-Mails pro Serviceinstanz monatlich weitere E-Mails senden wollen, können Sie eine weitere Serviceinstanz hinzufügen. Weitere Informationen zu SendGrid finden Sie unter [Getting Started with SendGrid](https://sendgrid.com/docs/index.html){: new_window}.    
{: tsResolve}

