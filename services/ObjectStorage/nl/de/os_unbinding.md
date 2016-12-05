---

copyright:
  years: 2014, 2016
lastupdated: "2016-11-04"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Bindung und Bereitstellung der {{site.data.keyword.objectstorageshort}}-Instanz aufheben {: #deprovisioning-object-storage}



### Bindung der Instanz aufheben
Wenn Sie {{site.data.keyword.objectstorageshort}} in Ihrer Cloud Foundry-App nicht mehr benötigen, jedoch Ihre gespeicherten Daten beibehalten möchten, können Sie die Bindung Ihrer Instanz des Service zu Ihrer App aufheben.

**Achtung**: Wenn Sie die Bindung einer {{site.data.keyword.objectstorageshort}}-Instanz an eine {{site.data.keyword.Bluemix_notm}}-Anwendung aufheben oder den Serviceschlüssel löschen, werden alle Ihre Berechtigungsnachweise für diese Instanz gelöscht und können nicht mehr wiederhergestellt werden. Das {{site.data.keyword.objectstorageshort}}-Konto wird erst gelöscht, wenn die Bereitstellung der {{site.data.keyword.objectstorageshort}}-Instanz aufgehoben wird. Sie können neue Cloudberechtigungsnachweise durch erneutes Binden oder Erstellen eines neuen Serviceschlüssels generieren.

1. Um die an Ihre App gebundenen Services anzuzeigen, klicken Sie in Ihrer Cloud Foundry-Anwendung auf die Registerkarte 'Verbindungen'.
2. Suchen Sie den Service, dessen Bindung Sie aufheben möchten, und klicken Sie auf der Servicekachel auf die Menüschaltfläche.
3. Wählen Sie **Bindung für Service aufheben** aus.
4. Nehmen Sie die Auswahl für **Serviceinstanz löschen** zurück und klicken Sie auf **OK**.
5. Klicken Sie auf die Option für ein erneutes Staging, damit Ihre Änderung wirksam wird.



### Bereitstellung der Instanz aufheben

Wenn Sie über eine nicht gebundene Instanz von {{site.data.keyword.objectstorageshort}} verfügen, die Sie nicht mehr benötigen, können Sie die Instanz löschen.

**Achtung**: Wenn Sie die Bereitstellung einer {{site.data.keyword.objectstorageshort}}-Instanz aufheben, werden das Cloudprojekt und das Swift-Konto gelöscht. Alle Container und Objekte in der Instanz, deren Bereitstellung aufgehoben wurde, werden gelöscht und können nicht wiederhergestellt werden.

1. Um die an Ihre App gebundenen Services anzuzeigen, klicken Sie in Ihrer Cloud Foundry-Anwendung auf die Registerkarte 'Verbindungen'.
2. Suchen Sie den Service, dessen Bindung Sie aufheben möchten, und klicken Sie auf der Servicekachel auf die Menüschaltfläche.
3. Wählen Sie **Service löschen** aus.
4. Klicken Sie zur Bestätigung auf **Löschen**.
5. Klicken Sie auf die Option für ein erneutes Staging, damit Ihre Änderung wirksam wird.
