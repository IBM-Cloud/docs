---

copyright:
  years: 2016, 2017
lastupdated:  "2016-08-03"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Wartung und Aktualisierungen
{: #maintupdates_mf}

{{site.data.keyword.mobilefoundation_short}} stellt einen {{site.data.keyword.mfserver_short_notm}}<!-- on {{site.data.keyword.containerlong}} as a container group--> bereit. Die Benutzer werden über Aktualisierungen des {{site.data.keyword.mobilefoundation_short}}-Servers benachrichtigt. Wenn es für Sie hilfreich ist, können Sie den {{site.data.keyword.mobilefoundation_short}}-Server aktualisieren.
{:shortdesc}

## Strategie für die Wartung
{: #maintupdate_strategy_mf}

Wenn eine Aktualisierung für {{site.data.keyword.mobilefoundation_short}} verfügbar ist, wird der Benutzer über die Verfügbarkeit der Aktualisierung benachrichtigt.  Die Benachrichtigung wird im Dashboard der Serviceinstanz angezeigt. Der Benutzer kann die Aktualisierung für {{site.data.keyword.mobilefoundation_short}} in einem von ihm festgelegten Wartungsfenster ausführen.

Die {{site.data.keyword.mobilefoundation_short}}-Serviceaktualisierung steht zur Verfügung, wenn eine der folgenden Komponenten aktualisiert ist.

* {{site.data.keyword.mfserver_short_notm}}.
* Zugrunde liegende Liberty-Version.
* Zugrunde liegende Java Developer Kit-Version.


## Aktualisierungen anwenden
{: #apply_update_mf}

Die Aktualisierung für {{site.data.keyword.mobilefoundation_short}} kann durch Klicken auf die Option für die Neuerstellung angewendet werden.

Bei der Anwendung der Aktualisierung wird die Version des Servers, die in der {{site.data.keyword.mfp_oc_short_notm}} zu sehen ist, so geändert, dass die Version der Serveraktualisierung angezeigt wird.

### Hinweis:
{: #note notoc}

* Benutzer können keine eigenen Fixes und Aktualisierungen auf ihre Instanz des {{site.data.keyword.mobilefoundation_short}}-Service anwenden.
* Informationen zu den Unterschieden im Verhalten der Pläne, wenn Sie auf die Option für die Neuerstellung klicken, Sie in den Themen zur [Erneuten Erstellung des Servers im Entwicklerplan](c_using_mfs_p1.html#recreate_mobilefoundation_p1) sowie zur [Erneuten Erstellung des Servers im Professional 1 Application-Plan](c_using_mfs_p2.html#recreate_mobilefoundation_p2).
