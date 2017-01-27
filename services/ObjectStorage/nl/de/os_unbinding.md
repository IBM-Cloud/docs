---

copyright:
  years: 2014, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Bindung und Bereitstellung der {{site.data.keyword.objectstorageshort}}-Instanz aufheben {: #deprovisioning-object-storage}

Wenn der {{site.data.keyword.objectstorageshort}}-Service an Ihre Cloud Foundry-App gebunden ist, Sie jedoch keinen Speicher mehr benötigen, können Sie die Bindung und die Bereitstellung für die Instanz aufheben.
{: shortdesc}


## Bindung der Instanz aufheben

Sie können Ihre gespeicherten Daten beibehalten und die Bindung des Service zur Cloud Foundry-App aufheben. Das {{site.data.keyword.objectstorageshort}}-Konto wird erst gelöscht, wenn die Bereitstellung des Service aufgehoben wird.

**Achtung**: Wenn Sie die Bindung einer {{site.data.keyword.objectstorageshort}}-Instanz an eine {{site.data.keyword.Bluemix_notm}}-Anwendung aufheben oder den Serviceschlüssel löschen, werden alle Ihre Berechtigungsnachweise für diese Instanz gelöscht und können nicht mehr wiederhergestellt werden. Sie können neue Cloudberechtigungsnachweise durch erneutes Binden der Instanz oder durch Erstellen eines neuen Serviceschlüssels generieren.

1. Um die an Ihre App gebundenen Services anzuzeigen, klicken Sie in Ihrer Cloud Foundry-Anwendung auf die Registerkarte 'Verbindungen'.
2. Suchen Sie den Service, dessen Bindung Sie aufheben möchten, und klicken Sie auf der Servicekachel auf die Menüschaltfläche.
3. Wählen Sie **Bindung für Service aufheben** aus.
4. Wählen Sie die Option **Serviceinstanz löschen** ab und klicken Sie auf **OK**.
5. Klicken Sie auf die Option für ein erneutes Staging, damit Ihre Änderung wirksam wird.



## Bereitstellung der Instanz aufheben

Wenn Sie über eine Instanz von {{site.data.keyword.objectstorageshort}} verfügen, die Sie nicht mehr benötigen, können Sie die Instanz löschen.

**Achtung**: Wenn Sie die Bereitstellung einer {{site.data.keyword.objectstorageshort}}-Instanz aufheben, werden das Cloudprojekt und das Swift-Konto gelöscht. Alle Container und Objekte in der Instanz, deren Bereitstellung aufgehoben wurde, werden gelöscht und können nicht wiederhergestellt werden.

1. Um die an Ihre App gebundenen Services anzuzeigen, klicken Sie in Ihrer Cloud Foundry-Anwendung auf die Registerkarte 'Verbindungen'.
2. Suchen Sie den Service, dessen Bereitstellung Sie aufheben möchten, und klicken Sie auf der Servicekachel auf die Menüschaltfläche.
3. Wählen Sie **Service löschen** aus.
4. Klicken Sie zur Bestätigung auf **Löschen**.
5. Klicken Sie auf die Option für ein erneutes Staging, damit Ihre Änderung wirksam wird.
