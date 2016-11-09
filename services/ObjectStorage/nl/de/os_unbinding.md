---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Bindung und Bereitstellung der {{site.data.keyword.objectstorageshort}}-Instanz aufheben{: #deprovisioning-object-storage}

*Letzte Aktualisierung: 19. Oktober 2016*
{: .last-updated}


### Bindung der Instanz aufheben
Wenn Sie {{site.data.keyword.objectstorageshort}} in Ihrer Cloud Foundry-App nicht mehr benötigen, jedoch Ihre gespeicherten Daten beibehalten möchten, können Sie die Bindung Ihrer Instanz des Service zu Ihrer App aufheben.

**Achtung**: Wenn Sie die Bindung einer {{site.data.keyword.objectstorageshort}}-Instanz an eine {{site.data.keyword.Bluemix_notm}}-Anwendung aufheben oder den Serviceschlüssel löschen, werden alle Ihre Berechtigungsnachweise für diese Instanz gelöscht und können nicht mehr wiederhergestellt werden.

1. Öffnen Sie die Details zu Ihrer App in der {{site.data.keyword.Bluemix_notm}}-Konsole.
2. Wählen Sie Ihre {{site.data.keyword.objectstorageshort}}-Instanz aus und klicken Sie auf **Bindung für Service aufheben**.
3. Klicken Sie auf **ENTFERNEN**.
4. Klicken Sie auf **ERNEUTES STAGING**.



### Bereitstellung der Instanz aufheben

Wenn Sie über eine nicht gebundene Instanz von {{site.data.keyword.objectstorageshort}} verfügen, die Sie nicht mehr benötigen, können Sie die Instanz löschen.

**Achtung**: Wenn Sie die Bereitstellung einer {{site.data.keyword.objectstorageshort}}-Instanz aufheben, wird das Cloudprojekt gelöscht. Alle Container und Objekte in der Instanz, deren Bereitstellung aufgehoben wurde, werden gelöscht und können nicht wiederhergestellt werden.

1. Öffnen Sie die Details zu Ihrer App in der {{site.data.keyword.Bluemix_notm}}-Konsole.
2. Wählen Sie Ihre {{site.data.keyword.objectstorageshort}}-Instanz aus und klicken Sie auf **Löschen**.
3. Klicken Sie auf **ERNEUTES STAGING**.
