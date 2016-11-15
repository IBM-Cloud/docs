---

copyright:
  years: 2016

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}

# Beispiel 'Sensor für mobiles Gerät'

Im Beispiel 'Sensor für mobiles Gerät' wird JavaScript verwendet, um Ihr Telefon mit {{site.data.keyword.iot_full}} zu verbinden und Sensordaten in Ihrer {{site.data.keyword.iot_short}}-Organisation zu publizieren.
{:shortdesc}

Die {{site.data.keyword.iot_short}}-Python-Clientbibliothek wird verwendet, um Befehle zu subskribieren und die von Ihrem Telefon publizierten Sensordaten zu visualisieren. Die Datenvisualisierung wird auf einer Webseite dargestellt, die in das Web Server Gateway Interface-Framework (WSGI) integriert ist.

Diese Anwendung demonstriert eine Methode, mit der der Zugriff des Benutzers auf Sensordaten von bestimmten Geräten gesteuert werden kann. Beim Klicken auf die Option für **Starten** (Let's Play) erstellt die Anwendung einen Benutzerdatensatz in einer {{site.data.keyword.cloudantfull}}-Datenbank und ruft die {{site.data.keyword.iot_short}}-Gerätemanagement-API auf, um das Gerät zu registrieren.

## Voraussetzungen

Vor dem Implementieren dieses Beispiels:

- Erstellen Sie ein {{site.data.keyword.bluemix_notm}}-Konto und melden Sie sich an. Weitere Informationen zu {{site.data.keyword.bluemix_notm}} finden Sie in [Kostenlose Testversion starten](https://apps.admin.ibmcloud.com/manage/trial/bluemix.html).
- Laden Sie die Cloud Foundry-Befehlszeilenschnittstelle herunter und installieren Sie sie. Die Cloud Foundry-Befehlszeilenschnittstelle ermöglicht Ihnen, Serviceinstanzen zu ändern und in {{site.data.keyword.bluemix_notm}} zu implementieren. Weitere Informationen finden Sie in [Codierung mit der cf-Befehlszeilenschnittstelle beginnen](https://www.ng.bluemix.net/docs/#starters/install_cli.html)

## Dieses Beispiel implementieren

Zum Implementieren Ihrer eigenen Kopie dieses Beispiels in {{site.data.keyword.bluemix_notm}} verwenden Sie folgende Schritte:

1. Erstellen Sie in {{site.data.keyword.bluemix_notm}} eine neue Python-Anwendung.
  a. Klicken Sie in Ihrem {{site.data.keyword.bluemix_notm}}-Dashboard auf **App erstellen** und klicken Sie anschließend auf **Web**.
  b. Wählen Sie die Option für **Python** aus und klicken Sie auf **Weiter**.
  c. Wählen Sie einen Anwendungsnamen aus und klicken Sie auf **Fertigstellen**.
  Ihre Python-Anwendung wird nun schrittweise ausgeführt.
2. Erstellen Sie eine Instanz des {{site.data.keyword.cloudant_short_notm}} NoSQL DB-Service.
  a. Klicken Sie in Ihrem {{site.data.keyword.bluemix_notm}}-Dashboard auf **Services oder APIs verwenden**.
  b. Wählen Sie die Option für **Daten und Analyse** aus und klicken Sie anschließend auf die Option für **Cloudant NoSQL DB**.
  c. Klicken Sie auf **Erstellen**.
3. Binden Sie Ihre Instanz von {{site.data.keyword.cloudant_short_notm}} NoSQL DB und Ihre Instanz von {{site.data.keyword.iot_short}} an Ihre Python-Anwendung.
  a. Klicken Sie auf **Service oder API binden**.
  b. Wählen Sie Ihren {{site.data.keyword.cloudant_short_notm}} NoSQL DB-Service und Ihre {{site.data.keyword.iot_short}}-Instanz aus und klicken Sie auf **Hinzufügen**.
4. Klonen Sie das [{{site.data.keyword.iot_short}}-Python-Github-Repository](https://github.com/ibm-messaging/iot-python.git). Zum Klonen des Repositorys über eine Befehlszeilenschnittstelle navigieren Sie zu dem Verzeichnis, das das Ziel des Klonvorgangs für das Repository sein soll, und führen Sie folgenden Befehl aus:
```
$ git clone https://github.com/ibm-messaging/iot-python.git
```
5. Wechseln Sie in der Befehlszeilenschnittstelle mithilfe des folgenden Befehls von Ihrem Verzeichnis zum Beispiel 'Sensor für mobiles Gerät':
```
$ cd iot-python/samples/bluemixZoneDemo
```
6. Führen Sie für Ihre Anwendung mithilfe des folgenden Befehls eine Push-Operation mit dem Ziel {{site.data.keyword.bluemix_notm}} durch, indem Sie `app_name` durch den Namen Ihrer Python-Anwendung ersetzen:
```
$ cf push app_name -m 32M -b https://github.com/cloudfoundry/cf-buildpack-python.git -c "python server.py"
```
7. Öffnen Sie `http://app_name.mybluemix.net/` in einem Web-Browser auf Ihrem Telefon. Folgende Seite sollte angezeigt werden: 

Es wird eine Seite angezeigt, die darstellt, wie die Daten des Beschleunigungssensors mithilfe des MQTT-Messagings von Ihrem Telefon an
<keyword conref="cloudoeconrefs.dita#cloudoeconrefs/iot_short"/> gesendet werden, und wie eine
<keyword conref="cloudoeconrefs.dita#cloudoeconrefs/bluemix_short"/> -App diese Daten zum Spiegeln Ihrer Bewegungen verwendet.
Geben Sie Ihre Geräte-ID ein, klicken Sie auf <uicontrol>Verbindung herstellen</uicontrol> und versuchen Sie nun weiterhin, Ihr Telefon zu bewegen.
