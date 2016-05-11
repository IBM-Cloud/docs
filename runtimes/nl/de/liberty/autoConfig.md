---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Automatische Konfiguration gebundener Services
{: #auto_config}

*Letzte Aktualisierung: 31. März 2016*

An die Liberty-Anwendung können verschiedene Services gebunden werden. Abhängig von den Vorgaben des Entwicklers können Services containerverwaltet und/oder anwendungsverwaltet sein.

Ein anwendungsverwalteter Service ist ein Service, der ohne Unterstützung von Liberty vollständig von der Anwendung verwaltet wird. Die Anwendung liest in der Regel VCAP_SERVICES, um Informationen zu dem gebundenen Service abzurufen, und greift direkt auf den Service zu. Die Anwendung stellt den gesamten erforderlichen Clientzugriffscode bereit. Es besteht keine Abhängigkeit von Liberty-Features oder der Konfiguration der Datei 'server.xml'. Die automatische Konfiguration des Liberty-Buildpacks wird auf Services dieses Typs nicht angewendet.

Ein containerverwalteter Service ist ein Service, der von der Liberty-Laufzeit verwaltet wird. In manchen Fällen kann es vorkommen, dass die Anwendung den gebundenen Service in JNDI sucht, während der Service in anderen Fällen direkt von Liberty selbst genutzt wird. Das Liberty-Buildpack liest VCAP_SERVICES, um Informationen zu den gebundenen Services zu erhalten. Für jeden containerverwalteten Service führt das Buildpack die folgenden drei Funktionen aus:

* Generieren von [Cloudvariablen](optionsForPushing.html#accessing_info_of_bound_services) für den gebundenen Service.
* Installieren der Liberty-Features und des Clientzugriffscodes, die für den Zugriff auf den gebundenen Service erforderlich sind.
* Generieren oder Aktualisieren der Zeilengruppen der Datei 'server.xml', die für den Service erforderlich sind.

Dieser Prozess wird als automatische Konfiguration bezeichnet.
Das Liberty-Buildpack bietet automatische Konfiguration für die folgenden Servicetypen:

* [SQL Database](../../services/SQLDB/index.html#SQLDB)
* ClearDB MySQL Database
* [MySQL](../../services/MySQL/index.html#MySQL)
* ElephantSQL
* [PostgreSQL](../../services/PostgreSQL/index.html#PostgreSQL)
* [Cloudant NoSQL Database](../../services/Cloudant/index.html#Cloudant)
* MongoLab
* [dashDB](../../services/dashDB/index.html#dashDB)
* [Data Cache](../../services/DataCache/index.html#data_cache)
* [Session Cache](../../services/SessionCache/index.html#session_cache)
* [MQ Light](../../services/MQLight/index.html#mqlight010)
* [Monitoring and Analytics](../..//services/monana/index.html#gettingstartedtemplate)
* [Auto-Scaling](../../services/Auto-Scaling/index.html#autoscaling)
* [Single Sign On](../../services/SingleSignOn/index.html#sso_gettingstarted)
* [New Relic](newRelic.html)
* [Dynatrace](dynatrace.html)

Wie bereits erwähnt können manche Services anwendungsverwaltet oder containerverwaltet sein. Mongo und SQLDB sind Beispiele für solche Services. Das Liberty-Buildpack geht standardmäßig davon aus, dass diese Services containerverwaltet sind und konfiguriert sie automatisch. Wenn die Anwendung den Service verwalten soll, können Sie die automatische Konfiguration für den Service ausschließen (Opt-out), indem Sie die Umgebungsvariable 'services_autoconfig_excludes' definieren. Weitere Informationen finden Sie in [Automatische Konfiguration von Services ausschließen](autoConfig.html#opting_out).

## Installation von Liberty-Features und Clientzugriffscode
{: #installation_of_liberty_features}

Bei der Bindung an einen containerverwalteten Service müssen möglicherweise Liberty-Features in der Zeilengruppe 'featureManager' der Datei 'server.xml' konfiguriert werden. Das Liberty-Buildpack nimmt eine entsprechende Aktualisierung der Zeilengruppe 'featureManager' vor und installiert die erforderlichen unterstützenden Binärdateien. Wenn der Service Clienttreiber-JAR-Dateien benötigt, werden die JAR-Dateien an eine bekannte Position in der Liberty-Installation heruntergeladen.

Weitere Einzelheiten finden Sie in der Dokumentation zum gebundenen Servicetyp.

## Konfigurationszeilengruppen der Datei 'server.xml' generieren oder aktualisieren
{: #generating_or_updating_serverxml}

Wenn Sie eine eigenständige Anwendung mit einer Push-Operation übertragen, generiert das Liberty-Buildpack die Zeilengruppe der Datei 'server.xml' für Bluemix, wie in [Optionen zur Durchführung von Push-Operationen für Liberty-Anwendungen](optionsForPushing.html#options_for_pushing) beschrieben. Wenn Sie eine eigenständige Anwendung mit einer Push-Operation übertragen und an containerverwaltete Services binden, generiert das Liberty-Buildpack die erforderlichen Zeilengruppen der Datei 'server.xml' für die gebundenen Services.

Bei Angabe einer Datei 'server.xml' und der Bindung an containerverwaltete Services führt das Liberty-Buildpack die folgenden Aktionen aus:

* Es generiert die Konfiguration für die gebundenen Services, wenn die angegebene Datei 'server.xml' keine Konfigurationszeilengruppen für die gebundenen Services enthält.
* Es aktualisiert die Konfiguration für die gebundenen Services, wenn die angegebene Datei 'server.xml' Konfigurationszeilengruppen für die gebundenen Services enthält.

Weitere Einzelheiten finden Sie in der Dokumentation zum gebundenen Servicetyp.

## Automatische Konfiguration von Services ausschließen
{: #opting_out}

In manchen Fällen soll das Liberty-Buildpack die gebundenen Services vielleicht nicht automatisch konfigurieren. Betrachten Sie die folgenden Szenarios:

* Eine Anwendung verwendet MongoDB, die Verbindung zur Datenbank soll aber von der Anwendung direkt verwaltet werden. Die Anwendung enthält die erforderliche Clienttreiber-JAR-Datei. Das Liberty-Buildpack soll den Mongo-Service nicht automatisch konfigurieren.
* Der Benutzer gibt die Datei 'server.xml' und die Konfigurationszeilengruppen für die SQLDB-Instanz an, da eine vom Standard abweichende Datenquellenkonfiguration erforderlich ist. Das Liberty-Buildpack soll die Datei 'server.xml' zwar nicht aktualisieren, aber dennoch sicherstellen, dass die entsprechende unterstützende Software installiert wird.

Sie können die automatische Servicekonfiguration über die Umgebungsvariable 'services_autoconfig_excludes' ausschließen. Diese Umgebungsvariable kann in eine Datei 'manifest.yml' eingefügt oder mit dem cf-Client definiert werden.

Das Ausschließen der automatischen Konfiguration kann pro Servicetyp erfolgen. Sie können die Konfiguration entweder vollständig (siehe Mongo-Szenario) oder nur die Konfigurationsaktualisierungen für die Datei 'server.xml' (siehe SQLDB-Szenario) ausschließen. Der Wert, den Sie für die Umgebungsvariable 'services_autoconfig_excludes' angeben, ist eine Zeichenfolge, für die Folgendes gilt:

* Die Zeichenfolge kann Opt-out-Spezifikationen für einen oder mehrere Services enthalten.
* Die Opt-out-Spezifikation für einen bestimmten Service lautet 'service_type=option'. Dabei gilt Folgendes:
  * 'service_type' ist die Bezeichnung für den Service gemäß VCAP_SERVICES.
  * Die Option lautet entweder 'all' oder 'config'.
* Wenn die Zeichenfolge eine Opt-out-Spezifikation für mehrere Services enthält, müssen die einzelnen Opt-out-Spezifikationen durch ein einzelnes Leerzeichen voneinander getrennt werden.

Formal sieht die Syntax der Zeichenfolge wie folgt aus.

```
    Opt-out-Zeichenfolge :: <Spezifikation_des_Servicetyps<Begrenzer>Spezifikation_des_Servicetyps]*
    <Spezifikation_des_Servicetyps> :: <Servicetyp>=<option>
    <Servicetyp> :: Servicetyp (Servicebezeichnung gemäß VCAP_SERVICES)
    <option> :: all | config
    <Begrenzer> :: ein Leerzeichen
```
{: #codeblock}

**Wichtig**: Der angegebene Servicetyp muss mit der in der Umgebungsvariablen VCAP_SERVICES enthaltenen Servicebezeichnung übereinstimmen. Leerzeichen sind nicht zulässig.
**Wichtig**: Innerhalb von <Spezifikation_des_Servicetyps> ist kein Leerzeichen zulässig. Leerzeichen dürfen nur verwendet werden, um mehrere Vorkommen von <Spezifikation_des_Servicetyps> voneinander zu trennen.

Über die Option "all" können alle automatischen Konfigurationsaktionen für einen Service ausgeschlossen werden (siehe Mongo-Szenario oben). Über die Option "config" können Sie angeben, dass nur die Konfigurationsaktualisierungsaktionen ausgeschlossen werden sollen (siehe SQLDB-Szenario oben).

Beispiele für Opt-out-Spezifikationen in der Datei 'manifest.yml' für das Mongo- und das SQLDB-Szenario.

```
    env:
      services_autoconfig_excludes: mongodb-2.2=all

    env:
      services_autoconfig_excludes: sqldb=config

    env:
      services_autoconfig_excludes: sqldb=config mongodb-2.2=all
```
{: #codeblock}

Beispiele für die Konfiguration der Umgebungsvariablen 'services_autoconfig_excludes' für die Anwendung 'myapp' über die Befehlszeilenschnittstelle:

```
    $ cf set-env myapp services_autoconfig_excludes sqldb=config
    $ cf set-env myapp services_autoconfig_excludes "sqldb=config mongodb-2.2=all"
```
{: #codeblock}

# Zugehörige Links
## Allgemein
* [Liberty-Laufzeit](index.html)
* [Übersicht über das Liberty-Profil](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
